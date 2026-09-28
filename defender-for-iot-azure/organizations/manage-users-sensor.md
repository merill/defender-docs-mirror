---
layout: Conceptual
title: Create and manage Users on an OT Network Sensor - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/manage-users-sensor
breadcrumb_path: ../breadcrumb/toc.json
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
description: Create and manage on-premises users on a Microsoft Defender for IoT OT network sensor.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 242c50be-6570-3dd4-2ee5-c4477a60a369
document_version_independent_id: 637bcf10-9f61-aa34-4718-30567699db6f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/manage-users-sensor.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/manage-users-sensor
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/manage-users-sensor.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: c70f004a-8754-4650-4c77-afe1c69d770c
---

# Create and manage Users on an OT Network Sensor - Microsoft Defender for IoT | Microsoft Learn

Microsoft Defender for IoT provides tools for managing on-premises user access in the OT network sensor. Azure users are managed at the Azure subscription level. For more information, see [Defender for IoT user management overview](manage-users-overview).

This article describes how to create, edit, and remove on-premises users directly on an OT network sensor, configure Active Directory integration, and recover privileged access. Some procedures require the **Admin** role or a privileged user account. For details, see the prerequisites listed in each section.

## Default privileged users

By default, each OT network sensor is installed with the privileged *admin* user, which has access to advanced tools for troubleshooting and setup.

When setting up a sensor for the first time, sign in the *admin* user, create an initial user with an **Admin** role, and then create extra users for security analysts and read-only users.

