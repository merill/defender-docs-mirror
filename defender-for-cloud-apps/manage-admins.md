---
layout: Conceptual
title: Configure admin access - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/manage-admins
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: Set up role-based administrator access in Defender for Cloud Apps and understand how Microsoft Entra ID and Microsoft 365 roles affect permissions.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: Naama-Goldbart
ms.custom:
- msecd-doc-authoring-1016
- sfi-ga-blocked
- sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: 4c36e7a7-9036-cba2-291d-01356224910d
document_version_independent_id: 4c36e7a7-9036-cba2-291d-01356224910d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/manage-admins.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: manage-admins
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/manage-admins.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 9b9b9bfc-e2b3-6150-4e73-59369de1bfc6
---

# Configure admin access - Microsoft Defender for Cloud Apps | Microsoft Learn

Microsoft Defender for Cloud Apps supports role-based access control. This article provides instructions for setting access to Defender for Cloud Apps for your admins. For more information about assigning administrator roles, see the articles for [Microsoft Entra ID](/en-us/azure/active-directory/roles/permissions-reference) and [Microsoft 365](/en-us/microsoft-365/admin/add-users/assign-admin-roles).

## Microsoft 365 and Microsoft Entra roles with access to Defender for Cloud Apps

Note

- Microsoft 365 and Microsoft Entra roles aren't listed in the Defender for Cloud Apps **Manage admin access** page. To assign roles in Microsoft 365 or Microsoft Entra ID, go to the relevant RBAC settings for that service.
- Defender for Cloud Apps uses Microsoft Entra ID to determine the user's [directory level inactivity timeout setting](/en-us/azure/azure-portal/set-preferences#change-the-directory-timeout-setting-admin). If a user is configured in Microsoft Entra ID to never sign out when inactive, the same setting applies in Defender for Cloud Apps as well.
- Defender for Cloud Apps Information Protection enablement requires a Microsoft Entra Admin ID, such as: Application Administrator or Cloud Application Administrator. For more details, see [Microsoft Entra built-in roles](/en-us/entra/identity/role-based-access-control/permissions-reference) and [Protect your Microsoft 365 environment](/en-us/defender-cloud-apps/protect-office-365)

Note

