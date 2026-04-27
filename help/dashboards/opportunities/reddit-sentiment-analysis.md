---
title: Reddit Sentiment Analysis
description: Learn how LLM Optimizer analyzes Reddit threads to surface recommendations that improve your brand's perception and visibility in AI search results.
feature: Opportunities
---

# Reddit Sentiment Analysis

Reddit is a critical data source for Large Language Models. When users ask AI assistants about your brand, the responses are influenced by Reddit content sentiment. How your brand is discussed across subreddits directly shapes how AI systems understand and represent it in generated responses.

The Reddit Sentiment Analysis opportunity appears when Reddit threads are detected as citations for prompts in your Brand Presence dashboard prompt set. It analyzes those cited threads and their comments for sentiment, share of voice, and recurring topics, then surfaces prioritized recommendations to improve how your brand is perceived and cited by AI systems.

It analyzes your brand across four dimensions:

- **Posts analyzed** — Number of Reddit posts examined for brand mentions and sentiment
- **Comments analyzed** — Number of comments examined across analyzed posts
- **Brand mentions (threads)** — How frequently your brand is mentioned across analyzed threads
- **Overall sentiment (threads)** — Aggregated sentiment toward your brand across analyzed threads

>[!NOTE]
>Reddit Sentiment Analysis is currently in beta. Features and availability may change as the capability continues to develop.

![Reddit Sentiment Analysis dashboard](/help/dashboards/opportunities/assets/reddit-sentiment-overview.png)

## How it works

LLM Optimizer monitors Reddit threads cited by AI systems for prompts in your Brand Presence dashboard prompt set. When cited threads are detected, it analyzes those threads and their comments for brand mentions, sentiment, share of voice, and AI citations. It compares your brand's performance against market competitors, identifies recurring topics driving sentiment, and generates recommendations to address perception gaps.

If no Reddit threads are cited for the prompts in your prompt set, this opportunity will not appear in your dashboard.

The results are displayed across two tabs: **Suggestions** and **Performance**.

## Suggestions

This tab shows recommendations for improving your brand's perception on Reddit. Suggestions are organized into three sub-tabs: **Current Suggestions**, **Fixed Suggestions**, and **Ignored Suggestions**.

![Suggestions tab](/help/dashboards/opportunities/assets/reddit-sentiment-suggestions.png)

The suggestions table includes the following columns:

- **Suggestion** — The recommended improvement to address a perception gap
- **Priority** — Urgency level (Critical, High, Medium, Low)
- **Action Items** — Opens a panel with specific steps to implement the recommendation, including the teams responsible (for example, PR, Community Management, Product Marketing)
- **Evidence** — Opens a Sources table showing the Reddit threads behind the suggestion

Expanding a suggestion reveals an **AI Analysis** section with:

- **Why this needs improvement** — An explanation of the perception gap identified, including competitive context and how the issue is forming across Reddit threads
- **How to improve** — Specific guidance on what content or actions would address the gap
- **Expected Outcome** — The anticipated result of implementing the recommendation

The **Sources** table shows the Reddit threads driving the suggestion, with the following columns:

- **Thread** — Title and link to the Reddit thread
- **Subreddit** — The subreddit where the thread was posted
- **Engagement** — Engagement level (Low, Medium, High)
- **Brand Mentions** — Count of your brand mentions vs. total mentions in the thread
- **Share of Voice** — Your brand's share of mentions relative to all brands mentioned
- **Top 5 Brands** — The most mentioned brands in the thread
- **Sentiment** — Overall sentiment toward your brand in the thread
- **AI Citations** — Number of AI answers that cited this thread

## Performance

The **Performance** tab provides a detailed breakdown of how your brand is performing across Reddit content. It is organized into four sections.

### Market Landscape

Compares your brand's performance against associated brands and market competitors based on mentions in threads.

![Market Landscape](/help/dashboards/opportunities/assets/reddit-sentiment-landscape.png)

It shows:

- **Brand mentions in threads** — Your share of voice vs. associated brands and market competitors
- **Market Tracking** — A filterable chart where you can select up to five competitor brands to compare share of voice across threads

### Sentiment Analysis

Tracks brand perception across analyzed threads with a **Sentiment Distribution** chart showing the percentage breakdown of favorable, neutral, and unfavorable sentiment across threads.

![Sentiment Analysis](/help/dashboards/opportunities/assets/reddit-sentiment-distribution.png)

### Threads

A detailed table of analyzed Reddit threads with the following columns:

- **Thread** — Title and link to the Reddit thread
- **Subreddit** — The subreddit where the thread was posted
- **Engagement** — Engagement level (Low, Medium, High)
- **Brand Mentions** — Count of your brand mentions vs. total mentions in the thread
- **Share of Voice** — Your brand's share of mentions relative to all brands mentioned
- **Top 5 Brands** — The most mentioned brands in the thread
- **Sentiment** — Overall sentiment toward your brand in the thread
- **AI Citations** — Number of AI answers that cited this thread

### Topics

A table of recurring topics identified across analyzed threads, showing:

- **Topic** — The recurring theme or subject identified
- **Brand Mentions** — Number of brand mentions associated with the topic
- **Sentiment** — Overall sentiment associated with the topic

Clicking **Details** on any topic opens a drill-down panel with two tabs:

- **Analysis** — A summary of how your brand is discussed across threads associated with that topic
- **Sources** — The specific Reddit threads contributing to the topic's sentiment signal

## Try it in the demo

See the Reddit Sentiment Analysis opportunity in action using the Frescopa demo environment.

[View Reddit Sentiment Analysis in the Frescopa demo](https://play.llmo.now/org/demo-org/opportunities/reddit-analysis/b7e4d9a0-3c1f-4e2b-9d5a-8f2c1e0a7b4d?siteId=frescopa-demo)

## Frequently asked questions

**Why does Reddit matter for AI search?**

Reddit is one of the most heavily weighted sources in LLM training data and real-time retrieval. When AI systems generate responses about brands, products, and topics, Reddit discussions frequently inform the tone, framing, and factual claims in those responses. A brand that is discussed unfavorably or inaccurately on Reddit is more likely to be represented that way in AI-generated answers.

**Why is this opportunity not showing in my dashboard?**

This opportunity only appears when Reddit threads are detected as citations for prompts in your Brand Presence dashboard prompt set. If no Reddit threads are being cited for those prompts, the opportunity will not be shown. As your brand gains more Reddit coverage and those threads are cited by AI systems for your prompt set, the opportunity will become available.

**What does Overall Sentiment mean?**

Overall sentiment reflects the aggregated tone of threads where your brand is mentioned — favorable, neutral, or unfavorable — calculated across all analyzed threads.

**What is Share of Voice?**

Share of voice is your brand's percentage of total brand mentions within a given thread or across all analyzed threads, relative to all other brands mentioned.

**What are AI Citations?**

AI citations show how many AI answers cited a given thread. Higher AI citation counts indicate the thread is actively being used by AI systems when generating responses about related topics — making the sentiment in those threads especially important for your brand's AI representation.

**How are market competitors identified?**

Competitors are identified automatically based on your brand's industry and the brands most frequently co-mentioned in the analyzed threads. You can also manually select up to five brands to compare in the Market Tracking chart.

**How often is the analysis updated?**

The Reddit analysis reflects content analyzed up to the date shown in the dashboard header. Revisit the opportunity after implementing recommendations to track changes in sentiment and share of voice.
