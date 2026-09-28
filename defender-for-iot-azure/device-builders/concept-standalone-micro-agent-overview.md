---
layout: Conceptual
title: Standalone micro agent overview - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/concept-standalone-micro-agent-overview
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
description: The Microsoft Defender for IoT security agents allow you to build security directly into your new IoT devices and Azure IoT projects.
ms.date: 2024-04-17T00:00:00.0000000Z
ms.topic: overview
locale: en-us
document_id: 2936806a-6d32-f1d2-4372-091dc5904ff8
document_version_independent_id: fb9209fa-4cb0-39e2-dcfa-a57f87ed870c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/concept-standalone-micro-agent-overview.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/concept-standalone-micro-agent-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/concept-standalone-micro-agent-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: f1f88215-fd31-67c6-b9c8-83c475411368
---

# Standalone micro agent overview - Microsoft Defender for IoT | Microsoft Learn

Security is a near-universal concern for IoT implementers. IoT devices have unique needs for endpoint monitoring, security posture management, and threat detection – all with highly specific performance requirements.

Note

Defender for IoT plans to retire the micro agent on June 1, 2027.

The Microsoft Defender for IoT security agent allows you to build security directly into your new IoT devices and Azure IoT projects. The micro agent has flexible deployment options, including the ability to deploy as a binary package or modify source code, and it's available for standard IoT operating systems like Linux and Eclipse ThreadX.

The Microsoft Defender for IoT micro agent provides endpoint visibility into security posture management, threat detection, and integration into Microsoft's other security tools for unified security management.

## Security posture management

Proactively monitor the security posture of your IoT devices. Microsoft Defender for IoT provides security posture recommendations based on the CIS benchmark, along with device-specific recommendations. Get visibility into operating system security, including OS configuration, firewall configuration, and permissions.

## Endpoint IoT and OT threat detection

Detect threats like botnets, brute force attempts, crypto miners, and suspicious network activity. Create custom alerts to target the most important threats in your unique organization.

## Flexible distribution and deployment models

The Microsoft Defender for IoT micro agent includes source code, allowing you to incorporate the micro agent into firmware, or customize it to include only what you need. The micro agent is also available as a binary package, or integrated directly into other Azure IoT solutions.

## Meets the needs of your IoT devices, with minimal impact

The Microsoft Defender for IoT micro agent is easy to deploy, and has minimal performance impact on the endpoint. With Defender for IoT micro agent you can:

- **Optimize for performance**: The Microsoft Defender for IoT micro agent has a small footprint and low CPU consumption.
- **Plug and Play**: There are no specific OS kernel dependencies or support necessary for all major IoT operating systems. The Microsoft Defender for IoT micro agent meets your devices where they are.
- **Flexible deployment**: As a standalone agent, The Microsoft Defender for IoT micro agent supports different distribution models and flexible deployment.