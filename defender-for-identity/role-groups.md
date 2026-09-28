---
layout: Conceptual
title: Role groups - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/role-groups
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
description: Learn about working with Microsoft Defender for Identity role groups.
ms.date: 2024-01-15T00:00:00.0000000Z
ms.topic: article
ms.reviewer: LiorShapiraa
ms.custom: sfi-ga-nochange
locale: en-us
document_id: 2674e172-f3c0-8aa2-030c-60e66dc34927
document_version_independent_id: 2674e172-f3c0-8aa2-030c-60e66dc34927
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/role-groups.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: role-groups
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/role-groups.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: be550c6c-ced5-6397-bfca-cd50e16bb225
---

# Role groups - Microsoft Defender for Identity | Microsoft Learn

Microsoft Defender for Identity offers role-based security to safeguard data according to your organization's specific security and compliance needs. We recommend that you use role groups to manage access to Defender for Identity, segregating responsibilities across your security team and granting only the amount of access that users need to do their jobs.

## Unified role-based access control (RBAC)

Users that are already have the [Security Administrators](/en-us/entra/identity/role-based-access-control/permissions-reference) on your tenant's Microsoft Entra ID are also automatically Defender for Identity administrator. Microsoft Entra Security Administrators don't need extra permissions to access Defender for Identity.

For other users, enable and use Microsoft 365 role-based access control (RBAC) to create custom roles and to support more Entra ID roles such as Security operator or Security Reader by default to manage access to Defender for Identity.

Important

Starting March 2, 2025, new Microsoft Defender for Identity tenants can only configure permissions through Microsoft Defender XDR [Unified Role-Based Access Control (RBAC)](/en-us/defender-xdr/manage-rbac). Tenants with roles assigned or exported before this date will retain their current configuration.

When creating your custom roles, make sure that you apply the permissions listed in the following table:

| Defender for Identity access level | Minimum required Microsoft 365 unified RBAC permissions |
| --- | --- |
| **Administrators** | - `Authorization and settings/Security settings/Read`- `Authorization and settings/Security settings/All permissions` - `Authorization and settings/System settings/Read`- `Authorization and settings/System settings/All permissions` - `Security operations/Security data/Alerts (manage)` -`Security operations/Security data /Security data basics (Read)`- `Authorization and settings/Authorization/All permissions` - `Authorization and settings/Authorization/Read` |
| **Users** | - `Security operations/Security data /Security data basics (Read)`- `Authorization and settings/System settings/Read`- `Authorization and settings/Security settings/Read`- `Security operations/Security data/Alerts (manage)`- `microsoft.xdr/configuration/security/manage` |
| **Viewers** | - `Security operations/Security data /Security data basics (Read)`- `Authorization and settings / System settings (Read and manage)`- `Authorization and settings / Security setting (All permissions)` |

For more information, see [Custom roles in role-based access control for Microsoft Defender](/en-us/microsoft-365/security/defender/custom-roles) and [Create custom roles with Microsoft Defender unified RBAC](/en-us/microsoft-365/security/defender/create-custom-rbac-roles).

Note

