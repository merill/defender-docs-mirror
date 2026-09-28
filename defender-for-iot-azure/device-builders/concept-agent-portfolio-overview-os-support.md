---
layout: Conceptual
title: Agent portfolio overview and OS support - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/concept-agent-portfolio-overview-os-support
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
description: Microsoft Defender for IoT provides a large portfolio of agents based on the device type.
ms.date: 2024-04-17T00:00:00.0000000Z
ms.topic: overview
locale: en-us
document_id: 4b210541-34b8-57f6-3262-09e038d548d0
document_version_independent_id: 802d96fd-d404-ace1-589d-9fa923d24a1b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/concept-agent-portfolio-overview-os-support.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/concept-agent-portfolio-overview-os-support
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/concept-agent-portfolio-overview-os-support.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 49e59f14-5800-acb3-73ce-99799890be0d
---

# Agent portfolio overview and OS support - Microsoft Defender for IoT | Microsoft Learn

Microsoft Defender for IoT provides a large portfolio of agents based on the device type.

Note

Defender for IoT plans to retire the micro agent on June 1, 2027.

## Standalone and Edge agent

Most of the Linux Operating Systems (OS) are covered by both agents. The agents can be deployed as a binary package, or as a source code that can be incorporated as part of the firmware. The customer can modify, and customize the agents as needed. The following are some examples of supported OS:

| Operating system | AMD64 | ARM32v7 | ARM64 |
| --- | --- | --- | --- |
| Debian 9 | ✓ | ✓ |  |
| Debian 10 | ✓ | ✓ | ✓ |
| Debian 11 | ✓ | ✓ |  |
| Ubuntu 18.04 | ✓ | ✓ | ✓ |
| Ubuntu 20.04 | ✓ | ✓ | ✓ |
| Ubuntu 22.04 | ✓ |  |  |

For a more granular view of the micro agent-operating system dependencies, see [Linux dependencies](concept-micro-agent-linux-dependencies#linux-dependencies).

## Eclipse ThreadX micro agent

The Microsoft Defender for IoT micro agent comes built in as part of the FileX NetX Duo component, and monitors the device's network activity. The micro agent consists of a comprehensive and lightweight security solution that provides coverage for common threats, and potential malicious activities on a real-time operating system (FileX) devices.