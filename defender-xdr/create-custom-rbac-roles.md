---
layout: Conceptual
title: Create custom roles with Microsoft Defender unified role-based access control (RBAC) - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/create-custom-rbac-roles
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Create custom roles in Microsoft Defender unified RBAC and assign specific permissions to users or groups for granular access to Microsoft Defender portal experiences.
ms.service: defender-xdr
ms.author: monaberdugo
author: mberdugo
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.custom: msecd-doc-authoring-1014
ms.topic: how-to
ms.date: 2026-08-31T00:00:00.0000000Z
ms.reviewer: 
ai-usage: ai-assisted
locale: en-us
document_id: 0f54d7c4-3348-d604-492f-244a5ae1acbb
document_version_independent_id: 0f54d7c4-3348-d604-492f-244a5ae1acbb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/create-custom-rbac-roles.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: create-custom-rbac-roles
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/create-custom-rbac-roles.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
platformId: 2976b715-427e-bfb1-c777-4702837cc518
---

# Create custom roles with Microsoft Defender unified role-based access control (RBAC) - Microsoft Defender XDR | Microsoft Learn

This article describes how to create custom roles in Microsoft Defender unified role-based access control (RBAC). Microsoft Defender unified RBAC enables you to create custom roles with specific permissions and assign them to users or groups, allowing for granular control over access to Microsoft Defender portal experiences.

