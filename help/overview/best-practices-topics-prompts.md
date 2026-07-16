---
title: Best Practices for Categories, Topics, Prompts, and Others
description: Optimize LLM insights by configuring categories, topics, prompts, and other brands to track including competitors for tailored brand monitoring and strategic content analysis.
feature: Best Practices, Customer Configuration
autotag-review: '2026-07-15T17:42:20.391Z'
TQID: 'https://experienceleague.adobe.com/nnLohajbU-fogbmBfGE5PUzdsoTJ5fjwW-ruVTjOWtM'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
    internal-label: LLM Optimizer
feature_v2:
  - id: c898dfb2-0885-42fb-b2af-b2d756752646
    internal-label: Best practices
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
    internal-label: Administration
subfeature_v2:
  - id: e69d5a42-0217-4ca5-9396-a9a826a170da
    internal-label: Configuration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: addf009e-030a-4310-8534-776a3e62ed48
    internal-label: Customer lifecycle
  - id: b5520579-b31f-4df7-9281-f0d9f91e2edc
    internal-label: Customer engagement
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
    internal-label: Customer experience
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
  - id: d00e9f03-e50b-4162-b143-0c0817c937c2
    internal-label: Customer journeys
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
  - id: f8667931-f646-4dd3-af2a-b9d0cb8098ad
    internal-label: Taxonomy
---
# Best practices for configuring categories, topics, prompts, and others to track

This section describes best practices for deciding how you want to set up your categories, topics, prompts, and others to track. In addition, it includes information on the Industry Prompt Library, which Adobe developed with extensive research with industry experts.

This configuration is a vital first step. What you decide now determines how information is tailored to your business context. Any changes to categories in the future reset historical data.

The [[!UICONTROL Brands Management]](/help/dashboards/customer-configuration.md) dashboard is where you define how your brand is monitored and analyzed within the LLM optimizer platform.

Here you can customize categories (such as business units or product lines), track other brands, and add brand mention aliases to capture all variations of your brand across prompts. This setup ensures the platform tailors insights to your business context, enabling accurate visibility, traffic, and opportunity analysis.

By default, each organization starts with one active brand and additional suggested brands to choose from.

![Brands Management - app navigation (Brand Centric experience)](/help/assets/brand-centric-experience/llmo-app-shell.png)

![Brands Management - configuration overview](/help/assets/brand-centric-experience/brands-management-configuration.png)

To set up topics and prompts for a specific brand, use the **Prompts Library** dashboard.

<!-- Add link to Prompts Management page when available-->

![Prompts Management](/help/assets/brand-centric-experience/prompts-management.png)

## Industry Prompt Library

To help get started with prompts and topics, Adobe has created an Industry Prompt Library developed through extensive research with industry experts and analysis of AI search behavior across 6,000+ customers. This library identifies the most relevant topics and prompts based on industry-specific trends, validated business objectives, and real-world customer search patterns.

To use the Industry Prompt Library:

1. Navigate to the **Prompts Library** dashboard.
1. Select **Download Prompts Library** to download the library file from LLM Optimizer.
<!--![Industry prompt library download](/help/assets/best-practices/download-prompts.png)-->
1. Review suggested **Topics** and **Prompts** for your brand's industry on the respective tab and choose the options that are most relevant.
1. Review **Customer Journey Stage column** to view prompt options across the customer lifecycle (for example, discovery to conversion to retention). Early stage/top of funnel prompts are high priority but also consider later stage options to promote retention, enable customer support, and so on.
1. Modify topics or prompts as needed to best support your goals and objectives before uploading your topics and prompts to Adobe LLM Optimizer (for example, add your brand/product name, add on-brand terminology). Prompts can be added to LLM Optimizer manually or via bulk upload using the provided *.csv* template.

>[!TIP]
>
> Use a combination of domain-specific prompts recommended by LLM Optimizer during initial set-up and the Industry Prompt Library to curate your prompt strategy.

### Prompt Library research foundation

The Industry Prompt Library was developed through a comprehensive research initiative combining:

* **Customer intelligence:** Analysis of AI search behavior and preferences across 6,000+ customers
* **Industry expertise:** Perspectives from experts in Auto, Financial Services, Healthcare, Telecom, and Travel sectors.
* **Data-driven insights:** Identification of high-impact topics and query patterns that drive customer engagement and conversion.

Top topics searched by customers across industries:

* **Auto:** Troubleshooting auto issues, Comparing vehicles and Financing/Leasing
* **Financial Services:** Researching financial products
* **Healthcare:** Looking up symptoms or health issues, Comparing treatment options, Understand lab results or medical terms
* **Telecom:** Comparing plans, Contract terms and promotions, Checking service in local area
* **Travel:** Preparing for a trip, Researching and booking travel

Customer trends on AI search and prompt behavior in LLM tools:

* Customers prefer to ask questions vs. use keywords while using LLM search tools.
* They primarily use LLM search tools for early-stage research and discovery.
* Customers tend to mention a specific brand or product name in their prompts.

## Best practices for categories

Categories let you organize your content into strategic business units or logical groupings. They are the "where it belongs" bucket and the top-level organizational structure for your content.

