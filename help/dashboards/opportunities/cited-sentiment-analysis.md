---
title: Cited Sentiment Analysis
description: Learn how LLM Optimizer analyzes top-cited URLs to surface recommendations that improve your brand's perception and visibility in AI search results.
feature: Opportunities
autotag-review: '2026-05-15T17:39:50.086Z'
TQID: 'https://experienceleague.adobe.com/ZqgWup29QoQ-j0fDM6DqhGpzRqscg1f-fdXHTMN9fIk'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
    internal-label: LLM Optimizer
feature_v2:
  - id: a0b5a505-2fd7-4c3d-b61c-b557fb6f0558
    internal-label: Dashboards
  - id: c0713b97-4af8-4c41-b742-5afcc6ced468
    internal-label: Insights
subfeature_v2:
  - id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
    internal-label: Opportunities
---

# Cited Sentiment Analysis

When AI systems answer questions about your brand, they rely on a set of top-cited URLs — third-party web pages that are frequently referenced in AI-generated responses. How your brand is portrayed on those pages directly shapes how AI systems represent it to users.

The Cited Sentiment Analysis opportunity analyzes the top-cited URLs detected for prompts in your Brand Presence dashboard prompt set. It evaluates brand mentions, sentiment, share of voice and recurring topics across those pages. Afterwards, it surfaces prioritized recommendations to improve how your brand is perceived on the content AI systems rely on most.

It surfaces four key metrics:

- **Pages analyzed** — Number of cited web pages examined for brand mentions and sentiment.
- **Pages skipped** — Number of pages that could not be analyzed (for example, due to access restrictions).
- **Brand mentions (pages)** — How frequently your brand is mentioned across analyzed pages.
- **Overall sentiment (pages)** — Aggregated sentiment toward your brand across analyzed pages.

>[!NOTE]
>Cited Sentiment Analysis is currently in beta. Features and availability may change as the capability continues to develop.

![Cited Sentiment Analysis dashboard](/help/dashboards/opportunities/assets/cited-sentiment-overview.png)

## How it works

LLM Optimizer identifies the top-cited URLs appearing in AI-generated responses for prompts in your Brand Presence dashboard prompt set. It analyzes those pages for brand mentions, sentiment, share of voice and AI citations. It compares your brand's performance against market competitors, identifies recurring topics and generates recommendations to address perception gaps on the pages that matter most to AI systems.

If no cited URLs are detected for the prompts in your prompt set, this opportunity will not appear in your dashboard.

The results are displayed across two tabs: **Suggestions** and **Performance**.

## Suggestions

This tab shows recommendations for improving your brand's perception across top-cited URLs. Suggestions are organized into three sub-tabs: **Current Suggestions**, **Fixed Suggestions**, and **Ignored Suggestions**.

![Suggestions tab](/help/dashboards/opportunities/assets/cited-sentiment-suggestions.png)

The suggestions table includes the following columns:

- **Suggestion** — The recommended improvement to address a perception gap.
- **Priority** — Urgency level (Critical, High, Medium, Low).
- **Action Items** — Opens a panel with specific steps to implement the recommendation, including the teams responsible.

Expanding a suggestion reveals an **AI Analysis** section with:

- **Why this needs improvement** — An explanation of the perception gap identified, including which cited URLs are under-representing your brand and competitive context.
- **How to improve** — Specific guidance on outreach, content creation or partnership actions to address the gap.
- **Expected Outcome** — The anticipated result of implementing the recommendation.

## Performance

The **Performance** tab provides a detailed breakdown of how your brand is performing across top-cited pages. It is organized into four sections.

### Market Landscape

Compares your brand's performance against associated brands and market competitors based on mentions across cited pages.

![Market Landscape](/help/dashboards/opportunities/assets/cited-sentiment-landscape.png)

It shows:

- **Brand mentions in pages** — Your share of voice versus associated brands and market competitors.
- **Market Tracking** — A filterable chart where you can select up to five competitor brands to compare share of voice across analyzed pages.

### Sentiment Analysis

Tracks brand perception across analyzed pages with a **Sentiment Distribution** chart showing the percentage breakdown of favorable, neutral and unfavorable sentiment across pages.

![Sentiment Analysis](/help/dashboards/opportunities/assets/cited-sentiment-distribution.png)

### Pages

A detailed table of analyzed cited web pages with the following columns:

- **Page** — URL of the analyzed page.
- **Brand Mentions** — Count of your brand mentions versus total mentions on the page.
- **Share of Voice** — Your brand's share of mentions relative to all brands mentioned.
- **Top 5 Brands** — The most mentioned brands on the page.
- **Sentiment** — Overall sentiment toward your brand on the page.
- **AI Citations** — Number of AI answers that cited this page.

### Topics

A table of recurring topics identified across analyzed pages, showing:

- **Topic** — The recurring theme or subject identified.
- **Brand Mentions** — Number of brand mentions associated with the topic.
- **Sentiment** — Overall sentiment associated with the topic.

Clicking **Details** on any topic opens a drill-down with an analysis summary and the contributing source pages.

## Try it in the demo

See the Cited Sentiment Analysis opportunity in action by using the Frescopa demo environment - [View Cited Sentiment Analysis in the Frescopa demo](https://play.llmo.now/org/demo-org/opportunities/cited-analysis/d3a8b217-9f4c-4e88-a612-6b7f91e5c044?siteId=frescopa-demo).

## Frequently asked questions

**Why do top-cited URLs matter for AI search?**

Top-cited URLs are the third-party pages AI systems most frequently reference when generating responses about your brand. The sentiment and framing on those pages has a direct and outsized influence on how AI represents your brand, more so than pages that are rarely cited. Improving how your brand is portrayed on those specific pages is one of the highest-leverage actions you can take for AI visibility.

**Why is this opportunity not showing in my dashboard?**

This opportunity only appears when cited URLs are detected for prompts in your Brand Presence dashboard prompt set. If no cited URLs have been identified for those prompts, the opportunity will not be shown.

**What does Pages Skipped mean?**

Pages skipped are cited URLs that could not be analyzed, typically because the page is behind a paywall, requires authentication or blocks automated access. These pages are counted but excluded from the sentiment and brand mention analysis.

**What is Share of Voice?**

Share of voice is your brand's percentage of total brand mentions on a given page or across all analyzed pages, relative to all other brands mentioned.

**What are AI Citations?**

AI citations show how many AI answers cited a given page. Higher AI citation counts indicate the page is actively being used by AI systems when generating responses about related topics making the sentiment on those pages especially important for your brand's AI representation.

**How are market competitors identified?**

Competitors are identified automatically based on your brand's industry and the brands most frequently co-mentioned across the analyzed pages. You can also manually select up to five brands to compare in the Market Tracking chart.

**How often is the analysis updated?**

The analysis reflects cited URLs detected up to the date shown in the dashboard header. Revisit the opportunity after implementing recommendations to track changes in sentiment and share of voice.
