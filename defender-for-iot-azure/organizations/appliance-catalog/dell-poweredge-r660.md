---
layout: Conceptual
title: Dell PowerEdge R660 for operational technology (OT) monitoring - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/appliance-catalog/dell-poweredge-r660
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
description: Learn about the Dell PowerEdge R660 appliance's configuration when used for OT monitoring with Microsoft Defender for IoT in enterprise deployments.
ms.date: 2024-07-29T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: d9da3a74-ac3a-7b03-ded8-2fed3eb099f8
document_version_independent_id: 34ce4084-7b59-9ebc-61ed-226fcd5b282a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/appliance-catalog/dell-poweredge-r660.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/appliance-catalog/dell-poweredge-r660
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/appliance-catalog/dell-poweredge-r660.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 453fcf87-e268-6696-60e9-d408de7de263
---

# Dell PowerEdge R660 for operational technology (OT) monitoring - Microsoft Defender for IoT | Microsoft Learn

This article describes the Dell PowerEdge R660 appliance, supported for operational technology (OT) sensors in an enterprise deployment.

| Appliance characteristic | Description |
| --- | --- |
| **Hardware profile** | C5600 |
| **Performance** | Max bandwidth: 3 GbpsMax devices: 12,000 |
| **Physical Specifications** | Mounting: 1U with rail kitPorts: 6x RJ45 1 GbE |
| **Status** | Supported, available as a preconfigured appliance |

The following image shows a view of the Dell PowerEdge R660 front panel:

![Photograph of the Dell PowerEdge R660 front panel.](media/dell-poweredge-r660/dell-r660-front.png)

The following image shows a view of the Dell PowerEdge R660 back panel:

![Photograph of the Dell PowerEdge R660 back panel.](media/dell-poweredge-r660/dell-r660-back.png)

## Specifications

| Component | Technical specifications |
| --- | --- |
| Chassis | 1U rack server |
| Dimensions | Height: 1.68 in / 42.8 mm Width: 18.97 in / 482.0 cmDepth: 23.04 in / 585.3 mm (without bezel) 23.57 in / 598.9 mm (with bezel) |
| Processor | Intel Xeon E-2434 3.4 GHz 8M Cache 4C/8T, Turbo, HT (55 W) DDR5-4800 |
| Memory | 128 GB |
| Storage | 7.2 TB Hard Drive |
| Network controller | - PowerEdge R660 Motherboard with Broadcom 5720 Dual Port 1 Gb On-Board LOM, - PCIe Blank Filler, Low Profile. - Intel Ethernet i350 Quad Port 1 GbE BASE-T Adapter, PCIe Low Profile, V2 |
| Management | iDRAC Group Manager, Disabled |
| Rack support | ReadyRails Sliding Rails With Cable Management Arm |

## Dell PowerEdge R660 - Bill of materials

### Components

