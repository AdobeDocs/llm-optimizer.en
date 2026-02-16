---
title: Optimize at Edge - Fastly (BYOCDN)
description: Learn how to configure Fastly BYOCDN for Optimize at Edge in LLM Optimizer.
feature: Opportunities
---

# Fastly (BYOCDN)

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

After completing the setup, [verify the configuration](/help/dashboards/optimize-at-edge.md#verify-the-setup) to confirm that traffic is being routed correctly.
