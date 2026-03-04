---
title: Log forwarding - Cloudflare (BYOCDN)
description: Learn how to forward CDN logs from Cloudflare to Adobe’s S3 bucket for agentic traffic data collection.
feature: Quickstart, Onboarding
---

# CloudFlare (BYOCDN)

This page explains how to forward CDN logs from Cloudflare to Adobe’s S3 bucket for agentic traffic data collection. You will use the LLM Optimizer CDN configuration page (link TBD) to onboard to LLM Optimizer. After the onboarding process is complete (fact check), follow the steps provided on this page to configure log forwarding in the Cloudflare dashboard console.

## Step 1

On LLM Optimizer page [https://llmo.now/](https://llmo.now/):

1. Go to the Customer Configuration Dashboard. ![Customer Configuration Dashboard](/help/overview/assets/cc-small.png)
2. Click on the CDN configuration tab. (maybe link?)
3. Click **Onboard CDN**.
4. Select Akamai (BYOCDN) (maybe screen? )from the list and click **Onboard**.

## Step 2

On the Cloudflare dashboard, follow these steps:

1. Go to the **Logpush** page at the **Domain (zone)** level.
1. Select **Create a Logpush job**.
1. In **Select a destination**, choose **Amazon S3**.
1. Enter the following destination information:

* **Bucket** — the S3 bucket name. Copy the value from the LLM Optimizer CDN Configuration page. ![Bucket Name Cloudfare](/help/overview/assets/bucket-name-cloudflare.png)
* **Path** — the bucket location within the storage container. Copy the value from the LLM Optimizer CDN Configuration page.
* **Organize logs into daily subfolders** (recommended) ![Organize Logs](/help/overview/assets/organize-logs.png)
* **Bucket region** - Copy the value from the LLM Optimizer CDN Configuration page.
* If server side encryption not needed.

When you complete the steps above click **Continue** and do the following:

1. To prove ownership, Cloudflare will send a file to your designated destination. To find the token, select the **Open** button in the **Overview** tab of the ownership challenge file. Copy the ownership token from the LLM Optimizer CDN configuration page then paste it into the Cloudflare dashboard to verify your access to the bucket. Enter the Ownership Token and select **Continue**.
1. Select **HTTP Requests** dataset to push to the storage service.
1. Configure your Logpush job:






