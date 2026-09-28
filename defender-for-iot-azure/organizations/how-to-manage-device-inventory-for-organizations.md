---
layout: Conceptual
title: Manage your device inventory from the Azure portal - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/how-to-manage-device-inventory-for-organizations
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
description: Learn how to view and manage OT and IoT devices (assets) from the Device inventory page in the Azure portal.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: msecd-doc-authoring-1016 - enterprise-iot - sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: 7ca1872f-a31f-dbeb-c720-4d8408d98593
document_version_independent_id: a951099f-82eb-4898-cc9c-8b03f3043a95
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/how-to-manage-device-inventory-for-organizations.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/how-to-manage-device-inventory-for-organizations
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/how-to-manage-device-inventory-for-organizations.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: a712d1ed-fdc7-9dae-2d5b-bae8ef19966f
---

# Manage your device inventory from the Azure portal - Microsoft Defender for IoT | Microsoft Learn

Use the **Device inventory** page in [Defender for IoT](https://portal.azure.com/#view/Microsoft_Azure_IoT_Defender/IoTDefenderDashboard/%7E/Getting_started) on the Azure portal to manage all network devices detected by cloud-connected sensors, including OT, IoT, and IT. Identify new devices detected, devices that might need troubleshooting, and more.

For more information, see [Devices monitored by Defender for IoT](architecture#devices-monitored-by-defender-for-iot).

Note

Currently, devices discovered in the Azure portal aren't synchronized with the Defender portal, and therefore the list of devices discovered could be different in each portal.

## View the device inventory

To view detected devices in the **Device inventory** page in the Azure portal, go to **Defender for IoT** &gt; **Device inventory**.

[![Screenshot of the Device inventory page in the Azure portal.](media/how-to-manage-device-inventory-on-the-cloud/device-inventory-page.png)](media/how-to-manage-device-inventory-on-the-cloud/device-inventory-page.png#lightbox)

Use any of the following options to modify or filter the devices shown:

| Option | Steps |
| --- | --- |
| **Sort devices** | Select a column header to sort the devices by that column. Select it again to change the sort direction. |
| **Filter devices shown** | Either use the **Search** box to search for specific device details, or select **Add filter** to filter the devices shown.  In the **Add filter** box, define your filter by column name, operator, and value. Select **Apply** to apply your filter. You can apply multiple filters at the same time. Search results and filters aren't saved when you refresh the **Device inventory** page.  The **Last active time** and **Network location (Preview)** filters are on by default. |
| **Modify columns shown** | Select **Edit columns**![](media/how-to-manage-device-inventory-on-the-cloud/edit-columns-icon.png) . In the **Edit columns** pane: - Select the **+ Add Column** button to add new columns to the grid. - Drag and drop fields to change the columns order.- To remove a column, select the **Delete**![](media/how-to-manage-device-inventory-on-the-cloud/trashcan-icon.png) icon to the right.- To reset the columns to their default settings, select **Reset**![](media/how-to-manage-device-inventory-on-the-cloud/reset-icon.png) . Select **Save** to save any changes made. |
| **Group devices** | From the **Group by** dropdown, select a category, such as **Class**, **Data source**, **Location**, **Purdue level**, **Site**, **Type**, **Vendor**, or **Zone**, to group the devices shown. Inside each group, devices retain the same column sorting. To remove the grouping, select **No grouping**. |

For more information, see [Device inventory column data](device-inventory#device-inventory-column-data).

Note

If your OT sensors detect multiple devices in the same zone with the same IP or MAC address, those devices are automatically merged and identified as a single, unique device. Devices that have different IP addresses, but the same MAC address, aren't merged, and continue to be listed as unique devices.

Merged devices are listed only once in the **Device inventory** page. For more information, see [Separating zones for recurring IP ranges](best-practices/plan-corporate-monitoring#separating-zones-for-recurring-ip-ranges).

### View full device details

To view full details about a specific device, select the device row. Initial details are shown in a pane on the right, where you can also select **View full details** to open the device details page and drill down more.

For example:

[![Screenshot of a device details pane and the View full details button in the Azure portal.](media/how-to-manage-device-inventory-on-the-cloud/device-information-window.png)](media/how-to-manage-device-inventory-on-the-cloud/device-information-window.png#lightbox)

The device details page displays comprehensive device information, including the following tabs:

| Section | Description |
| --- | --- |
| **Attributes** | Displays full device details such as class, data source, firmware details, activity, type, protocols, Purdue level, sensor, site, zone, and more. |
| **Backplane** | Displays the backplane hardware configuration, including slot and rack information. Select a slot in the backplane view to see the details of the underlying devices. The backplane tab is usually visible for Purdue level 1 devices that have slots in use, such as PLC, RTU, and DCS devices. |
| **Vulnerabilities** | Displays current vulnerabilities specific to the device. Defender for IoT provides vulnerability coverage for [supported OT vendors](resources-manage-proprietary-protocols) where Defender for IoT can detect firmware models and firmware versions.Vulnerability data is based on the repository of standards-based vulnerability data documented in the US government National Vulnerability Database (NVD). Select the CVE name to see the CVE details and description. **Tip**: View vulnerability data across your network with the [Defender for IoT Vulnerability workbook](workbooks#view-workbooks). |
| **Alerts** | Displays current open alerts related to the device. Select any alert to view more details, and then select **View full details** to open the alert page to view the full alert information and take action. For more information, see [View alerts on the Azure portal](how-to-manage-cloud-alerts#view-alerts-on-the-azure-portal). |
| **Recommendations** | Displays current recommendations for the device, such as Review PLC operating mode and Review unauthorized devices. For more information on recommendations, see [Enhance security posture with security recommendations](recommendations). |

For example:

[![Screenshot of the backplane tab in on the full device details page. ](media/how-to-manage-device-inventory-on-the-cloud/device-details-page.png)](media/how-to-manage-device-inventory-on-the-cloud/device-details-page.png#lightbox)

### Identify devices that aren't connecting successfully

If you suspect that certain devices aren't actively communicating with Azure, we recommend that you verify whether those devices have communicated with Azure recently at all. For example:

1. In the **Device inventory** page, make sure that the **Last activity** column is shown.

    Select **Edit columns**![](media/how-to-manage-device-inventory-on-the-cloud/edit-columns-icon.png) &gt; **Add column** &gt; **Last Activity** &gt; **Save**.
2. Select the **Last activity** column to sort the grid by that column.
3. Filter the grid to show active devices during a specific time period:

    1. Select **Add filter**.
    2. In the **Column** field, select **Last activity**.
    3. Select a predefined time range, or define a custom range to filter for.
    4. Select **Apply**.
4. Search for the devices you're verifying in the filtered list of devices.

## Edit device details

As you manage your network devices, you might need to update their details. For example, you might want to modify security value as assets change, or personalize the inventory to better identify devices, or if a device was classified incorrectly.

To edit device details:

1. Select one or more devices in the grid, and then select **Edit**![](media/how-to-manage-sensors-on-the-cloud/edit-device-details.png) .
2. If you've selected multiple devices, select **Add field type** and add the fields you want to edit, for all selected devices.
3. Modify the device fields as needed, and then select **Save** when you're done.

Your updates are saved for all selected devices.

For more information, see [Device inventory column data](device-inventory#device-inventory-column-data).

### Reference of editable fields

The following device fields are supported for editing in the **Device inventory** page:

| Name | Description |
| --- | --- |
| **General information** |  |
| **Name** | Mandatory. Supported for editing only when editing a single device. |
| **Authorized device** | Toggle on or off as needed as device security changes. |
| **Description** | Enter a meaningful description for the device. |
| **Location** | Enter a meaningful location for the device. |
| **Category** | Use the **Class**, **Type**, and **Subtype** options to categorize the device. |
| **Business function** | Enter a meaningful description of the device's business function. |
| **Hardware model** | Select the device's hardware model from the dropdown menu. |
| **Hardware vendor** | Select the device's hardware vendor from the dropdown menu. |
| **Firmware** | Device the device's firmware name and version. You can either select the **delete** button to delete an existing firmware definition, or select **+ Add** to add a new one. |
| **Purdue level** | The Purdue level in which the device exists. |
| **Tags** | Enter meaningful tags for the device. Select the **delete** button to delete an existing tag, or select **+ Add** to add a new one. |
| **Settings** |  |
| **Importance** | Select **Low**, **Normal**, or **High** to modify the device's importance. |
| **Programming device** | Toggle the **Programming Device** option on or off as needed for your device. |

For more information, see [Device inventory column data](device-inventory#device-inventory-column-data).

## Export the device inventory to CSV

Export your device inventory to a CSV file to manage or share data outside of the Azure portal. You can export a maximum of 30,000 devices at a time.

To export device inventory data:

On the **Device inventory page**, select **Export**![](media/how-to-manage-device-inventory-on-the-cloud/export-button.png) .

The device inventory is exported with any filters currently applied, and you can save the file locally.

## Delete a device

If you have devices no longer in use, delete them from the device inventory so that they're no longer connected to Defender for IoT.

Devices might be inactive because of misconfigured port mirroring (SPAN) ports, changes in network coverage, or because the device was unplugged from the network.

Delete inactive devices to maintain a correct representation of current network activity, better understand the number of devices that you're monitoring when managing your Defender for IoT [licenses and plans](billing), and to reduce clutter on your screen.

Important

Device deletions are one-directional. When you delete a device from the **Azure portal**, the deletion doesn't sync to the sensor connected to the same site. When you delete a device from the **sensor**, the deletion syncs to the **Device inventory** in the Azure portal.

To delete a device:

In the **Device inventory** page, select the device you want to delete, and then select **Delete**![](media/how-to-manage-device-inventory-on-the-cloud/delete-device.png) in the toolbar at the top of the page.

At the prompt, select **Yes** to confirm that you want to delete the device from Defender for IoT.