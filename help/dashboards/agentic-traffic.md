---
title: Agentic Traffic
description: Learn how to use the Agentic Traffic dashboard in order to see how AI agents interact with your site..
---

# Agentic Traffic {#agentic-traffic}

The Agentic Traffic dashboard shows you how AI agents (crawlers and chatbots) interact with your site. By using this view you can track the total number of requests and general performance-related metrics. You can also view the distribution of traffic across markets, categories, pages, and agents. The data used by this dashboard is sourced from the CDN logs so you must configure **CDN log forwarding** in order to display metrics. There are also customizable filters to help you refine the displayed data.

This page details the following:

* [Filters](#filters)
* [CDN Setup](#cdn-setup)
* [Traffic Distribution](#traffic-distribution)
* [Agentic Traffic Trends](#agentic-trends)
* [Top and Bottom Movers](#top-bottom-movers)
* [User Agent and URL Performance Analysis](#user-url-performance)

## CDN Setup {#cdn-setup}

On first login, the Agentic Traffic dashboard is blank. To view agentic interactions, you must configure **CDN log forwarding**. **TBD point to CDN setup in quickstart/onboarding?**

![CDN Setup](/help/dashboards/assets/ag-log-forward.png)

1. Select your CDN provider (for example, Akamai, Adobe-managed Fastly, Fastly, AWS Cloudfront, Azure CDN, Cloudflare, or Other).
2. Enter a primary contact email.
3. Click **Request Activation** to enable log forwarding.

Once activated, logs are ingested and the dashboard will populate with metrics such as total agent interactions, success rate, hits by market, user agent analysis, and URL-level performance.

## Filters {#filters}

At the top of the page, you can apply filters to refine your view. The filters you choose will impact **all** the sections present on the dashboard. You can customize the following:

* **Date Range** - Select the time frame for the displayed data. For example, the last 4 weeks. You also have the option to customize the time period by selecting the **Custom Weeks** option.
* **Category** - Filter the displayed results by predefined categories. You can also add custom categories to this field (**SR**-how?).
* **Platform** - Choose which AI engine to analyze.
* **Agent Type** - Filter by the type of AI agent that interacted with your site. You can filter between crawlers, chatbots or all agents.
* **Success Rate** - Filter by the interaction quality (high, medium or low). This metric represents the percentage of successful HTTP requests, including both direct successful responses and redirects.
* **Content Type** - Filter by content type, either HTML or txt.

After you select the desired filter, click **Apply Filters** to apply the selection to the dashboard.

## Traffic Distribution {#traffic-distribution}

The Traffic Distribution view shows how agent traffic is spread across markets, categories, and page types. As such, this view helps you determine which geographies, product areas, or content formats are most frequently accessed by AI agents when interacting with your site.

![Traffic Distribution](/help/dashboards/assets/ag-main.png)

At the top of the page, there are three key metrics that you need to be aware of:

* **Agentic interactions** - This metric represents the total number of requests made by AI agents to your website. This includes all traffic from search engines, chatbots, and other non-human traffic.
* **Success rate** - This metric represents the percentage of successful HTTP requests, including both direct successful responses and redirects.
* **Average TTFB** - Time To First Byte (TTFB) measures the time it takes for the first byte of data to be received from the server. Lower values indicate faster server response times.

Trend indicators for each key metric show how these values are changing over time compared to the previous period.

## Agentic Traffic Trends {#agentic-trends}

Use the Agentic Traffic Trends chart to track the weekly totals of successful, failed, and overall hits. As such, you can monitor changes in agent activity and performance over time. You can also hover the mouse along the chart to see the data evolution across the weekly time frame.

![Agentic Traffic Trends](/help/dashboards/assets/ag-trends.png)

## Top and Bottom Movers {#top-bottom-movers}

These two metrics sort the URLs as follows:

* **Top Movers** - The URLs with the biggest increase in agentic traffic from oldest to newest week.
* **Bottom Movers** - URLs with the biggest decrease in agentic traffic from oldest to newest week.

## User Agent and URL Performance Analysis {#user-url-performance}

The User Agent and URL Performance Analysis views provide further data breakdowns on how crawlers and chatbots interact with your site. Click on the tabs below for detailed descriptions.

![User Agent and URL Performance Analysis](/help/dashboards/assets/user-agent.png)

>[!BEGINTABS]

>[!TAB User Agent Analysis]

The User Agent Analysis table provides a breakdown of traffic by page type and agent type (for example, crawlers versus chatbots). This way, it is easy to understand which AI agents are crawling which parts of your site. It contains the following categories:

* **Page Type** - The page type.
* **Agent Type** - The AI agent crawling the page, either a crawler or a chatbot.
* **Hits** - The total number of requests made by AI agents for that specific page type.

You can also use the **Export** option to download the table .csv and share the agent analysis with your team or include it in executive reporting.

>[!TAB URL Performance Analysis]

The URL Performance Analysis table shows a detailed view of individual URLs. This includes hits, unique agents, top agent, success rates, and categories. This way, you can identify high-value pages, detect crawl gaps, and optimize content for AI engines. The URLs are ranked by traffic volume. The table contains the following categories:

* **URL** - The examined URL.
* **Total Hits** - Total number of requests made by AI agents to the URL.
* **Unique Agents** - The number of different AI agents that accessed the URL.
* **Top Agent** - The AI agent that generated the most traffic to the URL.
* **Top Agent Type** - The type of the AI agent that generated the most traffic to this URL.
* **Success Rate** - The percentage of successful HTTP requests, including both direct successful responses and redirects.
* **Category** - The category that most closely matches the content of your page.

The URL performance table has a search field for quick access to URLs. Also, you can use the **Export** option to download the table .csv and share the insights with your team or include the table in executive reporting.

>[!ENDTABS]
