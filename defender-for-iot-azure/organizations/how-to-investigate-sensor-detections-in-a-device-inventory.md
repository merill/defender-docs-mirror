---
layout: Conceptual
title: Manage your OT device inventory from a sensor console - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/how-to-investigate-sensor-detections-in-a-device-inventory
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
description: Learn how to view and manage OT devices (assets) from the Device inventory page on a sensor console.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 328598c6-b289-98f7-2064-ff0bb6359be3
document_version_independent_id: 31a52dc5-8fa9-b3c0-fbe4-7675e927c4fd
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/how-to-investigate-sensor-detections-in-a-device-inventory.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/how-to-investigate-sensor-detections-in-a-device-inventory
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/how-to-investigate-sensor-detections-in-a-device-inventory.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 1187c9ca-183a-4558-64ca-9a6547c70ccd
---

# Manage your OT device inventory from a sensor console - Microsoft Defender for IoT | Microsoft Learn

Use the **Device inventory** page from a sensor console to manage all OT and IT devices detected by that console. This article describes how to view, filter, and edit devices in the inventory, export inventory data to CSV, merge duplicate devices, and delete inactive devices.

For more information, see [Devices monitored by Defender for IoT](architecture#devices-monitored-by-defender-for-iot).

Tip

Alternately, view your device inventory from [the Azure portal](how-to-manage-device-inventory-for-organizations).

## View the device inventory

To view devices detected by your OT sensor, use the **Device inventory** page.

1. Sign-in to your OT sensor console, and then select **Device inventory**.

    [![Screenshot of the sensor console's Device inventory page.](media/how-to-work-with-asset-inventory-information/sensor-device-inventory.png)](media/how-to-work-with-asset-inventory-information/sensor-device-inventory.png#lightbox)

    Use any of the following options to modify or filter the devices shown:

    | Option | Steps |
    | --- | --- |
    | **Sort devices** | Select a column header to sort the devices by that column. |
    | **Filter devices shown** | Select **Add filter** to filter the devices shown. In the **Add filter** box, define your filter by column name, operator, and filter value. Select **Apply** to apply your filter.You can apply multiple filters at the same time. Search results and filters aren't saved when you refresh the **Device inventory** page. |
    | **Save a filter** | To save the current set of filters:1. Select **+Save Filter**. 2. In the **Create New Device Inventory Filter** pane on the right, enter a name for your filter, and then select **Submit**. Saved filters are also saved as **Device map** groups, and provides extra granularity when [viewing network devices](how-to-work-with-the-sensor-device-map) on the **Device map** page. |
    | **Load a saved filter** | If you have predefined filters saved, load them by selecting the **show side pane**![](media/how-to-inventory-sensor/show-side-pane.png) button, and then select the filter you want to load. |
    | **Modify columns shown** | Select **Edit Columns**![](media/how-to-manage-device-inventory-on-the-cloud/edit-columns-icon.png) . In the **Edit columns** pane: - Select **Add Column** to add new columns to the grid - Drag and drop fields to change the columns order.- To remove a column, select the **Delete**![](media/how-to-manage-device-inventory-on-the-cloud/trashcan-icon.png) icon to the right.- To reset the columns to their default settings, select **Reset**![](media/how-to-manage-device-inventory-on-the-cloud/reset-icon.png) . Select **Save** to save any changes made. |
2. Select a device row to view more details about that device. Initial details are shown in a pane on the right, where you can also select **View full details** to drill down more.

    For example:

    [![Screenshot of the Device inventory page on an OT sensor console.](media/how-to-inventory-sensor/sensor-inventory-view-details.png)](media/how-to-inventory-sensor/sensor-inventory-view-details.png#lightbox)

For more information, see [Device inventory column data](device-inventory#device-inventory-column-data).

## Edit device details

As you manage your network devices, you may need to update their details. For example, you may want to modify security value as assets change, or personalize the inventory to better identify devices, or if a device was classified incorrectly.

If you're working with a cloud-connected sensor, any edits you make in the sensor console are updated in the Azure portal.

**To edit device details**:

1. Select a device in the grid, and then select **Edit** in the toolbar at the top of the page.
2. In the **Edit** pane on the right, modify the device fields as needed, and then select **Save** when you're done.

You can also open the edit pane from the device details page:

1. Select a device in the grid, and then select **View full details** in the pane on the right.
2. In the device details page, select **Edit Properties**.
3. In the **Edit** pane on the right, modify the device fields as needed, and then select **Save** when you're done.

Editable fields include:

- Authorized status
- Device name
- Device type
- OS
- Purdue level
- Description
- Scanner or programming device

For more information, see [Device inventory column data](device-inventory#device-inventory-column-data).

## Export the device inventory to CSV

Export your device inventory to a CSV file to manage or share data outside of the OT sensor.

To export device inventory data, on the **Device inventory** page, select **Export**![](media/how-to-manage-device-inventory-on-the-cloud/export-button.png) .

The device inventory is exported with any filters currently applied, and you can save the file locally.

Note

In the exported file, date values use the region settings of the machine that accesses the OT sensor. Export data from a machine with the same region settings as your sensor. For more information, see [Synchronize time zones on an OT sensor](how-to-manage-individual-sensors#synchronize-time-zones-on-an-ot-sensor).

## Merge devices

You may need to merge duplicate devices if the sensor has discovered separate network entities that are associated with a single, unique device.

Examples of this scenario might include a PLC with four network cards, a laptop with both WiFi and a physical network card, or a single workstation with multiple network cards.

Note

- You can only merge authorized devices.
- Device merges are irreversible. If you merge devices incorrectly, you'll have to delete the merged device and wait for the sensor to rediscover both devices.
- Alternately, merge devices from the [Device map](how-to-work-with-the-sensor-device-map) page.

When merging, you instruct the sensor to combine the device properties of two devices into one. When you merge the devices, the Device Properties window and sensor reports will be updated with the new device property details.

For example, if you merge two devices, each with an IP address, both IP addresses will appear as separate interfaces in the Device Properties window.

To merge duplicate devices from the device inventory, perform the following steps:

1. In the **Device inventory** page, select the devices you want to merge, and then select **Merge** in the toolbar at the top of the page.
2. At the prompt, select **Confirm** to confirm that you want to merge the devices.

The devices are merged, and a confirmation message appears at the top right.

## View inactive devices

You may want to view devices in your network that have been inactive and delete them.

For example, devices may become inactive because of misconfigured SPAN ports, changes in network coverage, or because devices were unplugged from the network

**To view inactive devices**, filter the device inventory to display devices that have been inactive.

On the **Device inventory** page:

1. Select **Add filter**.
2. Select **Last Activity** in the column field.
3. Choose the time period in the **Filter** field. Filtering options include seven days or more, 14 days or more, 30 days or more, or 90 days or more.

Tip

We recommend that you delete inactive devices to display a more accurate representation of current network activity, better evaluate the number of [devices monitored by Defender for IoT](architecture#devices-monitored-by-defender-for-iot), and reduce clutter on your screen.

## Delete devices

You may want to delete devices from your device inventory, such as if they've been incorrectly merged (see Merge devices), or are inactive devices.

Deleted devices are removed from the **Device map** and the device inventories on the Azure portal, and aren't calculated when generating reports, such as Data Mining, Risk Assessment, or Attack Vector reports.

**To delete one or more devices**:

You can delete a device when it's been inactive for more than 10 minutes.

1. In the **Device inventory** page, select the device or devices you want to delete, and then select **Delete**![](media/how-to-manage-device-inventory-on-the-cloud/delete-device.png) in the toolbar at the top of the page.
2. At the prompt, select **Confirm** to confirm that you want to delete the device or devices from Defender for IoT.

The device or devices are deleted, and a confirmation message appears at the top right.

**To delete all inactive devices**:

This procedure is supported for the admin users only, including the default privileged *admin* user.

1. Select the **Last Activity** filter icon in the Inventory.
2. Select a filter option.
3. Select **Apply**.
4. Select **Delete Inactive Devices**. In the prompt displayed, enter the reason you're deleting the devices, and then select **Delete**.

All devices detected within the range of the currently applied **Last Activity** filter will be deleted. If you delete a large number of devices, the delete process may take a few minutes.

For more information, see [Default privileged on-premises users](roles-on-premises#default-privileged-on-premises-users).