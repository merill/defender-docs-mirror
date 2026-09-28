---
layout: Conceptual
title: Configure traffic mirroring with a Remote SPAN (RSPAN) port - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/traffic-mirroring/configure-mirror-rspan
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
description: This article describes how to configure a remote SPAN (RSPAN) port for traffic mirroring when monitoring OT networks with Microsoft Defender for IoT.
ms.date: 2022-11-08T00:00:00.0000000Z
ms.topic: install-set-up-deploy
locale: en-us
document_id: 19a62a8c-2c78-7d3a-cbab-0d7b765ea4e0
document_version_independent_id: 008ce4cf-8b72-e105-b6ae-77305b74050c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/traffic-mirroring/configure-mirror-rspan.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/traffic-mirroring/configure-mirror-rspan
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/traffic-mirroring/configure-mirror-rspan.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: f6bc74df-3ce9-5600-eeda-5bf64ec96aae
---

# Configure traffic mirroring with a Remote SPAN (RSPAN) port - Microsoft Defender for IoT | Microsoft Learn

This article is one in a series of articles describing the [deployment path](../ot-deploy/ot-deploy-path) for OT monitoring with Microsoft Defender for IoT.

[![Diagram of a progress bar with Network level deployment highlighted.](../media/deployment-paths/progress-network-level-deployment.png)](../media/deployment-paths/progress-network-level-deployment.png#lightbox)

This article describes a sample procedure for configuring [RSPAN](../best-practices/traffic-mirroring-methods#remote-span-rspan-ports) on a Cisco 2960 switch with 24 ports running IOS.

Important

This article is intended only as guidance and not as instructions. Mirror ports on other Cisco operating systems and other switch brands are configured differently. For more information, see your switch documentation.

## Prerequisites

- Before you start, make sure that you understand your plan for network monitoring with Defender for IoT, and the SPAN ports you want to configure.

    For more information, see [Traffic mirroring methods for OT monitoring](../best-practices/traffic-mirroring-methods).
- RSPAN requires a specific VLAN to carry the monitored SPAN traffic between switches. Before you start, make sure that your switch supports RSPAN.
- Make sure that the mirroring option on your switch is turned off.
- Make sure that the remote VLAN is allowed on the trunked port between the source and destination switches.
- Make sure that all switches connecting to the same RSPAN session are from the same vendor.
- Make sure that the trunk port sharing the same remote VLAN between switches isn't already defined as a mirror session source port.
- The remote VLAN increases the bandwidth on the trunked port by the amount of traffic being mirrored from the source session. Make sure that your switch's trunk port can support the increased bandwidth.

Caution

An increased bandwidth, whether due to large amounts of throughput or a large number of switches, can cause a switch to fail and therefore to bring down the entire network. When configuring traffic mirroring with RSPAN, make sure to consider the following:

- The number of access / distribution switches that you configure with RSPAN.
- The correlating throughput for the remote VLAN on each switch.

## Configure the source switch

On your source switch:

1. Enter `global configuration` mode and create a new, dedicated VLAN.
2. Identify your new VLAN as the RSPAN VLAN, and then return to `configure terminal` mode.
3. Configure all 24 ports as session sources.
4. Configure the RSPAN VLAN to be the session destination.
5. Return to the privileged `EXEC` mode and verify the port mirroring configuration.

## Configure the destination switch

On your destination switch:

1. Enter `global configuration` mode, and configure the RSPAN VLAN to be the session source.
2. Configure physical port 24 to be the session destination.
3. Return to privileged `EXEC` mode and verify the port mirroring configuration.
4. Save the configuration.

## Validate traffic mirroring

After configuring traffic mirroring, make an attempt to receive a sample of recorded traffic (PCAP file) from the switch SPAN or mirror port.

A sample PCAP file will help you:

- Validate the switch configuration
- Confirm that the traffic going through your switch is relevant for monitoring
- Identify the bandwidth and an estimated number of devices detected by the switch

1. Use a network protocol analyzer application, such as [Wireshark](https://www.wireshark.org/), to record a sample PCAP file for a few minutes. For example, connect a laptop to a port where you've configured traffic monitoring.
2. Check that *Unicast packets* are present in the recording traffic. Unicast traffic is traffic sent from address to another.

    If most of the traffic is ARP messages, your traffic mirroring configuration isn't correct.
3. Verify that your OT protocols are present in the analyzed traffic.

    For example:

    ![Screenshot of Wireshark validation.](../media/how-to-set-up-your-network/wireshark-validation.png)