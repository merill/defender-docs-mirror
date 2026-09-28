---
layout: Conceptual
title: Configure mirroring with a switch SPAN port - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/traffic-mirroring/configure-mirror-span
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
description: This article describes how to configure a SPAN port for traffic mirroring when monitoring OT networks with Microsoft Defender for IoT.
ms.date: 2022-09-20T00:00:00.0000000Z
ms.topic: install-set-up-deploy
locale: en-us
document_id: 50076e35-a6d6-287f-b045-821e2db7fa4e
document_version_independent_id: 4a66b79e-4243-f752-ac98-42346d712c78
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/traffic-mirroring/configure-mirror-span.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/traffic-mirroring/configure-mirror-span
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/traffic-mirroring/configure-mirror-span.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 0bcfbe8f-d513-a780-c933-ab267d1e64ec
---

# Configure mirroring with a switch SPAN port - Microsoft Defender for IoT | Microsoft Learn

This article is one in a series of articles describing the [deployment path](../ot-deploy/ot-deploy-path) for OT monitoring with Microsoft Defender for IoT.

[![Diagram of a progress bar with Network level deployment highlighted.](../media/deployment-paths/progress-network-level-deployment.png)](../media/deployment-paths/progress-network-level-deployment.png#lightbox)

Configure a SPAN port on your switch to mirror local traffic from interfaces on the switch to a different interface on the same switch.

This article provides sample configuration processes and procedures for configuring a SPAN port, using either the Cisco CLI or GUI, for a Cisco 2960 switch with 24 ports running IOS.

Important

This article is intended only as sample guidance and not as instructions. Mirror ports on other Cisco operating systems and other switch brands are configured differently. For more information, see your switch documentation.

## Prerequisites

Before you start, make sure that you understand your plan for network monitoring with Defender for IoT, and the SPAN ports you want to configure.

For more information, see [Traffic mirroring methods for OT monitoring](../best-practices/traffic-mirroring-methods).

## Sample CLI SPAN port configuration (Cisco 2960)

The following commands show a sample process for configuring a SPAN port on a Cisco 2960 via CLI:

```cli
Cisco2960# configure terminal
Cisco2960(config)# monitor session 1 source interface fastehernet 0/2 - 23 rx
Cisco2960(config)# monitor session 1 destination interface fastethernet 0/24
Cisco2960(config)# end
Cisco2960# show monitor session 1
Cisco2960# running-copy startup-config
```

## Sample GUI SPAN port configuration (Cisco 2960)

This procedure describes the high-level steps for configuring a SPAN port on a Cisco 2960 via the GUI. For more information, see the relevant Cisco documentation.

From the switch's configuration GUI:

1. Enter the global configuration mode.
2. Configure the first 23 ports as a session source, mirroring only RX packets.
3. Configure port 24 to be a session destination.
4. Return to privileged EXEC mode.
5. Verify the port mirroring configuration.
6. Save the configuration.

## Sample CLI SPAN port configuration with multiple VLANs (Cisco 2960)

Defender for IoT can monitor multiple VLANs configured in your network without any extra configuration, as long as the network switch is configured to send VLAN tags to Defender for IoT.

For example, the following commands must be configured on a Cisco switch to support monitoring VLANs in Defender for IoT:

**Monitor session**: The following commands configure your switch to send VLANs to the SPAN port.

```cli
monitor session 1 source interface Gi1/2
monitor session 1 filter packet type good Rx
monitor session 1 destination interface fastEthernet1/1 encapsulation dot1q
```

**Monitor Trunk Port F.E. Gi1/1**: The following commands configure your switch to support VLANs configured on the trunk port:

```cli
interface GigabitEthernet1/1
switchport trunk encapsulation dot1q
switchport mode trunk
```

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

## Deploy with unidirectional gateways/data diodes

You might deploy Defender for IoT with unidirectional gateways, also known as data diodes. Data diodes provide a secure way to monitor networks as they only allow data to flow in one direction. This means data can be monitored without compromising the security of the network, as data cannot be sent back in the opposite direction. Examples of data diode solutions are [Waterfall](https://waterfall-security.com), [Owl Cyber Defense](https://owlcyberdefense.com/products/data-diode-products/), or [Hirschmann](https://www.belden.com/products/by-brand/hirschmann/cybersecurity).

If unidirectional gateways are needed, we recommend deploying your data diodes on the SPAN traffic going to the sensor monitoring port. For example, use a data diode to monitor traffic from a sensitive system, such as an industrial control system, while keeping the system completely isolated from the monitoring system.

Place your OT sensors outside the electronic perimeter and have them receive traffic from the diode. In this scenario, you’ll be able to manage your Defender for IoT sensors from the cloud, keeping them automatically updated with the latest threat intelligence packages.