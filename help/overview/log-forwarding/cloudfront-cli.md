---
title: Log Forwarding - CloudFront (AWS CLI)
description: Forward CloudFront CDN logs to Adobe's S3 bucket using the AWS CLI for delivery setup and operations.
feature: Agentic Traffic
---

# Log Forwarding: CloudFront (AWS CLI) {#log-forwarding-cloudfront-cli}

This page details how to forward CDN logs from CloudFront to Adobe’s S3 bucket for agentic traffic data collection. You will use the LLM Optimizer CDN configuration page to onboard to LLM Optimizer. After the onboarding process is complete, follow the steps provided on this page to configure log forwarding by using the [AWS Command Line Interface](https://aws.amazon.com/cli/) in [Step 2](#step-2-cli).

>[!NOTE]
>
> This guide explains how to configure log forwarding by using the [AWS Command Line Interface](https://aws.amazon.com/cli/). If you want to configure log forwarding by using the **CloudFront UI**, see [Log Forwarding: CloudFront](/help/overview/log-forwarding/cloudfront.md).

## Step 1: Onboard in LLM Optimizer {#step-1}

On the LLM Optimizer page [https://llmo.now/](https://llmo.now/):

1. Go to the **Customer Configuration Dashboard**.

   ![Configuration button](/help/overview/assets/log-forwarding/common/config-button.png)

1. Click the **CDN Configuration** tab.

   ![CDN Configuration tab](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

1. Click **Get Started**.

   <!-- ![Onboard CDN button](/help/overview/assets/log-forwarding/common/onboard-cdn-button.png)-->

1. Next to **Activate AI Traffic Insights**, click **Configure**.

   ![Configure](/help/overview/assets/log-forwarding/common/configure.png)

1. Enter your **AWS Account** ID.

 <!--  ![AWS Account ID](/help/overview/assets/log-forwarding/cloudfront/cloudfront-aws-account.png)-->

1. Select **CloudFront (BYOCDN)**.

   ![Select CloudFront](/help/overview/assets/log-forwarding/cloudfront/cloudfront-select.png)

1. Click **Onboard**.

  <!-- ![Onboard button](/help/overview/assets/log-forwarding/common/onboard-button.png)-->

## Step 2: Set up CDN log forwarding with AWS CLI {#step-2-cli}

Setup CDN log forwarding with AWS CLI as follows:

### Configure AWS CLI credentials

Setup AWS CLI credential MAC. Open ~/.aws/credentials and enter the values for the variables below:

```text
[LLMO]
aws_access_key_id=<VALUE_OF_ACCESS_KEY_ID>
aws_secret_access_key=<VALUE_OF_SECRET_KEY>
aws_session_token=<ONLY_IF_USING_SECURITY_TOKEN_SERVICE> ## Optional
```

### Test the connection

Run the command below to test connection:

```bash
aws sts get-caller-identity --profile LLMO
```

Example of successful output:

```bash
aws sts get-caller-identity --profile LLMO
{
    "UserId": "AxxxxxxxxxxxP:user",
    "Account": "012345678912",
    "Arn": "arn:aws:sts::012345678912:assumed-role/klam-master-role-BatlY3dnPVinQLC/user"
}
```

### Initialize variables

Replace `REPLACEME123@AdobeOrg` with your organization Adobe IMS Org ID and run the command below. The output ID of this command will be referred to as `TRANSFORM_IMS_ID`.

```bash
echo "REPLACEME123@AdobeOrg" | sed 's/@AdobeOrg$//' | tr '[:upper:]' '[:lower:]'
```

Enter the values for `CUSTOMER`, `CDN_ID`, `ACCT1`, and `TRANSFORM_IMS_ID` following the guideline below and then run commands from your terminal.

```bash
export PROFILE1=LLMO
export REGION1=us-east-1
export CUSTOMER=<CUSTOMER_NAME> ## No Space, user letters,numbers and dash
export CDN_ID=<YOUR_CLOUDFRONT_DISTRIBUTION_ID>
export ACCT1=<YOUR_AWS_ACCOUNT_NUMBER>
export DELIVERY_DEST_ARN=arn:aws:logs:us-east-1:640168421876:delivery-destination:cdn-logs-<TRANSFORM_IMS_ID>-ams  ## Replace TRANSFORM_IMS_ID with the output of the command above 
```

<!--Use the **Delivery destination ARN** and org values from the LLM Optimizer CDN configuration page if they differ from the pattern above.-->

### Create the delivery source

From the same terminal in which step 3 was executed, run the command below:

```bash
aws logs put-delivery-source --name llmo-cf-${CUSTOMER}-${CDN_ID} \
  --profile $PROFILE1 --region $REGION1 \
  --resource-arn arn:aws:cloudfront::${ACCT1}:distribution/${CDN_ID} \
  --log-type ACCESS_LOGS
```

>[!IMPORTANT]
>
>If you get the following error, search for the existing delivery source: *An error occurred (ConflictException) when calling the PutDeliverySource operation: This ResourceId has already been used in another Delivery Source in this account.*
>
>To search for the existing delivery source, run this command:
>
>```bash
>aws logs describe-delivery-sources --region us-east-1 \
>--query "deliverySources[?contains(resourceArns[0], '<CDN DistributionID>')]"
>```
>
>In the next command, use the delivery source name from the results of the above command.

### Create the delivery configuration

```bash
aws logs create-delivery \
  --profile "$PROFILE1" --region "$REGION1" \
  --delivery-source-name "llmo-cf-${CUSTOMER}-${CDN_ID}" \
  --delivery-destination-arn $DELIVERY_DEST_ARN \
  --s3-delivery-configuration '{"suffixPath":"/{yyyy}/{MM}/{dd}/{HH}"}' \
  --record-fields 'date' 'time' 'x-edge-location' 'cs-method' 'cs(Host)' 'cs-uri-stem' 'sc-status' 'cs(Referer)' 'cs(User-Agent)' 'time-to-first-byte' 'sc-content-type' 'x-host-header'
```

<!--Align `--record-fields` and `--s3-delivery-configuration` with the field list and path suffix shown on your LLM Optimizer CDN configuration page if documentation or product values change.-->
