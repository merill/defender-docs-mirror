---
layout: Conceptual
title: Protect your Slack Enterprise environment - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/protect-slack
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
description: Connect Slack Enterprise to Microsoft Defender for Cloud Apps with the API connector to gain visibility into user activity and detect anomalous behavior.
ms.date: 2026-06-16T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: AmitMishaeli
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1014
locale: en-us
document_id: e0773a92-2714-6bfc-fc61-f991664bbb2d
document_version_independent_id: e0773a92-2714-6bfc-fc61-f991664bbb2d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/protect-slack.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: protect-slack
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/protect-slack.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 42572411-a97c-8d37-842b-6335102ce270
---

# Protect your Slack Enterprise environment - Microsoft Defender for Cloud Apps | Microsoft Learn

Slack is a cloud service that helps organizations collaborate and communicate in one place. Along with the benefits of effective collaboration in the cloud, your organization's most critical assets might be exposed to threats. Exposed assets include messages, channels, and files with potentially sensitive information, collaboration, and partnership details, and more. Preventing exposure of this data requires continuous monitoring to prevent any malicious actors or security-unaware insiders from exfiltrating sensitive information.

Connecting Slack Enterprise to Defender for Cloud Apps gives you improved insights into your users' activities and provides threat detection for anomalous behavior.

## Main threats to your Slack Enterprise environment

- Compromised accounts and insider threats
- Data leakage
- Insufficient security awareness
- Unmanaged bring your own device (BYOD)

## How Defender for Cloud Apps helps to protect your environment

Defender for Cloud Apps helps you protect your Slack Enterprise environment with the following best practices:

- [Detect cloud threats, compromised accounts, and malicious insiders](best-practices#detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware)
- [Use the audit trail of activities for forensic investigations](best-practices#use-the-audit-trail-of-activities-for-forensic-investigations)

## Control Slack with policies

The following table lists the policy types you can use to monitor and control Slack activities:

| **Type** | **Name** |
| --- | --- |
| Built-in anomaly detection policy | [Activity from anonymous IP addresses](anomaly-detection-policy#activity-from-anonymous-ip-addresses)[Activity from infrequent country](anomaly-detection-policy#activity-from-infrequent-country)[Activity from suspicious IP addresses](anomaly-detection-policy#activity-from-suspicious-ip-addresses)[Impossible travel](anomaly-detection-policy#impossible-travel)[Activity performed by terminated user](anomaly-detection-policy#activity-performed-by-terminated-user) (requires Microsoft Entra ID as IdP) [Multiple failed login attempts](anomaly-detection-policy#multiple-failed-login-attempts)[Unusual administrative activities](anomaly-detection-policy#unusual-activities-by-user)[Unusual impersonated activities](anomaly-detection-policy#unusual-activities-by-user) |
| Activity policy | Built a customized policy by the [Slack Audit Log](https://api.slack.com/admins/audit-logs#audit_logs_actions) activities |

For more information about creating policies, see [Create a policy](control-cloud-apps-with-policies#create-a-policy).

## Automate governance controls

In addition to monitoring for potential threats, you can apply and automate the following Slack governance actions to remediate detected threats:

| **Type** | **Action** |
| --- | --- |
| User governance | Notify user on alert (via Microsoft Entra ID) Require user to sign in again (via Microsoft Entra ID)  Suspend user (via Microsoft Entra ID) |

For more information about remediating threats from apps, see [Governing connected apps](governance-actions).

## Protect Slack in real time

Review our best practices for [securing and collaborating with guests](best-practices#secure-collaboration-with-external-users-by-enforcing-real-time-session-controls) and [blocking and protecting the download of sensitive data to unmanaged or risky devices](best-practices#block-and-protect-download-of-sensitive-data-to-unmanaged-or-risky-devices).

## Connect Slack to Microsoft Defender for Cloud Apps

The following instructions explain how to connect Microsoft Defender for Cloud Apps to your existing Slack using the App Connector APIs. This connection gives you visibility into and control over your organization's Slack use.

### Prerequisites

- Your Slack tenant must meet the following requirements:
    - Your Slack tenant must have an **Enterprise** license. Defender for Cloud Apps doesn't support non-enterprise licenses.
    - Your Slack tenant should have **Discovery API** enabled. To enable **Discovery API** for your Slack tenant, contact Slack support.
- The org Owner needs to be logged into their Slack organization within their browser before installing the connector.

### Connect Slack to Defender for Cloud Apps

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**.
2. In the **App connectors** page, select **+Connect an app**, followed by **Slack**.
3. In the next window, give the connector a descriptive name, and select **Next**.

    ![Screenshot that shows where to enter the instance name in the Defender portal.](media/connect-slack.png)
4. In the **External Link** page, select **Connect Slack**.

    ![Screenshot that shows where to enter the external link and connect to Slack.](media/connect-in-slack.png)
5. You'll be redirected to the Slack page. Make sure the org Owner is already logged into the Slack organization.
6. In the Slack Authorization page, make sure to choose the correct organization from the dropdown in the top-right corner.
7. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**. Make sure the status of the connected App Connector is **Connected**.

    Note

    - The first connection can take up to 4 hours to get all users and their activities in the 7 days before the connection.
    - After the connector's **Status** is marked as **Connected**, the connector is live and works.
    - The received activities are from the Slack Audit Log API. You can find them in the [Slack documentation](https://api.slack.com/admins/audit-logs#audit_logs_actions).
    - **Send Slack message** activity is an activity that can be received from [Conditional Access app control](proxy-intro-aad), and not from the Slack API connector.