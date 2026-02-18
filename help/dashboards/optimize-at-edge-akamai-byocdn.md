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

{{verify-setup-byocdn}}

{{return-to-overview}}
