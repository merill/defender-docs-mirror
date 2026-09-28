---
layout: Conceptual
title: Protect your Azure environment - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/protect-azure
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
description: Learn how to connect your Azure environment to Microsoft Defender for Cloud Apps using the API connector to monitor activities and detect threats.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: AmitMishaeli
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 2a2f1b2b-fe97-e646-2718-1206aa39fe92
document_version_independent_id: 2a2f1b2b-fe97-e646-2718-1206aa39fe92
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/protect-azure.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: protect-azure
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/protect-azure.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
platformId: 7b691ee1-049b-d56e-051e-f3f2a03dbe34
---

# Protect your Azure environment - Microsoft Defender for Cloud Apps | Microsoft Learn

Azure is a cloud provider that lets your organization host and manage its workloads. Cloud hosting has many benefits, but it can also expose critical assets to threats. These assets include storage with sensitive data, compute resources that run key apps, ports, and virtual private networks.

When you connect Azure to Defender for Cloud Apps, you can secure your assets and spot threats. The service monitors admin and sign-in activity. It alerts you to brute force attacks, misuse of privileged accounts, and unusual VM deletions.

## Main threats

The main threats to your Azure environment include:

- Abuse of cloud resources
- Compromised accounts and insider threats
- Data leakage
- Resource misconfiguration and insufficient access control

## How Defender for Cloud Apps helps to protect your environment

Use the following best practices to protect your Azure environment with Defender for Cloud Apps:

- [Detect cloud threats, compromised accounts, and malicious insiders](best-practices#detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware)
- [Limit exposure of shared data and enforce collaboration policies](best-practices#limit-exposure-of-shared-data-and-enforce-collaboration-policies)
- [Use the audit trail of activities for forensic investigations](best-practices#use-the-audit-trail-of-activities-for-forensic-investigations)

## Control Azure with built-in policies and policy templates

You can use the following built-in policy templates to detect and notify you about potential threats:

| Type | Name |
| --- | --- |
| Built-in anomaly detection policy | [Activity from anonymous IP addresses](anomaly-detection-policy#activity-from-anonymous-ip-addresses)[Activity from infrequent country](anomaly-detection-policy#activity-from-infrequent-country)[Activity from suspicious IP addresses](anomaly-detection-policy#activity-from-suspicious-ip-addresses)[Activity performed by terminated user](anomaly-detection-policy#activity-performed-by-terminated-user) (requires Microsoft Entra ID as IdP)[Multiple failed login attempts](anomaly-detection-policy#multiple-failed-login-attempts)[Unusual administrative activities](anomaly-detection-policy#unusual-activities-by-user) |

For more information about creating policies, see [Create a policy](control-cloud-apps-with-policies#create-a-policy).

## Automate governance controls

You can also automate Azure governance actions to fix detected threats. The following table lists the available actions:

| Type | Action |
| --- | --- |
| User governance | - Notify user on alert (via Microsoft Entra ID)- Require user to sign in again (via Microsoft Entra ID)- Suspend user (via Microsoft Entra ID) |

For more information about remediating threats from apps, see [Governing connected apps](governance-actions).

## Protect Azure in real time

Review best practices for [securing and collaborating with guests](best-practices#secure-collaboration-with-external-users-by-enforcing-real-time-session-controls) and [blocking and protecting the download of sensitive data to unmanaged or risky devices](best-practices#block-and-protect-download-of-sensitive-data-to-unmanaged-or-risky-devices).

## Connect Azure to Microsoft Defender for Cloud Apps

Use the app connector API to connect your Azure account to Defender for Cloud Apps. This connection gives you visibility into and control over Azure use. To learn how Defender for Cloud Apps protects Azure, see [Protect Azure](protect-azure).

### Prerequisites

Before you connect Azure to Microsoft Defender for Cloud Apps, make sure that the user connecting Azure has the **Security administrator** role in Azure Active Directory.

- The user connecting Azure must have a **Security administrator** role in Azure Active Directory.

### Scope and limitations

When you connect Azure to Defender for Cloud Apps, keep in mind the following scope and limitations:

> 
> - Defender for Cloud Apps displays activities from **all** subscriptions.
> - User account information is populated in Defender for Cloud Apps as users perform activities in Azure.
> - Defender for Cloud Apps monitors ARM activities only.
> 

### Connect Azure to Defender for Cloud Apps

To connect Azure to Defender for Cloud Apps, follow these steps:

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**.
2. In the **App connectors** page, select **+Connect an app**, followed by **Microsoft Azure**.

    ![Screenshot that shows the Azure connector in the Defender portal.](media/connect-azure-menu.png)
3. In the **Connect Microsoft Azure** page, select **Connect Microsoft Azure**.

    ![Screenshot that shows the Connect Microsoft Azure page in the Defender portal.](media/connect-azure.png)
4. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**. Make sure the status of the connected App Connector is **Connected**.

Note

After the Azure connection is established, Defender for Cloud Apps pulls data from that point forward.