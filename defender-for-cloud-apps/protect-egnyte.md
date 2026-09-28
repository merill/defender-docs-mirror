---
layout: Conceptual
title: Protect your Egnyte environment (Preview) - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/protect-egnyte
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
description: Connect Egnyte to Microsoft Defender for Cloud Apps by using the API connector to gain visibility into user activity and detect anomalous behavior.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: AmitMishaeli
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 74c853e9-a815-76c3-a423-c3e48f6d9334
document_version_independent_id: 74c853e9-a815-76c3-a423-c3e48f6d9334
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/protect-egnyte.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: protect-egnyte
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/protect-egnyte.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 4c915f11-1df3-db3a-8346-83359b05879a
---

# Protect your Egnyte environment (Preview) - Microsoft Defender for Cloud Apps | Microsoft Learn

Egnyte is a cloud platform for file sharing and data governance. Cloud tools like Egnyte help teams work together, but they can also expose critical assets to threats. You need to monitor Egnyte so that bad actors or careless insiders can't leak sensitive data.

Connecting Egnyte to Defender for Cloud Apps gives you improved insights into your users' activities and provides threat detection for anomalous behavior.

## Main threats

Using Egnyte without Defender for Cloud Apps exposes your organization to the following threats:

- Compromised accounts and insider threats
- Insufficient security awareness
- Unmanaged bring your own device (BYOD)

## How Defender for Cloud Apps helps to protect your environment

Defender for Cloud Apps helps protect your Egnyte environment in the following ways:

- [Detect cloud threats, compromised accounts, and malicious insiders](best-practices#detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware)
- [Use the audit trail of activities for forensic investigations](best-practices#use-the-audit-trail-of-activities-for-forensic-investigations)

## Control Egnyte with policies

The following table lists the policy types you can use to monitor and control Egnyte activities:

| **Type** | **Name** |
| --- | --- |
| Built-in anomaly detection policy | [Activity from anonymous IP addresses](anomaly-detection-policy#activity-from-anonymous-ip-addresses)[Activity from infrequent countries/regions](anomaly-detection-policy#activity-from-infrequent-country)[Activity from suspicious IP addresses](anomaly-detection-policy#activity-from-suspicious-ip-addresses)[Impossible travel](anomaly-detection-policy#impossible-travel)[Activity performed by terminated user](anomaly-detection-policy#activity-performed-by-terminated-user) (requires Microsoft Entra ID as IdP) [Multiple failed login attempts](anomaly-detection-policy#multiple-failed-login-attempts) |
| Activity policy | Build a customized policy by the Egnyte activities |

For more information about creating policies, see [Create a policy](control-cloud-apps-with-policies#create-a-policy).

## Automate governance controls

You can also automate Egnyte governance actions to respond to detected threats:

| **Type** | **Action** |
| --- | --- |
| User governance | Notify user on alert (via Microsoft Entra ID) Require user to sign in again (via Microsoft Entra ID)  Suspend user (via Microsoft Entra ID) |

For more information about remediating threats from apps, see [Governing connected apps](governance-actions).

## Protect Egnyte in real time

Review our best practices for [securing and collaborating with external users](best-practices#secure-collaboration-with-external-users-by-enforcing-real-time-session-controls) and [blocking and protecting the download of sensitive data to unmanaged or risky devices](best-practices#block-and-protect-download-of-sensitive-data-to-unmanaged-or-risky-devices).

## Connect Egnyte to Microsoft Defender for Cloud Apps

Use the App Connector APIs to connect Microsoft Defender for Cloud Apps to your existing Egnyte environment. The resulting connection gives you visibility into and control over your organization's use of Egnyte.

### Prerequisites

Make sure you meet the following requirements before you connect Egnyte to Defender for Cloud Apps:

- The authorizing user must be one of the following:

    - Power user with **can run reports** role
    - Administrator
- Audit reporting must be available in Egnyte's plan

**To connect Egnyte to Microsoft Defender for Cloud Apps**:

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**.
2. In the **App connectors** page, select **+Connect an app**, and then select **Egnyte**.
3. In the window that appears, give the connector a descriptive name, and then select **Next**.
4. In the **Enter details** page, in **Application URL**, insert your Egnyte URL by using the following format: `https://<domain_name>.egnyte.com`
5. Select **Next**.
6. Select **Connect Egnyte**.
7. In the redirected page, select **Allow**.
8. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**. Make sure the status of the connected App Connector is **Connected**.

Note

- Microsoft recommends using a short lived access token. Egnyte doesn't currently support short lived tokens. We recommend refreshing your access token every 6 months as a security best practice. To refresh the access token, revoke the old token. For more information, see [Revoking an oAuth token](https://developers.egnyte.com/docs/read/Public_API_Authentication#Revoking-an-OAuth-Token). Once the old token is revoked, reconnect the Egnyte connector.
- Microsoft Defender for Cloud Apps intentionally provides a lower rate limit than Egnyte's maximum to avoid exceeding the API constraints. For more information, see the relevant Egnyte documentation [Rate limiting](https://developers.egnyte.com/docs/read/Best_Practices) and [Audit Reporting API v2](https://developers.egnyte.com/docs/read/Audit_Reporting_API_V2).