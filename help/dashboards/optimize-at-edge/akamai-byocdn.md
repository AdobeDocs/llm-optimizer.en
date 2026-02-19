---
title: Optimize at Edge - Akamai (BYOCDN)
description: Learn how to configure Akamai BYOCDN for Optimize at Edge in LLM Optimizer.
feature: Opportunities
---

# Akamai (BYOCDN)

This configuration routes agentic traffic (requests from AI bots and LLM user agents) to the Edge Optimize backend service (`live.edgeoptimize.net`). Human visitors and SEO bots continue to be served from your origin as usual. To test the configuration, after the setup is complete, look for the header `x-edgeoptimize-request-id` in the response.

**Prerequisites**

Before setting up the Akamai Property Manager rules, ensure you have:

* Access to Akamai Property Manager for your domain.
* Completed the LLM Optimizer onboarding process.
* Completed CDN log forwarding to LLM Optimizer.
* An Edge Optimize API key retrieved from the LLM Optimizer UI.

{{retrieve-byocdn-api-key}}

**Configuration**

The following Akamai Property Manager rule routes LLM user agents to Edge Optimize. The configuration includes the following steps:

**1. Set routing criteria (User-Agent matching)**

Set routing for the following user-agents:image.png

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

The Site Failover configuration has two parts: the failover behavior (configured inside the main optimize-at-edge routing rule) and a separate failover test header rule. 

**9a. Site Failover Behavior (inside the main optimize-at-edge routing rule)**

Inside the main routing rule, configure the Site Failover behavior and the Advanced XML snippet as follows:

![Site Failover](/help/assets/optimize-at-edge/akamai-step9-failover.png)

Add the request header `x-edgeoptimize-request` with value `fo` through Advanced XML: 

```
<forward:availability.fail-action2>
<add-header>
<status>on</status>
<name>x-edgeoptimize-request</name>
<value>fo</value>
</add-header>
</forward:availability.fail-action2>
```

![Failover Behaviors](/help/assets/optimize-at-edge/akamai-step9-failover-behaviors.png)

**9b. Failover Test Header rule (sibling rule)**

>[!IMPORTANT]
>
>Create the **EdgeOptimize Failover - Test Header** rule as a **sibling** (at the same level) of the routing rules — **not** nested inside them. In the Akamai Property Manager rule tree, the hierarchy should look like:
>
>```
>▼ Parent Rule
>  ▶ Optimize at Edge Routing     ← routing rule
>    EdgeOptimize Failover - Test Header       ← sibling, same level
>```
>
>This ensures the failover test header rule evaluates for **all** routing rules, not just one.

If the request header `x-edgeoptimize-request` value is `fo`, then set the outgoing response header `x-edgeoptimize-fo` to `true`.

![Failover Rules](/help/assets/optimize-at-edge/akamai-step9-failover-rules.png)

Site Failover ensures that if Edge Optimize returns a `4XX` or `5XX` error, the request is automatically routed back to your default origin so the end-user still receives a response.

| Scenario | Behavior |
| --- | --- |
| Edge Optimize returns `2XX` | Optimized response is served to the client. |
| Edge Optimize returns `4XX` or `5XX` | Request is routed back to the default origin. |

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
