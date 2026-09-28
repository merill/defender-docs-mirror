---
layout: Conceptual
title: Roles and permissions in the Microsoft Sentinel platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/roles
breadcrumb_path: breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
description: Learn how Microsoft Sentinel assigns permissions to users using both Azure and Microsoft Entra ID role-based access control, and identify the allowed actions for each role.
ms.author: monaberdugo
author: mberdugo
ms.reviewer: noak
ms.topic: concept-article
ms.date: 2026-01-07T00:00:00.0000000Z
ms.collection: usx-security
locale: en-us
document_id: a48f0071-6884-c919-f316-1d7aad073de4
document_version_independent_id: 0213d067-42e7-9f1d-4da6-c0e6819f72c8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/roles.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/roles
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/roles.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: ccf854cb-1e62-49bf-5162-fac2202861ca
---

# Roles and permissions in the Microsoft Sentinel platform | Microsoft Learn

This article explains how Microsoft Sentinel assigns permissions to user roles for both Microsoft Sentinel SIEM and Microsoft Sentinel data lake, identifying the allowed actions for each role.

Microsoft Sentinel uses [Azure role-based access control (Azure RBAC)](/en-us/azure/role-based-access-control/) to provide built-in and custom roles for Microsoft Sentinel SIEM, and [Microsoft Entra ID role-based access control (Microsoft Entra ID RBAC)](/en-us/entra/identity/role-based-access-control/custom-overview) to provide built-in and custom roles for Microsoft Sentinel data lake.

Before assigning roles, see the planning guide [Steps to assign an Azure role](/en-us/azure/role-based-access-control/role-assignments-steps) for help determining who needs access, which role to choose, and what scope to apply.

Use the following step-by-step instructions to assign roles to users, groups, and services, based on your role type:

- **Azure roles**: [Assign Azure roles using the Azure portal](/en-us/azure/role-based-access-control/role-assignments-portal)
- **Microsoft Entra ID roles**: [Assign Microsoft Entra roles](/en-us/entra/identity/role-based-access-control/manage-roles-portal?tabs=admin-center)

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

Note

If you are running the Microsoft Defender XDR preview program, you can now experience the new Microsoft Defender Unified Role-Based Access Control (URBAC) model. For more information, see [Microsoft Defender XDR Unified role-based access control (RBAC)](/en-us/defender-xdr/manage-rbac).

Important

Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

## Built-in Azure roles for Microsoft Sentinel

The following built-in Azure roles are used for Microsoft Sentinel SIEM and grant read access to the workspace data, including support for the Microsoft Sentinel data lake. Assign these roles at the resource group level for best results.

| Role | SIEM support | Data lake support |
| --- | --- | --- |
| [**Microsoft Sentinel Reader**](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-reader) | View data, incidents, workbooks, recommendations and other resources | Access advanced analytics and run interactive queries on workspaces only. |
| [**Microsoft Sentinel Responder**](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-responder) | All Reader permissions, plus manage incidents | N/A |
| [**Microsoft Sentinel Contributor**](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-contributor) | All Responder permissions, plus install/update solutions, create/edit resources | Access advanced analytics and run interactive queries on workspaces only. |
| [**Microsoft Sentinel Playbook Operator**](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-playbook-operator) | List, view, and manually run playbooks | N/A |
| [**Microsoft Sentinel Automation Contributor**](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-automation-contributor) | Allows Microsoft Sentinel to add playbooks to automation rules. Not used for user accounts. | N/A |

For example, the following table shows examples of tasks that each role can perform in Microsoft Sentinel:

