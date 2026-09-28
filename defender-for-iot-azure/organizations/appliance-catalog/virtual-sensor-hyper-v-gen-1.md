---
layout: Conceptual
title: OT sensor VM (Microsoft Hyper-V) Gen 1- Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/appliance-catalog/virtual-sensor-hyper-v-gen-1
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
description: Learn about deploying a Microsoft Defender for IoT OT sensor as a virtual appliance using Microsoft Hyper-V.
ms.date: 2024-03-27T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: ab2c591f-5a35-7768-7942-eeb32511f8df
document_version_independent_id: 39bf0dbc-6c82-cade-efeb-ec26dda98f6f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/appliance-catalog/virtual-sensor-hyper-v-gen-1.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/appliance-catalog/virtual-sensor-hyper-v-gen-1
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/appliance-catalog/virtual-sensor-hyper-v-gen-1.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/2ed91286-6cf7-4b83-810d-75d0ee3b09dd
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/6735bd7e-4f7b-457d-b58c-29e6f0198677
platformId: 0ad5703e-4649-be8e-eb52-3e8b514d5ede
---

# OT sensor VM (Microsoft Hyper-V) Gen 1- Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn

This article describes an OT sensor deployment on a virtual appliance using Microsoft Hyper-V.

| Appliance characteristic | Details |
| --- | --- |
| **Hardware profile** | As required for your organization. For more information, see [Which appliances do I need?](../ot-appliance-sizing) |
| **Performance** | As required for your organization. For more information, see [Which appliances do I need?](../ot-appliance-sizing) |
| **Physical specifications** | Virtual Machine |
| **Status** | Supported |

Note

We recommend using the 2nd Generation configuration, which offers better performance and increased security, for configuration see [Microsoft Hyper-V Gen 2](virtual-sensor-hyper-v).

Important

Versions 22.2.x of the sensor are incompatible with Hyper-V, and are no longer supported. We recommend using the latest version.

## Prerequisites

Before you begin the installation, make sure you have the following items:

- Microsoft Hyper-V hypervisor (Windows 10 Pro or Enterprise) installed and operational. For more information, see [Introduction to Hyper-V on Windows 10](/en-us/virtualization/hyper-v-on-windows/about).
- Available hardware resources for the virtual machine. For more information, see [OT monitoring with virtual appliances](../ot-virtual-appliances).
- The OT sensor software [downloaded from Defender for IoT in the Azure portal](../ot-deploy/install-software-ot-sensor#download-software-files-from-the-azure-portal).

Make sure the hypervisor is running.

Note

There is no need to pre-install an operating system on the VM, the sensor installation includes the operating system image.

## Create the virtual machine

This procedure describes how to create a virtual machine by using Hyper-V.

**To create the virtual machine using Hyper-V**:

1. Create a virtual disk in Hyper-V Manager (Fixed size, as required by the hardware profile).
2. Select **format = VHDX**.
3. Enter the name and location for the VHD.
4. Enter the required size [according to your organization's needs](../ot-appliance-sizing) (select Fixed Size disk type).
5. Review the summary, and select **Finish**.
6. On the **Actions** menu, create a new virtual machine.
7. Enter a name for the virtual machine.
8. Select **Generation** and set it to **Generation 1**, and then select **Next**.
9. Specify the memory allocation [according to your organization's needs](../ot-appliance-sizing), in standard RAM denomination (for example, 8192, 16384, 32768). Don't enable **Dynamic Memory**.
10. Configure the network adaptor according to your server network topology. Under the "Hardware Acceleration" blade, disable "Virtual Machine Queue" for the monitoring (SPAN) network interface.
11. Connect the VHDX, created previously, to the virtual machine.
12. Review the summary, and select **Finish**.
13. Right-click on the new virtual machine, and select **Settings**.
14. Select **Add Hardware**, and add a new network adapter.
15. Select the virtual switch that connects to the sensor management network.
16. Allocate CPU resources [according to your organization's needs](../ot-appliance-sizing).
17. Select **BIOS**, in **Startup order** move **IDE** to the top of the list, select **Apply** and then select **OK**.
18. Connect the OT sensor's ISO image to a virtual DVD drive.
19. Start the virtual machine.
20. On the **Actions** menu, select **Connect** to continue the software installation.

## Software installation

1. To start installing the OT sensor software, open the virtual machine console.

    The VM starts from the ISO image, and the language selection screen will appear.
2. Continue with the [generic procedure for installing sensor software](../how-to-install-software).