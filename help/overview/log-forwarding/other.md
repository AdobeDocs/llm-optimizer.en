---
title: Log Forwarding - Other (Manual Upload)
description: Learn how to manually upload CDN logs to Adobe's S3 bucket for agentic traffic data collection in LLM Optimizer when using an unsupported CDN provider.
feature: Agentic Traffic
---

# Log Forwarding: Other (Manual Upload) {#log-forwarding-other}

The **Other BYOCDN** provisioning method is a catch-all option for customers who want to provide CDN logs to LLM Optimizer when:

- **Manual uploads** are preferred - for example, operational teams export logs and upload them periodically.
- **Ad-hoc automated processes** are used - one-off scripts, scheduled exports, serverless jobs.
- The customer uses a **CDN that is not natively supported** by the built-in log forwarding integrations.

This method imitates the "continuous forwarding" model: logs are produced and uploaded into the expected S3 location and are eventually processed automatically by the ingestion pipelines.

## Step 1: Onboard in LLM Optimizer {#step-1}

On [LLM Optimizer](https://llmo.now/):

1. Go to **Configuration**.

   ![Configuration button](/help/overview/assets/log-forwarding/common/config-button.png)

1. Click the **CDN Configuration** tab.

   ![CDN Configuration tab](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

1. Click **Get Started**.

   <!-- ![Onboard CDN button](/help/overview/assets/log-forwarding/common/onboard-cdn-button.png)-->

1. Next to **Activate AI Traffic Insights**, click **Configure**.

   ![Configure](/help/overview/assets/log-forwarding/common/configure.png)

1. Select **Other**.

   ![Select Other](/help/overview/assets/log-forwarding/other/other-select.png)

1. Click **Onboard**.

 <!--   ![Onboard button](/help/overview/assets/log-forwarding/common/onboard-button.png)-->

## Step 2: Prepare and upload logs {#step-2}

### Required log format (JSON Lines) {#log-format}

Logs must be uploaded as newline delimited JSON (**one JSON object per line**). Each log line must include the following fields **exactly as spelled below**.

#### Field-by-field schema {#schema}

| Field | Type | Description | Example |
|---|---|---|---|
| **timestamp** | String | The timestamp of the request following the **ISO 8601** format. | `"2025-02-01T23:00:05Z"` |
| **host** | String | The web domain that the client requested. | `"www.example.com"` |
| **url** | String | The **path** and the **query parameters** are required, while the domain should **not** be included. | `"/home?utm_source=google"` |
| **request_method** | String | The HTTP request method, sometimes referred to as HTTP verbs. | `"GET"` |
| **request_user_agent** | String | The HTTP User-Agent request header. | `"Mozilla/5.0 (compatible; GPTBot/1.0"` |
| **request_referer** | String | The HTTP Referer request header (can be empty). | `"https://chatgpt.com"` |
| **response_status** | Integer | The HTTP response status code. | `200` |
| **response_content_type** | String | The HTTP Content-Type response header. | `"text/html; charset=utf-8"` |
| **time_to_first_byte** | Integer | The time between creating a connection to the server and downloading the contents of a web page in **milliseconds**. Set to zero if unknown or unavailable. | `42` |

#### Example log lines {#example}

The following example shows three log lines:

```json
{"timestamp":"2025-02-01T23:06:14Z","host":"www.example.com","url":"/products/llm-optimizer?utm_source=google","request_method":"GET","request_user_agent":"Mozilla/5.0 (compatible; GPTBot/1.0; +https://openai.com/gptbot)","response_status":200,"request_referer":"","response_content_type":"text/html; charset=utf-8","time_to_first_byte":198}
{"timestamp":"2025-02-01T23:19:32Z","host":"www.example.com","url":"/services/ai-consulting/overview","request_method":"GET","request_user_agent":"PerplexityBot/1.0 (+https://www.perplexity.ai/perplexitybot)","response_status":200,"request_referer":"","response_content_type":"text/html; charset=utf-8","time_to_first_byte":255}
{"timestamp":"2025-02-01T23:44:05Z","host":"www.example.com","url":"/products/pricing/enterprise?utm_medium=social","request_method":"GET","request_user_agent":"ClaudeBot/1.0 (+https://www.anthropic.com)","response_status":200,"request_referer":"","response_content_type":"application/pdf","time_to_first_byte":312}
```

### Critical disclaimer (spelling and types) {#disclaimer}

The ingestion and aggregation pipelines are strict about **field names and data types**.

- Field names must match **exactly** (case and spelling).
- Data Types should be correct, as follows:
  - **timestamp** must be a string with **ISO 8601** format. UNIX-like timestamps may not work.
  - **response_status** must be an integer.
  - **time_to_first_byte** must be an integer and use milliseconds.
  - Strings must be valid JSON strings.
- Malformed JSON or missing/incorrect fields may cause logs to be skipped or fail to parse, resulting in missing data in the reports.

### Upload location and processing cadence {#upload-location}

#### Path rule {#path-rule}

Upload logs under the appropriate folder path using the format: **`yyyy/mm/dd/`** (with slashes).

An example log from Feb 1, 2025 UTC: `ABC123AdobeOrg/raw/byocdn-other/2025/02/01/`

#### Processing rule {#processing-rule}

- Logs uploaded during a given **UTC day** are processed by the pipelines **near the end of that UTC day** (daily run).
- Logs uploaded into **previous days' folders** (backfill) are **detected and processed** within 24 hours.

## Scenarios {#scenarios}

### Scenario 1: Logs in Splunk / Elasticsearch — export and upload to S3 {#scenario-splunk}

**Goal**: Retrieve logs from existing observability platforms and deliver them to the S3 location.

- Extract the required fields from Splunk/Elastic search events.
- Transform each event into one JSON object following the schema above (JSON Lines).
- Upload the resulting file(s) to the designated S3 bucket and the **current UTC day** path: `…/byocdn-other/yyyy/mm/dd/`
- The logs will be processed automatically by the end of the UTC day.

### Scenario 2: Lambda / Azure Function — format and upload to S3 {#scenario-serverless}

**Goal**: Use serverless compute to fetch/receive CDN logs, normalize them, and deliver them to the S3 location.

- The function retrieves logs from the customer's source (log store, queue, blob storage, etc.).
- The function maps fields into the expected schema and emits **JSON Lines**.
- The function uploads output to: `…/byocdn-other/yyyy/mm/dd/`
- The logs will be processed automatically by the end of the UTC day.

## Quick checklist {#checklist}

- **One JSON object per line** (JSON Lines)
- **Exact field spelling** as specified
- Correct data types
- **time_to_first_byte** in milliseconds (integer)
- Upload to the appropriate UTC folder: **yyyy/mm/dd/** under **byocdn-other**
