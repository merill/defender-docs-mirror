---
layout: Conceptual
title: Protect your Amazon Web Services environment - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/protect-aws
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: Learn how to connect your Amazon Web Services (AWS) environment to Microsoft Defender for Cloud Apps using the API connector to monitor activities and detect threats.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: AmitMishaeli
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 130de9b6-57bc-f828-ded7-a22e66c7e851
document_version_independent_id: 130de9b6-57bc-f828-ded7-a22e66c7e851
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/protect-aws.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: protect-aws
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/protect-aws.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: c57d6435-93e4-62a1-103d-3bdfe288c6cc
---

# Protect your Amazon Web Services environment - Microsoft Defender for Cloud Apps | Microsoft Learn

Amazon Web Services (AWS) is an IaaS provider that lets your organization host and manage workloads in the cloud. While cloud infrastructure offers many benefits, it can also expose critical assets to threats. These assets include storage instances with sensitive data, compute resources that run key applications, ports, and virtual private networks.

Connect AWS to Defender for Cloud Apps to secure your assets and detect threats. The connector monitors admin and sign-in activity. It notifies you about brute force attacks, misuse of privileged accounts, unusual VM deletions, and publicly exposed storage buckets.

## Main threats

Connecting AWS to Defender for Cloud Apps helps you detect and respond to the following threats:

- Abuse of cloud resources
- Compromised accounts and insider threats
- Data leakage
- Resource misconfiguration and insufficient access control

## Protect your environment with Defender for Cloud Apps

Defender for Cloud Apps protects your AWS environment by helping you:

- [Detect cloud threats, compromised accounts, and malicious insiders](best-practices#detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware)
- [Limit exposure of shared data and enforce collaboration policies](best-practices#limit-exposure-of-shared-data-and-enforce-collaboration-policies)
- [Use the audit trail of activities for forensic investigations](best-practices#use-the-audit-trail-of-activities-for-forensic-investigations)

## Control AWS with built-in policies and policy templates

You can use the following built-in policy templates to detect and notify you about potential threats:

Important

File policies retire on January 6, 2027. To maintain file-based data protection for this app, [migrate to Microsoft Purview DLP or auto-labeling policies](migrate-file-policies-to-purview).

| Type | Name |
| --- | --- |
| Activity policy template | Admin console sign-in failuresEC2 instance configuration changesIAM policy changesLogon from a risky IP addressNetwork access control list (ACL) changesNetwork gateway changesS3 Bucket ActivitySecurity group configuration changesVirtual private network changes |
| Built-in anomaly detection policy | [Activity from anonymous IP addresses](anomaly-detection-policy#activity-from-anonymous-ip-addresses)[Activity from infrequent country](anomaly-detection-policy#activity-from-infrequent-country)[Activity from suspicious IP addresses](anomaly-detection-policy#activity-from-suspicious-ip-addresses)[Impossible travel](anomaly-detection-policy#impossible-travel)[Activity performed by terminated user](anomaly-detection-policy#activity-performed-by-terminated-user) (requires Microsoft Entra ID as IdP)[Multiple failed login attempts](anomaly-detection-policy#multiple-failed-login-attempts)[Unusual administrative activities](anomaly-detection-policy#unusual-activities-by-user) |
| File policy template | S3 bucket is publicly accessible |

For more information about creating policies, see [Create a policy](control-cloud-apps-with-policies#create-a-policy).

## Automate governance controls

You can also apply and automate AWS governance actions to fix detected threats:

| Type | Action |
| --- | --- |
| User governance | - Notify user on alert (via Microsoft Entra ID)- Require user to sign in again (via Microsoft Entra ID)- Suspend user (via Microsoft Entra ID) |
| Data governance | - Make an S3 bucket private- Remove a collaborator for an S3 bucket |

For more information about remediating threats from apps, see [Governing connected apps](governance-actions).

## Protect AWS in real time

Review our best practices for [blocking and protecting the download of sensitive data to unmanaged or risky devices](best-practices#block-and-protect-download-of-sensitive-data-to-unmanaged-or-risky-devices).

## Connect Amazon Web Services to Microsoft Defender for Cloud Apps

Defender for Cloud Apps provides connector APIs that integrate with supported cloud services to ingest activity data. Use these APIs to connect your existing Amazon Web Services (AWS) account to Defender for Cloud Apps. For information about how Defender for Cloud Apps protects AWS, see [Protect AWS](protect-aws).

You can connect AWS **Security auditing** to Defender for Cloud Apps connections to gain visibility into and control over AWS app use.

### Step 1: Configure Amazon Web Services auditing

To configure AWS auditing for Defender for Cloud Apps, perform the following steps:

1. Sign in to the [Amazon Web Services console](https://aws.amazon.com/console/)
2. Add a new user for Defender for Cloud Apps, and give the user **Programmatic access**.
3. Select **Create policy** and enter a name for your new policy.
4. Select the **JSON** tab and paste the following script:

    ```json
    {
      "Version" : "2012-10-17",
      "Statement" : [{
          "Action" : [
            "cloudtrail:DescribeTrails",
            "cloudtrail:LookupEvents",
            "cloudtrail:GetTrailStatus",
            "cloudwatch:Describe*",
            "cloudwatch:Get*",
            "cloudwatch:List*",
            "iam:List*",
            "iam:Get*",
            "s3:ListAllMyBuckets",
            "s3:PutBucketAcl",
            "s3:GetBucketAcl",
            "s3:GetBucketLocation"
          ],
          "Effect" : "Allow",
          "Resource" : "*"
        }
      ]
     }
    ```
5. Select **Download .csv** to save a copy of the new user's credentials. You'll need these credentials later.

    Note

    After connecting AWS, you'll receive events for seven days prior to connection. If you just enabled CloudTrail, you receive events from the time you enabled CloudTrail.

### Step 2: Connect Amazon Web Services auditing to Defender for Cloud Apps

To connect AWS auditing to Defender for Cloud Apps, complete the following steps:

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**.
2. In the **App connectors** page, to provide the AWS connector credentials, do one of the following:

**For a new connector**

1. Select the **+Connect an app**, followed by **Amazon Web Services**.

    [![Screenshot that shows where to find the +Connect an app button in the Microsoft Defender portal.](media/connect-aws.png)](media/connect-aws.png#lightbox)
2. In the next window, provide a name for the connector, and then select **Next**.

    [![Screenshot that shows how to add the instance name for your new AWS connector. ](media/connect-aws-name.png)](media/connect-aws-name.png#lightbox)
3. On the **Connect Amazon Web Services** page, select **Security auditing**, and then select **Next**.
4. On the **Security auditing page**, paste the **Access key** and **Secret key** from the .csv file into the relevant fields, and select **Next**.

    [![Screenshot that shows the AWS app security auditing page and where to enter the access key and secret key.](media/aws-connect-app-audit.png)](media/aws-connect-app-audit.png#lightbox)

**For an existing connector**

1. In the list of connectors, on the row in which the AWS connector appears, select **Edit settings**.
2. On the **Instance name** and **Connect Amazon Web Services** pages, select **Next**. On the **Security auditing page**, paste the **Access key** and **Secret key** from the .csv file into the relevant fields, and select **Next**.

    [![Screenshot that shows the AWS app security auditing page and where to enter the access key and secret key.](media/aws-connect-app-audit.png)](media/aws-connect-app-audit.png#lightbox)
3. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**. Make sure the status of the connected App Connector is **Connected**.