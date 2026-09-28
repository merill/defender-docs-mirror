---
layout: Conceptual
title: Manage unified role-based access control in multitenant management - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/mto-urbac
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to view, create, edit, delete, and import roles for unified role-based access control (URBAC) across multiple tenants in the Microsoft Defender portal.
ms.service: defender-xdr
author: guywi-ms
ms.author: guywild
ms.collection:
- m365-security
- highpri
- tier1
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 3a79c53f-c783-c615-5ec5-72b3c92087a6
document_version_independent_id: 3a79c53f-c783-c615-5ec5-72b3c92087a6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/mto-urbac.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mto-urbac
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/mto-urbac.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 9d35e865-ade4-0fe6-3431-59b024ec32cf
---

# Manage unified role-based access control in multitenant management - Microsoft Defender XDR | Microsoft Learn

Use the Microsoft Defender multitenant management portal to manage unified role-based access control (URBAC) across multiple tenants. You can view permissions and access for all your tenants in one place. You can also manage these permissions from a central location. The following sections explain how to view custom roles, create or edit roles, delete roles, and import roles from tenant workloads.

## View custom roles

In the multitenant portal, navigate to the **Permissions & roles page** by selecting **System &gt; Permissions**.

![Screenshot of main Permissions and roles page](media/mto-urbac/urbac-main.png)

From the **Permissions & roles** page, you can create or edit a custom role. You can also import and delete roles. Use the **Search** function to find a specific role. To narrow results, filter roles by data source, permissions category, assignee type, or tenant name.

## Create or edit a custom role (Preview)

You can create a custom role to provide flexibility and control over access to specific data. To create a custom role, follow these steps:

1. Sign in to multitenant management in Microsoft Defender, then navigate to **System &gt; Permissions**.
2. Select **Create custom role**.

    ![Screenshot highlighting the create role option](media/mto-urbac/urbac-create-role.png)
3. In the dropdown menu, select the tenant for which you want to create a new role. Select **Continue**.

    ![Screenshot of the tenant dropdown menu](media/mto-urbac/urbac-create-dropdown.png)
4. In the **Basics** page, enter the name and description of the role. Select **Next**.

    ![Screenshot of the Basics page](media/mto-urbac/urbac-create-basics.png)
5. In the **Permissions** page, select the appropriate permissions for the role.
6. A new pane opens based on the permissions you selected. Select the appropriate permissions for the role, then select **Apply**. Here's an example.

    ![Screenshot of assigning permissions pane](media/mto-urbac/urbac-create-permissions.png)
7. Select **Next** to proceed to the next page.
8. In the **Assignments** page, select **Add assignment** or **Create assignment** to assign users and data sources.
9. In the **Add assignments** pane, enter the assignment name. Add the team members you want to assign. Select the data sources they can access and the identity scopes they need, then select **Add**.

    The following screenshot shows an example of the **Add assignments** pane:

    ![Screenshot of the options in the Add Assignments pane](media/mto-urbac/urbac-create-assignment.png)
10. Select **Next**. Review the details you provided in the **Review and finish** page. You can edit the custom role’s name and description, permissions, and assignments in this page.
11. Select **Submit** to finish creating the custom role.

To edit an existing role, select the three dots beside the role name in the Permissions and roles list, then select **Edit**.

![Screenshot of the Edit option in the Permissions page](media/mto-urbac/urbac-edit-role.png)

## Delete roles (Preview)

Warning

Deleting a role is permanent and removes all access assignments for that role. Review the selected roles carefully before you continue.

To delete roles, select one or more roles from the list. You can choose roles from different tenants, then select **Delete roles**.

![Screenshot highlighting multiple role selection for deletion](media/mto-urbac/urbac-delete-multiple.png)

To delete a single role, select the three dots next to the role name, then select **Delete**.

![Screenshot of the Delete option in the Permissions page](media/mto-urbac/urbac-delete-option.png)

The **Delete role** option is also available when editing a specific role.

![Screenshot highlighting the Delete option in the Edit role pane](media/mto-urbac/urbac-delete-edit-pane.png)

## Import roles (Preview)

You can import existing roles from a tenant’s workloads to migrate permissions and assignments. Imported roles become available in the Permissions and roles list.

To import roles, follow these steps:

1. Navigate to **System &gt; Permissions**.
2. Select **Import roles**.
3. In the **Import roles** pane, select the tenant from which you want to import roles in the dropdown menu. Select **Continue**.
4. In the **Workloads** page, select the workloads you want to import from. Select **Next**.

    ![Screenshot of the Workloads page in the Import role scenario](media/mto-urbac/urbac-import-workload.png)
5. In the **Roles** page, select all or some of the roles that you want to import from the Eligible roles list. To review the permissions and assignments for a role, select the role name. The following screenshot shows an example of the role review pane.

    ![Screenshot of the role review pane in the Import role scenario](media/mto-urbac/urbac-import-review-role.png)
6. Review the details then select **Submit** to finish importing the roles.

To learn more about unified RBAC, see [Microsoft Defender unified role-based access control](/en-us/defender-xdr/manage-rbac).