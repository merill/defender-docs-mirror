---
layout: Conceptual
title: OT monitoring with virtual appliances - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/ot-virtual-appliances
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
description: Learn about system requirements for virtual appliances used for the Microsoft Defender for IoT OT sensors.
ms.date: 2022-05-03T00:00:00.0000000Z
ms.topic: limits-and-quotas
locale: en-us
document_id: 959c1528-3191-c19a-c69c-b20cb1154926
document_version_independent_id: 9f351519-1ce3-53ac-44ff-2ff7c6345b08
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/ot-virtual-appliances.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/ot-virtual-appliances
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/ot-virtual-appliances.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 82bc61fd-66ad-992b-5cd9-e9f6f81291d5
---

# OT monitoring with virtual appliances - Microsoft Defender for IoT | Microsoft Learn

This article is one in a series of articles that describe the [deployment path](ot-deploy/ot-deploy-path) for operational technology (OT) monitoring with Microsoft Defender for IoT. The article lists the specifications that are required if you want to install Microsoft Defender for IoT software on your own virtual appliances.

[![Diagram of a progress bar with Plan and prepare highlighted.](media/deployment-paths/progress-plan-and-prepare.png)](media/deployment-paths/progress-plan-and-prepare.png#lightbox)

## About hypervisors

The virtualized hardware used to run guest operating systems is supplied by virtual machine hosts, also known as *hypervisors*. Defender for IoT supports the following hypervisor software:

- **VMware ESXi** (version 5.0 and later)
- **Microsoft Hyper-V** (VM configuration version 8.0 and later)

Learn more:

- [OT sensor as a virtual appliance with VMware ESXi](appliance-catalog/virtual-sensor-vmware)
- [OT sensor as a virtual appliance with Microsoft Hyper-V](appliance-catalog/virtual-sensor-hyper-v)

Important

Other types of hypervisors, such as hosted hypervisors, may also run Defender for IoT. However, due to their lack of exclusive hardware control and resource reservation, other types of hypervisors aren't supported for production environments. For example: Parallels, Oracle VirtualBox, and VMware Workstation or Fusion

## Virtual appliance design considerations

This section outlines considerations for virtual appliance components, for both OT sensors and on-premises monitoring consoles.

| Specification | Considerations |
| --- | --- |
| **CPU** | Assign dedicated CPU cores (also known as pinning) with at least 2.4 GHz, which aren't dynamically allocated. CPU usage is high because the appliance continuously records and analyzes network traffic. CPU performance is critical to capturing and analyzing network traffic, and any slowdown could lead to packet drops and performance degradation. |
| **Memory** | RAM should be allocated statically for the required capacity, not dynamically. Expect high RAM utilization due to the sensor's constant network traffic recording and analytics, |
| **Network interfaces** | Physical mapping provides best performance, lowest latency, and efficient CPU usage. Our recommendation is to physically map network interface cards (NICs) to the virtual machines with SR-IOV or a dedicated NIC.  As a result of high traffic monitoring levels, expect high network utilization.  Set the promiscuous mode on your vSwitch to **Accept**, which allows all traffic to reach the VM. Some vSwitch implementations may block certain protocols if it isn't configured correctly. |
| **Storage** | Make sure to allocate enough read and write Input-Output Processors (IOPs) and throughput to match the performance of the appliances listed in this article. You should expect high storage usage due to the large traffic monitoring volumes. |

## OT network sensor VM requirements

The following tables list system requirements for OT network sensors on virtual appliances, and performance measured in our qualification labs.

For all deployments, bandwidth results for virtual machines may vary, depending on the distribution of protocols and the actual hardware resources that are available, including the CPU model, memory bandwidth, and IOPS.

| Hardware profile | Performance / Monitoring | Physical specifications |
| --- | --- | --- |
| **C5600** | **Max bandwidth**: 2.5 Gb/sec **Max monitored assets**: 12,000 | **vCPU**: 32 **Memory**: 32 GB **Storage**: 5.6 TB (600 IOPS) |
| **E1800** | **Max bandwidth**: 800 Mb/sec **Max monitored assets**: 10,000 | **vCPU**: 8 **Memory**: 32 GB **Storage**: 1.8 TB (300 IOPS) |
| **E1000** | **Max bandwidth**: 800 Mb/sec **Max monitored assets**: 10,000 | **vCPU**: 8 **Memory**: 32 GB **Storage**: 1 TB (300 IOPS) |
| **E500** | **Max bandwidth**: 800 Mb/sec **Max monitored assets**: 10,000 | **vCPU**: 8 **Memory**: 32 GB **Storage**: 500 GB (300 IOPS) |
| **L500** | **Max bandwidth**: 160 Mb/sec **Max monitored assets**: 1,000 | **vCPU**: 4 **Memory**: 8 GB **Storage**: 500 GB (150 IOPS) |
| **L100** | **Max bandwidth**: 100 Mb/sec **Max monitored assets**: 800 | **vCPU**: 4 **Memory**: 8 GB **Storage**: 100 GB (150 IOPS) |

To review system requirements and performance details for OT network sensors on specific virtual appliances, see the [appliance catalog](appliance-catalog/).

Note

You don't need to preinstall an operating system on the VM, the sensor installation includes the operating system image.