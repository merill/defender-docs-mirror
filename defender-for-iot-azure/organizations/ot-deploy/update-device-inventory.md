---
layout: Conceptual
title: Verify and Update Detected Device Inventory - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/ot-deploy/update-device-inventory
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
description: Learn how to fine-tune your newly detected device inventory on an OT sensor, such as updating device types and properties, merging devices as needed, and more.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: fb414a7c-73df-fadd-d8d7-80f5b48eea8f
document_version_independent_id: bdc59eb9-44af-5707-16d3-2a6b582e3650
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/ot-deploy/update-device-inventory.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/ot-deploy/update-device-inventory
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/ot-deploy/update-device-inventory.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 6b0b8f19-ccce-c526-81cc-d779d2d44fa3
---

# Verify and Update Detected Device Inventory - Microsoft Defender for IoT | Microsoft Learn

This article is one in a series of articles describing the [OT monitoring deployment path](ot-deploy-path) for Operational Technology (OT) monitoring with Microsoft Defender for IoT, and describes how to review your device inventory and enhance security monitoring with fine-tuned device details.

[![Diagram of a progress bar with Fine-tune OT monitoring highlighted.](../media/deployment-paths/progress-fine-tuning-ot-monitoring.png)](../media/deployment-paths/progress-fine-tuning-ot-monitoring.png#lightbox)

## Prerequisites

Before performing the procedures in this article, make sure that you have:

- An OT sensor with [OT sensor software installed](install-software-ot-sensor) and [configured and activated](activate-deploy-sensor), with device data detected.
- Access to your OT sensor as **Security Analyst** or **Admin** user. For more information, see [On-premises users and roles for OT monitoring with Defender for IoT](../roles-on-premises).

Verifying and updating the device inventory is performed by your deployment teams.

## View the device inventory on your OT sensor

To view the device inventory on your OT sensor, perform the following steps:

1. Sign into your OT sensor and select the **Device inventory** page.
2. Select **Edit Columns** to make changes to the grid layout and display more data fields for reviewing the data detected for each device.

    We especially recommend reviewing data for the **Name**, **Type**, **Authorization**, **Scanner device**, and **Programming device** columns.
3. Review the devices listed in the device inventory, and identify the devices whose device properties must be edited.

## Edit properties for individual devices

For each device where you need to edit device properties:

1. Select the device in the grid and then select **Edit** to view the editing pane. For example:

    [![Screenshot of editing device details from the OT sensor.](../media/update-device-inventory/edit-device-details.png)](../media/update-device-inventory/edit-device-details.png#lightbox)
2. Edit any of the following device properties as needed:

    | Name | Description |
    | --- | --- |
    | **Authorized Device** | Select if the device is a known entity on your network. Defender for IoT doesn't trigger alerts for learned traffic on authorized devices. |
    | **Name** | By default, shown as the device's IP address. Update this to a meaningful name for your device as needed. |
    | **Description** | Left blank by default. Enter a meaningful description for your device as needed. |
    | **OS Platform** | If the operating system value is blocked for detection, select the device's operating system from the dropdown list. |
    | **Type** | If the device's type is blocked for detection or needs to be modified, select a device type from the dropdown list. For more information, see [Supported devices](../device-inventory#supported-devices). |
    | **Purdue Level** | If the device's Purdue level is detected as **Undefined** or **Automatic**, we recommend selecting another level to fine-tune your data. For more information, see [Placing OT sensors in your network](../best-practices/understand-network-architecture#placing-ot-sensors-in-your-network). |
    | **Scanner** | Select if your device is a scanning device. Defender for IoT doesn't trigger alerts for scanning activities detected on devices defined as scanning devices. |
    | **Programming device** | Select if your device is a programming device. Defender for IoT doesn't trigger alerts for programming activities detected on devices defined as programming devices. |
3. Select **Save** to save your changes.

## Enhance device data (optional)

You might want to increase device visibility and enhance device data with more details than the default device data detected by the OT sensor.

- To increase device visibility to Windows-based devices, use the Defender for IoT [Windows Management Instrumentation (WMI) tool](../detect-windows-endpoints-script).
- If your organization's network policies prevent some data from being ingested, [import device information in bulk](../how-to-import-device-information).