---
title: Referral Traffic
description: Learn how to use the Referral Traffic dashboard to see how visitors arrive at your site from external platforms, AI citations, and referral links..
---

# Referral Traffic

Referral Traffic shows how visitors arrive at your site from external platforms, AI citations, and referral links. It tracks and analyzes traffic sources, referral patterns, and conversion metrics from external websites and platforms. This will help you understand which sources, regions, and pages drive the most engaged traffic. Data is sourced from either the CDN logs or AEM Operational Telemetry **(add link)**. Both of these sources are privacy-preserving and do not capture personal user data.

There are also customizable filters to help you refine the displayed data.

This page details the following:

* [Setup](#setup)
* [Filters](#filters)
* [Overall referral performance](#overall-performance)
* [Top Referral URLs](#top-referrals)
* [Referral Traffic Details](#traffic-details)

## Setup {#setup}

On first login, the Referral Traffic dashboard may appear blank. To view your data, you must configure a referral traffic provider.

![Referral Setup](/help/dashboards/assets/referral-setup.png)

1. Select your Source (either CDN logs or AEM Operational Telemetry).
2. Enter a primary contact email.
3. Click **Request activation** to enable data ingestion.

Once activated, the dashboard will populate with referral traffic metrics. 

## Filters {#filters}

At the top of the page, you can apply filters to refine your view. The filters you choose will impact **all** the sections present on the dashboard. You can customize the following:

**Date Range** - Select the time frame for the displayed data. For example, the last 4 weeks. You also have the option to customize the time period by selecting the **Custom Weeks** option.
**Platform** - Choose a specific traffic source such as Google, OpenAI, or social media.
**Channel** - Filter between channels such as earned or paid. If you prefer a mix between the two select the the **All Channels** option.
**Channel Source** - Filter by the channel's source. options include: display, search, referral, video and social. You can also use the **All Platforms** to display all channel sources.
**Device Type** - Analyze traffic by the visitor's device type either desktop, mobile or all devices.
**Region** - View referral patterns across different geographies.

After you select the desired filter, click **Apply Filters** to apply the selection to the dashboard.

## Overall referral performance {#overall-performance}

The dashboard highlights the overall referral performance by displaying the following key metrics:

* **Total Referral Traffic** - The total referral traffic from all sources.
* **Consent rate** -  The percentage of visitors who accept a consent prompt.
* **Bounce rate** - The percentage of sessions from referral sources that had no engagement event.

![Referral Page](/help/dashboards/assets/referral-traffic.png)

Besides the overall performance metrics presented above, the **Top Regions** panel breaks down traffic by geography. Meanwhile, the **Top Referral Sources** panel shows the platforms driving the most visits.

## Top Referral URLs {#top-referrals}

The Top Referral URLs list surfaces your site’s most visited pages from referrals.

![Top Referral URLs](/help/dashboards/assets/top-url.png)

## Referral Traffic Details {#traffic-details}

The Referral Traffic Details table helps you evaluate both traffic volume and quality. It provides a detailed breakdown by source, including visit counts, bounce rates, and channel type.

![Referral Traffic Details](/help/dashboards/assets/traffic-details.png)

The table contains the following categories:

**Source** - The source of the referral traffic.
**Visits** - The total number of visits for each source.
**Bounce rate** - The percentage of sessions from the referral source that had no engagement event.
**Channel** - The channel for the source, either earned, paid or both.

You can use the **Export** option to download the table .csv and share the insights with your team or include the referral traffic table in executive reporting.