For more information, see [Install and set up your OT sensor](how-to-install-software) and [Default privileged on-premises users](roles-on-premises#default-privileged-on-premises-users).

Sensor versions earlier than 23.1.x also include the *cyberx* and *cyberx\_host* privileged users. In versions 23.1.x and higher, these users are installed, but not enabled by default.

To enable the *cyberx* and *cyberx\_host* users in versions 23.1.x and higher, such as to use them with the [Defender for IoT CLI](references-work-with-defender-for-iot-cli-commands), reset the password. For more information, see Change a sensor user's password.

## Configure an Active Directory connection

We recommend configuring on-premises users on your OT sensor with Active Directory in order to allow Active Directory users to sign in to your sensor and use Active Directory groups, with collective permissions assigned to all users in the group.

For example, use Active Directory when you have a large number of users that you want to assign Read Only access to, and you want to manage those permissions at the group level.

Tip

When you're ready to start managing your OT sensor settings at scale, define Active Directory settings from the Azure portal. Once you apply settings from the Azure portal, settings on the sensor console are read-only. For more information, see [Configure OT sensor settings from the Azure portal (Public preview)](configure-sensor-settings-portal).

To integrate with Active Directory:

1. Sign in to your OT sensor and select **System Settings** &gt; **Integrations** &gt; **Active Directory**.
2. Toggle on the **Active Directory Integration Enabled** option.
3. Enter the following values for your Active Directory server:

    | Name | Description |
    | --- | --- |
    | **Domain Controller FQDN** | The fully qualified domain name (FQDN), exactly as it appears on your LDAP server. For example, enter `host1.subdomain.contoso.com`.  If you encounter an issue with the integration using the FQDN, check your DNS configuration. You can also enter the explicit IP of the LDAP server instead of the FQDN when setting up the integration. |
    | **Domain Controller Port** | The port where your LDAP is configured. For example, use port 636 for LDAPS (SSL) connections. |
    | **Primary Domain** | The domain name, such as `subdomain.contoso.com`, and then select the connection type for your LDAP configuration. Supported connection types include: **LDAPS/NTLMv3** (recommended), **LDAP/NTLMv3**, or **LDAP/SASL-MD5** |
    | **Active Directory Groups** | Select **+ Add** to add an Active Directory group to each permission level listed, as needed.  When you enter a group name, make sure that you enter the group name exactly as it's defined in your Active Directory configuration on the LDAP server. Use these group names when adding new sensor users with Active Directory. Supported permission levels include **Read-only**, **Security Analyst**, **Admin**, and **Trusted Domains**. |

    Important

    When entering LDAP parameters:

    - Define values exactly as they appear in Active Directory, except for the case.
    - User lowercase characters only, even if the configuration in Active Directory uses uppercase.
    - LDAP and LDAPS can't be configured for the same domain. However, you can configure each in different domains and then use them at the same time.
4. To add another Active Directory server, select **+ Add Server** at the top of the page and define those server values.
5. When you've added all your Active Directory servers, select **Save**.

    For example:

    ![Screenshot of the active directory integration configuration on the sensor.](media/manage-users-sensor/active-directory-integration-example.png)

## Add new OT sensor users

This procedure describes how to create new users for a specific OT network sensor.

Note

This procedure is available for the *admin*, *cyberx*, and *cyberx\_host* users, and any user with the **Admin** role.

To add a user:

1. Sign in to the sensor console and select **Users** &gt; **+ Add user**.
2. On the **Create a user | Users** page, enter the following details:

    | Name | Description |
    | --- | --- |
    | **User name** | Enter a meaningful username for the user. |
    | **Email** | Enter the user's email address. |
    | **First Name** | Enter the user's first name. |
    | **Last Name** | Enter the user's last name. |
    | **Role** | Select one of the following user roles: **Admin**, **Security Analyst**, or **Read Only**. For more information, see [On-premises user roles](roles-on-premises#on-premises-user-roles). |
    | **Password** | Select the user type, either **Local** or **Active Directory User**. For local users, enter a password for the user. Password requirements include: - At least eight characters- Both lowercase and uppercase alphabetic characters- At least one number- At least one symbolLocal user passwords can only be modified by **Admin** users. |

    Tip

    Integrating with Active Directory lets you associate groups of users with specific permission levels. If you want to create users using Active Directory, first configure an Active Directory connection and then return to this procedure.
3. Select **Save** when you're done.

Your new user is added and is listed on the sensor **Users** page.

To edit a user, select the **Edit**![](media/manage-users-on-premises-management-console/icon-edit.png) icon for the user you want to edit, and change any values as needed.

Warning

Deleting a user removes that account from the sensor. This action can't be undone. Confirm that the user no longer needs access before you continue.

To delete a user, select the **Delete** button for the user you want to delete.

## Change a sensor user's password

This procedure describes how **Admin** users can change local user passwords. **Admin** users can change passwords for themselves or for other **Security Analyst** or **Read Only** users. Privileged users can change their own passwords, and the passwords for **Admin** users.

Tip

If you need to recover access to a privileged user account, see Recover privileged access to a sensor.

Note

This procedure is available only for the *cyberx*, *admin*, or *cyberx\_host* users, or for users with the **Admin** role.

To change a user's password on a sensor:

1. Sign into the sensor and select **Users**.
2. On the sensor's **Users** page, locate the user whose password needs to be changed.
3. At the right of that user row, select the options (**...**) menu &gt; **Edit** to open the user pane.
4. In the user pane on the right, in the **Change password** area, enter and confirm the new password. If you're changing your own password, you'll also need to enter your current password.

    Password requirements include:

    - At least eight characters
    - Both lowercase and uppercase alphabetic characters
    - At least one number
    - At least one symbol
5. Select **Save** when you're done.

## Recover privileged access to a sensor

This procedure describes how to recover privileged access to a sensor, for the *cyberx*, *admin*, or *cyberx\_host* users. For more information, see [Default privileged on-premises users](roles-on-premises#default-privileged-on-premises-users).

Note

This procedure is available only for the *cyberx*, *admin*, or *cyberx\_host* users.

To recover privileged access to a sensor:

1. Start signing in to the OT network sensor. On the sign-in screen, select the **Reset** link. For example:

    ![Screenshot of the sensor sign-in screen with the Reset password link.](media/manage-users-sensor/reset-privileged-password.png)
2. In the **Reset password** dialog, from the **Choose user** menu, select the user whose password you're recovering, either **Cyberx**, **Admin**, or **CyberX\_host**.
3. Copy the unique identifier code that's shown in the **Reset password identifier** to the clipboard. For example:

    ![Screenshot of the Reset password dialog on the OT sensor.](media/manage-users-sensor/password-recovery-sensor.png)
4. Go the Defender for IoT **Sites and sensors** page in the Azure portal. You might want to open the Azure portal in a new browser tab or window, keeping your sensor tab open.

    In your Azure portal settings &gt; **Directories + subscriptions**, make sure that you've selected the subscription where your sensor was onboarded to Defender for IoT.
5. On the **Sites and sensors** page, locate the sensor that you're working with, and select the options menu (**...**) on the right &gt; **Recover my password**. For example:

    [![Screenshot of the Recover my password option on the Sites and sensors page.](media/manage-users-sensor/recover-my-password.png)](media/manage-users-sensor/recover-my-password.png#lightbox)
6. In the **Recover** dialog that opens, enter the unique identifier that you've copied to the clipboard from your sensor and select **Recover**. A **password\_recovery.zip** file is automatically downloaded.

    All files downloaded from the Azure portal are signed by root of trust so that your machines use signed assets only.
7. Back on the sensor tab, on the **Password recovery** screen, select **Select file**. Navigate to and upload the **password\_recovery.zip** file you'd downloaded earlier from the Azure portal.

    Note

    If an error message appears, indicating that the file is invalid, you might have had an incorrect subscription selected in your Azure portal settings.

    Return to Azure, and select the settings icon in the top toolbar. On the **Directories + subscriptions** page, make sure that you've selected the subscription where your sensor was onboarded to Defender for IoT. Then repeat the steps in Azure to download the **password\_recovery.zip** file and upload it on the sensor again.
8. Select **Next**. A system-generated password for your sensor appears for you to use for the selected user. Make sure to write down the password as it won't be shown again.
9. Select **Next** again to sign into your sensor with the new password.

### Define maximum number of failed sign-ins

Use the OT sensor's CLI access to define the number of maximum failed sign-ins before an OT sensor prevents the user from signing in again from the same IP address.

For more information, see [Defender for IoT CLI users and access](references-work-with-defender-for-iot-cli-commands).

Note

This procedure is available for the *cyberx* user only.

1. Sign into your OT sensor via SSH and run:

    ```bash
    nano /var/cyberx/components/xsense-web/cyberx_web/settings.py
    ```
2. In the **settings.py** file, set the `"MAX_FAILED_LOGINS"` value to the maximum number of failed sign ins you want to define. Make sure that you consider the number of concurrent users in your system.
3. Exit the file and run `sudo monit restart all` to apply your changes.