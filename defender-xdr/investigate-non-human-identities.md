---
layout: Conceptual
title: Non-human identities in Microsoft Defender (Preview) - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/investigate-non-human-identities
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about non-human identities in Microsoft Defender, including OAuth apps, service accounts, and SaaS apps. Understand identity types and where to investigate them.
ms.author: abbyweisberg
author: AbbyMSFT
ms.reviewer: maelgami
ms.date: 2026-03-17T00:00:00.0000000Z
ms.topic: concept-article
ms.service: microsoft-defender-for-identity
ms.custom: msecd-doc-authoring-106
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
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: 26953eb8-54e0-211a-5cea-41e5afc496b6
---

# Non-human identities in Microsoft Defender (Preview) - Microsoft Defender XDR | Microsoft Learn

Non-human identities are accounts and applications that operate without direct human interaction. In Microsoft Defender, non-human identities include service principals registered in Microsoft Entra ID, Active Directory service accounts, and OAuth apps connected to Google Workspace and Salesforce. These identities often have elevated privileges and access to sensitive resources, which makes them a priority for security monitoring.

You can view and investigate non-human identities from the [Identity inventory](/en-us/defender-for-identity/identity-inventory) in the Microsoft Defender portal.

![Screenshot that shows the non-human identities page in the Defender portal.](media/investigate-non-human-identities/non-human-identities.png)

## Types of non-human identities

Microsoft Defender organizes non-human identities into the following categories, each shown as a tab in the identity inventory:

- **Entra ID**: Service principals registered in Microsoft Entra ID. These apps authenticate using OAuth and access resources through Microsoft Graph and other APIs.
- **Active Directory**: Service accounts from on-premises Active Directory. These specialized accounts run applications, services, and automated tasks, and often have elevated privileges.
- **Google Workspace**: OAuth apps connected through Google Workspace. Users authorize these apps, which have varying levels of access to Google Workspace resources.
- **Salesforce**: OAuth apps connected through Salesforce. Users authorize these apps to access Salesforce data and resources.

## Investigate identity details

Each identity type shows different columns, filters, and detail tabs in the inventory. For information about inventory fields and identity details, see the following articles:

- **Entra ID, Google Workspace, and Salesforce OAuth apps**: For inventory columns, filtering options, and identity details, see [View your app details with app governance](/en-us/defender-cloud-apps/app-governance-visibility-insights-view-apps).
- **Active Directory service accounts**: For inventory columns, connections, and classification rules, see [Investigate and protect Service Accounts](/en-us/defender-for-identity/service-account-discovery).