Information included from the [Defender for Cloud Apps activity log](classic-mcas-integration#activities) may still contain Defender for Identity data. This content adheres to existing Defender for Cloud Apps permissions.

Exception: If you have configured [Scoped deployment](/en-us/defender-cloud-apps/scoped-deployment) for Microsoft Defender for Identity alerts in Microsoft Defender for Cloud Apps, these permissions do not carry over and you will have to explicitly grant the Security operations \ Security data \ Security data basics (read) permissions for the relevant portal users.

## Required permissions Defender for Identity in Microsoft Defender

The following table details the specific permissions required for Defender for Identity activities in [Microsoft Defender](/en-us/microsoft-365/security/defender/microsoft-365-security-center-mdi).

| Activity | Least required permissions |
| --- | --- |
| **Onboard Defender for Identity** (create workspace) | [Security Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference) |
| **Configure Defender for Identity settings** | One of the following Microsoft Entra roles:- [Security Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference)- [Security Operator](/en-us/entra/identity/role-based-access-control/permissions-reference)**Or**The following Unified RBAC permissions:- `Authorization and settings/Security settings/Read`- `Authorization and settings/Security settings/All permissions`- `Authorization and settings/System settings/Read`- `Authorization and settings/System settings/All permissions` |
| **View Defender for Identity settings** | Microsoft Entra roles:- [Security Reader](/en-us/entra/identity/role-based-access-control/permissions-reference)**Or**The following Unified RBAC permissions:- `Authorization and settings/Security settings/Read`- `Authorization and settings/System settings/Read` |
| **Manage Defender for Identity security alerts and activities** | One of the following Microsoft Entra roles:- [Security Operator](/en-us/entra/identity/role-based-access-control/permissions-reference)**Or**The following Unified RBAC permissions:- `Security operations/Security data/Alerts (Manage)`- `Security operations/Security data /Security data basics (Read)` |
| **View Defender for Identity security assessments** (now part of Microsoft Secure Score) | [Permissions](/en-us/microsoft-365/security/defender/microsoft-secure-score#required-permissions) to access Microsoft Secure Score **And** The following Unified RBAC permissions: `Security operations/Security data /Security data basics (Read)` |
| **View the Assets / Identities page** | [Permissions](/en-us/defender-cloud-apps/manage-admins) to access Defender for Cloud Apps **Or** One of the Microsoft Entra roles required by [Microsoft Defender](/en-us/microsoft-365/security/defender/m365d-permissions) |
| **Perform Defender for Identity response actions** | A [custom role](/en-us/microsoft-365/security/defender/create-custom-rbac-roles) defined with permissions for **Response (manage)** **Or** One of the following Microsoft Entra roles:- [Security Operator](/en-us/entra/identity/role-based-access-control/permissions-reference)- [SOC Identity Responder](/en-us/entra/identity/role-based-access-control/permissions-reference) |

## Defender for Identity security groups

Important

Starting March 2, Defender for Identity will no longer create Microsoft Entra ID security groups. Tenants can still configure the same permissions through Microsoft Defender XDR [Unified Role-Based Access Control (RBAC)](/en-us/defender-xdr/manage-rbac)

Defender for Identity provides the following security groups to help manage access to Defender for Identity resources:

- **Azure ATP *(workspace name)* Administrators**
- **Azure ATP *(workspace name)* Users**
- **Azure ATP *(workspace name)* Viewers**

The following table lists the activities available for each security group:

| Activity | Azure ATP*(workspace name)*Administrators | Azure ATP*(Workspace name)*Users | Azure ATP*(Workspace name)*Viewers |
| --- | --- | --- | --- |
| **Change health issue status** | Available | Not available | Not available |
| **Change security alert status** (reopen, close, exclude, suppress) | Available | Available | Not available |
| **Delete workspace** | Available | Not available | Not available |
| **Download a report** | Available | Available | Available |
| **Sign in** | Available | Available | Available |
| **Share/Export security alerts** (via email, get link, download details) | Available | Available | Available |
| **Update Defender for Identity configuration** (updates) | Available | Not available | Not available |
| **Update Defender for Identity configuration** (entity tags, including both sensitive and honeytoken) | Available | Available | Not available |
| **Update Defender for Identity configuration** (exclusions) | Available | Available | Not available |
| **Update Defender for Identity configuration** (language) | Available | Available | Not available |
| **Update Defender for Identity configuration** (notifications, including both email and syslog) | Available | Available | Not available |
| **Update Defender for Identity configuration** (preview detections) | Available | Available | Not available |
| **Update Defender for Identity configuration** (scheduled reports) | Available | Available | Not available |
| **Update Defender for Identity configuration** (data sources, including directory services, SIEM, VPN, Defender for Endpoint) | Available | Not available | Not available |
| **Update Defender for Identity configuration** (sensor management, including downloading software, regenerating keys, configuring, deleting) | Available | Not available | Not available |
| **View entity profiles and security alerts** | Available | Available | Available |

## Add and remove users

Defender for Identity uses Microsoft Entra security groups as a basis for role groups.

Manage your role groups from [Groups management page](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/GroupsManagementMenuBlade/AllGroups) on the Azure portal. Only Microsoft Entra users can be added or removed from security groups.

## Assign Identity scoping

User Role-Based Access Control (URBAC) enables organizations to define custom roles that restrict visibility to specific Active Directory domains. Individuals assigned to these scoped roles will only see data, such as alerts, identities, and activities, related to the Active Directory domains included in their Defender XDR role assignment.

For more information, see: [Scoped access for Microsoft Defender for Identity](configure-scoped-access)