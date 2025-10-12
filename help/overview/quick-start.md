---
title: Quick Start
description: Get started with Adobe LLM Optimizer - onboard your brand, unlock AI visibility insights, and explore dashboards to boost search performance.
---

# Quick Start

To get started with LLM optimizer, you need to complete the onboarding process as detailed in the steps presented below. After you complete the process you will have full access to [LLM Optimizer's dashboards](/help/dashboards/dashboards-overview.md) and other functionalities.

## Onboarding overview

The onboarding process starts with onboarding your domain. The process is different depending on whether you are an AEM Cloud customer or not. After you complete the process, you will need to provide information for CDN Log Forwarding and finally customize categories, topics, and prompts. Each part of the process is detailed below along with helpful tips on how to get started with LLM Optimizer as soon as possible.

## Step 1: Onboard your domain

### Try Before you buy

AEM Cloud (Cloud Service,Managed Services, Edge Delivery Service) customers have the option to use the The Try Before You Buy offer. It is a free trial version of LLM Optimizer with up to 200 free prompts. Use of more than 200 prompts requires a separate license agreement. Access is provided on an “as-is” and “as-available” basis, and may be modified, limited or removed by Adobe at any time.

There are some product capabilities that are not available in the free version:

* Trial is limited to one domain. You will not be able to change the domain you provided after completing the setup.
* Support to deploy optimizations will not be available.

See the section below for details on how to activate the free trial version and onboard your domain.

### AEM Cloud Customers

If you are an AEM Cloud Customers you have the option to try LLM Optimizer by using the Product Announcement card in [Experience Hub](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/experience-hub/experience-hub).

>[!NOTE]
>Newly added prompts will not appear in the [Brand Presence Dashboard](/help/dashboards/brand-presence.md) until processing is complete. AEM Cloud Customers (Cloud Service, Managed Services/ Edge Delivery Service) can use the free trial version of LLM Optimizer. Use of more than 200 prompts requires a separate license agreement. Access is provided on an “as-is” and “as-available” basis, and may be modified, limited or removed by Adobe at any time. Please reach out to your account representative for more information.  

![LLM Optimizer Trial](/help/overview/assets/llm-trial.png)

Once you click the **Try LLM Optimizer** button, you will be redirected to [https://llmo.now](https://llmo.now). You will then be required to log in via IMS. Once you log in you will start the onboarding process by providing a domain and the brand name.

![LLM Optimizer domain](/help/overview/assets/domain.png)

>[!NOTE]
>The domain you provided will be used by everyone from your organization and cannot be changed.

To trigger the Brand Presence Analysis, you will need to provide categories, topics, and prompts.

![Brand Presence Analysis](/help/overview/assets/bp-analysis.png)

Additionally, you also need to configure [CDN log forwarding](#step-4) for traffic analysis. LLM Optimizer requires Brand Presence data and insights from agentic and referral traffic to identify opportunities and to provide prescriptive recommendations in order to boost AI-visibility.

### Non-AEM Cloud Customers

Once the business agreement has been finalized, you will be onboarded via slackbot command with the domain you would like to onboard on LLM Optimizer. Once this onboarding is complete, you will be able to log in to LLM Optimizer via [https://llmo.now](https://llmo.now).

### Step 2: Customize Categories, Topics, and Prompts

In order to trigger the Brand Presence analysis, and populate the dashboard with insights into your brand visibility, you need to customize Categories, Topics, and Prompts. This configuration is created on the [customer configuration dashboard](/help/dashboards/customer-configuration.md).

![Customer Configuration Dashboard](/help/overview/assets/prompt-creation.png)

From this dashboard, you can:

* Add **new categories** that align with your business priorities. Categories can be broad content areas relevant to your domain.
* Enter **custom topics** or subtopics you want tracked. Topics can be specific themes tied to high volume non-branded keywords associated with your domain.
* Create **your prompts** to monitor visibility in specific queries. Prompts are queries (branded and non-branded) that provide a baseline visibility. Only a limited number of prompts will be automatically generated based on the categories and topics that you provided.
* Define mention **aliases** to ensure all mentions of a brand are captured and accounted for.
* Define **competitor aliases** to track competitors accurately.

>[!NOTE]
>The exact prompts you ask LLMs are not publicly available because they are not disclosed by the LLMs.

### Step 3: Automatic Pre-population of Insights

Once your domain is onboarded and you have provided categories, and topics, LLM Optimizer will automatically trigger the Brand Presence analysis.

### Step 4: Provide information for CDN Log Forwarding {#step-4}

To unlock Agentic Traffic and Referral Traffic insights, you need to provide information for CDN log forwarding. It can be added from the [customer configuration dashboard](/help/dashboards/customer-configuration.md) by navigating to the **CDN Configuration** tab and clicking **Onboard CDN**.

![Customer Configuration CDN](/help/overview/assets/cc-cdn.png)

Alternatively, if no CDN provider has been added beforehand, you will be prompted to add CDN log forwarding when accessing the Agentic and Referral Traffic dashboards for the first time. For more details, see:

* [Agentic Traffic](/help/dashboards/agentic-traffic.md#cdn-setup)
* [Referral Traffic](/help/dashboards/referral-traffic.md#setup#setup)

### Step 5: Explore Dashboards and Take Action

After you provide information for CDN Log Forwarding, you can:

* View the [Brand Presence](/help/dashboards/brand-presence.md) dashboard, view your visibility score and track your performance relative to your competitors.
* Explore the [Agentic](/help/dashboards/agentic-traffic.md) and [Referral Traffic](/help/dashboards/referral-traffic.md) dashboards, if CDN log forwading has been configured.
* Use [Opportunities](/help/dashboards/opportunities.md) to identify content and technical improvements.
* Export data and collaborate your team or invite your co-worker to use the product.

Finally, to fully understand the capabilities of LLM optimizer, explore all the available [dashboards](/help/dashboards/dashboards-overview.md).
