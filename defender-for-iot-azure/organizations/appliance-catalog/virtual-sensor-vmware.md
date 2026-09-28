---
layout: Conceptual
title: OT sensor VM (VMware ESXi) - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/appliance-catalog/virtual-sensor-vmware
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
description: Learn about deploying a Microsoft Defender for IoT OT sensor as a virtual appliance using VMware ESXi.
ms.date: 2023-08-20T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: 1c1c46d1-086c-7013-184b-0056e6b9176f
document_version_independent_id: 40102b37-e67c-314c-7c16-b1466e523846
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/appliance-catalog/virtual-sensor-vmware.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/appliance-catalog/virtual-sensor-vmware
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/appliance-catalog/virtual-sensor-vmware.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/2ed91286-6cf7-4b83-810d-75d0ee3b09dd
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/6735bd7e-4f7b-457d-b58c-29e6f0198677
platformId: 272c9910-2c45-9841-2168-b55738082e47
---

# OT sensor VM (VMware ESXi) - Microsoft Defender for IoT | Microsoft Learn

This article describes an OT sensor deployment on a virtual appliance using VMware ESXi.

| Appliance characteristic | Details |
| --- | --- |
| **Hardware profile** | As required for your organization. For more information, see [Which appliances do I need?](../ot-appliance-sizing) |
| **Performance** | As required for your organization. For more information, see [Which appliances do I need?](../ot-appliance-sizing) |
| **Physical specifications** | Virtual Machine |
| **Status** | Supported |

## Prerequisites

Before you begin the installation, make sure you have the following items:

- VMware (ESXi 5.5 or later) installed and operational
- Available hardware resources for the virtual machine. For more information, see [OT monitoring with virtual appliances](../ot-virtual-appliances).
- The OT sensor software [downloaded from Defender for IoT in the Azure portal](../ot-deploy/install-software-ot-sensor#download-software-files-from-the-azure-portal).
- Traffic mirroring configured on your vSwitch. For more information, see [Configure traffic mirroring with a ESXi vSwitch](../traffic-mirroring/configure-mirror-esxi).

Make sure the hypervisor is running.

Note

There is no need to pre-install an operating system on the VM, the sensor installation includes the operating system image.

## Create the virtual machine

This procedure describes how to create a virtual machine by using ESXi.

**To create the virtual machine using ESXi**:

1. Sign in to the ESXi, choose the relevant **datastore**, and select **Datastore Browser**.
2. Select **Upload**, to upload the image, and select **Close**.
3. Navigate to VM, and then select **Create/Register VM**.
4. Select **Create new virtual machine**, and then select **Next**.
5. Add a sensor name, and select the following options:

    - Compatibility: **&lt;latest ESXi version&gt;**
    - Guest OS family: **Linux**
    - Guest OS version: **Debian**
6. Select **Next**.
7. Choose the relevant datastore and select **Next**.
8. Change the virtual hardware parameters according to the required architecture.
9. For **CD/DVD Drive 1**, select **Datastore ISO file** and choose the ISO file that you uploaded earlier.
10. In your VM options, change your boot options from **Firmware** to **BIOS**. Make sure that you're not booting from EFI.
11. Select **Next** &gt; **Finish**.

## Software installation

1. To start installing the OT sensor software, open the virtual machine console.

    The VM will start from the ISO image, and the language selection screen will appear.
2. Continue with the [generic procedure for installing sensor software](../ot-deploy/install-software-ot-sensor).