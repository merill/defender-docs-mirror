---
layout: Conceptual
title: Manage IoT and OT Devices with the Cloud Device Inventory - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/how-to-manage-device-inventory-on-the-cloud
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
ms.subservice: device-builders
description: Learn how to manage your IoT and OT devices with the device inventory.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: b99f7cac-737d-a5e2-7c6a-ce149e6e1bd0
document_version_independent_id: 5bd04e42-baf1-bf55-79b4-8071a37f28f3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/how-to-manage-device-inventory-on-the-cloud.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/how-to-manage-device-inventory-on-the-cloud
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/how-to-manage-device-inventory-on-the-cloud.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 02f3b27a-fa2e-5ac5-0d5d-f6260941e438
---

# Manage IoT and OT Devices with the Cloud Device Inventory - Microsoft Defender for IoT | Microsoft Learn

You can use the device inventory to view device systems and network information. You can use the Search, Filter, Edit columns, and Export tools to manage device system and network information.

![A total overview of Defender for IoT's device inventory screen.](media/how-to-manage-device-inventory-on-the-cloud/device-inventory-screenshot.png)

Some of the benefits of the device inventory include:

- Identify all IoT and OT devices from different inputs. For example, this allows you to understand which devices in your environment aren't communicating and require troubleshooting.
- Group, and filter devices by site, type, or vendor.
- Gain visibility into each device and investigate the different threats and alerts for each one.
- Export the entire device inventory to a CSV file for your reports.

Note

Defender for IoT plans to retire the micro agent on June 1, 2027.

## Device inventory overview

The Device inventory gives you an overview of all devices within your environment. Here you can see the individual details of each device and filter and order your search by various options.

The following table describes the different device properties in the device inventory.

| Parameter | Description | Default value |
| --- | --- | --- |
| **Data source** | The source of the data, such as Micro Agent, OtSensor, and Mde. | MicroAgent |
| **Device class** | The class of the device. | IoT |
| **Device model** | The device's model. | - |
| **Device name** | The name of the device as the sensor discovered it, or as entered by the user. | - |
| **Device subtype** | The subtype of the device, such as speaker and smart tv. | Managed Device |
| **Device Type** | The type of device, such as communication, and industrial. | Miscellaneous |
| **First seen** | The date, and time the device was first seen. Presented in format MM/DD/YYYY HH:MM:SS AM/PM. | - |
| **IP Address** | The IP address of the device. | - |
| **Last Activity** | The date, and time the device last sent an event to the cloud. Presented in format MM/DD/YYYY HH:MM:SS AM/PM. | - |
| **Last update time** | The date, and time the device last sent a system information event to the cloud. Presented in format MM/DD/YYYY HH:MM:SS AM/PM. | - |
| **MAC Address** | The MAC address of the device. | - |
| **OS architecture** | The architecture of the operating system. | - |
| **OS distribution** | The distribution of the operating system, such as Android, Linux, and Haiku. | - |
| **OS platform** | The OS of the device, if detected. | - |
| **OS version** | The version of the operating system, such as Windows 10 and Ubuntu 20.04.1. | - |
| **Site** | The site that contains this device. | - |
| **Vendor** | The name of the device's vendor, as defined in the MAC address. | - |

To view the device inventory:

1. Open the [Azure portal](https://portal.azure.com).
2. Navigate to **Defender for IoT** &gt; **Device inventory**.

    [![Select device inventory from the left side menu under Defender for IoT.](media/how-to-manage-device-inventory-on-the-cloud/device-inventory.png)](media/how-to-manage-device-inventory-on-the-cloud/device-inventory.png#lightbox)

## Customize the device inventory table

In the device inventory table, you can add or remove columns. You can also change the column order by dragging and dropping a field.

To customize the device inventory table:

1. Select the ![](media/how-to-manage-device-inventory-on-the-cloud/edit-columns-icon.png) button.
2. In the **Edit columns** tab, select the drop-down menu to change the value of a column.

    ![Select the drop-down menu to change the value of a given column.](media/how-to-manage-device-inventory-on-the-cloud/device-drop-down-menu.png)
3. Add a column by selecting the ![](media/how-to-manage-device-inventory-on-the-cloud/add-column-icon.png) button.
4. Reorder the columns by dragging a column parameter to a new location.
5. Delete a column by selecting the ![](media/how-to-manage-device-inventory-on-the-cloud/trashcan-icon.png) button.

    ![Select the trash can icon to delete a column.](media/how-to-manage-device-inventory-on-the-cloud/delete-a-column.png)
6. Select **Save** to save any changes made.

If you want to reset the device inventory to the default settings, select the ![](media/how-to-manage-device-inventory-on-the-cloud/reset-icon.png) button in the **Edit columns** tab.

## Filter the device inventory

You can search and filter the device inventory to define what information the table displays.

For a list of filters that you can apply to the device inventory table, see the Device inventory overview.

To filter the device inventory:

1. Select **Add filter**.

    ![Select  the add filter button to specify what you want to appear in the device inventory.](media/how-to-manage-device-inventory-on-the-cloud/add-filter.png)
2. In the **Add filter** window, select the column drop-down menu to choose which column to filter.

    ![Select which column you want to filter in the device inventory.](media/how-to-manage-device-inventory-on-the-cloud/add-filter-window.png)
3. Enter a value to filter by.
4. Select the **Apply** button.

You can apply filters at one time. The filters aren't saved when you leave the **Device inventory** page.

## View device information

To view a specific devices information, select the device and the device information window appears.

[![Select a device to see all of that device's information.](media/how-to-manage-device-inventory-on-the-cloud/device-information-window.png)](media/how-to-manage-device-inventory-on-the-cloud/device-information-window.png#lightbox)

## Export the device inventory to CSV

You can export your device inventory to a CSV file. Any filters that you apply to the device inventory table are exported when you export the table.

Select the ![](media/how-to-manage-device-inventory-on-the-cloud/export-button.png) button to export the device inventory.

## How to identify devices that haven't recently communicated with the Azure cloud

If you suspect that certain devices aren't actively communicating, there's a way to check and see which devices haven't communicated in a specified time period.

To identify all devices that haven't communicated recently:

1. Open the [Azure portal](https://portal.azure.com).
2. Navigate to **Defender for IoT** &gt; **Device inventory**.
3. Select the ![](media/how-to-manage-device-inventory-on-the-cloud/edit-columns-icon.png) button.
4. Add a column by selecting the ![](media/how-to-manage-device-inventory-on-the-cloud/add-column-icon.png) button.
5. Select **Last Activity**.
6. Select **Save**
7. On the main Device inventory page, select **Last activity** to sort the page by last activity.

    [![Screenshot of the device inventory organized by last activity.](media/how-to-manage-device-inventory-on-the-cloud/last-activity.png)](media/how-to-manage-device-inventory-on-the-cloud/last-activity.png#lightbox)
8. Select the ![](media/how-to-manage-device-inventory-on-the-cloud/add-filter-icon.png) to add a filter on the last activity column.

    ![Screenshot of the add filter screen where you can select the time period to see the last activity.](media/how-to-manage-device-inventory-on-the-cloud/last-activity-filter.png)
9. Enter a time period or a custom date range and select **Apply**.