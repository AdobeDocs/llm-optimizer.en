---
title: Customer Configuration
description: Use customer configuration to define how your brand will be monitored and analyzed within the LLM optimizer platform.
feature: Customer Configuration
autotag-review: '2026-07-15T17:48:20.742Z'
TQID: 'https://experienceleague.adobe.com/BvaFF-pMzojy1TNZvCQQRbcT5c5AQ75OqjclmDi14Z0'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
    internal-label: LLM Optimizer
feature_v2:
  - id: c898dfb2-0885-42fb-b2af-b2d756752646
    internal-label: Best practices
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
    internal-label: Administration
  - id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
    internal-label: Opportunities
subfeature_v2:
  - id: e69d5a42-0217-4ca5-9396-a9a826a170da
    internal-label: Configuration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
  - id: fc314d1d-7cb9-4a38-8dbd-8f9b6478f40d
    internal-label: Content strategy
---

# Customer Configuration {#customer-configuration}

The Customer Configuration Dashboard is a powerful tool that provides insights into your brand's visibility in LLMs. By correctly setting up categories, topics, prompts, you can ensure your brand is well positioned to appear in LLM-generated responses. This setup ensures the platform tailors insights to your business context, enabling accurate visibility, traffic, and opportunity analysis.

The Customer Configuration Dashboard (shown below) applies when your organization still uses this navigation.

![Customer Configuration Dashboard](/help/dashboards/assets/customer-config.png)

In order to configure how LLM Optimizer monitors and analyzes your brand presence across different markets and competitive landscapes, you have access to the following tabs:

