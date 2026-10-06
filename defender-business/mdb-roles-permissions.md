---
layout: Conceptual
title: Assign Security Roles and Permissions in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-business/mdb-roles-permissions
breadcrumb_path: /defender-business/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Assign roles to your cybersecurity team. Learn about these roles and permissions in Defender for Business.
author: chrisda
ms.author: chrisda
ms.topic: how-to
ms.service: defender-business
ms.localizationpriority: medium
ms.date: 2026-07-03T00:00:00.0000000Z
ms.reviewer: efratka, nehabha
ms.collection:
- SMB
- m365-security
- m365solution-mdb-setup
- highpri
- tier1
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 74150dbc-7ba3-c522-a048-fa19f14d089b
document_version_independent_id: 74150dbc-7ba3-c522-a048-fa19f14d089b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-business/mdb-roles-permissions.md
site_name: Docs
depot_name: Learn.defender-business
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdb-roles-permissions
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-business/mdb-roles-permissions.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b11ae577-8d18-47ab-998c-ea182a941e71
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/87b1d24d-826d-4337-90a0-b6c35e4561f2
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 03e51be4-f26d-d07b-827c-9336457340a3
---

# Assign Security Roles and Permissions in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn

This article describes how to assign security roles and permissions in Defender for Business.

![Visual depicting step 3 - assign security roles and permissions in Defender for Business.](media/mdb-setup-step3.png)

Your organization's security team needs certain permissions to perform tasks, such as:

- Configuring Defender for Business
- Onboarding or removing devices
- Viewing reports about devices and threat detections
- Viewing incidents and alerts
- Taking response actions on detected threats

You grant permissions through certain roles in the [Microsoft Entra ID](/en-us/entra/identity/role-based-access-control/manage-roles-portal). You can assign these roles in the Microsoft 365 admin center or in the Microsoft Entra admin center.

## Roles in Defender for Business

The following table describes the main roles that are assigned in Defender for Business.

| Permission level | Description |
| --- | --- |
| **Security Administrator** | Security Administrators can perform the following tasks: <br>- View and manage security policies<br>- View, respond to, and manage alerts<br>- Take response actions on devices with detected threats<br>- View security information and reports<br><br> In general, security admins use the [Microsoft Defender portal](https://security.microsoft.com) to perform security tasks. |
| **Security Reader** | Security Readers can perform the following tasks: <br>- View a list of onboarded devices<br>- View security policies<br>- View alerts and detected threats<br>- View security information and reports<br><br> Security readers can't add or edit security policies, nor can they onboard devices. |

For more information about roles, see the following articles:

- [About admin roles](/en-us/microsoft-365/admin/add-users/about-admin-roles)
- [Security guidelines for assigning roles](/en-us/microsoft-365/admin/add-users/about-admin-roles#security-guidelines-for-assigning-roles)

## View and edit role assignments

Important

Microsoft recommends that you grant people access to only what they need to perform their tasks. This concept is called *least privilege* for permissions. To learn more, see [Best practices for least-privileged access for applications](/en-us/entra/identity-platform/secure-least-privileged-access).

You can use the Microsoft 365 admin center or the Microsoft Entra admin center to view and edit role assignments.

# [Microsoft 365 admin center](#tab/M365Admin)
Use the following steps to open a user account in the Microsoft 365 admin center and manage role assignments:

1. Go to the [Microsoft 365 admin center](https://admin.microsoft.com) and sign in.
2. In the navigation pane, go to **Users** &gt; **Active users**.
3. Select a user account to open their flyout pane.
4. On the **Account** tab, under **Roles**, select **Manage roles**.
5. To add or remove a role, use one of the following procedures:

    | Task | Procedure |
    | --- | --- |
    | Add a role to a user account | 1. Select **Admin center access**, scroll down, and then expand **Show all by category**.<br>    2. Select one of the following roles:<br>        - Security Administrator (listed under **Security & Compliance**)<br>        - Security Reader (listed under **Read-only**)<br>    3. Select **Save changes**. |
    | Remove a role from a user account | 1. Either select **User (no admin center access)** to remove *all* admin roles, or clear the checkbox next to one or more of the assigned roles.<br>    2. Select **Save changes**. |

# [Microsoft Entra admin center](#tab/Entra)
Use the following steps in the Entra admin center to open a user account and manage assigned roles:

1. Go to the [Microsoft Entra admin center](https://entra.microsoft.com/) and sign in.
2. In the navigation pane, go to **Users** &gt; **All users**.
3. Open a user profile by selecting the user account.
4. To add or remove a role, use one of the following procedures:

    | Task | Procedure |
    | --- | --- |
    | Add a role to a user account | 1. Under **Manage**, select **Assigned roles**, and then choose **+ Add assignments**.2. Search for one of the following roles, select it, and then choose **Add** to assign that role to the user account.- Security Administrator- Security Reader |
    | Remove a role from a user account | 1. Under **Manage**, select **Assigned roles**.2. Select one or more administrative roles, and then select **X Remove assignments**. |

---