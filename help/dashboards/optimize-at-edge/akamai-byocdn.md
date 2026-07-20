---
title: Optimize at Edge - Akamai (BYOCDN)
description: Learn how to configure Akamai BYOCDN for Optimize at Edge in LLM Optimizer.
feature: Opportunities
autotag-review: '2026-07-15T17:40:02.356Z'
TQID: 'https://experienceleague.adobe.com/XlHpXbtxqPl-XQQKWeQc3rbsizCT7U0TF1bQkyv0iM8'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
    internal-label: LLM Optimizer
feature_v2:
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
    internal-label: Administration
  - id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
    internal-label: Opportunities
  - id: ef4e63f5-cb4d-462d-bf9a-1f617edf2a3a
    internal-label: Optimize at edge
  - id: e0828736-236a-487b-a478-5a635455eadc
    internal-label: Traffic analytics
subfeature_v2:
  - id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
    internal-label: CDN log forwarding
  - id: e06fae5f-830b-4222-a469-b5e148d36465
    internal-label: Agentic traffic
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
---

# Akamai (BYOCDN)

This configuration routes agentic traffic (requests from AI bots and LLM user agents) to the Edge Optimize backend service (`live.edgeoptimize.net`). Human visitors and SEO bots continue to be served from your origin as usual. To test the configuration, after the setup is complete, look for the header `x-edgeoptimize-request-id` in the response.

**Prerequisites**

Before you set up the Akamai Property Manager rules, ensure you have:

* Access to Akamai Property Manager for your domain.
* An Edge Optimize API key retrieved from the LLM Optimizer UI. For steps, see [Retrieve your API keys](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#production-api-key).
* (Optional) To test staging routing, see [Staging API key](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#staging-api-key-optional).

**Configuration**

The following Akamai Property Manager rule routes agentic HTML page traffic to Edge Optimize. The configuration includes the following steps:

**1. Set routing criteria (User-Agent and HTML traffic matching)**

Set routing for the following user agents:

```
 *AdobeEdgeOptimize-AI*
 *ChatGPT-User*
 *GPTBot*
 *OAI-SearchBot*
 *PerplexityBot*
 *Perplexity-User*
 *ClaudeBot*
 *Claude-User*
 *Claude-SearchBot*
```

>[!NOTE]
>
>Apply the Optimize at Edge routing rule only to agentic HTML page traffic. A common setup is to use request-side criteria such as **File Extension** to match `html` and `EMPTY_STRING` for extensionless page URLs. If your site serves HTML from other URL patterns, or includes extensionless non-page routes such as API endpoints, refine the rule with additional path-based criteria.

![Set routing criteria](/help/assets/optimize-at-edge/akamai-step1-routing.png)

**2. Set Origin and SSL behavior**

Set origin as `live.edgeoptimize.net` and Match SAN to `*.edgeoptimize.net`

>[!NOTE]
>
>If property activation fails after you add the Optimize at Edge rule, check whether the rule uses a different Origin Server SSL verification mode than the default rule. If it does, update the Optimize at Edge rule to match the default rule. For example, if the default rule uses **Platform Settings**, use **Platform Settings** here as well. If you cannot use the required setting, contact Akamai support.

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

**Allow Optimize at Edge through firewall rules (optional)**

{{waf-allowlist-setup}}

![Set x-edgeoptimize-fetcher-key header in Property Manager](/help/assets/optimize-at-edge/akamai-step10-fetcher-key.png)

>[!NOTE]
>
>Also allowlist the `*AdobeEdgeOptimize/1.0*` user agent and the `x-edgeoptimize-fetcher-key` header in Akamai Bot Manager.

**6. Modify Incoming Response Headers**

![Modify Incoming Response Headers](/help/assets/optimize-at-edge/akamai-step6-response.png)

**7. Cache ID Modification**

![Cache ID Modification](/help/assets/optimize-at-edge/akamai-step7-cacheid.png)

**8. Modify Outgoing Request Headers**

Set `x-forwarded-host` header to `{{builtin.AK_HOST}}`

![Modify Outgoing Request Headers](/help/assets/optimize-at-edge/akamai-step8-outgoing-request.png)

**9. Site Failover**

The Site Failover configuration has two parts: a failover behavior inside the main Optimize at Edge routing rule and a sibling rule that adds a response header when fallback occurs.

**9a. Configure the Site Failover behavior**

Inside the main Optimize at Edge routing rule, create a child rule named **Site Failover Behavior**. Set it to **Match Any** and add these criteria:

* **Response Status Code** is in the range `400` through `599`.
* **Origin Timeout** is `Yes`.

![Site Failover](/help/assets/optimize-at-edge/akamai-step9-failover.png)

![Configure the Site Failover behavior](/help/assets/optimize-at-edge/akamai-step9-failover-settings.png)

**9b. Configure the failover response header rule**

>[!IMPORTANT]
>
>Create the **EdgeOptimize Failover - Test Header** rule as a **sibling** (at the same level) of the routing rules — **not** nested inside them. In the Akamai Property Manager rule tree, the hierarchy should look like:
>
>```
>▼ Optimize at Edge                         ← parent rule group
>  ▼ Optimize at Edge Routing               ← routing child
>    Site Failover Behavior                 ← nested child
>  EdgeOptimize Failover - Test Header      ← sibling of routing child
>```
>
>The sibling rule is evaluated when Akamai recreates the failed request for the original hostname. The API-key criterion on the routing rule prevents that request from being sent to Edge Optimize again.
>
>Also ensure the **Optimize at Edge Routing** rule is not overridden by any later matching rule that changes the origin, caching behavior, or cache ID for the same requests. If another matching rule resets these behaviors, Optimize at Edge routing or caching may not work as expected.

![Configure the failover response header rule](/help/assets/optimize-at-edge/akamai-step9-failover-header.png)

Site Failover ensures that if Edge Optimize returns an error or times out, Akamai recreates the request for your original hostname so the visitor still receives the site's normal response.

| Scenario | Behavior |
| --- | --- |
| Edge Optimize returns `2XX` or `3XX` | The optimized response is served. `x-edgeoptimize-request-id` is present. |
| Edge Optimize returns `4XX`–`5XX`, or the origin times out | The request is recreated for the original hostname. The response includes `x-edgeoptimize-fo: true`. |

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
| `x-edgeoptimize-fo` | Present only if failover occurred (value: `true`) | Absent |

{{verify-routing-status-in-ui}}

{{return-to-overview}}
