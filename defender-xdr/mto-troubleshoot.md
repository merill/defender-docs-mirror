---
layout: Conceptual
title: Troubleshoot issues in Microsoft Defender multitenant management - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/mto-troubleshoot
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about issues in Microsoft Defender multitenant management and how to fix or troubleshoot them.
ms.service: defender-xdr
author: guywi-ms
ms.author: guywild
ms.collection:
- m365-security
- highpri
- tier1
- usx-security
ms.topic: concept-article
ms.date: 2025-03-31T00:00:00.0000000Z
locale: en-us
document_id: 848ecb03-06e2-3b14-494a-25eb9fbabfc8
document_version_independent_id: 848ecb03-06e2-3b14-494a-25eb9fbabfc8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/mto-troubleshoot.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mto-troubleshoot
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/mto-troubleshoot.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 433837b1-c1af-cb1a-906a-0773ea28cf03
---

# Troubleshoot issues in Microsoft Defender multitenant management - Microsoft Defender XDR | Microsoft Learn

This article addresses potential issues that might arise as you use the multitenant management in Microsoft Defender. It provides guidance on how to troubleshoot these issues.

## Problem adding or removing tenants

When adding or removing tenants, you might encounter errors like the following:

![Screenshot of error message while adding a tenant](media/mto-troubleshoot/add-tenants-error-small.png)

[![Screenshot of error message while removing a tenant](media/mto-troubleshoot/remove-tenants-error-small.png)](media/mto-troubleshoot/remove-tenants-error.png#lightbox)

The issue is resolved by refreshing the page and trying again.

## Some tenants are missing from the list

When loading the tenant list on the Settings page, you get the following error message:

[![Screenshot of error message where only some of the tenants are correctly loaded on the page](media/mto-troubleshoot/partial-tenants-error-small.png)](media/mto-troubleshoot/partial-tenants-error.png#lightbox)

The issue is due to [conditional access policy](/en-us/entra/identity/conditional-access/overview) requiring multifactor authentication (MFA) on your Azure Resource Manager app.

To resolve this issue, add *Microsoft 365 Security and Compliance Center app (80ccca67-54bd-44ab-8625-4b79c4dc7775)* to the same conditional access policy as your Azure Resource Manager app. This mitigation applies MFA on the origin tenant when a user tries to sign in to the Microsoft Defender portal.

Here’s an example of the policy setting in the Microsoft Entra admin center.

[![Screenshot of a conditional access policy settings page](media/mto-troubleshoot/ca-policy-small.png)](media/mto-troubleshoot/ca-policy.png#lightbox)

## Content assignment failure in cross-cloud tenant management

You see the following error when assigning content to distribution profiles:

[![Screenshot of permissions error when assigning content to tenants](media/mto-troubleshoot/tenant-perms-error.png)](media/mto-troubleshoot/tenant-perms-error.png#lightbox)

When a cross-cloud tenant is added to a distribution profile and subsequently removed from cross-cloud visibility, the tenant's name is removed from the tenant list and won't be available for content management, which causes the error. This is a recognized limitation of cross-cloud tenant management and is currently under review.