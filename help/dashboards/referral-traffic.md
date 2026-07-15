---
title: Referral Traffic
description: Learn how to use the Referral Traffic dashboard to see how visitors arrive at your site from external platforms, AI citations, and referral links.
feature: Referral Traffic
autotag-review: '2026-05-15T17:57:28.534Z'
TQID: 'https://experienceleague.adobe.com/rMSltSJf-UH4FHoST9NhmeY-hGVNLXsFXbCLzZenW5w'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
    internal-label: LLM Optimizer
feature_v2:
  - id: a0b5a505-2fd7-4c3d-b61c-b557fb6f0558
    internal-label: Dashboards
  - id: e0828736-236a-487b-a478-5a635455eadc
    internal-label: Reporting
subfeature_v2:
  - id: e3c08d81-9e25-4503-9df5-8dd1f489aa99
    internal-label: Referral Traffic
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
---

# Referral Traffic

Referral Traffic shows how visitors arrive at your site from external platforms, AI citations, and referral links. It tracks and analyzes traffic sources, referral patterns, and conversion metrics from external websites and platforms. This will help you understand which sources, regions, and pages drive the most engaged traffic. <!--Data is sourced from the CDN logs, a privacy-preserving source that does not capture personal user data.--> There are also customizable filters to help you refine the displayed data.

Navigate to **Referral Traffic** and select the site for which you want to view the LLM Referral Traffic insights.

![Referral Traffic — site selector (Brand Centric experience)](/help/assets/brand-centric-experience/referral-traffic-dashboard.png)


>[!NOTE]
>By default, this dashboard builds traffic insights from **CDN logs**. If your organization is on a paid offer, you can connect **Adobe Analytics** or **Google Analytics 4**(GA4) to add data that measures AI-driven discovery and site engagement. This data is available in the **Business Impact** tab. Please note that without integration to Adobe Analytics or GA4, the tab is not populated. As such, see [Adobe Analytics Integration](/help/dashboards/adobe-analytics-integration.md) or [Google Analytics Integration](/help/dashboards/google-analytics-integration.md) for more details.

<!-- ![Referral Page](/help/dashboards/assets/referral-traffic.png)-->

This page details the following:

* [Setup](#setup)
* [Filters](#filters)
* [Overall referral performance](#overall-performance)
* [Top Referral URLs](#top-referrals)
* [Referral Traffic Details](#traffic-details)

## Setup {#setup}

On first login, the Referral Traffic dashboard may appear blank. To view your data, you must configure CDN log forwarding.

You can add CDN log forwarding information by navigating to **Brands Management** and clicking on the **CDN** label.

<!-- **Customer Configuration (classic experience):** Configure [CDN log forwarding](/help/dashboards/customer-configuration.md#cdn-configuration) by selecting **Go To Configuration**.-->

<!--![Referral Setup](/help/dashboards/assets/referral-setup1.png)-->

<!--
1. Select your Source (either CDN logs or AEM Operational Telemetry).
2. Enter a primary contact email.
3. Click **Request activation** to enable data ingestion. Hiding this until confirmation from PM
-->

Once activated, the dashboard will be populated with referral traffic metrics.

## Filters {#filters}

At the top of the page, you can apply filters to refine your view. The filters you choose will impact **all** the sections present on the dashboard. You can customize the following:

* **Date Range** - Select the time frame for the displayed data. For example, the last 4 weeks. You also have the option to customize the time period by selecting the **Custom Weeks** option.
* **Platform** - Choose a specific traffic source such as Google, OpenAI, or social media.
* **Page Intent**  - Filter referral traffic by user intent.
* **Channel Source** - Filter by the channel's source. options include: LLMs, earned, paid, or mixed referral channels.
* **Device Type** - Analyze traffic by the visitor's device type either desktop, mobile or all devices.
* **Region** - View referral patterns across different geographies.

After you select the desired filter, click **Apply Filters** to apply the selection to the dashboard.

## Overall referral performance {#overall-performance}

The dashboard highlights the overall referral performance by displaying key metrics including:

* **Total Referral Traffic** - The total referral traffic from all sources.
* **Referral Traffic from LLM's** - The total referral traffic from LLM's.
* **Consent rate** -  The percentage of visitors who accept a consent prompt.
* **Bounce rate** - The percentage of sessions from referral sources that had no engagement event.

![Referral Page](/help/dashboards/assets/referral-traffic.png)

Besides the overall performance metrics presented above, there are three additional panels showing the traffic distribution across different markets, referral sources and page intent categories <!-- the **Top Regions** panel breaks down traffic by geography. Meanwhile, the **Top Referral Sources** panel shows the platforms driving the most visits. Trend indicators for the metrics show how these values are changing over time compared to the previous period.-->

<!--
## Top Referral URLs {#top-referrals}

The Top Referral URLs list surfaces your site's most visited pages from referrals.

![Top Referral URLs](/help/dashboards/assets/top-url.png)
-->

## Referral Sources Details and URL Performance Analysis {#traffic-details}

The Referral Sources Details and URL Performance Analysis tables help you evaluate both traffic volume and quality. Click on each tab below for more details:

![Referral Traffic Details](/help/dashboards/assets/traffic-details.png)

>[!BEGINTABS]

>[!TAB Referral Sources Details]

The Referral Sources Details view breaks down traffic coming from different platforms such as OpenAI, Microsoft, Google, and Perplexity. It displays key metrics like visits, bounce rate and channel type, helping you understand which AI and search sources are driving the most engaged traffic to your site.

* **Source** - The source of the referral traffic.
* **Visits** - The total number of visits for each source.
* **Bounce rate** - The percentage of sessions from the referral source that had no engagement event.
* **Channel** - The channel for the source, either earned, paid or both.

>[!TAB URL Performance Analysis]

The URL Performance Analysis view ranks top-performing pages based on referral traffic volume from LLMs and other sources. It highlights metrics like traffic, bounce rate, consent rate, and page intent, helping you identify which pages attract and retain the most engaged visitors from AI-driven referrals. The table has a search field for quick access to topics.

>[!ENDTABS]

On both tables, you can use the **Export** option to download the table .csv and share the insights with your team or include the tables in executive reporting. Additionally, for both tables, you can customize which metrics are displayed by clicking the **Configure Columns** button.
