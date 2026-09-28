---
layout: Conceptual
title: Create and manage tenant groups in Microsoft Defender multitenant management - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/mto-tenant-groups
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to create tenant groups and switch the multitenant view between groups in the Microsoft Defender portal.
ms.service: defender-xdr
author: mberdugo
ms.author: monaberdugo
ms.reviewer: soulisabag
ms.collection:
- m365-security
- tier1
- usx-security
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: eb457a05-61bc-c90c-948b-1bde69c191fc
document_version_independent_id: eb457a05-61bc-c90c-948b-1bde69c191fc
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/mto-tenant-groups.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mto-tenant-groups
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/mto-tenant-groups.md
platformId: e45afa21-f2dc-0dd5-ffbf-c125257fc43e
---

# Create and manage tenant groups in Microsoft Defender multitenant management - Microsoft Defender XDR | Microsoft Learn

Tenant groups in Microsoft Defender multitenant management let you organize the tenants you manage into named collections and switch the multitenant view between them. Use tenant groups to focus on a specific set of tenants, such as those that belong to a single customer, business unit, or geographic region, instead of viewing every tenant you have access to at once.

Note

The previous use of *tenant groups* for content distribution is now called [content distribution using distribution profiles](mto-distribution-profiles). The name *tenant groups* now refers to the groups of tenants you create to switch the multitenant view, as described in this article.

## Prerequisites

Before you create tenant groups, onboard your tenants to the Microsoft Defender multitenant portal. Only onboarded tenants appear when you create or edit a group.

For setup steps, see [Set up Microsoft Defender multitenant management](mto-requirements). To manage tenants, see [Manage tenants with Microsoft Defender multitenant management](mto-tenants).

## Required permissions

To access tenant groups, you need the following permissions.

**Microsoft Entra ID roles**

- [Security Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator)
- [Security Operator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-operator)

**Product-specific RBAC (for example, Microsoft Defender for Endpoint or Microsoft Defender for Identity)**

- [Security Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator)
- Custom RBAC roles with access across products. For details, see [Custom roles for role-based access control](/en-us/defender-xdr/custom-roles).

**[Unified role-based access control (URBAC)](/en-us/defender-xdr/manage-rbac)**

- *Security / read* to view tenant groups
- *Security / manage* to create tenant groups

To learn more about URBAC permissions, see [Manage unified role-based access control (URBAC) for multitenant management](mto-urbac).

Users only see tenants they have access to through B2B or [granular delegated admin privileges (GDAP)](/en-us/partner-center/gdap-introduction). A tenant group can include tenants that a user can't see.

## Access tenant groups

To access tenant groups, follow these steps:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com) with appropriate administrative credentials.
2. Go to **Multi-tenant management** &gt; **Tenant groups**.

The first time you open the **Tenant groups** page, you see **My private group**, which contains all tenants from your previous multitenant settings. You can add or remove tenants from **My private group**, but you can't delete it.

## Create a tenant group

To create a tenant group, follow these steps:

1. On the **Tenant groups** page, select **+ Create tenant group**.
2. Enter a descriptive name for the tenant group.
3. Optionally, enter a description.
4. Select the tenants you want to add to the group.
5. Select **Create**.

## Switch the view between tenant groups

To switch the multitenant view to a different tenant group, follow these steps:

1. In the top-left corner of the multitenant portal, select **Open multitenant management**.
2. Select the tenant group you want to view.

    [![Screenshot of the Multi-tenant view settings page in the Microsoft Defender portal, with the Open multitenant management icon highlighted in the top-right corner.](media/mto-tenant-groups/multitenant-view-settings.png)](media/mto-tenant-groups/multitenant-view-settings.png#lightbox)

After you switch groups, check that the portal shows data only from tenants in that group.

If someone changes the group while you have it open, the portal shows a notice. Refresh to load the new data.

![Screenshot of the Group changes detected dialog with Refresh and reload and Cancel buttons.](media/mto-tenant-groups/group-changes-detected.png)

## Edit a tenant group

To edit a tenant group, follow these steps:

1. Go to **Multi-tenant management** &gt; **Tenant groups**.
2. Select the tenant group you want to change, and then select **Edit**.
3. Add or remove tenants as needed, and then save your changes.
4. Switch the view to the edited tenant group to confirm the data reflects the updated membership.