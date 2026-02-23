---
title: Customer Configuration
description: Use customer configuration to define how your brand will be monitored and analyzed within the LLM optimizer platform.
feature: Customer Configuration
---

# Customer Configuration {#customer-configuration}

The Customer Configuration Dashboard is a powerful tool that provides insights into your brand's visibility in LLMs. By correctly setting up categories, topics, prompts, you can ensure your brand is well positioned to appear in LLM-generated responses. This setup ensures the platform tailors insights to your business context, enabling accurate visibility, traffic, and opportunity analysis.

![Customer Configuration Dashboard](/help/dashboards/assets/customer-config.png)

In order to configure how LLM Optimizer monitors and analyzes your brand presence across different markets and competitive landscapes, you have access to the following tabs:

* [Prompts](#prompts-brand)
* [Categories](#categories)
* [Other Brands](#other-brands)
* [Brand Aliases](#brand-aliases)
* [CDN Configuration](#agentic-cdn)
* [Google Search Console](#google-console)

>[!IMPORTANT]
>
> For more details on how to set up your categories, topics, prompts see the [Best practices for configuring categories, topics, prompts](/help/overview/best-practices-topics-prompts.md) page.

## Prompts {#prompts-brand}

From this tab, you can review, manage and customize prompts. You can upload a [Brand Presence analysis](/help/dashboards/brand-presence.md) .csv and the list will be populated with prompts and topics from that analysis or [Download a Prompts library](/help/overview/best-practices-topics-prompts.md) created by Adobe. You can also delete, modify and add topics and their associated prompts as needed.

To import a data insights .csv file, you first need to export a file from the Brand Presence dashboard. See the [data insights](/help/dashboards/brand-presence.md#data-insights) section to learn how to do that. Once you have the file:

1. On the dashboard, click **Upload CSV**.
2. On the Import Data Insights window, drag and drop or manually choose the file.
3. Click **Upload Data**.

You can also create a new CSV file by downloading the template from the **Import Data Insights** window. Once you have the template, open it and input your topics together with their associated prompts, categories, and regions each in a new line.

To learn how to download and use the Industry Prompt Library created by Adobe see the Industry Prompt Library section on [this page](/help/overview/best-practices-topics-prompts.md)

Additionally, you can also add topics/prompts to the list independently of a CSV file or prompt library. To achieve this, on the dashboard, you need to:

1. Click the **Add Topic** button.
2. In the new configuration window, select the **Category**. Previously created categories will appear here.
3. Enter the topic name.
4. Add the prompt text.
5. Select the region.
6. Click **Add Prompt** and the topic with the prompt will appear on the list.

>[!NOTE]
>Newly added prompts will not appear in Brand Presence until processing is complete.

On the list, you can click each topic and the associated prompt(s) will appear, To delete the topic and its associated prompts, click the delete icon from the list.

## Categories {#categories}

From the categories tab, you can define business categories or product lines that you want to track, and associate them with specific regions. Overall, the categories tab relates to almost every other customization on this page, because categories will appear in the category field for the other customizations (others tracking,aliases and so on). To add a new category:

1. Click the **Add** button.
2. In the new configuration window, add the **Category Name**.
3. Customize the **Associated Region** where the category will be monitored.
4. Click **Save** and the new category will appear on the category list.

Adding new categories will not automatically generate topics and prompts - these will need to be added manually from the [Data Insights](#data-insights) tab.

To delete a category, click the delete icon from the category list. Be careful, because **deleting a category will also delete the associated items** like brand aliases that are linked to that specific category.

## Other Brands {#others-tracking}

By using this tab, you can track how your others are mentioned in relation to your brand across different categories and regions. Monitor their presence and performance in your market segments. To customize tracking:

1. Click the **Add** button.
2. In the new configuration window, select the **Category**. Previously created categories will appear here.
3. Add the other's name.
4. Customize the other Alias and Domains if needed.
5. Click **Save**.

To delete an entry on the list , click the delete icon.

## Brand Aliases {#brand-aliases}

By using brand aliases, you can configure alternative names and variations of your brand that should be tracked across different categories and regions. This ensures comprehensive monitoring of all brand mentions. To add a brand alias:

1. Click the **Add** button.
2. In the new configuration window, select the **Category**. Previously created categories will appear here.
3. Select the **Region** where the alias will be monitored.
4. Add the brand alias.
5. Click **Save** and the brand alias will appear on the list.

To delete a brand alias, click the **Delete** icon from the alias list.

## CDN Configuration {#cdn-configuration}

From this tab, you can configure your CDN streams to enable Adobe LLM Optimizer to analyze your CDN data. This data will be used to power dashboards (like Agentic Traffic), providing insights into traffic patterns, performance metrics, and optimization opportunities. To onboard your CDN provider, click **Onboard CDN**.

![Customer Configuration CDN](/help/overview/assets/cc-cdn.png)

On the **Onboard CDN Provider** window:

1. Select your CDN provider.
2. Click **Onboard** to enable log forwarding.

If you select **Other**, you will have to reach out to llmo-now@adobe.com for assistance.

## Google Search Console {#google-console}

Adobe LLM Optimizer allows you to integrate your Google Search Console account to bring real search queries directly into the interface. By surfacing real Google Search Console queries, you can build prompt sets that are grounded in actual search behavior and high-intent discovery patterns. This helps you prioritize prompts based on proven demand and aligns LLM optimization efforts with how users currently search. Additionally, remember that you remain in full control because queries are never added automatically and must be explicitly selected before becoming active prompts.

### How it works {#how-it-works}

The key principle to understand about the integration between LLM Optimizer with Google Search Console is the following: instead of manually guessing what customers might ask an AI assistant, we look at what they **are already searching for** and transform those real queries into natural, conversational prompts. This process of moving from search queries to AI prompts is exemplified in the diagram below.

![Process Flow](/help/dashboards/assets/diagram-flow.png)

Generally speaking, the process has five steps:

#### Step 1 — Collect your real search data {#gsc-one}

The process starts with the keywords your audience is actually using when it finds your website via Google. This raw dataset (often thousands of unique queries) is the foundation for everything that follows.

#### Step 2 — Analyze meaning and filter for safety {#gsc-two}

Each query is analyzed for its semantic meaning (what the user is really asking about) and screened through a safety filter that removes inappropriate or off-brand content. This ensures only clean, relevant keywords move forward.

#### Step 3 — Group into categories and topics {#gsc-three}

Related queries are automatically grouped together into **categories** (broad business themes) and **topics** (focused subtopics within each category). The system prioritizes categories that are already configured in your LLM Optimizer setup. Additionally, it can also surface new categories that your search data reveals but are not being monitored yet. The following diagram is an example of categories and topics for a furniture brand:

![Furniture Brand](/help/dashboards/assets/diagram-example.png)

#### Step 4 — Generate prompts grounded in real keywords {#gsc-four}

For each topic, the system generates prompts that are similar to how real people talk with AI assistants. Each prompt is directly influenced by actual search keywords from your Google Search Console, transforming keyword intent into natural conversational questions.

This approach grounded in keywords means:

* Prompts reflect real demand, not hypothetical questions.
* The language mirrors how your customers actually phrase things.
* Coverage spans the full breadth of what people search for on your site.

The prompt generation also considers your brand profile — including products, competitors, industry positioning, and target audience — to ensure that prompts are contextually accurate.

#### Step 5 - Quality assurance and delivery {#gsc-five}

Before delivery, every prompt goes through several automated quality checks:

* Deduplication — near-identical prompts are removed.
* Branded ratio balancing — ensures a realistic mix (~75% unbranded, ~25% branded).
* Language quality — strips robotic phrasing so prompts sound natural.
* Consistency checks — validates dates, removes filler phrases, ensures concise length.

Additionally, every prompt is tagged with its category, topic, intent type, and branded/unbranded classification, ready for LLM Optimizer to begin monitoring.

#### Prompt Anatomy {#prompt-anatomy}

After the process above is complete, each prompt delivered to LLM Optimizer has the following attributes:

| Field | Description |
|---------|----------|
| Text | The prompt, similar to how a user would type it into an AI assistant |
| Category | The broad business theme assigned to this prompt. |
| Topic | The specific subtopic within the category. |
| Region | The target market (for example, US, UK and so on) . |
| Intent | The user mindset: informational, comparative, transactional, instructional, planning, or delegation . |
| Type | The type can be either branded (mentions the brand/products) or unbranded (generic industry question). |

### How to use {#how-to-use}

Follow the steps presented below to integrate and use the Google Search Console queries with LLM Optimizer.

#### Connect the Google Search Console {#connect-console}

Before using this feature you need to integrate your Google Search Console account with LLM optimizer.

1. Open the Customer Configuration dashboard.
1. Navigate to the Google Search Console tab and click **Connect Account**.
   ![Google Search Console](/help/dashboards/assets/google-console.png)
1. Sign in with a Google account that has access to the desired Search Console property.
   ![Google Account](/help/dashboards/assets/google-account.png)
1. Choose the property you want to connect.
   ![Console Property](/help/dashboards/assets/console-property.png)
1. After the connection is complete, LLM Optimizer begins retrieving relevant search queries.
   ![Retrieving Data](/help/dashboards/assets/console-complete.png)

#### Review and search queries {#search-query}

After you integrate the Google Search Console account with LLM optimizer, you can review the list of topics and prompts sourced from the search console and add the prompts from the list.

1. On the Google Search Console tab, review the list of topics and prompts sourced from the Search Console.
   ![Prompts List](/help/dashboards/assets/prompts-list.png)
1. Click on the desired topic/prompt category to expand the list.
1. Use the **Add** button to add prompts from the list. You can also bulk add prompts and categories by using **Add all**.
   ![Add Prompts](/help/dashboards/assets/add-prompts.png)
1. Once you are satisfied with the selection, click **Save** on the notification message.

#### View added queries in the Prompts list {#prompts-list}

After a query is added, it appears in the [Prompts](#prompts-brand) tab within the Customer Configuration dashboard. Prompts sourced from the Google Search Console are marked with a Google Search Console icon in the **Origin** column. The icon helps you distinguish between prompts that are grounded in actual user search behavior from those added manually or from other sources.

### Frequently Asked Questions {#gsc-faq}

Q: How often are prompts updated in the Google Search Console dashboard?

Prompts sourced from the Google Search Console are usually refreshed once per month. Each refresh pulls the latest search query data from your Google Search Console, re-runs the generation pipeline, and updates your prompt set. This ensures your prompts stay aligned with current search trends and seasonal shifts in user behavior.

Q: How many prompts are typically sourced from the Google Search Console?

The number depends on the size of your deployment and the amount of categories tracked. For example:

| Categories | Total Topics | Prompts Delivered |
|---------|----------|----------|
|1–2|3–8|~65–180|
|4–5|12–20|~270–450|
|10|30–40|~675–900|

We aim to deliver prompt sets that meet the quality targets communicated during trial and onboarding: at least 20 prompts per topic, with 3–4 topics per category, and a healthy branded/unbranded balance.

Q: How soon will I see prompts sourced from the Google Search Console after I connect to the Google Search Console?

Prompts are typically available **within a few hours** after your Google Search Console connection is established. The pipeline automatically pulls your search data, processes it through the generation and quality assurance steps and delivers the final prompt set to LLM Optimizer.

Q: Who can connect to the Google Search Console?

Anyone with **Owner** or **Full Permission** on the Google Search Console property can authorize the connection. These are the permission levels that grant read access to search query data. If you are unsure about your permission level, you can check it under **Settings>Users** and permissions in your Google Search Console.

Q: Can I mark prompts as ignored or skipped so that I do not see them in the Google Search Console prompts list?

Yes, you can delete any prompt you don not want to monitor. Deleted prompts are removed from your active prompt list and will not appear in future reporting. If a deleted prompt is regenerated in a subsequent monthly refresh, you can remove it again.

Q: Once I add prompts from Google Search Console to my prompts list, how soon will I see Brand Presence data for those prompts?

Brand Presence data for newly added prompts will appear during the next scheduled data refresh, which typically runs at the beginning of each week. Depending on when you add the prompts, you may see results within a few days.
