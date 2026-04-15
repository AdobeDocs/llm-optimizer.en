---
title: Optimize at Edge - AEM Cloud Service Managed CDN (Fastly)
description: Learn how to configure the AEM Cloud Service Managed CDN (Fastly) for Optimize at Edge in LLM Optimizer.
feature: Opportunities
---

# AEM Cloud Service Managed CDN (Fastly)

This configuration routes agentic traffic (requests from AI bots and LLM user agents) to the Edge Optimize backend service (`live.edgeoptimize.net`). Human visitors and SEO bots continue to be served from your origin as usual. To test the configuration, after the setup is complete, check for the header `x-edgeoptimize-request-id` in the response.

**Prerequisites**

To access this feature:  
- Paid customers must have access to the **Adobe LLM Optimize Users** IMS Product Profile.
- Trial customers must be part of the **LLMO Admin** IMS group.

>[!NOTE]
> This feature is not supported in Safari or in incognito/private browsing modes.

**Steps to Enable Routing**

To start routing agentic traffic to Edge Optimize:

1. In LLM Optimizer, open **Customer configuration** and select the **CDN configuration** tab.

   ![Navigate to Customer Configuration](/help/assets/optimize-at-edge/cs-fastly-prereq-customer-config-nav.png)

2. Locate the **Deploy optimizations to AI agents** section. Click the **Enable** button.

   ![Deploy optimizations to AI agents — pending](/help/assets/optimize-at-edge/cs-fastly-enable-button.png)

3. In the confirmation dialog, select **Enable** to confirm that you want to enable routing. If an error appears, refer to the [Troubleshooting](#troubleshooting) section to resolve it.

   ![Enable optimization engine confirmation dialog](/help/assets/optimize-at-edge/cs-fastly-enable-dialog.png)

4. Once confirmed, the routing takes a few minutes to complete.

   ![Routing in progress](/help/assets/optimize-at-edge/cs-fastly-enable-button-clicked-routing-in-progress.png)

   Reload the page after 5 minutes to verify that routing is complete. Once the routing is configured and active, the status updates to **Completed** with a green checkmark confirming that routing is enabled. No further action is required on your end.

   ![Deploy optimizations to AI agents — completed](/help/assets/optimize-at-edge/cs-fastly-disable-button.png)

   To disable routing at any time, return to the **Deploy optimizations to AI agents** section in the **CDN configuration** tab and click **Disable**.

Additionally, if you require any help with the above steps, reach out to your Adobe account team or `llmo-at-edge@adobe.com`.

**Troubleshooting**

If an error appears while enabling or disabling routing, it will look similar to the following:

![Confirmation Dialog Error](/help/assets/optimize-at-edge/cs-fastly-confirmation-dialog-error.png)

Use the list below to identify the error and follow the directions.

1. **User does not have LLMO product access**

   **Cause:** The user account does not have the LLM Optimizer product context in your Adobe IMS profile. This is required for paid customers to configure CDN routing.

   **Recommendation:** Verify that you have been assigned the **Adobe LLM Optimize Users** Product Profile in Adobe Admin Console by your Org Admin.

2. **Only LLMO Admin group members can configure CDN routing**

   **Cause:** Your account is not a member of the **LLMO Admin** IMS group. This is required for trial customers to configure CDN routing.

   **Recommendation:** Verify that you have been added to **LLMO Admin** IMS Group in Adobe Admin Console by your Org Admin.

3. **Requested CDN type aem-cs-fastly does not match the detected CDN for this domain**

   **Cause:** This indicates the CDN type detected for your site is not *AEM Cloud Service Managed CDN (Fastly)*.

   **Recommendation:** Verify that your site is served through AEM Cloud Service Managed CDN (Fastly).

4. **Error probing site**

   **Cause:** LLM Optimizer was unable to reach your site during the routing setup. This can happen if the site is down, unreachable, or the request timed out.

   **Recommendation:** Verify that your site is publicly accessible and returning a valid response, then try again.

5. **Site did not return a valid response for the routing probe**

   **Cause:** The site returned an unexpected HTTP status (not 2xx or 301) when probed during setup.

   **Recommendation:** Verify your site is returning a successful response (2xx) for the base URL registered in LLM Optimizer, then try again.

6. **Authentication failed with upstream IMS service**

   **Cause:** The session might have expired or there was an issue authenticating with Adobe IMS during the routing request.

   **Recommendation:** Log out of LLM Optimizer and log back in, then try enabling routing again.

If the issue persists, reach out to your Adobe account team or `llmo-at-edge@adobe.com`.

**(Optional) Verify the Setup**

After the routing configuration is complete, you can optionally verify that bot traffic is being routed to Edge Optimize and that human traffic remains unaffected.

1. **Test bot traffic (should be optimized)**

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

2. **Test human traffic (should NOT be affected)**

   Simulate a regular human browser request:

   ```
   curl -svo /dev/null https://www.example.com/page.html \
     --header "user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36"
   ```

   The response should not contain the `x-edgeoptimize-request-id` header. The page content and response time should remain identical to before enabling Optimize at Edge.

3. **How to differentiate between the two scenarios**

   | Header | Bot traffic (optimized) | Human traffic (unaffected) |
   |---|---|---|
   | `x-edgeoptimize-request-id` | Present — contains a unique request ID | Absent |
   | `x-edgeoptimize-fo` | Present only if failover occurred (value: `1`) | Absent |

4. **Check routing status in LLM Optimizer**

   You can also confirm routing in the LLM Optimizer UI. Open **Customer configuration** and select the **CDN configuration** tab. When routing is active, the **Deploy optimizations to AI agents** section shows **Completed**.

   ![Deploy optimizations to AI agents — completed](/help/assets/optimize-at-edge/cs-fastly-disable-button.png)

{{return-to-overview}}
