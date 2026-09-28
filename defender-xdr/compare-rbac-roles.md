---
layout: Conceptual
title: Map Microsoft Defender unified role-based access control (RBAC) permissions - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/compare-rbac-roles
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Compare permissions and access to Microsoft Defender XDR Security portal experiences using role-based access control (RBAC)
ms.service: defender-xdr
ms.author: monaberdugo
author: mberdugo
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.custom:
- sfi-ga-nochange
ms.topic: concept-article
ms.date: 2026-07-30T00:00:00.0000000Z
ms.reviewer: 
locale: en-us
document_id: 9c491e8a-e592-1f4c-0f2d-183a5dec7c34
document_version_independent_id: 9c491e8a-e592-1f4c-0f2d-183a5dec7c34
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/compare-rbac-roles.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: compare-rbac-roles
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/compare-rbac-roles.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 9e53b337-e1a7-f0bf-31df-05ed4c3eb568
---

# Map Microsoft Defender unified role-based access control (RBAC) permissions - Microsoft Defender XDR | Microsoft Learn

All permissions listed within the Microsoft Defender unified RBAC model align to existing permissions in the individual RBAC models. After you activate the Microsoft Defender unified RBAC model, the permissions and assignments configured in your imported roles replace the existing roles in the individual RBAC models.

This article describes how existing roles and permissions in the available Microsoft Defender workloads and in Microsoft Entra ID map to the roles and permission in the Microsoft Defender unified RBAC model.

Important

Microsoft recommends that you use roles with the fewest permissions. This strategy helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

This article contains tables describing how to map your existing individual RBAC role defintions to the new Microsoft Defender unified RBAC permissions for the following products:

Important

Starting 2025, the Microsoft Defender unified RBAC model is the default permissions model for new Microsoft Defender Endpoint tenants and Microsoft Defender for Identity tenants. These tenants can't export roles and permissions from the old model. Defender for Endpoint or Defender for Identity tenants with roles and permissions assigned or exported prior to this date maintain their old roles and permissions configuration.

Use the tables in the following sections to learn more about how your existing individual RBAC role definitions map to your new Microsoft Defender unified RBAC roles:

- Microsoft Defender for Endpoint and Defender Vulnerability Management
- Microsoft Defender for Office 365
- Microsoft Defender for Identity
- Microsoft Defender for Cloud Apps
- Microsoft Defender for Cloud
- Microsoft Sentinel
- Microsoft Entra Global roles access

## Microsoft Defender for Endpoint and Defender Vulnerability Management

Use the following table to learn how your existing permissions for Microsoft Defender for Endpoint and Defender Vulnerability Management map to the new Microsoft Defender unified RBAC permissions:

| Defender for Endpoint and Defender Vulnerability Management permissions | Microsoft Defender unified RBAC permission |
| --- | --- |
| View data - Security operations | Security operations \ Security data \ Security data basics (read) |
| View data - Defender Vulnerability Management | Security posture \ Posture management \ Vulnerability management (read) |
| Alerts investigation | Security operations \ Security data \ Alerts (manage) |
| Active remediation actions - Security operations | Security operations \ Security data \ Response (manage) |
| Active remediation actions - Defender Vulnerability Management - Exception handling | Security posture \ Posture management \ Exception handling (manage) |
| Active remediation actions - Defender Vulnerability Management - Remediation handling | Security posture \ posture management \ Remediation handling (manage) |
| Active remediation actions - Defender Vulnerability Management - Application handling | Security posture \ Posture management \ Application handling (manage) |
| Defender Vulnerability management – Manage security baselines assessment profiles | Security posture \ posture management \ Security baselines assessment (manage) |
| Live response capabilities | Security operations \ Basic live response (manage) |
| Live response capabilities - advanced | Security operations \ Advanced live response (manage)  Security operations \ Security data \ File collection (manage) |
| Manage security settings in the Security Center | Authorization and settings \ Security settings \ Core security settings (manage)  Authorization and settings\Security settings \ Detection tuning (manage) |
| Manage portal system settings | Authorization and settings \ System setting (Read and manage) |
| Manage endpoint security settings in Microsoft Intune | Not supported - this permission is managed in the Microsoft Intune admin center |

