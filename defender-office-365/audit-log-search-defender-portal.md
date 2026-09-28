---
layout: Conceptual
title: Audit log search in the Microsoft Defender portal - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/audit-log-search-defender-portal
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: how-to
ms.collection:
- m365-security
- tier2
ms.localizationpriority: medium
ms.assetid: 
ms.custom:
- msecd-doc-authoring-1016
- seo-marvel-apr2020
- sfi-ga-nochange
description: Admins can use the Audit page in the Microsoft Defender portal to search the unified audit log for user and admin actions in the organization.
ms.service: defender-office-365
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 216dd28a-093b-dfe1-3f13-b17e456da031
document_version_independent_id: 216dd28a-093b-dfe1-3f13-b17e456da031
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/audit-log-search-defender-portal.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: audit-log-search-defender-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/audit-log-search-defender-portal.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
platformId: 06cabb9d-08a0-8322-db54-556cffad7aa9
---

# Audit log search in the Microsoft Defender portal - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

## Overview

In all organizations with cloud mailboxes, the unified audit log records supported user and admin operations. Audit records for these events are searchable by security ops, IT admins, insider risk teams, and compliance and legal investigators in the organization. This capability provides visibility into the activities performed across your Microsoft 365 organization.

This article describes how to open and start an audit log search in the Microsoft Defender portal, including the required permissions and links to detailed search instructions. Before you begin, review the prerequisites to verify that you have the necessary permissions.

Tip

Audit log search in Microsoft Defender portal is identical to audit log search in the Microsoft Purview portal at https://purview.microsoft.com/auditlogsearch.

## What do you need to know before you begin?

Review the following prerequisites before you search the audit log.

- You need to be assigned permissions before you can do the procedures in this article. You have the following options:
    - [Exchange Online permissions](/en-us/exchange/permissions-exo/permissions-exo): Membership in the **Organization Management** or **Compliance Management** role groups.
    - [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): Membership in the **Global Administrator**^\*^ or **Compliance Administrator** roles gives users the required permissions *and* permissions for other features in Microsoft 365.

        Important

        ^\*^ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.

## Open audit log search

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Audit**. Or, to go directly to the **Audit** page, use https://security.microsoft.com/auditlogsearch.
2. On the **Audit** page, create the audit log search. For instructions, see [Audit New Search](/en-us/purview/audit-new-search) or [Use a PowerShell script to search the audit log](/en-us/purview/audit-log-search-script).