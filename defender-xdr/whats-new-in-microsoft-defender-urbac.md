---
layout: Conceptual
title: What's new in Microsoft Defender unified role-based access control (RBAC) - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/whats-new-in-microsoft-defender-urbac
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: See what features are available in the latest release of Microsoft Defender unified role-based access control (RBAC)
ms.service: defender-xdr
ms.author: monaberdugo
author: mberdugo
ms.localizationpriority: medium
ms.collection:
- m365-security-compliance
- tier2
ms.topic: whats-new
ms.date: 2025-07-06T00:00:00.0000000Z
locale: en-us
document_id: e1158944-ffa0-9f5e-75b5-db2f760caf50
document_version_independent_id: e1158944-ffa0-9f5e-75b5-db2f760caf50
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/whats-new-in-microsoft-defender-urbac.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: whats-new-in-microsoft-defender-urbac
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/whats-new-in-microsoft-defender-urbac.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 184c98ff-6304-d356-73c2-a6e4cd0b6a17
---

# What's new in Microsoft Defender unified role-based access control (RBAC) - Microsoft Defender XDR | Microsoft Learn

This article provides information about new features and important product updates for the latest release of Microsoft Defender unified role-based access control (RBAC).

## December 2025

### Microsoft Defender for Cloud Apps permissions are now integrated with Microsoft Defender unified RBAC

Integration of Microsoft Defender for Cloud Apps permissions with Microsoft Defender unified RBAC is now available worldwide.

## November 2025

### Microsoft Defender for Cloud permissions are now integrated with Microsoft Defender unified RBAC (Preview)

We’ve introduced Unified Role-Based Access Control (URBAC) to simplify permission management across Defender for Cloud resources.

Assign roles consistently across cloud scopes. Apply least-privilege principles with granular permissions. New consolidated role table available for quick reference.

