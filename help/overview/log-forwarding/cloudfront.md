---
title: Log Forwarding - CloudFront
description: Learn how to forward CDN logs from CloudFront to Adobe's S3 bucket for agentic traffic data collection in LLM Optimizer.
feature: Agentic Traffic
---

# Log Forwarding: CloudFront {#log-forwarding-cloudfront}

This guide explains how to forward CDN logs from CloudFront to Adobe's S3 bucket for agentic traffic data collection.

You will use the LLM Optimizer CDN configuration page to onboard to LLM Optimizer. After onboarding, the page will provide the required details to enable standard logging for cross-account log delivery.

## Step 1: Onboard in LLM Optimizer {#step-1}

On [LLM Optimizer](https://llmo.now/):

1. Go to **Configuration**.

   ![Configuration button](/help/overview/assets/log-forwarding/common/config-button.png)

2. Click the **CDN Configuration** tab.

   ![CDN Configuration tab](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

3. Click **Onboard CDN**.

   ![Onboard CDN button](/help/overview/assets/log-forwarding/common/onboard-cdn-button.png)

4. Enter your **AWS Account** ID.

   ![AWS Account ID](/help/overview/assets/log-forwarding/cloudfront/cloudfront-aws-account.png)

5. Select **CloudFront (BYOCDN)**.

   ![Select CloudFront](/help/overview/assets/log-forwarding/cloudfront/cloudfront-select.png)

6. Click **Onboard**.

   ![Onboard button](/help/overview/assets/log-forwarding/common/onboard-button.png)

## Step 2: Enable standard logging (CloudFront console) {#step-2}

1. In the [CloudFront console](https://console.aws.amazon.com/cloudfront/v4/home), [update an existing distribution](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/HowToUpdateDistribution.html#HowToUpdateDistributionProcedure).

2. Open the **Logging** tab.

3. Choose **Add**, then select the service to receive logs: **Amazon S3**.

4. For **Destination**, select or create the resource. Enter the **bucket name** — copy the value from the LLM Optimizer CDN configuration page.

   ![CloudFront bucket name](/help/overview/assets/log-forwarding/cloudfront/cloudfront-bucket-name.png)

5. Configure **Additional settings**:

   - **Field selection** — choose log file fields. See the required fields on the LLM Optimizer CDN configuration page.

     ![CloudFront field selection](/help/overview/assets/log-forwarding/cloudfront/cloudfront-field-selection.png)

   - **Partitioning** — copy the **path suffix** from the LLM Optimizer configuration page.

     ![CloudFront partitioning](/help/overview/assets/log-forwarding/cloudfront/cloudfront-partitioning.png)

   - **Output format** — JSON.

     ![CloudFront output format](/help/overview/assets/log-forwarding/cloudfront/cloudfront-output-format.png)

6. Finish the steps to update or create the distribution.

7. On the **Logs** page, confirm that **Enabled** appears next to the distribution.

## Enable standard logging for cross-account delivery {#cross-account}

The **source account** (with the CloudFront distribution) sends access logs to the **destination account** (the S3 bucket shown in the LLM Optimizer CDN configuration page). Both accounts must have the right permissions.

Example: source account `111111111111` sends logs to an S3 bucket in destination account `222222222222`. Use the AWS CLI.

![Delivery destination ARN](/help/overview/assets/log-forwarding/cloudfront/cloudfront-delivery-destination-arn.png)

>[!NOTE]
>
>In the commands below, replace the delivery destination ARN value (`arn:aws:logs:us-east-1:222222222222:delivery-destination:cloudfront-delivery-destination`) with the value of **Delivery destination ARN** from the LLM Optimizer configuration page.

### Configure the source account {#source-account}

1. **Create a delivery source** (replace the name and distribution ARN):

   ```bash
   aws logs put-delivery-source --name s3-cf-delivery \
     --resource-arn arn:aws:cloudfront::111111111111:distribution/E1TR1RHV123ABC \
     --log-type ACCESS_LOGS
   ```

2. **Create the delivery** (link source to destination; use the destination ARN from the "Configure the destination account" step):

   ```bash
   aws logs create-delivery --delivery-source-name s3-cf-delivery \
     --delivery-destination-arn arn:aws:logs:us-east-1:222222222222:delivery-destination:cloudfront-delivery-destination
   ```

3. **Verify:**

   - In the **source** account: CloudFront console > your distribution > **Logging** tab. Under **Type** you should see the S3 cross-account log delivery.
   - In the **destination** account: S3 console > bucket. You should see the prefix (for example, `MyLogPrefix`) and logs in that folder.
