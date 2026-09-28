---
layout: Conceptual
title: Configure OT sensor settings from the Azure portal - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/configure-sensor-settings-portal
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
description: Learn how to configure settings for OT network sensors from Microsoft Defender for IoT on the Azure portal.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: de184e1f-1c5e-e56b-c0a0-95fd7c9177b1
document_version_independent_id: 95868215-2455-968e-00e6-c39713422e11
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/configure-sensor-settings-portal.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/configure-sensor-settings-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/configure-sensor-settings-portal.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 97923c96-9510-231c-52e3-11e24cb4fbb0
---

# Configure OT sensor settings from the Azure portal - Microsoft Defender for IoT | Microsoft Learn

After [onboarding an OT sensor](onboard-sensors) a new OT network sensor to Microsoft Defender for IoT, you might want to define several settings directly on the OT sensor console, such as [managing local users on the OT sensor](manage-users-sensor).

The OT sensor settings listed in this article are also available directly from the Azure portal. Use the Azure portal to apply these settings in bulk across multiple cloud-connected OT sensors at a time, or across all cloud-connected OT sensors in a specific site or zone. This article describes how to view and configure view OT network sensor settings from the Azure portal.

Note

The **Sensor settings** page in Defender for IoT is in PREVIEW. The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include other legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

## Prerequisites

To define OT sensor settings, make sure that you have the following:

