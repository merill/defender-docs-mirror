---
layout: Conceptual
title: Non-human identities in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/investigate-non-human-identities
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about non-human identities in Microsoft Defender, including OAuth apps, service accounts, SaaS apps, identity types, and how to investigate them.
ms.author: andeshpande
author: anandd512
ms.reviewer: maelgami
ms.date: 2026-09-28T00:00:00.0000000Z
ms.topic: concept-article
ms.service: microsoft-defender-for-identity
ms.custom: msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 06529557-eb8b-ea52-899c-e46895927a54
document_version_independent_id: 06529557-eb8b-ea52-899c-e46895927a54
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/investigate-non-human-identities.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: investigate-non-human-identities
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/investigate-non-human-identities.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 26953eb8-54e0-211a-5cea-41e5afc496b6
---

# Non-human identities in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn

Non-human identities are accounts and applications that operate without direct human interaction. In Microsoft Defender, non-human identities include service principals registered in Microsoft Entra ID, Active Directory service accounts, and OAuth apps connected to Google Workspace and Salesforce. These identities often have elevated privileges and access to sensitive resources, which makes them a priority for security monitoring.

You can view and investigate non-human identities from the [Identity inventory](/en-us/defender-for-identity/identity-inventory) in the Microsoft Defender portal.

![Screenshot that shows the non-human identities page in the Defender portal.](media/investigate-non-human-identities/non-human-identities.png)

## Actionable insights

Actionable insights appear at the top of the non-human identities inventory. Select an insight to filter the list to identities that need review.

| Insight | Description | Available for |
| --- | --- | --- |
| **New identities** | Identities added in the last 30 days. | Microsoft 365 |
| **Highly privileged identities** | Identities with powerful permissions that allow them to access data or change important settings. For Salesforce, includes Connected Apps and External Client Apps (ECAs) whose granted permissions are classified as **High**. | Microsoft 365, Google Workspace, Salesforce |
| **Risky identities** | Identities with a high risk score. | Microsoft 365, Google Workspace, Salesforce |
| **Unused identities** | Identities that haven't signed in within the last 90 days. For Salesforce, includes Connected Apps and ECAs that haven't been used for more than 90 days based on the last used date. | Microsoft 365, Google Workspace, Salesforce |
| **Overprivileged identities** | Identities with unused permissions. | Microsoft 365 |
| **Identities from external unverified publishers** | Identities that originated from an external unverified publisher tenant. | Microsoft 365 |
| **Used by AI Agents** | Identities identified as being used by AI agent platforms. | Microsoft 365 |

## Types of non-human identities

Microsoft Defender organizes non-human identities into the following categories, each shown as a tab in the identity inventory:

- **Entra ID**: Service principals registered in Microsoft Entra ID. These apps authenticate using OAuth and access resources through Microsoft Graph and other APIs.
- **Active Directory**: Service accounts from on-premises Active Directory. These specialized accounts run applications, services, and automated tasks, and often have elevated privileges.
- **Google Workspace**: OAuth apps connected through Google Workspace. Users authorize these apps, which have varying levels of access to Google Workspace resources.
- **Salesforce**: OAuth apps connected through Salesforce. The inventory includes both Connected Apps and External Client Apps (ECAs).

## Investigate identity details

Each identity type shows different columns, filters, and detail tabs in the inventory. For information about inventory fields and identity details, see the following articles:

- **Entra ID, Google Workspace, and Salesforce OAuth apps**: For inventory columns, filtering options, and identity details, see [View your app details with app governance](/en-us/defender-cloud-apps/app-governance-visibility-insights-view-apps).
- **Active Directory service accounts**: For inventory columns, connections, and classification rules, see [Investigate and protect Service Accounts](/en-us/defender-for-identity/service-account-discovery).