| Role | Run playbooks | Create/edit playbooks | Create/edit analytics rules, workbooks, etc. | Manage incidents | View data, incidents, workbooks, recommendations | Manage content hub |
| --- | --- | --- | --- | --- | --- | --- |
| [**Microsoft Sentinel Reader**](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-reader) | -- | -- | --\* | -- | ✓ | -- |
| [**Microsoft Sentinel Responder**](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-responder) | -- | -- | --\* | ✓ | ✓ | -- |
| [**Microsoft Sentinel Contributor**](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-contributor) | -- | -- | ✓ | ✓ | ✓ | ✓ |
| [**Microsoft Sentinel Playbook Operator**](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-playbook-operator) | ✓ | -- | -- | -- | -- | -- |
| [**Logic App Contributor**](/en-us/azure/role-based-access-control/built-in-roles/integration#logic-app-contributor) | ✓ | ✓ | -- | -- | -- | -- |

\*With [Workbook Contributor](/en-us/azure/role-based-access-control/built-in-roles#workbook-contributor) role.

We recommend that you assign roles to the resource group that contains the Microsoft Sentinel workspace. This ensures that all related resources, such as Logic Apps and playbooks, are covered by the same role assignments.

As another option, assign the roles directly to the Microsoft Sentinel **workspace** itself. If you do that, you must assign the same roles to the SecurityInsights **solution resource** in that workspace. You might also need to assign them to other resources, and continually manage role assignments to the resources.

### Additional roles for specific tasks

Users with particular job requirements might need to be assigned other roles or specific permissions in order to accomplish their tasks. For example:

| Task | Required roles/permissions |
| --- | --- |
| **Connect data sources** | **Write** permission on the workspace. Check connector docs for extra permissions required per connector. |
| **Manage content from Content hub** | [Microsoft Sentinel Contributor](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-contributor) at the resource group level |
| **Automate responses with playbooks** | [Microsoft Sentinel Playbook Operator](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-playbook-operator), to run playbooks, and [Logic App Contributor](/en-us/azure/role-based-access-control/built-in-roles/integration#logic-app-contributor) to create/edit playbooks.  Microsoft Sentinel uses playbooks for automated threat response. Playbooks are built on Azure Logic Apps, and are a separate Azure resource. For specific members of your security operations team, you might want to assign the ability to use Logic Apps for Security Orchestration, Automation, and Response (SOAR) operations. |
| **Allow Microsoft Sentinel to run playbooks via automation** | Service account needs explicit permissions to playbook resource group; your account needs [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) permissions to assign these. Microsoft Sentinel uses a special service account to run incident-trigger playbooks manually or to call them from automation rules. The use of this account (as opposed to your user account) increases the security level of the service. For an automation rule to run a playbook, this account must be granted explicit permissions to the resource group where the playbook resides. At that point, any automation rule can run any playbook in that resource group. |
| **Guest users assign incidents** | [Directory Reader](/en-us/entra/identity/role-based-access-control/permissions-reference) AND [Microsoft Sentinel Responder](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-responder)The Directory Reader role isn't an Azure role but a Microsoft Entra ID role, and regular (nonguest) users have this role assigned by default. |
| **Create/delete workbooks** | [Microsoft Sentinel Contributor](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-contributor) or a lesser Microsoft Sentinel role AND [Workbook Contributor](/en-us/azure/role-based-access-control/built-in-roles#workbook-contributor) |

### Other Azure and Log Analytics roles

When you assign Microsoft Sentinel-specific Azure roles, you might come across other Azure and Log Analytics roles that might be assigned to users for other purposes. These roles grant a wider set of permissions that include access to your Microsoft Sentinel workspace and other resources:

- **Azure roles:**[Owner](/en-us/azure/role-based-access-control/built-in-roles#owner), [Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor), [Reader](/en-us/azure/role-based-access-control/built-in-roles#reader) – grant broad access across Azure resources.
- **Log Analytics roles:**[Log Analytics Contributor](/en-us/azure/role-based-access-control/built-in-roles#log-analytics-contributor), [Log Analytics Reader](/en-us/azure/role-based-access-control/built-in-roles#log-analytics-reader) – grant access to Log Analytics workspaces.

Important

Role assignments are cumulative. A user with both **Microsoft Sentinel Reader** and **Contributor** roles may have more permissions than intended.

### Recommended role assignments for Microsoft Sentinel users

| User type | Role | Resource group | Description |
| --- | --- | --- | --- |
| **Security analysts** | [Microsoft Sentinel Responder](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-responder) | Microsoft Sentinel resource group | View/manage incidents, data, workbooks |
|  | [Microsoft Sentinel Playbook Operator](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-playbook-operator) | Microsoft Sentinel/playbook resource group | Attach/run playbooks |
| **Security engineers** | [Microsoft Sentinel Contributor](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-contributor) | Microsoft Sentinel resource group | Manage incidents, content, resources |
|  | [Logic App Contributor](/en-us/azure/role-based-access-control/built-in-roles/integration#logic-app-contributor) | Microsoft Sentinel/playbook resource group | Run/modify playbooks |
| **Service Principal** | [Microsoft Sentinel Contributor](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-contributor) | Microsoft Sentinel resource group | Automated management tasks |

## Roles and permissions for the Microsoft Sentinel data lake

To use the Microsoft Sentinel data lake, your workspace must be [onboarded to the Defender portal](/en-us/azure/sentinel/microsoft-sentinel-onboard) and the [Microsoft Sentinel data lake](datalake/sentinel-lake-overview).

### Microsoft Sentinel data lake read permissions

Microsoft Entra ID roles provide broad access across all content in the data lake. Use the following roles to provide read access to all workspaces within the Microsoft Sentinel data lake, such as for running queries.

| Permission type | Supported roles |
| --- | --- |
| **Read access across all workspaces** | Use any of the following Microsoft Entra ID roles: - [Global reader](/en-us/entra/identity/role-based-access-control/permissions-reference#global-reader)- [Security reader](/en-us/azure/role-based-access-control/built-in-roles/security#security-reader)- [Security operator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-operator) - [Security administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator) - [Global administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-administrator) |

Alternatively, you might want to assign the ability to read tables from within a specific workspace. In such cases, use one of the following:

| Tasks | Permissions |
| --- | --- |
| **Read permissions on the [system tables](https://go.microsoft.com/fwlink/?linkid=2325420)** | Use a [custom Microsoft Defender XDR unified RBAC role with](/en-us/defender-xdr/custom-permissions-details)*[security data basics (read)](/en-us/defender-xdr/custom-permissions-details)* permissions over the Microsoft Sentinel data collection. |
| **Read permissions on any other workspace enabled for Microsoft Sentinel in the data lake** | Use one of the following built-in roles in Azure RBAC for permissions on that workspace: - [Log Analytics Reader](/en-us/azure/role-based-access-control/built-in-roles/monitor#log-analytics-reader)- [Log Analytics Contributor](/en-us/azure/role-based-access-control/built-in-roles/monitor#log-analytics-contributor)- [Microsoft Sentinel Contributor](/en-us/azure/role-based-access-control/built-in-roles/security#microsoft-sentinel-contributor)- [Microsoft Sentinel Reader](/en-us/azure/role-based-access-control/built-in-roles/security#microsoft-sentinel-reader)- [Reader](/en-us/azure/role-based-access-control/built-in-roles/general#reader)- [Contributor](/en-us/azure/role-based-access-control/built-in-roles/privileged#contributor)- [Owner](/en-us/azure/role-based-access-control/built-in-roles/privileged#owner) |

### Microsoft Sentinel data lake write permissions

Microsoft Entra ID roles provides broad access across all workspaces in the data lake. Use the following roles to provide write access to the Microsoft Sentinel data lake tables:

| Permission type | Supported roles |
| --- | --- |
| **Write to tables in the analytics tier using KQL jobs or notebooks** | Use one of the following Microsoft Entra ID roles:  - [Security operator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-operator)- [Security administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator)- [Global administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-administrator) |
| **Write to tables in the Microsoft Sentinel data lake** | Use one of the following Microsoft Entra ID roles: - [Security operator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-operator)- [Security administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator)- [Global administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-administrator) |

Alternatively, you might want to assign the ability to write output to a specific workspace. This can include the ability to configure connectors to that workspace, modifying retention settings for tables in the workspace, or creating, updating, and deleting custom tables in that workspace. In such cases, use one of the following:

| Tasks | Permissions |
| --- | --- |
| **Update [system tables](https://go.microsoft.com/fwlink/?linkid=2325420) in the data lake** | Use a [custom Microsoft Defender XDR unified RBAC role with](https://aka.ms/data-lake-custom-urbac)*[data (manage)](https://aka.ms/data-lake-custom-urbac)* permissions over the Microsoft Sentinel data collection. |
| **For any other Microsoft Sentinel workspace in the data lake** | Use any built-in or custom role that includes the following Azure RBAC [Microsoft operational insights](/en-us/azure/role-based-access-control/permissions/monitor#microsoftoperationalinsights) permissions on that workspace: - *microsoft.operationalinsights/workspaces/write* - *microsoft.operationalinsights/workspaces/tables/write* - *microsoft.operationalinsights/workspaces/tables/delete*For example, built-in roles that include these permissions [Log Analytics Contributor](/en-us/azure/role-based-access-control/built-in-roles/monitor#log-analytics-contributor), [Owner](/en-us/azure/role-based-access-control/built-in-roles/privileged#owner), and [Contributor](/en-us/azure/role-based-access-control/built-in-roles/privileged#contributor). |

### Manage jobs in the Microsoft Sentinel data lake

To create scheduled jobs or to manage jobs in the Microsoft Sentinel data lake, you must have one of the following Microsoft Entra ID roles:

- [Security operator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-operator)
- [Security administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator)
- [Global administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-administrator)

## Custom roles and advanced RBAC

To restrict access to specific data, but not the whole workspace, use [resource-context RBAC](resource-context-rbac) or [Table-level RBAC](https://techcommunity.microsoft.com/t5/azure-sentinel/table-level-rbac-in-azure-sentinel/ba-p/965043). This is useful for teams needing access to only certain data types or tables.

Otherwise, use one of the following options for advanced RBAC:

- For Microsoft Sentinel SIEM access, use [Azure custom roles](/en-us/azure/role-based-access-control/custom-roles).
- For the Microsoft Sentinel data lake, use [Defender XDR unified RBAC custom roles](/en-us/defender-xdr/create-custom-rbac-roles).