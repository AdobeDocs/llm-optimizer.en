---
title: Optimize at Edge - Cloudflare (BYOCDN)
description: Learn how to configure Cloudflare BYOCDN for Optimize at Edge in LLM Optimizer.
feature: Opportunities
---

# Cloudflare (BYOCDN)

This configuration routes agentic traffic (requests from AI bots and LLM user agents) to the Edge Optimize backend service (`live.edgeoptimize.net`). Human visitors and SEO bots continue to be served from your origin as usual. To test the configuration, after the setup is complete, look for the header `x-edgeoptimize-request-id` in the response.

**Prerequisites**

Before setting up the Cloudflare Worker routing rules, ensure you have:

* A Cloudflare account with Workers enabled on your domain.
* Access to your domain's DNS settings in Cloudflare.
* Completed the LLM Optimizer onboarding process.
* Completed CDN log forwarding to LLM Optimizer.
* An Edge Optimize API key retrieved from the LLM Optimizer UI.

{{retrieve-byocdn-api-key}}

**How routing works**

When configured correctly, a request to your domain (for example, `www.example.com/page.html`) from an agentic user agent is intercepted by the Cloudflare Worker and routed to the Edge Optimize backend. The backend request includes the required headers.

**Testing the backend request**

You can verify the routing by making a direct request to the Edge Optimize backend.

```
curl -svo /dev/null https://live.edgeoptimize.net/page.html \
  -H 'x-forwarded-host: www.example.com' \
  -H 'x-edgeoptimize-url: /page.html' \
  -H 'x-edgeoptimize-api-key: $EDGE_OPTIMIZE_API_KEY' \
  -H 'x-edgeoptimize-config: LLMCLIENT=TRUE;'
```

**Required Headers**

The following headers must be set on requests to the Edge Optimize backend:

| Header | Description | Example |
|--------|-------------|---------|
| `x-forwarded-host` | The original host of the request. Required for identifying the site domain. | `www.example.com` |
| `x-edgeoptimize-url` | The original URL path and query string of the request. | `/page.html` or `/products?id=123` |
| `x-edgeoptimize-api-key` | The API key provided by Adobe for your domain. | `your-api-key-here` |
| `x-edgeoptimize-config` | Configuration string for cache key differentiation. | `LLMCLIENT=TRUE;` |

**Step 1: Create the Cloudflare Worker**

1. Log in to your Cloudflare dashboard.
2. Navigate to **Workers & Pages** in the sidebar.
3. Click **Create application** and then **Create Worker**.
4. Name your worker (for example, `edge-optimize-router`).
5. Click **Deploy** to create the worker with the default code.

![Cloudflare Workers dashboard](/help/assets/optimize-at-edge/cloudflare-workers-dashboard.png)

**Step 2: Add the Worker code**

After creating the worker, click **Edit code** and replace the default code with the following:

```javascript
/**
 * Edge Optimize BYOCDN - Cloudflare Worker
 *
 * This worker routes requests from agentic bots (AI/LLM user agents) to the
 * Edge Optimize backend service for optimized content delivery.
 *
 * Features:
 * - Routes agentic bot traffic to Edge Optimize backend
 * - Failover to origin on Edge Optimize errors (any 4XX or 5XX errors)
 * - Loop protection to prevent infinite redirects
 * - Human visitors and SEO bots are served from the origin as usual
 */

// List of agentic bot user agents to route to Edge Optimize
const AGENTIC_BOTS = [
  'AdobeEdgeOptimize-AI',
  'ChatGPT-User',
  'GPTBot',
  'OAI-SearchBot',
  'PerplexityBot',
  'Perplexity-User'
];

// Targeted paths for Edge Optimize routing
// Set to null to route all HTML pages, or specify an array of paths
const TARGETED_PATHS = null; // e.g., ['/', '/page.html', '/products']

// Failover configuration
// Failover on any 4XX client error or 5XX server error from Edge Optimize
const FAILOVER_ON_4XX = true; // Failover on any 4XX error (400-499)
const FAILOVER_ON_5XX = true; // Failover on any 5XX error (500-599)

export default {
  async fetch(request, env, ctx) {
    return await handleRequest(request, env, ctx);
  },
};

async function handleRequest(request, env, ctx) {
  const url = new URL(request.url);
  const userAgent = request.headers.get("user-agent")?.toLowerCase() || "";

  // Check if request is already processed (loop protection)
  const isEdgeOptimizeRequest = !!request.headers.get("x-edgeoptimize-request");

  // Construct the original path and query string
  const pathAndQuery = `${url.pathname}${url.search}`;

  // Check if the path matches HTML pages (no extension or .html extension)
  const isHtmlPage = /(?:\/[^./]+|\.html|\/)$/.test(url.pathname);

  // Check if path is in targeted paths (if specified)
  const isTargetedPath = TARGETED_PATHS === null
    ? isHtmlPage
    : (isHtmlPage && TARGETED_PATHS.includes(url.pathname));

  // Check if user agent is an agentic bot
  const isAgenticBot = AGENTIC_BOTS.some((ua) => userAgent.includes(ua.toLowerCase()));

  // Route to Edge Optimize if:
  // 1. Request is NOT already from Edge Optimize (prevents infinite loops)
  // 2. User agent matches one of the agentic bots
  // 3. Path is targeted for optimization
  if (!isEdgeOptimizeRequest && isAgenticBot && isTargetedPath) {

    // Build the Edge Optimize request URL
    const edgeOptimizeURL = `https://live.edgeoptimize.net${pathAndQuery}`;

    // Clone and modify headers for the Edge Optimize request
    const edgeOptimizeHeaders = new Headers(request.headers);

    // Remove any existing Edge Optimize headers for security
    edgeOptimizeHeaders.delete("x-edgeoptimize-api-key");
    edgeOptimizeHeaders.delete("x-edgeoptimize-url");
    edgeOptimizeHeaders.delete("x-edgeoptimize-config");

    // x-forwarded-host: The original site domain
    // Use environment variable if set, otherwise use the request host
    edgeOptimizeHeaders.set("x-forwarded-host", env.EDGE_OPTIMIZE_TARGET_HOST ?? url.host);

    // x-edgeoptimize-api-key: Your Adobe-provided API key
    edgeOptimizeHeaders.set("x-edgeoptimize-api-key", env.EDGE_OPTIMIZE_API_KEY);

    // x-edgeoptimize-url: The original request URL path and query
    edgeOptimizeHeaders.set("x-edgeoptimize-url", pathAndQuery);

    // x-edgeoptimize-config: Configuration for cache key differentiation
    edgeOptimizeHeaders.set("x-edgeoptimize-config", "LLMCLIENT=TRUE;");

    try {
      // Send request to Edge Optimize backend
      const edgeOptimizeResponse = await fetch(new Request(edgeOptimizeURL, {
        headers: edgeOptimizeHeaders,
        redirect: "manual", // Preserve redirect responses from Edge Optimize
      }), {
        cf: {
          cacheEverything: true, // Enable caching based on origin's cache-control headers
        },
      });

      // Check if we need to failover to origin
      const status = edgeOptimizeResponse.status;
      const is4xxError = FAILOVER_ON_4XX && status >= 400 && status < 500;
      const is5xxError = FAILOVER_ON_5XX && status >= 500 && status < 600;

      if (is4xxError || is5xxError) {
        console.log(`Edge Optimize returned ${status}, failing over to origin`);
        return await failoverToOrigin(request, env, url);
      }

      // Return the Edge Optimize response
      return edgeOptimizeResponse;

    } catch (error) {
      // Network error or timeout - failover to origin
      console.log(`Edge Optimize request failed: ${error.message}, failing over to origin`);
      return await failoverToOrigin(request, env, url);
    }
  }

  // For all other requests (human users, SEO bots), pass through unchanged
  return fetch(request);
}

/**
 * Failover to origin server when Edge Optimize returns an error
 * @param {Request} request - The original request
 * @param {Object} env - Environment variables
 * @param {URL} url - Parsed URL object
 */
async function failoverToOrigin(request, env, url) {
  // Build origin URL
  const originURL = `${url.protocol}//${env.EDGE_OPTIMIZE_TARGET_HOST}${url.pathname}${url.search}`;

  // Prepare headers - clean Edge Optimize headers and add loop protection
  const originHeaders = new Headers(request.headers);
  originHeaders.set("Host", env.EDGE_OPTIMIZE_TARGET_HOST);
  originHeaders.delete("x-edgeoptimize-api-key");
  originHeaders.delete("x-edgeoptimize-url");
  originHeaders.delete("x-edgeoptimize-config");
  originHeaders.delete("x-forwarded-host");
  originHeaders.set("x-edgeoptimize-request", "fo");

  // Create and send origin request
  const originRequest = new Request(originURL, {
    method: request.method,
    headers: originHeaders,
    body: request.body,
    redirect: "manual",
  });

  const originResponse = await fetch(originRequest);

  // Add failover marker header to response
  const modifiedResponse = new Response(originResponse.body, {
    status: originResponse.status,
    statusText: originResponse.statusText,
    headers: originResponse.headers,
  });
  modifiedResponse.headers.set("x-edgeoptimize-fo", "1");
  return modifiedResponse;
}
```

Click **Save and deploy** to publish the worker.

![Cloudflare Worker code editor](/help/assets/optimize-at-edge/cloudflare-worker-editor.png)

**Step 3: Configure environment variables**

Environment variables store sensitive configuration like your API key securely.

1. In your worker's settings, navigate to **Settings** > **Variables**.
2. Under **Environment Variables**, click **Add variable**.
3. Add the following variables:

   | Variable Name | Description | Required |
   |---------------|-------------|----------|
   | `EDGE_OPTIMIZE_API_KEY` | Your Adobe-provided Edge Optimize API key. | Yes |
   | `EDGE_OPTIMIZE_TARGET_HOST` | The target host for Edge Optimize requests (sent as `x-forwarded-host` header) and the origin domain for failover. Must be the domain only without protocol (for example, `www.example.com`, not `https://www.example.com`). | Yes |

