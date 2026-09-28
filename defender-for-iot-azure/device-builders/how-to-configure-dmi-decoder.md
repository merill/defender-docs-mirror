---
layout: Conceptual
title: How to configure the DMI Decoder - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/how-to-configure-dmi-decoder
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
description: Learn how to configure your DMI decoder on your device, or use other alternatives.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: da8d8e9f-1b86-fcd5-0714-f04046e35b06
document_version_independent_id: 019edf34-3df7-bb00-c919-537f9fb1db00
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/how-to-configure-dmi-decoder.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/how-to-configure-dmi-decoder
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/how-to-configure-dmi-decoder.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: f1af0dd7-b52e-13d6-213f-2399b6ce6c72
---

# How to configure the DMI Decoder - Microsoft Defender for IoT | Microsoft Learn

This article explains how to configure the DMI decoder, and alternative configurations for devices that do not support it.

Note

Defender for IoT plans to retire the micro agent on June 1, 2027.

## Overview

The Microsoft Defender for IoT **Device inventory** provides an overview of all IoT devices in your environment. The device inventory table can be customized to your preferences by adding or removing information fields, and filtering the fields.

The DMI decoder is used to retrieve data on the hardware and firmware of the device.

Retrieved fields are:

- Firmware vendor
- Firmware version
- Hardware model
- Hardware serial number
- Hardware vendor

For more information on the DMI Decoder, see [dmidecode(8): DMI table decoder - Linux man page (die.net)](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Flinux.die.net%2Fman%2F8%2Fdmidecode&amp;data=05%7C01%7Cmiashapan%40microsoft.com%7C07f0384fdcf14dd8cdb808dae0be41a4%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C638069405000113003%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C3000%7C%7C%7C&amp;sdata=%2FSFH0ALDDf6OPMsXW99gEP%2Bvu%2F1eIXyunIQth682NbQ%3D&amp;reserved=0).

## Populate SMBIOS tables for dmidecode

The dmidecode(8) utility reads System Management BIOS (SMBIOS) tables to extract hardware and firmware information from the device. To support dmidecode(8), SMBIOS tables need to be present and valid. To implement SMBIOS support for dmidecode(8), refer to the [System Management BIOS specifications](https://lwn.net/Articles/451967/).

## Choose an alternative configuration method

For devices that do not support the DMI decoder, there are two alternative options for retrieving and setting the firmware and hardware fields:

- Configure by using a JSON file
- Configure by using module twin settings

### Configure DMI Decoder by using a JSON file

To manually set the values on the device, create a JSON file. The micro agent will read the values from the JSON file and send them to the cloud.

To configure the file, use the following path and format details:

- Path:

    ```bash
        /etc/defender_iot_micro_agent/sysinfo.json
    ```
- Format:

    ```bash
        "HardwareVendor": "<hardware vendor>", 
        "HardwareModel": "<hardware model>",
        "HardwareSerialNumber": "<hardware serial number>", 
        "FirmwareVendor": "<firmware vendor>", 
        "FirmwareVersion": "<firmware version>"
    ```

### Configure DMI Decoder by using module twin settings

To manually set the values on the cloud, use the module twin configuration. Set the following desired properties in the module twin JSON payload:

```json
{
  "properties": {
    "desired": {
      "SystemInformation_HardwareVendor": "<data>",
      "SystemInformation_HardwareModel": "<data>",
      "SystemInformation_FirmwareVendor": "<data>",
      "SystemInformation_FirmwareVersion": "<data>",
      "SystemInformation_HardwareSerialNumber": "<data>"
    }
  }
}
```