---
layout: Conceptual
title: Import extra data for detected OT devices - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/how-to-import-device-information
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
description: Learn how to manually enhance the device data automatically detected by your Microsoft Defender for IoT OT sensor with extra, imported data.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 523d30c3-837e-1825-e4af-d46cd4cb5a90
document_version_independent_id: 0a577e55-51b7-36ff-b40c-695f4228746e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/how-to-import-device-information.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/how-to-import-device-information
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/how-to-import-device-information.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 2bc90974-110f-a6e1-1f8c-9cab2390fd1d
---

# Import extra data for detected OT devices - Microsoft Defender for IoT | Microsoft Learn

OT network sensors automatically monitor and analyze detected device traffic. In some cases, your organization's network policies might prevent some device data from being ingested to Microsoft Defender for IoT.

This article describes how you can manually import the missing data to your OT sensor and add it to the device data already detected.

## Prerequisites

Before performing the procedures in this article, you must have:

- An OT network sensor with [OT sensor software installed](ot-deploy/install-software-ot-sensor) and [configured and activated](ot-deploy/activate-deploy-sensor).
- Access to your OT network sensor as an **Admin** user. For more information, see [On-premises users and roles for OT monitoring with Defender for IoT](roles-on-premises).
- An understanding of the extra device data you want to import. Use that understanding to choose one of the following import methods:

    - **Import data from the device map** to import device names, operating systems, groups, or Purdue layer
    - **Import data from system settings** to import device IP addresses, operating systems, patch levels, or authorization statuses
- Excel or another application that can create and edit `.csv` files.

Tip

A device's authorization status affects the alerts that are triggered by the OT sensor for the selected device. You'll receive alerts for any devices *not* listed as authorized devices, as they'll be considered to be unauthorized.

## Import data from the OT sensor device map

**To import device names, types, groups, or Purdue layers**:

1. Sign into your OT sensor and select **Device map** &gt; **Export Devices** to export the device data already detected by your OT sensor.
2. Open the downloaded .CSV file for editing and modify *only* the following data, as needed:

    - **Name**. Maximum length: 30 characters
    - **Device type**. The device’s functional role (for example, printer, surveillance camera, or smart appliance).
    - **Group**. Maximum length: 30 characters
    - **Purdue layer**. Enter one of the following: **Enterprise**, **Supervisory**, or **Process Control**

    Make sure to use capitalization standards already in use in the downloaded file. For example, in the **Purdue Layer** column, use *Title Caps*.

    Important

    Make sure that you don't import data to your OT sensor that you've exported from a different sensor.
3. When you're done, save your file to a location accessible from your OT sensor.
4. On your OT sensor, in the **Device map** page, select **Import Devices** and select your modified .csv file.

Your device data is updated.

## Import data from the OT sensor system settings

**To import device IP addresses, operating systems, or patch levels**:

1. In Excel, open a blank workbook and select **Save As** to save it in `.csv` format.
2. In your .csv file, type the following details for each device:

    - **IP Address**. Enter the device's IP address.
    - **Device OS**. Enter one of the device operating systems listed in the supported device operating system values.
    - **Last Update**. Enter the date that the device was last updated, in `YYYY-MM-DD` format.

To fill in the Device OS column, use the example device information CSV entry for sample device details and the supported device operating system values table for reference.

### Device information example

The following table shows an example of correctly formatted device information in the .csv file.

| **IP Address** | **Device OS** | **Last Update** |
| --- | --- | --- |
| 192.168.19.200 | Windows 7 | 2017-11-01 |

### Supported values for Device operating system

The following table lists the supported values you can enter in the **Device OS** column.

| Windows | Windows Server | Other OS |
| --- | --- | --- |
| Windows | Windows Server | macOS |
| Windows 11 | Windows Server 2003 | macOS X |
| Windows 10 | Windows Server 2003 R2 | Linux |
| Windows 10 32 | Windows Server 2008 | HP UX |
| Windows 10 64 | Windows Server 2008 32 | QNX |
| Windows 7 | Windows Server 2008 64 |  |
| Windows 7 32 | Windows Server 2008 R2 |  |
| Windows 7 64 | Windows Server 2012 |  |
| Windows 8 | Windows Server 2012 R2 |  |
| Windows 8 32 | Windows Server 2016 |  |
| Windows 8 64 | Windows Server 2019 |  |
| Windows 8.1 | Windows Server 2022 |  |
| Windows 8.1 32 |  |  |
| Windows 8.1 64 |  |  |
| Windows NT |  |  |
| Windows 2000 |  |  |
| Windows Vista |  |  |
| Windows Vista 32 |  |  |
| Windows Vista 64 |  |  |
| Windows XP |  |  |

1. Sign into your OT sensor and select **System settings &gt; Import settings &gt; Device information**.
2. In the **Device information** pane, select **+ Import file** and then select your edited .csv file.
3. Select **Close** to save your changes.

### Import device authorization status

After importing device authorization status, any devices *not* included in the authorized devices import list are newly defined as not-authorized, and you'll start to receive new alerts about any traffic on each of these devices.

1. Download the Defender for IoT [device authorization file](https://download.microsoft.com/download/8/2/3/823c55c4-7659-4236-bfda-cc2427be2cee/CSS/authorized_devices%20-%20example.csv) and open it for editing.
2. In the downloaded file, list IP addresses and names for any devices you want to list as authorized devices.

    Make sure that your names are accurate. Names imported from a .CSV file overwrite any names already shown in the OT sensor's device map.
3. Sign into your OT sensor and select **System settings &gt; Import settings &gt; Authorized devices**.
4. In the **Authorized devices** pane, select **+ Import File** and then select your edited .CSV file.
5. Select **Close** to save your changes.