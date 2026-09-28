---
layout: Conceptual
title: Dell PowerEdge R360 for operational technology (OT) monitoring - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/appliance-catalog/dell-poweredge-r360-e1800
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
description: Learn about the Dell PowerEdge R360 appliance's configuration when used for OT monitoring with Microsoft Defender for IoT in enterprise deployments.
ms.date: 2024-07-16T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: f52c17c5-76fd-c871-37e4-cc81a0114f8b
document_version_independent_id: 28781417-89f1-f1b7-7dfe-532fbbcf266d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/appliance-catalog/dell-poweredge-r360-e1800.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/appliance-catalog/dell-poweredge-r360-e1800
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/appliance-catalog/dell-poweredge-r360-e1800.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 957982fa-2037-9546-6fec-74d9670fbeda
---

# Dell PowerEdge R360 for operational technology (OT) monitoring - Microsoft Defender for IoT | Microsoft Learn

This article describes the Dell PowerEdge R360 appliance, supported for operational technology (OT) sensors in an enterprise deployment.

| Appliance characteristic | Description |
| --- | --- |
| **Hardware profile** | E1800 |
| **Performance** | Max bandwidth: 1 GbpsMax devices: 10,000 |
| **Physical Specifications** | Mounting: 1U with rail kitPorts: 6x RJ45 1 GbE |
| **Status** | Supported, available as a preconfigured appliance |

The following image shows a view of the Dell PowerEdge R360 front panel:

![Photograph of the Dell PowerEdge R360 front panel.](../media/tutorial-install-components/r360-front.png)

The following image shows a view of the Dell PowerEdge R360 back panel:

![Photograph of the Dell PowerEdge R360 back panel.](../media/tutorial-install-components/r360-rear.png)

## Specifications

| Component | Technical specifications |
| --- | --- |
| Chassis | 1U rack server |
| Dimensions | Height: 1.68 in / 42.8 mm Width: 18.97 in / 482.0 cmDepth: 23.04 in / 585.3 mm (without bezel) 23.57 in / 598.9 mm (with bezel) |
| Processor | Intel Xeon E-2434 3.4 GHz 8M Cache 4C/8T, Turbo, HT (55 W) DDR5-4800 |
| Memory | 32 GB |
| Storage | 2.4 TB Hard Drive |
| Network controller | - PowerEdge R360 Motherboard with with Broadcom 5720 Dual Port 1Gb On-Board LOM, - PCIe Blank Filler, Low Profile. - Intel Ethernet i350 Quad Port 1GbE BASE-T Adapter, PCIe Low Profile, V2 |
| Management | iDRAC Group Manager, Disabled |
| Rack support | ReadyRails Sliding Rails With Cable Management Arm |

## Dell PowerEdge R360 - Bill of materials

| Quantity | PN | Description |
| --- | --- | --- |
| 1 | 210-BJTR | Base PowerEdge R360 Server |
| 1 | 461-AAIG | Trusted Platform Module 2.0 V3 |
| 1 | 321-BKHP | 2.5" Chassis with up to 8 Hot Plug Hard Drives, Front PERC |
| 1 | 338-CMRB | Intel Xeon E-2434 3.4G, 4C/8T, 8M Cache, Turbo, HT (55 W) DDR5-4800 |
| 1 | 412-BBHK | Heatsink |
| 1 | 370-AAIP | Performance Optimized |
| 1 | 370-BBKS | 4800 MT/s UDIMMs |
| 2 | 370-BBKF | 16 GB UDIMM, 4800 MT/s ECC |
| 1 | 780-BCDQ | RAID 10 |
| 1 | 405-ABCQ | PERC H355 Controller Card |
| 1 | 750-ACFR | Front PERC Mechanical Parts, front load |
| 4 | 400-BEFU | 1.2 TB Hard Drive SAS 12 Gbps 10k 512n 2.5in Hot Plug |
| 1 | 384-BBBH | Power Saving BIOS Settings |
| 1 | 387-BBEY | No Energy Star |
| 1 | 384-BDML | Standard Fan |
| 1 | 528-CTIC | iDRAC9, Enterprise 16G |
| 2 | 450-AADY | C13 to C14, PDU Style, 10 AMP, 6.5 Feet (2m), Power Cord |
| 1 | 330-BCMK | Riser Config 2, Butterfly Gen4 Riser (x8/x8) |
| 1 | 329-BJTH | PowerEdge R360 Motherboard with with Broadcom 5720 Dual Port 1Gb On-Board LOM |
| 1 | 414-BBJB | PCIe Blank Filler, Low Profile |
| 1 | 540-BDII | Intel Ethernet i350 Quad Port 1GbE BASE-T Adapter, PCIe Low Profile, V2, FIRMWARE RESTRICTIONS APPLY |
| 1 | 379-BCRG | iDRAC, Factory Generated Password, No OMQR |
| 1 | 379-BCQX | iDRAC Service Module (ISM), NOT Installed |
| 1 | 325-BEVH | PowerEdge 1U Standard Bezel |
| 1 | 350-BCTP | Dell Luggage Tag R360 |
| 1 | 379-BCQY | iDRAC Group Manager, Disabled |
| 1 | 470-AFBU | BOSS Blank |
| 1 | 770-BCWN | ReadyRails Sliding Rails With Cable Management Arm |
| 2 | 450-AKMP | Dual, Hot-Plug, Redundant Power Supply (1+1), 600W MM **for US** Dual, Hot-Plug, Redundant Power Supply (1+1), 700W MM HLAC (Only for 200-240Vac) titanium **for Europe** |

## Install Defender for IoT software on the DELL R360

This procedure describes how to install Defender for IoT software on the Dell R360.

The installation process takes about 20 minutes. During the installation, the system restarts several times.

To install Defender for IoT software:

1. Connect the screen and keyboard to the appliance, and then connect to the CLI.
2. Connect an external CD or disk-on-key that contains the software you downloaded from the Azure portal.
3. Start the appliance.
4. Continue with the generic procedure for installing Defender for IoT software. For more information, see [Defender for IoT software installation](../how-to-install-software).