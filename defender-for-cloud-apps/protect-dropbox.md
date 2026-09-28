---
layout: Conceptual
title: Protect your Dropbox environment - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/protect-dropbox
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
description: Connect Dropbox to Microsoft Defender for Cloud Apps by using the API connector to monitor user activity, detect threats and external sharing risks, and enable automated remediation controls.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: AmitMishaeli
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 0f14bc4d-2e9f-a550-b8ec-9c4acd619303
document_version_independent_id: 0f14bc4d-2e9f-a550-b8ec-9c4acd619303
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/protect-dropbox.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: protect-dropbox
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/protect-dropbox.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 3e269144-b8cd-f51e-963e-fcb6f0e93cbb
---

# Protect your Dropbox environment - Microsoft Defender for Cloud Apps | Microsoft Learn

Dropbox is a cloud storage and collaboration tool that lets users share documents across your organization and with partners. However, Dropbox can expose sensitive data to external collaborators or make it publicly available through a shared link. Malicious actors or unaware employees can cause these incidents.

Connecting Dropbox to Defender for Cloud Apps gives you better insight into your users' activities. It provides threat detection through machine learning anomaly detections and information protection detections, such as detecting external information sharing. You can also enable automated remediation controls.

Note

Dropbox changed the way shared folders are stored, moving them to Team Spaces. The Defender for Cloud Apps file scan will be updated in due course to include Team Spaces.

## Main threats

Dropbox environments face the following main threats:

- Compromised accounts and insider threats
- Data leakage
- Insufficient security awareness
- Malware
- Ransomware
- Unmanaged bring your own device (BYOD)

## How Defender for Cloud Apps helps to protect your environment

Use the following best practices to protect your Dropbox environment with Defender for Cloud Apps:

- [Detect cloud threats, compromised accounts, and malicious insiders](best-practices#detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware)
- [Discover, classify, label, and protect regulated and sensitive data stored in the cloud](best-practices#discover-classify-label-and-protect-regulated-and-sensitive-data-stored-in-the-cloud)
- [Enforce DLP and compliance policies for data stored in the cloud](best-practices#enforce-dlp-and-compliance-policies-for-data-stored-in-the-cloud)
- [Limit exposure of shared data and enforce collaboration policies](best-practices#limit-exposure-of-shared-data-and-enforce-collaboration-policies)
- [Use the audit trail of activities for forensic investigations](best-practices#use-the-audit-trail-of-activities-for-forensic-investigations)

## Control Dropbox with built-in policies and policy templates

You can use the following built-in policy templates to detect and notify you about potential threats:

Important

File policies retire on January 6, 2027. To maintain file-based data protection for this app, [migrate to Microsoft Purview DLP or auto-labeling policies](migrate-file-policies-to-purview).

| Type | Name |
| --- | --- |
| Built-in anomaly detection policy | [Activity from anonymous IP addresses](anomaly-detection-policy#activity-from-anonymous-ip-addresses)[Activity from infrequent country](anomaly-detection-policy#activity-from-infrequent-country)[Activity from suspicious IP addresses](anomaly-detection-policy#activity-from-suspicious-ip-addresses)[Impossible travel](anomaly-detection-policy#impossible-travel)[Activity performed by terminated user](anomaly-detection-policy#activity-performed-by-terminated-user) (requires Microsoft Entra ID as IdP)[Malware detection](anomaly-detection-policy#malware-detection)[Multiple failed login attempts](anomaly-detection-policy#multiple-failed-login-attempts)[Ransomware detection](anomaly-detection-policy#ransomware-activity)[Unusual file deletion activities](anomaly-detection-policy#unusual-activities-by-user)[Unusual file share activities](anomaly-detection-policy#unusual-activities-by-user)[Unusual multiple file download activities](anomaly-detection-policy#unusual-activities-by-user) |
| Activity policy template | Logon from a risky IP addressMass download by a single userPotential ransomware activity |
| File policy template | Detect a file shared with an unauthorized domainDetect a file shared with personal email addressesDetect files with PII/PCI/PHI |

For more information about creating policies, see [Create a policy in Defender for Cloud Apps](control-cloud-apps-with-policies#create-a-policy).

## Automate governance controls

You can also apply and automate Dropbox governance actions to fix detected threats:

| Type | Action |
| --- | --- |
| Data governance | - Remove direct shared link- Send DLP violation digest to file owners- Trash file |
| User governance | - Notify user on alert (via Microsoft Entra ID) - Require user to sign in again (via Microsoft Entra ID) - Suspend user (via Microsoft Entra ID) |

To learn more about fixing threats from apps, see [Governing connected apps](governance-actions).

## Protect Dropbox in real time

Review our best practices for [securing and collaborating with external users](best-practices#secure-collaboration-with-external-users-by-enforcing-real-time-session-controls) and [blocking and protecting the download of sensitive data to unmanaged or risky devices](best-practices#block-and-protect-download-of-sensitive-data-to-unmanaged-or-risky-devices).

## SaaS security posture management for Dropbox

Connect Dropbox to automatically get security posture recommendations for Dropbox in Microsoft Secure Score. In Secure Score, select **Recommended actions** and filter by **Product** = **Dropbox**. Dropbox supports security recommendations to *Enable web session timeout for web users*.

For more information, see:

- [Security posture management for SaaS apps](security-saas)
- [Microsoft Secure Score](/en-us/microsoft-365/security/defender/microsoft-secure-score)

## Connect Dropbox to Microsoft Defender for Cloud Apps

Use the following instructions to connect Microsoft Defender for Cloud Apps to your existing Dropbox account using the connector APIs. Connector APIs let Defender for Cloud Apps connect directly to supported apps for monitoring and governance. This connection gives you visibility into and control over Dropbox use.

Dropbox enables access to files from shared links without signing in. Defender for Cloud Apps registers users who access files without signing in as Unauthenticated users. If you see unauthenticated Dropbox users, it might indicate users who aren't from your organization, or they might be recognized users from within your organization who didn't sign in.

**To connect Dropbox to Defender for Cloud Apps**

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**.
2. In the **App connectors** page, select **+Connect an app**, followed by **Dropbox**.

    [![Screenshot that shows how to connect Dropbox in the Microsoft Defender portal.](media/connect-dropbox/connect-an-app-drop-box.png)](media/connect-dropbox/connect-an-app-drop-box.png#lightbox)
3. In the next window, give the connector a name and select **Next**.
4. In the **Enter details** window, enter the admin account email address.
5. In the **Follow the link** window, select **Connect Dropbox**.

    The Dropbox sign in page opens. Enter your credentials to allow Defender for Cloud Apps access to your team's Dropbox instance.
6. Dropbox asks you if you want to allow Defender for Cloud Apps access to your team information, activity log, and perform activities as a team member. To proceed, select **Allow**.
7. Back in the Defender for Cloud Apps console, you should receive a message that Dropbox was successfully connected.
8. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**. Make sure the status of the connected App Connector is **Connected**.

    After connecting DropBox, you'll receive events for seven days prior to connection.

Note

Any Dropbox events for adding a file are displayed in Defender for Cloud Apps as Upload file to align to all other apps connected to Defender for Cloud Apps.

If you have any problems connecting the app, see [Troubleshooting App Connectors](troubleshooting-api-connectors-using-error-messages).