---
title: Optimize at Edge - CloudFront (BYOCDN)
description: Learn how to configure CloudFront BYOCDN for Optimize at Edge in LLM Optimizer.
feature: Opportunities
---

# CloudFront (BYOCDN)

This configuration routes agentic traffic (requests from AI bots and LLM user agents) to the Edge Optimize backend service (`live.edgeoptimize.net`). Human visitors and SEO bots continue to be served from your origin as usual. To test the configuration, after the setup is complete, look for the header `x-edgeoptimize-request-id` in the response.

**Prerequisites**

Before setting up the CloudFront configuration, ensure you have:

* An existing CloudFront distribution serving your website.
* AWS IAM permissions to create Lambda functions, IAM roles, CloudFront distributions, and cache policies.
* Completed the LLM Optimizer onboarding process.
* Completed CDN log forwarding to LLM Optimizer.
* An Edge Optimize API key retrieved from the LLM Optimizer UI.

{{retrieve-byocdn-api-key}}

**Step 1: Create Edge Optimize Origin**

**Navigation:** AWS Console > CloudFront > Distributions > [Your Distribution] > Origins tab

1. Click **Create origin**.

2. Configure the origin:
   * **Origin domain:** `live.edgeoptimize.net`
   * **Name:** `EdgeOptimize_Origin`

3. Leave all other fields with their default values.

4. Add custom headers:

   | Header | Value |
   |--------|-------|
   | `x-edgeoptimize-api-key` | Your API key |
   | `x-forwarded-host` | `www.example.com` |

   Replace `www.example.com` with your actual website domain and `Your API key` with the Edge Optimize API key provided by your Adobe representative.

5. Click **Create origin**.

  ![Cloudfront Origin Creation](/help/assets/optimize-at-edge/cloudfront-origin-creation.png)

**Step 2: Create viewer request function**

**Navigation:** AWS Console > CloudFront > Functions

1. Click **Create function**.

2. Configure:
   * **Name:** `edgeoptimize-routing`
   * **Runtime:** `cloudfront-js-2.0`

