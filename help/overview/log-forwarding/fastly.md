---
title: Log Forwarding - Fastly
description: Learn how to forward CDN logs from Fastly to Adobe's S3 bucket for agentic traffic data collection in LLM Optimizer.
feature: Agentic Traffic
---

# Log Forwarding: Fastly {#log-forwarding-fastly}

This guide explains how to forward CDN logs from Fastly to Adobe's S3 bucket for agentic traffic data collection.

You will use the LLM Optimizer CDN configuration page to onboard to LLM Optimizer. After onboarding, the page will provide the required details to configure log forwarding from the Fastly web console.

## Step 1: Onboard in LLM Optimizer {#step-1}

On [LLM Optimizer](https://llmo.now/):

1. Go to **Configuration**.

   ![Configuration button](/help/overview/assets/log-forwarding/common/config-button.png)

2. Click the **CDN Configuration** tab.

   ![CDN Configuration tab](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

3. Click **Onboard CDN**.

   ![Onboard CDN button](/help/overview/assets/log-forwarding/common/onboard-cdn-button.png)

4. Select **Fastly (BYOCDN)**.

   ![Select Fastly](/help/overview/assets/log-forwarding/fastly/fastly-select.png)

5. Click **Onboard**.

   ![Onboard button](/help/overview/assets/log-forwarding/common/onboard-button.png)

## Step 2: Create an S3 endpoint in Fastly {#step-2}

On the **Fastly Control Panel**:

1. In the Fastly dashboard, go to **CDN services** (not Compute services).
2. In the **Amazon Web Services S3** area, click **Create endpoint**.
3. Fill out the **Create an Amazon S3 endpoint** fields:

| Field | Description |
| --- | --- |
| **Name** | Human-readable name for the endpoint. |
| **Placement** | Default |
| **Log format** | Use the log format string shown below. |
| **Timestamp format** | `%Y-%m-%dT%H:%M:%S.000` |
| **Bucket name** | Copy **Bucket Name** from the LLM Optimizer configuration page. ![Bucket name](/help/overview/assets/log-forwarding/fastly/fastly-bucket-name.png) |
| **Domain** | Copy **Domain Name** from the LLM Optimizer configuration page. ![Domain name](/help/overview/assets/log-forwarding/fastly/fastly-domain-name.png) |
| **Access method** | **User Credentials** |
| **User Credentials** | Copy **Access Key** and **Secret Key** from the LLM Optimizer configuration page. ![Access keys](/help/overview/assets/log-forwarding/common/access-keys.png) |
| **Period** | `300` |

**Log format string:**

```json
{ "timestamp": "%{strftime(\{"%Y-%m-%dT%H:%M:%S%z"\}, time.start)}V", "host": "%{if(req.http.Fastly-Orig-Host, req.http.Fastly-Orig-Host, req.http.Host)}V", "url": "%{json.escape(req.url)}V", "request_method": "%{json.escape(req.method)}V", "request_referer": "%{json.escape(req.http.referer)}V", "request_user_agent": "%{json.escape(req.http.User-Agent)}V", "response_status": %{resp.status}V, "response_content_type": "%{json.escape(resp.http.Content-Type)}V", "client_country_code": "%{client.geo.country_name}V", "time_to_first_byte": "%{time.to_first_byte}V" }
```

>[!WARNING]
>
>Password managers may auto-fill the **Secret Key** field with your Fastly password. If AWS integration fails, enter the Secret Key manually.

4. Click **Advanced options** and set:

| Field | Description |
| --- | --- |
| **Path** | Copy **Path** from the LLM Optimizer configuration page. ![Path](/help/overview/assets/log-forwarding/fastly/fastly-path.png) |
| **Select a log line format** | Blank |
| **Compression** | Gzip |
| **Redundancy level** | Standard |
| **ACL** | None |
| **Server side encryption** | None |
| **Maximum bytes** | 0 |

5. Click **Create** to create the endpoint.
6. From the **Activate** menu, select **Activate on Production** to deploy.

>[!NOTE]
>
>Fastly streams logs continuously to S3; the S3 website and API only make files available after upload is complete.

### Example log entry {#example}

```json
{
  "timestamp": "2026-02-10T05:05:36+0000",
  "host": "example.com",
  "url": "/my/path",
  "request_method": "GET",
  "request_referer": "https://example.com/my/other/path",
  "request_user_agent": "Mozilla/5.0 (iPhone; CPU iPhone OS 13_2_3 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/13.0.3 Mobile/15E148 Safari/604.1",
  "response_status": 200,
  "response_content_type": "text/css; charset=utf-8",
  "client_country_code": "argentina",
  "time_to_first_byte": "0.138"
}
```
