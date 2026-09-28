---
layout: Conceptual
title: Defender for IoT glossary for device builder - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/references-defender-for-iot-glossary
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
description: The glossary provides a brief description of important Defender for IoT platform terms and concepts.
ms.date: 2023-01-01T00:00:00.0000000Z
ms.topic: article
locale: en-us
document_id: bc34bbea-188a-621a-3509-b0368eb3f3e0
document_version_independent_id: ab9d684c-ba51-a171-9ebd-38675233eb1e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/references-defender-for-iot-glossary.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/references-defender-for-iot-glossary
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/references-defender-for-iot-glossary.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 0a7184e5-fe0e-dbb9-304e-ebf80aa8601c
---

# Defender for IoT glossary for device builder - Microsoft Defender for IoT | Microsoft Learn

This glossary provides a brief description of important terms and concepts for the Microsoft Defender for IoT platform. Select the **Learn more** links to go to related terms in the glossary. This will help you to learn and use the product tools quickly and effectively.

Note

Defender for IoT plans to retire the micro agent on June 1, 2027.

## D

| Term | Description | Learn more |
| --- | --- | --- |
| **Device twins** | Device twins are JSON documents that store device state information including metadata, configurations, and conditions. | Module Twin |
| **Defender-IoT-micro-agent twin**`(DB)` | The Defender-IoT-micro-agent twin holds all of the information that is relevant to device security, for each specific device in your solution. | Device twinModule Twin |
| **Device inventory** | Defender for IoT identifies, and classifies devices as a single unique network device in the inventory for:  - Standalone IT, OT, and IoT devices with 1 or multiple NICs.  - Devices composed of multiple backplane components. This includes all racks, slots, and modules.  - Devices that act as network infrastructure. For example, switches, and routers with multiple NICs.  - Public internet IP addresses, multicast groups, and broadcast groups aren't considered inventory devices. Devices that have been inactive for more than 60 days are classified as inactive Inventory devices. |  |

## I

| Term | Description | Learn more |
| --- | --- | --- |
| **IoT Hub** | Managed service, hosted in the cloud, that acts as a central message hub for bi-directional communication between your IoT application and the devices it manages. |  |

## M

| Term | Description | Learn more |
| --- | --- | --- |
| **Micro Agent** | Provides depth security capabilities for IoT devices including security posture and threat detection. |  |
| **Module twin** | Module twins are JSON documents that store module state information including metadata, configurations, and conditions. | Device twinsDefender-IoT-micro-agent twin |