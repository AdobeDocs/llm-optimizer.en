---
title: Retrieve your API keys
description: How to retrieve your production and staging Edge Optimize API keys from LLM Optimizer.
feature: Opportunities
autotag-review: '2026-07-15T18:05:12.505Z'
TQID: 'https://experienceleague.adobe.com/X3vIzxrlaqJ5Mx3K8rOpX2QqgGyxT6p8qfdLzTWC1gQ'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
    internal-label: LLM Optimizer
feature_v2:
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
    internal-label: Administration
  - id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
    internal-label: Opportunities
subfeature_v2:
  - id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
    internal-label: CDN log forwarding
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
    internal-label: Customer experience
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
---

# Retrieve your API keys

Before configuring your CDN, retrieve your Edge Optimize API keys from LLM Optimizer UI. You need a **production** API key for live traffic. Optionally, you can also retrieve a **staging** API key to test routing on a staging hostname first.

## Production API key

1. In LLM Optimizer, open **Customer configuration** and select the **CDN configuration** tab.

   ![Navigate to Customer Configuration](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. Locate the **Deploy optimizations to AI agents** section. Tick the **Enable optimization engine** checkbox.

   ![Deploy optimizations to AI agents — pending](/help/assets/optimize-at-edge/byocdn-deploy-optimizations-pending.png)

3. In the confirmation dialog, select **Enable**.

   ![Enable optimization engine confirmation dialog](/help/assets/optimize-at-edge/byocdn-enable-optimization-engine-dialog.png)

4. Select **View details**. In the **Deploy optimizations details** dialog, copy the **Production API key** (use **Copy** next to the field).

   ![Production API key in Deploy optimizations details](/help/assets/optimize-at-edge/byocdn-production-api-key-details.png)

   >[!NOTE]
   >The dialog may show that setup is not complete. This is expected until routing is verified — you can still copy the API key so your IT or CDN team can finish the configuration.

If you require any help with the above steps, reach out to your Adobe account team or `llmo-at-edge@adobe.com`.

## Staging API key (optional)

To validate the routing in a lower environment before enabling production routing, you can configure a staging hostname.

**Requirements**

* The staging hostname must be on the **same registrable domain** as production (for example, `https://staging.example.com` when production is `https://www.example.com`).
* Only **one** staging domain per site. After it is saved, it cannot be changed without contacting Adobe.

**Steps**

1. In LLM Optimizer, open **Customer configuration** and select the **CDN configuration** tab.
2. Under **Deploy optimizations to AI agents**, select **Add stage domain** (or **Stage domain** if a staging domain is already configured).
3. Enter the full staging URL including `https://` and select **Set Domain**.
4. Copy the **staging** API key from the confirmation dialog.

   ![Staging domain API key](/help/assets/optimize-at-edge/byocdn-staging-domain-api-key.png)

Deploy the same routing rules on your staging environment using the staging API key.

If you need help, contact `llmo-at-edge@adobe.com`.

## Next steps

After retrieving your API keys, return to your [CDN setup guide](/help/dashboards/optimize-at-edge/overview.md#cdn-configuration-guides) to configure routing.
