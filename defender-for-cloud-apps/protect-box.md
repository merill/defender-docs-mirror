---
layout: Conceptual
title: Protect your Box environment - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/protect-box
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
description: Learn how to connect Box to Microsoft Defender for Cloud Apps using the API connector for activity visibility, threat detection, and remediation controls.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: AmitMishaeli
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 4f9776ca-b5bb-0b01-2e49-7a0949550ee3
document_version_independent_id: 4f9776ca-b5bb-0b01-2e49-7a0949550ee3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/protect-box.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: protect-box
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/protect-box.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: c2b77dbb-4b2a-f93d-dcf7-6760f5ce86fd
---

# Protect your Box environment - Microsoft Defender for Cloud Apps | Microsoft Learn

Box is a cloud storage and collaboration tool that lets your users share documents across your organization and with partners. However, using Box might expose sensitive data to external collaborators or make it publicly available via a shared link. These incidents can be caused by malicious actors or by unaware employees.

When you connect Box to Defender for Cloud Apps, you get better insights into your users' activities. The connection provides threat detection through machine learning, helps detect external information sharing, and enables automated remediation controls.

## Main threats

The main threats to consider in a Box environment include:

- Compromised accounts and insider threats
- Data leakage
- Insufficient security awareness
- Malware
- Ransomware
- Unmanaged bring your own device (BYOD)

## Ways Defender for Cloud Apps protects your environment

Defender for Cloud Apps protects your Box environment by helping you:

