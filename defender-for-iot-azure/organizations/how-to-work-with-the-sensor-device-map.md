---
layout: Conceptual
title: Investigate Devices in the OT Sensor Device Map - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/how-to-work-with-the-sensor-device-map
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
description: Learn how to use the device map on an OT sensor which provides a graphical representation of devices and the connections between them.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 240aff51-a197-409a-00b4-b467188762f2
document_version_independent_id: e72e9c80-1d41-a729-caf7-f1c0cefaeada
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/how-to-work-with-the-sensor-device-map.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/how-to-work-with-the-sensor-device-map
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/how-to-work-with-the-sensor-device-map.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: dda8d7e8-fd1f-ef09-1ec1-db18fdfcf0e0
---

# Investigate Devices in the OT Sensor Device Map - Microsoft Defender for IoT | Microsoft Learn

OT device maps provide a graphic representation of the network devices detected by the OT network sensor and the connections between them.

Use a device map to retrieve, analyze, and manage device information, either all at once or by network segment, such as specific interest groups or Purdue layers. If you're working in an air-gapped environment with an OT sensor, use a *zone map* to view devices across all connected OT sensors in a specific zone.

Before you start, make sure you meet the prerequisites, including a deployed and activated OT sensor and the required user permissions.

## Prerequisites

To perform the procedures in this article, make sure that you have:

- An OT network sensor [Install OT sensor software](ot-deploy/install-software-ot-sensor), [configure and activate your OT sensor](ot-deploy/activate-deploy-sensor), with network traffic ingested.
- Access to your OT sensor. Users with the **Viewer** role can view data on the map. To import or export data or edit the map view, you need access as a **Security Analyst** or **Admin** user. For more information, see [On-premises users and roles for OT monitoring with Defender for IoT](roles-on-premises).

To view devices across multiple sensors in a zone, you'll also need an OT sensor installed, activated, and configured, with multiple sensors connected and assigned to sites and zones.

## View devices on OT sensor device map