For more information, see: [Unified RBAC roles in Microsoft Defender for Cloud](compare-rbac-roles#microsoft-defender-for-cloud)

## July 2025

### Microsoft Sentinel data lake permissions integrated with Microsoft Defender unified RBAC (Preview)

Starting in July 2025, Microsoft Sentinel data lake permissions are provided through Microsoft Defender unified RBAC. Support for unified RBAC is available in addition the support provided by global Microsoft Entra ID roles.

For more information, see:

- [Microsoft Defender unified role-based access control (RBAC)](manage-rbac)
- [Create custom roles with Microsoft Defender unified RBAC](create-custom-rbac-roles)
- [Permissions in Microsoft Defender unified role-based access control (RBAC)](custom-permissions-details)
- [Roles and permissions for the Microsoft Sentinel data lake (Preview)](/en-us/azure/sentinel/roles#roles-and-permissions-for-the-microsoft-sentinel-data-lake-preview)

## March 2025

Starting March 2, 2025, new Microsoft Defender for Identity tenants will have the unified RBAC model as their default permissions model. They won't be able to export roles and permissions from the current model. Existing Defender for Identity tenants will maintain their current roles and permissions configuration.

## February 2025

Starting February 16, 2025, the Microsoft Defender unified RBAC model is the default permissions model for new Microsoft Defender Endpoint tenants. These new tenants won't have the capability to export roles and permissions from the current model. Defender for Endpoint tenants with roles and permissions assigned or exported prior to this date will maintain their current roles and permissions configuration.

## November 2024

### Microsoft Defender for Cloud Apps permissions are now integrated with Microsoft Defender unified RBAC (Preview)

You can control access and grant granular permissions for Microsoft Defender for Cloud Apps as part of the Microsoft Defender unified RBAC model. For more information, see [Map Microsoft Defender for Cloud Apps permissions to the Microsoft Defender unified RBAC permissions](compare-rbac-roles#microsoft-defender-for-cloud-apps). To activate the Defender for Cloud Apps workload, see [Activate Microsoft Defender unified RBAC](activate-defender-rbac).

## May 2024

The permissions model to access *Email & collaboration* schema in advanced hunting for Microsoft Defender for Office 365 customers has been updated to align with Threat Explorer.

As part of this change, customers who are using Microsoft Defender unified RBAC with Defender for Office 365 should use the **Security operations \ Raw data \ Email & collaboration metadata (read)** permission to grant analysts access to the *Email & collaboration* schema in advanced hunting.

Users with the **Security operations \ Security data \ Security data basics (read)** permission for Defender for Office 365 will no longer have access to the *Email & collaboration* schema in advanced hunting, but will keep their access to the *Alerts & behaviors* schema.

## January 2024

Microsoft Defender unified RBAC is now generally available to GCC High and DoD customers. To learn more about the supported workloads and supported data sources, see [Microsoft Defender unified role-based access control (RBAC)](manage-rbac).

The process of importing roles from individual workloads' RBAC models into Microsoft Defender unified RBAC has been improved. Admins can now view the permissions and assignment of a role before importing it by clicking the role name at the roles to import selection stage.

## December 2023

### Microsoft Defender unified RBAC is now generally available

Microsoft Defender unified RBAC is now generally available. This offering is also available to GCC Moderate customers. To learn more about the supported workloads and supported data sources, see [Microsoft Defender unified role-based access control (RBAC)](manage-rbac).

## October 2023

### Exchange Online permission management for Microsoft Defender for Office 365 is now supported in Microsoft Defender unified role-based access control (RBAC) providing full integration of Defender for Office 365 roles and permissions

Microsoft Defender unified Role-Based Access Control (RBAC) model now supports all security permission management scenarios for Microsoft Defender for Office 365.

In addition to the existing support for scenarios that are controlled by Email & collaboration roles (configured in the Microsoft Defender portal at https://security.microsoft.com/emailandcollabpermissions), Microsoft Defender unified RBAC now also supports the management of protection-related Exchange Online permissions, which could previously only be managed in the Exchange admin center (EAC) at https://admin.exchange.microsoft.com/#/adminRoles. To learn more about the Exchange Online permissions that are now supported, see [Exchange Online permissions mapping](compare-rbac-roles#exchange-online-permissions-mapping).

## September 2023

### Export roles for Microsoft Defender unified role-based access control (RBAC)

Now you can easily export your existing roles in Defender unified RBAC to a CSV file. The exported file will include details such as the role name, the included permissions, the assigned users or user groups, and assigned data sources. When a role has multiple assignments, each assignment will be listed on a separate row in the CSV file. The CSV also includes a snapshot of the Defender unified RBAC activation status for each workload available on the tenant. For more information, see [Edit, delete and export roles](edit-delete-rbac-roles#export-roles).

## August 2023

### Detection tuning and Security settings permissions

You can now assign a new granular permission called **Detection tuning (manage)** in Microsoft Defender unified RBAC. Granting the **Detection Tuning (manage)** permission allows security operations analysts to create and manage Custom Detection, Alerts Tuning, and Threat Indicators of Compromise rules without granting them the full **Security Settings (manage)** permission.  You can add the new permissions to a custom role by selecting **Authorization and settings \ Security settings** when creating or updating the role. For more information, see [Create custom roles with Microsoft Defender unified RBAC](create-custom-rbac-roles).

The **Security settings** permission name has been updated to **Core security settings**. This change has no impact on existing roles and permissions.

### Microsoft Defender Vulnerability Management permissions are now integrated with Microsoft Defender unified role-based access control (RBAC)

You can now control access and grant granular permissions for Microsoft Defender Vulnerability Management as part of the Microsoft Defender unified RBAC model. For more information, see [Microsoft Defender 365 Unified role-based access control (RBAC)](manage-rbac). You can add the new permissions to a custom role by selecting them from the **Security posture** permissions group when creating the role. For more information, see [Create custom roles with Microsoft Defender unified RBAC](create-custom-rbac-roles).

### Microsoft Secure Score permissions integration with Microsoft Defender unified role-based access control (RBAC) is now in Public Preview

You can control access and grant granular permissions for the Microsoft Secure Score experience as part of the Microsoft Defender unified RBAC model. For more information, see [Manage permissions with Microsoft Defender unified role-based access control(RBAC)](microsoft-secure-score#manage-permissions-with-microsoft-365-defender-unified-role-based-access-controlrbac).

### A new file collection permission in Microsoft Defender unified RBAC is now in Public Preview

You can now assign a new granular permission in Microsoft Defender unified RBAC that allows users to collect or download files for analysis. This permission enables Microsoft Defender for Endpoint users download files directly from the file page and during a live response investigation in the live response console. You can add the new permission to a custom role by selecting it from the **Security operations** permissions group when creating the role. For more information, see [Create custom roles with Microsoft Defender unified RBAC](create-custom-rbac-roles).

For more information on what's new with other Microsoft Defender security products, see:

- [What's new in Microsoft Defender Vulnerability Management](/en-us/defender-vulnerability-management/whats-new-in-microsoft-defender-vulnerability-management)
- [What's new in Microsoft Defender for Endpoint](/en-us/defender-endpoint/whats-new-in-microsoft-defender-endpoint)
- [What's new in Microsoft Defender XDR](whats-new)
- [What's new in Microsoft Defender for Office 365](/en-us/defender-office-365/defender-for-office-365-whats-new)
- [What's new in Microsoft Defender for Identity](/en-us/defender-for-identity/whats-new)
- [What's new in Microsoft Defender for Cloud Apps](/en-us/cloud-app-security/release-notes)