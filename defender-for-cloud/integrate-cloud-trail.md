---
layout: Conceptual
title: Integrate AWS CloudTrail Logs - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/integrate-cloud-trail
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
description: AWS CloudTrail logs give Defender for Cloud visibility into permission changes and control-plane activity. Learn to enable and verify ingestion.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: d7c664df-9ca6-5cc8-e2d5-9d0b7c0a0348
document_version_independent_id: 6c2f4fe6-5341-0551-b760-7b32ee08ff50
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/integrate-cloud-trail.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/integrate-cloud-trail
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/integrate-cloud-trail.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 40a2280f-3989-0992-c85e-2a4b66eb0df5
---

# Integrate AWS CloudTrail Logs - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud can collect Amazon Web Services (AWS) CloudTrail management events to increase visibility into identity operations, permission changes, and other control-plane activity in your AWS environments.

CloudTrail ingestion adds activity-based signals to Defender for Cloud's Cloud Infrastructure Entitlement Management (CIEM) capabilities, allowing identity and permission risk analysis to be based not only on configured identity entitlements, but also on observed usage.

CloudTrail ingestion enhances CIEM by helping identify unused permissions, misconfigured roles, dormant identities, and potential privilege escalation paths. It also provides activity context that strengthens configuration drift detection, security recommendations, and attack path analysis.

CloudTrail ingestion is available for single AWS accounts and AWS Organizations that use centralized logging.

## Prerequisites

Before you enable CloudTrail ingestion, ensure that your AWS account has:

- Microsoft Defender Cloud Security Posture Management plan enabled on the Azure subscription. See [Enable the Defender CSPM plan](tutorial-enable-cspm-plan).
- Permission to access AWS CloudTrail.
- Access to the Amazon S3 bucket that stores CloudTrail log files.
- Access to the Amazon SQS queue notifications associated with that bucket.
- Access to AWS KMS keys if CloudTrail logs are encrypted. See [Encrypting CloudTrail log files with AWS KMS](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/encrypting-cloudtrail-log-files-with-aws-kms.html).
- Permissions to create or modify CloudTrail trails and required resources if provisioning a new trail.
- CloudTrail configured to log management events. See [Logging management events with CloudTrail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/logging-management-events-with-cloudtrail.html).

Note

**Microsoft Sentinel users**: If you already stream AWS CloudTrail logs to Microsoft Sentinel, enabling CloudTrail ingestion in Defender for Cloud might require updates to your Sentinel configuration. For more information, see [Connect a Sentinel connected AWS account to Defender for Cloud](sentinel-connected-aws).

## Configure CloudTrail ingestion

To enable CloudTrail ingestion for your AWS connector, follow these steps:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select the AWS connector you want to configure.
4. Under **Monitoring coverage**, open **Settings**.
5. Turn on **AWS CloudTrail ingestion (Preview)**. This setting adds CloudTrail configuration options to the setup workflow.

    [![Screenshot showing the Defender for Cloud plan selection page for an AWS connector.](media/integrate-cloud-trail/defender-plans-selection.png)](media/integrate-cloud-trail/defender-plans-selection.png#lightbox)
6. Choose whether to integrate with an existing CloudTrail trail or create a new one:

    - Select **Manually provide trail details** to use an existing CloudTrail trail.

        1. Enter the Amazon S3 bucket ARN and SQS queue ARN associated with the existing trail.
        2. If prompted, deploy or update the CloudFormation stack provided by Defender for Cloud.

        Note

        When you select an existing trail, Defender for Cloud performs a one-time collection of up to 90 days of historical CloudTrail management events. If you disable CloudTrail ingestion, the historical data collected during the one-time historical data collection is removed. Re-enabling CloudTrail ingestion triggers a new historical data collection.
    - Select **Create a new AWS CloudTrail** to provision a new trail.

        1. Deploy the CloudFormation or Terraform template provided by Defender for Cloud when prompted.
        2. After the deployment completes, locate the SQS queue ARN in the AWS console.
        3. Return to Defender for Cloud and enter the SQS ARN in the **SQS ARN** field.

        [![Screenshot showing the AWS CloudTrail ingestion settings for an AWS connector in Defender for Cloud.](media/integrate-cloud-trail/ingestion-settings.png)](media/integrate-cloud-trail/ingestion-settings.png#lightbox)

## How Defender for Cloud uses CloudTrail data

After you complete the configuration:

- AWS CloudTrail records management events from your AWS account.
- Log files are written to an Amazon S3 bucket.
- Amazon SQS sends notifications when new logs are available.
- Defender for Cloud polls the SQS queue to retrieve the log file references.
- Defender for Cloud processes log telemetry and enriches CIEM and posture insights.

You can customize CloudTrail event selectors to change which management events are captured.

## Validate CloudTrail ingestion

To confirm CloudTrail telemetry is flowing into Defender for Cloud:

- Verify that the S3 bucket grants Defender for Cloud permission to read log files.
- Ensure SQS notifications are configured for new log deliveries.
- Confirm IAM roles allow access to CloudTrail artifacts and encrypted objects.
- Review Defender for Cloud recommendations and identity insights after setup.

Signals can take time to appear depending on CloudTrail delivery frequency and event volume.