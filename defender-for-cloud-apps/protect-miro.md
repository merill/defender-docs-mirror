---
layout: Conceptual
title: Protect your Miro environment - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/protect-miro
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
description: Connect Miro to Microsoft Defender for Cloud Apps by using the API connector to gain visibility into user activity and detect anomalous behavior.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: AmitMishaeli
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 298ff3c7-e839-03d1-ea92-188981f2d8ae
document_version_independent_id: 298ff3c7-e839-03d1-ea92-188981f2d8ae
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/protect-miro.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: protect-miro
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/protect-miro.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: ee03e5b4-fe77-3f25-c2be-623714887d14
---

# Protect your Miro environment - Microsoft Defender for Cloud Apps | Microsoft Learn

Miro is an online workspace that enables distributed, cross-functional teams organize and collaborate on projects. Miro holds critical data of your organization, which makes Miro a target for malicious actors.

Connecting Miro to Defender for Cloud Apps gives you improved insights into your users' activities and provides threat detection using machine learning based anomaly detections. Before you connect, review the prerequisites for connecting Miro to Defender for Cloud Apps to ensure your environment is ready.

## Main threats to your Miro environment

The main threats to consider in a Miro environment include the following:

- Compromised accounts and insider threats
- Data leakage
- Insufficient security awareness
- Unmanaged bring your own device (BYOD)

## How Defender for Cloud Apps helps to protect your environment

Defender for Cloud Apps helps protect your Miro environment in the following ways:

- [Detect cloud threats, compromised accounts, and malicious insiders](best-practices#detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware)
- [Use the audit trail of activities for forensic investigations](best-practices#use-the-audit-trail-of-activities-for-forensic-investigations)

## Control Miro with policies

The following table lists the detection policies available for Miro in Defender for Cloud Apps.

| **Type** | **Name** |
| --- | --- |
| Built-in anomaly detection policy | [Activity from anonymous IP addresses](anomaly-detection-policy#activity-from-anonymous-ip-addresses)[Activity from infrequent country](anomaly-detection-policy#activity-from-infrequent-country)[Activity from suspicious IP addresses](anomaly-detection-policy#activity-from-suspicious-ip-addresses)[Impossible travel](anomaly-detection-policy#impossible-travel)[Activity performed by terminated user](anomaly-detection-policy#activity-performed-by-terminated-user) (requires Microsoft Entra ID as IdP) [Multiple failed login attempts](anomaly-detection-policy#multiple-failed-login-attempts) |
| Activity policy | Built a customized policy by using the [Miro Audit Log](https://help.miro.com/hc/en-us/articles/360017571434-Audit-logs) activities |

For more information about creating policies, see [Create a policy](control-cloud-apps-with-policies#create-a-policy).

## Automate governance controls

In addition to monitoring for potential threats, you can apply and automate the following Miro governance actions to remediate detected threats.

### Supported governance actions

The following table lists the governance actions supported for Miro.

| **Type** | **Action** |
| --- | --- |
| User governance | Notify user on alert (via Microsoft Entra ID) Require user to sign in again (via Microsoft Entra ID)  Suspend user (via Microsoft Entra ID) |

For more information about remediating threats from apps, see [Governing connected apps](governance-actions).

## Connect Miro to Microsoft Defender for Cloud Apps

This section provides instructions for connecting Microsoft Defender for Cloud Apps to your existing Miro account using the App Connector APIs. This connection gives you visibility into and control over Miro usage.

**Prerequisites**:

- You must have a Miro account with an enterprise plan.

### Configure Miro

Perform the following steps in Miro to create the app registration needed for the connector:

1. Sign into [Miro](https://miro.com/app/dashboard/) portal with a company admin account.
2. Create a developer team with default permissions.
3. Create a new application in the developer team and ensure the “Expire user authentication token” setting is checked.
4. Copy the **Client ID** and **Client secret**. You'll need them later.
5. Configure 'OAuth2.0' by setting the redirect URL to 'https://portal.cloudappsecurity.com/api/oauth/saga'.
6. Grant these required permissions, and then select **Install app and get OAuth token**.

- ‘auditlogs:read’
- ‘organization:read’

### Connect Microsoft Defender for Cloud Apps

After you configure Miro, complete the connection in Defender for Cloud Apps by following these steps:

1. In the [Defender for Cloud Apps](https://portal.cloudAppSecurity.com) portal, navigate to Investigate &gt; Connected apps.
2. In the **App connectors** page, select **Connect an app**, and choose **Miro**.
3. In the connection wizard, enter a name for Miro connection, and select **Connect Miro**.
4. Enter the **Client ID, Client secret** and select **Connect in Miro**.
5. Select the Miro team that you want to connect with Defender for Cloud Apps and select **Add** again. Note that this Miro team is different from the developer team in which you created the app.
6. Select **Test now** to make sure the connection succeeded. Audit events start flowing into Defender for Cloud apps from the time the connection is successfully established.