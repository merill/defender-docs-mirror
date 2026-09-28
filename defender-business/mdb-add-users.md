---
layout: Conceptual
title: Add users and assign licenses in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-business/mdb-add-users
breadcrumb_path: /defender-business/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Add users, assign Microsoft Defender for Business licenses, and verify that multifactor authentication (MFA) is enabled to help protect devices.
author: chrisda
ms.author: chrisda
ms.topic: how-to
ms.service: defender-business
ms.localizationpriority: medium
ms.date: 2026-07-03T00:00:00.0000000Z
ms.collection:
- m365-security
- tier1
ms.reviewer: efratka
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 08fb7df3-bb21-a778-7bf4-908cbbbaad30
document_version_independent_id: 08fb7df3-bb21-a778-7bf4-908cbbbaad30
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-business/mdb-add-users.md
site_name: Docs
depot_name: Learn.defender-business
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdb-add-users
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-business/mdb-add-users.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b11ae577-8d18-47ab-998c-ea182a941e71
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/87b1d24d-826d-4337-90a0-b6c35e4561f2
platformId: 5cb20694-4458-a0a2-4b1e-1783d82e6154
---

# Add users and assign licenses in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn

After you sign up for Microsoft Defender for Business, your first step is to add users and assign licenses. This article describes how to add users and assign licenses, and how to verify multifactor authentication (MFA) is enabled for users.

![Visual depicting step 2 - add users and assign licenses in Defender for Business.](media/mdb-setup-step2.png)

## Add users and assign licenses in the Microsoft 365 admin center

For complete instructions, see [Add users and assign licenses at the same time](/en-us/microsoft-365/admin/add-users/add-users).

## Verify MFA is enabled for users

All organizations created after October 2019 have *security defaults* enabled by default, which requires MFA for all users. For more information, see [Multifactor authentication for Microsoft 365](/en-us/microsoft-365/admin/security-and-compliance/multi-factor-authentication-microsoft-365).

To verify that security defaults is enabled in your organization, see [Set up multifactor authentication for Microsoft 365](/en-us/microsoft-365/admin/security-and-compliance/set-up-multi-factor-authentication).

Tip

Organizations with Microsoft Entra ID P1 (for example, Microsoft 365 Business Premium or an add-on subscription) also have access to Conditional Access to enforce MFA and other security requirements. For more information, see [Multifactor authentication for Microsoft 365](/en-us/microsoft-365/admin/security-and-compliance/multi-factor-authentication-microsoft-365). If you don't have any licenses available, you can still add a user and buy additional licenses. For more information about adding users, see [Add users and assign licenses at the same time](/en-us/Microsoft-365/admin/add-users/add-users).