---
layout: Conceptual
title: Protect your Cisco Webex environment - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/protect-webex
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
description: Connect Cisco Webex to Microsoft Defender for Cloud Apps by using the API connector to gain activity visibility, information protection detections, and automated governance controls.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: AmitMishaeli
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: d5005b15-a221-aa72-087c-58c9b382715d
document_version_independent_id: d5005b15-a221-aa72-087c-58c9b382715d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/protect-webex.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: protect-webex
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/protect-webex.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: ccf05d10-ef0c-dd00-bfcd-e8e7c20dbe99
---

# Protect your Cisco Webex environment - Microsoft Defender for Cloud Apps | Microsoft Learn

As a communication and collaboration platform, Cisco Webex enables streamlined communication and collaboration across your organization. Using Cisco Webex for your data and assets exchange may expose your sensitive organizational information to external users, for example, in chat rooms where they may also be participating in a conversation with your employees.

Connecting Cisco Webex to Defender for Cloud Apps gives you improved insights into your users' activities, provides information protection detections, and enables automated governance controls.

## Main threats

Cisco Webex usage can expose your organization to the following threats:

- Compromised accounts and insider threats
- Data leakage
- Insufficient security awareness
- Ransomware
- Unmanaged bring your own device (BYOD)

## How Defender for Cloud Apps helps to protect your environment

Defender for Cloud Apps helps protect your Cisco Webex environment with the following best practices:

- [Enforce DLP and compliance policies for data stored in the cloud](best-practices#enforce-dlp-and-compliance-policies-for-data-stored-in-the-cloud)
- [Limit exposure of shared data and enforce collaboration policies](best-practices#limit-exposure-of-shared-data-and-enforce-collaboration-policies)
- [Use the audit trail of activities for forensic investigations](best-practices#use-the-audit-trail-of-activities-for-forensic-investigations)

## Control Cisco Webex with built-in policies and policy templates

You can use the following built-in policy templates to detect and notify you about potential threats:

Important

File policies retire on January 6, 2027. To maintain file-based data protection for this app, [migrate to Microsoft Purview DLP or auto-labeling policies](migrate-file-policies-to-purview).

| Type | Name |
| --- | --- |
| Built-in anomaly detection policy | [Activity performed by terminated user](anomaly-detection-policy#activity-performed-by-terminated-user) (requires Microsoft Entra ID as the identity provider (IdP))[Ransomware detection](anomaly-detection-policy#ransomware-activity)[Unusual file deletion activities](anomaly-detection-policy#unusual-activities-by-user)[Unusual file share activities](anomaly-detection-policy#unusual-activities-by-user)[Unusual multiple file download activities](anomaly-detection-policy#unusual-activities-by-user) |
| File policy template | Detect a file shared with an unauthorized domainDetect a file shared with personal email addresses |
| Activity policy template | Mass download by a single userPotential ransomware activity |

Note

After connecting Cisco Webex, and when using Webex Meetings, attachments are ingested to Defender for Cloud Apps only when they're shared in chats. Attachments shared in meetings aren't ingested.

For more information about creating policies, see [Create a policy in Defender for Cloud Apps](control-cloud-apps-with-policies#create-a-policy).

## Automate governance controls

In addition to monitoring for potential threats, you can apply and automate the following Cisco Webex governance actions to remediate detected threats:

| Type | Action |
| --- | --- |
| User governance | - Notify user on alert (via Microsoft Entra ID)- Require user to sign in again (via Microsoft Entra ID)- Suspend user (via Microsoft Entra ID) |
| Data governance | - Trash file |

For more information about remediating threats from apps, see [Governance actions for connected apps](governance-actions).

## Protect Cisco Webex in real time

Review our best practices for [securing and collaborating with external users](best-practices#secure-collaboration-with-external-users-by-enforcing-real-time-session-controls) and [blocking and protecting the download of sensitive data to unmanaged or risky devices](best-practices#block-and-protect-download-of-sensitive-data-to-unmanaged-or-risky-devices).

## Connect Cisco Webex to Microsoft Defender for Cloud Apps

Use the connector APIs to connect Microsoft Defender for Cloud Apps to your existing Cisco Webex account. Connecting Microsoft Defender for Cloud Apps to your Cisco Webex account gives you visibility into and control over Webex users, activities, and files. For information about how Defender for Cloud Apps protects Cisco Webex, see [Protect Cisco Webex](protect-webex).

**Prerequisites**:

- We suggest that you create a dedicated service account for the connection. This enables you to see that governance actions performed in Webex as being performed from this account, such as delete messages sent in Webex. Otherwise, the name of the admin who connected Defender for Cloud Apps to Webex will appear as the user who performed the actions.
- You must have Full Administrator **and** Compliance Officer roles in Webex (under **Roles and Security** &gt; **Administrator Roles**).

    ![Screenshot of the prerequisite Full Administrator and Compliance Officer roles required in Webex.](media/connect-webex-roles.png)

**To connect Webex to Defender for Cloud Apps**:

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**.
2. In the **App connectors** page, click **+Connect an app**, followed by **Cisco Webex**.
3. In the next window, give the connector a name and select **Next**.

    ![Screenshot of the Cisco Webex connector name and configuration dialog in Defender for Cloud Apps.](media/cisco-webex.png)
4. In the **Follow the link** page, select **Connect Cisco Webex**. The Webex sign in page opens. Enter your credentials to allow Defender for Cloud Apps access to your team's Webex instance.
5. Webex asks you if you want to allow Defender for Cloud Apps access to your team information, activity log, and perform activities as a team member. To proceed, click **Allow**.
6. Back in the Defender for Cloud Apps console, you should receive a message that Webex was successfully connected.
7. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**. Make sure the status of the connected App Connector is **Connected**.

After connecting Webex, you'll receive events for 7 days prior to connection. Defender for Cloud Apps scans events over the past three months. To increase the default three-month Defender for Cloud Apps event scan period, you must have a Cisco Webex Pro license and open a ticket with Defender for Cloud Apps support.

If you have any problems connecting the app, see [Troubleshooting App Connectors](troubleshooting-api-connectors-using-error-messages).