4. For the API key, click **Encrypt** to store it securely.
5. Click **Save and deploy**.

![Cloudflare environment variables](/help/assets/optimize-at-edge/cloudflare-env-variables.png)

**Step 4: Add a route to your domain**

To activate the worker on your domain:

1. Go to your worker's **Settings** > **Triggers**.
2. Under **Routes**, click **Add route**.
3. Enter your domain pattern (for example, `www.example.com/*` or `example.com/*`).
4. Select your zone from the dropdown.
5. Click **Save**.

Alternatively, you can configure routes at the zone level:

1. Navigate to your domain in Cloudflare.
2. Go to **Workers Routes**.
3. Click **Add route** and specify the pattern and worker.

![Cloudflare Worker routes](/help/assets/optimize-at-edge/cloudflare-worker-routes.png)

**Verifying failover behavior**

If Edge Optimize is unavailable or returns an error, the worker automatically fails over to your origin. Failover responses include the `x-edgeoptimize-fo` header:

```
< HTTP/2 200
< x-edgeoptimize-fo: 1
```

You can monitor failover events in Cloudflare Workers logs to troubleshoot issues.

**Understanding the Worker logic**

The Cloudflare Worker implements the following logic:

1. **User Agent detection:** Checks if the incoming request's user agent matches any of the defined agentic bots (case-insensitive).

2. **Path targeting:** Optionally filters requests based on targeted paths. By default, all HTML pages (URLs ending with `/`, no extension, or `.html`) are routed. You can specify specific paths using the `TARGETED_PATHS` array.

3. **Loop protection:** The `x-edgeoptimize-request` header prevents infinite loops. When Edge Optimize makes requests back to your origin, this header is set to `"1"`, and the worker passes the request through without routing it back to Edge Optimize.

4. **Header security:** Before setting Edge Optimize headers, the worker removes any existing `x-edgeoptimize-*` headers from the incoming request to prevent header injection attacks.

5. **Header mapping:** The worker sets the required headers for Edge Optimize:
   * `x-forwarded-host` – Identifies the original site domain.
   * `x-edgeoptimize-url` – Preserves the original request path and query string.
   * `x-edgeoptimize-api-key` – Authenticates the request with Edge Optimize.
   * `x-edgeoptimize-config` – Provides cache key configuration.

6. **Failover logic:** If Edge Optimize returns any error status code (4XX client errors or 5XX server errors) or the request fails due to a network error, the worker automatically fails over to your origin using `EDGE_OPTIMIZE_TARGET_HOST`. The failover response includes the `x-edgeoptimize-fo: 1` header to indicate that failover occurred.

7. **Redirect handling:** The `redirect: "manual"` option ensures that redirect responses from Edge Optimize are passed through to the client without the worker following them.

**Customizing the configuration**

You can customize the worker behavior by modifying the configuration constants at the top of the code:

**Agentic bot list**

Modify the `AGENTIC_BOTS` array to add or remove user agents:

```javascript
const AGENTIC_BOTS = [
  'AdobeEdgeOptimize-AI',
  'ChatGPT-User',
  'GPTBot',
  'OAI-SearchBot',
  'PerplexityBot',
  'Perplexity-User',
  // Add additional user agents as needed
  'ClaudeBot',
  'Anthropic-AI'
];
```

**Targeted paths**

By default, all HTML pages are routed to Edge Optimize. To limit routing to specific paths, modify the `TARGETED_PATHS` array:

```javascript
// Route all HTML pages (default)
const TARGETED_PATHS = null;

// Or specify exact paths to route
const TARGETED_PATHS = ['/', '/page.html', '/products', '/about-us'];
```

**Failover configuration**

By default, the worker fails over on any 4XX or 5XX error from Edge Optimize. Customize this behavior:

