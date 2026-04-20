---
title: Retrieve your API keys
description: How to retrieve your production and staging Edge Optimize API keys from LLM Optimizer.
feature: Opportunities
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

Use a staging hostname when you want to test Optimize at Edge in a lower environment before production traffic uses the routing rules.

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
