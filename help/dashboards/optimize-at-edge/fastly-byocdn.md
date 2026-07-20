---
title: Optimize at Edge - Fastly (BYOCDN)
description: Learn how to configure Fastly BYOCDN for Optimize at Edge in LLM Optimizer.
feature: Opportunities
autotag-review: '2026-07-15T17:50:43.991Z'
TQID: 'https://experienceleague.adobe.com/Ueis3UcuGZz19FUJavq44dF3q3Irz2Ri4s7JTCB-H80'
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

# Fastly (BYOCDN)

This configuration routes agentic traffic (requests from AI bots and LLM user agents) to the Edge Optimize backend service (`live.edgeoptimize.net`). Human visitors and SEO bots continue to be served from your origin as usual. To test the configuration, after the setup is complete, look for the header `x-edgeoptimize-request-id` in the response.

## Prerequisites

Before you set up the Fastly VCL rules, ensure you have:

* Access to Fastly for your domain.
* An Edge Optimize API key retrieved from the LLM Optimizer UI. For steps, see [Retrieve your API keys](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#production-api-key).
* (Optional) To test staging routing, see [Staging API key](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#staging-api-key-optional).

## Configuration

Add the following three VCL snippets to your Fastly service. These snippets handle routing agentic requests to Edge Optimize, cache-key separation, and failover to your default origin.

![Fastly backend configuration](/help/assets/optimize-at-edge/fastly-backend-config.png)

![Add VCL snippets](/help/assets/optimize-at-edge/add-vcl-snippets.png)

### vcl_recv snippet

```
unset req.http.x-edgeoptimize-url;
unset req.http.x-edgeoptimize-config;
unset req.http.x-edgeoptimize-api-key;
unset req.http.x-edgeoptimize-fetcher-key; # Optional (required only in case of WAF)

if (!req.http.x-edgeoptimize-request
    && req.http.user-agent ~ "(?i)(AdobeEdgeOptimize-AI|ChatGPT-User|GPTBot|OAI-SearchBot|PerplexityBot|Perplexity-User|ClaudeBot|Claude-User|Claude-SearchBot)") {
  set req.http.x-forwarded-host = req.http.host; # required for identifying the original host
  set req.http.x-edgeoptimize-url = req.url; # required for identifying the original url
  set req.http.x-edgeoptimize-config = "LLMCLIENT=TRUE;"; # required for cache key
  set req.http.x-edgeoptimize-api-key = "<YOUR API KEY>"; # required for identifying the client
  set req.http.x-edgeoptimize-fetcher-key = "<YOUR FETCHER KEY>"; # Optional (required only in case of WAF)
  set req.backend = F_EDGE_OPTIMIZE;
  return(lookup);
}
```

### vcl_hash snippet

```
if (req.http.x-edgeoptimize-config) {
  set req.hash += "edge-optimize";
  set req.hash += req.http.x-edgeoptimize-config;
}
```

### vcl_deliver snippet

```
if (req.http.x-edgeoptimize-config && resp.status >= 400) {
  set req.http.x-edgeoptimize-request = "failover";
  restart;
}

if (req.http.x-edgeoptimize-config) {
  return(deliver);
}

if (!req.http.x-edgeoptimize-config && req.http.x-edgeoptimize-request == "failover") {
  set resp.http.x-edgeoptimize-fo = "1";
}
```

### Failover

The `vcl_deliver` snippet handles failover automatically. If Edge Optimize returns a `4XX` or `5XX` error, the request is restarted and routed back to your default origin so the end-user still receives a response. Failover responses include the `x-edgeoptimize-fo: 1` header.

| Scenario | Behavior |
| --- | --- |
| Edge Optimize returns `2XX` | Optimized response is served to the client. |
| Edge Optimize returns `4XX` or `5XX` | Request is restarted and served from the default origin. |
| Failover response | Includes the header `x-edgeoptimize-fo: 1`. |

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
