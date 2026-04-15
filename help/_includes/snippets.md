# Snippets

## API key retrieval steps {#retrieve-byocdn-api-key}

**Steps to retrieve your production Edge Optimize API key:**

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

## Check routing status in LLM Optimizer {#verify-routing-status-in-ui}

The status of the traffic routing can also be checked in the LLM Optimizer UI. Navigate to **Customer configuration** and select the **CDN configuration** tab.

![Deploy optimizations to AI agents — completed](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

## Allowing Optimize at Edge through firewall rules (optional) {#waf-bypass-setup}

If your CDN uses a WAF or Bot Manager:

* Allowlist the `*AdobeEdgeOptimize/1.0*` user agent so the Optimize at Edge service can fetch your origin content.
* If your firewall requires additional verification, add the `x-edgeoptimize-fetcher-key` shared secret header in your routing rules alongside the other `x-edgeoptimize-*` headers.
* Generate a secret (for example, `openssl rand -hex 32`) and create a firewall rule to allow requests where the header matches your secret.
* Optimize at Edge forwards this header as-is — you own the full key lifecycle including rotation.
* To rotate, update both the firewall rule and routing rules. Accept both old and new keys temporarily to avoid downtime.

## Return to overview {#return-to-overview}

To learn more about Optimize at Edge, including available opportunities, auto-optimization workflows, and FAQs, return to the [Optimize at Edge overview](/help/dashboards/optimize-at-edge/overview.md).
