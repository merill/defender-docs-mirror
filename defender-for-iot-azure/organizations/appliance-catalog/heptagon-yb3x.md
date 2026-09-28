---
layout: Conceptual
title: Heptagon Systems YB3x for OT monitoring in L100 deployments - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/appliance-catalog/heptagon-yb3x
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
description: Learn about the Heptagon Systems YB3x appliance when used for OT monitoring with Microsoft Defender for IoT in L100 deployments.
ms.date: 2024-04-01T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: 84fc59ea-3a95-0537-8a81-6d7547cbb660
document_version_independent_id: c4ad32f8-a454-00c7-4335-04c70c5a7d93
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/appliance-catalog/heptagon-yb3x.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/appliance-catalog/heptagon-yb3x
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/appliance-catalog/heptagon-yb3x.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 2815bf74-142f-b6c8-a41e-475d2d0d806d
---

# Heptagon Systems YB3x for OT monitoring in L100 deployments - Microsoft Defender for IoT | Microsoft Learn

This article describes the **Heptagon Systems YB3x** appliance deployment and installation for OT sensors.

| Appliance characteristic | Details |
| --- | --- |
| **Hardware profile** | L100 |
| **Performance** | Max bandwidth: 20-25 Mbps  Max devices: 200 |
| **Physical specifications** | Ports: 6 x 1-GbE ports |
| **Status** | Supported, available as preconfigured |

The following image shows a view of the Heptagon Systems YB3x front panel:

![Picture of the front view of the Heptagon Systems YB3x.](media/yb3x.png)

## Specifications

| Component | Technical specifications |
| --- | --- |
| Construction | Fanless cooling |
| Dimensions | 1U, 209x187x37.5mm |
| Weight | 1.1 kg |
| CPU | Intel C3708 – 8 cores |
| Memory | 16 GB |
| Storage | 500 GB |
| Network controller | Intel I210, Intel x553 |
| Device access | 4x USB 3.0, TPM 2.0, 2x Serial ports |
| Power Adapter | 12 VDC or optional 9-28 VDC with reverse polarity, Over/under voltage protection |
| BMC | BMC AST2600, OpenBMC, IPMI 2.0, iKVM, Virtual Media |
| Temperature | -40 °C to +75 °C |
| Humidity | 95% @ 40°C (noncondensing) |
| Shock & Vibration | ETSI standard ETS 300 019-1-5, 5M2 |
| Safety | IEC 60950-1, AS/NZS |
| EMC | CE, FCC, AS/NZS |

## Heptagon Systems YB3x - Bill of Materials

| Description | PN | Quantity |
| --- | --- | --- |
| CPU: Atom-C3708, 8C, 16 MB Cache, 1.7Ghz, 17 W, Embedded/Ind. Temp  DRAM - Not installed  COMM1: COM-4X1: Quad 1G Base-T  COMM2: No Comm Module  BMC: BMC, based on Aspeed AST2600, with Display port video | YB3708-0-4T0B | 1 |
| 500G NV2 M.2 2280 PCIe 4.0 NVMe SSD | SNV2S/500G | 1 |
| Intel X710 Dual Port 10 GbE SFP+ Adapter | 540-BDQZ | 1 |
| 8 GB 2,666 MT/s DDR4 ECC Reg CL19 DIMM 1Rx8 Hynix D IDT | KSM26RS8/8HDI | 2 |
| Power supply, 110-220 VAC to 12 VDC, 100 W, IP 67, Industrial temp | PS100-12-IP67 | 1 |

## Heptagon Systems YB3x software setup

This procedure describes how to install Defender for IoT software on the Heptagon Systems YB3x. The installation process takes about 20 minutes. After the installation, the system restarts several times.

To install Defender for IoT software:

1. Connect the screen and keyboard to the appliance, and then connect to the CLI.
2. Connect an external CD or disk-on-key that contains the software you downloaded from the Azure portal.
3. Start the appliance.
4. Continue by installing your Defender for IoT software. For more information, see [Defender for IoT software installation](../ot-deploy/install-software-ot-sensor#install-defender-or-iot-software-on-ot-sensors).