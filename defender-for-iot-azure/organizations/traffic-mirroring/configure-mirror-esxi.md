---
layout: Conceptual
title: Configure a monitoring interface using an ESXi vSwitch - Sample - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/traffic-mirroring/configure-mirror-esxi
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
description: This article describes traffic mirroring methods with an ESXi vSwitch for OT monitoring with Microsoft Defender for IoT.
ms.date: 2024-04-08T00:00:00.0000000Z
ms.topic: install-set-up-deploy
locale: en-us
document_id: a354a358-7107-5116-bc25-63a3ef3b338c
document_version_independent_id: 0a7383b7-6fa5-7b23-8af3-281f942a516c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/traffic-mirroring/configure-mirror-esxi.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/traffic-mirroring/configure-mirror-esxi
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/traffic-mirroring/configure-mirror-esxi.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 46b238e7-e0bf-eb03-e4a8-576146b1ae1e
---

# Configure a monitoring interface using an ESXi vSwitch - Sample - Microsoft Defender for IoT | Microsoft Learn

This article is one in a series of articles describing the [deployment path](../ot-deploy/ot-deploy-path) for OT monitoring with Microsoft Defender for IoT.

[![Diagram of a progress bar with Network level deployment highlighted.](../media/deployment-paths/progress-network-level-deployment.png)](../media/deployment-paths/progress-network-level-deployment.png#lightbox)

This article describes how to use *Promiscuous mode* in a ESXi vSwitch environment as a workaround for configuring traffic mirroring, similar to a [SPAN port](configure-mirror-span). A SPAN port on your switch mirrors local traffic from interfaces on the switch to a different interface on the same switch.

For more information, see [Traffic mirroring with virtual switches](../best-practices/traffic-mirroring-methods#traffic-mirroring-with-virtual-switches).

## Prerequisites

Before you start, make sure that you understand your plan for network monitoring with Defender for IoT, and the SPAN ports you want to configure.

For more information, see [Traffic mirroring methods for OT monitoring](../best-practices/traffic-mirroring-methods).

## Configure a monitoring interface using Promiscuous mode

To configure a monitoring interface with Promiscuous mode on an ESXi v-Switch:

1. Open the vSwitch properties page and select **Add standard virtual switch**.
2. Enter **SPAN Network** as the network label.
3. In the MTU field, enter **4096**.
4. Select **Security**, and verify that the **Promiscuous Mode** policy is set to **Accept** mode.
5. Select **Add** to close the vSwitch properties.
6. Highlight the vSwitch you have just created, and select **Add uplink**.
7. Select the physical NIC you will use for the SPAN traffic, change the MTU to **4096**, then select **Save**.
8. Open the **Port Group** properties page and select **Add Port Group**.
9. Enter **SPAN Port Group** as the name, enter **4095** as the VLAN ID, and select **SPAN Network** in the vSwitch drop down, then select **Add**.
10. Open the **OT Sensor VM** properties.
11. For **Network Adapter 2**, select the **SPAN** network.
12. Select **OK**.
13. Connect to the sensor, and verify that mirroring works.

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