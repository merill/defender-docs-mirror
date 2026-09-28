---
layout: Conceptual
title: Permissions needed for the site security feature of Microsoft Defender for IoT in the Defender portal - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-iot/set-up-rbac
breadcrumb_path: /defender-for-iot/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Assign the RBAC roles and permissions needed to access site security, Defender for IoT alerts, and vulnerability updates in the Defender portal.
ms.service: defender-for-iot
author: limwainstein
ms.author: lwainstein
ms.localizationpriority: medium
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ms.custom: sfi-ga-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 27103e37-55f3-2aa4-a5c6-585212628af4
document_version_independent_id: 27103e37-55f3-2aa4-a5c6-585212628af4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot/set-up-rbac.md
site_name: Docs
depot_name: Learn.defender-for-iot
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: set-up-rbac
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot/set-up-rbac.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 2400ccad-d38f-8834-45c1-0975ec2328fc
---

# Permissions needed for the site security feature of Microsoft Defender for IoT in the Defender portal - Microsoft Defender for IoT | Microsoft Learn

The Microsoft Defender portal allows granular access to features and data based on user roles and the permissions given to each user with Role-Based Access Control (RBAC).

To access the Microsoft Defender for IoT features in the Defender portal, such as site security, and Defender for IoT specific alerts and vulnerability updates, you need to assign permissions and roles to the correct users.

This article shows you how to set up the new roles and permissions to access the site security and Defender for IoT specific features. Before you begin, make sure you meet the prerequisites.

To make general changes to RBAC roles and permissions that relate to all other areas of Defender for IoT, see [configure general RBAC permissions](configure-permissions).

Important

This article discusses Microsoft Defender for IoT in the Defender portal (Preview).

Some features are not yet available in the Defender portal. If you're interested in these features, or you're an existing customer working on the Azure portal, see the [Defender for IoT on Azure documentation](/en-us/azure/defender-for-iot/organizations/overview).

Learn more about the [Defender for IoT management portals](/en-us/defender-for-iot/microsoft-defender-iot#what-are-the-different-management-portals-for-microsoft-defender-for-iot).

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Prerequisites

- Review [the general prerequisites for Microsoft Defender for IoT](prerequisites).
- Details of all users to be assigned site security permissions.

## Access management options

There are three ways to manage user access to the Defender portal, depending on whether your organization uses Global Microsoft Entra roles, Microsoft Defender unified RBAC, or Microsoft Defender for Endpoint XDR RBAC. Each access-control system listed below has different permission names that allow access to site security:

- [Global Microsoft Entra roles](/en-us/entra/identity/role-based-access-control/permissions-reference).
- [Microsoft Defender unified RBAC](/en-us/defender-xdr/manage-rbac): Use Defender unified role-based access control (RBAC) to manage access to specific data, tasks, and capabilities in the Defender portal.
- [Microsoft Defender for Endpoint XDR RBAC](/en-us/defender-endpoint/user-roles): Use Defender for Endpoint XDR role-based access control (RBAC) to manage access to specific data, tasks, and capabilities in the Defender portal.

The instructions and permission settings listed in this article apply to both Defender unified RBAC and Microsoft Defender for Endpoint RBAC.

## Set up Defender unified RBAC roles for site security

Assign RBAC permissions and roles, based on the RBAC roles and permissions summary, to give users access to site security features:

1. In the Defender portal, select **Settings** &gt; **Microsoft Defender XDR** &gt; **Permissions and roles**.
2. Enable **Endpoints & Vulnerability Management**.
3. Select **Go to Permissions and roles**.
4. Select **Create custom role**.
5. Type a **Role name**, and then select **Next** for Permissions.

    [![Screenshot of the permissions set up page for site security.](media/set-up-rbac/permissions-set-up.png)](media/set-up-rbac/permissions-set-up.png#lightbox)
6. For read permissions, select **Security operations**, and select **Select custom permissions**.
7. In **Security data**, select **Security data basics(read)** and select **Apply**.

    [![Screenshot of the permissions set up page with the specific read permissions chosen for site security.](media/set-up-rbac/permissions-unified-read-options.png)](media/set-up-rbac/permissions-unified-read-options.png#lightbox)
8. For write permissions, in **Authorization and settings**, select **Select custom permissions**.
9. In **Security data**, select **Core security settings (manage)** and select **Apply**.

    [![Screenshot of the permissions set up page with the specific write permissions chosen for site security.](media/set-up-rbac/permissions-choose-options.png)](media/set-up-rbac/permissions-choose-options.png#lightbox)
10. Select **Next** for Assignments.
11. Select **Add assignment**, type a name, choose users and groups and select the Data sources.
12. Select **Add**.
13. Select **Next** to **Review and finish**.
14. Select **Submit**.

## Set up Microsoft Defender for Endpoint XDR RBAC (Version 2) roles for site security

Assign RBAC permissions and roles, based on the RBAC roles and permissions summary for site security, to give users access to site security features:

1. In the Defender portal, select **Settings** &gt; **Endpoints** &gt; **Roles**.
2. Select **Add role**.
3. Type a **Role name**, and a **Description**.
4. Select **Next** for Permissions.

    [![Screenshot of the Microsoft Defender for Endpoint XDR RBAC (version2) permissions set up page for site security.](media/set-up-rbac/permissions-mde-rbac2-add-role.png)](media/set-up-rbac/permissions-mde-rbac2-add-role.png#lightbox)
5. For read permissions, in **View Data**, select **Security Operations**.

    [![Screenshot of the Microsoft Defender for Endpoint XDR RBAC (version2) permissions set up page with the specific read permissions chosen for site security.](media/set-up-rbac/permissions-mde-rbac2-read-options.png)](media/set-up-rbac/permissions-mde-rbac2-read-options.png#lightbox)
6. For write permissions, select **Manage security settings in Security Center**.

    [![Screenshot of the Microsoft Defender for Endpoint XDR RBAC (version2) permissions set up page with the specific read and write permissions chosen for site security.](media/set-up-rbac/permissions-mde-rbac2-write-options.png)](media/set-up-rbac/permissions-mde-rbac2-write-options.png#lightbox)
7. Select **Next**.
8. In **Assigned user groups**, select the user groups from the list to assign to this role.
9. Select **Submit**.

### Summary of RBAC roles and permissions for site security

The following tables summarize the write and read permissions required for site security across the supported RBAC models.

**For Unified RBAC**:

| Write permissions | Read permissions |
| --- | --- |
| **Defender permissions**: Core security settings (manage) under Authorization and Settings and scoped to all device groups. **Entra ID roles**: Global Administrator, Security Administrator, Security Operator and scoped to all device groups. | Write roles (including roles that are non-scoped to all device groups). **Defender permissions**: Security data basics (under Security Operations).**Entra ID roles**: Global Reader, Security Reader. |

**For Microsoft Defender for Endpoint RBAC (version 2)**:

| Write permissions | Read permissions |
| --- | --- |
| **Defender for Endpoint roles**: Manage security settings in Security Center and scoped to all device groups.**Entra ID roles**: Global Administrator, Security Administrator. | Write roles (including roles that are non-scoped to all device groups). **Defender for Endpoint roles**: View data - Security operations (read). **Entra ID roles**: Global Reader, Security Reader. |