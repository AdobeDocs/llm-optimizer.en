---
title: Customer Configuration
description: Use customer configuration to define how your brand will be monitored and analyzed within the LLM optimizer platform.
---

# Customer configuration

Customer Configuration is where you define how your brand will be monitored and analyzed within the LLM optimizer platform. You can customize categories (such as business units or product lines), track competitors, and add brand mention aliases to capture all variations of your brand across prompts. This setup ensures the platform tailors insights to your business context, enabling accurate visibility, traffic, and opportunity analysis.

![Customer Configuration Dashboard](/help/dashboards/assets/customer-config.png)


## Best practices for configuring categories, topics, and prompts

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

## Customer Configuration dashboard

The Customer Configuration Dashboard is a powerful tool that provides insights into your brand's visibility in LLMs. By correctly setting up categories, topics, prompts, and competitors, you can ensure your brand is well-positioned to appear in LLM-generated responses. Regularly reviewing insights like Share of Voice, content visibility, and opportunities will help you adapt your strategy and stay ahead of competitors.

In order to configure how LLM Optimizer monitors and analyzes your brand presence across different markets and competitive landscapes, you have access to the following tabs:

* [Categories](#categories)
* [Competitor Tracking](#competitor-tracking)
* [Brand Aliases](#brand-aliases)
* [Data Insights](#data-insights)
* [Agentic CDN](#agentic-cdn)

## Categories {#categories}

From the categories tab, you can define business categories or product lines you want to track, and associate them with specific regions. Overall, the categories tab relates to every other customization on this page, because categories will appear in the category field for the other customizations (competitor tracking,aliases and so on). To add a new category:

1. Click the **Add** button.
2. In the new configuration window, add the **Category Name**.
3. Customize the **Associated Region** where the category will be monitored.
4. Click **Save** and the new category will appear on the category list.

Adding new categories will not automatically generate topics and prompts - these will need to be added manually From the [Data Insights](#data-insights) tab.

To delete a category, click the delete icon from the category list. Be careful, because **deleting a category will also delete the associated items** like competitors you might have set up or brand aliases that are linked to that specific category.

## Competitor Tracking {#competitor-tracking}

By using competitor tracking, you can track how your competitors are mentioned in relation to your brand across different categories and regions. Monitor their presence and performance in your market segments. To customize competitor tracking:

1. To add a new competitor, click the **Add** button.
2. In the new configuration window, select the **Category**. Previously created categories will appear here.
3. Add the competitor's name.
4. Customize the competitor Alias and Domains if needed.
5. Click **Save** and the new competitor will appear on the competitor list.

To delete a competitor, click the delete icon from the competitor list.

## Brand Aliases {#brand-aliases}

By using brand aliases, you can configure alternative names and variations of your brand that should be tracked across different categories and regions. This ensures comprehensive monitoring of all brand mentions. To add a brand alias:

1. Click the **Add** button.
2. In the new configuration window, select the **Category**. Previously created categories will appear here.
3. Select the **Region** where the alias will be monitored.
4. Add the brand alias.
5. Click **Save** and the brand alias will appear on the list.

To delete a brand alias, click the delete icon from the alias list.

## Data Insights {#data-insights}

From this tab, you can review, manage and customize prompts. You can upload a [Brand Presence data insights](/help/dashboards/brand-presence.md#data-insights) .csv and the list be populated with prompts and topics from that analysis. You can also delete, modify and add topics and their associated prompts as needed.

To import a data insights .csv file, you first need to export a file from the Brand Presence dashboard. See the [data insights](/help/dashboards/brand-presence.md#data-insights) section to learn how to do that. Once you have the file:

1. On the dashboard, click **Upload CSV**.
2. On the Import Data Insights window, drag and drop or manually choose the file.
3. Click **Upload Data**.

You can also create a new CSV file by downloading the template from the **Import Data Insights** window. Once you have the template, open it and input your topics together with their associated prompts, categories, and regions each in a new line.

Additionally, you can also add topics/prompts to the list independently of a CSV file. To achieve this, on the dashboard, you need to:

1. Click the **Add Topic** button.
2. In the new configuration window, select the **Category**. Previously created categories will appear here.
3. Enter the topic name.
4. Add the prompt text.
5. Select the region.
6. Click **Add Prompt** and the topic with the prompt will appear on the list.

>[!NOTE]
>Newly added prompts will not appear in Brand Presence until processing is complete.

On the list, you can click each topic and the associated prompt(s) will appear, To delete the topic and its associated prompts, click the delete icon from the list.

## Agentic CDN {#agentic-cdn}

Not available (will it be available for release?).