Creating custom roles for [Microsoft Sentinel data lake](https://aka.ms/data-lake-overview) is supported in Preview. Before you begin, make sure you meet the prerequisites listed in this article.

## Prerequisites

To create custom roles in Microsoft Defender unified RBAC, you must be assigned one of the following roles or permissions:

- At leastSecurity Administrator in Microsoft Entra ID.
- All **Authorization** permissions assigned in Microsoft Defender Unified RBAC.

For more information on permissions, see [Permission prerequisites](manage-rbac#permissions-prerequisites).

To create custom roles for the Microsoft Sentinel data lake using the **Security Operations** or **Data operations** permission group, you must have a Log Analytics workspace enabled for Microsoft Sentinel and onboarded to the Defender portal.

- [Onboard Microsoft Sentinel](/en-us/azure/sentinel/quickstart-onboard?tabs=defender-portal)
- [Connect Microsoft Sentinel to the Microsoft Defender portal](/en-us/azure/sentinel/microsoft-sentinel-onboard)

## Create a custom role

The following steps describe how to create custom roles in the Microsoft Defender portal.

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com). In the navigation pane on the side, scroll down and select **Permissions**.
2. On the **Permissions** page, under **Microsoft Defender XDR**, select **Roles** &gt; **Create custom role**.
3. In the wizard that opens, on the **Basics** tab, enter the role name and an optional description, and then select **Next**.
4. On the **Choose permissions** page, select each of the following as needed to configure permissions for that area:

    - **Security operations**: Permissions for roles that manage day-to-day operations and respond to incidents and advisories.
    - **Security posture**: Permissions for roles that manage the organization's security posture and perform Defender Vulnerability Management.
    - **Authorization and settings**: Permissions for roles that modify the portal configurations such as authorization, security settings, and system settings.
    - **Data operations** (Preview): Permissions for managing the organization's security data and controlling advanced analytics permissions. Supported for the **Microsoft Sentinel data lake** data collection.

    Hover over the description column for each permission group for a detailed description of the permissions available in that group.

    An extra **Authorization and settings** side pane slides open for each permission group you select, where you can choose the specific permissions to assign to the role.

    If you select **All read-only permissions**, or **All read and manage permissions**, any new permissions later added to these categories are also automatically assigned under this role.

    For more information, see [Permissions in Microsoft Defender unified role-based access control (RBAC)](custom-permissions-details).
5. When you're done assigning permissions for each selected permission group, select **Apply** and then **Next** to continue configuring the remaining permission groups you selected.

    Note

    If all read-only permissions or all read and manage permissions are assigned, any new permissions added to those permission categories in the future are automatically assigned under this role.

    If you assigned custom permissions and new permissions are added to the same category, you'll need to reassign your roles with the new permissions if needed.
6. After you select your permissions for any relevant permission group, select **Apply** and then **Next** to assign users and data sources.
7. On the **Assign users and data sources** page, select **Add assignment**.

    1. On the **Add assignment** side pane, enter the following details:

        - **Assignment name**: Enter a descriptive name for the assignment.
        - **Employees**: Select Microsoft Entra security groups or individual users to assign users to the role.
        - - **Remote tenant group**: Select one or more GDAP remote tenant groups to assign to this role. Users who are members of the selected remote tenant groups inherit the permissions, data source access, and applicable scopes configured in this assignment. This option enables organizations to extend Microsoft Defender unified RBAC permissions to external tenants through an established GDAP relationship.
        - **Data sources**: Select the **Data sources** drop down and then select the services where the assigned users will have the selected permissions. If you assigned read-only permissions for a single data source, such as Microsoft Defender for Endpoint, the assigned users can't read alerts in the other services, such as Microsoft Defender for Office 365 or Microsoft Defender for Identity.
        - **Data collections**: Users assigned in this assignment can be granted permissions either across all available Sentinel workspaces or only to selected workspaces. For example, if a role with 'Security operations - read only permission' is created, one team may be assigned this role for US-Workspace and UK-Workspace, allowing them to access all alerts from these sources. Another assignment can be created for the same role, providing another team in the organization access to only UK-Workspace alerts from Sentinel UK-Workspace.
    2. Select **Include future data sources automatically** to include all other data sources supported by Microsoft Defender unified RBAC. If this option is selected, any future data sources that are added for unified RBAC support are also automatically added to the assignment.
    3. In the **Data collections** area on the **Add assignments** side pane, the Microsoft Sentinel default data lake is listed by default. Select **Edit** to either remove access to the data lake, or define a custom data lake selection.

    Note

    In Microsoft Defender unified RBAC, you can create as many assignments as needed under the same role with same permissions. For example, you can have an assignment within a role that has access to all data sources and then a separate assignment for a team that only needs access to Endpoint alerts from the Defender for Endpoint data source. This enables maintaining the minimum number of roles.
8. Back on the **Assign users and data sources** page, select **Next** to review the role and assignment details. Select **Submit** to create the role.

## Create a role to access and manage roles and permissions

**Authorization** permissions are the unified RBAC permissions that allow users to view, create, and manage roles and permissions in the Microsoft Defender portal. If you're not at least a Security Administrator in Microsoft Entra ID, you need a role with **Authorization** permissions to access and manage roles and permissions. To create this role:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com) as Security Administrator or higher.
2. In the navigation pane, select **Permissions &gt; Microsoft Defender XDR &gt; Roles &gt; Create custom role**.
3. Enter your role name and description, and then select **Next**.
4. Select **Authorization and settings**, and then on the **Authorization and settings** side pane, select **Select custom permissions**.
5. Under **Authorization**, select one of the following options:

    - **Select all permissions**. Users are able to create and manage roles and permissions.
    - **Read-only**. Users can access and view roles and permissions in a read-only mode.

    For example:

    [![Screenshot of the permissions and roles page](media/create-custom-rbac-roles/m365-defender-rbac-authorization-role.png)](media/create-custom-rbac-roles/m365-defender-rbac-authorization-role.png#lightbox)
6. Select **Apply** and then **Next** to assign users and data sources.
7. Select **Add assignments** and enter the **Assignment name**.
8. To configure the access scope for users assigned with the *Authorization* permission, select one of the following access settings:

    - **Choose all data sources**: Grants users permissions to create and manage roles for all data sources.
    - **Select specific data sources**: Grants users permissions to create and manage roles for a specific data source. For example, select **Microsoft Defender for Endpoint** from the dropdown to grant users the *Authorization* permission for the Microsoft Defender for Endpoint data source only.
    - **Microsoft Sentinel data lake collection**: Grants users the *Authorization* permission for the Microsoft Sentinel data lake data collection.
9. In **Assigned users and groups** – choose the Microsoft Entra security groups or individual users to assign the role to, and select **Add**.
10. Select **Next** to review and finish creating the role and then select **Submit**.

Note

For the Microsoft Defender portal to start enforcing the permissions and assignments configured in your new or imported roles, you need to activate the new Microsoft Defender unified RBAC model. For more information, see [Activate Microsoft Defender unified RBAC](activate-defender-rbac).

## Configure scoped roles for Microsoft Defender for Identity

You can configure scoped access using Microsoft Defender Unified RBAC (URBAC) model for identities managed by Microsoft Defender for Identity (MDI). This allows you to restrict access and visibility to specific Active Directory domains or Organizational units, helping align with team responsibilities and reduce unnecessary data exposure.

For more information, see: [Configure scoped access for Microsoft Defender for Identity](/en-us/defender-for-identity/configure-scoped-access).

## Configure scoped roles for Microsoft Defender for Cloud

You can configure scoped access using the Microsoft Defender Unified RBAC model for resources managed by Microsoft Defender for Cloud. This enables you to limit access and visibility to specific **subscriptions**, **resource groups**, or **individual resources**. By applying scoped roles, you help ensure that team members only see and manage the assets relevant to their responsibilities, reducing unnecessary exposure and improving operational security.

For more information, see: [Manage cloud scopes and unified role-based access control](/en-us/azure/defender-for-cloud/cloud-scopes-unified-rbac?pivots=defender-portal).

## Scoping considerations for Microsoft Defender for Endpoint device groups

Microsoft Defender for Endpoint device groups continue to govern per-device visibility and actions alongside unified RBAC. When you create or import URBAC roles, device group assignments determine which devices assigned users can see and act on. Configure device groups in the Microsoft Defender portal separately from URBAC role assignments to ensure proper scoping.

For more information, see [Create and manage device groups in Microsoft Defender for Endpoint](/en-us/defender-endpoint/machine-groups).

Note

In multi-workspace Microsoft Sentinel environments, URBAC data source selections control access to Sentinel workspace data in the Defender portal. These selections don't change security information and event management (SIEM) access or permissions configured through Azure RBAC for individual workspaces. Azure RBAC continues to govern direct workspace access outside the Defender portal.