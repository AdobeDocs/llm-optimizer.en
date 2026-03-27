---
title: Adobe Analytics integration
description: "Learn how to connect Adobe Analytics with LLM Optimizer to measure AI-driven discovery, site engagement, and business outcomes in Referral Traffic."
feature: Referral Traffic
---

# Adobe Analytics integration

The Adobe Analytics integration connects LLM Optimizer with your organization's Adobe Analytics data so you can measure how AI-driven discovery relates to real website engagement and business outcomes.

## Value {#value}

By linking analytics data with AI visibility insights, LLM Optimizer helps you track:

* User engagement on AI-referred pages
* Conversion signals tied to AI discovery journeys
* Performance impact of GEO optimizations

This integration connects AI visibility measurement with business performance analytics. Teams can see not only where the brand appears in AI responses, but what happens after users arrive.

## Availability {#availability}

>[!IMPORTANT]
>
>The Adobe Analytics integration is included with the paid LLM Optimizer offer. Organizations on the free trial cannot connect Adobe Analytics until they upgrade to a paid offer.

## Connect Adobe Analytics (Referral Traffic) {#connect}

The connection flow starts from the [Referral Traffic](/help/dashboards/referral-traffic.md) dashboard, where you open the **Business Impact** experience and complete analytics credentials in [Customer Configuration](/help/dashboards/customer-configuration.md).

1. Open the [Referral Traffic](/help/dashboards/referral-traffic.md) dashboard.

   The default view is often **Traffic Insights**.

   ![Referral Traffic dashboard, Traffic Insights tab](/help/dashboards/assets/aa-integration-01-referral-traffic-traffic-insights.png)

1. Select the **Business Impact** tab.

   If no analytics provider is connected, a banner appears: **Connect to See Business Impact**, with **Connect to Analytics**.

   ![Business Impact tab with Connect to Analytics](/help/dashboards/assets/aa-integration-02-business-impact-connect.png)

1. Select **Connect to Analytics**.

   You are taken to [Customer Configuration](/help/dashboards/customer-configuration.md) on the **Analytics** tab.

   ![Customer Configuration, Analytics tab](/help/dashboards/assets/aa-integration-03-analytics-tab.png)

1. Under **Credentials**, enter the **Client ID** and **Client Secret**, then select **Verify & Continue**.

   * **Verify & Continue** is available only when both fields are filled.
   * After verification succeeds, report suites load for selection.
   * Use the **Client ID** and **Client Secret** for a [technical account](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/){target="_blank"} that has access to the report suite you need.

   ![Analytics credentials and Verify & Continue](/help/dashboards/assets/aa-integration-04-credentials.png)

1. Under **Configuration**, choose a **Report Suite**.

   When a report suite is selected, LLM Optimizer loads the **Page URL Dimension** options available for that suite.

   ![Report suite selected and dimensions loading](/help/dashboards/assets/aa-integration-05-report-suite.png)

1. Choose a **Page URL Dimension**, then select **Save & Enable**.

   * **Page URL Dimension** stays disabled until a report suite is selected and dimensions have loaded.
   * **Save & Enable** is available only after you select a page URL dimension.

   ![Page URL dimension and Save & Enable](/help/dashboards/assets/aa-integration-06-page-url-dimension.png)

1. After saving, the configuration shows **Connected**. You can return to the dashboard with **Go to Referral Traffic Dashboard**. In **Referral Traffic** on **Business Impact**, the status appears as **Connected to Adobe Analytics**.

   ![Connected to Adobe Analytics in configuration and Business Impact](/help/dashboards/assets/aa-integration-07-connected.png)

### After you connect {#after-connect}

* The last four full calendar weeks and the current calendar week are backfilled.
* After backfill, data is refreshed with a **daily** pull of the full prior day.

## How it works {#how-it-works}

### Configuration

During setup, you define which report suite and page dimension LLM Optimizer uses for Adobe Analytics ingestion. The page dimension can be the standard `variables/page` mapping or a custom eVar that represents the page URL, depending on your report suite.

After you save the configuration:

* LLM Optimizer backfills the **last four full calendar weeks** and the **current calendar week to date**
* LLM Optimizer then runs **daily** and ingests the **full prior day**

>[!NOTE]
>
>Backfill can take a few hours to complete.

### How LLM traffic is identified

LLM-originated traffic is identified using Adobe Analytics when **Referrer type** is **Conversational AI tools**. See [Referrer type — Conversational AI tools](https://experienceleague.adobe.com/en/docs/analytics/components/dimensions/referrer-type#conversational-ai-tools){target="_blank"} in the Adobe Analytics documentation.

### Data ingested {#data-ingested}

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

This dataset supports LLM Optimizer insights for:

* Page-level LLM traffic performance
* Referrer performance across LLM sources
* Regional and device-level trends
* Downstream commerce outcomes

## Frequently asked questions {#faq}

Q: Is the Adobe Analytics integration available during the trial?

A: No. The integration is available only to paid LLM Optimizer customers.

Q: What data is collected or stored?

A: See [Data ingested](#data-ingested). LLM Optimizer works with aggregated metrics from Adobe Analytics APIs authorized by your organization—not raw hit-level exports for individual users.

Q: How is data ingested?

A: Your organization authorizes LLM Optimizer to query Adobe Analytics APIs. Referral traffic aligned to LLM sources is consumed through those APIs.

Q: How often is data refreshed?

A: Data is refreshed **daily** (full prior day after backfill completes).

Q: Is raw hit-level data stored in LLM Optimizer?

A: No. Only **aggregated** metrics are used to understand traffic patterns and trends.

Q: Are full URLs, query strings, or page content stored?

A: Full URLs used for the selected page dimension can be ingested; query strings and page content are not ingested for this integration.

Q: Are user identifiers (ECID, IP address, cookie IDs) stored?

A: No.

Q: How long is data retained?

A: Retention policies may evolve. Contact Adobe or your account team for current retention terms.

Q: Is data encrypted in transit and at rest?

A: Data is encrypted **in transit**. For encryption **at rest**, rely on your organization's Adobe Analytics and cloud commitments; confirm details with Adobe if you have compliance requirements.

Q: Is historical data backfilled?

A: Yes. After a successful setup, the last four full calendar weeks and the current calendar week are backfilled (see [After you connect](#after-connect)).
