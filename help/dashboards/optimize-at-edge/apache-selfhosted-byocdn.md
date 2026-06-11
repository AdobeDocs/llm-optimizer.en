---
title: Optimize at Edge - Apache HTTP Server / Self-Hosted (BYOCDN)
description: Learn how to configure Apache HTTP Server (self-hosted reverse proxy) BYOCDN for Optimize at Edge in LLM Optimizer.
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

# Apache HTTP Server / Self-Hosted (BYOCDN)

This configuration applies when Apache HTTP Server acts as the reverse proxy in front of your origin (a self-hosted setup, **without** AEM Dispatcher). It routes agentic traffic (requests from AI bots and LLM user agents) to the Edge Optimize backend service (`live.edgeoptimize.net`). Human visitors and SEO bots continue to be served from your origin as usual. To test the configuration, after the setup is complete, look for the header `x-edgeoptimize-request-id` in the response.

The integration is a set of native Apache `Include` files — there is no code or worker to deploy. You download three files, set your API key, and add two `Include` lines to your virtual host.

**Prerequisites**

Before you set up the Apache routing rules, ensure you have:

* Apache HTTP Server 2.4 or later with these modules enabled: `proxy`, `proxy_http`, `ssl`, `rewrite`, `headers`, `env`, and `setenvif`.
* Access to your Apache configuration (the `<VirtualHost>` for your site) and the ability to reload Apache.
* An Edge Optimize API key retrieved from the LLM Optimizer UI. For steps, see [Retrieve your API keys](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#production-api-key).
* (Optional) To test staging routing, see [Staging API key](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#staging-api-key-optional).

## Configuration

**1. Download the configuration files**

Download the three Edge Optimize include files from the [Optimize at Edge code samples repository](https://github.com/adobe/llmo-code-samples/tree/main/optimize-at-edge/apache) and place them in a directory on your Apache server (for example, `conf/oae/`):

| File | Purpose |
|------|---------|
| `oae-routing.conf` | Detects AI bots, injects the Edge Optimize headers, routes HTML page requests to the backend, and sets up cache isolation and failover. |
| `oae-failover.conf` | Replays the original request against your origin if Edge Optimize returns an error. |
| `domains.conf` | Enables Optimize at Edge per domain and holds your API key. |

You do not need to modify `oae-routing.conf` or `oae-failover.conf` — use them as-is.

**2. Enable your domain and set the API key (`domains.conf`)**

Edit `domains.conf` and add one line per domain you are enabling. Replace the host with your domain and `YOUR_API_KEY` with the key from the LLM Optimizer UI. Domains not listed route to origin unchanged, so you can enable one domain at a time.

```
SetEnvIfExpr "%{HTTP_HOST} =~ m#(?i)^(www\.)?example\.com(:\d+)?$#" OAE_DOMAIN_ENABLED=1 OAE_API_KEY=YOUR_API_KEY
```

**3. Include the files in your virtual host**

Add the two `Include` lines to your existing `<VirtualHost *:443>`. The routing file goes **before** your rewrite and `ProxyPass` rules; the failover file goes **after** them. In the example below, lines marked `#NEWLINE` are the only lines you add for Optimize at Edge — everything else (`ServerName`, `ProxyPass`, and the rest) is your existing, unchanged configuration.

```
Define OAE_CONF_DIR conf/oae                       #NEWLINE  directory holding the OAE include files

<VirtualHost *:443>
    ServerName www.example.com

    Include "${OAE_CONF_DIR}/oae-routing.conf"     #NEWLINE  OAE routing — BEFORE your Rewrite & ProxyPass rules

    # --- your existing rewrite rules and ProxyPass to origin ---
    ProxyPass        "/" "https://www.example.com/"
    ProxyPassReverse "/" "https://www.example.com/"

    Include "${OAE_CONF_DIR}/oae-failover.conf"    #NEWLINE  OAE failover — AFTER your ProxyPass rules
</VirtualHost>
```

**4. Reload Apache**

Validate the configuration and reload Apache to apply the changes.

>[!NOTE]
>
>Bot-optimized and human responses are kept in separate cache entries automatically (the routing file sets `Vary: x-edgeoptimize-config`). If your Apache already uses `mod_cache`, ensure it has `CacheQuickHandler Off` so the cache lookup runs after the Edge Optimize headers are set.

**Allow Optimize at Edge through firewall rules (optional)**

{{waf-allowlist-setup}}

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

{{verify-routing-status-in-ui}}

{{return-to-overview}}