3. Replace the default code with the code from [viewer-request.js](https://github.com/adobe-rnd/llmo-edge-optimize-samples/blob/main/cloudfront/cloudfront-function/viewer-request.js).

   Before publishing, customize the following values in the code:

   * `YOUR_DEFAULT_ORIGIN` — Replace with the name of your existing default origin (found in CloudFront > Distributions > [Your Distribution] > Origins tab).
   * `TARGETED_PATHS` — Set to `null` to target all HTML pages, or set to an array of specific paths, for example, `['/', '/products', '/about']`.

4. Click **Save changes** > **Publish function**.
  
  ![Cloudfront Function Creation](/help/assets/optimize-at-edge/cloudfront-function-creation.png)


**Step 3: Configure cache policy**

**Navigation:** AWS Console > CloudFront > Distributions > [Your Distribution] > Behaviors

Check the cache policy currently attached to your behavior. Click **Edit** on your behavior and look at the **Cache key and origin requests** section to identify your scenario:

* **Scenario A (Legacy):** You see a radio button labeled **Legacy cache settings** selected. There is no policy name dropdown — instead you see inline TTL and header settings.
* **Scenario B (Custom policy):** You see **Cache policy** selected with a policy name that you or your team created (not an AWS-provided policy).
* **Scenario C (Managed policy):** You see **Cache policy** selected with an AWS-provided name like `CachingOptimized`, `CachingDisabled`, or `CachingOptimizedForUncompressedObjects` — these cannot be edited.

**Scenario A: Legacy cache settings**

If your behavior uses legacy cache settings:

1. Under **Cache key and origin requests**, you will see **Legacy cache settings** selected.

2. Add `x-edgeoptimize-config` and `x-edgeoptimize-url` to the **Headers** allow list:

   * Select **Include the following headers** from the dropdown.
   * Add `x-edgeoptimize-config` and `x-edgeoptimize-url`.
   ![Cloudfront Cache Legacy](/help/assets/optimize-at-edge/cloudfront-cache-policy-legacy.png)

   If you already have **All** selected in the Headers dropdown, skip this step — all headers are automatically forwarded to the origin.

3. Check the **Object caching** setting:

   * If set to **Customize** — it is recommended to set **Minimum TTL** to `0`. However, if your current Minimum TTL is already very short, you may not need to change it.
   * If set to **Use origin cache headers** — no change needed.

4. Click **Save changes**.

**Scenario B: Non-legacy with a custom cache policy**

If your behavior already uses a custom cache policy (one you created, not an AWS managed policy):

**Navigation:** AWS Console > CloudFront > Policies > Cache

1. Click on your existing policy.

2. Click **Edit**.

3. It is recommended to set **Minimum TTL** to `0`. However, if your current Minimum TTL is already very short, you may not need to change it.
   ![Cache policy TTL settings](/help/assets/optimize-at-edge/cloudfront-cache-policy-ttl.png)

4. Under **Cache key settings** > **Headers**, along with your existing inclusions, add `x-edgeoptimize-config` and `x-edgeoptimize-url`.
   ![Cache policy headers](/help/assets/optimize-at-edge/cloudfront-cache-policy-headers.png)

5. Click **Save changes**.

**Scenario C: Non-legacy with a managed (AWS) cache policy**

If your behavior uses an AWS managed cache policy (for example, `CachingOptimized`), you cannot edit it. You need to create a new custom cache policy that replicates the existing managed policy settings and adds the Edge Optimize headers on top.

**Part 1: Note down your current managed cache policy settings**

**Navigation:** AWS Console > CloudFront > Policies > Cache

1. Find and click on the managed cache policy currently attached to your behavior (for example, `CachingOptimized`).

2. Note down all the existing settings:
   * Minimum TTL, Maximum TTL, Default TTL
   * Headers included in the cache key
   * Cookies included in the cache key
   * Query strings included in the cache key
   * Compression support (Gzip, Brotli)

**Part 2: Create a new custom cache policy with the same settings + Edge Optimize config**

**Navigation:** AWS Console > CloudFront > Policies > Cache

1. Click **Create cache policy**.

2. **Name:** `edgeoptimize-cache`

   ![Cache policy name](/help/assets/optimize-at-edge/cloudfront-cache-policy-name.png)

3. Replicate all the settings noted in Part 1, with the following modifications:

   * It is recommended to set **Minimum TTL** to `0`. However, if your current Minimum TTL is already very short, you may not need to change it.

   ![Cache policy TTL settings](/help/assets/optimize-at-edge/cloudfront-cache-policy-ttl.png)

   * Under **Cache key settings** > **Headers**, include everything the managed policy had, plus add `x-edgeoptimize-config` and `x-edgeoptimize-url`.

   ![Cache policy headers](/help/assets/optimize-at-edge/cloudfront-cache-policy-headers.png)

4. Click **Create**.

5. Go back to your behavior and associate the newly created policy:

   **Navigation:** AWS Console > CloudFront > Distributions > [Your Distribution] > Behaviors

   1. Edit your behavior.
   2. Under **Cache key and origin requests**, select **Cache policy**.
   3. Choose `edgeoptimize-cache` from the dropdown.
   4. Click **Save changes**.

**Step 4: Create Lambda@Edge function (origin request and response)**

>[!IMPORTANT]
>Lambda@Edge functions **must be created in the `us-east-1` (N. Virginia) region**. This is an AWS requirement. Even though the function is created in `us-east-1`, AWS automatically replicates it to all CloudFront edge locations worldwide, so it executes at the nearest edge location to the viewer. Make sure you are in the `us-east-1` region in the AWS Console before proceeding.

**Create the Lambda function**

**Navigation:** AWS Console > Lambda

1. Click **Create function**.

2. Select **Author from scratch**.

3. Configure:
   * **Function name:** `edgeoptimize-origin`
   * Leave all other fields with their default values.

4. Click **Create function**.

5. In the code editor, replace the default code with the code from [origin-request-response.js](https://github.com/adobe-rnd/llmo-edge-optimize-samples/blob/main/cloudfront/lambda/origin-request-response.js).

6. Click **Deploy** to save the code.

7. Note the **execution role name** shown under **Configuration** > **Permissions** (for example, `edgeoptimize-origin-role-xxxxx`). You need this in the following steps.

**Update the execution role's trust policy**

The auto-created role only trusts `lambda.amazonaws.com`. For Lambda@Edge, you must also add `edgelambda.amazonaws.com`.

**Navigation:** AWS Console > IAM > Roles > [your role from the previous step] > Trust relationships tab

1. Click **Edit trust policy**.

2. Replace the policy with the content from [trust-policy.json](https://github.com/adobe-rnd/llmo-edge-optimize-samples/blob/main/cloudfront/lambda/trust-policy.json).

3. Click **Update policy**.

>[!WARNING]
>The `edgelambda.amazonaws.com` service principal is **required** for Lambda@Edge. Without it, CloudFront cannot invoke your function at edge locations.

**Fix the CloudWatch Logs permission policy**

The auto-created role comes with an `AWSLambdaBasicExecutionRole` policy configured for regular Lambda, which has the wrong region and log group name for Lambda@Edge. You need to update it.

**Navigation:** AWS Console > IAM > Roles > [your role] > Permissions tab > click on the attached policy name (for example, `AWSLambdaBasicExecutionRole-xxxx`)

1. Click **Edit**.

2. Replace the policy with the content from [cloudwatch-policy.json](https://github.com/adobe-rnd/llmo-edge-optimize-samples/blob/main/cloudfront/lambda/cloudwatch-policy.json).

   In the JSON, replace `ACCOUNT_ID` with your actual AWS account ID (found in the top-right corner of the AWS Console) and `FUNCTION_NAME` with the name of your Lambda function (for example, `edgeoptimize-origin`).

3. Click **Save changes**.

>[!WARNING]
>The region in the ARN must be `*` — Lambda@Edge executes at the nearest edge location to the viewer, so logs are written to CloudWatch in the region of the edge location (for example, `ap-south-1`, `eu-west-1`), not necessarily `us-east-1`. The log group uses a region-prefixed name: `/aws/lambda/us-east-1.FUNCTION_NAME`, where `us-east-1` is always the function's home region.

**Publish a version**

1. On the function page, click **Actions** (top right) > **Publish new version**.

2. Add a description.

3. Click **Publish**.
   ![Lambda Publish](/help/assets/optimize-at-edge/cloudfront-lambda-publish.png)

4. Copy or note down the **Function ARN** — you need this in the next step.
   ![Lambda ARN](/help/assets/optimize-at-edge/cloudfront-lambda-arn.png)

**Step 5: Associate the functions and cache policy with behavior**

**Navigation:** AWS Console > CloudFront > Distributions > [Your Distribution] > Behaviors

1. Edit your behavior.

2. If you created a new cache policy in Step 3 (Scenario C), set **Cache policy** to `edgeoptimize-cache`.
   ![Cache Policy](/help/assets/optimize-at-edge/cloudfront-behaviour-cache.png)

3. Under **Function associations**, configure:

   * **Viewer request:** `edgeoptimize-routing`
   * **Origin request:** Versioned Function ARN from Step 4 (in **Publish a version**)
   * **Origin response:** Versioned Function ARN from Step 4 (in **Publish a version**)

   ![Function associations configuration](/help/assets/optimize-at-edge/cloudfront-function-association.png)

4. Click **Save changes**.

**Step 6: Test the configuration**

**1. Test bot traffic (should be optimized)**

Send a request with an agentic bot user agent. On the **first request**, Edge Optimize may return a proxied (non-optimized) response while it processes and caches the page. You can identify this by the `x-edgeoptimize-proxy: 1` header in the response.

Simulate an AI bot request using an agentic user-agent:

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: chatgpt-user"
```

A successful response includes the `x-edgeoptimize-request-id` header, confirming that the request was routed through Edge Optimize:

```
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

**2. Test human traffic (should NOT be affected)**

Simulate a regular human browser request:

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36"
```

The response should **not** contain the `x-edgeoptimize-request-id` header. The page content and response time should remain identical to before enabling Optimize at Edge.

**3. How to differentiate between the two scenarios**

| Header | Bot traffic (optimized) | Human traffic (unaffected) |
|---|---|---|
| `x-edgeoptimize-request-id` | Present — contains a unique request ID | Absent |
| `x-edgeoptimize-fo` | Present only if failover occurred (value: `1`) | Absent |

The status of the traffic routing can also be checked in the LLM Optimizer UI. Navigate to **Customer Configuration** and select the **CDN Configuration** tab.

![AI Traffic Routing status with routing enabled](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

**4. Verify logs are flowing correctly**

After running the test requests above, verify that logs are being written for both the CloudFront function and the Lambda@Edge function.

*CloudFront function logs (`edgeoptimize-routing`)*

**Navigation:** AWS Console > CloudWatch > Log groups (in `us-east-1` or the region where your CloudFront distribution is configured)

1. Look for a log group named `/aws/cloudfront/function/edgeoptimize-routing`.
2. Open the latest log stream.
3. For agentic requests, you should see entries such as:
   * `Adding origin group for userAgent: chatgpt-user`
   * `Routing to Edge Optimize origin for userAgent: chatgpt-user`
4. For non-agentic requests, you should see:
   * `Routing to Default origin for userAgent: ...`

You can also check the **Metrics** tab under **AWS Console > CloudFront > Functions > edgeoptimize-routing** to view invocation counts and error rates.

*Lambda@Edge logs (`edgeoptimize-origin`)*

>[!IMPORTANT]
>Lambda@Edge logs are written to CloudWatch in the **region of the edge location** that served the request, not `us-east-1`. Check CloudWatch in the AWS region closest to where you ran the curl command.

**Navigation:** AWS Console > CloudWatch > Log groups (ensure you are in the correct region)

1. Look for a log group named `/aws/lambda/us-east-1.edgeoptimize-origin`.
2. Open the latest log stream.
3. For agentic requests, you should see entries such as:
   * `Calling Edge Optimize Origin for agentic requests` — primary path
   * `Calling Default Origin in case of failover for agentic requests` — failover path
   * `Failover Triggered for agentic requests` — origin-response failover detection

If the log group is not present, verify that the IAM permissions were updated correctly in Step 4. Also check other nearby AWS regions — the edge location that served your request may differ from what you expect.

**Troubleshooting**

| Issue | Possible Cause | Solution |
|-------|----------------|----------|
| No `x-edgeoptimize-request-id` in response for agentic requests | Origin group not routing to Edge Optimize | Verify `YOUR_DEFAULT_ORIGIN` was replaced correctly in the CloudFront function code (Step 2). |
| 403 errors on agentic requests | Invalid or missing API key | Check the `x-edgeoptimize-api-key` header value in the Edge Optimize origin custom headers (Step 1). |
| Cannot find CloudWatch logs for Lambda@Edge | Wrong IAM permissions | Verify the CloudWatch Logs permission policy was updated (Step 4). Note: Lambda@Edge logs appear in the edge region that served the request, not necessarily `us-east-1`. |
| Cache not honoring `cache-control: no-store` | Minimum TTL may be too high | Set Minimum TTL to `0` in your cache policy (Step 3). If your Minimum TTL is already very short, this may not be the issue. |
| Regular (non-agentic) traffic broken after setup | Cache policy misconfiguration | If you created a new cache policy (Scenario C), ensure you replicated all settings from the original managed policy. |

**Disabling and Re-enabling Optimize at Edge**

The Lambda@Edge function (`edgeoptimize-origin`) is associated with the origin request and origin response events of your CloudFront behavior. Because it runs inline on every request passing through that behavior — both human and agentic — a Lambda@Edge outage will impact all live traffic, not just agentic requests. If you detect a Lambda@Edge outage, remove the function associations immediately to restore normal traffic flow to your default origin.

**How to detect a Lambda@Edge outage**

* **AWS Service Health Dashboard** — Check the [AWS Service Health Dashboard](https://health.aws.amazon.com/health/status) for any active incidents affecting **Amazon CloudFront** or **AWS Lambda**. A global or regional outage reported here is the fastest way to confirm the issue is on the AWS infrastructure side rather than in your configuration.
* **Lambda@Edge errors** — Navigate to **AWS Console > CloudFront > Monitoring > [Your Distribution]**. Open the **Lambda@Edge errors** tab and check the **Execution errors** graph for execution errors. If these are high, Lambda@Edge might be down.

**Detaching the Lambda@Edge function**

**Navigation:** AWS Console > CloudFront > Distributions > [Your Distribution] > Behaviors

1. Click **Edit** on your behavior.

2. Scroll down to the **Function associations** section.

3. Set the following associations to **No association**:

   | Event | Change to |
   |---|---|
   | Viewer request | No association |
   | Origin request | No association |
   | Origin response | No association |

   ![Function associations configuration](/help/assets/optimize-at-edge/cloudfront-no-function-association.png)

4. Click **Save changes**.

5. Wait for the CloudFront distribution to finish deploying. The status changes from **Deploying** to the last modified date, typically within a few minutes.

Once deployed, all traffic routes directly to your default origin. No configuration is deleted; the Lambda function and its associations can be restored at any time.

**Re-attaching the Lambda@Edge function**

**Navigation:** AWS Console > CloudFront > Distributions > [Your Distribution] > Behaviors

1. Click **Edit** on your behavior.

2. Scroll down to the **Function associations** section.

3. Restore the associations:

   | Event | Set to |
   |---|---|
   | Viewer request | `edgeoptimize-routing` (CloudFront function) |
   | Origin request | Versioned Lambda ARN from Step 4 |
   | Origin response | Versioned Lambda ARN from Step 4 |

   Use the versioned **Function ARN** you noted in Step 4 (in **Publish a version**).

   ![Function associations configuration](/help/assets/optimize-at-edge/cloudfront-function-association.png)

4. Click **Save changes**.

5. Wait for the distribution to finish deploying, then verify that agentic requests return the `x-edgeoptimize-request-id` header as described in Step 6.

{{return-to-overview}}