```javascript
// Default: failover on any 4XX or 5XX error
const FAILOVER_ON_4XX = true;
const FAILOVER_ON_5XX = true;

// Failover only on 5XX server errors (not 4XX client errors)
const FAILOVER_ON_4XX = false;
const FAILOVER_ON_5XX = true;

// Disable automatic failover (not recommended)
const FAILOVER_ON_4XX = false;
const FAILOVER_ON_5XX = false;
```

**Important considerations**

* **Failover behavior:** The worker automatically fails over to your origin if Edge Optimize returns any error (4XX or 5XX status codes) or if the request fails due to a network error. Failover uses `EDGE_OPTIMIZE_TARGET_HOST` as the origin domain (similar to Fastly's `F_Default_Origin` or CloudFront's `Default_Origin`). Failover responses include the `x-edgeoptimize-fo: 1` header, which you can use for monitoring and debugging.

* **Caching:** Cloudflare caches responses based on the URL by default. Because agentic traffic receives different content than human traffic, ensure your cache configuration accounts for this. Consider using Cache API or cache headers to differentiate cached content. The `x-edgeoptimize-config` header should be included in your cache key.

* **Rate limiting:** Monitor your Edge Optimize usage and consider implementing rate limiting for agentic traffic if needed.

* **Testing:** Always test the configuration in a staging environment before deploying to production. Verify that both agentic and human traffic behave as expected. Test failover behavior by simulating Edge Optimize errors.

* **Logging:** Enable Cloudflare Workers logging to monitor requests and troubleshoot issues. Navigate to **Workers** > **your worker** > **Logs** to view real-time logs. The worker logs failover events for debugging purposes.

**Troubleshooting**

| Issue | Possible Cause | Solution |
|-------|----------------|----------|
| No `x-edgeoptimize-request-id` header in response | Worker route not matched, or user agent not in the agentic bots list. | Verify your route pattern matches the request URL. Check that the user agent is in the `AGENTIC_BOTS` array. |
| 401 or 403 errors from Edge Optimize | Invalid or missing API key. | Verify `EDGE_OPTIMIZE_API_KEY` is correctly set in environment variables. Contact Adobe to confirm your API key is active. |
| Infinite redirects or loops | Loop protection header not being set or checked correctly. | Ensure the `x-edgeoptimize-request` header check is in place. |
| Human traffic affected | Worker routing logic is too broad. | Verify the user agent matching logic is correct and case-insensitive. Check that `TARGETED_PATHS` is configured correctly. |
| Slow response times | Network latency to Edge Optimize backend. | This is expected for the first request; subsequent requests are cached at Edge Optimize. |
| `x-edgeoptimize-fo: 1` header in response | Edge Optimize returned an error and failover to origin occurred. | Check Cloudflare Workers logs for the specific error code. Verify Edge Optimize service status with Adobe. |
| Failover not working | Failover flags disabled, or error in failover logic. | Verify `FAILOVER_ON_4XX` and `FAILOVER_ON_5XX` are set to `true`. Check worker logs for error messages. |
| Certain paths not being optimized | Path not matching the targeted paths or HTML page pattern. | Verify the path is in `TARGETED_PATHS` (if specified) and matches the HTML page regex pattern. |
| Requests failing with invalid host | `EDGE_OPTIMIZE_TARGET_HOST` includes protocol (for example, `https://`). | Use only the domain name without protocol (for example, `example.com`, not `https://example.com`). |
| 530 error during failover | Cloudflare cannot connect to origin, or failover request has invalid headers. | Ensure the failover function removes Edge Optimize headers. Verify your origin is accessible and DNS is configured correctly. |

**Verify the setup**

After completing the setup, verify that bot traffic is being routed to Edge Optimize and that human traffic remains unaffected.

**1. Test bot traffic (should be optimized)**

Simulate an AI bot request using an agentic user-agent:

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: chatgpt-user"
```

A successful response includes the `x-edgeoptimize-request-id` header, confirming that the request was routed through Edge Optimize:

```
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

**2. Test human traffic (should NOT be affected)**

Simulate a regular human browser request:

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36"
```

The response should **not** contain the `x-edgeoptimize-request-id` header. The page content and response time should remain identical to before enabling Optimize at Edge.

**3. How to differentiate between the two scenarios**

| Header | Bot traffic (optimized) | Human traffic (unaffected) |
|---|---|---|
| `x-edgeoptimize-request-id` | Present — contains a unique request ID | Absent |
| `x-edgeoptimize-fo` | Present only if failover occurred (value: `1`) | Absent |

The status of the traffic routing can also be checked in the LLM Optimizer UI. Navigate to **Customer Configuration** and select the **CDN Configuration** tab.

![AI Traffic Routing status with routing enabled](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

{{return-to-overview}}
