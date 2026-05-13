---
title: Google Analytics Integration
description: Learn how to connect Google Analytics 4 with LLM Optimizer to measure AI-driven discovery, site engagement, and business outcomes in the Referral Traffic dashboard.
feature: Referral Traffic
---

# Google Analytics Integration

The Google Analytics 4 (GA4) integration connects LLM Optimizer with your organization's GA4 data so you can measure how AI-driven discovery on platforms such as ChatGPT, Gemini, Copilot, Claude and Perplexity translates into real website engagement and business outcomes. After you connect a GA4 property, LLM Optimizer pulls the referral traffic, engagement and conversion metrics that GA4 attributes to those sources and surfaces them in the **Referral Traffic** dashboard under the **Business Impact** tab.

## Availability {#availability}

>[!IMPORTANT]
>
>The GA4 integration is included in the paid LLM Optimizer offer. Customers using the free trial will not be able to connect GA4 until they upgrade to a paid offer.

## Before you begin {#before-you-begin}

To complete the connection you need:

* A Google account with at least **Viewer** access on the GA4 property you want to connect. Property-level access is managed in Google Analytics under **Admin > Property Access Management**.
* Permission to manage configuration in LLM Optimizer (otherwise the Connect button is visible but disabled).
* A browser that allows pop-ups from the LLM Optimizer origin — the Google sign-in step opens in a new tab.

You do **not** need to create a Google Cloud project, generate a service account, upload a JSON key or enter a Property ID. LLM Optimizer brokers the connection through Google's standard OAuth consent screen.

## Connect GA4 to the Referral Traffic dashboard {#connect}

The connection flow starts from the [Referral Traffic](/help/dashboards/referral-traffic.md) dashboard as follows:

1. Open **Referral Traffic** in LLM Optimizer.

1. Open the **Business Impact** tab.

   ![Referral Traffic dashboard, Business Impact tab](/help/dashboards/assets/ga4-integration-01-business-impact-tab.png)

1. Select **Connect to Analytics**. LLM Optimizer routes you to **Customer Configuration > Analytics**. In the Analytics Provider picker, select **Google Analytics 4**.

   ![Customer Configuration, Analytics tab with GA4 selected](/help/dashboards/assets/ga4-integration-02-analytics-ga4-picker.png)

1. Select **Connect**. A new browser tab opens to Google's sign-in screen.

   ![Google sign-in for GA4 connection](/help/dashboards/assets/ga4-integration-03-google-sign-in.png)

1. Sign in with the Google account that has access to the GA4 property you want to connect. Approve the `See and download your Google Analytics data` permission (`analytics.readonly` scope) when Google prompts you.

1. Google returns you to LLM Optimizer, which lists the GA4 properties your account can access. Select the property to connect and submit.

1. Return to the LLM Optimizer tab. The Analytics tab automatically detects the completed connection and the GA4 card shows a **Connected** status.

### After you connect {#after-connect}

After GA4 is connected to LLM Optimizer, the following occurs:

* LLM Optimizer backfills the **last four full calendar weeks** and the **current calendar week to date**.
* After backfill, data is refreshed **daily** with a pull of the **full prior day**.

>[!NOTE]
>
>The backfill may take a couple of hours to complete. The Business Impact dashboard begins to populate progressively as data lands; no action is required from you while the backfill runs.

If you reconnect (for example, to switch either the Google account or the GA4 property), only the current calendar week is backfilled again, prior weeks that are already loaded are preserved.

## How it works {#how-it-works}

### Connection model

The integration uses Google's standard OAuth 2.0 user-delegated flow. LLM Optimizer stores a refresh token scoped to your selected GA4 property and that token allows LLM Optimizer to call the GA4 Data API on your behalf (with read-only access) until you revoke it from your Google account.

### How LLM traffic is identified

LLM Optimizer asks GA4 only for the sessions GA4 itself attributes to an LLM platform. Today, those are sessions whose `sessionSourceMedium` matches one of `chatgpt`, `gemini.google.com`, `copilot.microsoft.com`, `claude` or `perplexity`. The list of supported LLM sources is maintained by Adobe and may expand over time.

### Data ingested {#data-ingested}

Each daily pull retrieves an aggregated report containing the following:

**Dimensions**

| GA4 dimension | What it represents |
| --- | --- |
| `date` | The day the session occurred. |
| `landingPage` | The first page the visitor saw on your site. |
| `countryId` | The visitor's country, as determined by GA4's IP geolocation. |
| `deviceCategory` | Mobile / desktop / tablet. |
| `sessionSourceMedium` | The LLM source/medium attributed by GA4. |

**Metrics**

| GA4 metric | What it represents |
| --- | --- |
| `sessions` | Number of sessions in the bucket. |
| `screenPageViews` | Page views in the bucket. |
| `bounceRate` | Fraction of sessions that bounced. |
| `totalPurchasers` | Distinct purchasers (if e-commerce is configured in GA4). |
| `transactions` | Transaction count (if e-commerce is configured). |
| `purchaseRevenue` | Purchase revenue (USD). |
| `totalRevenue` | Total revenue (USD). |

### How LLM Optimizer uses this data

LLM Optimizer uses this data to populate the Business Impact dashboard's page-level performance, source breakdowns, country and device splits and time trends. No data is used to train models or shared outside your tenant.

### What is not ingested

No user identifiers (Google Client ID, IP address, device ID), no session-level rows, no event-level rows, no custom dimensions or metrics beyond those listed above and no GA4 audience or segment definitions.

## Frequently asked questions {#faq}

Q: Is the GA4 integration available during the trial?

No. The integration is available only to paid LLM Optimizer customers.

Q: Do I need to create a Google Cloud project or service account?

No. The connection is a standard Google sign-in. LLM Optimizer manages the Google OAuth client on Adobe's side; you only need a Google account with Viewer access on the GA4 property.

Q: What data is collected or stored?

LLM Optimizer works with aggregated metrics from the GA4 Data API authorized by your organization, not raw event-level data.

Q: How is data ingested?

Your organization authorizes LLM Optimizer to query the GA4 Data API for the selected property. Referral traffic aligned to LLM sources is consumed through that API.

Q: How often is data refreshed?

Data is refreshed **daily** (full prior day after backfill completes).

Q: Is raw event-level data stored in LLM Optimizer?

No. Only **aggregated** metrics are used to understand traffic patterns and trends.

Q: Are full URLs, query strings or page content stored?

Landing-page paths are ingested as part of the standard report; query strings and page content are not ingested for this integration.

Q: Are user identifiers (Google Client ID, IP address, device ID) stored?

No.

Q: How long is data retained?

Currently, data is stored indefinitely.

Q: Is data encrypted in transit and at rest?

Currently, data is encrypted in transit, not at rest. This may change in future updates.

Q: Is historical data backfilled?

Yes. After a successful setup, the last four full calendar weeks and the current calendar week are backfilled. See also [After you connect](#after-connect).

Q: Can I disconnect or revoke access?

Yes — at any time. You can either reconnect to a different account or property from the GA4 card in LLM Optimizer, or revoke LLM Optimizer's access entirely from your Google account at [https://myaccount.google.com/permissions](https://myaccount.google.com/permissions). Revoking access stops new data pulls; previously ingested aggregated data remains in LLM Optimizer.

Q: My GA4 property is connected but Business Impact is empty — why?

LLM Optimizer only pulls sessions that GA4 itself attributes to a supported LLM source/medium (today: ChatGPT, Gemini, Copilot, Claude, Perplexity). If your GA4 property has not yet recorded referral sessions from any of these sources in the time window shown, the dashboard will be empty even though the connection is healthy.
