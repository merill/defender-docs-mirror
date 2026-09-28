---
layout: Conceptual
title: Sample OT  network connectivity models - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/best-practices/sample-connectivity-models
breadcrumb_path: ../../breadcrumb/toc.json
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
description: This article describes sample connectivity methods for Microsoft Defender for IoT OT sensor connections.
ms.date: 2022-11-08T00:00:00.0000000Z
ms.topic: install-set-up-deploy
locale: en-us
document_id: 24261996-7e39-b7b1-7f0d-b645db047411
document_version_independent_id: 98310a3b-c9f0-3d69-c4bf-89699f99f87e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/best-practices/sample-connectivity-models.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/best-practices/sample-connectivity-models
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/best-practices/sample-connectivity-models.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: c5192a8f-1b1e-7c0d-d7b4-034547c2115e
---

# Sample OT  network connectivity models - Microsoft Defender for IoT | Microsoft Learn

This article provides sample network models for Microsoft Defender for IoT sensor connections.

## Sample: Ring topology

The following diagram shows an example of a ring network topology, in which each switch or node connects to exactly two other switches, forming a single continuous pathway for the traffic.

[![Diagram of the ring topology.](../media/how-to-set-up-your-network/ring-topology.png)](../media/how-to-set-up-your-network/ring-topology.png#lightbox)

## Sample: Linear bus and star topology

In a star network such as the one shown in the diagram below, every host is connected to a central hub. In its simplest form, one central hub acts as a conduit to transmit messages. In the following example, lower switches aren't monitored, and traffic that remains local to these switches won't be seen. Devices might be identified based on ARP messages, but connection information will be missing.

[![Diagram of the linear bus and star topology.](../media/how-to-set-up-your-network/linear-bus-star-topology.png)](../media/how-to-set-up-your-network/linear-bus-star-topology.png#lightbox)

## Sample: Multi-layer, multi-tenant network

The following diagram is a general abstraction of a multilayer, multi-tenant network, with an expansive cybersecurity ecosystem typically operated by an security operations center (SOC) and managed security service provider (MSSP). Defender for IoT sensors are typically deployed in layers 0 to 3 of the OSI model.

[![Diagram of the OSI model.](../media/how-to-set-up-your-network/osi-model.png)](../media/how-to-set-up-your-network/osi-model.png#lightbox)