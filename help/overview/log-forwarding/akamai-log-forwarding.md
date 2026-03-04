---
title: Log forwarding - Akamai (BYOCDN)
description: Learn how to forward CDN logs from Akamai to Adobe’s S3 bucket for agentic traffic data collection.
feature: Quickstart, Onboarding
---

# Akamai (BYOCDN)

This guide explains how to forward CDN logs from Akamai to Adobe’s S3 bucket for agentic traffic data collection. You will use the LLM Optimizer CDN configuration page (link TBD) to onboard to LLM Optimizer. After the onboarding process is complete (fact check), follow the steps provided on this page to configure log forwarding in the Akamai Control Panel.

## Step 1

On LLM Optimizer page [https://llmo.now/](https://llmo.now/):

1. Go to the Customer Configuration Dashboard. ![Customer Configuration Dashboard](/help/overview/assets/cc-small.png)
2. Click on the CDN configuration tab. (maybe link?)
3. Click **Onboard CDN**.
4. Select Akamai (BYOCDN) (maybe screen? )from the list and click **Onboard**.

## Step 2

On the Akamai control panel [https://control.akamai.com/](https://control.akamai.com/) follow the steps from the official Akamai documentation to [create a stream](https://techdocs.akamai.com/datastream2/docs/create-stream).

## Step 3

After creating the stream, on the Akamai control panel, click Next to continue to **Data sets** tab. Follow the steps from the official Akamai documentation  to choose the [data parameters](https://techdocs.akamai.com/datastream2/docs/choose-data-parameters). The following fields from the LLM Optimizer configuration will be needed:

![Data Parameters](/help/overview/assets/data-parameters.png)

Follow the groups below to more easily locate the parameters:

* Log Information: 
  reqTimeSec
* Geo Data 
  country
* Message exchange data
  reqHost
  reqPath
  queryStr
  reqMethod
  ua
  statusCode
  rspContentType
* Request header data 
  referer
* Network performance data 
  timeToFirstByte

## Step 4

After creating the data streams and choosing the parameters you need to configure the destination. To configure the destination, follow these steps:

1. In **Destination**, select S3.
1. In **Name**, enter a human-readable description for the destination.
1. In **Bucket**, copy the Bucket Name from the LLM Optimizer configuration page. ![Bucket Name](/help/overview/assets/bucket-name.png)
1. In **Folder path** copy Path from LLM Optimizer configuration page. ![Folder Path](/help/overview/assets/folder-path.png)
1. In **Region**, copy region from LLM Optimizer configuration page.
1. In **Access key ID** and **Secret access** key copy from the parameters from the LLM Optimizer configuration page.
1. Click **Validate & Save** to validate the connection to the destination, and save the details you provided. As part of the validation process, the system uses the provided access key identifier and secret access key to create a verification file in your S3 folder, with a timestamp in the filename in the `Akamai_access_verification_[TimeStamp].txt` format. You can only see this file if the validation process is successful, and you have access to the Amazon S3 bucket and folder that you're trying to send logs to.
1. In the **Delivery options** menu, edit the **Filename** field as follows:
    a) Change the prefix. Copy value from the LLM Optimizer configuration page Log file prefix . `{%Y}-{%m}-{%d}T{%H}:{%M}:{%S}.000`
    b) Change the suffix. Copy value from the LLM Optimizer configuration page Log file suffix.
1. Change the **Push frequency**. Copy value from the LLM Optimizer configuration page **Log Interval**. ![Log Interval](/help/overview/assets/log-interval.png)
1. Click **Next** to complete the process.
