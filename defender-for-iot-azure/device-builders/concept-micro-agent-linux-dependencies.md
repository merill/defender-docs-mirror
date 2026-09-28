---
layout: Conceptual
title: Micro agent Linux dependencies - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/concept-micro-agent-linux-dependencies
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
description: This article describes the different Linux OS dependencies for the Defender for IoT micro agent.
ms.topic: reference
ms.custom: linux-related-content
ms.date: 2023-01-01T00:00:00.0000000Z
locale: en-us
document_id: a1906de3-5165-cb00-6efa-3b249f678639
document_version_independent_id: e183d78c-16f0-f238-58d0-387ff2cba1aa
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/concept-micro-agent-linux-dependencies.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/concept-micro-agent-linux-dependencies
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/concept-micro-agent-linux-dependencies.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: c9d1df34-b509-5665-b426-995158dd358c
---

# Micro agent Linux dependencies - Microsoft Defender for IoT | Microsoft Learn

This article describes the different Linux OS dependencies for the Defender for IoT micro agent.

Note

Defender for IoT plans to retire the micro agent on June 1, 2027.

## Linux dependencies

The table below shows the Linux dependencies for each component.

| Component | Dependency | Type | Required by IoT SDK | Notes |
| --- | --- | --- | --- | --- |
| **Core** |  |  |  |  |
|  | libcurl-openssl (libcurl) | Library | ✔ |  |
|  | libssl | Library | ✔ |  |
|  | uuid | Library | ✔ |  |
|  | pthread | ulibc compilation flag | ✔ |  |
|  | libuv1 | Library |  |  |
|  | sudo | Package |  |  |
|  | uuid-runtime | Package |  |  |
| **System information collector** |  |  |  |  |
|  | uname | System call |  |  |
| **Baseline collector** |  |  |  |  |
|  | BusyBox | Linux compilation flag |  |  |
|  | Bash | Linux compilation flag |  |  |
| **Process collector** |  |  |  |  |
|  | CONFIG\_CONNECTOR=y | Kernel config |  |  |
|  | CONFIG\_PROC\_EVENTS=y | Kernel config |  |  |
| **Network collector** |  |  |  |  |
|  | libpcap | Library |  |  |
|  | CONFIG\_PACKET=y | Kernel config |  |  |
|  | CONFIG\_NETFILTER =y | Kernel config |  | Optional – Performance improvement |
| **Login collector** |  |  |  |  |
|  | Wtmp, btmp | Log files |  | [utmp](https://en.wikipedia.org/wiki/Utmp) |