- [Detect cloud threats, compromised accounts, and malicious insiders](best-practices#detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware)
- [Discover, classify, label, and protect regulated and sensitive data stored in the cloud](best-practices#discover-classify-label-and-protect-regulated-and-sensitive-data-stored-in-the-cloud)
- [Enforce DLP and compliance policies for data stored in the cloud](best-practices#enforce-dlp-and-compliance-policies-for-data-stored-in-the-cloud)
- [Limit exposure of shared data and enforce collaboration policies](best-practices#limit-exposure-of-shared-data-and-enforce-collaboration-policies)
- [Use the audit trail of activities for forensic investigations](best-practices#use-the-audit-trail-of-activities-for-forensic-investigations)

## Control Box with built-in policies and policy templates

You can use the following built-in policy templates to detect and notify you about potential threats:

Important

File policies retire on January 6, 2027. To maintain file-based data protection for this app, [migrate to Microsoft Purview DLP or auto-labeling policies](migrate-file-policies-to-purview).

| Type | Name |
| --- | --- |
| Built-in anomaly detection policy | [Activity from anonymous IP addresses](anomaly-detection-policy#activity-from-anonymous-ip-addresses)[Activity from infrequent country](anomaly-detection-policy#activity-from-infrequent-country)[Activity from suspicious IP addresses](anomaly-detection-policy#activity-from-suspicious-ip-addresses)[Impossible travel](anomaly-detection-policy#impossible-travel)[Activity performed by terminated user](anomaly-detection-policy#activity-performed-by-terminated-user) (requires Microsoft Entra ID as IdP)[Malware detection](anomaly-detection-policy#malware-detection)[Multiple failed login attempts](anomaly-detection-policy#multiple-failed-login-attempts)[Ransomware detection](anomaly-detection-policy#ransomware-activity)[Unusual administrative activities](anomaly-detection-policy#unusual-activities-by-user)[Unusual file deletion activities](anomaly-detection-policy#unusual-activities-by-user)[Unusual file share activities](anomaly-detection-policy#unusual-activities-by-user)[Unusual multiple file download activities](anomaly-detection-policy#unusual-activities-by-user) |
| Activity policy template | Logon from a risky IP addressMass download by a single userPotential ransomware activity |
| File policy template | Detect a file shared with an unauthorized domainDetect a file shared with personal email addressesDetect files with PII/PCI/PHI |

For more information about creating policies, see [Create a policy](control-cloud-apps-with-policies#create-a-policy).

## Automate governance controls

In addition to monitoring for potential threats, you can apply and automate the following Box governance actions to remediate detected threats:

| Type | Action |
| --- | --- |
| Data governance | - Change shared link access level on folders- Put folders in admin quarantine- Put folders in user quarantine- Remove a collaborator from folders- Remove direct shared links on folders - Send policy-match digest to file owners- Send violation digest to last file editor- Set expiration date to a folder shared link - Trash folder |
| User governance | - Suspend user- Notify user on alert (via Microsoft Entra ID)- Require user to sign in again (via Microsoft Entra ID)- Suspend user (via Microsoft Entra ID) |

For more information about remediating threats from apps, see [Governing connected apps](governance-actions).

## Protect Box in real time

Review our best practices for [securing and collaborating with external users](best-practices#secure-collaboration-with-external-users-by-enforcing-real-time-session-controls) and [blocking and protecting the download of sensitive data to unmanaged or risky devices](best-practices#block-and-protect-download-of-sensitive-data-to-unmanaged-or-risky-devices).

## Connect Box to Microsoft Defender for Cloud Apps

You can connect Microsoft Defender for Cloud Apps to your existing Box account using the App Connector APIs, which are the API-based integration method that Defender for Cloud Apps uses to connect to supported SaaS apps. The connection gives you visibility into and control over Box use. For information about how Defender for Cloud Apps protects Box, see [Protect Box](protect-box).

Note

Deploying with an account that isn't an Admin account leads to a failure in the API test and doesn't allow Defender for Cloud Apps to scan all of the files in Box. If the inability to scan all files is a problem for you, you can deploy with a Co-Admin that has all of the privileges checked, but the API test will continue to fail and files owned by other admins in Box will not be scanned.

### Prerequisites

- A Box Admin account (or Co-Admin account with all privileges selected). Deploying with a non-Admin account causes the API test to fail and prevents Defender for Cloud Apps from scanning all files in Box.

### Configure Box

1. Sign into your Box account as an Admin user.
2. Go to the custom app settings. For more information, see [Managing custom apps – Box Support](https://support.box.com/hc/en-us/articles/360044196653-Managing-custom-apps#:%7E:text=Open%20your%20Admin%20Console.%20In%20the%20left%20sidebar%2C,you%20want%20to%20enforce%2C%20click%20the%20slider%20button.)
3. If your settings are configured to disable unpublished apps by default, enter the Defender for Cloud Apps API key for your data center, as listed in the following table, and save your changes.

| **Data center** | **Defender for Cloud Apps API key** |
| --- | --- |
| US1 | `nduj1o3yavu30dii7e03c3n7p49cj2qh` |
| US2 | `w0ouf1apiii9z8o0r6kpr4nu1pvyec75` |
| US3 | `dmcyvu1s9284i2u6gw9r2kb0hhve4a0r` |
| EU1 | `me9cm6n7kr4mfz135yt0ab9f5k4ze8qp` |
| EU2 | `uwdy5r40t7jprdlzo85v8suw1l4cdsbf` |

Your data center details are shown in the Defender for Cloud Apps **About** page in the **Settings** area. For more information, see [View your data center](network-requirements#view-your-data-center).

### Connect Box to Defender for Cloud Apps

After you configure Box, complete the following steps to connect your Box instance to Defender for Cloud Apps:

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**.
2. In the **App connectors** page, select **+Connect an app**, and then select **Box**.

    ![Screenshot of the App connectors page with Box available as a connector option.](media/connect-box.png)
3. In the **Instance name** page, enter a name for the connection. Then select **Next**.
4. In the **Follow the link** pop-up, select **Connect Box**.
5. The Box sign-in page opens. Enter your credentials to allow Defender for Cloud Apps access to your team's Box app.
6. Box asks you if you want to allow Defender for Cloud Apps access to your team information, activity log, and perform activities as a team member. To proceed, select **Allow**.
7. Back in the Microsoft Defender Portal, you should receive a message saying that Box was successfully connected.
8. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**. Make sure the status of the connected App Connector is **Connected**.

**After connecting Box**:

- You'll receive events for the 7 days prior to connection.
- Defender for Cloud Apps will perform a full scan of all files. Depending on how many files and users you have, completing the full scan can take a while.

To enable near real-time scanning, files on which activities are detected are moved to the beginning of the scan queue. For example, a file that is edited, updated, or shared is scanned right away rather than waiting for the regular scan process. Near real-time scanning doesn't apply to files that aren't inherently modified. For example, files that are viewed, previewed, printed, or exported are scanned as part of the regularly scheduled scan.