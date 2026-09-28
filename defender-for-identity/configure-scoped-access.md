---
layout: Conceptual
title: Configure scoped access for Microsoft Defender for Identity - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/configure-scoped-access
feedback_system: Standard
feedback_product_url: https://aka.ms/MDIcommunity
breadcrumb_path: /azure-advanced-threat-protection/bread/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: microsoft-defender-for-identity
uhfHeaderId: MSDocsHeader-MicrosoftDefender
ms.suite: ems
description: Configure scoped access in Microsoft Defender for Identity by creating custom unified RBAC roles that limit visibility to specific Active Directory domains or organizational units.
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ms. reviewer: LiorShapiraa
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 9b70182d-d14a-ae89-79ca-8eaa584b241d
document_version_independent_id: 9b70182d-d14a-ae89-79ca-8eaa584b241d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/configure-scoped-access.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-scoped-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/configure-scoped-access.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: 6a4c467d-55db-96ec-3f6e-73274c4ec8e1
---

# Configure scoped access for Microsoft Defender for Identity - Microsoft Defender for Identity | Microsoft Learn

## Overview

As your organization grows, you need to control who can access which resources. Microsoft Defender for Identity scoping lets you focus monitoring on specific Active Directory domains or organizational units. Scoping reduces noise from data you don't need and helps you focus on critical assets. You can also limit visibility to specific entities so that access matches each person's role. To set up scoped access, [create a custom role using Microsoft Defender unified RBAC](/en-us/defender-xdr/create-custom-rbac-roles). When you configure the role, you choose which users or Entra ID groups can access specific Active Directory domains or organizational units.

## Prerequisites

Before you begin, make sure you meet the following requirements:

- A Microsoft Defender for Identity sensor is installed.
- The [Identity workload in Microsoft Defender unified RBAC](/en-us/defender-xdr/activate-defender-rbac#activate-from-the-permissions-and-roles-page) is turned on.
- You have the [Security Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference) role in Microsoft Entra ID.
- Authorization permissions are set up through [URBAC](/en-us/defender-xdr/manage-rbac) if you want to manage roles without the Security Administrator role.

### Configure scoping rules

To enable identity scoping, follow these steps:​

1. Navigate to **Permissions &gt; Microsoft Defender XDR &gt; Roles​**.

    ![Screenshot showing the roles page in the Microsoft Defender portal.](media/custom-roles/permissions-roles.png)
2. Select **+ Create custom role** and follow the instructions in [Create custom roles with Microsoft Defender unified RBAC.](/en-us/defender-xdr/create-custom-rbac-roles#create-a-custom-role)

    ![Screenshot showing the create custom roles button.](media/custom-roles/create-custom-role.png)
3. You can edit the role at any time. Select the role from the list of custom roles and choose **Edit**.

    ![Screenshot showing how to edit a custom role.](media/custom-roles/edit-custom-role.png)
4. Select Add assignments and add the Assignment name.

    1. Under **Assign users and groups**, enter the usernames or Microsoft Entra ID groups you want to assign to the role.
    2. Select Microsoft Defender for Identity as the data source.
    3. Under **Scope**, select the user groups (AD domains or OU's) that will be scoped to the assignment. For an optimal experience, use the filter or search box. ![Screenshot of the scoped assignment page with a user group selected for the assignment.](media/configure-scoped-access/add-scope.png)

    ![Screenshot of the custom scope creation page with options for defining a custom scope.](media/configure-scoped-access/custom-scope.png)
5. Select **Apply** and **Add**.

### Known limitations

The following table lists the current limitations and supported scenarios for scoped access in Microsoft Defender for Identity.

Note

- Custom roles apply only to new alerts and activities. Alerts and activities triggered before a custom role was created aren't retroactively tagged or filtered.
- The Exposure Management section in the Defender Portal is not visible to users with an MDI scope assignment.
- Microsoft Entra ID IP alerts aren't included within scoped MDI detections.

| Defender for Identity experience | Scoping by OU's | Scoping by AD domain |
| --- | --- | --- |
| MDI alerts and incidents | Available | Available |
| Hunting tables: AlertEvidence+Info, IdentityInfo, IdentityDirectoryEvents, IdentityLogonEvents, IdentityQueryEvents | Available | Available |
| User page and user global search | Available | Available |
| MDI alerts based on XDR detection platform (detection source is XDR and service source is MDI) | Available | Available |
| Health issues | Unavailable | Available |
| Identities inventory and service accounts discovery page | Available | Available |
| Identities settings: manual tagging | Available | Available |
| Identities settings: sensors page, health issues notifications | Unavailable | Available |
| Defender XDR Incident email notifications | Available | Unavailable |
| ISPMs and exposure management | Unavailable | Unavailable |
| Download scheduled reports and Graph API | Unavailable | Unavailable |
| Device and group global search and entity page | Available | Available |
| Alert tuning and critical asset management | Unavailable | Unavailable |

### Related articles

- [Microsoft Defender for Identity role groups](role-groups)
- [Microsoft Defender unified role-based access control (RBAC)](/en-us/defender-xdr/manage-rbac)
- [Create custom roles with Microsoft Defender unified RBAC](/en-us/defender-xdr/create-custom-rbac-roles)
- [Import roles to Microsoft Defender unified role-based access control (RBAC)](/en-us/defender-xdr/import-rbac-roles)
- [Activate Microsoft Defender unified role-based access control (RBAC)](/en-us/defender-xdr/activate-defender-rbac)