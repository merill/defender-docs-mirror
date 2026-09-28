---
layout: Conceptual
title: Connect a Microsoft Sentinel Connected AWS Account to Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/sentinel-connected-aws
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Configure CloudTrail ingestion for Defender for Cloud when your AWS account is already connected to Microsoft Sentinel.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 6ffbc217-3094-ca04-61be-a0bf6dd37722
document_version_independent_id: 4509644d-2ca5-0636-773c-e6d0e412da9b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/sentinel-connected-aws.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/sentinel-connected-aws
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/sentinel-connected-aws.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: bfacbccb-8d72-b4ec-7f0a-ac6c14f7f7ed
---

# Connect a Microsoft Sentinel Connected AWS Account to Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud generates a CloudFormation template that includes the resources required to onboard your Amazon Web Services (AWS) account. Microsoft Defender for Cloud and Microsoft Sentinel can both ingest AWS CloudTrail events. Use these procedures to enable CloudTrail ingestion for Defender for Cloud when your AWS account is already connected to Microsoft Sentinel.

By default, the Microsoft Sentinel connector receives CloudTrail notifications directly from Amazon S3 through an Amazon SQS queue. Because an Amazon SQS queue supports only one consumer, enabling CloudTrail ingestion for Defender for Cloud requires configuring an Amazon SNS fan-out pattern so both services can receive CloudTrail events in parallel.

## Prerequisites

To complete the procedures in this article, you need:

- A Microsoft Azure subscription. If you don't have an Azure subscription, you can [sign up for a free Azure account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- [Enable Microsoft Defender for Cloud on your Azure subscription](get-started#enable-defender-for-cloud-on-your-azure-subscription).
- Access to an AWS account.
- Contributor level permission for the relevant Azure subscription.
- **SNS fan-out method only:** AWS CloudTrail configured to deliver logs to an Amazon S3 bucket.
- **SNS fan-out method only:** An existing Microsoft Sentinel AWS connector that ingests CloudTrail logs from that bucket.

## Enable CloudTrail ingestion using SNS fan-out

If your AWS CloudTrail logs already stream to Microsoft Sentinel, you can enable CloudTrail ingestion for Defender for Cloud by using Amazon SNS as a fan-out mechanism. This configuration allows both services to receive CloudTrail events in parallel.

Important

These steps configure AWS resources for shared CloudTrail ingestion. To finalize Defender for Cloud setup, [integrate AWS CloudTrail logs with Microsoft Defender for Cloud](integrate-cloud-trail).

### Create an Amazon SNS topic for CloudTrail

Create an Amazon SNS topic to distribute CloudTrail event notifications to multiple subscribers.

1. In the AWS Management Console, open **Amazon SNS**.
2. Select **Create topic** and choose **Standard**.
3. Enter a descriptive name, such as *CloudTrail-SNS*, and select **Create topic**.
4. Copy the **Topic ARN** for later use.
5. On the topic details page, select **Edit**, and then expand **Access policy**.
6. Add a policy statement that allows the CloudTrail S3 bucket to publish events to the topic.

    Replace `<region>`, `<accountid>`, and `<S3_BUCKET_ARN>` with your values:

    ```json
    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Sid": "AllowS3ToPublish",
          "Effect": "Allow",
          "Principal": {
            "Service": "s3.amazonaws.com"
          },
          "Action": "SNS:Publish",
          "Resource": "arn:aws:sns:<region>:<accountid>:CloudTrail-SNS",
          "Condition": {
            "StringEquals": {
              "aws:SourceArn": "<S3_BUCKET_ARN>"
            }
          }
        }
      ]
    }
    ```

### Create an SQS queue for Defender for Cloud

Create a dedicated SQS queue that Defender for Cloud uses to receive CloudTrail event notifications from the SNS topic.

1. In **Amazon SQS**, select **Create queue** and choose **Standard**.
2. Enter a name, such as *DefenderForCloud-SQS*, and create the queue.
3. Update the SQS queue access policy to allow the SNS topic ARN to perform the `SQS:SendMessage` action for this queue.

    Apply this policy to each SQS queue that subscribes to the CloudTrail SNS topic. These queues typically include:

    - The SQS queue used by Microsoft Sentinel
    - The SQS queue created for Defender for Cloud

    To grant the SNS topic permission to send messages to the SQS queue, use the following policy statement. Replace `<region>`, `<accountid>`, and `<QUEUE_NAME>` with your values:

    ```json
    {
      "Sid": "AllowCloudTrailSnsToSendMessage",
      "Effect": "Allow",
      "Principal": {
        "Service": "sns.amazonaws.com"
      },
      "Action": "SQS:SendMessage",
      "Resource": "arn:aws:sqs:<region>:<accountid>:<QUEUE_NAME>",
      "Condition": {
        "ArnLike": {
          "aws:SourceArn": "arn:aws:sns:<region>:<accountid>:CloudTrail-SNS"
        }
      }
    }
    ```

