---
layout: Conceptual
title: Prepare an OT site deployment - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/best-practices/plan-prepare-deploy
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
description: Learn how to prepare for an OT site deployment, including understanding how many OT sensors you'll need, where they should be placed, and how they'll be managed.
ms.topic: install-set-up-deploy
ms.date: 2024-04-08T00:00:00.0000000Z
locale: en-us
document_id: 974ede06-cae2-4f35-eb7f-a7afe03aa9f3
document_version_independent_id: a162ca7a-9941-f1a2-d7cb-338edab1443e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/best-practices/plan-prepare-deploy.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/best-practices/plan-prepare-deploy
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/best-practices/plan-prepare-deploy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 9f15ece6-1c3a-e43d-8159-999b098175d7
---

# Prepare an OT site deployment - Microsoft Defender for IoT | Microsoft Learn

This article is one in a series of articles describing the [deployment path](../ot-deploy/ot-deploy-path) for OT monitoring with Microsoft Defender for IoT.

[![Diagram of a progress bar with Plan and prepare highlighted.](../media/deployment-paths/progress-plan-and-prepare.png)](../media/deployment-paths/progress-plan-and-prepare.png#lightbox)

To fully monitor your network, you'll need visibility on all of the endpoint devices in your network. Microsoft Defender for IoT mirrors the traffic that moves through your network devices to Defender for IoT network sensors. [OT network sensors](../architecture) then analyze your traffic data, trigger alerts, generate recommendations, and send data to Defender for IoT in Azure.

This article helps you plan where to place OT sensors in your network so that the traffic you want to monitor is mirrored as required, and how to prepare your site for sensor deployment.

## Prerequisites

Before planning OT monitoring for a specific site, make sure you've [planned your overall OT monitoring system](plan-corporate-monitoring).

This step is performed by your architecture teams.

### Learn about Defender for IoT's monitoring architecture

Use the following articles to understand more about the components and architecture in your network and Defender for IoT system:

- [Microsoft Defender for IoT components](../architecture)
- [Understanding your OT network architecture](understand-network-architecture)

## Create a network diagram

Each organization’s network will have its own complexity. Create a network map diagram that thoroughly lists all the devices in your network so that you can identify the traffic you want to monitor.

While creating your network diagram, use the following questions to identify and make notes about the different elements in your network and how they communicate.

### General questions

- What are your overall monitoring goals?
- Do you have any redundant networks, and are there areas of your network map that don't need monitoring and you can disregard?
- Where are your network's security and operational risks?

### Network questions

- Which protocols are active on monitored networks?
- Are VLANs configured in the network design?
- Is there any routing in the monitored networks?
- Is there any serial communication in the network?
- Where are firewalls installed in the networks you want to monitor?
- Is there traffic between an industrial control (ICS) network and an enterprise, business network? If so, is this traffic monitored?
- What's the physical distance between your switches and the enterprise firewall?
- Is OT system maintenance done with fixed or transient devices?

### Switch questions

- If a switch is otherwise unmanaged, can you monitor the traffic from a higher-level switch? For example, if your OT architecture uses a [ring topology](sample-connectivity-models#sample-ring-topology), only one switch in the ring needs monitoring.
- Can unmanaged switches be replaced with managed switches, or is the use of network TAPs an option?
- Can you monitor the switch's VLAN, or is the VLAN visible in another switch that you can monitor?
- If you connect a network sensor to the switch, will it mirror the communication between the HMI and PLCs?
- If you want to connect a network sensor to the switch, is there physical rack space available in the switch's cabinet?
- What's the cost/benefit of monitoring each switch?

## Identify the devices and subnets you want to monitor

The traffic you want to monitor and mirror to Defender for IoT network sensors is the traffic that's most [interesting](understand-network-architecture#identifying-interesting-traffic-points) to you from a security or operational perspective.

Review your OT network diagram together with your site engineers to define where you'll find the most relevant traffic for monitoring. We recommend that you meet with both network and operational teams to clarify expectations.

Together with your team, create a table of devices you want to monitor with the following details:

| Specification | Description |
| --- | --- |
| **Vendor** | The device's manufacturing vendor |
| **Device name** | A meaningful name for ongoing use and reference |
| **Type** | The device type, such as: *Switch*, *Router*, *Firewall*, *Access Point*, and so on |
| **Network layer** | The devices you'll want to monitor are either L2 or L3 devices: - *L2 devices* are devices within the IP segment- *L3 devices* are devices outside of the IP segmentDevices that support both layers can be considered as L3 devices. |
| **Crossing VLANs** | The IDs of any VLANs that cross the device. For example, verify these VLAN IDs by checking the spanning tree operation mode on each VLAN to see if they cross an associated port. |
| **Gateway for** | The VLANs for which the device acts as a default gateway. |
| **Network details** | The device's IP address, subnet, D-GW, and DNS host |
| **Protocols** | Protocols used on the device. Compare your protocols against Defender for IoT's [list of protocols](../concept-supported-protocols) supported out-of-the-box. |
| **Supported traffic mirroring** | Define what sort of traffic mirroring is supported by each device, such as SPAN, RSPAN, ERSPAN, or TAP. Use this information to [choose traffic mirroring methods for your OT sensors](traffic-mirroring-methods). |
| **Managed by partner services?** | Describe if a partner service, such as Siemens, Rockwell, or Emerson, manages the device. If relevant, describe the management policy. |
| **Serial connections** | If the device communicates via a serial connection, specify the serial communication protocol. |

### Calculate devices in your network

Calculate the number of devices in each site so that you can [purchase Defender for IoT licenses](../how-to-manage-subscriptions#purchase-a-defender-for-iot-license) at the correct size.

**To calculate the number of devices in each site:**:

1. Collect the total number of devices in your site and add them together.
2. Remove any of the following devices, which are *not* identified as individual devices by Defender for IoT:

    - **Public internet IP addresses**
    - **Multi-cast groups**
    - **Broadcast groups**
    - **Inactive devices**: Devices that have no network activity detected for more than 60 days

For more information, see [Devices monitored by Defender for IoT](../architecture#devices-monitored-by-defender-for-iot).

### Plan a multi-sensor deployment

If you're planning on deploying multiple network sensors, also consider the following recommendations when deciding where to place your sensors:

- **Physically connected switches**: For switches that are physically connected by Ethernet cable, make sure to plan at least one sensor for every 80 meters of distance between switches.
- **Multiple networks without physical connectivity**: If you have multiple networks without any physical connectivity between them, plan for at least one sensor for each individual network
- **Switches with RSPAN support**: If you have switches that can use [RSPAN traffic mirroring](../traffic-mirroring/configure-mirror-rspan), plan at least one sensor for every eight switches, with a local SPAN port. Plan to place the sensor close enough to the switches so that you can connect them by cable.

### Create a list of subnets

Create an aggregated list of subnets that you want to monitor, based on the list of devices you want to monitor across your entire network.

After deploying your sensors, you'll use this list to verify that the listed subnets are detected automatically, and manually update the list as needed.

## List your planned OT sensors

After you understand the traffic you want to mirror to Defender for IoT, create a full list of all the OT sensors you'll be onboarding.

For each sensor, list:

- Whether the sensor will be a [cloud-connected or locally managed sensor](../architecture#cloud-connected-vs-local-ot-sensors)
- For cloud-connected sensors, the [cloud connection method](../architecture-connections) you'll be using.
- Whether you'll be using physical or virtual appliances for your sensors, considering the bandwidth that you'll need for quality of service (QoS). For more information, see [Which appliances do I need?](../ot-appliance-sizing)
- The [site and zone](plan-corporate-monitoring#plan-ot-sites-and-zones) you'll be assigning to each sensor.

    Data ingested from sensors in the same site or zone can be viewed together, segmented out from other data in your system. If there's sensor data that you want to view grouped together in the same site or zone, make sure to assign sensor sites and zones accordingly.
- The [traffic mirroring method](traffic-mirroring-methods) you'll use for each sensor

As your network expands in time, you can onboard more sensors, or modify your existing sensor definitions.

Important

We recommend checking the characteristics of the devices you expect each sensor to detect, such as IP and MAC addresses. Devices that are detected in the same zone with the same logical set of device characteristics are automatically consolidated and are identified as the same device.

For example, if you're working with multiple networks and recurring IP addresses, make sure that you plan your each sensor with a different zone so that devices are identified correctly as separate and unique devices.

For more information, see [Separating zones for recurring IP ranges](plan-corporate-monitoring#separating-zones-for-recurring-ip-ranges).

## Prepare on-premises appliances

- **If you're using virtual appliances**, ensure that you have the relevant resources configured. For more information, see [OT monitoring with virtual appliances](../ot-virtual-appliances).
- **If you're using physical appliances**, ensure that you have the required hardware. You can buy [pre-configured appliances](../ot-pre-configured-appliances), or plan to [install software](../ot-deploy/install-software-ot-sensor) on your own appliances.

    To buy pre-configured appliances:

    1. Go to Defender for IoT in the Azure portal.
    2. Select **Getting started** &gt; **Sensor** &gt; **Buy preconfigured appliance** &gt; **Contact**.

    The link opens an email to [hardware.sales@arrow.com](mailto:hardware.sales@arrow.com?cc=DIoTHardwarePurchase@microsoft.com&amp;subject=Information%20about%20Microsoft%20Defender%20for%20IoT%20pre-configured%20appliances&amp;body=Dear%20Arrow%20Representative,%0D%0DOur%20organization%20is%20interested%20in%20receiving%20quotes%20for%20Microsoft%20Defender%20for%20IoT%20appliances%20as%20well%20as%20fulfillment%20options.%0D%0DThe%20purpose%20of%20this%20communication%20is%20to%20inform%20you%20of%20a%20project%20which%20involves%20%5BNUMBER%5D%20sites%20and%20%5BNUMBER%5D%20sensors%20for%20%5BORGANIZATION%20NAME%5D.%20Having%20reviewed%20potential%20appliances%20suitable%20for%20our%20project,%20we%20would%20like%20to%20obtain%20more%20information%20about:%20___________%0D%0D%0DI%20would%20appreciate%20being%20contacted%20by%20an%20Arrow%20representative%20to%20receive%20a%20quote%20for%20the%20items%20mentioned%20above.%0DI%20understand%20the%20quote%20and%20appliance%20delivery%20shall%20be%20in%20accordance%20with%20the%20relevant%20Arrow%20terms%20and%20conditions%20for%20Microsoft%20Defender%20for%20IoT%20pre-configured%20appliances.%0D%0D%0DBest%20Regards,%0D%0D%0D%0D%0D%0D//////////////////////////////%20%0D/////////%20Replace%20%5BNUMBER%5D%20with%20appropriate%20values%20related%20to%20your%20request.%0D/////////%20Replace%20%5BORGANIZATION%20NAME%5D%20with%20the%20name%20of%20the%20organization%20you%20represent.%0D//////////////////////////////%0D%0D)with a template request for Defender for IoT appliances.

For more information, see [Which appliances do I need?](../ot-appliance-sizing)

### Prepare ancillary hardware

If you're using physical appliances, make sure that you have the following extra hardware available for each physical appliance:

- A monitor and keyboard
- Rack space
- AC power
- A LAN cable to connect the appliance's management port to the network switch
- LAN cables for connecting mirror (SPAN) ports and network terminal access points (TAPs) to your appliance

### Prepare appliance network details

When you have your appliances ready, make a list of the following details for each appliance:

- IP address
- Subnet
- Default gateway
- Host name
- DNS server (optional), with the DNS server IP address and host name

## Prepare a deployment workstation

Prepare a workstation from where you can run Defender for IoT deployment activities. The workstation can be a Windows or Mac machine, with the following requirements:

- Terminal software, such as PuTTY
- A supported browser for connecting to sensor consoles and the Azure portal. For more information, see [recommended browsers for the Azure portal](/en-us/azure/azure-portal/azure-portal-supported-browsers-devices#recommended-browsers).
- Required firewall rules configured, with access open for required interfaces. For more information, see [Networking requirements](../networking-requirements).

## Prepare CA-signed certificates

We recommend using CA-signed certificates in production deployments.

Make sure that you understand the [SSL/TLS certificate requirements for on-premises resources](certificate-requirements). If you want to deploy a CA-signed certificate during initial deployment, make sure to have the certificate prepared.

If you decide to deploy with the built-in, self-signed certificate, we recommend that you deploy a CA-signed certificate in production environments later on.

For more information, see:

- [Create SSL/TLS certificates for OT appliances](../ot-deploy/create-ssl-certificates)
- [Manage SSL/TLS certificates](../how-to-manage-individual-sensors#manage-ssltls-certificates)