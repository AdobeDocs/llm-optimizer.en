---
title: Optimize at Edge
description: Learn how to deliver optimizations in LLM Optimizer at the CDN edge without any authoring changes required.
feature: Opportunities
---

# Optimize at Edge

This page provides a detailed overview on how to deliver optimizations at the CDN edge without any authoring changes. It covers the onboarding process, the available optimization opportunities and how to auto-optimize at edge.

>[!NOTE]
>This functionality is currently in Early Access. You can learn more about Early Access programs [here](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current#aem-beta-programs).

## What is Optimize at Edge?

Optimize at Edge is an edge-based deployment capability in LLM Optimizer that serves AI friendly changes to LLM user agents. In the current context, "Edge" means that the optimization is applied at the CDN layer. Because it delivers optimizations at the CDN layer, no authoring changes in the Content Management System (CMS) are required so your origin CMS remains unchanged. This separation lets you improve LLM visibility without altering your existing publishing workflows. It targets only agentic traffic and does not impact either human users or SEO bots. When LLM Optimizer detects opportunities to optimize a page, users can deploy fixes directly at the CDN edge.

Optimize at Edge is a faster, leaner alternative to traditional fixes that demand complex engineering efforts. As mentioned, once you complete a one-time setup, no platform changes or long development cycles are required to apply the changes. You can publish improvements in minutes without requiring developer engagement. It is a no-code way to optimize your website for AI agents.

Optimize at Edge is designed for business users in marketing, SEO, content and digital strategy teams. It can enable business users to complete the full journey in LLM Optimizer: identifying opportunities, understanding suggestions, and easily deploying the fixes. With Optimize at Edge, users can preview the changes, deploy them quickly at the CDN edge and validate that the optimizations are live. Performance can be tracked in the LLM Optimizer ecosystem.

### Key benefits

* **AI-only delivery:** Serves optimized HTML only to AI agents with no impact on either human visitors or SEO bots.
* **Faster cycles:** Publish changes in minutes not weeks. No platform changes or long engineering cycles required.
* **Reversible:** Supported with a one-click rollback capability that can revert the page in minutes.
* **No performance impact:** Edge based optimizations and caching keep the site latency unaffected.
* **CDN and CMS-agnostic:** Works with any CDN configuration and front-end setup regardless of the Content Management System.

### Which opportunities are supported with Optimize at Edge?

Opportunities that can improve the agentic web experience are supported with Optimize at Edge. Learn more about each opportunity both in the [Opportunities Dashboard](/help/dashboards/opportunities.md) page and the opportunities section in the current page.

## Onboarding

You should reach out to either your Adobe account team or the FDE team to start the onboarding process. Your IT or CDN team is also required to complete the pre-requisites and setup process. Additionally, you can also contact `llmo-at-edge@adobe.com` for further onboarding assistance.

Pre-requisites to onboard to Optimize at Edge:

* Complete the onboarding process to LLM Optimizer.
* Complete the log forwarding process for your CDN logs.

Requirements for your IT/CDN team:
* Add `*AdobeEdgeOptimize/1.0*` user-agent to the Allowlist in your site's robots.txt file or bot-traffic management rules.
* Ensure that pages are not blocked at the domain or CDN level.
* Add Optimize at Edge routing rules in the CDN.
* Confirm Optimize at Edge routing in the LLM Optimizer interface.

To guide the setup process, presented below, are sample configurations for a number of CDN setups. Keep in mind that these examples should be adapted to your actual live configuration. We recommend applying changes in the lower environments first.

>[!BEGINTABS]

>[!TAB AEM Cloud Service Managed CDN (Fastly)]

**Edge Optimize - AEM Cloud Service Managed CDN (Fastly)**

This configuration routes agentic traffic (requests from AI bots and LLM user agents) to the Edge Optimize backend service (`live.edgeoptimize.net`). Human visitors and SEO bots continue to be served from your origin as usual. To test the configuration, after the setup is complete, look for the header `x-edgeoptimize-request-id` in the response.

**Prerequisites**

To start routing agentic traffic to Edge Optimize:

1. Navigate to **Customer Configuration** and select the **CDN Configuration** tab.

   ![Navigate to Customer Configuration](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. Under **AI Traffic Routing to Deploy Optimizations**, tick the **Deploy Optimizations to AI Agents** checkbox. The Adobe team will handle the routing configuration on your behalf.

   ![Tick Deploy Optimizations to AI Agents](/help/assets/optimize-at-edge/prereq-deploy-checkbox.png)

3. After enabling the checkbox, the status will show that the setup is in progress. The Adobe team will complete the routing configuration for you.

   ![AI Traffic Routing setup in progress](/help/assets/optimize-at-edge/prereq-traffic-routing-progress.png)

   Once the routing is configured and active, the status will update to show a green checkmark indicating that routing is successfully enabled. No further action is required on your end.

Additionally, if you require any help with the above steps, reach out to your Adobe account team or `llmo-at-edge@adobe.com`.

**Self-service routing via Cloud Manager Pipeline**

If you prefer to configure the routing yourself through the Cloud Manager Pipeline, follow the steps below. The routing configuration is done by using an [originSelector CDN rule](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#origin-selectors). The prerequisites are as follows:

* Decide the domain to be routed.
* Decide the paths to be routed.
* Decide the user agents to be routed (recommended regex).

In order to deploy the rule, you need to:

* Create a [configuration pipeline](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/config-pipeline).
* Commit the `cdn.yaml` configuration file in your repository.
* Run the configuration pipeline.

```
kind: "CDN"
version: "1"
data:
  # Origin selectors to route to Edge Optimize backend
  originSelectors:
    rules:
      - name: route-to-edge-optimize-backend
        when:
          allOf:
            - reqHeader: x-edgeoptimize-request
              exists: false # avoid loops when requests comes from Edge Optimize
            - reqHeader: user-agent
              matches: "(?i)(AdobeEdgeOptimize-AI|ChatGPT-User|GPTBot|OAI-SearchBot|PerplexityBot|Perplexity-User)" # routed user agents
            - reqProperty: domain
              equals: "example.com" # routed domain
            - reqProperty: originalPath
              matches: '(/[^./]+|\.html|/)$' # routed extensions, with .html extension or without extension
            - anyOf:
              - { reqProperty: originalPath, in: [ "/page.html" ] } # routed pages, exact path matching
              - { reqProperty: originalPath, like: "/dir/*" } # routed pages, wildcard path matching
        action:
          type: selectOrigin
          originName: edge-optimize-backend
    origins:
      - name: edge-optimize-backend
        domain: "live.edgeoptimize.net"

```

**Verify the setup**

To test the setup, run a curl and expect the following:

```
curl -svo /dev/null https://www.example.com/page.html --header "user-agent: chatgpt-user"
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85

```

The status of the traffic routing can also be checked in the LLM Optimizer UI. Navigate to **Customer Configuration** and select the **CDN Configuration** tab.

![AI Traffic Routing status with routing enabled](/help/assets/optimize-at-edge/adobe-CDN-traffic-routed-tick.png)

>[!TAB Fastly (BYOCDN)]

**Edge Optimize - Fastly (BYOCDN)**

This configuration routes agentic traffic (requests from AI bots and LLM user agents) to the Edge Optimize backend service (`live.edgeoptimize.net`). Human visitors and SEO bots continue to be served from your origin as usual. To test the configuration, after the setup is complete, look for the header `x-edgeoptimize-request-id` in the response.

**Prerequisites**

Before setting up the Fastly VCL rules, ensure you have:

* Access to Fastly for your domain.
* Completed the LLM Optimizer onboarding process.
* Completed CDN log forwarding to LLM Optimizer.
* An Edge Optimize API key retrieved from the LLM Optimizer UI.

**Steps to retrieve your API key:**

1. Navigate to **Customer Configuration** and select the **CDN Configuration** tab.

   ![Navigate to Customer Configuration](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. Under **AI Traffic Routing to Deploy Optimizations**, tick the **Deploy Optimizations to AI Agents** checkbox.

   ![Tick Deploy Optimizations to AI Agents](/help/assets/optimize-at-edge/prereq-deploy-checkbox.png)

3. Copy the API key and proceed with the routing configuration steps below.

   ![Copy the API key](/help/assets/optimize-at-edge/prereq-copy-api-key.png)

   >[!NOTE]
   >At this stage, the status may show a red cross indicating that the setup is not yet completed. This is expected — once you complete the routing configuration below and AI bot traffic starts flowing, the status will update to a green checkmark confirming that routing is successfully enabled.

Additionally, if you require any help with the above steps, reach out to your Adobe account team or `llmo-at-edge@adobe.com`.

**Configuration**

Add the following three VCL snippets to your Fastly service. These snippets handle routing agentic requests to Edge Optimize, cache-key separation, and failover to your default origin.

![Fastly VCL](/help/assets/optimize-at-edge/fastly-vcl.png)

![Add VCL snippets](/help/assets/optimize-at-edge/add-vcl-snippets.png)

**vcl_recv snippet**

```
unset req.http.x-edgeoptimize-url;
unset req.http.x-edgeoptimize-config;
unset req.http.x-edgeoptimize-api-key;

if (!req.http.x-edgeoptimize-request
    && req.http.user-agent ~ "(?i)(AdobeEdgeOptimize-AI|ChatGPT-User|GPTBot|OAI-SearchBot|PerplexityBot|Perplexity-User)") {
  set req.http.x-forwarded-host = req.http.host; # required for identifying the original host
  set req.http.x-edgeoptimize-url = req.url; # required for identifying the original url
  set req.http.x-edgeoptimize-config = "LLMCLIENT=TRUE;"; # required for cache key
  set req.http.x-edgeoptimize-api-key = "<YOUR API KEY>"; # required for identifying the client
  set req.backend = F_EDGE_OPTIMIZE;
}
```

**vcl_hash snippet**

```
if (req.http.x-edgeoptimize-config) {
  set req.hash += "edge-optimize";
  set req.hash += req.http.x-edgeoptimize-config;
}
```

**vcl_deliver snippet**

```
if (req.http.x-edgeoptimize-config && resp.status >= 400) {
  set req.http.x-edgeoptimize-request = "failover";
  set req.backend = F_Default_Origin;
  restart;
}

if (!req.http.x-edgeoptimize-config && req.http.x-edgeoptimize-request == "failover") {
  set resp.http.x-edgeoptimize-fo = "1";
}
```

**Failover**

The `vcl_deliver` snippet handles failover automatically. If Edge Optimize returns a `4XX` or `5XX` error, the request is restarted and routed back to your default origin so the end-user still receives a response. Failover responses include the `x-edgeoptimize-fo: 1` header.

| Scenario | Behavior |
| --- | --- |
| Edge Optimize returns `2XX` | Optimized response is served to the client. |
| Edge Optimize returns `4XX` or `5XX` | Request is restarted and served from the default origin. |
| Failover response | Includes the header `x-edgeoptimize-fo: 1`. |

**Verify the setup**

To test the setup, run a curl and expect the following:

```
curl -svo /dev/null https://www.example.com/page.html --header "user-agent: chatgpt-user"
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85

```

The status of the traffic routing can also be checked in the LLM Optimizer UI. Navigate to **Customer Configuration** and select the **CDN Configuration** tab.

![AI Traffic Routing status with routing enabled](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

>[!TAB Akamai (BYOCDN)]

**Edge Optimize - Akamai (BYOCDN)**

This configuration routes agentic traffic (requests from AI bots and LLM user agents) to the Edge Optimize backend service (`live.edgeoptimize.net`). Human visitors and SEO bots continue to be served from your origin as usual. To test the configuration, after the setup is complete, look for the header `x-edgeoptimize-request-id` in the response.

**Prerequisites**

Before setting up the Akamai Property Manager rules, ensure you have:

* Access to Akamai Property Manager for your domain.
* Completed the LLM Optimizer onboarding process.
* Completed CDN log forwarding to LLM Optimizer.
* An Edge Optimize API key retrieved from the LLM Optimizer UI.

**Steps to retrieve your API key:**

1. Navigate to **Customer Configuration** and select the **CDN Configuration** tab.

   ![Navigate to Customer Configuration](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. Under **AI Traffic Routing to Deploy Optimizations**, tick the **Deploy Optimizations to AI Agents** checkbox.

   ![Tick Deploy Optimizations to AI Agents](/help/assets/optimize-at-edge/prereq-deploy-checkbox.png)

3. Copy the API key and proceed with the routing configuration steps below.

   ![Copy the API key](/help/assets/optimize-at-edge/prereq-copy-api-key.png)

   >[!NOTE]
   >At this stage, the status may show a red cross indicating that the setup is not yet completed. This is expected — once you complete the routing configuration below and AI bot traffic starts flowing, the status will update to a green checkmark confirming that routing is successfully enabled.

Additionally, if you require any help with the above steps, reach out to your Adobe account team or `llmo-at-edge@adobe.com`.

**Configuration**

The following Akamai Property Manager rule routes LLM user agents to Edge Optimize. The configuration includes the following steps:

**1. Set routing criteria (User-Agent matching)**

Set routing for the following user-agents:

```
 *AdobeEdgeOptimize-AI*,
 *ChatGPT-User*,
 *GPTBot*,
 *OAI-SearchBot*,
 *PerplexityBot*,
 *Perplexity-User*
```

![Set routing criteria](/help/assets/optimize-at-edge/akamai-step1-routing.png)

**2. Set Origin and SSL behavior**

Set origin as `live.edgeoptimize.net` and Match SAN to `*.edgeoptimize.net`

![Set Origin and SSL behavior](/help/assets/optimize-at-edge/akamai-step2-origin.png)

**3. Set Cache Key Variable**

Set the cache key variable `PMUSER_EDGE_OPTIMIZE_CACHE_KEY` to `LLMCLIENT=TRUE;X_FORWARDED_HOST={{builtin.AK_HOST}}`

![Set Cache Key Variable](/help/assets/optimize-at-edge/akamai-step3-cachekey.png)

**4. Caching Rules**

![Caching Rules](/help/assets/optimize-at-edge/akamai-step4-rules.png)

**5. Modify Incoming Request Headers**

Set the following incoming request headers:
`x-edgeoptimize-api-key` to the API Key retrieved from LLMO
`x-edgeoptimize-config` to `LLMCLIENT=TRUE;`
`x-edgeoptimize-url` to `{{builtin.AK_URL}}`

![Modify Incoming Request Headers](/help/assets/optimize-at-edge/akamai-step5-request.png)

**6. Modify Incoming Response Headers**

![Modify Incoming Response Headers](/help/assets/optimize-at-edge/akamai-step6-response.png)

**7. Cache ID Modification**

![Cache ID Modification](/help/assets/optimize-at-edge/akamai-step7-cacheid.png)

**8. Modify Outgoing Request Headers**

Set `x-forwarded-host` header to `{{builtin.AK_HOST}}`

![Modify Outgoing Request Headers](/help/assets/optimize-at-edge/akamai-step8-outgoing-request.png)

**9. Site Failover**

![Site Failover](/help/assets/optimize-at-edge/akamai-step9-failover.png)

![Failover Behaviors](/help/assets/optimize-at-edge/akamai-step9-failover-behaviors.png)

![Failover Rules](/help/assets/optimize-at-edge/akamai-step9-failover-rules.png)

Site Failover ensures that if Edge Optimize returns a `4XX` or `5XX` error, the request is automatically routed back to your default origin so the end-user still receives a response.

| Scenario | Behavior |
| --- | --- |
| Edge Optimize returns `2XX` | Optimized response is served to the client. |
| Edge Optimize returns `4XX` or `5XX` | Request is routed back to the default origin. |

**Verify the setup**

To test the setup, run a curl and expect the following:

```
curl -svo /dev/null https://www.example.com/page.html --header "user-agent: chatgpt-user"
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

The status of the traffic routing can also be checked in the LLM Optimizer UI. Navigate to **Customer Configuration** and select the **CDN Configuration** tab.

![AI Traffic Routing status with routing enabled](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

>[!TAB Cloudflare (BYOCDN)]

**Edge Optimize - Cloudflare (BYOCDN)**

This configuration routes agentic traffic (requests from AI bots and LLM user agents) to the Edge Optimize backend service (`live.edgeoptimize.net`). Human visitors and SEO bots continue to be served from your origin as usual. To test the configuration, after the setup is complete, look for the header `x-edgeoptimize-request-id` in the response.

**Prerequisites**

Before setting up the Cloudflare Worker routing rules, ensure you have:

* A Cloudflare account with Workers enabled on your domain.
* Access to your domain's DNS settings in Cloudflare.
* Completed the LLM Optimizer onboarding process.
* Completed CDN log forwarding to LLM Optimizer.
* An Edge Optimize API key retrieved from the LLM Optimizer UI.

**Steps to retrieve your API key:**

1. Navigate to **Customer Configuration** and select the **CDN Configuration** tab.

   ![Navigate to Customer Configuration](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. Under **AI Traffic Routing to Deploy Optimizations**, tick the **Deploy Optimizations to AI Agents** checkbox.

   ![Tick Deploy Optimizations to AI Agents](/help/assets/optimize-at-edge/prereq-deploy-checkbox.png)

3. Copy the API key and proceed with the routing configuration steps below.

   ![Copy the API key](/help/assets/optimize-at-edge/prereq-copy-api-key.png)

   >[!NOTE]
   >At this stage, the status may show a red cross indicating that the setup is not yet completed. This is expected — once you complete the routing configuration below and AI bot traffic starts flowing, the status will update to a green checkmark confirming that routing is successfully enabled.

Additionally, if you require any help with the above steps, reach out to your Adobe account team or `llmo-at-edge@adobe.com`.

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

**Step 5: Verify the setup**

After deploying, test the configuration by making a request with an agentic user agent.

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: chatgpt-user"
```

A successful response includes the `x-edgeoptimize-request-id` header:

```
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

The status of the traffic routing can also be checked in the LLM Optimizer UI. Navigate to **Customer Configuration** and select the **CDN Configuration** tab.

![AI Traffic Routing status with routing enabled](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

You can also verify that normal traffic continues to work:

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: Mozilla/5.0"
```

This request should be served from your origin without the `x-edgeoptimize-request-id` header.

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

>[!ENDTABS]

>[!NOTE]
>For other CDN providers, please reach out to `llmo-at-edge@adobe.com` to assist your IT/CDN teams with onboarding. Once the setup configurations are complete, you can deploy suggestions for Optimize at Edge opportunities in LLM Optimizer.

## Opportunities

Presented in the following table are opportunities that can improve the agentic web experience and are supported with Optimize at Edge.

| Opportunity | Type | Auto-Identify | Auto-suggest | Auto-optimize |
|---------|----------|----------|----------|----------|
|Recover Content Visibility | Technical GEO | Detects pages where critical content is hidden from AI agents. Shows affected URLs and expected content that can be recovered.| Highlights content that can be made available for AI agents and recommends enabling pre-rendering for those pages. | Serves a fully rendered, AI-friendly HTML snapshot to agentic traffic that recovers the previously hidden content.|
| Add LLM-Friendly Summaries | Content Optimization | Identifies long or complex pages that lack concise summaries at the page or section level, making them harder for AI to quickly scan and understand.| Recommends short, AI-generated summaries at the page and section level that capture key content.| Inserts the summaries into the relevant HTML sections, improving how models interpret and describe the page content.|
| Add Relevant FAQs | Content Optimization | Detects intent gaps in the existing page content that could benefit from FAQs. | Suggests AI-generated FAQ content aligned to the user intent and existing topics. | Injects FAQ content into the HTML, making pages more discoverable and relevant in AI-driven answers.|
| Simplify Complex Content | Content Optimization | Flags pages with complex text that can hinder AI comprehension. | Provides AI-generated simplified versions of complex text while preserving the original meaning. | Rewrites complex sections in the page, improving AI readability. |

### Additional Tools

The [Adobe LLM Optimizer: Is your webpage citable?](https://chromewebstore.google.com/detail/adobe-llm-optimizer-is-yo/jbjngahjjdgonbeinjlepfamjdmdcbcc) Chrome extension shows how much of your webpage content LLMs can access and what stays hidden. Designed as a free, standalone diagnostic tool, it requires no product license or setup.

With a single-click, you can evaluate any site's machine readability. You can view a side-by-side comparison of what AI agents see versus what human users see, and estimate how much content could be recovered by using LLM Optimizer. See the [Can AI read your website?](https://business.adobe.com/blog/introducing-the-llm-optimizer-chrome-extension) page for more information.

## Opportunities detailed

In the sections that follow, you can view additional details for each opportunity that is supported with Optimize at Edge.

### Recover Content Visibility

This opportunity flags pages where key content is hidden for AI agents due to client-side rendering. For each identified page, it shows you exactly which content is missing from the AI agent view, highlights visibility gaps, and enables you to directly apply changes to recover the hidden content. When you deploy this opportunity with Optimize at Edge, a pre-rendered, AI-optimized version of the page is served to LLM user agents so they can access the full context without executing Javascript.
This ensures the page is first fully visible to AI agents. Additional enhancements are applied on top of that pre-rendered HTML.

>[!IMPORTANT]
>This pre-rendering capability automatically applies to all opportunities presented below when deployed with Optimize at Edge to ensure the page is fully visible to AI agents.

### Add LLM-Friendly Summaries

This opportunity identifies pages that can benefit from concise summaries to help LLMs quickly understand what the page content is about. For each page, the opportunity detects where a summary is most needed and creates AI-generated summaries either at the page level or section level. When you deploy with Optimize at Edge these summaries are inserted into the HTML that AI agents retrieve, improving the chances of having your content be described more accurately.

### Add Relevant FAQs

This opportunity flags pages where additional Q&A content could better match the user intent and prompts in AI-driven discovery. For each page, it proposes AI-generated FAQ blocks tied to user intent and content on the page. With Optimize at Edge, these FAQs are injected into the HTML, making your page more AI-friendly and increasing the likelihood that AI answers directly reflect your guidance.

### Simplify Complex Content

This opportunity finds pages with long, complex paragraphs that can reduce AI comprehension. For each page that exceeds the readability thresholds, it creates AI-generated content that is simpler and easier to scan while preserving the original meaning. When deployed at the edge, the simplified content delivered to agentic traffic helps LLMs interpret and summarize your content more faithfully.

## Auto-Optimize at Edge

For each opportunity, you can preview, edit, deploy, view live, and roll back the optimizations at the edge.

>[!VIDEO](https://video.tv.adobe.com/v/3477983/?learn=on&enablevpops)

### Preview

**Preview** lets you see the impact of a suggestion before it goes live. It surfaces a side-by-side difference between the current page and the AI-optimized version expected after applying the suggestion. This view uses the same Optimize at Edge logic that will power live traffic, but in an isolated preview mode. This does not impact live traffic as it is a read-only simulation for review.

![Preview](/help/assets/optimize-at-edge/preview.png)

### Edit

**Edit** allows you to refine or rewrite altogether the auto-generated suggestion before deploying it. Instead of accepting the suggestion, you maintain full control through the edit workflow. The view displays proposed changes in a structured editor, where you can modify the text to better match your original intent. The edited version will then be served to AI agents once deployed.

![Edit](/help/assets/optimize-at-edge/edit.png)

### Deploy

**Deploy** publishes the selected suggestions so the optimized experiences can be served from the edge to AI agents. If the CDN is fully routed, all pages in the domain usually go live with the new changes within minutes. If routing has been configured for select paths only, only the allowlisted pages go live with the optimizations.

![Deploy](/help/assets/optimize-at-edge/deploy.png)

### View Live

**View Live** lets you verify that the optimization is live and behaving as expected for agentic traffic, a view that would otherwise be hard to access. You can view the live page under Fixed Suggestions, which renders the page as shown to AI agents.

![View Live](/help/assets/optimize-at-edge/view-live.png)

### Rollback

Rollback safely reverts a previously deployed optimization. The AI-only version of the page is typically returned to its previous state within minutes, making it safe to experiment with optimizations when needed.

![Rollback](/help/assets/optimize-at-edge/rollback.png)

## Frequently Asked Questions

Q. What kind of LLMs do you target with Optimize at Edge?

The list of user agents to target is defined by you during the onboarding process.

<!--Q. What does "Edge" in Optimize at Edge mean?

In our context, "Edge" means that the optimization is applied at the CDN layer and not inside your CMS.

Q. Why does this optimization require a CDN?

The CDN is where the optimized version of the page is assembled and delivered to AI agents. We leverage the CDN to ensure your origin CMS remains unchanged. This separation lets you improve LLM visibility without altering your existing publishing workflows.-->

Q. What happens if I'm not onboarded to Optimize at Edge yet?

If you click **Deploy optimizations** before completing the required setup, nothing will be applied to your site. Instead, a pop-up dialog prompts you to contact our team at `llmo-at-edge@adobe.com` for onboarding assistance. Until onboarding is complete, you can still explore the detected opportunities and suggestions, but the one-click deployment workflow will remain inactive.

Q: What happens when the content is updated at source?

We serve the optimized version of your page from cache as long as the underlying source page has not changed. However, when the source does change for **Recover Content Visibility**, our system automatically refreshes so AI agents always receives the most up-to-date content. This is because we use low cache time to live (TTL) settings (by order of minutes) so that any content update on your site triggers a new optimization within that window. For content opportunities like **Add LLM-Friendly Summaries**, LLM Optimizer monitors the source page for changes. If a change is detected, we pause the optimization and flag it for human review to prevent content drift between the agent-visible page and human-visible page.
<!--As there is no universal TTL that fits every site, we can configure this TTL based on your cache invalidation rules to ensure both systems stay in sync.-->

Q. Is Optimize at Edge only for sites using Adobe Edge Delivery Service (EDS)?

No. Optimize at Edge is CDN-agnostic and works with any front-end architecture, not just the ones deployed on Adobe's EDS Stack.

Q. How is Optimize at Edge pre-rendering different from traditional server-side rendering (SSR)?

Both solve different problems and can work together. Traditional SSR renders server-side content but doesn't include content loaded later in the browser. Optimize at Edge pre-rendering captures the page after JavaScript and client-side data has loaded, producing the fully assembled version at the CDN edge. SSR focuses on improving the human experience and Optimize at Edge improves the web experience for LLMs.

Q. What happens if I deploy optimizations for some URLs in my domain but not all?

Only the URLs you explicitly optimize are modified. For URLs with deployed opportunities, AI agents receive the optimized version. For URLs with no deployed opportunities, our service simply proxies the original page as-is without applying changes or storing it in our optimization cache layer. This ensures you can selectively deploy optimizations without affecting the rest of your site.
