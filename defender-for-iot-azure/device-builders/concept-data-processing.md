---
layout: Conceptual
title: Data processing and residency - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/concept-data-processing
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
description: Microsoft Defender for IoT data processing, and residency can occur in regions that are different than the IoT Hub's region.
ms.date: 2023-01-12T00:00:00.0000000Z
ms.topic: concept-article
locale: en-us
document_id: 57d5a760-c58e-4f61-80c6-57f1c29d9c32
document_version_independent_id: edfafc96-8a4c-7f54-24d2-430fb0a31866
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/concept-data-processing.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/concept-data-processing
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/concept-data-processing.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/816835a3-1c5d-4536-835c-4b59dc9c9d97
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/a98c4e96-5248-4755-860b-6c76f1933f0c
platformId: 3db5b206-34e6-1022-169c-903912230f7b
---

# Data processing and residency - Microsoft Defender for IoT | Microsoft Learn

Microsoft Defender for IoT is a separate service, which adds an extra layer of threat protection to the Azure IoT Hub, IoT Edge, and your devices. Defender for IoT may process, and store your data within a different geographic location than your IoT Hub.

Mapping between the IoT Hub, and Microsoft Defender for IoT's regions is as follows:

- For a Hub located in Europe, the data is stored in the *West Europe* region.
- For a Hub located outside Europe, the data is stored in the *East US* region.

Microsoft Defender for IoT, uses the device twin, unmasked IP addresses, and additional configuration data as part of its security detection logic by default. To disable the device twin, and unmask the IP address collection, navigate to the data collection's settings page.

![Screenshot of the data collections setting page.](media/concept-data-processing/data-collection-settings.png)