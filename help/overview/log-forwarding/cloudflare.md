---
title: Log Forwarding - Cloudflare
description: Learn how to forward CDN logs from Cloudflare to Adobe's S3 bucket for agentic traffic data collection in LLM Optimizer.
feature: Agentic Traffic
---

# Log Forwarding: Cloudflare {#log-forwarding-cloudflare}

This page explains how to forward CDN logs from Cloudflare to Adobe’s S3 bucket for agentic traffic data collection. You will use the LLM Optimizer CDN configuration page (link TBD) to onboard to LLM Optimizer. After the onboarding process is complete (fact check), follow the steps provided on this page to configure log forwarding in the Cloudflare dashboard console.

## Step 1: Onboard in LLM Optimizer {#step-1}

On LLM Optimizer page [https://llmo.now/](https://llmo.now/)::

1. Go to the Customer **Configuration Dashboard**.

   ![Configuration button](/help/overview/assets/log-forwarding/common/config-button.png)

1. Click the **CDN Configuration** tab.

   ![CDN Configuration tab](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

1. Click **Onboard CDN**.

   <!-- ![Onboard CDN button](/help/overview/assets/log-forwarding/common/onboard-cdn-button.png) -->

1. Select **Cloudflare (BYOCDN)**.

   ![Select Cloudflare](/help/overview/assets/log-forwarding/cloudflare/cloudflare-select.png)

1. Click **Onboard**.

   <!-- ![Onboard button](/help/overview/assets/log-forwarding/common/onboard-button.png)-->

## Step 2: Create a Logpush job in Cloudflare {#step-2}

On the Cloudflare dashboard, follow these steps:

1. Go to the **Logpush** page at the **Domain (zone)** level.
1. Select **Create a Logpush job**.
1. In **Select a destination**, choose **Amazon S3**.
1. Enter the following destination information:

   - **Bucket** — the S3 bucket name. Copy the value from the LLM Optimizer CDN Configuration page.

     ![Bucket Name](/help/overview/assets/log-forwarding/common/bucket-name.png)

   - **Path** — the bucket location within the storage container. Copy the value from the LLM Optimizer CDN Configuration page.

     ![Cloudflare path](/help/overview/assets/log-forwarding/cloudflare/cloudflare-path.png)

   - **Organize logs into daily subfolders** (recommended).

     ![Daily subfolders](/help/overview/assets/log-forwarding/cloudflare/cloudflare-daily-subfolders.png)

   - **Bucket region** — copy the value from the LLM Optimizer CDN Configuration page.

     <!-- ![Region](/help/overview/assets/log-forwarding/cloudflare/cloudflare-region.png)-->

   - If server-side encryption is not needed, leave unchecked.

   After you complete the steps above, select **Continue**.

1. To prove ownership, Cloudflare will send a file to your designated destination. To find the token, select the **Open** button in the **Overview** tab of the ownership challenge file. Copy the ownership token from the LLM Optimizer CDN configuration page then paste it into the Cloudflare dashboard to verify your access to the bucket. Enter the Ownership Token and select **Continue**.

   <!--![Ownership token](/help/overview/assets/log-forwarding/cloudflare/cloudflare-ownership-token.png)-->

1. Select the **HTTP Requests** dataset to push to the storage service.

1. Configure your Logpush job:

   - Enter the **Job name**.

   - In **Send the following fields**, see the values in the LLM Optimizer configuration page.

     ![Logpush fields](/help/overview/assets/log-forwarding/cloudflare/cloudflare-logpush-fields.png)

   - **Log format**: JSON.

     <!--![JSON format](/help/overview/assets/log-forwarding/cloudflare/cloudflare-json-format.png)-->

1. In **Advanced Options**:

   - Choose the format of timestamp fields in your logs: `RFC3339`.

     ![Timestamp format](/help/overview/assets/log-forwarding/cloudflare/cloudflare-timestamp-format.png)

   - For sampling rates, select **All logs**.

     ![Sampling rate](/help/overview/assets/log-forwarding/cloudflare/cloudflare-sampling-rate.png)

1. Select **Submit** once you are done configuring your Logpush job.