* [Prompts](#prompts-brand)
* [Categories](#categories)
* [Other Brands](#other-brands)
* [Brand Aliases](#brand-aliases)
* [CDN Configuration](#agentic-cdn)
* [Google Search Console](#google-console)
* [Prompt Suggestions based on Citation Attempts and Referral Traffic](#prompt-suggestions)

If you are on the [Brand Centric experience](/help/overview/quick-start.md#brand-centric-experience), navigate to **Brands Management** to setup and configure brands, brand aliases and define competitors to track against. **Brands Management** is also used to configure integrations such as Google Search Console, Adobe Analytics, and CDN log forwarding related to URLs associated with brands. You can do this by clicking on the corresponding tabs: GSC, CDN and so on.

![Brands Management - app navigation (Brand Centric experience)](/help/assets/brand-centric-experience/llmo-app-shell.png)

![Brands Management - configuration overview (Brand Centric experience)](/help/assets/brand-centric-experience/brands-management-configuration.png)

>[!IMPORTANT]
>
> For more details on how to set up your categories, topics, prompts see the [Best practices for configuring categories, topics, prompts](/help/overview/best-practices-topics-prompts.md) page.

## Prompts {#prompts-brand}

From the **Prompts** tab, you can review, manage and customize prompts. You can upload a [Brand Presence analysis](/help/dashboards/brand-presence.md) .csv and the list will be populated with prompts and topics from that analysis or [Download a Prompts library](/help/overview/best-practices-topics-prompts.md) created by Adobe. You can also delete, modify and add topics and their associated prompts as needed.

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

For customers that are on the [Brand Centric experience](/help/overview/quick-start.md#brand-centric-experience), to add Topics and Prompts, navigate to **Prompts Management**.

![Prompts Management (Brand Centric experience)](/help/assets/brand-centric-experience/prompts-management.png)

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

Adobe LLM Optimizer allows you to integrate your Google Search Console account to bring real search queries directly into the interface. By surfacing real Google Search Console queries, you can build prompt sets that are grounded in actual search behavior and high-intent discovery patterns. This helps you prioritize prompts based on proven demand and aligns LLM optimization efforts with how users currently search. Additionally, you remain in full control because queries are never added automatically and must be explicitly selected before becoming active prompts.

### How it works {#how-it-works}

The main thing to remember about the integration between LLM Optimizer with Google Search Console is the following: instead of manually guessing what customers might ask an AI assistant, we look at what they **are already searching for** and transform those real queries into natural, conversational prompts. This process of moving from search queries to AI prompts is exemplified in the diagram below.

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

This approach (grounded in keywords) means:

* Prompts reflect real demand, not hypothetical questions.
* The language mirrors how your customers actually phrase things.
* Coverage spans the full breadth of what people search for on your site.

The prompt generation also considers your brand profile — including products, competitors, industry positioning, and target audience — to ensure that prompts are contextually accurate.

#### Step 5 - Quality assurance and delivery {#gsc-five}

Before delivery, every prompt goes through several automated quality checks:

* Deduplication — near-identical prompts are removed.
* Branded ratio balancing — ensures a realistic mix (~75% unbranded, ~25% branded).
* Language quality — strips robotic phrasing so prompts sound natural.
* Consistency checks — validates dates, removes filler phrases, ensures a concise length.

Additionally, every prompt is tagged with its category, topic, intent type, and branded/unbranded classification, ready for LLM Optimizer to begin monitoring.

#### Prompt Anatomy {#prompt-anatomy}

After the process above is complete, each prompt delivered to LLM Optimizer has the following attributes:

| Field | Description |
|---------|----------|
| Text | The prompt, similar to how a user would type it into an AI assistant |
| Category | The broad business theme assigned to this prompt. |
| Topic | The specific subtopic within the category. |
| Region | The target market (for example, US, UK and so on). |
| Intent | The user mindset: informational, comparative, transactional, instructional, planning, or delegation. |
| Type | The type can be either branded (mentions the brand/products) or unbranded (generic industry question). |

### How to use {#how-to-use}

Follow the steps presented below to integrate and use the Google Search Console queries with LLM Optimizer.

#### Connect the Google Search Console {#connect-console}

Before using this feature you need to integrate your Google Search Console account with LLM optimizer.

1. Open the **Customer Configuration** dashboard (classic navigation) or **Brands Management** (Brand Centric experience), then go to the Google Search Console integration (GSC tag in the Brand Centric experience).
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

After a query is added, it appears in the [Prompts](#prompts-brand) tab within the Customer Configuration dashboard (classic navigation) or in **Prompts Management** (Brand Centric experience). Prompts sourced from the Google Search Console are marked with a Google Search Console icon in the **Origin** column. The icon helps you distinguish between prompts that are grounded in actual user search behavior from those added manually or from other sources.

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

Yes, you can delete any prompt you do not want to monitor. Deleted prompts are removed from your active prompt list and will not appear in future reporting. If a deleted prompt is regenerated in a subsequent monthly refresh, you can remove it again.

Q: Once I add prompts from Google Search Console to my prompts list, how soon will I see Brand Presence data for those prompts?

Brand Presence data for newly added prompts will appear during the next scheduled data refresh, which typically runs at the beginning of each week. Depending on when you add the prompts, you may see results within a few days.

## Prompt Suggestions based on Citation Attempts and Referral Traffic {#prompt-suggestions}

Instead of guessing which prompts matter, **Prompt Suggestions** start from what AI agents and users are already accessing or being referred to on your site.

Adobe LLM Optimizer analyzes your CDN data to identify which pages AI agents are already consistently accessing (citation attempts) and referring users to (LLM referral traffic). After that, it automatically generates prompt suggestions based on gaps in your current prompt coverage. Instead of guessing which URLs to prioritize and which prompts to create, the workflow starts from real traffic signals: pages that agents are already reaching for and then defining the kind of user prompts those pages should be answering.

When a page is already being consistently accessed by AI agents, the question is not how to get agents to know about the page, but which questions the page content could answer. Without prompts configured for these pages, you have no visibility into how your brand shows up in AI answers on topics that matter most. Prompt Suggestions from Agentic Traffic closes that gap so you can start tracking and improving brand visibility for the pages where agents are already most active.

>[!NOTE]
>
> On the [Brand Centric experience](/help/overview/quick-start.md#brand-centric-experience), prompt suggestions are surfaced in the **Prompts Management** section.

### How it works {#prompt-suggestions-how-it-works}

The Prompt Suggestions workflow runs in four steps, turning CDN traffic signals into ready-to-configure prompt suggestions. Each step builds on the previous one: starting from pages where AI agent activity is already proven, understanding what those pages are about, checking what is already covered and generating prompts that are specific, grounded and ready to publish.

![Prompt Suggestions from Agentic Traffic workflow](/help/dashboards/assets/prompt-suggestions-workflow.png)

#### Step 1 — Identify high-signal pages from agentic traffic {#prompt-suggestions-step-1}

The pipeline begins by identifying pages on your site that AI systems are already actively engaging with, using two signals from your CDN data: how frequently AI systems access your pages as a source while answering real user questions and whether those pages are already driving real users to your site from AI-generated answers.

* **Citation attempts** — how AI systems accessed a page as a potential source while answering user questions. The pipeline looks for pages that show consistent citation attempt activity week over week, giving a more holistic picture of interest than a single point in time.
* **LLM referral traffic** — instances where a user clicked through from an AI-generated answer to land on the URL. The pipeline focuses on the most recent referral data and prioritizes pages with the highest volume of AI-driven visits, ensuring suggestions are grounded in current and proven AI recommendation patterns.

| Signal | What it means |
|--------|---------------|
| Citation attempts only | Agents are consistently accessing this page as a potential source |
| LLM referral traffic only | Agents are actively sending users to this page |
| Both | Agents access it and users click through — the highest-confidence target |

A page can qualify through either signal or both. Pages showing both signals represent the highest-confidence targets for prompt generation.

#### Step 2 — Analyze page content and intent {#prompt-suggestions-step-2}

For each qualifying page, the pipeline reads the page content and:

* **Summarizes** it into a concise, fact-grounded description that becomes the basis for everything that follows.
* **Classifies** the page type whether it is a Product, Resource, Support or Hub.
* Identifies the **primary journey intent** — the type of question the page is best positioned to answer, such as informational, instructional, comparative or transactional.

The two classifications work together. For example, prompts generated from a support page such as a setup guide or tutorial are more likely to be relevant to an existing user persona than a new audience.

#### Step 3 — Check existing prompt coverage {#prompt-suggestions-step-3}

Before generating anything new, the pipeline checks whether each qualifying page is already covered by prompts configured in your LLM Optimizer account, running in two passes:

1. A semantic similarity scan that quickly identifies candidate prompts from your existing prompt library that are potentially related to the page.
2. An LLM-powered review that scores how well each prompt candidate aligns with the page content — not just whether it is topically related, but whether it covers what the page is about.

A page is considered covered if at least one existing prompt meets that threshold. Pages with no adequate match are identified as gaps and move to step 4.

#### Step 4 — Generate, quality check, and rank prompts by URL {#prompt-suggestions-step-4}

![Prompt generation and quality check](/help/dashboards/assets/prompt-suggestions-generation.png)

For each gap page, the pipeline generates natural-sounding prompts grounded in what the page content is about. It begins by identifying relevant personas — someone who would realistically ask questions that this page answers and builds a realistic scenario around that persona before generating candidate prompts.

Every prompt goes through an automated quality review across three dimensions:

* Whether it is **specific** to this page rather than a generic question that could apply to any page in the category.
* Whether it is **grounded** in the page's actual content.
* Whether it sounds like something a **real user** would type into an AI tool such as ChatGPT.

Prompts that do not pass this review are rewritten with specific feedback and reviewed again. If they still do not pass, they are dropped.

The final step is a diversity check, prompts across URLs that are too similar to each other are dropped from the final list. Each prompt is tagged with your pre-configured topic and category, and includes a reasoning field that explains why the source URL was targeted based on its citation attempt and referral traffic signals. Prompts are also assigned a priority ranking so you know which suggestions to act on first — higher priority means stronger combined AI signal from the source URL. Prompts are then ready to review under the **Prompt Suggestions** tab in the Customer Configuration dashboard.

### How to use {#prompt-suggestions-how-to-use}

1. Open the **Customer Configuration** dashboard and go to the **Prompt Suggestions** tab.
1. Use the **Source** filter to select **Citation Attempt** to view suggestions generated from agentic traffic.
1. Review the **Reasoning** and **Priority** columns to evaluate each suggestion.
1. Select the prompts you want to add and click **Add selection** to add them to your configured prompts.

![Prompt Suggestions tab with Citation Attempt source filter](/help/dashboards/assets/prompt-suggestions-citation-attempt.png)

![Add selected prompt suggestions](/help/dashboards/assets/prompt-suggestions-add-selection.png)

### Frequently Asked Questions {#prompt-suggestions-faq}

Q: Does my organization need any additional configuration to use this feature?

This feature relies on CDN log data. If you have already enabled [CDN log forwarding](#cdn-configuration), no additional setup is needed. Without CDN logs, citation attempt or referral traffic data will not be available for analysis.

Q: Why doesn't a specific URL show up in the suggestions?

There are a few common reasons. The page may not yet have consistent AI retrieval activity or meaningful referral traffic — without one of those signals, it does not enter the pipeline. It may already be covered by an existing configured prompt since the pipeline only generates suggestions for true gaps. Or the page type may not be eligible for prompt generation.

Q: Can suggestions change over time?

Yes. The pipeline runs periodically as new CDN data becomes available. As user and agent behavior evolves (which pages are being accessed, how frequently and which are driving referral traffic) the suggestions reflect those changes. Pages that were not high-signal before may qualify in future runs and existing gaps that have been addressed will no longer generate new suggestions.

Q: Why am I seeing URLs I didn't expect in the suggestions?

The URLs surfaced are based entirely on observed agentic behavior — pages that AI systems have been consistently accessing or referring users to, regardless of how prominent they appear in your content strategy. In some cases, these may be pages you never considered important but that AI has repeatedly reached for. If a URL appears in the suggestions, it is because the data supports it. You are always free to ignore suggestions that do not fit your strategy, but the data behind each suggestion is grounded in real AI activity.

Q: What does the reasoning field mean?

Each prompt includes an explanation of why its source URL was listed as a suggestion. For pages qualifying through citation attempts, it shows how the page ranks among all pages being accessed based on weekly attempts. For pages qualifying through referral traffic, it shows the same for referral page views. Pages with both signals show both. This helps you understand priority and choose which suggestions to publish first.

For a page with both signals, the reasoning might look like: *Generated for [page URL] — ranks in top 3% by median weekly citation attempts and top 1% by LLM referral traffic.*

Q: How is priority determined?

Priority is based on a combined score of two signals: how a page ranks among all pages by citation attempts and how it ranks among all pages by LLM referral page views. Both are expressed as percentiles and added together, so pages that score strongly on both signals naturally rise to the top. A page that AI is both consistently accessing and actively sending users to, will always rank higher than a page with only one signal.

Q: How does the pipeline decide which pages qualify based on citation attempts?

The pipeline looks for pages that show consistent AI retrieval activity over time. To qualify, a page must meet two conditions: it must show meaningful activity in at least half of the weeks in the available data and its median agentic hits count during those active weeks must rank in the top 25% across all pages. Both conditions must hold — frequency alone is not enough and hits volume alone is not enough either.

Q: How does the pipeline decide which pages qualify based on referral traffic?

A page qualifies if it appears in the top 10% of all pages by total LLM referral visits over the most recent three months. This ensures suggestions are grounded in pages that are already generating real, measurable click-through from AI answers, based on recent behavior.

Q: Are prompt suggestions available in languages other than English?

Not yet. The pipeline currently generates prompts in English only. Multi-language support will be added in a future release.
