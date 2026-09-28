---
layout: Conceptual
title: Microsoft Defender unified role-based access control (RBAC) - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/manage-rbac
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Manage permissions and access to the Microsoft Defender portal experiences using unified role-based access control (RBAC).
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.custom:
- sfi-ga-nochange
ms.topic: overview
ms.date: 2026-08-07T00:00:00.0000000Z
ms.reviewer: Tomas Beerthuis
locale: en-us
document_id: 052939e2-4006-5dea-3d5f-1af95fd5b448
document_version_independent_id: 052939e2-4006-5dea-3d5f-1af95fd5b448
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/manage-rbac.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: manage-rbac
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/manage-rbac.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 017c3947-c12b-57c7-78e3-e49580098012
---

# Microsoft Defender unified role-based access control (RBAC) - Microsoft Defender XDR | Microsoft Learn

**Applies to:**

- [Microsoft Defender for Endpoint Plan 2](/en-us/defender-endpoint/microsoft-defender-endpoint)
- [Microsoft Defender XDR](microsoft-365-defender)
- [Microsoft Defender for Identity](https://go.microsoft.com/fwlink/?LinkID=2198108)
- [Microsoft Defender for Office 365 P2](https://go.microsoft.com/fwlink/?LinkID=2158212)
- [Microsoft Defender Vulnerability Management](/en-us/defender-vulnerability-management/defender-vulnerability-management)
- [Microsoft Defender for Cloud](/en-us/azure/defender-for-cloud/defender-for-cloud-introduction)
- [Microsoft Security Exposure Management](/en-us/security-exposure-management/)
- [Microsoft Defender for Cloud Apps](/en-us/defender-cloud-apps/what-is-defender-for-cloud-apps)
- [Microsoft Sentinel](/en-us/azure/sentinel/sentinel-overview)

Microsoft Defender provides integrated threat protection, detection, and response across endpoints, email, identities, applications, and data within a single portal. Controlling a user's permissions around their access to view data or complete tasks is essential for organizations to minimize the risks associated with unauthorized access.

The Microsoft Defender unified role-based access control (RBAC) model provides a single permissions management experience that provides one central location for administrators to control user permissions across different security solutions.

Important

Starting 2025, the Microsoft Defender unified RBAC model is the default permissions model for new Microsoft Defender Endpoint tenants and Microsoft Defender for Identity tenants. These tenants can't export roles and permissions from the old model. Defender for Endpoint or Defender for Identity tenants with roles and permissions assigned or exported prior to this date maintain their old roles and permissions configuration.

Starting July 2026, the Microsoft Defender unified RBAC model is also the default permissions model for new Microsoft Defender for Office 365 Plan 2 organizations. For more information, see [MC1246006](https://admin.microsoft.com/Adminportal/Home#/MessageCenter/:/messages/MC1246006).

## What's supported by the Microsoft Defender unified RBAC model

Centralized permissions management is supported for the following services:

| Service name | Unified RBAC support |
| --- | --- |
| **Microsoft Defender** | Centralized permissions management for Microsoft Defender experiences. |
| **Microsoft Defender for Endpoint** | Full support for all endpoint data and actions. All roles are compatible with the device group's scope as defined on the device groups page. Limiting permissions to different device groups is accomplished in the Devices Groups page. |
| **Microsoft Defender Vulnerability Management** | Centralized permissions management for all Defender Vulnerability Management capabilities. |
| **Microsoft Defender for Office 365** | Full support for all data and actions. **Note**: <br>- Initially, the Microsoft Defender RBAC model is available only for organizations with Microsoft Defender for Office 365 Plan 2 licenses (trial licenses aren't supported).<br>- Exchange Online PowerShell and Security & Compliance PowerShell continue to use [Exchange Online roles](/en-us/exchange/permissions-exo/permissions-exo) and [Email & Collaboration roles](/en-us/defender-office-365/mdo-portal-permissions). Microsoft Defender unified RBAC doesn't affect Exchange Online PowerShell or Security & Compliance PowerShell. |
| **Microsoft Defender for Identity** | Full support for all identity data and actions. All roles are compatible with [Microsoft Defender for Identity scoped access](/en-us/defender-for-identity/configure-scoped-access).**Note:** Defender for Identity experiences also adhere to permissions granted from [Microsoft Defender for Cloud Apps](https://security.microsoft.com/cloudapps/permissions/roles). For more information, see [Microsoft Defender for Identity role groups](https://go.microsoft.com/fwlink/?linkid=2202729). |
| **Microsoft Defender for Cloud** | Support access management for all Defender for Cloud data that is available in Microsoft Defender portal. |
| **Microsoft Security Exposure Management** | Full support for all Exposure Management data and actions, including Microsoft Secure Score data. |
| **Microsoft Defender for Cloud Apps (Preview)** | **Note:** Once Unified RBAC is activated, some built-in scoped roles will no longer be supported. For more information, see [Map Microsoft Defender for Cloud Apps permissions to the Microsoft Defender unified RBAC permissions](compare-rbac-roles#microsoft-defender-for-cloud-apps). |
| **Microsoft Sentinel** | Supports unified access management for all Microsoft Sentinel workspaces onboarded to the Defender portal. Sentinel role assignments made in Unified RBAC sync with Azure RBAC and are visible there. However, unified RBAC becomes the source of permissions once enabled. When activating Sentinel in Unified RBAC, the *User Access Administrator* role is assigned to the MTP Unified RBAC app within the enabled workspace.Assigning permissions to a service principal or to a GDAP user group in Microsoft Sentinel isn't supported in unified RBAC. If you need either capability, keep using Azure RBAC for Microsoft Sentinel. For more information, see [Activate Microsoft Defender unified RBAC](activate-defender-rbac). Sentinel experiences in the Defender portal continue to respect ARM roles and permissions in addition to URBAC. Therefore, users with more permissions in ARM than in URBAC may see more data in the Sentinel pages in the Defender portal than configured in their URBAC permissions. Supports permission management for the Microsoft Sentinel data lake default workspace, when Microsoft Sentinel is onboarded to both the Defender portal and the Microsoft Sentinel data lake. Microsoft Sentinel users with built-in Azure RBAC roles for their workspaces receive parallel permissions in the Microsoft Sentinel data lake experiences, such as the lake explorer and notebooks. For more information, see [Roles and permissions for the Microsoft Sentinel data lake](/en-us/azure/sentinel/roles#roles-and-permissions-for-the-microsoft-sentinel-data-lake). For row-level access to Sentinel data by using reusable scope tags, see [Configure Microsoft Sentinel scoping](scoping). To see which roles are supported, check the [unified RBAC roles mapping](compare-rbac-roles#microsoft-sentinel). |

Note

Scenarios and experiences controlled by Compliance permissions are managed in the Microsoft Purview portal. Specifically, Data Loss Prevention (DLP) and Insider Risk Management experiences accessible from the Defender portal are governed by Microsoft Purview RBAC, not Microsoft Defender unified RBAC. To manage permissions for these experiences, see [Permissions in the Microsoft Purview portal](/en-us/purview/purview-permissions).

## Before you start

This section provides useful information on what you need to know before you start using Microsoft Defender unified RBAC.

### Permissions prerequisites

- You must be at least a Security Administrator in Microsoft Entra ID to:

    - Gain initial access to [Permissions and roles](https://security.microsoft.com/mtp_roles) in the Microsoft Defender portal.
    - Manage roles and permissions in Microsoft Defender unified RBAC.
    - Create a custom role that can grant access to security groups or individual users to manage roles and permissions in Microsoft Defender unified RBAC. This removes the need for Microsoft Entra global roles to manage permissions. To do this, you need to assign the **Authorization** permission in Microsoft Defender unified RBAC. For details on how to assign the Authorization permission, see [Create a role to access and manage roles and permissions](create-custom-rbac-roles#create-a-role-to-access-and-manage-roles-and-permissions).
- The Microsoft Defender security solution continues to respect existing Microsoft Entra global roles when you activate the Microsoft Defender unified RBAC model for some or all of your workloads, that is, Security Administrators retain assigned administrator privileges.
- To activate a Microsoft Sentinel workspace in unified RBAC, you need:

    - Security Administrator role in Microsoft Entra ID
    - AND one of the following:
        - Subscription Owner, OR
        - User Access Administrator + Sentinel Contributor on the workspace
- In unified RBAC, being a Global Administrator does not grant you automatic permissions over workspaces. It does grant you the right to assign permissions, including to yourself.

### Migration of existing roles and permissions

The new Microsoft Defender unified RBAC model provides easy migration of the existing permissions in the individual supported unified RBAC models to the new RBAC model.

Defender for Endpoint Devices Groups now use the device groups side of the interface to define which groups have access to the proper Device Groups.

All permissions listed within the Microsoft Defender unified RBAC model align to permissions in the individual RBAC models to ensure backward compatibility. For more information on how the permissions align, see [Map permissions in Microsoft Defender unified role-based access control (RBAC)](compare-rbac-roles).

### Activation of the Microsoft Defender unified RBAC model

You must activate the workloads in Microsoft Defender to use the Microsoft Defender unified RBAC model. Until activated, Microsoft Defender continues to respect the existing RBAC models. Microsoft Sentinel must be activated on a per-workspace basis. For more information, see [Activate Microsoft Defender unified RBAC](activate-defender-rbac).

When you activate some or all of your workloads to use the new permission model, the roles and permissions for these workloads are fully controlled by the Microsoft Defender unified RBAC model in the Microsoft Defender portal.

## Start using Microsoft Defender unified RBAC model

Use the following steps as a guide to start using the Microsoft Defender unified RBAC model:

1. **Get started with creating custom roles and importing roles from existing RBAC role models**

    - [Create custom roles](create-custom-rbac-roles)
    - [Import existing RBAC roles](import-rbac-roles)
    - [View, edit, and delete RBAC roles](edit-delete-rbac-roles)
2. **Activate and manage your roles with the Microsoft Defender unified RBAC model**

    - [Activate Microsoft Defender unified RBAC](activate-defender-rbac)
3. **Learn more about the Microsoft Defender unified RBAC model**

    - [Microsoft Defender unified RBAC permissions](custom-permissions-details)
    - [Map existing RBAC roles to Microsoft Defender unified RBAC roles](compare-rbac-roles)
4. **Learn more about Microsoft Defender for Identity scoped access**

    - [Configure scoped access in Microsoft Defender for Identity](/en-us/defender-for-identity/configure-scoped-access).
5. **Manage unified RBAC across multiple tenants**

    - [Manage unified role-based access control in multitenant management](/en-us/defender-xdr/mto-urbac)

Watch the following video to see the preceding steps in action:

Tip

Do you want to learn more? Engage with the Microsoft Security community in our Tech Community: [Microsoft Defender XDR Tech Community](https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection).