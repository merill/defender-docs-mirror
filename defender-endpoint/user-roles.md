---
layout: Conceptual
title: Create and manage roles for role-based access control - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/user-roles
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Create roles and define the permissions assigned to the role as part of the role-based access control implementation in the Microsoft Defender XDR
ms.service: defender-endpoint
ms.subservice: onboard
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.custom:
- msecd-doc-authoring-1014
- admindeeplinkDEFENDER
- sfi-ga-nochange
ms.topic: how-to
ms.date: 2026-06-17T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 227628c1-70cb-b9b6-7583-982969221742
document_version_independent_id: 227628c1-70cb-b9b6-7583-982969221742
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/user-roles.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: user-roles
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/user-roles.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 8bd1554c-e4ed-1c41-73da-ddd96baee0d1
---

# Create and manage roles for role-based access control - Microsoft Defender for Endpoint | Microsoft Learn

This article explains how to create, edit, and delete custom roles for role-based access control (RBAC) in Microsoft Defender for Endpoint. You can define permissions for each role and assign the role to Microsoft Entra security groups to control user access to portal features.

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

Important

Starting February 16, 2025, new Microsoft Defender for Endpoint customers will only have access to the Unified Role-Based Access Control (URBAC). Existing customers keep their current roles and permissions. For more information, see URBAC [Unified Role-Based Access Control (URBAC) for Microsoft Defender for Endpoint](/en-us/defender-xdr/manage-rbac)

## Create roles and assign the role to a Microsoft Entra group

Important

Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

The following steps guide you on how to create roles in the Microsoft Defender portal. It assumes that you have already created Microsoft Entra user groups.

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com) using account with the Security Administrator role assigned.
2. In the navigation pane, select **Settings** &gt; **Endpoints** &gt; **Roles** (under **Permissions**).
3. Select **Add role**.
4. Enter the role name, description, and permissions you'd like to assign to the role.
5. Select **Next** to assign the role to a Microsoft Entra Security group.
6. Use the filter to select the Microsoft Entra group that you'd like to add to this role to.
7. **Save and close**.
8. Apply the role and group assignment settings.

Important

After creating roles, you'll need to create a device group and provide access to the device group by assigning it to a role that you created.

Note

Device group creation is supported in Defender for Endpoint Plan 1 and Plan 2.

### Permission options

The following permissions are available when you configure roles:

- **View data**

    - **Security Operations** - View all security operations data in the portal
    - **Defender Vulnerability Management** - View Defender Vulnerability Management data in the portal
- **Active remediation actions**

    - **Security Operations** - Take response actions, approve or dismiss pending remediation actions, manage allowed/blocked lists for automation and indicators
    - **Defender Vulnerability Management - Exception handling** - Create new exceptions and manage active exceptions
    - **Defender Vulnerability Management - Remediation handling** - Submit new remediation requests, create tickets, and manage existing remediation activities
    - **Defender Vulnerability Management - Application handling** - Apply immediate mitigation actions by blocking vulnerable applications, as part of the remediation activity and manage the blocked apps and perform unblock actions
- **Security baselines**

    - **Defender Vulnerability Management – Manage security baselines assessment profiles** - Create and manage profiles so you can assess if your devices comply to security industry baselines.
- **Alerts investigation** - Manage alerts, initiate automated investigations, run scans, collect investigation packages, manage device tags, and download only portable executable (PE) files
- **Manage portal system settings** - Configure storage settings, SIEM, and threat intel API settings (applies globally), advanced settings, automated file uploads, roles, and device groups

    Note

    This setting is only available in the Microsoft Defender for Endpoint Administrator (default) role.
- **Manage security settings in Security Center** - Configure alert suppression settings, manage folder exclusions for automation, onboard and offboard devices, manage email notifications, manage evaluation lab, and manage allowed/blocked lists for indicators
- **Live response capabilities**

    - **Basic**commands:
        - Start a live-response session
        - Perform read-only live-response commands on remote device (excluding file copy and execution)
        - Download a file from the remote device via live response
    - **Advanced**commands:
        - Download PE and non-PE files from the file page
        - Upload a file to the remote device
        - View a script from the files library
        - Execute a script on the remote device from the files library

For more information on the available commands, see [Investigate devices using Live response](live-response).

## Edit roles

To edit an existing role, perform the following steps:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com) using account with the Security administrator role assigned.
2. In the navigation pane, select **Settings** &gt; **Endpoints** &gt; **Roles** (under **Permissions**).
3. Select the role you'd like to edit.
4. Select **Edit**.
5. Modify the details or the groups that are assigned to the role.
6. Select **Save and close**.

## Delete roles

To delete a role that you no longer need, perform the following steps:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com) using account with the Security Administrator role assigned.
2. In the navigation pane, select **Settings** &gt; **Endpoints** &gt; **Roles** (under **Permissions**).
3. Select the role you'd like to delete.
4. Select the drop-down button and select **Delete role**.