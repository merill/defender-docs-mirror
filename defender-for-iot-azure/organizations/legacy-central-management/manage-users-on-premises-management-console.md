---
layout: Conceptual
title: Create and Manage Users on an On-premises Management Console - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/legacy-central-management/manage-users-on-premises-management-console
breadcrumb_path: ../../breadcrumb/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-iot-blog/bg-p/MicrosoftDefenderIoTBlog
feedback_help_link_type: ask-the-community
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
ms.service: defender-for-iot
author: limwainstein
manager: bagol
ms.author: lwainstein
description: Create and manage users on a Microsoft Defender for IoT on-premises management console.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: e7fbd234-280f-5e2d-2a41-7a440427814d
document_version_independent_id: 6d723d6b-500c-54a3-47a8-783cf54cfa65
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/legacy-central-management/manage-users-on-premises-management-console.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/legacy-central-management/manage-users-on-premises-management-console
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/legacy-central-management/manage-users-on-premises-management-console.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 9817c093-0519-1252-4a0c-cd254a213f71
---

# Create and Manage Users on an On-premises Management Console - Microsoft Defender for IoT | Microsoft Learn

Important

Defender for IoT now recommends using Microsoft cloud services or existing IT infrastructure for central monitoring and sensor management, and [plans to retire the on-premises management console](../whats-new-archive#new-architecture-for-hybrid-and-air-gapped-support) on **January 1st, 2025**.

For more information, see [Deploy hybrid or air-gapped OT sensor management](../ot-deploy/air-gapped-deploy).

Microsoft Defender for IoT provides tools for managing on-premises user access in the [OT network sensor](../manage-users-sensor), and the on-premises management console. Azure users are managed at the Azure subscription level using Azure RBAC. For more information, see [Manage users and user access](../manage-users-overview).

This article describes how to create, edit, and delete on-premises users, change passwords, recover privileged access, integrate with Active Directory, define global access permissions, and control session timeouts on an on-premises management console. Each procedure lists the required permissions as prerequisites.

## Default privileged users

By default, each on-premises management console is installed with the privileged *support* and *cyberx* users, which have access to advanced tools for troubleshooting and setup.

When setting up an on-premises management console for the first time, sign in with one of these privileged users, create an initial user with an **Admin** role, and then create extra users for security analysts and read-only users.

For more information, see [Install OT monitoring software on an on-premises management console](install-software-on-premises-management-console) and [Default privileged on-premises users](../roles-on-premises#default-privileged-on-premises-users).

## Add new on-premises management console users

This procedure describes how to create new users for an on-premises management console.

Note

This procedure is available for the *support* and *cyberx* users, and any user with the **Admin** role.

To add a user:

1. Sign in to the on-premises management console and select **Users** &gt; **+ Add user**.
2. Select **Create user** and then define the following values:

    | Name | Description |
    | --- | --- |
    | **Username** | Enter a username. |
    | **Email** | Enter the user's email address. |
    | **First Name** | Enter the user's first name. |
    | **Last Name** | Enter the user's last name. |
    | **Role** | Select a user role. For more information, see [On-premises user roles](../roles-on-premises#on-premises-user-roles). |
    | **Remote Sites Access Group** | Available for the on-premises management console only.  Select either **All** to assign the user to all global access groups, or **Specific** to assign them to a specific group only, and then select the group from the drop-down list. For more information, see Define global access permission for on-premises users. |
    | **Password** | Select the user type, either **Local** or **Active Directory User**. For local users, enter a password for the user. Password requirements include: - At least eight characters- Both lowercase and uppercase alphabetic characters- At least one number- At least one symbol |

    Tip

    Integrating with Active Directory lets you associate groups of users with specific permission levels. If you want to create users using Active Directory, first configure Active Directory integration on the on-premises management console and then return to this procedure.
3. Select **Save** when you're done.

Your new user is added and is listed on the on-premises management console **Users** page.

To edit a user, select the **Edit**![](../media/manage-users-on-premises-management-console/icon-edit.png) button for the user you want to edit, and change any values as needed.

**To delete a user**:

Warning

Deleting a user is irreversible and cannot be undone.

To delete a user, select the **Delete**![](../media/manage-users-on-premises-management-console/icon-delete.png) button for the user you want to delete.

### Change a user's password

The following steps describe how **Admin** users can change local user passwords. **Admin** users can change passwords for themselves or for other **Security Analyst** or **Read Only** users. Privileged users can change their own passwords, and the passwords for **Admin** users.

Tip

If you need to recover access to a privileged user account, see Recover privileged access to an on-premises management console.

Note

This procedure is available only for the *support* or *cyberx* users, or for users with the **Admin** role.

To reset a user's password on the on-premises management console:

1. Sign into the on-premises management console and select **Users**.
2. On the **Users** page, locate the user whose password needs to be changed.
3. At the right of that user row, select the **Edit**![](../media/manage-users-on-premises-management-console/icon-edit.png) button.
4. In the **Edit user** pane that appears, scroll down to the **Change password** section. Enter and confirm the new password.

    Passwords must be at least 16 characters, contain lowercase and uppercase alphabetic characters, numbers, and one of the following symbols: **#%\*+,-./:=?@[]^\_{}~**
5. Select **Update** when you're done.

### Recover privileged access to an on-premises management console

The following steps describe how to recover either the *support* or *cyberx* user password on an on-premises management console. For more information, see [Default privileged on-premises users](../roles-on-premises#default-privileged-on-premises-users).

Note

This procedure is available for the *support* and *cyberx* users only.

To recover privileged access to an on-premises management console:

1. Start signing in to your on-premises management console. On the sign-in screen, under the **Username** and **Password** fields, select **Password recovery**.
2. In the **Password Recovery** dialog, select either **CyberX** or **Support** from the drop-down menu, and copy the unique identifier code that's displayed to the clipboard.
3. Go the Defender for IoT **Sites and sensors** page in the Azure portal. You might want to open the Azure portal in a new browser tab or window, keeping your on-premises management console open.

    In your Azure portal settings &gt; **Directories + subscriptions**, make sure that you've selected the subscription where your sensors were onboarded to Defender for IoT.
4. In the **Sites and sensors** page, select the **More Actions** drop down menu &gt; **Recover on-premises management console password**.

    ![Screenshot of the recover on-premises management console password option.](../media/how-to-create-and-manage-users/recover-password.png)
5. In the **Recover** dialog that opens, enter the unique identifier that you've copied to the clipboard from your on-premises management console and select **Recover**. A **password\_recovery.zip** file is automatically downloaded.

    All files downloaded from the Azure portal are signed by root of trust so that your machines use signed assets only.
6. Back on the on-premises management console tab, on the **Password recovery** dialog, select **Upload**. Browse to an upload the **password\_recovery.zip** file you downloaded from the Azure portal.

    Note

    If an error message appears, indicating that the file is invalid, you might have had an incorrect subscription selected in your Azure portal settings.

    Return to Azure, and select the settings icon in the top toolbar. On the **Directories + subscriptions** page, make sure that you've selected the subscription where your sensors were onboarded to Defender for IoT. Then repeat the steps in Azure to download the **password\_recovery.zip** file and upload it on the on-premises management console again.
7. Select **Next**. A system-generated password for your on-premises management console appears for you to use for the selected user. Make sure to write down the password as it won't be shown again.
8. Select **Next** again to sign into your on-premises management console.

## Integrate users with Active Directory

Configure an integration between your on-premises management console and Active Directory to:

- Allow Active Directory users to sign in to your on-premises management console
- Use Active Directory groups, with collective permissions assigned to all users in the group

For example, use Active Directory when you have a large number of users that you want to assign Read Only access to, and you want to manage those permissions at the group level.

For more information, see [Microsoft Entra ID support on sensors and on-premises management consoles](../manage-users-overview#microsoft-entra-id-support-on-sensors).

Note

This procedure is available for the *support* and *cyberx* users only, or any user with an **Admin** role.

To integrate with Active Directory:

1. Sign in to your on-premises management console and select **System Settings**.
2. Scroll down to the **Management console integrations** area on the right, and then select **Active Directory**.
3. Select the **Active Directory Integration Enabled** option and enter the following values for an Active Directory server:

    | Field | Description |
    | --- | --- |
    | **Domain Controller FQDN** | The fully qualified domain name (FQDN), exactly as it appears on your LDAP server. For example, enter `host1.subdomain.contoso.com`.  If you encounter an issue with the integration using the FQDN, check your DNS configuration. You can also enter the explicit IP of the LDAP server instead of the FQDN when setting up the integration. |
    | **Domain Controller Port** | The port on which your LDAP is configured. |
    | **Primary Domain** | The domain name, such as `subdomain.contoso.com`, and then select the connection type for your LDAP configuration. Supported connection types include: **LDAPS/NTLMv3** (recommended), **LDAP/NTLMv3**, or **LDAP/SASL-MD5** |
    | **Active Directory Groups** | Select **+ Add** to add an Active Directory group to each permission level listed, as needed. When you enter a group name, make sure that you enter the group name as it's defined in your Active Directory configuration on the LDAP server. Then, make sure to use these groups when creating new sensor users from Active Directory. Supported permission levels include **Read-only**, **Security Analyst**, **Admin**, and **Trusted Domains**. Add groups as **Trusted endpoints** in a separate row from the other Active Directory groups. To add a trusted domain, add the domain name and the connection type of a trusted domain. You can configure trusted endpoints only for users who were defined under users. |

    Select **+ Add Server** to add another server and enter its values as needed, and **Save** when you're done.

    Important

    When entering LDAP parameters:

    - Define values exactly as they appear in Active directory, except for the case.
    - User lowercase only, even if the configuration in Active Directory uses uppercase.
    - LDAP and LDAPS can't be configured for the same domain. However, you can configure each in different domains and then use them at the same time.

    For example:

    ![Screenshot of Active Directory integration configuration on the on-premises management console.](../media/manage-users-on-premises-management-console/active-directory-config-example.png)
4. Create access group rules for on-premises management console users.

    If you configure Active Directory groups for on-premises management console users, you must also create an access group rule for each Active Directory group. Active Directory credentials won't work for on-premises management console users without a corresponding access group rule.

    For more information, see Define global access permission for on-premises users.

## Define global access permission for on-premises users

Large organizations often have a complex user permissions model based on global organizational structures. To manage your on-premises Defender for IoT users, we recommend that you use a global business topology that's based on business units, regions, and sites, and then define user access permissions around those entities.

Create *user access groups* to establish global access control across Defender for IoT on-premises resources. Each access group includes rules about the users that can access specific entities in your business topology, including business units, regions, and sites.

For more information, see [On-premises global access groups](../manage-users-overview#on-premises-global-access-groups).

Note

This procedure is available for the *support* and *cyberx* users, and any user with the **Admin** role.

Before you create access groups, we also recommend that you:

- Plan which users are associated with the access groups that you create. Two options are available for assigning users to access groups:

    - **Assign groups of Active Directory groups**: Verify that you set up an Active Directory instance to integrate with the on-premises management console.
    - **Assign local users**: Verify that you've created local users.

        Users with **Admin** roles have access to all business topology entities by default, and can't be assigned to access groups.
- Carefully set up your business topology. For a rule to be successfully applied, you must assign sensors to zones in the **Site Management** window. For more information, see [Create OT sites and zones on an on-premises management console](sites-and-zones-on-premises).

To create access groups:

1. Sign in to the on-premises management console as user with an **Admin** role.
2. Select **Access Groups** from the left navigation menu, and then select **Add**![](../media/how-to-define-global-user-access-control/add-icon.png) .
3. In the **Add Access Group** dialog box, enter a meaningful name for the access group, with a maximum of 64 characters.
4. Select **ADD RULE**, and then select the business topology options that you want to include in the access group. The options that appear in the **Add Rule** dialog are the entities that you'd created in the **Enterprise View** and **Site Management** pages. For example:

    [![Screenshot of the Add Rule dialog box.](../media/how-to-define-global-user-access-control/add-rule.png)](../media/how-to-define-global-user-access-control/add-rule.png#lightbox)

    If they don't otherwise exist yet, default global business units and regions are created for the first group you create. If you don't select any business units or regions, users in the access group will have access to all business topology entities.

    Each rule can include only one element per type. For example, you can assign one business unit, one region, and one site for each rule. If you want the same users to have access to multiple business units, in different regions, create more rules for the group. When an access group contains several rules, the rule logic aggregates all rules using an AND logic.

    Any rules you create are listed in the **Add Access Group** dialog box, where you can edit them further or delete them as needed. For example:

    [![Screenshot of the Add Access Group dialog box.](../media/how-to-define-global-user-access-control/edit-access-groups.png)](../media/how-to-define-global-user-access-control/edit-access-groups.png#lightbox)
5. Add users with one or both of the following methods:

    - If the **Assign an Active Directory Group** option appears, assign an Active Directory group of users to this access group as needed. For example:

        [![Screenshot of adding an Active Directory group to a Global Access Group.](../media/how-to-define-global-user-access-control/add-access-group.png)](../media/how-to-define-global-user-access-control/add-access-group.png#lightbox)

        If the option doesn't appear, and you want to include Active Directory groups in access groups, make sure that you've included your Active Directory group in your Active Directory integration. For more information, see Integrate users with Active Directory.
    - Add local users to your groups by editing existing users from the **Users** page. On the **Users** page, select the **Edit** button for the user you want to assign to the group, and then update the **Remote Sites Access Group** value for the selected user. For more information, see Add new on-premises management console users.

### Changes to topology entities

If you later modify a topology entity and the change affects the rule logic, the rule is automatically deleted.

If modifications to topology entities affect rule logic so that all rules are deleted, the access group remains but users won't be able to sign in to the on-premises management console. Instead, users are notified to contact their on-premises management console administrator for help with signing in. Edit each affected user (see Add new on-premises management console users) to update their **Remote Sites Access Group** assignment so that they're no longer part of the legacy access group.

## Control user session timeouts

By default, on-premises users are signed out of their sessions after 30 minutes of inactivity. Admin users can use the local CLI to either turn this feature on or off, or to adjust the inactivity thresholds. For more information, see [Work with Defender for IoT CLI commands](../references-work-with-defender-for-iot-cli-commands).

Note

Any changes made to user session timeouts are reset to defaults when you update the software. For more information, see [Update OT monitoring software](../update-ot-software).

Note

This procedure is available for the *support* and *cyberx* users only.

To control on-premises management console user session timeouts:

1. Sign in to your on-premises management console via a terminal and run:

    ```cli
    sudo nano /var/cyberx/properties/authentication.properties
    ```

    The following output appears:

    ```cli
    infinity_session_expiration = true
    session_expiration_default_seconds = 0
    # half an hour in seconds
    session_expiration_admin_seconds = 1800
    session_expiration_security_analyst_seconds = 1800
    session_expiration_read_only_users_seconds = 1800
    certificate_validation = true
    CRL_timeout_seconds = 3
    CRL_retries = 1
    
    ```
2. Do one of the following:

    - To turn off user session timeouts entirely, change `infinity_session_expiration = true` to `infinity_session_expiration = false`. Change it back to turn it back on again.
    - To adjust an inactivity timeout period, adjust one of the following values to the required time, in seconds:

        - `session_expiration_default_seconds` for all users
        - `session_expiration_admin_seconds` for *Admin* users only
        - `session_expiration_security_analyst_seconds` for *Security Analyst* users only
        - `session_expiration_read_only_users_seconds` for *Read Only* users only