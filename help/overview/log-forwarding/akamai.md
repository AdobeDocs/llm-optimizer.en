---
title: Log Forwarding - Akamai
description: Learn how to forward CDN logs from Akamai to Adobe's S3 bucket for agentic traffic data collection in LLM Optimizer.
feature: Agentic Traffic
---

# Log Forwarding: Akamai {#log-forwarding-akamai}

This page explains how to forward CDN logs from Akamai to Adobe’s S3 bucket for agentic traffic data collection. You will use the LLM Optimizer CDN configuration page (link TBD) to onboard to LLM Optimizer. After the onboarding process is complete, follow the steps provided on this page to configure log forwarding in the Akamai Control Panel.

## Step 1: Onboard in LLM Optimizer {#step-1}

On the LLM Optimizer page [https://llmo.now/](https://llmo.now/):

1. Go to the **Customer Configuration Dashboard**.

   ![Configuration button](/help/overview/assets/log-forwarding/common/config-button.png)

1. Click the **CDN Configuration** tab.

   ![CDN Configuration tab](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

1. Click **Get Started**.

   <!--![Onboard CDN button](/help/overview/assets/log-forwarding/common/onboard-cdn-button.png)-->

1. Next to **Activate AI Traffic Insights**, click **Configure**.

   ![Configure](/help/overview/assets/log-forwarding/akamai/akamai-configure.png)

1. Select **Akamai (BYOCDN)**.

   ![Select Akamai](/help/overview/assets/log-forwarding/akamai/akamai-select.png)

1. Click **Onboard**.

   <!--![Onboard button](/help/overview/assets/log-forwarding/common/onboard-button.png)-->

## Step 2: Create a stream in Akamai {#step-2}

On the Akamai control panel [https://control.akamai.com/](https://control.akamai.com/) follow the steps from the official Akamai documentation to [create a stream](https://techdocs.akamai.com/datastream2/docs/create-stream).

## Step 3: Choose data parameters {#step-3}

After creating the stream, on the Akamai control panel, click Next to continue to **Data sets** tab. Follow the steps from the official Akamai documentation  to choose the [data parameters](https://techdocs.akamai.com/datastream2/docs/choose-data-parameters). The following fields from the LLM Optimizer configuration will be needed:

![LLMO configuration fields](/help/overview/assets/log-forwarding/akamai/akamai-llmo-config-fields.png)

The mapping should be as follows:

* **Log Information**
  reqTimeSec -> Request time
* **Geo Data**
  country -> Country/Region
* **Message exchange data**
  reqHost -> Request host
  reqPath -> Request path
  queryStr -> Query string
  reqMethod -> Request method
  ua -> User-Agent
  statusCode -> HTTP status code
  rspContentType -> Response Content-Type
* **Request header data**
  referer -> Referer
* **Network performance data**
  timeToFirstByte -> Time to first byte

The Akamai data set fields (including IDs) are as follows:

1100, # reqTimeSec -> Request time
2012, # country -> Country/Region
1011, # reqHost -> Request host
1013, # reqPath -> Request path
2009, # queryStr -> Query string
1012, # reqMethod -> Request method
1017, # ua -> User-Agent
1008, # statusCode -> HTTP status code
1032, # referer -> Referer
1016, # rspContentType -> Response Content-Type
2025  # timeToFirstByte -> Time to first byte



## Step 4: Configure destination {#step-4}

After creating the data streams and choosing the parameters you need to configure the destination. To configure the destination, follow these steps:

1. In **Destination**, select **S3**.
2. In **Name**, enter a human-readable description for the destination.
3. In **Bucket**, copy the **Bucket Name** from the LLM Optimizer configuration page.

   ![Bucket Name](/help/overview/assets/log-forwarding/common/bucket-name.png)

4. In **Folder path**, copy the **Path** from the LLM Optimizer configuration page.

   ![Path configuration](/help/overview/assets/log-forwarding/akamai/akamai-path-config.png)

5. In **Region**, copy the **Region** from the LLM Optimizer configuration page.

   <!--![Region](/help/overview/assets/log-forwarding/common/region.png)-->

6. In **Access key ID** and **Secret access key**, copy both values from the LLM Optimizer configuration page.

   ![Access keys](/help/overview/assets/log-forwarding/common/access-keys.png)

7. Click **Validate & Save** to validate the connection to the destination, and save the details you provided. As part of this validation process, the system uses the provided access key identifier and secret access key to create a verification file in your S3 folder, with a timestamp in the filename in the `Akamai_access_verification_[TimeStamp].txt` format. You can only see this file if the validation process is successful and you have access to the Amazon S3 bucket and folder you are trying to send logs to.

8. In the **Delivery options** menu, edit the **Filename** field as follows:

   a. Change the **prefix**. Copy the value from the LLM Optimizer configuration page under **Log file prefix**:

   ```
   {%Y}-{%m}-{%d}T{%H}:{%M}:{%S}.000
   ```

   b. Change the **suffix**. Copy the value from the LLM Optimizer configuration page under **Log file suffix**.

9. Change the **Push frequency**. Copy the value from the LLM Optimizer configuration page under **Log Interval**.

   ![Log interval](/help/overview/assets/log-forwarding/akamai/akamai-log-interval.png)

10. Click **Next** to complete the process.

Before final validation, the configuration should look similar this example:

![Configuration Validation](/help/overview/assets/log-forwarding/akamai/akamai-validation.png)