1. Sign into your OT sensor and select **Device map**. All devices detected by the OT sensor are displayed by default according to [Purdue network architecture](best-practices/understand-network-architecture).

    On the OT sensor's device map:

    - Devices with currently active alerts are highlighted in red
    - Starred devices are those that had been marked as important
    - Devices with no alerts are shown in black, or grey in the zoomed-in connections view

    For example:

    [![Screenshot of a default view of an OT sensor's device map.](media/how-to-work-with-maps/device-map-default.png)](media/how-to-work-with-maps/device-map-default.png#lightbox)
2. Zoom in and select a specific device to view the connections between it and other devices, highlighted in blue.

    When zoomed in, each device shows the following details:

    - The device's host name, IP address, and subnet address, if relevant.
    - The number of currently active alerts on the device.
    - The device type, represented by a various icons.
    - The number of devices grouped in a subnet in an IT network, if relevant. This number of devices is shown in a black circle.
    - Whether the device is newly detected or unauthorized.
3. Right-click a specific device and select **View properties** to drill down further to the **Map View** tab on the device's [View the device inventory](how-to-investigate-sensor-detections-in-a-device-inventory#view-the-device-inventory) page.

### Modify the OT sensor map display

Use any of the following map tools to modify the data shown and how it's displayed:

| Name | Description |
| --- | --- |
| **Refresh map** | Select to refresh the map with updated data. |
| **Notifications** | Select to view and Manage device notifications. |
| **Search by IP / MAC** | Filter the map to display only devices connected to a specific IP or MAC address. |
| **Multicast/broadcast** | Select to edit the filter that shows or hides multicast and broadcast devices. By default, multicast and broadcast traffic is hidden. |
| **Add filter** (Last seen) | Select to filter devices displayed by those shown in a specific time period, from the last five minutes to the last seven days. |
| **Reset filters** | Select to reset the *Last seen* filter. |
| **Highlight** | Select to highlight the devices in a specific built-in device map groups category. Highlighted devices are shown on the map in blue. Use the **Search groups** box to search for device groups to highlight, or expand your group options, and then select the group you want to highlight. |
| **Filter** | Select to filter the map to show only the devices in a specific built-in device map groups category. Use the **Search groups** box to search for device groups, or expand your group options, and then select the group you want to filter by. |
| **Zoom**![](media/how-to-work-with-maps/zoom-in-icon-v2.png) / ![](media/how-to-work-with-maps/zoom-out-icon-v2.png) | Zoom in on the map to view the connections between each device, either using the mouse or the **+**/**-** buttons on the right of the map. |
| **Fit to screen**![](media/how-to-work-with-maps/fit-to-screen-icon.png) | Zooms out to fit all devices on the screen |
| **Fit to selection**![](media/how-to-work-with-maps/fit-to-selection-icon.png) | Zooms out enough to fit all selected devices on the screen |
| **IT/OT Presentation Options**![](media/how-to-work-with-maps/collapse-view-icon.png) | Select **Disable Display IT Networks Groups** to prevent the ability to view IT subnets from an OT sensor device map in the map. This option is selected on by default. |
| **Layout options**![](media/how-to-work-with-maps/layouts-icon-v2.png) | Select one of the following: - **Pin layout**. Select to save device locations if you've dragged them to new places on the map. - **Layout by connection**. Select to view devices organized by their connections. - **Layout by Purdue**. Select to view devices organized by their Purdue layers. |

To see device details, select a device and expand the device details pane on the right. In a device details pane:

- Select **Activity Report** to jump to the device's [data mining queries report](how-to-create-data-mining-queries)
- Select **Event Timeline** to jump to the device's [sensor activity tracking timeline](how-to-track-sensor-activity)
- Select **Device Details** to jump to [View the device inventory](how-to-investigate-sensor-detections-in-a-device-inventory#view-the-device-inventory).

### View IT subnets from an OT sensor device map

By default, IT devices are automatically aggregated by [OT and IoT subnet definitions](../how-to-control-what-traffic-is-monitored#define-ot-and-iot-subnets), so that the map focuses on your local OT and IoT networks.

To expand an IT subnet:

1. Sign into your OT sensor and select **Device map**.
2. Locate your subnet on the map. You might need to zoom in on the map to view a subnet icon, which looks like several machines inside a box. For example:

    ![Screenshot of a subnet device on the device map.](media/how-to-work-with-maps/expand-collapse-subnets.png)
3. Right-click the subnet device on the map and **Expand Network**.
4. In the confirmation message that appears above the map, select **OK**.

To collapse an IT subnet:

1. Sign into your OT sensor and select **Device map**.
2. Select one or more expanded subnets and then select **Collapse All**.

### View traffic details between connected devices

To view traffic details between connected devices:

1. Sign into your OT sensor and select **Device map**.
2. Locate two connected devices on the map. You might need to zoom in on the map to view a device icon, which looks like a monitor.
3. Click on the line connecting two devices on the map and then ![](media/how-to-work-with-maps/expand-pane-icon.png) expand the **Connection Properties** pane on the right. For example:

    [![Screenshot of connection properties on the device map.](media/how-to-work-with-maps/connection-properties.png)](media/how-to-work-with-maps/connection-properties.png#lightbox)
4. In the **Connection Properties** pane, you can view traffic details between the two devices, such as:

    - How long ago the connection was first detected.
    - The IP address of each device.
    - The status of each device.
    - The number of alerts for each device.
    - A chart for total bandwidth.
    - A chart for top traffic by port.

## Create a custom device group

In addition to OT sensor's built-in device groups, create new custom groups as needed to use when highlighting or filtering devices on the map.

1. Either select **+ Create Custom Group** in the toolbar, or right-click a device in the map and then select **Add to custom group**.
2. In the **Add custom group** pane:

    - In the **Name** field, enter a meaningful name for your group, with up to 30 characters.
    - From the **Copy from groups** menu, select any groups you want to copy devices from.
    - From the **Devices** menu, select any extra devices to add to your group.

## Import / export device data

Use one of the following options to import and export device data:

- **Import Devices**. Select to import devices from a pre-configured .CSV file.
- **Export Devices**. Select to export all currently displayed devices, with full details, to a .CSV file.
- **Export Device Summary**. Select to export a high level summary of all currently displayed devices to a .CSV file.

## Edit devices

To edit device properties or perform other actions on a device from the device map:

1. Sign into an OT sensor and select **Device map**.
2. Right-click a device to open the device options menu, and then select any of the following options:

    | Name | Description |
    | --- | --- |
    | **Edit properties** | Opens the edit pane where you can edit device properties, such as authorization, name, description, OS platform, device type, Purdue level and if it is a scanner or programming device. |
    | **View properties** | Opens the device's details page. |
    | **Authorize/Unauthorize** | Changes the device's authorization status. For more information, see [Unauthorized devices in Device inventory](device-inventory#unauthorized-devices). |
    | **Mark as Important / Non-Important** | Changes the device's [important OT devices](device-inventory#important-ot-devices) status, highlighting business critical servers on the map with a star and elsewhere, including OT sensor reports and the Azure device inventory. |
    | **Show Alerts** / **Show Events** | Opens the **Alerts** or **Event Timeline** tab on the device's details page. |
    | **Activity Report** | Generates an activity report for the device for the selected timespan. |
    | **Simulate Attack Vectors** | Generates an attack vector simulation for the selected device. For more information, see [Create attack vector reports](how-to-create-attack-vector-reports). |
    | **Add to custom group** | Creates a new custom group with the selected device. |
    | **Delete** | Deletes the device from the inventory. **Warning:** Deleting a device permanently removes it from the inventory. Make sure you no longer need the device record before proceeding. |

## Merge devices

You might want to merge devices if the OT sensor detected multiple network entities associated with a unique device, such as a PLC with four network cards, or a single laptop with both WiFi and a physical network card.

You can only merge authorized devices. For more information, see [Unauthorized devices in Device inventory](device-inventory#unauthorized-devices).

Important

You can't undo a device merge. If you mistakenly merged two devices, delete the devices and then wait for the sensor to rediscover both.

To merge multiple devices:

1. Sign into your OT sensor and select **Device map**.
2. Select the authorized devices you want to merge by using the SHIFT key to select more than one device, and then right-click and select **Merge**.
3. At the prompt, select **Confirm** to confirm that you want to merge the devices.

The devices are merged, and a confirmation message appears at the top right. Merge events are listed in the OT sensor's event timeline.

## Manage device notifications

As opposed to alerts, which provide details about changes in your traffic that might present a threat to your network, device notifications on an OT sensor device map provide details about network activity that might require your attention, but aren't threats.

For example, you might receive a notification about an inactive device that needs to be reconnected, or removed if it's no longer part of the network.

To view and handle device notifications:

1. Sign into the OT sensor and select **Device map** &gt; **Notifications**.
2. In the **Discovery Notifications** pane on the right, filter notifications as needed by time range, device, subnet, or operating systems.

    For example:

    [![Screenshot of device notifications on an OT sensor's Device map page.](media/how-to-work-with-maps/device-notifications.png)](media/how-to-work-with-maps/device-notifications.png#lightbox)
3. Each notification might have different mitigation options. Do one of the following:

    - Handle one notification at a time, selecting a specific mitigation action, or selecting **Dismiss** to close the notification with no activity.
    - Select **Select All** to show which notifications can be handled together. Clear selections for specific notifications, and then select **Accept All** or **Dismiss All** to handle any remaining selected notifications together.

Note

Selected notifications are automatically resolved if they aren't dismissed or otherwise handled within 14 days. For more information, see the **Auto-resolve** column in Respond to device notifications.

### Handle multiple notifications together

You might have situations where you'd want to handle multiple notifications together, such as:

- IT upgraded the OS across multiple network servers and you want to learn all of the new server versions.
- A group of devices is no longer active, and you want to instruct the OT sensor to remove the devices from the OT sensor.

When you handle multiple notifications together, you might still have remaining notifications that need to be handled manually, such as for new IP addresses or no subnets detected.

### Respond to device notifications

Each device notification type has specific available responses. Use the recommended response for each notification type:

| Type | Description | Available responses | Auto-resolve |
| --- | --- | --- | --- |
| **New IP detected** | A new IP address is associated with the device. This might occur in the following scenarios: - A new or additional IP address was associated with a device already detected, with an existing MAC address. - A new IP address was detected for a device that's using a NetBIOS name.  - An IP address was detected as the management interface for a device associated with a MAC address.  - A new IP address was detected for a device that's using a virtual IP address. | - **Set Additional IP to Device**: Merge the devices - **Replace Existing IP**: Replaces any existing IP address with the new address  - **Dismiss**: Remove the notification. | **Dismiss** |
| **No subnets configured** | No subnets are currently configured in your network.  We recommend configuring subnets for the ability to differentiate between OT and IT devices on the map. | - **Open Subnet Configuration** and [configure subnets](how-to-manage-individual-sensors#update-the-ot-sensor-network-configuration). - **Dismiss**: Remove the notification. | **Dismiss** |
| **Operating system changes** | One or more new operating systems have been associated with the device. | - Select the name of the new OS that you want to associate with the device. - **Dismiss**: Remove the notification. | Set with new operating system only if not already configured manually. If the operating system has already been configured: **Dismiss**. |
| **New subnets** | New subnets were discovered. | - **Learn**: Automatically add the subnet.- **Open Subnet Configuration**: Add all missing subnet information.- **Dismiss**: Remove the notification. | **Dismiss** |

## View a device map for a specific zone

If you're working with an OT sensor with sites and zones configured, device maps are also available for each zone. Before you begin, make sure you have multiple sensors connected and assigned to sites and zones, as described in Prerequisites.

On the OT sensor console, zone maps show all network elements related to a selected zone, including OT sensors, detected devices, and more.

To view a zone map:

1. Sign into an OT sensor and select **Site Management** &gt; **View Zone Map** for the zone you want to view. For example:

    [![Screenshot of default region to default business unit.](media/how-to-work-with-asset-inventory-information/default-region-to-default-business-unit-v2.png)](media/how-to-work-with-asset-inventory-information/default-region-to-default-business-unit-v2.png#lightbox)
2. Use any of the following map tools to change your map display:

    | Name | Description |
    | --- | --- |
    | **Save current arrangement**![](media/how-to-work-with-maps/save-zone-map.png) | Saves any changes you've made in the map display. |
    | **Hide multicast/broadcast addresses**![](media/how-to-work-with-maps/hide-multi-cast-zone-map.png) | Selected by default. Select to show multicast and broadcast devices on the map. |
    | **Present Purdue lines**![](media/how-to-work-with-maps/present-purdue-zone-map.png) | Selected by default. Select to hide Purdue lines on the map. |
    | **Relayout**![](media/how-to-work-with-maps/relayout-zone-map.png) | Select to reorganize the layout by Purdue lines or by zone. |
    | **Scale to fit screen**![](media/how-to-work-with-maps/scale-zone-map.png) | Zooms in or out on the map so that the entire map fits on the screen. |
    | **Search by IP / MAC** | Select a specific IP or MAC address to highlight the device on the map. |
    | **Change to a different zone map**![](media/how-to-work-with-maps/change-zone-map.png) | Select to open the **Change Zone Map** dialog, where you can select a different zone map to view. |
    | **Zoom**![](media/how-to-work-with-maps/zoom-in-icon-v2.png) / ![](media/how-to-work-with-maps/zoom-out-icon-v2.png) | Zoom in on the map to view the connections between each device, either using the mouse or the **+**/**-** buttons on the right of the map. |
3. Zoom in to view more details per devices, such as to view the number of devices grouped in a subnet, or to expand a subnet.
4. Right-click a device and select **View properties** to open a **Device Properties** dialog, with more details about the device.
5. Right-click a device shown in red and select **View alerts** to jump to the **Alerts page**, with alerts filtered only for the selected device.

## Built-in device map groups

The following table lists the device groups available out-of-the-box on the OT sensor **Device map** page. Create extra, custom groups as needed for your organization.

| Group name | Description |
| --- | --- |
| **Attack vector simulations** | Vulnerable devices detected in attack vector reports, where the **Show in Device Map** option is toggled on. For more information, see [Create attack vector reports](how-to-create-attack-vector-reports). |
| **Authorization** | Devices that were either discovered during an initial learning period or were later manually marked as *authorized* devices. |
| **Cross subnet connections** | Devices that communicate from one subnet to another subnet. |
| **Device inventory filters** | Any devices based on a [Device inventory filter](how-to-investigate-sensor-detections-in-a-device-inventory) created in the OT sensor's **Device inventory** page. |
| **Known applications** | Devices that use reserved ports, such as TCP. |
| **Last activity** | Devices grouped by the time frame they were last active, for example: One hour, six hours, one day, or seven days. |
| **Non-standard ports** | Devices that use non-standard ports or ports that haven't been assigned an alias. |
| **Not In Active Directory** | All non-PLC devices that aren't communicating with the Active Directory. |
| **OT protocols** | Devices that handle known OT traffic. |
| **Polling intervals** | Devices grouped by polling intervals. The polling intervals are generated automatically according to cyclic channels or periods. For example, 15.0 seconds, 3.0 seconds, 1.5 seconds, or any other interval. Reviewing this information helps you learn if systems are polling too quickly or slowly. |
| **Programming** | Engineering stations, and programming machines. |
| **Subnets** | Devices that belong to a specific subnet. |
| **VLAN** | Devices associated with a specific VLAN ID. |