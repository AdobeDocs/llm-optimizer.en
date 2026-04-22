# Snippets

## Check routing status in LLM Optimizer {#verify-routing-status-in-ui}

The status of the traffic routing can also be checked in the LLM Optimizer UI. Navigate to **Customer configuration** and select the **CDN configuration** tab.

![Deploy optimizations to AI agents — completed](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

## Allowing Optimize at Edge through firewall rules (optional) {#waf-allowlist-setup}

If your CDN uses a WAF or Bot Manager:

* Allowlist the `*AdobeEdgeOptimize/1.0*` user agent in your WAF or Bot Manager so the Optimize at Edge service can fetch your origin content.
* If your firewall requires additional verification beyond user agent, generate a secret (for example, `openssl rand -hex 32`) and:
  * Add `x-edgeoptimize-fetcher-key` with the secret in your routing rules alongside the other `x-edgeoptimize-*` headers.
  * Add a WAF or Bot Manager rule to allow requests where `x-edgeoptimize-fetcher-key` matches the same secret.
* Optimize at Edge forwards this header as-is — you own the full key lifecycle.

## Return to overview {#return-to-overview}

To learn more about Optimize at Edge, including available opportunities, auto-optimization workflows, and FAQs, return to the [Optimize at Edge overview](/help/dashboards/optimize-at-edge/overview.md).
