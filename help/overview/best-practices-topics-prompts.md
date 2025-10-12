---
title: Best Practices for Categories, Topics and Prompts
description: Description here
---

# Intro here

Customer Configuration is where you define how your brand will be monitored and analyzed within the LLM optimizer platform. You can customize categories (such as business units or product lines), track competitors, and add brand mention aliases to capture all variations of your brand across prompts. This setup ensures the platform tailors insights to your business context, enabling accurate visibility, traffic, and opportunity analysis.

## Best practices for configuring categories, topics and prompts

This section describes best practices for deciding how you want to set up your categories, topics, prompts, and competitors.
This is a vital first step. What you decide now determines how information is tailored to your business context. Any changes to categories in the future reset historical data.

### Best practices for categories

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
* If you are a *merchandising/offers manager*, pick the **Product/Service category** approach.

>[!IMPORTANT]
>
> * Pick one approach and stick to it.
> * You can only have **one** Category model per account/brand. Do not mix **SBU** and **URL_DIR** at the same time.

Example:

|Type of site | Category | Topic taxonomy examples |
|---------|----------|---------|
| Enterprises with multiple businesses | SBU | small intent set (How-to, Troubleshooting, Comparison, Pricing, Policy) |
| Documentation/support heavy site | URL_DIR | How-to, Troubleshooting, Reference, Release notes |
| eCommerce/Services catalog | Product/Service | Comparison, Reviews, Pricing/Availability, How-to, Troubleshooting |

### Best practices for topics

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
* Corporate / News (if you truly need them)

When creating the list, consider the following:

* Can an editor understand the topic in 5 seconds from the prompt text? If not, rename/simplify.
* Will a different team own the fix for different topics? If yes, you picked useful topics.

Some additional helpful hints:

* Use knowledge of your business or site to define topics that align with your brand's strategic goals
* Consider how your brand compares to competitors within specific topics.

>[!IMPORTANT]
>
> * Keep topics intent-based, not organizational.
> * Do not add categories/filters for brand/non-brand/geographic as you can filter specifically for this in the **Brands** tab.
> * Topics are spread out across several categories, you can **not** have different topics per category.
> * A single prompt can exist in several topics or categories.

### Best practices for prompts

Prompts identify the specific questions or queries that customers are asking, which can impact your business. They are the actual questions or queries that users input into LLMs.

Be sure to review and update prompts regularly to ensure they align with customer needs and business goals.

>[!TIP]
>
>* You can use tools like the Adobe LLM Optimizer and Google Search Console with regex filters to identify common question structures (for example, "how," "what," "when," "where") and find out what prompts people are using to visit your site.
>* To find out what prompts are relevant to your site/brand, you can use on-site search data, FAQs in search engine results pages, or even ask LLM chatbots directly what questions customers might ask about your brand.

### Best practices for competitors

Competitors let you monitor visibility and mentions in LLM responses for prompts and topics that are important to your business.

The [!UICONTROL **Competitor Tracking**] tab lets you add competitors and track their visibility for specific prompts and topics.

With competitor tracking, you can see how often competitors are mentioned alongside your brand in different regions and categories and compare their visibility to your own.

>[!TIP]
>
>Regularly review competitor mentions and citations to identify areas where your brand can improve.

