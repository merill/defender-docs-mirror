---
layout: Conceptual
title: What is Microsoft Defender for IoT for device builders? - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/overview
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
description: Learn about how Microsoft Defender for IoT helps device builders to embed security into new IoT/OT devices.
ms.topic: overview
ms.date: 2024-04-17T00:00:00.0000000Z
locale: en-us
document_id: eaf42091-f905-049b-e3d5-16c334174f0b
document_version_independent_id: 2b6916cd-651f-9c1e-cca7-acaad131e358
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/overview.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: dd5ca4d6-c605-2932-bee8-bd58caf65db3
---

# What is Microsoft Defender for IoT for device builders? - Microsoft Defender for IoT | Microsoft Learn

For IoT implementers, security is a near-universal concern. IoT devices have unique needs for endpoint monitoring, security posture management, and threat detection – all with highly specific performance requirements.

Microsoft Defender for IoT provides lightweight security agents so that you can build security directly into your new IoT/OT initiatives. The micro agent provides endpoint visibility into security posture management and threat detection, and integrates with other Microsoft tools for unified security management.

- **Security posture management**: Monitor the security posture of your IoT devices. Defender for IoT provides security posture recommendations based on the CIS benchmark, along with device-specific recommendations. Get visibility into operating system security, including OS configuration, firewall settings, and permissions.
- **Endpoint threat detection**: Detect threats like botnets, brute force attempts, crypto miners, hardware connections, and suspicious network activity using the Microsoft TI database.
- **Device vulnerabilities management**: Monitor a full list of device vulnerabilities based on a real-time dynamic SBoM and your operating system.
- **Microsoft Sentinel integration**: Use Microsoft Sentinel to investigate and manage your device security, create custom dashboards and automatic response playbooks.
- **Raw events investigation**: Investigate all the raw events sent from your devices in your Log Analytics workspace.

## Defender for IoT micro agent

Note

Defender for IoT plans to retire the micro agent on June 1, 2027.

The Defender for IoT micro agent provides deep security protection, and visibility into device behavior.

- The micro agent collects, aggregates, and analyzes raw security events from your devices. Events can include IP connections, process creation, user logons, and other security-relevant information.
- Defender for IoT device agents handle event aggregation, to help avoid high network throughput.
- The micro agent has flexible deployment options. The micro agent includes source code, so you can incorporate it into firmware, or customize it to include only what you need. It's also available as a binary package, or integrated directly into other Azure IoT solutions. The micro agent is available for standard IoT operating systems, such as Linux and Eclipse ThreadX.
- The agents are highly customizable, allowing you to use them for specific tasks, such as sending only important information at the fastest SLA, or for aggregating extensive security information and context into larger segments, avoiding higher service costs.

[![Diagram of the micro agent architecture.](media/overview/micro-agent-architecture.png)](media/overview/micro-agent-architecture.png#lightbox)