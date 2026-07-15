---
title: Quick Start
description: Learn how to onboard your brand name and domain, activate your trial from Experience Hub or Experience Cloud and complete the setup for Adobe LLM Optimizer.
feature: Quickstart, Onboarding
autotag-review: '2026-07-15T18:07:16.514Z'
TQID: 'https://experienceleague.adobe.com/Hp5j1st4fkfiBVKTTL-eHQX6Ovmw61-2hX2g1T8Ui8Y'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
    internal-label: LLM Optimizer
feature_v2:
  - id: a080bb92-ba2a-4e53-ba60-f5184d1a9e9a
    internal-label: Getting started
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
    internal-label: Administration
subfeature_v2:
  - id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
    internal-label: CDN log forwarding
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
  - id: d00e9f03-e50b-4162-b143-0c0817c937c2
    internal-label: Customer journeys
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
---

# Quick Start

To get started with LLM Optimizer, complete the onboarding process. Then customize categories, topics, and prompts, configure CDN log forwarding and open the [dashboards](/help/dashboards/dashboards-overview.md) for fuller insights.

<!--Where steps differ by layout, use **Customer Configuration (classic experience)** or **Brands Management** / **Prompts Management**, whichever matches your current interface.-->

## Brand Centric experience {#brand-centric-experience}

By default, customers start in a focused, brand-first interface with onboarding-driven setup. In this interface, each organization starts with one active brand and additional suggested brands to choose from. <!--Existing LLM Optimizer customers will shift to this Brand Centric experience gradually.-->

## Onboarding overview

The onboarding process starts with onboarding your domain and your brand name. Each part of the onboarding journey is detailed below along with helpful tips on how to get started with LLM Optimizer as soon as possible.

### Allowing Adobe LLM Optimizer to access public pages

To deliver accurate content and technical recommendations, Adobe LLM Optimizer requires access to your public-facing pages. This is achieved through a secure internal crawler (Spacecat/1.0 user agent).

Configuration requirements:

* Add the Spacecat/1.0 user agent to the Allowlist in your site's robots.txt file or bot-traffic management rules.
* Ensure that pages are not blocked either at the domain or CDN level. Blocked pages cannot be indexed, which means optimization tasks and insights cannot be generated for them.

If content visibility appears low in the dashboard, verify that the crawler has access to your domains. Restricted access is a common cause of incomplete indexing.

## Step 1: Onboard your brand name and domain {#step-1-onboard-your-domain}

To get started with LLM Optimizer, first activate your trial (if eligible) and onboard your brand name and domain.

### Activate your trial

The activation flow differs depending on your Adobe product.

#### AEM Cloud customers

To activate your trial, as an AEM Cloud customer, you can either:

