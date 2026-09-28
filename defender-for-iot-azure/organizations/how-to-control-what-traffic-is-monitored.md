---
layout: Conceptual
title: Control the OT traffic monitored by Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/how-to-control-what-traffic-is-monitored
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
description: Learn how to control the OT network traffic monitored by Microsoft Defender for IoT.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 8a976e3a-3d84-383f-e1bb-ad06dfede5d3
document_version_independent_id: eb4ed80b-2b6d-d790-9f1d-124ad3b399ac
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/how-to-control-what-traffic-is-monitored.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/how-to-control-what-traffic-is-monitored
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/how-to-control-what-traffic-is-monitored.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 5bd937c1-8a58-4146-45b3-ccd0191f5e71
---

# Control the OT traffic monitored by Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn

This article is one in a series of articles describing the [OT sensor deployment path](ot-deploy/ot-deploy-path) for OT monitoring with Microsoft Defender for IoT.

[![Diagram of a progress bar with Fine-tune OT monitoring highlighted.](media/deployment-paths/progress-fine-tuning-ot-monitoring.png)](media/deployment-paths/progress-fine-tuning-ot-monitoring.png#lightbox)

Microsoft Defender for IoT OT network sensors automatically run deep packet detection for IT and OT traffic, resolving network device data, such as device attributes and behavior.

After installing, activating, and configuring your OT network sensor, use the tools described in this article to analyze the traffic that's detected automatically, add extra subnets if needed, and control the traffic information included in Defender for IoT alerts.

## Prerequisites

Before performing the procedures in this article, you must have:

- An OT network sensor [installed and set up](ot-deploy/install-software-ot-sensor), then [configured and activated as an OT sensor](ot-deploy/activate-deploy-sensor).
- Access to your OT network sensor as an **Admin** user. For more information, see [On-premises users and roles for OT monitoring with Defender for IoT](roles-on-premises).

Installing, configuring, and activating the OT network sensor is performed by your deployment teams.

## Analyze your deployment

After [onboarding an OT network sensor](onboard-sensors) to Microsoft Defender for IoT, validate that your sensor is deployed correctly by analyzing the traffic being monitored.

**To analyze your network**:

1. Sign into your OT sensor as an Admin user and select **System settings** &gt; **Basic** &gt; **Deployment**.
2. Select **Analyze**. The analysis starts, and a tab is shown for each interface that's monitored by the sensor. Each tab shows the subnets detected by the indicated interface.
3. Each interface tab shows the following details:

    - Connection status, indicated by a green or red connection icon in the tab name. For example, an interface tab shown in green, such as *eth1*, indicates that the interface is connected.
    - The total number of detected subnets and VLANs, shown at the top of the tab.
    - The protocols detected on each subnet.
    - The number of unicast addresses detected for each subnet.
    - Whether broadcast traffic is detected for each subnet, indicating a local network.
4. Wait for the analysis to complete, and then check each interface tab to understand whether the interface is monitoring relevant traffic, or needs further fine-tuning.

If the traffic shown on the **Deployment** page isn't what you expect, you might need to fine tune your deployment by changing the sensor's location in the network, or verifying that your monitoring interfaces are connected correctly. If you make any changes and want to analyze the traffic again to see if it's improved, select **Analyze** again to see the updated monitoring state.

## Fine tune your subnet list

After having analyzed the traffic your sensor is monitoring and fine tuning the deployment, you may need to further fine tune your subnet list. Use the following subnet configuration procedure to ensure that your subnets are configured correctly.

While your OT sensor automatically learns your network subnets during the initial deployment, we recommend analyzing the detected traffic and updating the subnets as needed to optimize your map views and device inventory.

You can also use the subnet configuration procedure to define subnet settings, determining how devices are displayed in the [OT sensor device map](how-to-work-with-the-sensor-device-map) and the [Azure device inventory](device-inventory).

- **In the device map**, IT devices are automatically aggregated by subnet, where you can expand and collapse each subnet view to drill down as needed.
- **In the Azure device inventory**, once the subnets have been configured, use the *Network location* (Public preview) filter to view *local* or *routed* devices as defined in your subnets list. All of the devices associated with the listed subnets are displayed as *local*, while devices associated with detected subnets not included in the list will be displayed as *routed*.

While the OT network sensor automatically learns the subnets in your network, we recommend confirming the learned settings and updating them as needed to optimize your map views and device inventory. Any subnets not listed as subnets are treated as external networks.

Tip

When you're ready to start managing your OT sensor settings at scale, define subnets from the Azure portal. Once you apply settings from the Azure portal, settings on the sensor console are read-only. For more information, see [Configure OT sensor settings from the Azure portal (Public preview)](configure-sensor-settings-portal).

**To fine-tune your detected subnets**:

1. Sign into your OT sensor as an Admin user and select **System settings** &gt; **Basic** &gt; **Subnets**. For example:

    ![Screenshot of the Subnets page in the OT sensor settings.](media/how-to-control-what-traffic-is-monitored/define-subnets.png)
2. Update the subnets listed using any of the following options:

    | Name | Description |
    | --- | --- |
    | **Import subnets** | Import a .CSV file of subnet definitions. The subnet information is updated with the information that you imported. If you import an empty field, you lose the data in that field. |
    | **Export subnets** | Export the currently listed subnets to a .CSV file. |
    | **Clear all** | Clear all currently defined subnets. |
    | **Auto subnet learning** | Selected by default. Clear this option to prevent the sensor from detecting your subnets automatically. |
    | **Resolve all Internet traffic as internal/private** | Select to consider all public IP addresses as private, local addresses. If selected, public IP addresses are treated as local addresses, and alerts aren't sent about unauthorized internet activity. This option reduces notifications and alerts received about external addresses. |
    | **IP address** | Define the subnet's IP address. |
    | **Mask** | Define the subnet's IP mask. |
    | **Name** | We recommend that you enter a meaningful name that specifies the subnet's network role. Subnet names can have up to 60 characters. |
    | **Segregated** | Select to show this subnet separately when displaying the device map according to Purdue level. |
    | **Remove subnet** | Select to remove any subnets that aren't related to your IoT/OT network scope. |

    In the subnet grid, subnets marked as **ICS subnet** are recognized as OT networks. The **ICS subnet** setting is read-only in this grid, but if there's an OT subnet not being recognized correctly, you can manually define a subnet as ICS by changing the device type.
3. When you're done, select **Save** to save your updates.

Tip

Once the **Auto subnet learning** setting is disabled and the subnet list has been edited to include only the locally monitored subnets that are in your IoT/OT scope, you can filter the Azure device inventory by *Network location* to view only the devices defined as *local*. For more information, see [View the device inventory](legacy-central-management/how-to-investigate-all-enterprise-sensor-detections-in-a-device-inventory#view-the-device-inventory).

### Manually define a subnet as ICS

If you have an OT subnet that isn't being marked automatically as an ICS subnet by the sensor, edit the device type for any of the devices in the relevant subnet to an ICS or IoT device type. The subnet will then be automatically marked by the sensor as an ICS subnet.

Note

To manually change the subnet to be marked as ICS, change the device type in the device inventory in the OT sensor. In the Azure portal, subnets in the subnet list are marked as ICS by default in the [OT sensor settings for local subnets](configure-sensor-settings-portal#local-subnets).

**To change the device type to manually update the subnet**:

1. Sign in to your OT sensor console and go to **Device inventory**.
2. In the device inventory grid, select a device from the relevant subnet, and then select **Edit** in the toolbar at the top of the page.
3. In the **Type** field, select a device type from the dropdown list that is listed under **ICS** or **IoT**.

The subnet will now be marked as an ICS subnet in the sensor.

For more information, see [Edit device details](how-to-investigate-sensor-detections-in-a-device-inventory#edit-device-details).

## Customize port and VLAN names

Use the port naming and VLAN naming procedures in this section to enrich the device data shown in Defender for IoT by customizing port and VLAN names on your OT network sensors.

For example, you might want to assign a name to a nonreserved port that shows unusually high activity in order to call it out, or to assign a name to a VLAN number in order to identify it quicker.

Note

For cloud-connected sensors, you may eventually start configuring OT sensor settings from the Azure portal. Once you start configuring settings from the Azure portal, the **VLANs** and **Port naming** panes on the OT sensors are read-only. For more information, see [Configure OT sensor settings from the Azure portal](configure-sensor-settings-portal).

### Customize names of detected ports

Defender for IoT automatically assigns names to most universally reserved ports, such as DHCP or HTTP. However, you might want to customize the name of a specific port to highlight it, such as when you're watching a port with unusually high detected activity.

Port names are shown in Defender for IoT when viewing device groups from the [OT sensor device map](how-to-work-with-the-sensor-device-map), or when you create OT sensor reports that include port information.

To customize a port name:

1. Sign into your OT sensor as an **Admin** user.
2. Select **System settings** and then, under **Network monitoring**, select **Port Naming**.
3. In the **Port naming** pane that appears, enter the port number you want to name, the port's protocol, and a meaningful name. Supported protocol values include: **TCP**, **UDP**, and **BOTH**.
4. Select **+ Add port** to customize another port, and **Save** when you're done.

### Customize a VLAN name

VLANs are either discovered automatically by the OT network sensor or added manually. Automatically discovered VLANs can't be edited or deleted, but manually added VLANs require a unique name. If a VLAN isn't explicitly named, the VLAN's number is shown instead.

VLAN's support is based on 802.1q (up to VLAN ID 4094).

To configure VLAN names on an OT network sensor:

1. Sign in to your OT sensor as an **Admin** user.
2. Select **System Settings** and then, under **Network monitoring**, select **VLAN Naming**.
3. In the **VLAN naming** pane that appears, enter a VLAN ID and unique VLAN name. VLAN names can contain up to 50 ASCII characters.
4. Select **+ Add VLAN** to customize another VLAN, and **Save** when you're done.
5. **For Cisco switches**: Add the `monitor session 1 destination interface XX/XX encapsulation dot1q` command to the SPAN port configuration, where *XX/XX* is the name and number of the port.

## Define DNS servers

Enhance device data enrichment by configuring multiple DNS servers to carryout reverse lookups and resolve host names or FQDNs associated with the IP addresses detected in network subnets. For example, if a sensor discovers an IP address, it might query multiple DNS servers to resolve the host name. You need the DNS server address, server port and the subnet addresses.

To define the DNS server lookup:

1. On your OT sensor console, select **System settings** &gt; **Network monitoring** and under **Active Discovery**, select **Reverse DNS Lookup**.
2. Use the **Schedule Reverse Lookup** options to define your scan as in fixed intervals, per hour, or at a specific time.

    If you select **By specific times**, use a 24-hour clock, such as **14:30** for **2:30 PM**. Select the **+** button on the side to add additional, specific times that you want the lookup to run.
3. Select **Add DNS Server**, and then populate your fields as needed to define the following fields:

    - **DNS server address**, which is the DNS server IP address
    - **DNS server port**
    - **Number of labels**, which is the number of domain labels you want to display. To get this value, resolve the network IP address to device FQDNs. You can enter up to 30 characters in this field.
    - **Subnets**, which is the subnets that you want the DNS server to query
4. Toggle on the **Enabled** option at the top to start the reverse lookup query as scheduled, and then select **Save** to finish the configuration.

For more information, see [Configure reverse DNS lookup](configure-reverse-dns-lookup).

### Test the DNS configuration

Use a test device to verify that the reverse DNS lookup settings configured in the Define DNS servers section work as expected.

1. On your sensor console, select **System settings** &gt; **Network monitoring** and under **Active Discovery**, select **Reverse DNS Lookup**.
2. Make sure that the **Enabled** toggle is selected.
3. Select **Test**.
4. In the **DNS reverse lookup test for server** dialog, enter an address in the **Lookup Address** and then select **Test**.

## Configure DHCP address ranges

Your OT network might consist of both static and dynamic IP addresses.

- **Static addresses** are typically found on OT networks through historians, controllers, and network infrastructure devices such as switches and routers.
- **Dynamic IP allocation** is typically implemented on guest networks with laptops, PCs, smartphones, and other portable equipment, using Wi-Fi or LAN physical connections in different locations.

If you're working with dynamic networks, you need to handle IP addresses changes as they occur, by defining DHCP address ranges on each OT network sensor. When an IP address is defined as a DHCP address, Defender for IoT identifies any activity happening on the same device, regardless of IP address changes.

To define DHCP address ranges:

1. Sign into your OT sensor and select **System settings** &gt; **Network monitoring** &gt; **DHCP Ranges**.
2. Do one of the following:

    - To add a single range, select **+ Add range** and enter the IP address range and an optional name for your range.
    - To add multiple ranges, create a .CSV file with columns for the *From*, *To*, and *Name* data for each of your ranges. Select **Import** to import the file to your OT sensor. Range values imported from a .CSV file overwrite any range data currently configured for your sensor.
    - To export currently configured ranges to a .CSV file, select **Export**.
    - To clear all currently configured ranges, select **Clear all**.

    Range names can have up to 256 characters.
3. Select **Save** to save your changes.

## Configure traffic capture filters (advanced)

To reduce alert fatigue and focus your network monitoring on high priority traffic, you may decide to filter the traffic that streams into Defender for IoT at the source. Capture filters are configured via the OT sensor CLI, and allow you to block high-bandwidth traffic at the hardware layer, optimizing both appliance performance and resource usage.

For more information, see [Traffic capture filters](cli-ot-sensor#traffic-capture-filters).