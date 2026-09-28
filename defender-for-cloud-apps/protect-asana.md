---
layout: Conceptual
title: Protect your Asana environment - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/protect-asana
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
description: Connect Asana to Microsoft Defender for Cloud Apps with the API connector to monitor user activity, improve visibility, and detect threats.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: AmitMishaeli
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 57723c22-1c7d-aff0-ce8e-9a6c2cf0f8f7
document_version_independent_id: 57723c22-1c7d-aff0-ce8e-9a6c2cf0f8f7
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/protect-asana.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: protect-asana
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/protect-asana.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: cbd0f520-d392-574d-b94b-30d552d47d9e
---

# Protect your Asana environment - Microsoft Defender for Cloud Apps | Microsoft Learn

Asana is a cloud-based tool for project management. Your users can collaborate on projects and tasks across your organization and with partners. Asana holds critical data, which makes it a target for malicious actors.

Connect Asana to Defender for Cloud Apps to get better insights into user activity. You also get threat detection through machine learning anomaly detections.

This article explains how to connect Asana to Defender for Cloud Apps using the App Connector API, configure policies to monitor Asana activity, and automate governance actions.

Main threats include:

- Compromised accounts and insider threats
- Data leakage
- Insufficient security awareness
- Unmanaged bring your own device (BYOD)

## Control Asana with policies

The following table lists the policy types you can use to monitor and control Asana activity.

| **Type** | **Name** |
| --- | --- |
| **Built-in anomaly detection policy** | [Activity from anonymous IP addresses](anomaly-detection-policy#activity-from-anonymous-ip-addresses)[Activity from infrequent country](anomaly-detection-policy#activity-from-infrequent-country)[Activity from suspicious IP addresses](anomaly-detection-policy#activity-from-suspicious-ip-addresses)[Impossible travel](anomaly-detection-policy#impossible-travel)[Activity performed by terminated user](anomaly-detection-policy#activity-performed-by-terminated-user) (requires Microsoft Entra ID as IdP) [Multiple failed login attempts](anomaly-detection-policy#multiple-failed-login-attempts) |
| **Activity policy** | Built a customized policy by using the [Asana Audit Log](https://developers.asana.com/docs/audit-log-events) activities |

For more information about creating policies, see [Create a policy](control-cloud-apps-with-policies#create-a-policy).

## Automate governance controls

You can also automate Asana governance actions to fix detected threats. The following table lists the available actions:

| **Type** | **Action** |
| --- | --- |
| **User governance** | Notify user on alert (via Microsoft Entra ID) Require user to sign in again (via Microsoft Entra ID)  Suspend user (via Microsoft Entra ID) |

For more information about remediating threats from apps, see [Governing connected apps](governance-actions).

## Connect Asana to Defender for Cloud Apps

Use the App Connector APIs to connect Microsoft Defender for Cloud Apps to your existing Asana account. The connection gives you visibility into and control over your organization's Asana use.

### Prerequisites

Before you connect Asana, make sure you meet the following requirements:

- An Asana enterprise account.
- You must be signed-in as an admin to Asana.

### Connect Asana

Collect the access token and workspace ID from Asana by completing the following steps.

1. Sign in to [Asana](https://app.asana.com/) with an admin account.
2. If you have an existing service account, you might need to select **Reset and generate new token** before continuing. Copy the service account token.
3. Copy the workspace ID from the URL and save it for future reference.

### Configure Defender for Cloud Apps

After you collect the required Asana values, complete the connection in Microsoft Defender for Cloud Apps.

1. In the [Microsoft Defender portal](https://security.microsoft.com), navigate to **Settings &gt; Cloud Apps &gt; Connected apps &gt; App Connectors**.
2. Select **Connect an app** and then select **Asana.**
3. Enter an Instance name, and select **Next.**
4. Enter the copied access token and workspace ID in API Key and workspace ID fields. Once entered select **Submit.**
5. Defender for Cloud Apps will start to fetch Asana audit logs once the connection is successfully established.