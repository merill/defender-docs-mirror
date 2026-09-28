---
layout: Conceptual
title: Set up your Amazon Web Services (AWS) environment to collect AWS logs to Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/connect-aws-configure-environment
breadcrumb_path: breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
description: Set up your Amazon Web Services environment to send AWS logs to Microsoft Sentinel using one of the Microsoft Sentinel AWS connectors.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: ac29da7b-31ac-6263-151e-2a98e027c412
document_version_independent_id: ed13df21-406d-3e2b-6674-b091e9a85359
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/connect-aws-configure-environment.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/connect-aws-configure-environment
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/connect-aws-configure-environment.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 10196697-f34c-f328-fcc2-2083ea340a63
---

# Set up your Amazon Web Services (AWS) environment to collect AWS logs to Microsoft Sentinel | Microsoft Learn

Amazon Web Services (AWS) connectors simplify the process of collecting logs from Amazon S3 (Simple Storage Service) and ingesting them into Microsoft Sentinel. The connectors provide tools to help you configure your AWS environment for Microsoft Sentinel log collection.

This article outlines the AWS environment setup required to send logs to Microsoft Sentinel and links to step-by-step instructions for setting up your environment and collecting AWS logs using each supported connector.

## AWS environment setup overview

This diagram shows how to set up your AWS environment to send logs to Microsoft Sentinel in Azure:

![Screenshot of A W S S 3 connector architecture.](media/connect-aws/s3-connector-architecture.png)

1. **Create an S3 (Simple Storage Service) storage bucket and a Simple Queue Service (SQS) queue** to which the S3 bucket publishes notifications when it receives new logs.

    Microsoft Sentinel connectors:

    - Poll the SQS queue, at frequent intervals, for messages, which contain the paths to new log files.
    - Fetch the files from the S3 bucket based on the path specified in the SQS notifications.
2. **Create an Open ID Connect (OIDC) web identity provider** and add Microsoft Sentinel as a registered application (by adding it as an audience).

    Microsoft Sentinel connectors use Microsoft Entra ID to authenticate with AWS through OpenID Connect (OIDC) and assume an AWS IAM role.

    Important

    If you already have an OIDC Connect provider set up for Microsoft Defender for Cloud, add Microsoft Sentinel as an audience to your existing provider (Commercial: `api://1462b192-27f7-4cb9-8523-0f4ecb54b47e`, Government:`api://d4230588-5f84-4281-a9c7-2c15194b28f7`). Don't try to create a new OIDC provider for Microsoft Sentinel.
3. **Create an AWS assumed role** to grant your Microsoft Sentinel connector permissions to access your AWS S3 bucket and SQS resources.

    1. Assign the appropriate **IAM permissions policies** to grant the assumed role access to the resources.
    2. Configure your connectors to use the assumed role and SQS queue you created to access the S3 bucket and retrieve logs.
4. **Configure AWS services to send logs to the S3 bucket**.

### Manual setup

Although you can set up the AWS environment manually by following the manual setup procedures in this section, we strongly recommend using the automated tools provided in the Deploy AWS connectors section instead. The Deploy AWS connectors section provides connector-specific setup instructions, automated configuration scripts, and links to each supported connector type.

#### 1. Create an S3 bucket and SQS queue

Create the S3 bucket and SQS queue required for log collection.

1. Create an **S3 bucket** to which you can send the logs from your AWS services - VPC, GuardDuty, CloudTrail, or CloudWatch.

    For details, see [Create an S3 storage bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/create-bucket-overview.html) in the AWS documentation.
2. Create a standard **Simple Queue Service (SQS) message queue** to which the S3 bucket can publish notifications.

    For details, see [Create a standard SQS queue](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/creating-sqs-standard-queues.html) in the AWS documentation.
