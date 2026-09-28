---
layout: Conceptual
title: Enable data security posture management - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/data-security-posture-enable
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
description: Learn how to enable data security posture management in Microsoft Defender for Cloud, including prerequisites and setup guidance for Azure and AWS resources.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: template-how-to-pattern, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 2424120a-56a5-cafe-6be2-7c48cbd324ea
document_version_independent_id: 9ad5f984-3598-d602-7dbb-81ab64c607a3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/data-security-posture-enable.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/data-security-posture-enable
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/data-security-posture-enable.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 98eb85fa-3bee-76e0-f4c8-f34b3e3c8a8b
---

# Enable data security posture management - Microsoft Defender for Cloud | Microsoft Learn

This article explains how to enable data security posture management in Microsoft Defender for Cloud. Data security posture management helps you discover and classify sensitive data, identify risks, and prioritize remediation. Before you begin, review the prerequisites in this article.

## Before you start

Review the following prerequisites before you enable data security posture management:

- Before you enable data security posture management, [review support and prerequisites](concept-data-security-posture-prepare).
- When you enable Defender CSPM or Defender for Storage plans, the sensitive data discovery extension is automatically enabled. You can disable this setting if you don't want to use data security posture management, but we recommend that you use the feature to get the most value from Defender for Cloud.
- Sensitive data is identified based on the data sensitivity settings in Defender for Cloud. You can [customize the data sensitivity settings](data-sensitivity-settings) to identify the data that your organization considers sensitive.
- It takes up to 24 hours to see the results of a first discovery after enabling the feature.

## Enable in Defender CSPM (Azure)

Follow these steps to enable data security posture management. Don't forget to review [required permissions](concept-data-security-posture-prepare#whats-supported) before you start.

1. Navigate to **Microsoft Defender for Cloud** &gt; **Environment settings**.
2. Select the relevant Azure subscription.
3. For the Defender CSPM plan, select the **On** status.

    If Defender CSPM is already on, select **Settings** in the Monitoring coverage column of the Defender CSPM plan and make sure that the **Sensitive data discovery** component is set to **On** status.
4. Once sensitive data discovery is turned **On** in Defender CSPM, it will automatically incorporate support for additional resource types as the range of supported resource types expands.

## Enable in Defender CSPM (AWS)

Follow these steps to enable data security posture management for your AWS resources. Review the prerequisites and then configure scanning for your S3 buckets and RDS instances.

### Before you start in AWS

Complete the following checks before you enable data security posture management for Amazon Web Services (AWS):

- Don't forget to: [AWS discovery requirements](concept-data-security-posture-prepare#discovery), and [required permissions for S3 and RDS scanning](concept-data-security-posture-prepare#whats-supported).
- Check that there's no policy that blocks the connection to your Amazon S3 buckets.
- For Amazon Relational Database Service (RDS) instances, cross-account AWS Key Management Service (KMS) encryption is supported, but additional KMS access policies might prevent access.

### Enable for AWS resources

After you complete the prerequisites, configure scanning for your AWS resources.

#### Configure S3 buckets and RDS instances

To enable scanning for S3 buckets and RDS instances:

1. In Defender for Cloud, go to **Environment settings** and select your AWS connector.
2. Turn on Defender CSPM with **Sensitive data discovery**.
3. Proceed with the instructions to download the CloudFormation template and to run it in AWS.

Automatic discovery of S3 buckets in the AWS account starts automatically.

For S3 buckets, the Defender for Cloud scanner runs in your AWS account and connects to your S3 buckets.

For RDS instances, discovery will be triggered once **Sensitive Data Discovery** is turned on. The scanner will take the latest automated snapshot for an instance, create a manual snapshot within the source account, and copy it to an isolated Microsoft-owned environment within the same region.

The snapshot is used to create a live instance that is spun up, scanned and then immediately destroyed (together with the copied snapshot).

Only scan findings are reported by the scanning platform.

[![Diagram explaining the RDS scanning platform.](media/data-security-posture-enable/rds-scanning-platform.png)](media/data-security-posture-enable/rds-scanning-platform.png#lightbox)

### Check for S3 blocking policies

If enabling scanning for S3 buckets and RDS instances didn't work because of a blocked policy, check the following:

- Make sure that the S3 bucket policy doesn't block the connection. In the AWS S3 bucket, select the **Permissions** tab &gt; Bucket policy. Check the policy details to make sure the Microsoft Defender for Cloud scanner service running in the Microsoft account in AWS isn't blocked.
- Make sure that there's no SCP policy that blocks the connection to the S3 bucket. For example, your SCP policy might block read API calls to the AWS Region where your S3 bucket is hosted.
- Check that these required API calls are allowed by your SCP policy: AssumeRole, GetBucketLocation, GetObject, ListBucket, GetBucketPublicAccessBlock
- Check that your SCP policy allows calls to the us-east-1 AWS Region, which is the default region for API calls.

## Enable data-aware monitoring in Defender for Storage

Sensitive data threat detection is enabled by default when the sensitive data discovery component is enabled in the Defender for Storage plan. For details, see [Sensitive data threat detection in Defender for Storage](defender-for-storage-data-sensitivity).

Note

If you turn off Defender CSPM, only Azure Storage resources are scanned.