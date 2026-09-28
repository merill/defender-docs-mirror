---
layout: Conceptual
title: Microsoft Defender for IoT Feature Support and Retirement - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/edge-security-module-deprecation
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
description: Review Microsoft Defender for IoT feature support status and retirement timelines for different capabilities.
ms.date: 2026-06-12T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: e0e54b90-7ecd-62e6-ac65-0237aba9b927
document_version_independent_id: 9f88bc47-5653-77ee-d9c1-cc0d57bfea6f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/edge-security-module-deprecation.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/edge-security-module-deprecation
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/edge-security-module-deprecation.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 304c0c88-0cb3-2ad3-ac9b-5742bb44a581
---

# Microsoft Defender for IoT Feature Support and Retirement - Microsoft Defender for IoT | Microsoft Learn

This article lists support status and retirement dates for Microsoft Defender for IoT micro agent features. Learn about the legacy Defender-IoT-micro-agent and its replacement. Find details on the end of support for C, C#, and Edge micro agent types.

## Legacy Defender for IoT micro-agent

The legacy Defender-IoT-micro-agent has been replaced by the new Defender for IoT micro agent.

To get started, see these tutorials:

- [Tutorial: Create a DefenderIotMicroAgent module twin (Preview)](tutorial-create-micro-agent-module-twin)
- [Tutorial: Install the Defender for IoT micro agent (Preview)](tutorial-standalone-agent-binary-installation)

Note

Defender for IoT plans to retire the micro agent on June 1, 2027.

### Timeline

Microsoft Defender for IoT will continue to support the legacy Microsoft Defender for IoT experience under IoT hub until March 31, 2023.

## Defender for IoT C, C#, and Edge Defender-IoT-micro-agent deprecation

The new micro agent will replace the current C, C#, and Edge Defender-IoT-micro-agent. 

The new micro agent development is based on the knowledge, and experience gathered from the legacy security module development, customers, and feedback from partners with four important improvements:

- **Depth security value**: The new agent will run on the host level, which will provide more visibility to the underlying operations of the device, and to allow for better security coverage.
- **Improved device performance and reduced footprint**: Achieved by a small RAM, and ROM memory footprint as well as low CPU consumption.
- **Plug and play**: The new micro agent has no kernel level dependencies anymore, and all of its software dependencies are provided as part of its package. The micro agent supports common CPU architecture.
- **Easy to deploy**: The micro agent supports different distribution models, through source code, and as a binary package.

### Timeline

Defender for IoT will continue to support C, C#, and Edge until March 1, 2022.

## Micro agent preview support

During the preview the micro agent may experience breaking changes without notice.