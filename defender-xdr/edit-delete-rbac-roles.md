---
layout: Conceptual
title: Edit or delete roles in Microsoft Defender unified role-based access control (RBAC) - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/edit-delete-rbac-roles
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Edit or delete roles in Microsoft Defender Security portal experiences using role-based access control (RBAC)
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.custom: msecd-doc-authoring-1016
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.reviewer: 
ai-usage: ai-assisted
locale: en-us
document_id: 00b109a2-0ec8-c6ec-54ff-3e1e4c549b28
document_version_independent_id: 00b109a2-0ec8-c6ec-54ff-3e1e4c549b28
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/edit-delete-rbac-roles.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: edit-delete-rbac-roles
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/edit-delete-rbac-roles.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 1483b10c-4f49-c85e-2e4a-8d466c995665
---

# Edit or delete roles in Microsoft Defender unified role-based access control (RBAC) - Microsoft Defender XDR | Microsoft Learn

This article walks you through how to edit, delete, and export roles in Microsoft Defender unified role-based access control (RBAC). These tasks apply to custom roles you created in unified RBAC and roles imported from Defender for Endpoint, Defender for Identity, or Defender for Office 365. Each section lists the required permissions before the steps.

## Edit roles

To edit roles in Microsoft Defender unified RBAC, follow these steps:

Important

You must be a Security Administrator or higher in Microsoft Entra ID. You can also perform this task if you have all Authorization permissions in Microsoft Defender Unified RBAC. For more information, see [Permission prerequisites](manage-rbac#permissions-prerequisites).

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com) as security administrator or higher.
2. In the navigation pane, select **Permissions**.
3. Select **Roles** under Microsoft Defender XDR to get to the **Permissions and roles** page.
4. Select the role you want to edit. You can only edit one role at a time.
5. Once selected, a flyout pane opens where you can edit the role:

    [![Screenshot of the edit roles flyout page](media/edit-delete-rbac-roles/m365-defender-rbac-edit-roles.png)](media/edit-delete-rbac-roles/m365-defender-rbac-edit-roles.png#lightbox)

Note

After editing an imported role, the changes made in Microsoft Defender unified RBAC will not be reflected back in the individual product RBAC model.

## Delete roles

To delete roles in Microsoft Defender unified RBAC:

1. Select the role or roles you want to delete.
2. Select **Delete roles**.

Warning

If a Microsoft Defender workload that uses the role is active, deleting the role also removes all assigned user permissions.

Note

When an an imported role is deleted, the role isn't deleted from the individual product RBAC model. If needed, you can reimport it to the Microsoft Defender unified RBAC list of roles.

## Export roles

Important

Starting in 2025, Microsoft Defender unified RBAC is the default model for new Defender for Endpoint and Defender for Identity tenants. These tenants can't export roles from the old model. Tenants that had roles assigned or exported before 2025 keep their old roles setup.

The Export feature lets you export the following role data:

- Role name
- Role description
- Permissions in the role
- Assignment name
- Assigned data sources
- Assigned users or user groups

When a role has multiple assignments, each assignment appears as a separate row in the CSV file.

The CSV also includes the Defender unified RBAC activation status for each workload on the tenant.

To export roles in Microsoft Defender unified RBAC, follow these steps:

Note

To export roles, you must be a Security Administrator or higher in Microsoft Entra ID. Or, you must have the **Authorization (manage)** permission for all data sources in Microsoft Defender Unified RBAC and at least one workload activated.

For more information, see [Permission prerequisites](manage-rbac#permissions-prerequisites).

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com) with the required roles or permissions.
2. In the navigation pane, select **Permissions**.
3. Select **Roles** under Microsoft Defender XDR to get to the Permissions and roles page.
4. Select the **Export** button.

    [![Screenshot of the export roles page](media/edit-delete-rbac-roles/m365-defender-rbac-export-roles.png)](media/edit-delete-rbac-roles/m365-defender-rbac-export-roles.png#lightbox)

A CSV file containing all the roles data is generated and downloaded to the local computer.