- **An Azure subscription onboarded to Defender for IoT**. If you need to, [sign up for a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn), and then use the [Quickstart: Get started with Defender for IoT](getting-started) to set up your OT plan.
- **Permissions**:

    - To view settings that others have defined, sign in with a [Security Reader](/en-us/azure/role-based-access-control/built-in-roles#security-reader), [Security admin](/en-us/azure/role-based-access-control/built-in-roles#security-admin), [Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor), or [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) role for the subscription.
    - To define or update settings, sign in with [Security admin](/en-us/azure/role-based-access-control/built-in-roles#security-admin), [Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor), or [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) role.

    For more information, see [Azure user roles and permissions for Defender for IoT](roles-azure).
- **One or more cloud-connected OT network sensors**. For more information, see [Onboard OT sensors to Defender for IoT](onboard-sensors).

## Define a new sensor setting

Define a new setting whenever you want to define a specific configuration for one or more OT network sensors. For example, if you want to define bandwidth caps for all OT sensors in a specific site or zone, or define them for a single OT sensor at a specific location in your network.

**To define a new setting**:

1. In [Defender for IoT](https://portal.azure.com/#view/Microsoft_Azure_IoT_Defender/IoTDefenderDashboard/%7E/Getting_started) on the Azure portal, select **Sites and sensors** &gt; **Sensor settings (Preview)**.
2. On the **Sensor settings (Preview)** page, select **+ Add**, and then use the wizard to define the following values for your setting. Select **Next** when you're done with each tab in the wizard to move to the next step.

    | Tab name | Description |
    | --- | --- |
    | **Basics** | Select the subscription where you want to apply your setting, and your setting type. Enter a meaningful name and an optional description for your setting. |
    | **Setting** | Define the values for your selected setting type.For details about the options available for each setting type, find your selected setting type in the Sensor setting reference below. |
    | **Apply** | Use the **Select sites**, **Select zones**, and **Select sensors** dropdown menus to define where you want to apply your setting. **Important**: Selecting a site or zone applies the setting to all connected OT sensors, including any OT sensors added to the site or zone later on. If you select to apply your settings to an entire site, you don't also need to select its zones or sensors. |
    | **Review and create** | Check the selections made for your setting. If your new setting replaces an existing setting, a ![](media/how-to-manage-individual-sensors/warning-icon.png) warning is shown to indicate the existing setting.When you're satisfied with the setting's configuration, select **Create**. |

Your new setting is now listed on the **Sensor settings (Preview)** page under its setting type, and on the sensor details page for any related OT sensor. Sensor settings are shown as read-only on the sensor details page. For example:

![Screenshot of a sensor details page showing a setting applied.](media/configure-sensor-settings-portal/sensor-details-setting.png)

Tip

You may want to configure exceptions to your settings for a specific OT sensor or zone. In such cases, create an extra setting for the exception.

Settings override each other in a hierarchical manner, so that if your setting is applied to a specific OT sensor, it overrides any related settings that are applied to the entire zone or site. To create an exception for an entire zone, add a setting for that zone to override any related settings applied to the entire site.

## View and edit current OT sensor settings

**To view the current settings already defined for your subscription**:

1. In [Defender for IoT](https://portal.azure.com/#view/Microsoft_Azure_IoT_Defender/IoTDefenderDashboard/%7E/Getting_started) on the Azure portal, select **Sites and sensors** &gt; **Sensor settings (Preview)**

    The **Sensor settings (Preview)** page shows any settings already defined for your subscriptions, listed by setting type. Expand or collapse each type to view detailed configurations. For example:

    ![Screenshot of OT sensor settings on the Azure portal.](media/configure-sensor-settings-portal/view-settings.png)
2. Select a specific setting to view its exact configuration and the site, zones, or individual sensors where the setting is applied.
3. To edit the setting's configuration, select **Edit** and then use the same wizard you used to create the setting to make the updates you need. When you're done, select **Apply** to save your changes.

### Delete an existing OT sensor setting

Warning

Deleting a sensor setting permanently removes that configuration from the selected scope. To restore the setting, you must recreate it.

To delete an OT sensor setting altogether:

1. On the **Sensor settings (Preview)** page, locate the setting you want to delete.
2. Select the **...** options menu at the top-right corner of the setting's card and then select **Delete**.

For example:

![Screenshot of the Delete setting option.](media/configure-sensor-settings-portal/delete-setting.png)

## Edit settings for disconnected OT sensors

The following procedure describes how to edit OT sensor settings when your OT sensor is currently disconnected from Azure, such as during an ongoing security incident.

By default, if you configure any settings from the Azure portal, all settings that are configurable from both the Azure portal and the OT sensor are set to read-only on the OT sensor itself. For example, if you configure a VLAN from the Azure portal, then bandwidth cap, subnet, and VLAN settings are *all* set to read-only, and blocked from modifications on the OT sensor.

If you're in a situation where the OT sensor is disconnected from Azure, and you need to modify one of these settings, you must first gain write access to those settings.

**To gain write access to blocked OT sensor settings**:

1. On the Azure portal, in the **Sensor settings (Preview)** page, locate the setting you want to edit and open it for editing. For more information, see View and edit current OT sensor settings.

    Edit the scope of the setting so that it no longer includes the OT sensor, and any changes you make while the OT sensor is disconnected aren't overwritten when you connect it back to Azure.

    Important

    Settings defined on the Azure portal always override settings defined on the OT sensor.
2. Sign into the affected OT sensor console, and select **Settings &gt; Advanced configurations** &gt; **Azure Remote Config**.
3. In the code box, modify the `block_local_config` value from `1` to `0`, and select **Close**. For example:

    [![Screenshot of the Azure Remote Config option.](media/how-to-manage-individual-sensors/remote-config-sensor.png)](media/how-to-manage-individual-sensors/remote-config-sensor.png#lightbox)

Continue by updating the unblocked sensor setting directly on the OT network sensor console. For more information, see [Manage individual sensors](how-to-manage-individual-sensors).

## OT sensor setting reference

The following subsections describe the individual OT sensor setting types that you can configure from the Azure portal. Each subsection provides field-level details for one setting type.

The available sensor setting types in the **Type** dropdown list are:

- Active Directory
- Bandwidth cap
- NTP
- Local subnets
- VLAN naming
- Public addresses
- Single sign-on
- DHCP ranges

To add a new setting **Type**, select **Sites and sensors** &gt; **Sensor settings**. Select the setting from the **Type** drop down, for example:

![The screenshot shows the sensor settings page with the type dropdown list options.](media/configure-sensor-settings-portal/sensor-settings-type.png)

### Configure Active Directory settings

To configure Active Directory settings from the Azure portal, define values for the following options:

| Name | Description |
| --- | --- |
| **Domain Controller FQDN** | The fully qualified domain name (FQDN), exactly as it appears on your LDAP server. For example, enter `host1.subdomain.contoso.com`.  If you encounter an issue with the integration using the FQDN, check your DNS configuration. You can also enter the explicit IP of the LDAP server instead of the FQDN when setting up the integration. |
| **Domain Controller Port** | The port where your LDAP is configured. For example, use port 636 for LDAPS (SSL) connections. |
| **Primary Domain** | The domain name, such as `subdomain.contoso.com`, and then select the connection type for your LDAP configuration. Supported connection types include: **LDAPS/NTLMv3** (recommended), **LDAP/NTLMv3**, or **LDAP/SASL-MD5** |
| **Active Directory Groups** | Select **+ Add** to add an Active Directory group to each permission level listed, as needed.  When you enter a group name, make sure that you enter the group name exactly as defined in your Active Directory configuration on the LDAP server. You use these group names when adding new sensor users with Active Directory. Supported permission levels include **Read-only**, **Security Analyst**, **Admin**, and **Trusted Domains**. |

Important

When entering LDAP parameters:

- Define values exactly as they appear in Active Directory, except for the case.
- User lowercase characters only, even if the configuration in Active Directory uses uppercase.
- LDAP and LDAPS can't be configured for the same domain. However, you can configure each in different domains and then use them at the same time.

To add another Active Directory server, select **+ Add Server** and define those server values.

### Configure a bandwidth cap

For a bandwidth cap, define the maximum bandwidth you want the sensor to use for outgoing communication from the sensor to the cloud, either in Kbps or Mbps.

**Default**: 1500 Kbps

**Minimum required for a stable connection to Azure**: 350 Kbps. At this minimum setting, connections to the sensor console might be slower than usual.

### Configure NTP settings

To configure an NTP server for your sensor from the Azure portal, define an IP/Domain address of a valid IPv4 NTP server using port 123.

### Configure local subnet settings

To focus the Azure device inventory on devices that are in your OT scope, you need to manually edit the subnet list to include only the locally monitored subnets that are in your OT scope.

Defender for IoT marks subnets in the subnet list as ICS (industrial control system) subnets by default, which means it recognizes these subnets as OT networks. You can edit the ICS subnet setting when you configure subnets in the Azure portal.

Once the subnets are configured, the network location of the devices is shown in the *Network location* (Public preview) column in the Azure device inventory. All of the devices associated with the listed subnets are displayed as *local*, while devices associated with detected subnets not included in the list are displayed as *routed*.

#### Configure subnets in the Azure portal

Use the following steps to configure local subnets in the Azure portal:

1. Under **Local subnets**, review the configured subnets. To focus the device inventory and view local devices in the inventory, delete any subnets that are not in your IoT/OT scope by selecting the options menu (...) on any subnet you want to delete.
2. To modify additional settings, select any subnet and then select **Edit** for the following options:

    - Select **Import subnets** to import a comma-separated list of subnet IP addresses and masks. Select **Export subnets** to export a list of currently configured data, or **Clear all** to start from scratch.
    - Enter values in the **IP Address**, **Mask**, and **Name** fields to add subnet details manually. Select **Add subnet** to add additional subnets as needed.
    - **ICS Subnet** is on by default, which means that Defender for IoT recognizes the subnet as an OT network. To mark a subnet as non-ICS, toggle off **ICS Subnet**.

### Configure VLAN naming settings

To define a VLAN for your OT sensor, enter the VLAN ID and a meaningful name.

Select **Add VLAN** to add more VLANs as needed.

### Configure public address settings

Some internal devices use public IP addresses. Add those public IP addresses to the sensor's public address list so that the sensor includes the devices in inventory and doesn't classify their traffic as internet communication.

1. In the **Settings** tab, type the **IP address** and **Mask** address.

    ![The screenshot shows the Settings tab for adding public addresses to the sensor settings.](media/configure-sensor-settings-portal/sensor-settings-ip-addresses.png)
2. Select **Next**
3. In the **Apply** tab, select sites, and toggle the **Add selection by specific zone/sensor** to optionally apply the IP addresses to specific zones and sensors.
4. Select **Next**.
5. Review the details and select **Create** to add the address to the public addresses list.

### Configure single sign-on settings

Single sign-on (SSO) lets users access the sensor console with one set of credentials across multiple sensors and sites, instead of maintaining separate login credentials for each. To set up SSO for your sensors, see [create SSO configuration](set-up-sso#create-sso-configuration).

### Configure DHCP range settings

Add the range of IP addresses to configure the DHCP settings that can apply to a device that might have multiple IP addresses associated with it.

1. In the **Settings** tab, type the **From** and **To** IP addresses, and optionally enter a **Name**.

    ![The screenshot shows the Settings tab for adding DHCP IP addresses to the sensor settings.](media/configure-sensor-settings-portal/dhcp-ranges.png)
2. To add additional ranges, select **Add range**.
3. Select **Next: Selection**.
4. In the **Apply to** tab, select the sites, and toggle the **Add selection by specific zone/sensor** to optionally apply the IP addresses to specific zones and sensors.
5. Select **Next: Review**.
6. Review the details and select **Save and assign** to add the range of addresses to the DHCP range list.

## Configure a backup server

You can set up a backup server for your OT sensor during its first deployment or later. Use this procedure to confirm the backup server is set up correctly.

A misconfigured backup server might flag normal traffic as malware. This can trigger a [Malware engine alert](alert-engine-messages#malware-engine-alerts). If you see a false **Suspicion of Malicious Activity** alert, check the backup server setup by using the steps below.

**To configure the backup server:**

1. Sign into your OT sensor console and select **System settings** &gt; **Sensor management** &gt; **Advanced configurations**.
2. Select the **Global** category. Ensure the parameter **is\_reduce\_backup\_malware\_enabled** is set to **1** or **true**.
3. Select the **Vulnerability assessment** category. Ensure **backup\_servers** lists the backup server device's IP address.
4. Select the **Ports** category. Ensure that **backup\_known\_ports** lists the port(s) that the backup server uses.
5. Select **Save**.