---
layout: Conceptual
title: Protect your Okta environment - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/protect-okta
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
description: Connect Okta to Microsoft Defender for Cloud Apps with the API connector to monitor admin activity, managed users, and sign-ins, and detect anomalous behavior.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: AmitMishaeli
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 65831163-8ddb-a181-d64a-621765842201
document_version_independent_id: 65831163-8ddb-a181-d64a-621765842201
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/protect-okta.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: protect-okta
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/protect-okta.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/cd48b104-e308-4e08-a405-66f04a7df418
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/ac23bdb5-c078-4620-8ee2-60eba45e97f8
platformId: de667dc5-25e0-dabc-34a5-b3fb8239fd8d
---

# Protect your Okta environment - Microsoft Defender for Cloud Apps | Microsoft Learn

As an identity and access management solution, Okta holds the keys to your organizations most business critical services. Okta manages the authentication and authorization processes for your users and customers. Any abuse of Okta by a malicious actor or any human error might expose your most critical assets and services to potential attacks.

Connecting Okta to Defender for Cloud Apps gives you improved insights into your Okta admin activities, managed users, and customer sign-ins and provides threat detection for anomalous behavior.

Use this app connector to access SaaS Security Posture Management (SSPM) features, via security controls reflected in Microsoft Secure Score. [Learn more](/en-us/microsoft-365/security/defender/microsoft-secure-score).

## Main threats to your Okta environment

- Compromised accounts and insider threats

## How Defender for Cloud Apps helps to protect your environment

Defender for Cloud Apps helps you protect your Okta environment with the following best practices:

- [Detect cloud threats, compromised accounts, and malicious insiders](best-practices#detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware)
- [Use the audit trail of activities for forensic investigations](best-practices#use-the-audit-trail-of-activities-for-forensic-investigations)

## SaaS security posture management for Okta

Connect Okta to Microsoft Defender for Cloud Apps using the procedure below to automatically get security recommendations in Microsoft Secure Score.

In Secure Score, select **Recommended actions** and filter by **Product** = **Okta**. For example, recommendations for Okta include:

- *Enable multi-factor authentication*
- *Enable session timeout for web users*
- *Enhance password requirements*

For more information, see:

- [Security posture management for SaaS apps](security-saas)
- [Microsoft Secure Score](/en-us/microsoft-365/security/defender/microsoft-secure-score)

## Control Okta with built-in policies and policy templates

You can use the following built-in policy templates to detect and notify you about potential threats:

| Type | Name |
| --- | --- |
| Built-in anomaly detection policy | [Activity from anonymous IP addresses](anomaly-detection-policy#activity-from-anonymous-ip-addresses)[Activity from infrequent country](anomaly-detection-policy#activity-from-infrequent-country)[Activity from suspicious IP addresses](anomaly-detection-policy#activity-from-suspicious-ip-addresses)[Impossible travel](anomaly-detection-policy#impossible-travel)[Multiple failed login attempts](anomaly-detection-policy#multiple-failed-login-attempts)[Ransomware detection](anomaly-detection-policy#ransomware-activity)[Unusual administrative activities](anomaly-detection-policy#unusual-activities-by-user) |
| Activity policy template | Logon from a risky IP address |

For more information about creating policies, see [Create a policy](control-cloud-apps-with-policies#create-a-policy).

## Automate governance controls

Currently, there are no governance controls available for Okta. If you're interested in having governance actions for this connector, you can [contact Microsoft Defender support](/en-us/defender-xdr/contact-defender-support) with details of the actions you want.

For more information about remediating threats from apps, see [Governing connected apps](governance-actions).

## Protect Okta in real time

Review our best practices for [securing and collaborating with external users](best-practices#secure-collaboration-with-external-users-by-enforcing-real-time-session-controls) and [blocking and protecting the download of sensitive data to unmanaged or risky devices](best-practices#block-and-protect-download-of-sensitive-data-to-unmanaged-or-risky-devices).

## Prerequisites

To connect Okta to Defender for Cloud Apps:

- Create an Okta admin service account dedicated to Defender for Cloud Apps. You use this account to generate the API token required for the connector.
- Make sure you use an account with Super Admin permissions.
- Make sure your Okta account is verified.

## Connect Okta to Microsoft Defender for Cloud Apps

The following procedure provides instructions for connecting Microsoft Defender for Cloud Apps to your existing Okta account using the connector APIs. This connection gives you visibility into and control over Okta use. For information about how Defender for Cloud Apps protects Okta, see [Protect Okta](protect-okta).

Use this app connector to access SaaS Security Posture Management (SSPM) features, via security controls reflected in Microsoft Secure Score. [Learn more](/en-us/microsoft-365/security/defender/microsoft-secure-score).

### Configure Okta

In the Okta console, create a token for the API. Copy the token value. You will need the token value later.

### Configure Defender for Cloud Apps

Perform the following steps in Defender for Cloud Apps to complete the Okta connection:

1. In the Microsoft Defender Portal, select **Settings** &gt; **Cloud Apps**.
2. Under **Connected apps**, select **App Connectors**.
3. In the **App connectors page**, select **+Connect an app**, and then **Okta**.

    ![Screenshot of the App connectors page with the Connect Okta option.](media/connect-okta.png)
4. In the next window, give your connection a name and select **Next**.
5. In the **Enter details** window, in the **Domain** field, enter your Okta domain and paste your Token into the **Token** field.
6. Select **Submit** to create the token for Okta in Defender for Cloud Apps.
7. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**. Make sure the status of the connected App Connector is **Connected**.

After connecting Okta, you'll receive events for seven days prior to connection.