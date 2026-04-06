# Snippets

## API key retrieval steps {#retrieve-byocdn-api-key}

**Steps to retrieve your production Edge Optimize API key:**

1. In LLM Optimizer, open **Customer configuration** and select the **CDN configuration** tab.

   ![Navigate to Customer Configuration](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. Locate the **Deploy optimizations to AI agents** section. Until your IT or CDN team finishes the CDN configuration, the status shows **Pending**. Depending on your interface, you may see the **Enable optimization engine** checkbox on the card:

   ![Deploy optimizations to AI agents — pending with Enable optimization engine checkbox](/help/assets/optimize-at-edge/byocdn-deploy-optimizations-pending.png)

   Or you may see **+ Enable** and **Add stage domain** buttons:

   ![Deploy optimizations to AI agents — pending with Enable and Add stage domain buttons](/help/assets/optimize-at-edge/byocdn-deploy-optimizations-pending-actions.png)

3. To activate the optimization engine, select **+ Enable**. In the confirmation dialog, select **Enable**.

   ![Enable optimization engine confirmation dialog](/help/assets/optimize-at-edge/byocdn-enable-optimization-engine-dialog.png)

4. Select **View details**. In the **Deploy optimizations details** dialog, copy the **Production API key** (use **Copy** next to the field).

   ![Production API key in Deploy optimizations details](/help/assets/optimize-at-edge/byocdn-production-api-key-details.png)

   >[!NOTE]
   >The dialog may show that setup is not complete. This is expected until routing is verified — you can still copy the API key so your IT or CDN team can finish the configuration.

When routing is fully enabled, the status shows **Completed** and confirms that routing of AI bot traffic to LLM Optimizer is enabled.

![Deploy optimizations to AI agents with routing enabled](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

Additionally, if you require any help with the above steps, reach out to your Adobe account team or `llmo-at-edge@adobe.com`.

## Staging domain API key (optional) {#retrieve-staging-edge-optimize-api-key}

Use a staging hostname when you want to test Optimize at Edge in a lower environment before production traffic uses the routing rules.

**Prerequisites**

* The staging hostname must belong to the **same registrable domain** as your production site (for example, `https://staging.example.com` when production is `https://www.example.com`).
* Only **one** staging domain can be configured for the site. After it is saved, it cannot be changed without assistance.

**Steps**

1. In LLM Optimizer, open **Customer configuration** and select the **CDN configuration** tab.

2. In the **Deploy optimizations to AI agents** section, select **Add stage domain** (or **Stage domain** if a staging domain is already configured).

3. In the **Stage Domain** dialog, enter the full staging URL including `https://` and select **Set Domain**.

   ![Stage Domain input dialog](/help/assets/optimize-at-edge/byocdn-staging-domain-input.png)

4. Confirm the domain in the next prompt. When the workflow completes, the **Stage Domains** dialog shows the configured domain and its **API key**. Select **Copy** to copy the staging API key.

   ![Staging domain API key](/help/assets/optimize-at-edge/byocdn-staging-domain-api-key.png)

If you need help, contact `llmo-at-edge@adobe.com`.

## Return to overview {#return-to-overview}

To learn more about Optimize at Edge, including available opportunities, auto-optimization workflows, and FAQs, return to the [Optimize at Edge overview](/help/dashboards/optimize-at-edge/overview.md).