| Quantity | PN | Module | Description |
| --- | --- | --- | --- |
| 1 | 210-BFUZ | Base | PowerEdge R660xs |
| 1 | 461-AAIG | Trusted platform module | Trusted platform module 2.0 V3 |
| 1 | 470-AFQI | Chassis configuration | 2.5" Chassis with up to 8 Hard Drives (SAS/SATA), 2 CPU |
| 1 | 338-CKVW | Processor | Intel Xeon Silver 4410T 2.7 G 10C/20T, 16 GT/s, 27 M caches, Turbo, HT (150 W) DDR5-4000 |
| 1 | 338-CKVW | Additional processor | Intel Xeon Silver 4410T 2.7 G 10C/20T, 16 GT/s, 27 M caches, Turbo, HT (150 W) DDR5-4000 |
| 1 | 379-BDCO | Additional processor | Additional processor selected |
| 1 | 338-CHQT | Processor thermal configuration | Heatsink for 2 CPU configuration (CPU less than or equal to 150 W) |
| 1 | 370-AAIP | Memory configuration type | Performance Optimized |
| 1 | 370-AHCL | Memory DIMM type and speed | 4800-MT/s RDIMMs |
| 4 | 370-AGZP | Memory capacity | 8 \* 16 GB RDIMM, 4,800 MT/s single rank |
| 1 | 780-BCDS | RAID configuration | unconfigured RAID |
| 1 | 405-AAZB | RAID controller | PERC H755 SAS Front |
| 1 | 750-ACFR | RAID controller | Front PERC Mechanical Parts, front load |
| 8 | 161-BCBX | Hard drives | 2.4 TB Hard Drive SAS ISE 12 Gbps 10k 512e 2.5in Hot Plug |
| 1 | 384-BBBH | BIOS and Advanced System Configuration Settings | Power Saving BIOS Settings |
| 1 | 387-BBEY | Advanced System Configurations | No Energy Star |
| 1 | 384-BDJC | Fans | Standard Fan X7 |
| 1 | 528-CTIC | Embedded Systems Management | iDRAC9, Enterprise 16G |
| 1 | 450-AKLF | Power supply | Dual, Redundant(1+1), Hot-Plug Power Supply, 1100 W MM(100-240Vac) Titanium |
| 2 | 450-AADY | Power cords | C13 to C14, PDU Style, 10 AMP, 6.5 Feet (2 m), Power Cord |
| 1 | 330-BCCE | PCIe Riser | Riser Config 6, Low profile, 1x 16 LP slots (Gen 5) + 1x8 LP Slot (Gen 5), 2 CPU |
| 1 | 384-BDKV | Motherboard | PowerEdge R660xs Motherboard with Broadcom 5720 Dual Port 1 Gb On-Board LOM |
| 1 | 540-BCOB | Network daughter card | Broadcom 5720 Quad Port 1 GbE BASE-T Adapter, OCP NIC 3.0 |
| 1 | 350-BCEL | Quick sync | Quick Sync 2 (At-the-box mgmt) |
| 1 | 379-BCSF | Password | iDRAC, Factory Generated Password |
| 1 | 379-BCQX | IDRAC service module | iDRAC Service Module (ISM), NOT Installed |
| 1 | 379-BCQV | Group manager | iDRAC group manager, Enabled |
| 1 | 325-BEVH | Bezel | PowerEdge 1U Standard Bezel |
| 1 | 350-BEUF | Bezel | Dell Luggage Tag, 0/6/8/10 |
| 1 | 770-BCJI | Rack rails | A11 drop-in/stab-in Combo Rails Without Cable Management Arm |
| 1 | 340-DLRR | Shipping | PowerEdge R660XS Shipping EMEA1 (English/French/German/Spanish/Russian/Hebrew) |
| 1 | 340-DFKP | Shipping material | PowerEdge R660xs, 8x2.5, Short Drive Shipping Material |
| 1 | 389-FBMD | Regulatory | PowerEdge R660xs HS5610 Label, CE and CCC Marking, for below 1,300 W PSU |
| 1 | 683-11870 | Dell Services: Deployment Services | No Installation Service Selected (Contact Sales Rep for more details) |

### Software

| Quantity | PN | Module | Description |
| --- | --- | --- | --- |
| 1 | 800-BBDM | Advanced system configuration | UEFI BIOS Boot Mode with GPT Partition |
| 1 | 528-COYT | Embedded Systems Management | Secured Component Verification |
| 1 | 611-BBBF | Operating system | No operating system |
| 1 | 605-BBFN | OS media kits | No media required |
| 1 | 631-AACK | System documentation | No Systems Documentation, No OpenManage DVD Kit |

### Service

| Quantity | PN | Module | Description |
| --- | --- | --- | --- |
| 1 | 293-10049 | Shipping Box Labels - Standard | Order Configuration Shipbox Label (Ship Date, Model, Processor Speed, HDD Size, RAM) |
| 1 | 865-BBLL | Dell Services: Extended Service | ProSupport and Next Business Day Onsite Service Extension, 24 Months |
| 1 | 865-BBLM | Dell Services: Extended Service | ProSupport and Next Business Day Onsite Service Initial, 12 Months |
| 1 | 709-BBIX | Dell Services: Hardware Support | Parts Only Warranty 12 Months |

## Install Defender for IoT software on the DELL R660

This procedure describes how to install Defender for IoT software on the Dell R660.

The installation process takes about 20 minutes. During the installation, the system restarts several times.

To install Defender for IoT software:

1. Connect the screen and keyboard to the appliance, and then connect to the CLI.
2. Connect an external CD or disk-on-key that contains the software you downloaded from the Azure portal.
3. Start the appliance.
4. Continue with the generic procedure for installing Defender for IoT software. For more information, see [Defender for IoT software installation](../how-to-install-software).