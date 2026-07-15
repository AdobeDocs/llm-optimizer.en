---
title: Log Forwarding - Imperva
description: Learn how to forward CDN logs from Imperva to Adobe's S3 bucket for agentic traffic data collection in LLM Optimizer.
feature: Agentic Traffic
autotag-review: '2026-07-15T17:57:30.264Z'
TQID: 'https://experienceleague.adobe.com/l-DYz7pXzFDqZn1rnZWUOG9PpRqosq00LmGrlsOMqNk'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
    internal-label: LLM Optimizer
feature_v2:
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
    internal-label: Administration
  - id: ef4e63f5-cb4d-462d-bf9a-1f617edf2a3a
    internal-label: Optimize at edge
  - id: e0828736-236a-487b-a478-5a635455eadc
    internal-label: Traffic analytics
subfeature_v2:
  - id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
    internal-label: CDN log forwarding
  - id: dd952468-5202-43af-a365-6e0d2e67a703
    internal-label: BYOCDN
  - id: e06fae5f-830b-4222-a469-b5e148d36465
    internal-label: Agentic traffic
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
---

# Log Forwarding: Imperva {#log-forwarding-imperva}

This guide explains how to forward CDN logs from Imperva to Adobe's S3 bucket for agentic traffic data collection. You will use the LLM Optimizer CDN configuration page to onboard to LLM Optimizer. After the onboarding process is complete, follow the steps provided on this page to configure log forwarding from the Imperva web console.

## Step 1: Onboard in LLM Optimizer {#step-1}

On the LLM Optimizer page [https://llmo.now/](https://llmo.now/):

1. Go to **Configuration**.

   ![Configuration button](/help/overview/assets/log-forwarding/common/config-button.png)

1. Click the **CDN Configuration** tab.

   ![CDN Configuration tab](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)
1. Click **Get Started**.
1. Next to **Activate AI Traffic Insights**, click **Configure**.

   ![Configure](/help/overview/assets/log-forwarding/common/configure.png)
1. Select **Imperva (BYOCDN)**.

   ![Select Imperva](/help/overview/assets/log-forwarding/imperva/imperva-select.png)
1. Click **Onboard**.

## Step 2: Configure log forwarding in Imperva {#step-2}

On the [Imperva console](https://my.imperva.com):

>[!NOTE]
>
>Logs should be sent daily.

1. Log in to your Imperva account at [https://my.imperva.com](https://my.imperva.com).

2. In the sidebar, go to **Logs** > **Log Setup** (or **Log Integration**).

3. Select **Amazon S3 ARN** as the connection type (log destination).

4. Enter the following:

   | Field | Description | Note |
   |---|---|---|
   | **Connection name** | A descriptive name for the connection (for example, Production S3 logs). You can rename the default. | |
   | **Path** | The location of the folder where log files will be stored. Use the format `<Amazon S3 bucket name>/<log folder>`. For example: `MyBucket/MyImpervaLogFolder`. | `Amazon S3 bucket name` is the **Bucket Name** from the LLM Optimizer configuration page. ![Bucket Name](/help/overview/assets/log-forwarding/imperva/imperva-bucket-name.png) The log folder is **Path** from the LLM Optimizer configuration page. ![Path](/help/overview/assets/log-forwarding/imperva/imperva-path.png) |

5. Click **Test connection**. Imperva runs a full test in which a test file (no real data) is sent to the designated folder and then removed when the transfer is complete.

   - **Available** — storage details are valid; you can configure logs to use this connection.
   - **Undefined** — either the required details are missing or the test failed.

6. Click **Save** to store the configuration.

7. Configure log options (log types, log level, format, compression) and **Log Levels**. You can get the values from the LLM Optimizer configuration page.

   | Field | Note |
   |---|---|
   | Log integration mode | ![Log integration mode](/help/overview/assets/log-forwarding/imperva/imperva-log-integration-mode.png) |
   | Delivery method | ![Delivery method](/help/overview/assets/log-forwarding/imperva/imperva-delivery-method.png) |
   | Log types | ![Log types](/help/overview/assets/log-forwarding/imperva/imperva-log-types.png) |
   | Log level | ![Log level](/help/overview/assets/log-forwarding/imperva/imperva-log-level.png) |
   | Format | ![Format](/help/overview/assets/log-forwarding/imperva/imperva-format.png) |
   | Compress logs | ![Compress logs](/help/overview/assets/log-forwarding/imperva/imperva-compress-logs.png) |
