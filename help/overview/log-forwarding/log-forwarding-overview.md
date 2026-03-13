---
title: CDN Log Forwarding Overview
description: Learn how to forward CDN logs from your provider to Adobe's S3 bucket for agentic traffic data collection in LLM Optimizer.
feature: Agentic Traffic
---

# CDN Log Forwarding Overview {#cdn-log-forwarding}

CDN log forwarding is the process of sending your CDN access logs to Adobe's Amazon S3 bucket so that LLM Optimizer can collect and analyze agentic traffic data. Without CDN log forwarding, the [Agentic Traffic](/help/dashboards/agentic-traffic.md) dashboard cannot display metrics.

The guides provided below, follow the same two-phase workflow:

1. **Onboard in LLM Optimizer** — register your CDN on the [CDN Configuration](/help/dashboards/customer-configuration.md) page to generate the S3 credentials and path details you need.
2. **Configure your CDN** — use those details to create a log-forwarding job (or upload logs manually) in your CDN provider's console.

## CDN providers {#cdn-providers}

Follow the corresponding guide for you CDN provider.

| CDN Provider | Guide |
|---|---|
| Akamai | [View setup guide](/help/overview/log-forwarding/akamai.md) |
| Cloudflare | [View setup guide](/help/overview/log-forwarding/cloudflare.md) |
| CloudFront | [View setup guide](/help/overview/log-forwarding/cloudfront.md) |
| Fastly | [View setup guide](/help/overview/log-forwarding/fastly.md) |
| Imperva | [View setup guide](/help/overview/log-forwarding/imperva.md) |
| Other (manual / unsupported CDN) | [View setup guide](/help/overview/log-forwarding/other.md) |

>[!NOTE]
>
>If your CDN provider is not listed above, use the **Other (manual / unsupported CDN)** guide, which covers manual uploads, ad-hoc scripts and any CDN that is not natively supported.
