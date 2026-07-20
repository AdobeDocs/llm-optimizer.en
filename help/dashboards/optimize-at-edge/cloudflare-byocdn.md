---
title: Optimize at Edge - Cloudflare (BYOCDN)
description: Learn how to configure Cloudflare BYOCDN for Optimize at Edge in LLM Optimizer.
feature: Opportunities
autotag-review: '2026-07-15T17:46:02.378Z'
TQID: 'https://experienceleague.adobe.com/ZgOX0yC8qyb13Y7YNCg3Y1A6Q3TSk9-mUQ8gthzQvLM'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
    internal-label: LLM Optimizer
feature_v2:
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
    internal-label: Administration
  - id: e0828736-236a-487b-a478-5a635455eadc
    internal-label: Traffic analytics
  - id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
    internal-label: Opportunities
  - id: ef4e63f5-cb4d-462d-bf9a-1f617edf2a3a
    internal-label: Optimize at edge
subfeature_v2:
  - id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
    internal-label: CDN log forwarding
  - id: e06fae5f-830b-4222-a469-b5e148d36465
    internal-label: Agentic traffic
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
---

# Cloudflare (BYOCDN)

This configuration routes agentic traffic (requests from AI bots and LLM user agents) to the Edge Optimize backend service (`live.edgeoptimize.net`). Human visitors and SEO bots continue to be served from your origin as usual. To test the configuration, after the setup is complete, look for the header `x-edgeoptimize-request-id` in the response.

## Prerequisites

Before you set up the Cloudflare Worker routing rules, ensure you have:

* A Cloudflare account with Workers enabled on your domain.
* Access to your domain's DNS settings in Cloudflare.
* An Edge Optimize API key retrieved from the LLM Optimizer UI. For steps, see [Retrieve your API keys](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#production-api-key).
* (Optional) To test staging routing, see [Staging API key](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#staging-api-key-optional).

## How routing works

When configured correctly, a request to your domain (for example, `www.example.com/page.html`) from an agentic user agent is intercepted by the Cloudflare Worker and routed to the Edge Optimize backend. The backend request includes the required headers.

### Testing the backend request

You can verify the routing by making a direct request to the Edge Optimize backend.

```
curl -svo /dev/null https://live.edgeoptimize.net/page.html \
  -H 'x-forwarded-host: www.example.com' \
  -H 'x-edgeoptimize-url: /page.html' \
  -H 'x-edgeoptimize-api-key: $EDGE_OPTIMIZE_API_KEY' \
  -H 'x-edgeoptimize-config: LLMCLIENT=TRUE;'
```

### Required Headers

The following headers must be set on requests to the Edge Optimize backend:

| Header | Description | Example |
|--------|-------------|---------|
| `x-forwarded-host` | The original host of the request. Required for identifying the site domain. | `www.example.com` |
| `x-edgeoptimize-url` | The original URL path and query string of the request. | `/page.html` or `/products?id=123` |
| `x-edgeoptimize-api-key` | The API key provided by Adobe for your domain. | `your-api-key-here` |
| `x-edgeoptimize-config` | Configuration string for cache key differentiation. | `LLMCLIENT=TRUE;` |

## Setup options

There are two ways to set up the Cloudflare Worker for Edge Optimize:

* [**Option 1: Deploy to Cloudflare (recommended)**](#option-1-deploy-to-cloudflare) — Automatically creates a new worker and prompts you for the required environment variables and secrets. Use this option if you do not have an existing Cloudflare Worker for this domain.
* [**Option 2: Manual setup**](#option-2-manual-setup) — Step-by-step instructions for creating and configuring the worker yourself. Use this option if you already have an existing Cloudflare Worker configured on your domain — you will need to merge the Edge Optimize code into your existing worker (see [Step 2: Add the Worker code](#option-2-manual-setup)), or if you prefer full control over the deployment.

Regardless of which option you choose, you must manually link the worker to your domain — see [Step: Add a route to your domain](#add-a-route-to-your-domain).

## Option 1: Deploy to Cloudflare

This option uses the **Deploy to Cloudflare** button to automatically create the worker and configure the required environment variables and secrets in your Cloudflare account. This is the quickest way to get started if you are setting up a new worker.

>[!IMPORTANT]
>
>Use this option only if you **do not** have an existing Cloudflare Worker on your domain. If you already have a worker, use [Option 2: Manual setup](#option-2-manual-setup) to add the Edge Optimize routing logic to your existing worker.

### Step 1: Deploy the worker

Click the button below to deploy the Edge Optimize worker to your Cloudflare account:

[![Deploy to Cloudflare](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/adobe/llmo-code-samples/tree/main/optimize-at-edge/cloudflare/automation)

### Step 2: Fill in the deployment form

Clicking the button opens the Workers setup page. Fill in the form as follows:

![Cloudflare Workers setup page](/help/assets/optimize-at-edge/cloudflare-deploy-form.png)

1. **Git account** — Select your GitHub or GitLab account from the dropdown. Cloudflare forks the worker code into a repository in your account. If no account is listed, you can add a new connection directly from the dropdown by selecting **+ New GitHub Connection** or **+ New GitLab Connection**. For more information, see the [Cloudflare Git integration guide](https://developers.cloudflare.com/workers/ci-cd/builds/git-integration/github-integration/).

   ![Git account dropdown showing New GitHub Connection and New GitLab Connection options](/help/assets/optimize-at-edge/cloudflare-git-connection.png)
2. **Create private Git repository** — Leave this checked (default).
3. **Project name** — Leave as `edge-optimize-router` or enter a name of your choice.
4. **EDGE_OPTIMIZE_API_KEY** — Paste your Adobe-provided Edge Optimize API key. This value is stored as an encrypted secret.
5. **EDGE_OPTIMIZE_TARGET_HOST** — Enter your site's domain without the protocol (for example, `www.example.com`).
6. **Build command** — Leave empty.
7. **Deploy command** — Leave as `npm run deploy` (pre-filled).
8. **Builds for non-production branches** — Leave unchecked. This is a developer workflow feature and is not needed for this deployment.
9. Click **Create and deploy**.

After the worker is deployed, proceed to [Add a route to your domain](#add-a-route-to-your-domain) to link the worker with your domain. Routing is not configured automatically and must be completed manually.

## Option 2: Manual setup

Follow these steps to create and configure the worker manually.

### Step 1: Create the Cloudflare Worker

1. Log in to your Cloudflare dashboard.
2. Navigate to **Workers & Pages** in the sidebar.
3. Click **Create application** and then **Create Worker**.
4. Name your worker (for example, `edge-optimize-router`).
5. Click **Deploy** to create the worker with the default code.

![Cloudflare Workers dashboard](/help/assets/optimize-at-edge/cloudflare-workers-dashboard.png)

### Step 2: Add the Worker code

After creating the worker, click **Edit code** and replace the default code with the code from [worker.js](https://github.com/adobe/llmo-code-samples/blob/main/optimize-at-edge/cloudflare/automation/src/worker.js). If you already have an existing Cloudflare Worker, merge the code with your existing worker code instead of replacing it entirely.

Click **Save and deploy** to publish the worker.

### Step 3: Configure environment variables and secrets

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

## Add a route to your domain {#add-a-route-to-your-domain}

Regardless of which setup option you used, you must manually link the worker to your domain. This step activates the worker on your traffic.

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

### Verifying failover behavior

If Edge Optimize is unavailable or returns an error, the worker automatically fails over to your origin. Failover responses include the `x-edgeoptimize-fo` header:

```
< HTTP/2 200
< x-edgeoptimize-fo: 1
```

You can monitor failover events in Cloudflare Workers logs to troubleshoot issues.

### Understanding the Worker logic

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

## Customizing the configuration

You can customize the worker behavior by modifying the configuration constants at the top of the code:

### Agentic bot list

Modify the `AGENTIC_BOTS` array to add or remove user agents:

```javascript
const AGENTIC_BOTS = [
  'AdobeEdgeOptimize-AI',
  'ChatGPT-User',
  'GPTBot',
  'OAI-SearchBot',
  'PerplexityBot',
  'Perplexity-User',
  'ClaudeBot',
  'Claude-User',
  'Claude-SearchBot',
  // Add additional user agents as needed
];
```

### Targeted paths

By default, all HTML pages are routed to Edge Optimize. To limit routing to specific paths, modify the `TARGETED_PATHS` array:

```javascript
// Route all HTML pages (default)
const TARGETED_PATHS = null;

// Or specify exact paths to route
const TARGETED_PATHS = ['/', '/page.html', '/products', '/about-us'];
```

### Failover configuration

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

### Important considerations

* **Failover behavior:** The worker automatically fails over to your origin if Edge Optimize returns any error (4XX or 5XX status codes) or if the request fails due to a network error. Failover uses `EDGE_OPTIMIZE_TARGET_HOST` as the origin domain (similar to Fastly's `F_Default_Origin` or CloudFront's `Default_Origin`). Failover responses include the `x-edgeoptimize-fo: 1` header, which you can use for monitoring and debugging.

* **Caching:** Cloudflare caches responses based on the URL by default. Because agentic traffic receives different content than human traffic, ensure your cache configuration accounts for this. Consider using Cache API or cache headers to differentiate cached content. The `x-edgeoptimize-config` header should be included in your cache key.

* **Rate limiting:** Monitor your Edge Optimize usage and consider implementing rate limiting for agentic traffic if needed.

* **Testing:** Always test the configuration in a staging environment before deploying to production. Verify that both agentic and human traffic behave as expected. Test failover behavior by simulating Edge Optimize errors.

* **Logging:** Enable Cloudflare Workers logging to monitor requests and troubleshoot issues. Navigate to **Workers** > **your worker** > **Logs** to view real-time logs. The worker logs failover events for debugging purposes.

## Troubleshooting

| Issue | Possible Cause | Solution |
|-------|----------------|----------|
| No `x-edgeoptimize-request-id` header in response | Worker route not matched, or user agent not in the agentic bots list. | Verify your route pattern matches the request URL. Check that the user agent is in the `AGENTIC_BOTS` array. |
| 401 or 403 errors from Edge Optimize | Invalid or missing API key. | Verify `EDGE_OPTIMIZE_API_KEY` is correctly set in environment variables and secrets. Contact Adobe to confirm your API key is active. |
| Infinite redirects or loops | Loop protection header not being set or checked correctly. | Ensure the `x-edgeoptimize-request` header check is in place. |
| Human traffic affected | Worker routing logic is too broad. | Verify the user agent matching logic is correct and case-insensitive. Check that `TARGETED_PATHS` is configured correctly. |
| Slow response times | Network latency to Edge Optimize backend. | This is expected for the first request; subsequent requests are cached at Edge Optimize. |
| `x-edgeoptimize-fo: 1` header in response | Edge Optimize returned an error and failover to origin occurred. | Check Cloudflare Workers logs for the specific error code. Verify Edge Optimize service status with Adobe. |
| Failover not working | Failover flags disabled, or error in failover logic. | Verify `FAILOVER_ON_4XX` and `FAILOVER_ON_5XX` are set to `true`. Check worker logs for error messages. |
| Certain paths not being optimized | Path not matching the targeted paths or HTML page pattern. | Verify the path is in `TARGETED_PATHS` (if specified) and matches the HTML page regex pattern. |
| Requests failing with invalid host | `EDGE_OPTIMIZE_TARGET_HOST` includes protocol (for example, `https://`). | Use only the domain name without protocol (for example, `example.com`, not `https://example.com`). |
| 530 error during failover | Cloudflare cannot connect to origin, or failover request has invalid headers. | Ensure the failover function removes Edge Optimize headers. Verify your origin is accessible and DNS is configured correctly. |

## Allow Optimize at Edge through firewall rules (optional)

{{waf-allowlist-setup}}

## Verify the setup

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

{{verify-routing-status-in-ui}}

{{return-to-overview}}
