# Snippets

## API key retrieval steps {#retrieve-byocdn-api-key}

**Steps to retrieve your production Edge Optimize API key:**

1. In LLM Optimizer, open **Customer configuration** and select the **CDN configuration** tab.

   ![Navigate to Customer Configuration](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. In the **Deploy optimizations to AI agents** section, select **View details**.

3. In the **Deploy optimizations details** dialog, copy the **Production API key** (use **Copy** next to the field).

   >[!NOTE]
   >Until your CDN routing rules are fully deployed, the dialog may show that setup is not complete. This is expected. You can still copy the API key so your IT or CDN team can finish the configuration.

Additionally, if you require any help with the above steps, reach out to your Adobe account team or `llmo-at-edge@adobe.com`.

## Staging domain API key (optional) {#retrieve-staging-edge-optimize-api-key}

Use a staging hostname when you want to test Optimize at Edge in a lower environment before production traffic uses the routing rules.

**Prerequisites**

* The staging hostname must belong to the **same registrable domain** as your production site (for example, `https://staging.example.com` when production is `https://www.example.com`).
* Only **one** staging domain can be configured for the site. After it is saved, it cannot be changed without assistance.

**Steps**

1. In LLM Optimizer, open **Customer configuration** and select the **CDN configuration** tab.

2. In the **Deploy optimizations to AI agents** section, select **Add stage domain** (or **Stage domain** if a staging domain is already configured).

3. Enter the full staging URL, including `https://`, then confirm. When the workflow completes, copy the **API key** shown for the staging domain.

If you need help, contact `llmo-at-edge@adobe.com`.

## Return to overview {#return-to-overview}

To learn more about Optimize at Edge, including available opportunities, auto-optimization workflows, and FAQs, return to the [Optimize at Edge overview](/help/dashboards/optimize-at-edge/overview.md).