## Microsoft Defender for Office 365

Use the following tables to learn how your existing email and collaboration permissions and protection-related Exchange Online permissions for Defender for Office 365 map to Microsoft Defender unified RBAC permissions:

- Email and collaboration permissions mapping
- Exchange Online permissions mapping

Note

When you activate Defender unified RBAC for the Email & collaboration workload, only source roles and role groups that are actively assigned to at least one user are imported. Built-in roles and role groups without active user assignments aren't imported.

### Email & collaboration permissions mapping

You configured Email & collaboration permissions in the Defender portal at https://security.microsoft.com/emailandcollabpermissions.

| Email & collaboration permission | Type | Microsoft Defender unified RBAC permission |
| --- | --- | --- |
| Global Reader | Role group | Security operations \ Security data \ Security data basics (read)Security operations \ Raw data (Email & collaboration) \ Email & collaboration metadata (read)Security operations \ Security data \ Response (manage)Authorization and settings \ Security settings \ Core security settings (read)Authorization and settings \ System setting (read)Security operations \ Raw data (Email & collaboration) \ Email & collaboration content: Quarantine Emails (read) |
| Organization Management | Role group | Security operations \ Security data \ Security data basics (read)Security operations \ Security data \ Alerts (manage)Security operations \ Raw data (Email & collaboration) \ Email & collaboration metadata (read)Security operations \ Security data \ Response (manage)Security operations \ Security data \ Email advanced actions (manage)Security operations \ Security data \ Email quarantine (manage)Authorization and settings \ Authorization (Read and manage)Authorization and settings \ Security setting (All permissions)Authorization and settings \ System settings (Read and manage)Security operations \ Raw data (Email & collaboration) \ Email & collaboration content: Quarantine Emails (read) |
| Security Administrator | Role group | Security operations \ Security data \ Security data basics (read)Security operations \ Security data \ Alerts (manage)Security operations \ Raw data (Email & collaboration) \ Email & collaboration metadata (read)Security operations \ Security data \ Response (manage)Security operations \ Security data \ Email quarantine (manage)Authorization and settings \ Authorization (read)Authorization and settings \ Security setting (All permissions)Authorization and settings \ System settings (Read and manage)Security operations \ Raw data (Email & collaboration) \ Email & collaboration content: Quarantine Emails (read) |
| Security Reader | Role group | Security operations \ Security data \ Security data basics (read)Security operations \ Raw data (Email & collaboration) \ Email & collaboration metadata (read)Security operations \ Security data \ Response (manage)Authorization and settings \ Security settings \ Core security settings (read)Authorization and settings \ System setting (read)Security operations \ Raw data (Email & collaboration) \ Email & collaboration content: Quarantine Emails (read) |
| Security Operator | Role group | Security operations \ Security data \ Security data basics (read)Security operations \ Security data \ Alerts (manage)Security operations \ Raw data (Email & collaboration) \ Email & collaboration metadata (read)Security operations \ Security data \ Response (manage)Authorization and settings \ Security settings \ Core security settings (read)Authorization and settings \ System setting (read)Security operations \ Raw data (Email & collaboration) \ Email & collaboration content: Quarantine Emails (read) |
| Audit Manager | Role group | Security operations \ Security data \ Security data basics (read) |
| Audit Reader | Role group | Security operations \ Security data \ Security data basics (read) |
| Quarantine Administrator | Role group | Security operations \ Security data \ Email quarantine (manage)Security operations \ Raw data (Email & collaboration) \ Email & collaboration content: Quarantine Emails (read) |
| Security Reader | Role | Security operations \ Security data \ Security data basics (read)Security operations \ Raw data (Email & collaboration) \ Email & collaboration metadata (read)Security operations \ Security data \ Response (manage)Authorization and settings \ Security settings (Read-only)Authorization and settings \ System setting (read)Security operations \ Raw data (Email & collaboration) \ Email & collaboration content: Quarantine Emails (read) |
| Security Administrator | Role | Security operations \ Security data \ Security data basics (read)Security operations \ Security data \ Alerts (manage)Security operations \ Raw data (Email & collaboration) \ Email & collaboration metadata (read)Security operations \ Security data \ Response (manage)Security operations \ Security data \ Email quarantine (manage)Authorization and settings \ Authorization (read)Authorization and settings \ Security setting (All permissions)Authorization and settings \ System settings (Read and manage)Security operations \ Raw data (Email & collaboration) \ Email & collaboration content: Quarantine Emails (read) |
| Audit Logs | Role | Security operations \ Security data \ Security data basics (read) |
| Manage Alerts | Role | Security operations \ Security data \ Security data basics (read)Security operations \ Security data \ Alerts (manage) |
| Preview | Role | Security operations \ Raw data (Email & collaboration) \ Email & collaboration content: All Emails (read) |
| Quarantine | Role | Security operations \ Security data \ Email quarantine (manage)Security operations \ Raw data (Email & collaboration) \ Email & collaboration content: Quarantine Emails (read) |
| Role Management | Role | Authorization and settings \ Authorization (Read and manage) |
| Search and Purge | Role | Security operations \ Security data \ Email advanced actions (manage) |
| View-Only Manage Alerts | Role | Security operations \ Security data \ Security data basics (read) |
| View-Only Recipients | Role | Security operations \ Security data \ Security data basics (read)Security operations \ Raw data (Email & collaboration) \ Email & collaboration metadata (read) |
| View-only Audit Logs | Role | Security operations \ Security data \ Security data basics (read) |
| Compliance Administrator | Role | Security operations \ Security data \ Security data basics (read)Security operations \ Security data \ Alerts (manage) |
| DLP Compliance Management | Role | Security operations \ Security data \ Security data basics (read)Security operations \ Security data \ Alerts (manage) |
| Organization Configuration | Role | Security operations \ Security data \ Security data basics (read)Security operations \ Security data \ Alerts (manage) |
| Record Management | Role | Security operations \ Security data \ Security data basics (read)Security operations \ Security data \ Alerts (manage) |
| Retention Management | Role | Security operations \ Security data \ Security data basics (read)Security operations \ Security data \ Alerts (manage) |
| View-Only DLP Compliance Management | Role | Security operations \ Security data \ Security data basics (read) |
| View-Only Record Management | Role | Security operations \ Security data \ Security data basics (read) |
| View-Only Retention Management | Role | Security operations \ Security data \ Security data basics (read) |

