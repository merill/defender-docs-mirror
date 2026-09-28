---
layout: Conceptual
title: Protect your OneLogin environment - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/protect-onelogin
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
description: Connect OneLogin to Microsoft Defender for Cloud Apps with the API connector to gain visibility into admin activity and managed user sign-ins and detect anomalous behavior.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: AmitMishaeli
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 1f04bfc8-4a8e-89e8-5dd4-189cc541f2e3
document_version_independent_id: 1f04bfc8-4a8e-89e8-5dd4-189cc541f2e3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/protect-onelogin.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: protect-onelogin
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/protect-onelogin.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 7dc2f016-05bc-35c2-0012-7327e914f46c
---

# Protect your OneLogin environment - Microsoft Defender for Cloud Apps | Microsoft Learn

As an identity and access management solution, OneLogin holds the keys to your organizations most business critical services. OneLogin manages the authentication and authorization processes for your users. Any abuse of OneLogin by a malicious actor or any human error might expose your most critical assets and services to potential attacks.

Connecting OneLogin to Defender for Cloud Apps gives you improved insights into your OneLogin admin activities and managed users sign-ins and provides threat detection for anomalous behavior.

## Main threats to your OneLogin environment

The main threats to consider in a OneLogin environment include:

- Compromised accounts and insider threats
- Data leakage
- Insufficient security awareness
- Unmanaged bring your own device (BYOD)

## How Defender for Cloud Apps helps to protect your environment

Defender for Cloud Apps helps you protect your OneLogin environment in the following ways:

- [Detect cloud threats, compromised accounts, and malicious insiders](best-practices#detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware)
- [Use the audit trail of activities for forensic investigations](best-practices#use-the-audit-trail-of-activities-for-forensic-investigations)

## Control OneLogin with policies

The following table lists the policy types and detections you can use to monitor and control OneLogin activity:

| **Type** | **Name** |
| --- | --- |
| Built-in anomaly detection policy | [Activity from anonymous IP addresses](anomaly-detection-policy#activity-from-anonymous-ip-addresses)[Activity from infrequent country](anomaly-detection-policy#activity-from-infrequent-country)[Activity from suspicious IP addresses](anomaly-detection-policy#activity-from-suspicious-ip-addresses)[Impossible travel](anomaly-detection-policy#impossible-travel)[Activity performed by terminated user](anomaly-detection-policy#activity-performed-by-terminated-user) (requires Microsoft Entra ID as IdP) [Multiple failed login attempts](anomaly-detection-policy#multiple-failed-login-attempts)[Unusual administrative activities](anomaly-detection-policy#unusual-activities-by-user)[Unusual impersonated activities](anomaly-detection-policy#unusual-activities-by-user) |
| Activity policy | Built a customized policy by the [OneLogin activities](https://developers.onelogin.com/api-docs/1/events/event-resource) |

For more information about creating policies, see [Create a policy](control-cloud-apps-with-policies#create-a-policy).

## Automate governance controls

Besides monitoring for potential threats, you can apply and automate the following OneLogin governance actions to fix detected threats:

| **Type** | **Action** |
| --- | --- |
| User governance | Notify user on alert (via Microsoft Entra ID) Require user to sign in again (via Microsoft Entra ID)  Suspend user (via Microsoft Entra ID) |

For more information about remediating threats from apps, see [Governing connected apps](governance-actions).

## Protect OneLogin in real time

Review our best practices for [securing and collaborating with external users](best-practices#secure-collaboration-with-external-users-by-enforcing-real-time-session-controls) and [blocking and protecting the download of sensitive data to unmanaged or risky devices](best-practices#block-and-protect-download-of-sensitive-data-to-unmanaged-or-risky-devices).

## Connect OneLogin to Microsoft Defender for Cloud Apps

The following instructions explain how to connect Microsoft Defender for Cloud Apps to your existing OneLogin app using the App Connector APIs. This connection gives you visibility into and control over your organization's OneLogin use.

### Prerequisites

Before you begin, make sure you meet the following prerequisite:

- The OneLogin account used for logging into OneLogin must be a Super User. For more information, see [OneLogin administrative privileges](https://onelogin.service-now.com/kb_view_customer.do?sysparm_article=KB0010391).

### Configure OneLogin

Perform the following steps in OneLogin to create the credentials required for the connector:

1. Sign-in to the OneLogin admin portal.
2. Select **New Credential**.
3. Name the application **Microsoft Defender for Cloud Apps**, and assign **Read all** permissions.
4. Copy the **Client ID** and the **Client Secret**. You'll enter them when you configure the OneLogin connector in Defender for Cloud Apps.

### Configure Defender for Cloud Apps

Perform the following steps in Defender for Cloud Apps to create the OneLogin connector:

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**.
2. In the **App connectors** page, select **+Connect an app**, followed by **OneLogin**.
3. In the next window, give the connector a descriptive name, and select **Next**.

    [![Screenshot that shows where to add the instance name when connecting OneLogin in the Defender portal.](media/connect-onelogin.png)](media/connect-onelogin.png#lightbox)
4. In the **Enter details** window, enter the **Client ID** and the **Client Secret** that you copied and select **Submit**.
5. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**. Make sure the status of the connected App Connector is **Connected**.
6. The first connection can take up to 4 hours to get all users and their activities after the connector was established.
7. After the connector's **Status** is marked as **Connected**, the connector is live and working.