When deciding how to set categories up, you need to consider your goals and who needs to act on what you are reporting.

>[!IMPORTANT]
>
> Ensure categories are set up correctly from the start, as changes to categories reset historical data. That means that if you change these, you lose historical data from before the change.

Here's an overview of the types of approaches you could take and when you would choose a particular approach:

|Approach | Description| Benefit|
|---------|----------|---------|
| Strategic Business Unit (SBU) | Use this approach if your organization is split by P&L (e.g., Consumer, Enterprise, Services). | You get clean reporting by business line and easier accountability. |
| Website Top-Level Directory (URL_DIR) | Use if your site information architecture mirrors ownership (/products/, /support/, /docs/, /news/). | You get alignment with how teams publish and maintain content. |
| Product (or Service) category | Use it if you sell a catalog (SKUs/services). | You get assortment views, gap analysis, and "which category needs content" answers. |

How to decide how you set up categories is based on one question: **Who needs to act on the report?**

* If you are a *business leader*, pick the **SBU** approach.
* If you are a *web/content owner*, pick the **URL_DIR** approach.
* If you are a *merchandising/offers manager*, pick the **Product/Service category** approach.<!--How do you pick a region? Or is that handled differently?>

![Adding categories in LLM Optimizer](/help/assets/best-practices/create-category1.png)

>[!IMPORTANT]
>
> * Pick one approach and stick to it.
> * You can only have **one** Category model per account/brand. Do not mix **SBU** and **URL_DIR** at the same time.
<!--Can you mix Product/Service with these?-->

Example:

|Type of site | Category | Topic taxonomy examples |
|---------|----------|---------|
| Enterprises with multiple businesses | SBU | Small intent set (How-to, Troubleshooting, Comparison, Pricing, Policy) |
| Documentation/support heavy site | URL_DIR | How-to, Troubleshooting, Reference, Release notes |
| eCommerce/Services catalog | Product/Service | Comparison, Reviews, Pricing/Availability, How-to, Troubleshooting |

## Best practices for topics

Topics help you understand the user intent - they show you what the user wants. They let you group prompts with similar user intent. Think of it as clustering relevant prompts together.

>[!IMPORTANT]
>
>Topics are universal across **all** categories, meaning they remain consistent regardless of the category that they are assigned to. They represent clusters of questions or prompts that share a common intent.

When deciding on topics, you want to create a short, flat list (6-12 maximum). For example:

* Products/Services
* How-to (setup/usage)
* Troubleshooting (errors/issues)
* Comparison (X vs Y; "best … for …")
* Reviews and Ratings
* Pricing and Availability
* Policy and Warranty
* Support Contact
* Corporate/News (if you truly need this)

![Adding topics in LLM Optimizer](/help/assets/best-practices/add-new-topic1.png)

When creating the list, consider the following:

* Can an editor understand the topic in 5 seconds from the prompt text? If not, rename/simplify.
* Will a different team own the fix for different topics? If yes, you picked useful topics.
<!-- Last bullet point does not make sense. Clarification needed. Also not sure what is meant by "editor"?-->

Some additional helpful hints:

* Use knowledge of your business or site to define topics that align with your brand's strategic goals
* Consider how your brand compares to other brands within specific topics.

>[!IMPORTANT]
>
> * Keep topics intent-based, not organizational.
> * Do not add categories/filters for brand/non-brand/geographic as you can filter specifically for this in the **[!UICONTROL Brands]** tab.
> * Topics are spread out across several categories. You **cannot** define unique topics to each category.
> * A single prompt **can** exist in several topics or categories.

## Best practices for prompts

Prompts identify the specific questions or queries that customers are asking, which can impact your business. They are the actual questions or queries that users input into LLMs.

Be sure to review and update prompts regularly to ensure they align with customer needs and business goals.

Best practices for prompts:

* Group similar prompts together based on what people are asking.
* Focus on the prompts that are most important to your customers.
* Check if your brand has a good chance of being mentioned for certain prompts.

>[!TIP]
>
>* You can use tools like Adobe LLM Optimizer and Google Search Console with regex filters to identify common question structures (for example, "how," "what," "when," "where") and find out what prompts people are using to visit your site.
>* To find out what prompts are relevant to your site/brand, you can use on-site search data, FAQs in search engine results pages, or even ask LLM chatbots directly what questions customers might ask about your brand.

## Best practices for tracking other brands

Tracking Others let you monitor visibility and mentions in LLM responses for prompts and topics that are important to your business.

The [!UICONTROL **Others Tracking**] tab lets you add others including competitors to track their visibility for specific prompts and topics.

With others tracking, you can see how often other brands are mentioned alongside your brand in different regions and categories and compare their visibility to your own.

>[!TIP]
>
>Regularly review competitor or others mentions and citations to identify areas where your brand can improve.

## Learn More

* [Customer Configuration dashboard](/help/dashboards/customer-configuration.md) is where you configure your categories, topics, prompts, and others tracking.
* [LLM Optimizer best practices](/help/tutorials/best-practices.md) describes best practices around LLM Optimization