As Microsoft Defender moves toward a fully unified identity platform, some Defender for Cloud Apps data pipelines remain separate. Defender for Cloud Apps RBAC scoping uses a separate data pipeline that isn't yet integrated with the [Identity inventory](/en-us/defender-for-identity/identity-inventory). Correlations defined in the Identity inventory don't affect Defender for Cloud Apps scoping. For a full list of affected features, see [Enable Identity inventory integration](/en-us/defender-cloud-apps/general-setup#enable-identity-inventory-integration).

By default, the following Microsoft 365 and [Microsoft Entra ID](/en-us/azure/active-directory/roles/permissions-reference) admin roles have access to Defender for Cloud Apps:

| Role name | Description |
| --- | --- |
| **Security administrator** | Administrators with **Full access** have full permissions in Defender for Cloud Apps. They can add admins, add policies and settings, upload logs and perform governance actions, access and manage SIEM agents. |
| **Cloud App Security administrator** | Allows full access and permissions in Defender for Cloud Apps. This role grants full permissions to Defender for Cloud Apps, like the Microsoft Entra ID **Global administrator** role. However, this role is scoped to Defender for Cloud Apps and doesn't grant full permissions across other Microsoft security products. |
| **Compliance administrator** | Has read-only permissions and can manage alerts. Can't access Security recommendations for cloud platforms. Can create and modify file policies, allow file governance actions, and view all the built-in reports under Data Management. |
| **Compliance data administrator** | Has read-only permissions, can create and modify file policies, allow file governance actions, and view all discovery reports. Can't access Security recommendations for cloud platforms. |
| **Security operator** | Has read-only permissions and can manage alerts. These admins are restricted from doing the following actions: <br>- Create policies or edit and change existing ones<br>- Performing any governance actions<br>- Uploading discovery logs<br>- Banning or approving non-Microsoft apps<br>- Accessing and viewing the IP address range settings page<br>- Accessing and viewing any system settings pages<br>- Accessing and viewing the Discovery settings<br>- Accessing and viewing the App connectors page<br>- Accessing and viewing the Governance log<br>- Accessing and viewing the Manage snapshot reports page |
| **Security reader** | Has read-only permissions and can create API access tokens. These admins are restricted from doing the following actions: <br>Create policies or edit and change existing ones- Performing any governance actions<br>- Uploading discovery logs<br>- Banning or approving non-Microsoft apps<br>- Accessing and viewing the IP address range settings page<br>- Accessing and viewing any system settings pages<br>- Accessing and viewing the Discovery settings<br>- Accessing and viewing the App connectors page<br>- Accessing and viewing the Governance log<br>- Accessing and viewing the Manage snapshot reports page |
| **Global reader** | Has full read-only access to all aspects of Defender for Cloud Apps. Can't change any settings or take any actions. |

^\*^ Microsoft recommends that you use roles with the fewest permissions. Using least-privilege roles helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

Note

Virtually all app governance experiences are controlled by Microsoft Entra ID roles **only**. The only exception is the [OAuthAppInfo table in advanced hunting](/en-us/defender-xdr/advanced-hunting-oauthappinfo-table). [Unified RBAC permissions in Defender for Cloud Apps](/en-us/defender-xdr/compare-rbac-roles#map-microsoft-defender-for-cloud-apps-permissions-to-the-microsoft-defender-xdr-unified-rbac-permissions-preview) grant access to the app governance data in this specific table.

In the [unified alerts and incidents experiences in Defender XDR](/en-us/defender-xdr/investigate-alerts), access to app governance data is controlled by Microsoft Entra ID **only**.

For more information about permissions in app governance, see [App governance roles](app-governance-get-started#roles).

### Roles and permissions

| Permissions | GlobalAdmin | SecurityAdmin | ComplianceAdmin | ComplianceData Admin | SecurityOperator | SecurityReader | GlobalReader | PBI Admin | Cloud AppSecurity admin |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Read alerts | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| Manage alerts | ✔ | ✔ | ✔ | ✔ | ✔ |  |  | ✔ | ✔ |
| Read OAuth applications | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| Perform OAuth application actions | ✔ | ✔ |  |  |  |  |  | ✔ | ✔ |
| Access discovered apps, the cloud app catalog, and other cloud discovery data | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |  | ✔ |
| Configure API connectors | ✔ | ✔ |  |  | ✔ |  |  |  | ✔ |
| Perform cloud discovery actions | ✔ | ✔ |  |  |  |  |  |  | ✔ |
| Access files data and file policies | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| Perform file actions | ✔ | ✔ |  |  |  |  |  | ✔ | ✔ |
| Access governance log | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| Perform governance log actions | ✔ | ✔ |  |  |  |  |  | ✔ | ✔ |
| Access scoped discovery governance log | ✔ | ✔ |  |  |  |  |  |  | ✔ |
| Read policies | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| Perform all policy actions | ✔ | ✔ |  |  |  |  |  | ✔ | ✔ |
| Perform file policy actions | ✔ | ✔ | ✔ | ✔ |  |  |  |  | ✔ |
| Perform OAuth policy actions | ✔ | ✔ |  |  |  |  |  | ✔ | ✔ |
| View manage admin access | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |  | ✔ |
| Manage admins and activity privacy | ✔ | ✔ |  |  |  |  |  |  | ✔ |

## Built-in admin roles in Defender for Cloud Apps

The following specific admin roles can be configured in the Microsoft Defender portal, in the **Permissions &gt; Cloud Apps &gt; Roles** area:

| Role name | Description |
| --- | --- |
| **Global administrator** | Has **Full access** similar to the Microsoft Entra Global Administrator role but only to Defender for Cloud Apps. |
| **Compliance administrator** | Grants the same permissions as the Microsoft Entra Compliance administrator role but only to Defender for Cloud Apps. |
| **Security reader** | Grants the same permissions as the Microsoft Entra Security reader role but only to Defender for Cloud Apps. |
| **Security operator** | Grants the same permissions as the Microsoft Entra Security operator role but only to Defender for Cloud Apps. |
| **App/instance admin** | Has full or read-only permissions to all of the data in Defender for Cloud Apps that deals exclusively with the specific app or instance of an app selected. For example, you give a user admin permission to your Box European instance. The admin sees only data that relates to the Box European instance, whether it's files, activities, policies, behaviors, or alerts: <br>- Activities page - Only activities about the specific app<br>- Alerts/Behaviors - Only relating to the specific app. In some cases, alert/behavior data related to another app if the data is correlated with the specific app. Visibility to alert data related to another app is limited, and there's no access to drill down for more details<br>- Policies - Can view all policies and if assigned full permissions can edit or create only policies that deal exclusively with the app/instance<br>- Accounts page - Only accounts for the specific app/instance<br>- App permissions - Only permissions for the specific app/instance<br>- Files page - Only files from the specific app/instance<br>- Conditional access app control - No permissions<br>- Cloud discovery activity - No permissions<br>- Security extensions - Only permissions for API token with user permissions<br>- Governance actions - Only for the specific app/instance<br>- Security recommendations for cloud platforms - No permissions<br>- IP ranges - No permissions |
| **User group admin** | Has full or read-only permissions to all of the data in Defender for Cloud Apps that deals exclusively with the specific groups assigned to them. For example, if you assign a user admin permissions to the group "Germany - all users", the admin can view and edit information in Defender for Cloud Apps only for that user group. The User group admin has the following access: <br>- Activities page - Only activities about the users in the group<br>- Alerts - Only alerts relating to the users in the group. In some cases, alert data related to another user if the data is correlated with the users in the group. Visibility to alert data related to another users is limited, and there's no access to drill down for more details.<br>- Policies - Can view all policies and if assigned full permissions can edit or create only policies that deal exclusively with users in the group<br>- Accounts page - Only accounts for the specific users in the group<br>- App permissions – No permissions<br>- Files page – No permissions<br>- Conditional access app control - No permissions<br>- Cloud discovery activity - No permissions<br>- Security extensions - Only permissions for API token with users in the group<br>- Governance actions - Only for the specific users in the group<br>- Security recommendations for cloud platforms - No permissions<br>- IP ranges - No permissions<br><br>**Notes**: <br>- To assign groups to user group admins, you must first [import user groups](user-groups) from connected apps.<br>- You can only assign user group admins permissions to imported Microsoft Entra groups. |
| **Cloud Discovery global admin** | Has permission to view and edit all cloud discovery settings and data. The Global Discovery admin has the following access: <br>- Settings: System settings - View only; Cloud Discovery settings - View and edit all (anonymization permissions depend on whether it was allowed during role assignment)<br>- Cloud discovery activity - full permissions<br>- Alerts - view and manage only alerts related to the relevant cloud discovery report<br>- Policies - Can view all policies and can edit or create only cloud discovery policies<br>- Activities page - No permissions<br>- Accounts page - No permissions<br>- App permissions – No permissions<br>- Files page – No permissions<br>- Conditional access app control - No permissions<br>- Security extensions - Creating and deleting their own API tokens<br>- Governance actions - Only Cloud Discovery related actions<br>- Security recommendations for cloud platforms - No permissions<br>- IP ranges - No permissions |
| **Cloud Discovery report admin** | - Settings: System settings - View only; Cloud discovery settings - View all (anonymization permissions depend on whether it was allowed during role assignment)<br>- Cloud discovery activity - read permissions only<br>- Alerts – view only alerts related to the relevant cloud discovery report<br>- Policies - Can view all policies and can create only cloud discovery policies, without the possibility to govern application (tagging, sanction and unsanctioned)<br>- Activities page - No permissions<br>- Accounts page - No permissions<br>- App permissions – No permissions<br>- Files page – No permissions<br>- Conditional access app control - No permissions<br>- Security extensions - Creating and deleting their own API tokens<br>- Governance actions – view only actions related to the relevant cloud discovery report<br>- Security recommendations for cloud platforms - No permissions<br>- IP ranges - No permissions |

Important

Microsoft recommends that you use roles with the fewest permissions. Using least-privilege roles helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

The built-in Defender for Cloud Apps admin roles only provide access permissions to Defender for Cloud Apps.

## Override admin permissions

You can override a user's permissions from Microsoft Entra ID or Microsoft 365. To do so, manually add the user to Defender for Cloud Apps and assign new permissions.

For example, Stephanie is a Security reader in Microsoft Entra ID. To give her **Full access** in Defender for Cloud Apps, add her manually and assign **Full access**. The new role overrides her existing permissions.

You can't override Microsoft Entra roles that already grant Full access (Global administrator, Security administrator, and Cloud App Security administrator).

## Add additional admins

You can add additional admins to Defender for Cloud Apps without adding users to Microsoft Entra administrative roles.

### Prerequisites

- To access the **Manage admin access** page, you must be a member of one of the following groups: Global Administrators, Security Administrators, Compliance Administrators, Compliance Data Administrators, Security Operators, Security Readers, or Global Readers.
- To edit the **Manage admin access** page and grant other users access to Defender for Cloud Apps, you must have at least a Security Administrator role.

Important

Microsoft recommends that you use roles with the fewest permissions. Using least-privilege roles helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

To add additional admins, perform the following steps:

1. In the Microsoft Defender Portal, in the left-hand menu, select **Permissions**.
2. Under **Cloud Apps**, choose **Roles**.

    ![Permissions menu.](media/permissions-menu.png)
3. Select **+Add user** to add the admins who should have access to Defender for Cloud Apps. Provide an email address of a user from inside your organization.

    Note

    If you want to add external Managed Security Service Providers (MSSPs) as administrators for Defender for Cloud Apps, make sure you first invite the MSSPs as guests to your organization.

    ![Screenshot showing the add user dialog to add additional admins in Defender for Cloud Apps.](media/add-admin.png)
4. Next, select the drop-down to set what type of role the admin has. If you select **App/Instance admin**, select the app and instance for the admin to have permissions for.

    Note

    Limited access admins who attempt to access a restricted page or perform a restricted action receive an error that they don't have permission to access the page or perform the action.
5. Select **Add admin**.

## Invite external admins

Defender for Cloud Apps enables you to invite external admins (MSSPs) as administrators of your organization's (MSSP customer) Defender for Cloud Apps service. To add MSSPs, make sure Defender for Cloud Apps is enabled on the MSSPs tenant, and then add the MSSPs as [Microsoft Entra B2B collaboration users](/en-us/azure/active-directory/external-identities/add-users-administrator) in the MSSP customer's Azure portal. Once added, MSSPs can be configured as administrators and assigned any of the roles available in Defender for Cloud Apps.

### To add MSSPs to the MSSP customer Defender for Cloud Apps service

To add MSSPs to the MSSP customer Defender for Cloud Apps service, complete the following steps:

1. Add MSSPs as people outside the organization in the MSSP customer directory using the steps under [Add people outside the organization to the directory](/en-us/azure/active-directory/external-identities/add-users-administrator#add-guest-users-to-the-directory).
2. Add MSSPs and assign an administrator role in the MSSP customer Defender for Cloud Apps using the steps under Add additional admins. Provide the same external email address used when adding them as guests in the MSSP customer directory.

### Access for MSSPs to the MSSP customer Defender for Cloud Apps service

By default, Managed Security Service Providers (MSSPs) access their Defender for Cloud Apps tenant through the following URL: `https://security.microsoft.com`.

MSSPs however, need to access the MSSP customer Microsoft Defender Portal using a tenant-specific URL in the following format: `https://security.microsoft.com/?tid=<tenant_id>`.

To obtain the MSSP customer portal tenant ID and access the tenant-specific URL, complete this procedure:

1. As an MSSP, sign in to Microsoft Entra ID with your credentials.
2. Switch directory to the MSSP customer's tenant.
3. Select **Microsoft Entra ID** &gt; **Properties**. The MSSP customer tenant ID is in the **Tenant ID** field.
4. Access the MSSP customer portal by replacing the `<tenant_id>` value in the following URL: `https://security.microsoft.com/?tid=<tenant_id>`.

## Admin activity auditing

Defender for Cloud Apps lets you export a log of admin sign-in activities and an audit of views of a specific user or alerts carried out as part of an investigation.

To export a log, perform the following steps:

1. In the Microsoft Defender Portal, in the left-hand menu, select **Permissions**.
2. Under **Cloud Apps**, choose **Roles**.
3. In the **Admin roles** page, in the top-right corner, select **Export admin activities**.
4. Specify the required time range.
5. Select **Export**.