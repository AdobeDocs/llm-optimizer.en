---
title: Quick Start
description: Learn how to onboard your brand name and domain, activate your trial from Experience Hub or Experience Cloud, and complete setup for Adobe LLM Optimizer.
feature: Quickstart, Onboarding
---

# Quick Start

To get started with LLM Optimizer, complete the onboarding process in the steps below. After onboarding, you have full access to [LLM Optimizer's dashboards](/help/dashboards/dashboards-overview.md) and other functionality.

## Onboarding overview

The onboarding process starts with onboarding your domain and your brand name. After this step, each part of the onboarding journey is detailed below along with helpful tips on how to get started with LLM Optimizer as soon as possible.

### Allowing Adobe LLM Optimizer to access public pages

To deliver accurate content and technical recommendations, Adobe LLM Optimizer requires access to your public-facing pages. This is achieved through a secure internal crawler (Spacecat/1.0 user agent).

Configuration requirements:

* Add the Spacecat/1.0 user agent to the Allowlist in your site's robots.txt file or bot-traffic management rules
* Ensure that pages are not blocked at the domain or CDN level. Blocked pages cannot be indexed, which means optimization tasks and insights cannot be generated for them.

If content visibility appears low in the dashboard, verify that the crawler has access to your domains. Restricted access is a common cause of incomplete indexing.

## Step 1: Onboard your brand name and domain {#step-1-onboard-your-domain}

To get started with LLM Optimizer, first activate your trial (if eligible) and onboard your brand name and domain. The activation flow differs depending on your Adobe product.

### Activate your trial

#### AEM Cloud customers

* Navigate to [Experience Hub](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/experience-hub/experience-hub) and use the Product Announcement card to activate LLM Optimizer. After you select **Try LLM Optimizer**, you are redirected to [https://llmo.now](https://llmo.now). Sign in through IMS, then enter a domain and brand name to start onboarding.
* Or go directly to [https://llmo.now](https://llmo.now) and sign in.

![LLM Optimizer Trial](/help/overview/assets/llm-trial.png)

#### Adobe Analytics customers

Adobe Analytics customers see a banner on the Experience Cloud home page.

![Experience Cloud home page with Start your Adobe LLM Optimizer Trial banner](/help/overview/assets/experience-cloud-llmo-trial-banner.png)

You can activate your trial in one of the following ways:

* Select **Start your Adobe LLM Optimizer Trial** in the banner.
* Or go directly to [https://llmo.now](https://llmo.now) and sign in.

Once activated, proceed with onboarding your brand name and domain.

>[!NOTE]
>
>**Free trial:** AEM Cloud and Adobe Analytics customers can use the free trial version of LLM Optimizer.
>
>**Customers who activate the trial on or after April 1, 2026** can use up to 100 prompts, one domain, and can deploy optimizations across up to 10 URLs for a single opportunity type.
>
>**Customers who activated the trial before April 1, 2026** continue to have access to up to 200 prompts under their existing terms.
>
>Use beyond included limits requires a separate license agreement. Access is provided on an "as-is" and "as-available" basis, and may be modified, limited, or removed at any time. Contact your account representative for more information.

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

The ability to deploy optimizations is available in Early Access. Learn more in [Optimize at Edge — Frequently asked questions](https://experienceleague.adobe.com/en/docs/llm-optimizer/using/resources/optimize-at-edge/overview#frequently-asked-questions).

Additionally, configure [CDN log forwarding](#step-4) for traffic analysis. LLM Optimizer requires Brand Presence data and insights from agentic and referral traffic to identify opportunities and provide prescriptive recommendations that boost AI visibility.

### Non-AEM Cloud customers

After your organization finalizes the business agreement, you are onboarded to LLM Optimizer with the domain your organization selected. When onboarding finishes, sign in at [https://llmo.now](https://llmo.now).

## Step 2: Customize Categories, Topics, and Prompts

Once your site has been onboarded, you can view the Brand Presence Analysis based on the small set of prompts that were automatically generated during the onboarding phase. Moving forward, you can customize the categories, topics and prompts for your brand. This configuration is created on the [customer configuration dashboard](/help/dashboards/customer-configuration.md).

![Customer Configuration Dashboard](/help/overview/assets/prompt-creation.png)

From this dashboard, you can:

* Add **new categories** that align with your business priorities. Categories can be broad content areas relevant to your domain.
* Enter **custom topics** or subtopics you want tracked. Topics can be specific themes tied to high volume non-branded keywords associated with your domain.
* Create **your prompts** to monitor visibility in specific queries. Prompts are queries (branded and non-branded) that provide a baseline visibility. Only a limited number of prompts will be automatically generated based on the categories and topics that you provided.
* Define mention **aliases** to ensure all mentions of a brand are captured and accounted for.
* Define **other aliases** to track other brands accurately.

>[!NOTE]
>The exact prompts you ask LLMs are not publicly available because they are not disclosed by the LLMs.

>[!NOTE]
>
> For more details on how to set up your categories, topics, prompts see the [Best practices for configuring categories, topics, prompts](/help/overview/best-practices-topics-prompts.md) page.

## Step 3: Brand Presence Insights

After your domain has been onboarded, you will see initial insights in the Brand Presence view based on the prompts that were automatically generated during onboarding. Once you customize your own categories, topics, and prompts, LLM Optimizer will automatically trigger the Brand Presence analysis on the prompts you provided and results will be available in 24 hours.

## Step 4: Provide information for CDN Log Forwarding {#step-4}

To unlock Agentic Traffic and Referral Traffic insights, add CDN log forwarding information from the [customer configuration dashboard](/help/dashboards/customer-configuration.md#cdn-configuration). Open the **CDN Configuration** tab and select **Onboard CDN**.

![Customer Configuration CDN](/help/overview/assets/cc-cdn.png)

Alternatively, if no CDN provider has been added beforehand (as described above), you will be prompted to add CDN log forwarding when accessing the Agentic and Referral Traffic dashboards for the first time. For more details, see:

* [Agentic Traffic](/help/dashboards/agentic-traffic.md#cdn-setup)
* [Referral Traffic](/help/dashboards/referral-traffic.md#setup)

>[!NOTE]
>For details regarding log forwarding when using a customer managed CDN (BYOCDN) see [BYOCDN Log Forwarding Overview](/help/overview/log-forwarding/log-forwarding-overview.md)

## Step 5: Explore Dashboards and Take Action

After you provide information for CDN Log Forwarding, you can:

* View the [Brand Presence](/help/dashboards/brand-presence.md) dashboard and view your visibility score and track your performance relative to other brands.
* Explore the [Agentic](/help/dashboards/agentic-traffic.md) and [Referral Traffic](/help/dashboards/referral-traffic.md) dashboards, if CDN log forwarding has been configured.
* Use [Opportunities](/help/dashboards/opportunities.md) to identify content and technical improvements.
* Export data and collaborate your team or invite your co-worker to use the product.

Finally, to fully understand the capabilities of LLM Optimizer, you should explore all available [dashboards](/help/dashboards/dashboards-overview.md).