### Subscribe both SQS queues to the SNS topic

1. In **Amazon SNS**, open the topic you created.
2. Create subscriptions to the SNS topic for both:

    - Your existing **Microsoft Sentinel SQS queue**
    - The new **Defender for Cloud SQS queue**

    [![Screenshot of the Amazon Simple Notification Service create subscription page showing Amazon Simple Queue Service selected as the protocol and raw message delivery enabled.](media/sentinel-connected-aws/amazon-simple-notification-service-create-subscription.png)](media/sentinel-connected-aws/amazon-simple-notification-service-create-subscription.png#lightbox)
3. When creating each subscription:

    - Select **Amazon SQS** as the protocol.
    - Paste the **Queue ARN**.
    - Enable **Raw message delivery**.

### Update the Microsoft Sentinel SQS queue access policy

If your AWS account is already connected to Microsoft Sentinel, you must also update the existing Sentinel SQS queue to allow the SNS topic to send messages.

1. In **Amazon SQS**, open the SQS queue used by Microsoft Sentinel.
2. Edit the **Access policy**.
3. Add the same `SQS:SendMessage` statement used for the Defender for Cloud queue, referencing the CloudTrail SNS topic ARN.
4. Save the policy.

If you skip this step, Microsoft Sentinel stops receiving CloudTrail notifications after you switch to the SNS fan-out configuration.

### Update S3 event notifications to publish CloudTrail logs to SNS

1. In **Amazon S3**, open your CloudTrail bucket and go to **Event notifications**.
2. Delete the existing S3 → SQS event notification used by Microsoft Sentinel.
3. Create a new event notification to publish to the SNS topic.
4. Set the event type to **Object created (PUT)**.
5. Configure a **prefix filter** so that only CloudTrail log files generate notifications.

    Use the full CloudTrail log path format:

    `AWSLogs/<AccountID>/CloudTrail/`
6. Save the configuration.

After these changes, both Microsoft Sentinel and Defender for Cloud receive CloudTrail event notifications using the SNS fan-out pattern.

[![Screenshot of the Amazon Simple Notification Service topic subscriptions list showing two Amazon Simple Queue Service subscriptions for Microsoft Sentinel and Defender for Cloud.](media/sentinel-connected-aws/amazon-simple-notification-service-topic-subscriptions.png)](media/sentinel-connected-aws/amazon-simple-notification-service-topic-subscriptions.png#lightbox)

## Resolve OIDC identity provider conflicts

1. Follow the steps in [Connect AWS accounts to Microsoft Defender for Cloud](quickstart-onboard-aws) until step 8 in the [Connect your AWS Account](quickstart-onboard-aws#connect-your-aws-account) section.
2. Select **Copy**.

    [![Screenshot that shows where the copy button is located.](media/sentinel-connected-aws/copy-template.png)](media/sentinel-connected-aws/copy-template.png#lightbox)
3. Paste the template into a local text editing tool.
4. Search for the **"ASCDefendersOIDCIdentityProvider": {** section of the template, and make a separate copy of the entire **ClientIdList**.
5. Search for the **ASCDefendersOIDCIdentityProvider** section in the template and delete it.
6. Save the file locally.
7. In a separate browser window, sign in to your AWS account.
8. Go to **Identity and Access Management (IAM)** &gt; **Identity Providers**.
9. Search for and select **33e01921-4d64-4f8c-a055-5bdaffd5e33d**.
10. Select **Actions** &gt; **Add audience**.
11. Paste the **ClientIdList** section you copied in step 4.
12. Go to the Configure access page in Defender for Cloud.
13. Follow the [Create a Stack in AWS](quickstart-onboard-aws#connect-your-aws-account) instructions, and use the template you saved locally.

    [![Screenshot that shows where the create stack instructions are located.](media/sentinel-connected-aws/create-stack.png)](media/sentinel-connected-aws/create-stack.png#lightbox)
14. Select **Next**.
15. Select **Create**.