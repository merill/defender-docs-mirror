---
layout: Conceptual
title: Configure ERSPAN traffic mirroring with a Cisco switch - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/traffic-mirroring/configure-mirror-erspan
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
description: This article describes how to configure the Cisco switch for encapsulated remote switched port analyzer (ERSPAN) traffic mirroring for Microsoft Defender for IoT.
ms.date: 2024-05-26T00:00:00.0000000Z
ms.topic: install-set-up-deploy
locale: en-us
document_id: fe6537de-fa58-23c8-8ec7-f0bac0881d01
document_version_independent_id: 1fa5755d-4660-eb89-ba63-e9b82bb21afa
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/traffic-mirroring/configure-mirror-erspan.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/traffic-mirroring/configure-mirror-erspan
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/traffic-mirroring/configure-mirror-erspan.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: c04fce85-d2f9-bfd7-770a-e2236a55eecb
---

# Configure ERSPAN traffic mirroring with a Cisco switch - Microsoft Defender for IoT | Microsoft Learn

This article is one in a series of articles describing the [deployment path](../ot-deploy/ot-deploy-path) for OT monitoring with Microsoft Defender for IoT.

[![Diagram of a progress bar with Network level deployment highlighted.](../media/deployment-paths/progress-network-level-deployment.png)](../media/deployment-paths/progress-network-level-deployment.png#lightbox)

This article provides high-level guidance for configuring encapsulated remote switched port analyzer [(ERSPAN) traffic mirroring](../best-practices/traffic-mirroring-methods#erspan-ports) for a Cisco switch.

We recommend using your receiving router as the generic routing encapsulation (GRE) tunnel destination.

## Prerequisites

Before you start, make sure that you understand your plan for network monitoring with Defender for IoT, and the SPAN ports you want to configure.

For more information, see [Traffic mirroring methods for OT monitoring](../best-practices/traffic-mirroring-methods).

## Configure the Cisco switch

The following code shows a sample `ifconfig` output for ERSPAN configured on a Cisco switch:

```cli
monitor session 1 type erspan-source
description ERSPAN to D4IoT
erspan-id 32                              # required, # between 1-1023
vrf default                               # required
destination ip 172.1.2.3                  # IP address of destination
source interface port-channel1 both       # Port(s) to be sniffed
filter vlan 1                             # limit VLAN(s) (optional)
no shut                                   # enable

monitor erspan origin ip-address 172.1.2.1 global
```

For more information, see [CLI command reference from OT network sensors](../cli-ot-sensor).

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

## Configure legacy ERSPAN in the CLI

Important

We don't recommend using legacy versions of the software as this might cause security issues for your system. If you're still using the legacy version the user needs to run specific CLI commands discussed in this section.

## Configure setup via the CLI

Use this procedure to configure the following initial setup settings via CLI:

- Signing into the sensor console and setting a new *admin* user password
- Defining network details for your sensor
- Defining the interfaces you want to monitor

### CLI Legacy

To configure a legacy ERSPAN tunneling interface in the CLI you need to use an adapted line of code. This code ensures that the legacy ERSPAN option is available in the CLI sensor configuration wizard.

A new legacy ERPSAN can only be configured if you have an existing interface configured.

**To configure the legacy ERSPAN**:

1. Log in to your sensor using a CLI interface with a cyberx or admin user.
2. Type `ERSPAN=1 python3 -m cyberx.config.configure`.

    ![Screenshot of the CLI sensor configuration for a legacy version interface.](media/configure-mirror-erspan/legacy-erspan-cli.png)
3. Select **LegacyErspan** and assign an interface.
4. Select **Save**.