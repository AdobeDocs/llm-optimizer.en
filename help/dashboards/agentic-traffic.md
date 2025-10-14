---
title: Agentic Traffic
description: Learn how to use the Agentic Traffic dashboard in order to see how AI agents interact with your site.
feature: Agentic Traffic
---

# Agentic Traffic {#agentic-traffic}

The Agentic Traffic dashboard shows how AI agents (crawlers and chatbots) interact with your site. By using this view you can track the total number of requests and general performance related metrics. You can also view the distribution of traffic across markets, categories, pages, and agents. The data used by this dashboard is sourced from the CDN logs so you must configure **CDN log forwarding** in order to display metrics. There are also customizable filters to help you refine the displayed data.

![Traffic Distribution](/help/dashboards/assets/ag-main.png)

This page details the following:

* [Filters](#filters)
* [CDN Setup](#cdn-setup)
* [Traffic Distribution](#traffic-distribution)
* [Agentic Traffic Trends](#agentic-trends)
* [Top and Bottom Movers](#top-bottom-movers)
* [User Agent and URL Performance Analysis](#user-url-performance)

## CDN Log Forwarding {#cdn-setup}

Without **CDN log forwarding**, the Agentic Traffic dashboard is blank. To view agentic interactions, you must configure **CDN log forwarding**.  On first login, you will see a message as shown in the image below.

![CDN Setup](/help/dashboards/assets/ag-log-forward1.png)

Select **Go to Configuration** and you will automatically navigate to the **CDN Configuration** tab of the [customer configuration dashboard](/help/dashboards/customer-configuration.md).

![CDN Setup Onboard](/help/dashboards/assets/ag-log-forward2.png)

On this tab, select **Onboard CDN**. And the CDN provider window is displayed.

<!-- [CDN Provider](/help/dashboards/assets/ag-log-forward3.png)-->
On the **Onboard CDN Provider** window:

1. Select your CDN provider (for example, Akamai, Adobe-managed Fastly, Fastly, AWS Cloudfront, Azure CDN, Cloudflare, or Other).
2. Click **Onboard** to enable log forwarding.

If you select **Other**, you will have to reach out to llmo-now@adobe.com for assistance.

Once activated, logs are ingested and the dashboard will populate with metrics such as total agent interactions, success rate, hits by market, user agent analysis, and URL-level performance.

## Filters {#filters}

At the top of the page, you can apply filters to refine your view. The filters you choose will impact **all** the sections present on the dashboard. You can customize the following:

* **Date Range** - Select the time frame for the displayed data. For example, the last 4 weeks. You also have the option to customize the time period by selecting the **Custom Weeks** option.
* **Category** - Filter the displayed results by predefined categories or custom categories.
* **Platform** - Choose which AI engine to analyze.
* **Agent Type** - Filter by the type of AI agent that interacted with your site. You can filter between crawlers, chatbots or all agents.
* **Success Rate** - Filter by the interaction quality (high, medium or low). This metric represents the percentage of successful HTTP requests, including both direct successful responses (2xx status codes) and redirects (3xx status codes).
* **Content Type** - View agentic interaction for different content types, such as HTML, PDF and so on.

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

The Top and Bottom Movers view highlights URLs with the largest week-over-week changes in agentic traffic — visits or hits from AI systems accessing your content. Top Movers shows pages gaining visibility or engagement, while Bottom Movers reveals URLs with the steepest declines. This helps you quickly identify which content is trending upward, which may need attention, and where AI-driven discovery patterns are shifting.

![Top and Bottom Movers](/help/dashboards/assets/movers.png)

## User Agent and URL Performance Analysis {#user-url-performance}

The User Agent and URL Performance Analysis views provide further data breakdowns on how crawlers and chatbots interact with your site. Click the tabs below for detailed descriptions.

![User Agent and URL Performance Analysis](/help/dashboards/assets/user-agent.png)

>[!BEGINTABS]

>[!TAB User Agent Analysis]

The User Agent Analysis table provides a breakdown of traffic by page type and agent type (for example, crawlers versus chatbots). This way, it is easy to understand which AI agents are crawling which parts of your site. It contains the following categories:

* **Page Type** - The page type.
* **Agent Type** - The AI agent crawling the page, either a crawler or a chatbot.
* **Hits** - The total number of requests made by AI agents for that specific page type.

>[!TAB URL Performance Analysis]

The URL Performance Analysis table shows a detailed view of individual URLs. This includes hits, unique agents, top agent, success rates, and categories. This way, you can identify high-value pages, detect crawl gaps, and optimize content for AI engines. The URLs are ranked by traffic volume. The table contains the following categories:

* **URL** - The examined URL.
* **Total Hits** - Total number of requests made by AI agents to the URL.
* **Unique Agents** - The number of different AI agents that accessed the URL.
* **Top Agent** - The AI agent that generated the most traffic to the URL.
* **Top Agent Type** - The type of the AI agent that generated the most traffic to this URL.
* **Success Rate** - The percentage of successful HTTP requests, including both direct successful responses and redirects.
* **Category** - The category that most closely matches the content of your page.

The URL performance table has a search field for quick access to URLs. You can also view additional details for each URL by clicking on the information icon at the end of each row.

![URL details](/help/dashboards/assets/details.png)

The URL Details view provides a holistic understanding of a page's performance — showing how often it's cited, the sentiment of AI responses where it is mentioned, the topics and prompts it appears in, and trends in agentic and referral traffic over time.

>[!ENDTABS]

On both tables, you can use the **Export** option to download the table .csv and share the insights with your team or include the table in executive reporting.