3. Configure your S3 bucket to send notification messages to your SQS queue.

    For details, see [Enable S3 event notifications to an SQS queue](https://docs.aws.amazon.com/AmazonS3/latest/userguide/enable-event-notifications.html) in the AWS documentation.

#### 2. Create an Open ID Connect (OIDC) web identity provider

Important

If you already have an OIDC Connect provider set up for Microsoft Defender for Cloud, add Microsoft Sentinel as an audience to your existing provider (Commercial: `api://1462b192-27f7-4cb9-8523-0f4ecb54b47e`, Government:`api://d4230588-5f84-4281-a9c7-2c15194b28f7`). Don't try to create a new OIDC provider for Microsoft Sentinel.

Follow these instructions in the AWS documentation:[Creating OpenID Connect (OIDC) identity providers](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers_create_oidc.html).

| Parameter | Selection/Value | Comments |
| --- | --- | --- |
| **Client ID** | - | Ignore this, you already have it. See **Audience**. |
| **Provider type** | *OpenID Connect* | Instead of default *SAML*. |
| **Provider URL** | Commercial:`sts.windows.net/33e01921-4d64-4f8c-a055-5bdaffd5e33d/`Government:`sts.windows.net/cab8a31a-1906-4287-a0d8-4eef66b95f6e/` |  |
| **Thumbprint** | `626d44e704d1ceabe3bf0d53397464ac8080142c` | If created in the IAM console, selecting **Get thumbprint** should give you this result. |
| **Audience** | Commercial:`api://1462b192-27f7-4cb9-8523-0f4ecb54b47e`Government:`api://d4230588-5f84-4281-a9c7-2c15194b28f7` |  |

#### 3. Create an AWS assumed role

Create an AWS assumed role for the OIDC identity provider you configured in Create an Open ID Connect (OIDC) web identity provider. When you name the role, the role name must start with `OIDC_`.

Important

The role name must include the exact prefix `OIDC_`; otherwise, the connector can't function properly.

1. Follow these instructions in the AWS documentation:[Creating a role for web identity or OpenID Connect Federation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-idp_oidc.html#idp_oidc_Create).

    | Parameter | Selection/Value | Comments |
    | --- | --- | --- |
    | **Trusted entity type** | *Web identity* | Instead of default *AWS service*. |
    | **Identity provider** | Commercial:`sts.windows.net/33e01921-4d64-4f8c-a055-5bdaffd5e33d/`Government:`sts.windows.net/cab8a31a-1906-4287-a0d8-4eef66b95f6e/` | The provider you created in the previous step. |
    | **Audience** | Commercial:`api://1462b192-27f7-4cb9-8523-0f4ecb54b47e`Government:`api://d4230588-5f84-4281-a9c7-2c15194b28f7` | The audience you defined for the identity provider in the previous step. |
    | **Permissions to assign** | - `AmazonSQSReadOnlyAccess`<br>    - `AWSLambdaSQSQueueExecutionRole`<br>    - `AmazonS3ReadOnlyAccess`<br>    - `ROSAKMSProviderPolicy`<br>    - Other policies for ingesting the different types of AWS service logs | For information on these policies, see the [AWS Commercial S3 connector permissions policies page](https://github.com/Azure/Azure-Sentinel/blob/master/DataConnectors/AWS-S3/AwsRequiredPolicies.md) or the [AWS Government S3 connector permissions policies page](https://github.com/Azure/Azure-Sentinel/blob/master/DataConnectors/AWS-S3/AwsRequiredPoliciesForGov.md) in the Microsoft Sentinel GitHub repository. |
    | **Name** | "OIDC\_*MicrosoftSentinelRole*" | Choose a meaningful name that includes a reference to Microsoft Sentinel.The name must include the exact prefix `OIDC_`; otherwise, the connector can't function properly. |
2. Edit the new role's trust policy and add another condition:`"sts:RoleSessionName": "MicrosoftSentinel_{WORKSPACE_ID)"`

    Important

    The value of the `sts:RoleSessionName` parameter must have the exact prefix `MicrosoftSentinel_`; otherwise the connector doesn't function properly.

    The finished trust policy should look like this:

    ```json
    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Effect": "Allow",
          "Principal": {
            "Federated": "arn:aws:iam::XXXXXXXXXXXX:oidc-provider/sts.windows.net/cab8a31a-1906-4287-a0d8-4eef66b95f6e/"
          },
          "Action": "sts:AssumeRoleWithWebIdentity",
          "Condition": {
            "StringEquals": {
              "sts.windows.net/cab8a31a-1906-4287-a0d8-4eef66b95f6e/:aud": "api://d4230588-5f84-4281-a9c7-2c15194b28f7",
              "sts:RoleSessionName": "MicrosoftSentinel_XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
            }
          }
        }
      ]
    }
    ```

    - `XXXXXXXXXXXX` is your AWS Account ID.
    - `XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX` is your Microsoft Sentinel workspace ID.

    Update (save) the policy when you're done editing.

#### Configure AWS services to export logs to an S3 bucket

See the linked Amazon Web Services documentation for instructions for sending each type of log to your S3 bucket:

- [Publish a VPC flow log to an S3 bucket](https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs-s3.html).

    Note

    If you choose to customize the log's format, you must include the *start* attribute, as it maps to the *TimeGenerated* field in the Log Analytics workspace. Otherwise, the *TimeGenerated* field is populated with the event's *ingested time*, which doesn't accurately describe the log event.
- Configure GuardDuty to export findings to your S3 bucket so Microsoft Sentinel can ingest them. For details, see [Export your GuardDuty findings to an S3 bucket](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_exportfindings.html).

    Note

    - In AWS, findings are exported by default every 6 hours. Adjust the export frequency for updated Active findings based on your environment requirements. To expedite the process, you can modify the default setting to export findings every 15 minutes. See [Setting the frequency for exporting updated active findings](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_exportfindings.html#guardduty_exportfindings-frequency).
    - The *TimeGenerated* field is populated with the finding's *Update at* value.
- AWS CloudTrail trails are stored in S3 buckets by default.

    - [Create a trail for a single account](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-create-a-trail-using-the-console-first-time.html).
    - [Create a trail spanning multiple accounts across an organization](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/creating-trail-organization.html).
- [Export your CloudWatch log data to an S3 bucket](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/S3Export.html).

## 4. Deploy AWS connectors

Microsoft Sentinel provides these AWS connectors:

- [Amazon Web Services Web Application Firewall (WAF) connector](connect-aws-s3-waf): Ingests AWS WAF logs, collected in AWS S3 buckets, to Microsoft Sentinel.
- [Amazon Web Services service log connector](connect-aws): Ingests AWS service logs, collected in AWS S3 buckets, to Microsoft Sentinel.
- [Amazon Web Services Elastic Kubernetes Service (EKS) log connector](connect-aws-eks): Ingests AWS EKS audit logs, collected in AWS S3 buckets, to Microsoft Sentinel.