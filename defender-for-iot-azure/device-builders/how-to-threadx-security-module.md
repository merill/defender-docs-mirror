---
layout: Conceptual
title: Configure and Customize Defender-IoT-micro-agent for Eclipse ThreadX - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/how-to-threadx-security-module
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
description: Learn about how to configure and customize your Defender-IoT-micro-agent for Eclipse ThreadX.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: e2a55ffb-2f29-3b31-b132-86d653b36bf5
document_version_independent_id: 4e636c2f-198a-0ca5-aa78-6b6ff93a08a0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/how-to-threadx-security-module.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/how-to-threadx-security-module
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/how-to-threadx-security-module.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/45f51b57-72c2-4c0b-ab6c-cde4f0bed5d8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/0888e80f-d6a8-407d-b2ed-e325482a4715
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: fefc0ee7-6ca5-e24c-0d92-94afb975b8fa
---

# Configure and Customize Defender-IoT-micro-agent for Eclipse ThreadX - Microsoft Defender for IoT | Microsoft Learn

This article describes how to configure the Defender-IoT-micro-agent for your Eclipse ThreadX device to meet your network, bandwidth, and memory requirements. You learn how to select a target distribution, tune device behavior settings, adjust data collection intervals, and enable or disable individual collectors for resource-constrained devices.

Note

Defender for IoT plans to retire the micro agent on June 1, 2027.

## Configure the Defender-IoT-micro-agent

You must select a target distribution file that has a `*.dist` extension from the `netxduo/addons/azure_iot/azure_iot_security_module/configs` directory.

When using a CMake compilation environment, you must set a command line parameter to `IOT_SECURITY_MODULE_DIST_TARGET` for the chosen value. For example: `-DIOT_SECURITY_MODULE_DIST_TARGET=RTOS_BASE`.

In an IAR, or other non CMake compilation environment, you must add the `netxduo/addons/azure_iot/azure_iot_security_module/inc/configs/<target distribution>/` path to any known included paths. For example: `netxduo/addons/azure_iot/azure_iot_security_module/inc/configs/RTOS_BASE`.

## Configure device behavior settings

Use the following file to configure your device behavior.

**netxduo/addons/azure\_iot/azure\_iot\_security\_module/inc/configs/&lt;target distribution&gt;/asc\_config.h**

In a CMake compilation environment, you must change the default configuration by editing the `netxduo/addons/azure_iot/azure_iot_security_module/configs/<target distribution>.dist` file. Use the following CMake format `set(ASC_XXX ON)`, or the following file `netxduo/addons/azure_iot/azure_iot_security_module/inc/configs/<target distribution>/asc_config.h` for all other environments. For example, `#define ASC_XXX`.

The default values for the general, data collection, and collector configuration settings are provided in the following tables:

## Configure general micro agent settings

The following table lists the general configuration settings and their default values:

| Name | Type | Default | Details |
| --- | --- | --- | --- |
| ASC\_SECURITY\_MODULE\_ID | String | defender-iot-micro-agent | The unique identifier of the device. |
| SECURITY\_MODULE\_VERSION\_(MAJOR)(MINOR)(PATCH) | Number | 3.2.1 | The version. |
| ASC\_SECURITY\_MODULE\_SEND\_MESSAGE\_RETRY\_TIME | Number | 3 | The amount of time the Defender-IoT-micro-agent will take to send the security message after a fail (in seconds). |
| ASC\_SECURITY\_MODULE\_PENDING\_TIME | Number | 300 | The Defender-IoT-micro-agent pending time (in seconds). The state changes to suspend, if the time is exceeded. |

## Configure data collection settings

The following table lists the data collection configuration settings and their default values:

| Name | Type | Default | Details |
| --- | --- | --- | --- |
| ASC\_FIRST\_COLLECTION\_INTERVAL | Number | 30 | The Collector's startup collection interval offset. During startup, the value is added to the collection of the system in order to avoid sending messages from multiple devices simultaneously. |
| ASC\_HIGH\_PRIORITY\_INTERVAL | Number | 10 | The collector's high priority group interval (in seconds). |
| ASC\_MEDIUM\_PRIORITY\_INTERVAL | Number | 30 | The collector's medium priority group interval (in seconds). |
| ASC\_LOW\_PRIORITY\_INTERVAL | Number | 145,440 | The collector's low priority group interval (in seconds). |

### Configure network activity collection

To customize your collector network activity configuration, use the following:

| Name | Type | Default | Details |
| --- | --- | --- | --- |
| ASC\_COLLECTOR\_NETWORK\_ACTIVITY\_TCP\_DISABLED | Boolean | false | Filters the `TCP` network activity. |
| ASC\_COLLECTOR\_NETWORK\_ACTIVITY\_UDP\_DISABLED | Boolean | false | Filters the `UDP` network activity events. |
| ASC\_COLLECTOR\_NETWORK\_ACTIVITY\_ICMP\_DISABLED | Boolean | false | Filters the `ICMP` network activity events. |
| ASC\_COLLECTOR\_NETWORK\_ACTIVITY\_CAPTURE\_UNICAST\_ONLY | Boolean | true | Captures the unicast incoming packets only. When set to false, it captures both Broadcast, and Multicast. |
| ASC\_COLLECTOR\_NETWORK\_ACTIVITY\_SEND\_EMPTY\_EVENTS | Boolean | false | Sends an empty events of collector. |
| ASC\_COLLECTOR\_NETWORK\_ACTIVITY\_MAX\_IPV4\_OBJECTS\_IN\_CACHE | Number | 64 | The maximum number of IPv4 network events to store in memory. |
| ASC\_COLLECTOR\_NETWORK\_ACTIVITY\_MAX\_IPV6\_OBJECTS\_IN\_CACHE | Number | 64 | The maximum number of IPv6 network events to store in memory. |

### Available collectors

The following table lists the available collector enablement flags:

| Name | Type | Default | Details |
| --- | --- | --- | --- |
| ASC\_COLLECTOR\_HEARTBEAT\_ENABLED | Boolean | ON | Enables the heartbeat collector. |
| ASC\_COLLECTOR\_NETWORK\_ACTIVITY\_ENABLED | Boolean | ON | Enables the network activity collector. |
| ASC\_COLLECTOR\_SYSTEM\_INFORMATION\_ENABLED | Boolean | ON | Enables the system information collector. |

Other configurations flags are advanced and have unsupported features. Contact support to change these advanced configuration flags, or for more information.

## Supported security alerts and recommendations

The Defender-IoT-micro-agent for Eclipse ThreadX supports specific security alerts and recommendations. Make sure to [customize the security alert and recommendation values for Eclipse ThreadX](concept-threadx-security-alerts-recommendations) for your service.

## Log Analytics (optional)

You can enable and configure Log Analytics to investigate device events and activities. Learn about how to set up and use [Log Analytics with the Defender for IoT service](how-to-security-data-access#log-analytics).