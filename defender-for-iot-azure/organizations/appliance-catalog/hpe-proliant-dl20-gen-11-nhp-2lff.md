---
layout: Conceptual
title: HPE ProLiant DL20 Gen 11 (NHP 2LFF) for OT monitoring in SMB/ L500 deployments - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/appliance-catalog/hpe-proliant-dl20-gen-11-nhp-2lff
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
description: Learn about the HPE ProLiant DL20 Gen 11 (NHP 2LFF) appliance when used for OT monitoring with Microsoft Defender for IoT in SMB deployments.
ms.date: 2024-04-09T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: 949c1097-3927-a8c0-9b37-3d7c592362b4
document_version_independent_id: 1a6eb8d7-c363-966e-28c0-5a6c64fbe715
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/appliance-catalog/hpe-proliant-dl20-gen-11-nhp-2lff.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/appliance-catalog/hpe-proliant-dl20-gen-11-nhp-2lff
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/appliance-catalog/hpe-proliant-dl20-gen-11-nhp-2lff.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 224e6bc6-bd5a-7b93-2b42-f9c8769005e3
---

# HPE ProLiant DL20 Gen 11 (NHP 2LFF) for OT monitoring in SMB/ L500 deployments - Microsoft Defender for IoT | Microsoft Learn

This article describes the **HPE ProLiant DL20 Gen 11** appliance for OT sensors monitoring production lines.

| Appliance characteristic | Details |
| --- | --- |
| **Hardware profile** | L500 |
| **Performance** | Max bandwidth: 200 Mbps Max devices: 1,000 |
| **Physical specifications** | Mounting: 1U  Ports: 4x RJ45 |
| **Status** | Supported, not available pre-configured |

## Specifications

| Component | Technical specifications |
| --- | --- |
| Chassis | 1U rack server |
| Dimensions | 4.32 x 43.46 x 37.84 cm  1.69 x 17.11 x 15.25in |
| Processor | Intel Xeon E-2434 3.4 GHz 4-core 55 W |
| Chipset | Intel C262 |
| Memory | HPE 16 GB (1 x 16 GB) Single Rank x8 DDR5-4800 |
| Storage | HPE 1 TB SATA 6 G Business Critical 7.2 K LFF |
| Network controller | On-board: 4 x 1 Gb |
| On-board | iLO Port Card 1 Gb |
| External | 1 x Broadcom BCM5719 Ethernet 1 Gb 4-port BASE-T Adapter for HPE |
| Management | HPE iLO Advanced |
| Device access | Front: One USB 3.2 1 x USB iLO Service Port Rear: Four USBs 3.2 |
| External | 1 x Broadcom BCM5719 Ethernet 1 Gb 4-port BASE-T Adapter for HPE |
| Internal | One USB 3.2 |
| Power | HPE 800 W Flex Slot Titanium Hot Plug Low Halogen Power Supply Kit |
| Rack support | HPE Easy Install Rail 12 Kit |

## DL20 Gen11 (NHP 2LFF) - Bill of materials

| Quantity | PN | Description |
| --- | --- | --- |
| 1 | P65390-B21 | HPE ProLiant DL20 Gen 11 2LFF Non-hot Plug Configure-to-order Server |
| 1 | P65390-B21 B19 | HPE DL20 Gen11 2LFF NHP CTO Svr |
| 1 | P65224-B21 | Intel Xeon E-2434 3.4-GHz 4-core 55 W FIO Processor for HPE |
| 1 | P64336-B21 | HPE 16 GB (1 x 16 GB) Single Rank x8 DDR5-4800 CAS-40-39-39 Unbuffered Standard Memory Kit |
| 1 | 801882-B21 | HPE 1 TB SATA 6 G Business Critical 7.2 K LFF RW 1-year Warranty Multi Vendor HDD |
| 1 | P52753-B21 | HPE ProLiant DL320 Genll x 16 FHHL Riser Kit |
| 1 | P51178-B21 | Broadcom BCM5719 Ethernet 1-Gb 4-port BASE-T Adapter for HPE |
| 1 | 865438-B21 | HPE 800 W Flex Slot Titanium Hot Plug Low Halogen Power Supply Kit |
| 1 | AF573A | HPE C13 - C14 WW 250V 10 Amp Flint Gray 2.0 m Jumper Cord |
| 1 | 512485-B21 | HPE iLO Advanced 1-server License with 1 yr Support on iLO Licensed Features |
| 1 | P64576-B21 | HPE Easy Install Rail 12 Kit |
| 1 | P65407-B21 | HPE ProLiant DL20 Gen11 LP iLO/M.2 Enablement Kit |

### Install Defender for IoT software on the HPE ProLiant DL20 Gen 11 (NHP 2LFF)

This procedure describes how to install Defender for IoT software on the HPE ProLiant DL20 Gen 11 (NHP 2LFF).

The installation process takes about 20 minutes. After the installation, the system is restarted several times.

**To install Defender for IoT software**:

1. Connect the screen and keyboard to the appliance, and then connect to the CLI.
2. Connect an external CD or disk-on-key that contains the software you downloaded from the Azure portal.
3. Start the appliance.
4. Continue with the generic procedure for installing Defender for IoT software. For more information, see [Defender for IoT software installation](../how-to-install-software).