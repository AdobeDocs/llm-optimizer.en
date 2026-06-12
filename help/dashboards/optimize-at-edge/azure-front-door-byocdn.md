---
title: Optimize at Edge - Azure Front Door (BYOCDN)
description: Learn how to configure Azure Front Door BYOCDN for Optimize at Edge in LLM Optimizer.
feature: Opportunities
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
    internal-label: LLM Optimizer
feature_v2:
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
    internal-label: Administration
subfeature_v2:
  - id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
    internal-label: CDN
---

# Azure Front Door (BYOCDN)

This configuration routes agentic traffic (requests from AI bots and LLM user agents) to the Edge Optimize backend service (`live.edgeoptimize.net`). Human visitors and SEO bots continue to be served from your origin as usual. To test the configuration, after the setup is complete, look for the header `x-edgeoptimize-request-id` in the response.

Azure Front Door does not run custom code at the edge. Instead, routing is configured declaratively using a **Rule Set** (which inspects the request and overrides the origin) together with a dedicated **origin group** for Edge Optimize. Failover is handled by Azure Front Door's priority-based origin group health probes rather than per-request logic.

**Prerequisites**

Before you set up the Azure Front Door routing rules, ensure you have:

* Access to your Azure Front Door (Standard or Premium) profile.
* An existing endpoint and route that serves your origin (the default origin group created with your profile).
* An Edge Optimize API key retrieved from the LLM Optimizer UI. For steps, see [Retrieve your API keys](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#production-api-key).
* (Optional) To test staging routing, see [Staging API key](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#staging-api-key-optional).

**How routing works**

When configured correctly, a request to your domain (for example, `www.example.com/page.html`) from an agentic user agent matches a rule in the `EORouting` rule set. The rule overrides the route's origin group to `edge-optimize-origin-group` and sets the required headers, so the request is sent to the Edge Optimize backend. All other traffic (human visitors, SEO bots, static assets) passes through to your default origin unchanged.

```
Agentic request ──▶ EORouting rule set ──▶ edge-optimize-origin-group
                                            │
                                            ├─ Priority 1: live.edgeoptimize.net  (optimized response)
                                            └─ Priority 2: www.example.com         (failover, re-enters rules → default origin)

Human / SEO / asset request ──▶ default-origin-group ──▶ your origin
```

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
| `x-forwarded-host` | The original host of the request. Set automatically by Azure Front Door from the origin group's **Origin host header**. | `www.example.com` |
| `x-edgeoptimize-url` | The original URL path and query string of the request. | `/page.html` or `/products?id=123` |
| `x-edgeoptimize-api-key` | The API key provided by Adobe for your domain. | `your-api-key-here` |
| `x-edgeoptimize-config` | Configuration string for cache key differentiation. | `LLMCLIENT=TRUE;` |

## Step 1: Create an origin group for Edge Optimize

Your Azure Front Door profile already has a default origin group that points to your origin. Create a **new** origin group for Edge Optimize.

In your Front Door profile, go to **Origin groups** > **Add an origin group** and configure it as follows:

* **Name:** `edge-optimize-origin-group`
* **Health probes:** **Enabled**
  * **Protocol:** HTTPS
  * **Path:** `/health/<your-domain>` (for example, `/health/www.example.com`)
  * **Probe method:** GET
  * **Interval:** 225 seconds
* **Session affinity:** **Disabled**

![Edge Optimize origin group with two priority-based origins and health probes](/help/assets/optimize-at-edge/azure-front-door-origin-group.png)

Add **two** origins to the group. Front Door uses the **Priority** value for failover: it always tries Priority 1 first, and only routes to Priority 2 if the Priority 1 origin is unhealthy.

**Origin 1 — Edge Optimize (Priority 1)**

* **Name:** `edge-optimize-origin`
* **Origin type:** Custom
* **Host name:** `live.edgeoptimize.net`
* **Origin host header:** `live.edgeoptimize.net`
* **Certificate subject name validation:** **Enabled**
* **Priority:** `1`

![Add the Priority 1 Edge Optimize origin](/help/assets/optimize-at-edge/azure-front-door-origin-priority1.png)

**Origin 2 — Your domain (Priority 2, failover)**

* **Name:** `your-domain-origin`
* **Origin type:** Custom
* **Host name:** your domain endpoint (for example, `www.example.com`)
* **Origin host header:** your domain (for example, `www.example.com`)
* **Certificate subject name validation:** **Enabled**
* **Priority:** `2`

This Priority 2 origin provides failover: if Edge Optimize is unhealthy, requests route to your domain, which re-enters Azure Front Door and is served from your default origin.

![Add the Priority 2 failover origin](/help/assets/optimize-at-edge/azure-front-door-origin-priority2.png)

>[!NOTE]
>
>The `edge-optimize-origin-group` origin group shows an **"Unassociated"** warning in the portal. This is expected — the group is referenced through a Rule Set route override (Step 3), not directly by a route.

## Step 2: Use your existing route

A default route is typically created with your Azure Front Door profile. The Rule Set in Step 3 overrides the origin group for agentic traffic, so you do **not** need to create a separate route for Edge Optimize. You associate the rule set with your existing route in Step 4.

## Step 3: Create the rule set

Go to **Rule sets** > **Add a rule set** and name it `EORouting`. Add three rules in the following order.

![EORouting rule set showing the header-stripping and bot-routing rules](/help/assets/optimize-at-edge/azure-front-door-ruleset-routing.png)

### Rule 1: StripIncomingEOHeaders01

This rule strips incoming Edge Optimize headers to prevent clients from spoofing them. It has **no conditions**, so it applies to all requests. Set **Stop evaluating remaining rules** to **Off**.

**Actions** — add a **Delete request header** action for each of the following headers:

* `x-edgeoptimize-api-key`
* `x-edgeoptimize-url`
* `x-edgeoptimize-config`
* `x-edgeoptimize-fetcher-key` (only required if you use a WAF — see [Allow Optimize at Edge through firewall rules](#allow-optimize-at-edge-through-firewall-rules-optional))

### Rule 2: EOGPTBotRootGET03

This rule routes agentic requests on HTML page paths to Edge Optimize. Set **Stop evaluating remaining rules** to **On**.

**Conditions** (all must match):

| Condition | Operator | Value | String transform |
|---|---|---|---|
| Request method | Equal | `GET` | — |
| Request path | RegEx | `(^$\|^.*/$\|(^\|.*/)[^./]+$\|^.*\.html$)` | — |
| Request header `User-Agent` | Contains | `chatgpt-user` `gptbot` `oai-searchbot` `adobeedgeoptimize-ai` `perplexitybot` `perplexity-user` `claudebot` `claude-user` `claude-searchbot` | To lowercase |
| Request header `x-edgeoptimize-monitor` | Not Contains | `1` | — |
| Request header `x-edgeoptimize-request` | Not Contains | `failover` `1` | — |

The Request path RegEx matches the site root, paths ending in `/`, extensionless page paths, and `.html` paths — so only HTML pages are routed and static assets (CSS, JS, images) always go to your origin.

>[!IMPORTANT]
>
>The **Contains** operator in Azure Front Door is case-sensitive. Set the **String transform** on the `User-Agent` condition to **To lowercase** and list the user agents in lowercase, as shown above, so that user-agent matching works regardless of case.

**Actions:**

| Action | Operator | Header / Field | Value |
|---|---|---|---|
| Request header | Overwrite | `x-edgeoptimize-url` | `/{url_path}?{query_string}` |
| Request header | Overwrite | `x-edgeoptimize-config` | `LLMCLIENT=TRUE;` |
| Request header | Overwrite | `x-edgeoptimize-api-key` | `YOUR_API_KEY` |
| Request header | Overwrite | `x-edgeoptimize-monitor` | `1` |
| Route configuration override | — | Origin group | `edge-optimize-origin-group` |
| Route configuration override | — | Forwarding protocol | Match incoming request |
| Route configuration override | — | Caching | **Disabled** |

The `x-edgeoptimize-monitor` header marks the request on its first pass through the rule engine. On the failover path (when the request re-enters Front Door from the Priority 2 origin), this header is already present, so the bot conditions no longer match and the request falls through to your default origin instead of looping back to Edge Optimize.

### Rule 3: HealthProbeRewrite02

This rule rewrites Azure Front Door health probe requests so they reach your origin as `/` instead of `/health/<domain>`. This lets Front Door monitor Edge Optimize availability without requiring a dedicated health endpoint on your origin. Set **Stop evaluating remaining rules** to **On**.

![Health probe rewrite rule](/help/assets/optimize-at-edge/azure-front-door-ruleset-healthprobe.png)

**Conditions** (all must match):

| Condition | Operator | Value |
|---|---|---|
| Request URL path | Begins With | `/health/` |
| Request header `x-fd-healthprobe` | Contains | `1` |

**Actions:**

| Action | Operator | Detail | Value |
|---|---|---|---|
| URL rewrite | — | Source pattern: `/health/`, Destination: `/`, Preserve unmatched path: No | — |
| Response header | Overwrite | `Origin-Health` | `Healthy` |
| Request header | Append | `user-agent` | ` AdobeEdgeOptimize/1.0` |
| Route configuration override | — | Origin group | `default-origin-group` |
| Route configuration override | — | Forwarding protocol | Match incoming request |
| Route configuration override | — | Caching | **Disabled** |

>[!NOTE]
>
>When you append the `user-agent` value, include a leading space (` AdobeEdgeOptimize/1.0`). Azure Front Door appends the value exactly as entered, so the leading space keeps it separated from the existing user-agent string. The `AdobeEdgeOptimize/1.0` user agent lets your origin and WAF identify health probe traffic.
>
>The `Origin-Health: Healthy` response header is a diagnostic that confirms the health probe rewrite is being applied. You can remove it after you verify the setup.

## Step 4: Associate the rule set with the route

Open your route, scroll to the **Rules** section at the bottom, and select the `EORouting` rule set from the dropdown. If you already have other rule sets, use **Move to top** to position `EORouting` at **#1**.

The Optimize at Edge rules only intercept agentic traffic and Edge Optimize loop-back requests — all other traffic passes through unaffected to your other rules.

Save the configuration and wait for it to propagate (approximately 20 minutes).

**Failover**

Azure Front Door handles failover through the priority-based origin group rather than per-request logic. When the Edge Optimize health probe (Priority 1) fails, Front Door routes agentic traffic to the Priority 2 origin (your domain endpoint), which re-enters the rule engine. Because the `x-edgeoptimize-monitor` header is already set from the first pass, the bot rule does not re-route the request, so it falls through to your default origin and the end-user still receives a response.

| Scenario | Behavior |
| --- | --- |
| Edge Optimize (Priority 1) healthy | Optimized response is served to the client. |
| Edge Optimize (Priority 1) unhealthy | Request routes to the Priority 2 origin and is served from your default origin. |

>[!NOTE]
>
>Failover on Azure Front Door is transparent — it is driven by origin group priority and health probes, not by per-request logic. Unlike code-based CDN integrations, Azure Front Door does **not** add an `x-edgeoptimize-fo` response header to failover responses. To confirm whether a response came from Edge Optimize, check for the `x-edgeoptimize-request-id` header.

**Allow Optimize at Edge through firewall rules (optional)** {#allow-optimize-at-edge-through-firewall-rules-optional}

{{waf-allowlist-setup}}

>[!NOTE]
>
>If you add an `x-edgeoptimize-fetcher-key` header in the routing rule (Rule 2), make sure the matching **Delete request header** action for `x-edgeoptimize-fetcher-key` is also present in the header-stripping rule (Rule 1) so that clients cannot spoof it.

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

>[!NOTE]
>
>Azure Front Door does not add an `x-edgeoptimize-fo` header on failover. Use the presence or absence of `x-edgeoptimize-request-id` to tell whether a response was served by Edge Optimize.

**Troubleshooting**

| Issue | Possible Cause | Solution |
|-------|----------------|----------|
| No `x-edgeoptimize-request-id` header in response | The rule set is not associated with the route, or the request did not match the bot conditions. | Confirm `EORouting` is associated with your route and positioned at #1. Verify the user agent is in the `User-Agent` condition and that **To lowercase** is set as the string transform. |
| Human traffic is being optimized | Bot conditions are too broad, or caching is enabled on the agentic rule. | Verify the `User-Agent` condition matches only agentic user agents. Ensure **Caching** is **Disabled** in the route configuration override for Rule 2 — Azure Front Door has no cache-key mechanism to separate bot and human responses. |
| Changes do not take effect | Configuration has not finished propagating. | Azure Front Door changes can take approximately 20 minutes to propagate. Wait and re-test. |
| 401 or 403 errors from Edge Optimize | Invalid or missing API key. | Verify the `x-edgeoptimize-api-key` value in Rule 2 matches the key from the LLM Optimizer UI. |
| Static assets (CSS, JS, images) are being routed to Edge Optimize | Request path RegEx is matching non-HTML paths. | Confirm the Request path RegEx in Rule 2 is `(^$\|^.*/$\|(^\|.*/)[^./]+$\|^.*\.html$)`. |
| Infinite loop or repeated routing | The loop-protection header is not being set or checked. | Verify Rule 2 sets `x-edgeoptimize-monitor` to `1` and includes the `x-edgeoptimize-monitor` (Not Contains `1`) and `x-edgeoptimize-request` (Not Contains `failover`, `1`) conditions. |
| Edge Optimize origin always shows unhealthy | Health probe path or rewrite rule is misconfigured. | Confirm the origin group health probe path is `/health/<your-domain>` and that Rule 3 (`HealthProbeRewrite02`) rewrites `/health/` to `/` and overrides the origin group to `default-origin-group`. |

>[!NOTE]
>
>**Cache isolation:** Azure Front Door has no mechanism (such as a Vary header or cache key) to separate bot and human cache entries. The agentic routing rule disables caching entirely to prevent optimized content from being served to human visitors.

{{verify-routing-status-in-ui}}

{{return-to-overview}}
