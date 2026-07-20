---
title: BYOCDN Log Forwarding Overview
description: Learn how to forward CDN logs from your provider to Adobe's S3 bucket for agentic traffic data collection in LLM Optimizer.
feature: Agentic Traffic
autotag-review: '2026-07-15T18:07:52.453Z'
TQID: 'https://experienceleague.adobe.com/iN1Tm-7j2FTQ1UodWvCZpOSy0FnQEyMkBMZIL9z3t38'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
    internal-label: LLM Optimizer
feature_v2:
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
    internal-label: Administration
  - id: ef4e63f5-cb4d-462d-bf9a-1f617edf2a3a
    internal-label: Optimize at edge
  - id: e0828736-236a-487b-a478-5a635455eadc
    internal-label: Traffic analytics
subfeature_v2:
  - id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
    internal-label: CDN log forwarding
  - id: dd952468-5202-43af-a365-6e0d2e67a703
    internal-label: BYOCDN
  - id: e06fae5f-830b-4222-a469-b5e148d36465
    internal-label: Agentic traffic
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
---

# BYOCDN Log Forwarding Overview {#cdn-log-forwarding}

Log forwarding for a customer managed CDN (BYOCDN) is the process of sending your CDN access logs to Adobe's Amazon S3 bucket so that LLM Optimizer can collect and analyze agentic traffic data. Without CDN log forwarding, the [Agentic Traffic](/help/dashboards/agentic-traffic.md) dashboard cannot display metrics.

The guides provided below, follow the same two-phase workflow:

1. **Onboard in LLM Optimizer** — register your CDN on the [CDN Configuration](/help/dashboards/customer-configuration.md) page to generate the needed S3 credentials and path details.
2. **Configure your CDN** — use those details to create a log-forwarding job (or upload logs manually) in your CDN provider's console. For CloudFront, you can use the console or complete delivery setup with the **AWS CLI** only; see [CloudFront (AWS CLI)](/help/overview/log-forwarding/cloudfront-cli.md).

## CDN providers {#cdn-providers}

Follow the corresponding guide for you CDN provider.

| CDN Provider | Guide |
|---|---|
| Akamai | [View guide](/help/overview/log-forwarding/akamai.md) |
| Cloudflare | [View guide](/help/overview/log-forwarding/cloudflare.md) |
| CloudFront (console) | [View guide](/help/overview/log-forwarding/cloudfront.md) |
| CloudFront (AWS CLI) | [View guide](/help/overview/log-forwarding/cloudfront-cli.md) |
| Fastly | [View guide](/help/overview/log-forwarding/fastly.md) |
| Imperva | [View guide](/help/overview/log-forwarding/imperva.md) |
| Other (manual / unsupported CDN) | [View guide](/help/overview/log-forwarding/other.md) |

>[!NOTE]
>
>If your CDN provider is not listed above, use the **Other (manual / unsupported CDN)** guide which covers manual uploads, ad-hoc scripts and any CDN that is not natively supported.
