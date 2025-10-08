---
title: Customer Configuration
description: This is the article overview.
---

# Customer Configuration

Customer Configuration is where you define how your brand will be monitored and analyzed within the platform. You can customize categories (such as business units or product lines), track competitors, and add brand mention aliases to capture all variations of your brand across prompts. This setup ensures the platform tailors insights to your business context, enabling accurate visibility, traffic, and opportunity analysis.

In order to configure how LLM Optimizer monitors and analyzes your brand presence across different markets and competitive landscapes, you have access to the following tabs:

[Categories](#categories)
[Competitor Tracking](competitor-tracking)
[Brand Aliases](#brand-aliases)
[Data Insights](#data-insights)
[Agentic CDN](#agentic-cdn)

## Categories {#categories}

From the categories tab, you can define business categories or product lines you want to track, and associate them with specific regions. Overall, the categories tab relates to every other customization on this page, because categories will appear in the category field for the other customizations (competitor tracking,aliases and so on).To add a new category:

1. Click the **Add** button.
2. In the new configuration window, add the **Category Name**.
3. Customize the **Associated Region** where the category will be monitored.
4. Click **Save** and the new category will appear on the category list.

Adding new categories will not automatically generate topics and prompts - these will need to be added manually From the [Data Insights](#data-insights) tab.

To delete a category, click the delete icon from the category list. Be careful, because **deleting a category will also delete the associated items** like competitors you might have set up or brand aliases that are linked to that specific category.

## Competitor Tracking {competitor-tracking}

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

Click the **Add Topic** button.
In the new configuration window, select the **Category**. Previously created categories will appear here.
Enter the topic name.
Add the prompt text.
Select the region.
Click **Add Prompt** and the topic with the prompt will appear on the list.

>[!NOTE]
>Newly added prompts will not appear in Brand Presence until processing is complete.

On the list, you can click each topic and the associated prompt(s) will appear, To delete the topic and its associated prompts, click the delete icon from the list.

## Agentic CDN {#agentic-cdn}

Not available (will it be available for release?).

