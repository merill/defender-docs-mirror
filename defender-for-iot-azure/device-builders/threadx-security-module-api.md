---
layout: Conceptual
title: Defender-IoT-micro-agent for Eclipse ThreadX API - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/threadx-security-module-api
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
description: Reference API for the Defender-IoT-micro-agent for Eclipse ThreadX.
ms.topic: reference
ms.date: 2024-04-17T00:00:00.0000000Z
locale: en-us
document_id: d2792889-6913-d7ee-27dc-2e8c0d05312d
document_version_independent_id: 70e6f647-d88a-248b-e29f-cbce00331804
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/threadx-security-module-api.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/threadx-security-module-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/threadx-security-module-api.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/45f51b57-72c2-4c0b-ab6c-cde4f0bed5d8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8905b934-b96c-4513-8447-7040eb93b2b2
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/0888e80f-d6a8-407d-b2ed-e325482a4715
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/203e4af6-88b5-4e82-bf7b-51a6102005c3
platformId: 6946ba6e-21b7-66a0-dccb-b29b9039c69d
---

# Defender-IoT-micro-agent for Eclipse ThreadX API - Microsoft Defender for IoT | Microsoft Learn

Defender for IoT APIs are governed by [Microsoft API License and Terms of use](/en-us/legal/microsoft-apis/terms-of-use).

This API is intended for use with the Defender-IoT-micro-agent for Eclipse ThreadX only. For additional resources, see the [Defender-IoT-micro-agent for Eclipse ThreadX GitHub resource](https://github.com/eclipse-threadx).

Note

Defender for IoT plans to retire the micro agent on June 1, 2027.

## Enable Defender-IoT-micro-agent for Eclipse ThreadX

**nx\_azure\_iot\_security\_module\_enable**

### Prototype

```c
UINT nx_azure_iot_security_module_enable(NX_AZURE_IOT *nx_azure_iot_ptr);
```

### Description

This routine enables the Azure IoT Defender-IoT-micro-agent subsystem. An internal state machine manages collection of security events and sends them to Azure IoT Hub. Only one NX\_AZURE\_IOT\_SECURITY\_MODULE instance is required and needed to manage data collection.

### Parameters

| Name | Description |
| --- | --- |
| nx\_azure\_iot\_ptr [in] | A pointer to a `NX_AZURE_IOT`. |

### Return values

| Return values | Description |
| --- | --- |
| NX\_AZURE\_IOT\_SUCCESS | Successfully enabled Azure IoT Security Module. |
| NX\_AZURE\_IOT\_FAILURE | Failed to enable the Azure IoT Security Module due to an internal error. |
| NX\_AZURE\_IOT\_INVALID\_PARAMETER | Security module requires a valid #NX\_AZURE\_IOT instance. |

### Allowed from

Threads

## Disable Azure IoT Defender-IoT-micro-agent

**nx\_azure\_iot\_security\_module\_disable**

### Prototype

```c
UINT nx_azure_iot_security_module_disable(NX_AZURE_IOT *nx_azure_iot_ptr);
```

### Description

This routine disables the Azure IoT Defender-IoT-micro-agent subsystem.

### Parameters

| Name | Description |
| --- | --- |
| nx\_azure\_iot\_ptr [in] | A pointer to `NX_AZURE_IOT`. If NULL the singleton instance is disabled. |

### Return values

| Return values | Description |
| --- | --- |
| NX\_AZURE\_IOT\_SUCCESS | Successful when the Azure IoT Security Module is successfully disabled. |
| NX\_AZURE\_IOT\_INVALID\_PARAMETER | Azure IoT Hub instance is different than the singleton composite instance. |
| NX\_AZURE\_IOT\_FAILURE | Failed to disable the Azure IoT Security Module due to an internal error. |

### Allowed from

Threads