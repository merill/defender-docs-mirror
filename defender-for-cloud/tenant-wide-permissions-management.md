---
layout: Conceptual
title: Grant and Request Tenant-wide Permissions - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/tenant-wide-permissions-management
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Learn how Global Administrators can grant or request the Azure permissions needed to view organization-wide information in Microsoft Defender for Cloud.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: sfi-ga-nochange, sfi-image-nochange, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 0a185ed0-5585-3b3d-1eed-b0b3a05a3065
document_version_independent_id: c1fbdf6a-fe33-69ca-0fea-4a4b04c301a8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/tenant-wide-permissions-management.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/tenant-wide-permissions-management
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/tenant-wide-permissions-management.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: c29170d0-720c-f0d1-8f76-8ccca43b15b2
---

# Grant and Request Tenant-wide Permissions - Microsoft Defender for Cloud | Microsoft Learn

A user with the Microsoft Entra role of **Global Administrator** might have tenant-wide responsibilities, but lack the Azure permissions to view that organization-wide information in Microsoft Defender for Cloud. Permission elevation is required because Microsoft Entra role assignments don't grant access to Azure resources.

## Grant tenant-wide permissions to yourself

**To assign yourself tenant-level permissions**:

1. If your organization manages resource access with [Microsoft Entra Privileged Identity Management (PIM)](/en-us/azure/active-directory/privileged-identity-management/pim-configure), or any other PIM tool, the global administrator role must be active for the user.
2. As a Global Administrator user without an assignment on the root management group of the tenant, open Defender for Cloud's **Overview** page and select the **tenant-wide visibility** link in the banner.

    [![Enable tenant-level permissions in Microsoft Defender for Cloud.](media/management-groups-roles/enable-tenant-level-permissions-banner.png)](media/management-groups-roles/enable-tenant-level-permissions-banner.png#lightbox)
3. Select the new Azure role to be assigned.

    [![Form for defining the tenant-level permissions to be assigned to your user.](media/management-groups-roles/enable-tenant-level-permissions-form.png)](media/management-groups-roles/enable-tenant-level-permissions-form.png#lightbox)

    Tip

    Generally, the Security Admin role is required to apply policies on the root level, while Security Reader suffices to provide tenant-level visibility. For more information about the permissions granted by these roles, see the [Security Admin built-in role description](/en-us/azure/role-based-access-control/built-in-roles#security-admin) or the [Security Reader built-in role description](/en-us/azure/role-based-access-control/built-in-roles#security-reader).

    For differences between these roles specific to Defender for Cloud, see the table in [Roles and allowed actions](permissions#roles-and-allowed-actions).

    The organizational-wide view is achieved by granting roles on the root management group level of the tenant.
4. Sign out of the Azure portal, and then sign back in again.
5. After you have elevated access, open or refresh Microsoft Defender for Cloud to verify you have visibility into all subscriptions under your Microsoft Entra tenant.

The process of assigning yourself tenant-level permissions performs many operations automatically for you:

- The user's permissions are temporarily elevated.
- Using the new permissions, the user is assigned to the desired Azure RBAC role on the root management group.
- The elevated permissions are removed.

For more information of the Microsoft Entra elevation process, see [Elevate access to manage all Azure subscriptions and management groups](/en-us/azure/role-based-access-control/elevate-access-global-admin).

## Request tenant-wide permissions when yours are insufficient

When you navigate to Defender for Cloud, you might see a banner that alerts you to the fact that your view is limited. If you see this banner, select the banner to send a request to the global administrator for your organization. In the request, you can include the role you'd like to be assigned. The global administrator decides which role to grant.

It's the global administrator's decision whether to accept or reject these requests.

Important

You can only submit one request every seven days.

To request elevated permissions from your global administrator:

1. From the Azure portal, open Microsoft Defender for Cloud.
2. If the banner **You're seeing limited information** is present, select it.

    ![Banner informing a user they can request tenant-wide permissions.](media/management-groups-roles/request-tenant-permissions.png)
3. In the detailed request form, select the desired role and the justification for why you need these permissions.

    ![Details page for requesting tenant-wide permissions from your Azure global administrator.](media/management-groups-roles/request-tenant-permissions-details.png)
4. Select **Request access**.

    An email is sent to the global administrator. The email contains a link to Defender for Cloud where they can approve or reject the request.

    ![Email to the global administrator for new permissions.](media/management-groups-roles/request-tenant-permissions-email.png)

    After the global administrator selects **Review the request** and completes the process, the decision is emailed to the requesting user.

## Remove tenant-wide permissions

To remove permissions from the root tenant group, follow these steps:

1. Go to the Azure portal.
2. In the Azure portal, search for **Management Groups** in the search bar at the top.
3. In the **Management Groups** pane, find and select the **Tenant Root Group** from the list of management groups.
4. Inside the **Tenant Root Group**, from the left menu, select **Access Control (IAM)**.
5. In the **Access Control (IAM)** pane, select **Role assignments**. This option shows a list of all role assignments for the **Tenant Root Group**.
6. Review the role assignments to identify which one you need to remove.
7. Select the role assignment you want to remove (**Security admin** or **Security reader**) and select **Remove**. Be sure that you have the necessary permissions to make changes to role assignments in the **Tenant Root Group**.