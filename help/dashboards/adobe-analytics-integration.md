---
title: Adobe Analytics Integration
description: Learn how to connect Adobe Analytics with LLM Optimizer to measure AI-driven discovery, site engagement, and business outcomes in the Referral Traffic dashboard.
feature: Referral Traffic
---

# Adobe Analytics Integration

The Adobe Analytics integration connects LLM Optimizer with your organization's Adobe Analytics data so you can measure how AI-driven discovery translates into real website engagement and business outcomes. After the integration process is complete, the data will be available in the **Referral Traffic** dashboard under the **Business Impact** tab .

By linking analytics data with AI visibility insights, LLM Optimizer helps you track:

* User engagement on AI-referred pages.
* Conversion signals tied to AI discovery journeys.
* Performance impact of GEO optimizations.

This integration bridges the gap between AI visibility measurement and business performance analytics. Teams can now see not only where the brand appears in AI responses, but what happens after users arrive.

## Availability {#availability}

>[!IMPORTANT]
>
>The Adobe Analytics integration is included in the paid LLM Optimizer offer. Customers using the free trial will not be able to connect Adobe Analytics until they upgrade to a paid offer.

## Connect Adobe Analytics to the Referral Traffic dashboard {#connect}

The connection flow starts from the [Referral Traffic](/help/dashboards/referral-traffic.md) dashboard as follows:

1. Open the [Referral Traffic](/help/dashboards/referral-traffic.md) dashboard. The default view is **Traffic Insights**.

   ![Referral Traffic dashboard, Traffic Insights tab](/help/dashboards/assets/aa-integration-01-referral-traffic-traffic-insights.png)

1. Select the **Business Impact** tab. If no analytics provider is connected, a banner appears: **Connect to See Business Impact**, with **Connect to Analytics**.

   ![Business Impact tab with Connect to Analytics](/help/dashboards/assets/aa-integration-02-business-impact-connect.png)

1. Select **Connect to Analytics**. This opens the [Customer Configuration](/help/dashboards/customer-configuration.md) dashboard on the **Analytics** tab.

   ![Customer Configuration, Analytics tab](/help/dashboards/assets/aa-integration-03-analytics-tab.png)

1. Under **Credentials**, enter the **Client ID** and **Client Secret**, then select **Verify & Continue**. Please note the following:

   * **Verify & Continue** is available only when both fields are filled.
   * After successful verification, the report suites are loaded.
   * Use the **Client ID** and **Client Secret** of a [technical account](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/) that has access to the report suite you need.

   ![Analytics credentials and Verify & Continue](/help/dashboards/assets/aa-integration-04-credentials.png)

1. Under **Configuration**, choose a **Report Suite**.

   When a report suite is selected, LLM Optimizer loads the **Page URL Dimension** options available for that suite.

   ![Report suite selected and dimensions loading](/help/dashboards/assets/aa-integration-05-report-suite.png)

1. Choose a **Page URL Dimension** (suite-specific dimension list), then select **Save & Enable**.

   * **Page URL Dimension** stays disabled until a report suite is selected and dimensions have loaded.
   * **Save & Enable** is available only after you select a page URL dimension.

   ![Page URL dimension and Save & Enable](/help/dashboards/assets/aa-integration-06-page-url-dimension.png)

1. After saving, the configuration should show the  **Connected** status. You can return to the Referral Traffic dashboard with **Go to Referral Traffic Dashboard**. In **Referral Traffic** on the **Business Impact** tab, the status should appear as **Connected to Adobe Analytics**.

   ![Connected to Adobe Analytics in configuration and Business Impact](/help/dashboards/assets/aa-integration-07-connected.png)

### After you connect {#after-connect}

* LLM Optimizer backfills the **last four full calendar weeks** and the **current calendar week to date**.
* After backfill, data is refreshed **daily** with a pull of the **full prior day**.

>[!NOTE]
>
>The backfill may take a couple of hours to complete.

## How it works {#how-it-works}

### Configuration

During setup, you define which report suite and page dimension LLM Optimizer uses for the Adobe Analytics ingestion. The page dimension can be the standard `variables/page` mapping or a custom `eVar`, depending on your report suite.

### How LLM traffic is identified

LLM-originated traffic is identified by using the Adobe Analytics [Referrer type — Conversational AI tools](https://experienceleague.adobe.com/en/docs/analytics/components/dimensions/referrer-type#conversational-ai-tools).

### Data ingested {#data-ingested}

The following data is ingested by LLM Optimizer.

**Dimensions**

* Referrer domain
* Referrer type
* Country
* Device type
* Selected page dimension

**Metrics**

* Page views
* Visits
* Visitors
* Entries
* Exits
* Bounces
* Single-page visits
* Time spent
* Carts
* Cart additions
* Cart removals
* Cart views
* Checkouts
* Orders
* Revenue
* Units

### How LLM Optimizer uses this data

This dataset powers LLM Optimizer insights for:

* Page-level LLM traffic performance.
* Referrer performance across LLM sources.
* Regional and device-level trends.
* Downstream commerce outcomes.

## Frequently asked questions {#faq}

Q: Is the Adobe Analytics integration available during the trial?

No. The integration is available only to paid LLM Optimizer customers.

Q: What data is collected or stored?

See the [Data ingested](#data-ingested) chapter above. LLM Optimizer works with aggregated metrics from Adobe Analytics APIs authorized by your organization not raw hit-level data.

Q: How is data ingested?

Your organization authorizes LLM Optimizer to query Adobe Analytics APIs. Referral traffic aligned to LLM sources is consumed through those APIs.

Q: How often is data refreshed?

Data is refreshed **daily** (full prior day after backfill completes).

Q: Is raw hit-level data stored in LLM Optimizer?

No. Only **aggregated** metrics are used to understand traffic patterns and trends.

Q: Are full URLs, query strings, or page content stored?

Full URLs used for the selected page dimension can be ingested; query strings and page content are not ingested for this integration.

Q: Are user identifiers (ECID, IP address, cookie IDs) stored?

 No.

Q: How long is data retained?

Keep in mind that retention policies may evolve. Currently, data is stored indefinitely.

Q: Is data encrypted in transit and at rest?

Currently, data is encrypted in transit not at rest. This may change in future updates.

Q: Is historical data backfilled?

Yes. After a successful setup, the last four full calendar weeks and the current calendar week are backfilled. See also [After you connect](#after-connect)).
