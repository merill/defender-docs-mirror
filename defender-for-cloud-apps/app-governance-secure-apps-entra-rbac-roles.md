---
layout: Conceptual
title: Secure OAuth apps with Microsoft Entra RBAC roles - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/app-governance-secure-apps-entra-rbac-roles
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: anandd512
manager: bagol
ms.author: andeshpande
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: Learn how to use app governance to identify and investigate Microsoft Entra roles assigned directly to service principals and assess privilege risk.
ms.topic: how-to
ms.reviewer: anandd512
ms.date: 2026-09-28T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1016
ai-usage: ai-generated
locale: en-us
document_id: b91fa801-9944-8c22-3313-49e575710af0
document_version_independent_id: b91fa801-9944-8c22-3313-49e575710af0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/app-governance-secure-apps-entra-rbac-roles.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: app-governance-secure-apps-entra-rbac-roles
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/app-governance-secure-apps-entra-rbac-roles.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 86859de8-a372-2588-e906-350f50210f9b
---

# Secure OAuth apps with Microsoft Entra RBAC roles - Microsoft Defender for Cloud Apps | Microsoft Learn

Microsoft Entra role assignments can give service principals broad access to Microsoft 365 resources. Use app governance to find role-assigned apps and inspect their role permissions and risk.

Before you begin, make sure your account has access to app governance data.

## Prerequisites

Your sign-in account must have one of the [required app governance roles](app-governance-get-started#roles) to view app governance data.

## Overview

Microsoft Entra service principals can access Microsoft 365 resources through API permissions or through Microsoft Entra role-based access control (RBAC) roles that are assigned directly to the service principal. App governance provides visibility into these role assignments so security teams can identify service principals with privileged roles and review their risk.

Note

Currently, app governance includes built-in and custom Microsoft Entra directory roles that are assigned directly to a service principal. Azure RBAC roles and roles inherited through group membership aren't included.

Role-based signals contribute to the service principal's privilege level and risk score.

## Identify apps with Microsoft Entra roles

Use the **Roles** filter to find service principals with specific built-in Microsoft Entra role assignments:

1. In the [Microsoft Defender portal](https://security.microsoft.com), go to **Assets** &gt; **Identities**.
2. Select the **Non-human identities** tab, and then select **Entra ID**.
3. Open the **Roles** filter.
4. Search for and select one or more built-in Microsoft Entra roles.
5. Select **Apply**.

[![Screenshot of the Roles filter in the non-human identities inventory.](media/app-governance-secure-apps-entra-rbac-roles/roles-filter.png)](media/app-governance-secure-apps-entra-rbac-roles/roles-filter.png#lightbox)

The **Permission type** column and filter show how each service principal accesses resources. The available values are:

- **Delegated**: The app has delegated API permissions.
- **Application**: The app has application API permissions.
- **Microsoft Entra roles**: The app has Microsoft Entra roles and no API permissions.
- **Mixed**: The app has more than one access type.
- **None**: The app has no API permissions or Microsoft Entra role assignments.

## View roles assigned to an app

To review the Microsoft Entra roles assigned to a service principal, follow these steps:

1. Select a service principal in the inventory.
2. In the details pane, select the **Permissions** tab.
3. Expand **Microsoft Entra roles**.
4. Review each role's name, privilege level, and role type.
5. Select a role to view the permission actions that make up the role, including each action's description and privilege level.

[![Screenshot of Microsoft Entra role assignments on the Permissions tab for a non-human identity.](media/app-governance-secure-apps-entra-rbac-roles/role-details.png)](media/app-governance-secure-apps-entra-rbac-roles/role-details.png#lightbox)

The summary shows the total number of assigned roles. It also shows the app's total permissions, privileged permissions, and unused permissions.

Note

Microsoft Entra role information is also available in the `AssignedRoles` column of the [`OAuthAppInfo` table in advanced hunting](/en-us/defender-xdr/advanced-hunting-oauthappinfo-table) for investigations and custom detections.