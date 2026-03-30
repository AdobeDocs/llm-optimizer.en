---
title: Access control
description: "Learn how product-assigned and organizational users differ in Adobe LLM Optimizer, what read-only users see in the UI and how admins assign access in [!DNL Adobe Admin Console]."
feature: Customer Configuration
---

# Access control

[!DNL Adobe LLM Optimizer] supports basic access control based on user personas. This capability is available only to **paying customers** and is enabled upon request. It is not available for [Try Before You Buy](/help/overview/quick-start.md#try-before-you-buy) trial customers.

>[!IMPORTANT]
>
>To request access to this feature, paying customers should contact their Adobe account manager.

## Product-assigned users {#product-assigned-users}

If you are assigned to the product, you have the same capabilities as a standard organizational user, in addition to the following permissions::

* Write access in [Customer Configuration](/help/dashboards/customer-configuration.md) for prompts, categories, topics, and related settings.
* Deploy [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md) optimizations and manage suggestions.
* Manage Google Search Console configurations.
* Manage Optimize at Edge and CDN configurations.
* Onboard a new site.

## Organizational users {#organizational-users}

Organizational users are standard users who are **not** assigned to the product. If you are an organizational user, you have **read-only** access to the [LLM Optimizer dashboards](/help/dashboards/dashboards-overview.md) and related views. The following restrictions apply.

### Customer Configuration {#customer-configuration-restrictions}

* **[!UICONTROL Upload Prompts]** is disabled.
* Managing and editing prompts, categories, topics, and region is disabled.

  ![Customer Configuration restrictions for read-only users](/help/dashboards/assets/access-control-customer-configuration.png)

### CDN configuration (Customer Configuration) {#cdn-configuration-restrictions}

* **[!UICONTROL Onboard CDN]** is disabled (read-only users cannot add a CDN provider).
* **[!UICONTROL Delete CDN]** is disabled (read-only users cannot remove an existing CDN configuration).
* The **Submit** button in the CDN onboard dialog is disabled (read-only users cannot complete CDN setup).

  ![CDN configuration restrictions for read-only users](/help/dashboards/assets/access-control-cdn-configuration.png)

### Brand Presence — data insights {#brand-presence-restrictions}

* The **Delete** buttons next to topics are hidden (read-only users cannot remove topics from tracking).
* The **Delete** buttons next to prompts are hidden (read-only users cannot remove prompts from tracking).

  ![Brand Presence actions hidden for read-only users](/help/dashboards/assets/access-control-brand-presence.png)

### Agentic Traffic opportunities (error-page opportunities) {#agentic-opportunities}

For opportunities such as 404, 403, and 503 error pages:

* **[!UICONTROL Deploy Optimization]** is hidden.
* An informational alert explains that deploy access is required.

  ![Deploy Optimization hidden on Agentic Traffic opportunities](/help/dashboards/assets/access-control-agentic-deploy.png)

### Other opportunity detail pages {#other-opportunities}

Read-only behavior also applies to opportunity types such as:

* Table of contents
* Summarization
* Readability
* Prerender
* Headings
* FAQ
* Missing structured data
* Generic patch opportunity

For these pages:

* **[!UICONTROL Deploy Optimization]** is hidden when the user does not have deploy access.
* An inline alert explains that deploy access is required. The message is similar to: *Deploy Access Required — You don't have permission to deploy optimizations or manage suggestions. Please contact your administrator to request access.*
* The sticky bottom bar with deploy actions is hidden.

  ![Inline alert when deploy access is required](/help/dashboards/assets/access-control-deploy-alert.png)

  ![Optimize at Edge deploy actions hidden for read-only users](/help/dashboards/assets/access-control-optimize-at-edge.png)

### Google Search Console prompt configuration {#gsc-restrictions}

* Manage and connect actions are disabled or hidden.
* The actions column used to add prompts is hidden.

  ![Google Search Console configuration restrictions](/help/dashboards/assets/access-control-gsc.png)

### Onboard a new site {#onboarding-restrictions}

* Onboarding a new site is disabled for users without access control.

  ![Onboard new site disabled](/help/dashboards/assets/access-control-onboarding.png)

## Assign the product to a user or group {#assign-product}

A **system administrator** for your organization can use the [[!DNL Adobe Admin Console]](https://adminconsole.adobe.com/) to assign [!DNL Adobe LLM Optimizer] to a user or group.

1. Sign in to the [[!DNL Adobe Admin Console]](https://adminconsole.adobe.com/) with an account that has administrative rights for your organization.
1. Assign the [!DNL Adobe LLM Optimizer] product profile (or your organization's equivalent product entitlement) to the user or group that should receive product-assigned capabilities.

For detailed steps, see [Managing products in the Admin Console](https://helpx.adobe.com/enterprise/using/manage-products.html) and [Manage user groups](https://helpx.adobe.com/enterprise/using/user-groups.html).

>[!NOTE]
>
>Screen flows in [!DNL Adobe Admin Console] can change between releases. If the options above do not match your console, use the in-product help links in [!DNL Adobe Admin Console] or contact your Adobe account team.