* Navigate to [Experience Hub](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/experience-hub/experience-hub) and use the Product Announcement card to activate LLM Optimizer. After you select **Try LLM Optimizer**, you are redirected to [https://llmo.now](https://llmo.now). Sign in through IMS, then enter a domain and brand name to start the onboarding process.
* Or go directly to [https://llmo.now](https://llmo.now) and sign in.

![LLM Optimizer Trial](/help/overview/assets/llm-trial.png)

#### Adobe Analytics and Adobe Customer Journey Analytics

For Adobe Analytics and Adobe Customer Journey Analytics customers, you will see a banner on the Experience Cloud home page.

![Experience Cloud home page with Start your Adobe LLM Optimizer Trial banner](/help/overview/assets/experience-cloud-llmo-trial-banner.png)

You can activate your trial in one of the following ways:

* Select **Start your Adobe LLM Optimizer Trial** in the banner.
* Go directly to [https://llmo.now](https://llmo.now) and sign in.

Once the trial is active, proceed with onboarding your brand name and domain.

>[!NOTE]
>
> * **Free trial:** AEM Cloud and Adobe Analytics/Customer Journey Analytics customers can use the free trial version of LLM Optimizer.
> * **Customers who activate the trial on or after April 1, 2026** can use up to 100 prompts, one domain, and can deploy optimizations across up to 10 URLs for a single opportunity type.
> * **Customers who activated the trial before April 1, 2026** continue to have access to up to 200 prompts under their existing terms.
>
>Use beyond the included limits requires a separate license agreement. Access is provided on an "as-is" and "as-available" basis, and may be modified, limited or removed at any time. Contact your account representative for more information.

#### Onboard your brand name and domain

Onboard your brand name and domain to begin using LLM Optimizer.

1. Enter your brand name and the associated domain.

   * This should be the main domain where you want to analyze and optimize content.

1. Complete onboarding.

   * Once submitted, LLM Optimizer begins analyzing your domain and generating insights.

![LLM Optimizer domain](/help/overview/assets/domain.png)

>[!NOTE]
>Newly added prompts will not appear in the [Brand Presence Dashboard](/help/dashboards/brand-presence.md) until processing is complete.

>[!NOTE]
>The domain you provided will be used by everyone from your organization and cannot be changed.

A small set of categories, topics and prompts will be generated during the onboarding phase. Brand Presence Analysis on those prompts will be available shortly after your site has been onboarded.

The ability to deploy optimizations at edge is also available. Learn more in [Optimize at Edge — Frequently asked questions](https://experienceleague.adobe.com/en/docs/llm-optimizer/using/resources/optimize-at-edge/overview#frequently-asked-questions).

Additionally, configure [CDN log forwarding](#step-4) for traffic analysis. LLM Optimizer requires Brand Presence data and insights from agentic and referral traffic to identify opportunities and provide prescriptive recommendations that boost AI visibility.

### Non-AEM Cloud customers

After your organization finalizes the business agreement, you are onboarded to LLM Optimizer with the domain your organization selected. When onboarding finishes, sign in at [https://llmo.now](https://llmo.now).

## Step 2: Customize Categories, Topics, and Prompts {#step-2-customize-categories-topics-and-prompts}

Once your site has been onboarded, you can view the Brand Presence Analysis based on the small set of prompts that were automatically generated during the onboarding phase. Moving forward, you can customize categories, topics, and prompts for your brand.

### Brand Centric experience categories, topics, and prompts

You can add categories, topics, and prompts as follows:

* **Categories** — Navigate to **Brands Management** and click **Categories**. Categories are defined at a global level and apply to all brands under Brands Management.

  ![Brands Management with Categories in the navigation](/help/assets/brand-centric-experience/llmo-app-shell.png)

* **Topics and prompts** — Navigate to **Prompts Management** to create topics and prompts, including prompts for a specific brand.

  ![Prompts Management](/help/assets/brand-centric-experience/prompts-management.png)

>[!NOTE]
>The exact prompts you ask LLMs are not publicly available because they are not disclosed by the LLMs.

>[!NOTE]
>
> For more details on how to set up your categories, topics, prompts see the [Best practices for configuring categories, topics, prompts](/help/overview/best-practices-topics-prompts.md) page.

## Step 3: Brand Presence Insights

After your domain has been onboarded, you will see initial insights in the Brand Presence view based on the prompts that were automatically generated during onboarding. Once you customize your own categories, topics, and prompts, LLM Optimizer will automatically trigger the Brand Presence analysis on the prompts you provided and results will be available in 24 hours.

Navigate to **Brand Presence** and select a brand that you want to view Brand Presence for using the brand dropdown. You can also view the brand visibility at an **All Brands** level with this experience.

## Step 4: Provide information for CDN Log Forwarding {#step-4}

To unlock Agentic Traffic and Referral Traffic insights, register CDN log forwarding so LLM Optimizer can read your access logs.

### CDN Log Forwarding

You can add CDN log forwarding information from **Brands Management** as follows: open **Brands Management** and click the **CDN** label.

![Brands Management — CDN log forwarding](/help/assets/brand-centric-experience/brands-management-cdn.png)

>[!NOTE]
>For details regarding log forwarding when using a customer managed CDN (BYOCDN) see [BYOCDN Log Forwarding Overview](/help/overview/log-forwarding/log-forwarding-overview.md)


## Step 5: Explore Dashboards and Take Action

After you provide information for CDN Log Forwarding, you can access the desired dashboard from the navigation section to the left.

* View the [Brand Presence](/help/dashboards/brand-presence.md) dashboard and view your visibility score and track your performance relative to other brands.
* Explore the [Agentic](/help/dashboards/agentic-traffic.md) and [Referral Traffic](/help/dashboards/referral-traffic.md) dashboards, if CDN log forwarding has been configured.
* Use [Opportunities](/help/dashboards/opportunities-overview.md) to identify content and technical improvements.
* Export data and collaborate your team or invite your co-worker to use the product.

Finally, to fully understand the capabilities of LLM Optimizer, you should explore all available [dashboards](/help/dashboards/dashboards-overview.md).
