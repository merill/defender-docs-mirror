---
layout: Conceptual
title: Traffic mirroring overview - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/traffic-mirroring/traffic-mirroring-overview
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
description: This article serves as an overview for configuring traffic mirroring for Microsoft Defender for IoT.
ms.date: 2023-07-04T00:00:00.0000000Z
ms.topic: concept-article
locale: en-us
document_id: 811c0b1a-4ec6-5f9c-af28-17ff8dd2d475
document_version_independent_id: 6267bbdd-e171-38f6-bf65-2fb52272135f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/traffic-mirroring/traffic-mirroring-overview.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/traffic-mirroring/traffic-mirroring-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/traffic-mirroring/traffic-mirroring-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 952fb031-6eae-870d-e2ba-6f88b1decbe1
---

# Traffic mirroring overview - Microsoft Defender for IoT | Microsoft Learn

This article is one in a series of articles describing the [deployment path](../ot-deploy/ot-deploy-path) for OT monitoring with Microsoft Defender for IoT and provides an overview of the procedures for configuring traffic mirroring in your network.

[![Diagram of a progress bar with Network level deployment highlighted.](../media/deployment-paths/progress-network-level-deployment.png)](../media/deployment-paths/progress-network-level-deployment.png#lightbox)

## Prerequisites

Before you configure traffic mirroring, make sure that you've decided on your sensor locations and the traffic mirroring method.

### Sensor location

Identify the best location to place the sensor in the network, to monitor the network traffic and provide the best discovery and security value possible. The location should give the sensor access to the following three important types of network traffic:

| Type | Description |
| --- | --- |
| Layer 2 (L2) Traffic | L2 traffic, which includes protocols such as ARP and DHCP, is a critical indicator of the sensor's placement. Accessing L2 traffic also means that the sensor can gather precise and valuable data about the network's devices. When a sensor is correctly positioned, it accurately captures the MAC addresses of devices. This vital information provides vendor indicators, which enhances the sensor's ability to classify devices. |
| OT Protocols | OT protocols are essential for extracting detailed information about devices within the network. These protocols provide crucial data that leads to accurate device classification. By analyzing OT protocol traffic, the sensor can gather comprehensive details about each device, such as its model, firmware version, and other relevant characteristics. This level of detail is necessary for maintaining an accurate and up-to-date inventory of all devices, which is crucial for network management and security. |
| Inner Subnet Communication | OT networks devices communicate within a subnet, and the information found within the inner subnet communication ensures the quality of the data collected by the sensors. Sensors are placed where they have access to the inner subnet communication in order to monitor device interactions, which often include critical data. By capturing these data packets, the sensors build a detailed and accurate picture of the network. |

For more information, see [placing OT sensors in your network](../best-practices/understand-network-architecture#placing-ot-sensors-in-your-network).

### Traffic mirroring methods

There are three types of traffic mirroring methods each designed for specific usage scenarios. Choose the best method based on the usage and size of your network.

| Mirroring type | Switched Port Analyzer (SPAN) | Remote SPAN (RSPAN) | Encapsulated Remote SPAN (ERSPAN) |
| --- | --- | --- | --- |
| **Usage Scenario** | Ideal for monitoring and analyzing traffic within a single switch or a small network segment. | Suitable for larger networks or scenarios where traffic needs to be monitored across different network segments. | Ideal for monitoring traffic over diverse or geographically dispersed networks, including remote sites. |
| **Description** | SPAN is a local traffic mirroring technique used within a single switch or a switch stack. It allows network administrators to duplicate traffic from specified source ports or VLANs to a destination port where the monitoring device, such as a network sensor or analyzer, is connected. | RSPAN extends the capabilities of SPAN by allowing traffic to be mirrored across multiple switches. It's designed for environments where monitoring needs to occur over different switches or switch stacks. | ERSPAN takes RSPAN a step further by encapsulating mirrored traffic in Generic Routing Encapsulation (GRE) packets. This method enables traffic mirroring across different network segments or even across the internet. |
| **Mirroring set up** | - **Source Ports/VLANs**: Configure the switch to mirror traffic from selected ports or VLANs. - **Destination Port**: The mirrored traffic is sent to a designated port on the same switch. This port is connected to your monitoring device. | - **Source Ports/VLANs**: Traffic is mirrored from specified source ports or VLANs on a source switch. - **RSPAN VLAN**: The mirrored traffic is sent to a special RSPAN VLAN that spans multiple switches.  - **Destination Port**: The traffic is then extracted from this RSPAN VLAN at a designated port on a remote switch where the monitoring device is connected. | - **Source Ports/VLANs**: Similar to SPAN and RSPAN, traffic is mirrored from specified source ports or VLANs. - **Encapsulation**: The mirrored traffic is encapsulated in GRE packets, which can then be routed across IP networks.  - **Destination Port**: The encapsulated traffic is sent to a monitoring device connected to a destination port where the GRE packets are decapsulated and analyzed. |
| **Benefits** | - Simplicity: Easy to configure and manage.  - Low Latency: Since it’s confined to a single switch, it introduces minimal delay. | - Extended Coverage: Allows for monitoring across multiple switches. - Flexibility: Can be used to monitor traffic from different parts of the network. | - Broad Coverage: Enables monitoring across different IP networks and locations.  - Flexibility: Can be used in scenarios where traffic needs to be monitored over long distances or through complex network paths. |
| **Limitations** | Local Scope: Limited to monitoring within the same switch, which might not be sufficient for larger networks. | Network Load: Potentially increases the load on the network due to the RSPAN VLAN traffic. |  |

When selecting a mirroring method, also consider the following factors:

| Factors | Description |
| --- | --- |
| Network Size and Layout | - SPAN is suitable for local monitoring. - RSPAN for larger, multi-switch environments  - ERSPAN for geographically dispersed or complex networks. |
| Traffic Volume | Ensure that the chosen method can handle the volume of traffic without introducing significant latency or network load. |
| Monitoring Needs | Determine if traffic is captured locally or across different network segments and choose the appropriate method. |

## Traffic mirroring processes

Use one of the following procedures to configure traffic mirroring in your network:

**SPAN ports**:

- [Configure mirroring with a switch SPAN port](configure-mirror-span)
- [Configure traffic mirroring with a Remote SPAN (RSPAN) port](configure-mirror-rspan)
- [Update a sensor's monitoring interfaces (configure ERSPAN)](../how-to-manage-individual-sensors#update-a-sensors-monitoring-interfaces-configure-erspan)

**Virtual switches**:

- [Configure traffic mirroring with a ESXi vSwitch](configure-mirror-esxi)
- [Configure traffic mirroring with a Hyper-V vSwitch](configure-mirror-hyper-v)

Defender for IoT also supports traffic mirroring with TAP configurations. For more information, see [Active or passive aggregation (TAP)](../best-practices/traffic-mirroring-methods#active-or-passive-aggregation-tap).