To identify which built-in Microsoft Purview role groups include a given role, see [Roles and role groups in Microsoft Defender for Office 365 and Microsoft Purview](/en-us/defender-office-365/scc-permissions#role-groups-in-microsoft-defender-for-office-365-and-microsoft-purview).

Note

Permissions are mapped at the individual-role level. When an imported assignment is based on a role group, the resulting Microsoft Defender unified RBAC role receives the union of the mapped permissions for the roles assigned to that role group. Depending on how the source permission was assigned, you might see either a role name or a role-group name in the imported Microsoft Defender unified RBAC view.

As a result, Microsoft Purview or custom role groups that aren't listed explicitly in the table can still appear in the imported view if they contain mapped roles. To determine the effective permissions for an unlisted role group, identify its assigned roles using the preceding Microsoft Purview documentation, and combine the corresponding role mappings in the table.

For example, the **Preview** role is assigned by default to the following Microsoft Purview role groups: **Data Investigator**, **eDiscovery Manager**, **Privacy Management**, **Privacy Management Administrators**, **Privacy Management Analysts**, **Privacy Management Contributors**, **Privacy Management Investigators**, **Privacy Management Viewers**, **Subject Rights Request Administrators**, and **Subject Rights Request Approvers**. These role groups can therefore appear in the imported view with the mapped Preview permission. Data Investigator also contains **Search and Purge**, so it additionally receives the mapped Email advanced actions permission.

The **Preview** role maps to **Security operations \ Raw data (Email & collaboration) \ Email & collaboration content: All Emails (read)**. In the Defender unified RBAC experience, selecting this permission—whether through role import or manual role configuration—also selects **Security operations \ Security data \ Security data basics (read)** and **Security operations \ Raw data (Email & collaboration) \ Email & collaboration metadata (read)** as prerequisites. An administrator can review and update the resulting role and its assignments in the Defender unified RBAC role experience as appropriate.

### Exchange Online permissions mapping

You configured protection-related Exchange Online permissions in the Exchange admin center (EAC) at https://admin.exchange.microsoft.com/#/adminRoles.

Note

In the **Activate workloads** experience in the Defender portal, the role groups and roles in the following table are activated under the workload named **Exchange Online permissions**.

| Exchange Online permission | Type | Microsoft Defender unified RBAC permission |
| --- | --- | --- |
| Hygiene Management | Role group | Security operations \ Security data \ Email quarantine (manage)Security operations \ Raw data (Email & collaboration) \ Email & collaboration metadata (read)Authorization and settings \ Security settings \ Core security settings (manage)Authorization and settings \ Security settings \ Detection tuning (manage) |
| Organization Management | Role group | Security operations \ Raw data (email & collaboration) \ Email & collaboration metadata (read)Authorization and settings \ Security settings \ Core security settings (manage)Authorization and settings \ Security settings \ Detection tuning (manage)Authorization and settings \ System settings (Read and manage) |
| Security Administrator | Role group | Authorization and settings \ Security settings \ Detection tuning (manage)Authorization and settings \ System settings (Read and manage) |
| View-Only Organization Management | Role group | Security operations \ Raw data (Email & collaboration) \ Email & collaboration metadata (read)Authorization and settings \ Security settings (Read-only)Authorization and settings \ System settings (Read-only) |
| Tenant AllowBlockList Manager | Role | Authorization and settings \ Security settings \ Detection tuning (manage) |
| View-only Recipients | Role | Security operations \ Raw data (email & collaboration) \ Email & collaboration metadata (read) |
| Security Reader | Role group | Authorization and settings \ Security settings \ Core security settings (read) |
| View-Only Configuration | Role | Authorization and settings \ Security settings \ Core security settings (read) |
| Security Operator | Role group | Authorization and settings \ Security settings \ Detection tuning (manage) |

To identify which built-in Exchange Online role groups include a given role, see [Permissions in Exchange Online](/en-us/exchange/permissions-exo/permissions-exo#role-groups-in-exchange-online).

Note

For the built-in Exchange Online role groups listed in this table, the resulting Microsoft Defender unified RBAC permissions include both the permissions mapped directly from the role group and the mapped permissions for roles assigned to that group. For example, **Hygiene Management** contains **View-Only Configuration** and **View-Only Recipients**, and **View-Only Organization Management** contains those same two roles. As a result, both role groups include the mapped permissions contributed by those roles, including **Email & collaboration metadata (read)** from View-Only Recipients.

Custom Exchange Online role groups can also appear in the imported view when they contain a mapped role. The resulting Microsoft Defender unified RBAC role receives the union of the mapped permissions for those assigned roles. Depending on how the source permission was assigned, you might see either a role name or a role-group name in the imported Microsoft Defender unified RBAC view.

## Microsoft Defender for Identity

Use the following table to learn how your existing permissions for Microsoft Defender for Identity Management map to the new Microsoft Defender unified RBAC permissions:

| Defender for Identity permission | Defender unified RBAC permission |
| --- | --- |
| MDI admin | Security operations \ Security data \ Security data basics (read)  Security operations \ Security data \ Alerts (manage)  Authorization and settings \ Authorization (Read and manage)  Authorization and settings \ Security setting (All permissions)  Authorization and settings \ System settings (Read and manage) |
| MDI user | Security operations \ Security data \ Security data basics (read)  Security operations \ Security data \ Alerts (manage)  Authorization and settings \ Security setting (All permissions)  Authorization and settings \ System setting (read) |
| MDI viewer | Security operations \ Security data \ Security data basics (read)  Authorization and settings \ Security settings \ Core security settings (read)  Authorization and settings \ System setting (read) |

Note

Defender for Identity experiences also adhere to permissions granted from [Microsoft Defender for Cloud Apps](https://security.microsoft.com/cloudapps/permissions/roles). For more information, see [Microsoft Defender for Identity role groups](https://go.microsoft.com/fwlink/?linkid=2202729). Exception: If you configured [Scoped deployment](/en-us/defender-cloud-apps/scoped-deployment) for Microsoft Defender for Identity alerts in Microsoft Defender for Cloud Apps, these permissions don't carry over. You need to explicitly grant the Security operations \ Security data \ Security data basics (read) permissions for the relevant portal users.

## Microsoft Defender for Cloud Apps

Important

- Virtually all app governance experiences are controlled by Microsoft Entra ID roles **only**. The only exception is the [OAuthAppInfo table in advanced hunting](advanced-hunting-oauthappinfo-table). Unified RBAC permissions in Defender for Cloud Apps grant access to the app governance data in this specific table.
- In the [unified alerts and incidents experiences in Defender](investigate-alerts), access to app governance data is controlled by Microsoft Entra ID **only**.

    For more information about permissions in app governance, see [App governance roles](/en-us/defender-cloud-apps/app-governance-get-started#roles).
- [Activating Defender for Cloud Apps integration with Defender unified RBAC](activate-defender-rbac) has the following results:

    - Microsoft Entra ID roles continue to function as normal.
    - The following [built-in scoped roles in Defender for Cloud Apps](/en-us/defender-cloud-apps/manage-admins#roles-and-permissions)are no longer supported:
        - **App/instance admin**
        - **User group admin**
        - **Cloud Discovery global admin**
        - **Cloud Discovery report admin**

| Defender for Cloud Apps permission | Defender unified RBAC permission |
| --- | --- |
| Local Global administrator | Security operations \ Security data \ Security data basics (read)  Security operations \ Security data \ Alerts (manage)  Authorization and settings \ Authorization (all permissions)  Authorization and settings \ Security settings (all permissions)  Authorization and settings \ System settings (all permissions) |
| Local Security operator | Security operations \ Security data \ Security data basics (read)  Security operations \ Security data \ Alerts (manage)  Authorization and settings \ Authorization (read)  Authorization and settings \ Security setting (all permissions)  Authorization and settings \ System setting (read) |
| Local Security reader | Security operations \ Security data \ Security data basics (read)  Authorization and settings \ Authorization (read)  Authorization and settings \ Security settings \ Security settings (read)  Authorization and settings \ System settings (read) |
| Local Compliance administrator | Security operations \ Security data \ Security data basics (read)  Security operations \ Security data \ Alerts (manage)  Authorization and settings \ Authorization (read)  Authorization and settings \ Security settings \ Security settings (all permissions)  Authorization and settings \ System settings (read) |

## Microsoft Defender for Cloud

Unified Role-Based Access Control (uRBAC) lets you manage permissions across Microsoft Defender for Cloud resources using a consistent model. Roles define what actions users can perform and assign roles carefully to maintain least-privilege access.

The following table lists the available uRBAC roles and their permissions.

| Role | Permissions | Description |
| --- | --- | --- |
| **Security data basics**: Security operations / Security data / Security data basics (read) | Read | Access alerts, incidents, investigations, hunting, devices, cloud assets, and reports. Includes cloud inventory and threat protection. |
| **Alerts**: Security operations / Security data / Alerts (manage) | Manage | Manage alerts, investigations, scans, device tags, and packages. Includes cloud threat protection features. |
| **Vulnerability Management**: Security posture / Posture management / Vulnerability management (read) | Read | View vulnerability data: software inventory, weaknesses, missing KBs, baselines, hunting, and devices. Includes data lake (Preview). |
| **Exposure Management**: Security posture / Posture management / Exposure Management (read); Security posture / Posture management / Exposure Management (manage) | Read/Manage | View or manage exposure insights, including Secure Score, recommendations, initiatives, and metrics. |

Note

Roles can be combined for broader access, but always apply least-privilege principles. Some capabilities might require more permissions or feature enablement.

## Microsoft Sentinel

Use the following table to learn how your existing permissions for Microsoft Sentinel map to the new Microsoft Defender unified RBAC permissions:

| Sentinel role | URBAC role | Defender unified RBAC permission |
| --- | --- | --- |
| Sentinel Reader | Defender Unified RBAC Reader | Security operations \ Security data \ Security data basics (read) |
| Sentinel Responder | Defender Unified RBAC Responder | Security operations \ Security data \ Security data basics (read) Security operations \ Security data \ Alerts (manage) Security operations \ Security data \ Response (manage) |
| Sentinel Contributor | Defender Unified RBAC Contributor and Responder | Security operations \ Security data \ Security data basics (read) Security operations \ Security data \ Alerts (manage) Security operations \ Security data \ Response (manage) Authorization and settings \ Detection tuning (manage) |
| N/A | Defender Unified RBAC Scoped Reader | Security operations \ Security data \ Security data basics (read) Applies only to role assignments with Sentinel Scope applied |
| N/A | Defender Unified RBAC Data Manager | Data operations \ Data management \ Data (manage) |

The following roles aren't available in unified RBAC and must be managed in the Azure portal: Microsoft Sentinel Playbook Operator, Automation Contributor, and Workbook Contributor.

### Sample permission mappings of Microsoft Sentinel built-in roles to Microsoft Defender unified RBAC roles

These are examples of the permissions that can be assigned to the users based on their roles in Microsoft Sentinel XDR. As unified RBAC provides the option to have more granular permissions on Microsoft Defender XDR, you can utilize that granularity to separate certain Microsoft Defender permissions on Tier level as well. For example, you can apply Live Response Basic to Tier 1, but Live Response Advanced permission to Tier 2.

If some users need only read access to Microsoft Sentinel SIEM raw data, they can also utilize Log Analytics [Granular RBAC](/en-us/azure/azure-monitor/logs/granular-rbac-log-analytics) functionality to scope access to only specific data saved in Log Analytics workspace. Please note that Granular RBAC will not scope access to Microsoft Sentinel incidents, alerts, watchlists, UEBA, TI, or any other Microsoft Sentinel SIEM features.

| Group | Role | Scope | Notes |
| --- | --- | --- | --- |
| Security Analysts | Microsoft Sentinel Responder | Microsoft Sentinel's Resource Group | View data, incidents, workbooks, and other Microsoft Sentinel resources. Manage incidents (assign, dismiss, etc.) |
| Security Analysts | Microsoft Sentinel Playbook Operator | Microsoft Sentinel's Resource Group (or the Resource Group where Playbooks are stored) | List, view and run playbooks. To attach playbooks to analytics rules, Microsoft Sentinel Contributor role is needed |
| Security Analysts | Security Operator Unified RBAC role | Microsoft Defender portal | View, investigate, and respond to security threats alertsManage Microsoft Defender security settingsList of URBAC permissions equivalent for Security Operator Entra ID role are listed on this link:/defender-xdr/compare-rbac-roles#microsoft-entra-global-roles-access |
| Security Engineer | Microsoft Sentinel Contributor | Microsoft Sentinel's Resource Group | View data, incidents, workbooks, and other Microsoft Sentinel resources. Manage incidents (assign, dismiss, etc.). Create and edit workbooks, analytics rules, and other Microsoft Sentinel resources. |
| Security Engineer | Logic Apps Contributor | Microsoft Sentinel's Resource Group (or the Resource Group where Playbooks are stored) | Run and modify playbooks.Attach playbooks to analytics rules and automation rules. |
| Security Engineer | Monitoring Contributor | Subscription and/or Resource group and/or An existing data collection rule | Create or edit data collection rules |
| Security Engineer | Log Analytics Contributor | Microsoft Sentinel's Resource Group | Use the Search feature |
| Security Engineer | Virtual Machine Contributor Azure Connected Machine Resource Administrator | Virtual machines, virtual machine scale sets Arc-enabled servers | Deploy DCR associations (i.e. to assign rules to the machine) |
| Security Engineer | Template Spec Contributor | Microsoft Sentinel's Resource Group | Deploy v2.0 solutions from Content hub. |
| Security Engineer | Security Administrator Unified RBAC role | Microsoft Defender portal | Monitor security-related policies across Microsoft Defender servicesManage security threats and alertsView reportsList of URBAC permissions equivalent for Security Administrator Entra ID role are listed on this link:/defender-xdr/compare-rbac-roles#microsoft-entra-global-roles-access |
| Security Architect | Microsoft Sentinel Contributor | Microsoft Sentinel's Resource Group | View data, incidents, workbooks, and other Microsoft Sentinel resources. Manage incidents (assign, dismiss, etc.). Create and edit workbooks, analytics rules, and other Microsoft Sentinel resources. |
| Security Architect | User Access Administrator | Microsoft Sentinel's Resource Group | This is privileged role! This permission is needed to onboard Microsoft Sentinel SIEM to Microsoft Defender portal. |
| Security Architect | Security Administrator | Microsoft Entra ID tenant level | This is a privileged role! Users with this role have permissions to manage security-related features in the Microsoft 365 Defender portal, Microsoft Entra ID Protection, Microsoft Entra Authentication, Azure Information Protection, and Microsoft Purview compliance portal.This permission is needed to onboard Microsoft Sentinel SIEM to Microsoft Defender portal, offboard the workspace, or change primary/secondary workspace. |

## Microsoft Entra Global roles access

Users assigned with Microsoft Entra global roles might also have access to the [Microsoft Defender portal](https://security.microsoft.com).

Use this table to learn about the permissions assigned by default for each workload (Defender for Endpoint, Defender Vulnerability Management, Defender for Office and Defender for Identity) in Microsoft Defender unified RBAC to each global Microsoft Entra role.

| Microsoft Entra role | Microsoft Defender unified RBAC assigned permissions for all workloads | Microsoft Defender unified RBAC assigned permissions – workload specific |
| --- | --- | --- |
| Global administrator | Security operations \ Security data \ Security data basics (read)  Security operations \ Security data \ Alerts (manage)  Security operations \ Security data \ Response (manage)  Security posture \ Posture management \ Exposure Management (read)  Security posture \ Posture management \ Exposure Management (manage)  Authorization and settings \ Authorization (Read and manage)  Authorization and settings \ Security settings (All permissions)  Authorization and settings \ System settings (Read and manage) | ***Defender for Endpoint and Defender Vulnerability Management permissions only permissions*** Security operations \ Basic live response (manage)  Security operations \ Advanced live response (manage)  Security operations \ Security data \ File collection (manage)  Security posture \ Posture management \ Vulnerability management (read)  Security posture \ Posture management \ Exception handling (manage)  Security posture \ Posture management \ Remediation handling (manage)  Security posture \ Posture management \ Application handling (manage)  Security posture \ Posture management \ Security baseline assessment (manage) ***Defender for Office only permissions*** Security operations \ Security data \ Email quarantine (manage)  Security operations \ Security data \ Email advanced actions (manage)  Security operations \ Raw data (Email & collaboration) \ Email & collaboration metadata (read)  Security operations \ Raw data (Email & collaboration) \ Email & collaboration content: Quarantine Emails (read) |
| Security administrator | Same as Global administrator | Same as Global administrator |
| Global reader | Security operations \ Security data \ Security data basics (read)  Security posture \ Posture management \ Exposure Management (read) | ***Defender for Endpoint and Defender Vulnerability Management permissions only permissions*** Security posture \ Posture management \ Vulnerability management (read) ***Defender for Office only permissions*** Security operations \ Security data \ Response (manage)  Security operations \ Raw data (Email & collaboration) \ Email & collaboration metadata (read)  Security operations \ Raw data (Email & collaboration) \ Email & collaboration content: Quarantine Emails (read)  Authorization and settings \ Authorization (read) ***Defender for Office and Defender for Identity only permissions*** Authorization and settings \ Security settings \ Core security settings (read)  Authorization and settings \ System settings (read) |
| Security reader | Security operations \ Security data \ Security data basics (read)  Security posture \ Posture management \ Exposure Management (read) | ***Defender for Endpoint and Defender Vulnerability Management permissions only permissions*** Security posture \ Posture management \ Vulnerability management (read) ***Defender for Office only permissions*** Security operations \ Security data \ Response (manage)  Security operations \ Raw data (Email & collaboration) \ Email & collaboration metadata (read)  Security operations \ Raw data (Email & collaboration) \ Email & collaboration content: Quarantine Emails (read) ***Defender for Office and Defender for Identity only permissions*** Authorization and settings \ Security settings \ Core security settings (read)  Authorization and settings \ System settings (read) |
| Security operator | Security operations \ Security data \ Security data basics (read)  Security posture \ Posture management \ Exposure Management (read)  Security operations \ Security data \ Response (manage)  Security posture \ Posture management \ Secure Score (read)  Authorization and settings \ Security settings (All permissions) | ***Defender for Endpoint and Defender Vulnerability Management permissions only permissions*** Security operations \ Security data \ Basic live response (manage)  Security operations \ Security data \ Advanced live response (manage)  Security operations \ Security data \ File collection (manage)  Security posture \ Posture management \ Vulnerability management (read)  Security posture \ Posture management \ Exception handling (manage)  Security posture \ Posture management \ Remediation handling (manage) ***Defender for Office only permissions*** Security operations \ Raw data (Email & collaboration) \ Email & collaboration metadata (read)  Security operations \ Raw data (Email & collaboration) \ Email & collaboration content: Quarantine Emails (read)  Authorization and settings \ System settings (Read and manage) ***Defender for Identity only permissions*** Authorization and settings \ System settings (read) |
| SOC Identity Responder | Security operations \ Security data \ Security data basics (read)  Security operations \ Security data \ Alerts (manage)  Security operations \ Security data \ Response (manage) | not applicable |
| Exchange Administrator | Security posture \ Posture management \ Exposure Management (read)  Security posture \ Posture management \ Exposure Management (manage) | ***Defender for Office only permissions*** Security operations \ Security data \ Security data basics (read)  Security operations \ Raw data (Email & collaboration) \ Email & collaboration metadata (read)  Authorization and settings \ System settings (Read and manage) |
| SharePoint Administrator | Security posture \ Posture management \ Exposure Management (read)  Security posture \ Posture management \ Exposure Management (manage) | not applicable |
| Service Support Administrator | Security posture \ Posture management \ Exposure Management (read) | not applicable |
| User Administrator | Security posture \ Posture management \ Exposure Management (read) | not applicable |
| HelpDesk Administrator | Security posture \ Posture management \ Exposure Management (read) | not applicable |
| Compliance administrator | not applicable | ***Defender for Office only permissions*** Security operations \ Security data \ Security data basics (read)  Security operations \ Security data \ Alerts (manage) |
| Compliance data administrator | not applicable | Same as Compliance administrator |
| Billing admin | not applicable | not applicable |

Note

By activating the Microsoft Defender unified RBAC model, users with the Security Reader and Global Reader roles are granted read-only access to resources from workloads integrated into the model. However, accessing Microsoft Defender for Endpoint device data requires more configuration before Security Reader permissions take effect. For details, see the [Before you begin section](/en-us/defender-endpoint/rbac).