---
title: Agentic Traffic
description: This is the article overview.
---

# Overview

The Agentic Traffic dashboard shows how AI agents (crawlers and chatbots) interact with your site. Use this view to track total requests, performance, and the distribution of traffic across markets, categories, pages, and agents. Data is sourced from CDN logs.

## Setup

On first login, the Agentic Traffic dashboard may appear blank. To view agentic interactions, you must configure **CDN log forwarding**.

**Add image here**

1. Select your CDN provider (e.g., Akamai, Adobe-managed Fastly, Fastly, AWS Cloudfront, Azure CDN, Cloudflare, or Other).
2. Enter a primary contact email.
3. Click Request activation to enable log forwarding.

Once activated, logs are ingested and the dashboard will populate with metrics such as total agent interactions, success rate, hits by market, user agent analysis, and URL-level performance.

An example of a populated dashboard is shown below:

**Add image here**

## Filters

At the top of the page, refine your view with:

Date Range → select the reporting window.
Category → filter by category 
Platform → focus on a specific AI engine (e.g., ChatGPT, Perplexity).
Agent Type → view crawlers, chatbots, or all agents.
Success Rate → filter by interaction quality.

The Traffic Distribution view shows how agent traffic is spread across markets, categories, and page types, helping you see which geographies, product areas, or content formats are most frequently accessed by AI agents. 

**Add image here**

The Traffic Trends chart tracks weekly totals of successful, failed, and overall hits, allowing you to monitor changes in agent activity and performance over time.

**Add image here**

The User Agent Analysis table provides a breakdown of traffic by page type and agent type (e.g., crawlers vs chatbots), making it easy to understand which AI agents are crawling which parts of your site.

**Add image here**

The URL Performance Analysis table gives a detailed view of individual URLs, including hits, unique agents, top agent, success rates, and categories, so you can identify high-value pages, detect crawl gaps, and optimize content for AI engines.

**Add image here**

