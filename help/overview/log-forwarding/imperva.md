---
title: Log Forwarding - Imperva
description: Learn how to forward CDN logs from Imperva to Adobe's S3 bucket for agentic traffic data collection in LLM Optimizer.
feature: Agentic Traffic
---

# Log Forwarding: Imperva {#log-forwarding-imperva}

This guide explains how to forward CDN logs from Imperva to Adobe's S3 bucket for agentic traffic data collection. You will use the LLM Optimizer CDN configuration page to onboard to LLM Optimizer. After the onboarding process is complete, follow the steps provided on this page to configure log forwarding from the Imperva web console.

## Step 1: Onboard in LLM Optimizer {#step-1}

On the LLM Optimizer page [https://llmo.now/](https://llmo.now/):

1. Go to **Configuration**.

   ![Configuration button](/help/overview/assets/log-forwarding/common/config-button.png)

1. Click the **CDN Configuration** tab.

   ![CDN Configuration tab](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)
1. Click **Onboard CDN**.
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
   | **Connection name** | A descriptive name for this connection (for example, Production S3 logs). You can rename the default. | |
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
