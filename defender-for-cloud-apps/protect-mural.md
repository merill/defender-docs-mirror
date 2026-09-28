---
layout: Conceptual
title: Protect your Mural environment - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/protect-mural
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
description: Connect Mural to Microsoft Defender for Cloud Apps by using the API connector to monitor user activity and detect anomalous behavior.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: AmitMishaeli
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: d04fadfc-b998-e3e9-e205-bc799c318a42
document_version_independent_id: d04fadfc-b998-e3e9-e205-bc799c318a42
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/protect-mural.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: protect-mural
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/protect-mural.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 277f617c-de9f-9201-8ce3-20fc1c09f510
---

# Protect your Mural environment - Microsoft Defender for Cloud Apps | Microsoft Learn

Mural is an online workspace where teams can organize and work together on projects. Mural holds key data for your organization, which makes it a target for malicious actors.

When you connect Mural to Defender for Cloud Apps, you get better visibility into user activity. You also get threat detection with machine learning based anomaly detections.

## Main threats to your Mural environment

Connecting Mural without adequate protection exposes your organization to the following threats:

- Compromised accounts and insider threats
- Data leakage
- Insufficient security awareness
- Unmanaged bring your own device (BYOD)

## How Defender for Cloud Apps helps to protect your environment

Defender for Cloud Apps can help protect your Mural environment in the following ways:

- [Detect cloud threats, compromised accounts, and malicious insiders](best-practices#detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware)
- [Use the audit trail of activities for forensic investigations](best-practices#use-the-audit-trail-of-activities-for-forensic-investigations)

## Control Mural with policies

You can use these policy types to monitor and control Mural.

Note

The **Activity performed by terminated user** policy requires Microsoft Entra ID as your identity provider (IdP).

| **Type** | **Name** |
| --- | --- |
| **Built-in anomaly detection policy** | [Activity from anonymous IP addresses](anomaly-detection-policy#activity-from-anonymous-ip-addresses)[Activity from infrequent country](anomaly-detection-policy#activity-from-infrequent-country)[Activity from suspicious IP addresses](anomaly-detection-policy#activity-from-suspicious-ip-addresses)[Impossible travel](anomaly-detection-policy#impossible-travel)[Activity performed by terminated user](anomaly-detection-policy#activity-performed-by-terminated-user) (requires Microsoft Entra ID as IdP) [Multiple failed login attempts](anomaly-detection-policy#multiple-failed-login-attempts) |
| **Activity policy** | Build a custom policy with the [Mural Audit Log API](https://support.mural.co/s/article/audit-logs). |

For more information about creating policies, see [Create a policy](control-cloud-apps-with-policies#create-a-policy).

## Automate governance controls

You can also apply and automate these Mural governance actions to fix detected threats:

| **Type** | **Action** |
| --- | --- |
| **User governance** | Notify user on alert (via Microsoft Entra ID) Require user to sign in again (via Microsoft Entra ID)  Suspend user (via Microsoft Entra ID) |

To learn more about fixing threats from apps, see [Governing connected apps](governance-actions).

## Connect Mural to Microsoft Defender for Cloud Apps

The following instructions explain how to connect Microsoft Defender for Cloud Apps to your existing Mural account using the App Connector APIs. This connection gives you visibility into and control over Mural usage.

### Prerequisites

- A Mural enterprise account.
- You must be signed-in as an admin to Mural.

### Connect Mural to Defender for Cloud Apps

Perform the following steps to connect Mural to Defender for Cloud Apps:

1. Sign into your [Mural](https://app.mural.co/) account.
2. Create an API Key and then copy the key.
3. In the Microsoft Defender portal, select **Settings &gt; Cloud Apps &gt; Connected Apps &gt; App Connectors &gt; Connect an app &gt; Mural**.
4. In the connection wizard, enter your instance name, and then select **Next**.
5. Paste the API key you copied from the Mural portal and then select **Submit**.

After the connection is established, Defender for Cloud Apps starts fetching Mural audit logs. Because Mural's API logs are delayed by 48 hours, audit log ingestion into Defender for Cloud Apps is also delayed by 48 hours.