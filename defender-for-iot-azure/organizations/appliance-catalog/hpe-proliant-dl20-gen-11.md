---
layout: Conceptual
title: HPE ProLiant DL20 Gen 11 (4SFF) for OT monitoring in SMB/ E1800 deployments - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/appliance-catalog/hpe-proliant-dl20-gen-11
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
description: Learn about the HPE ProLiant DL20 Gen 11 (4SFF) appliance when used for OT monitoring with Microsoft Defender for IoT in SMB deployments.
ms.date: 2024-04-09T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: 313e81c9-0931-1549-ba95-465f90af0c0a
document_version_independent_id: 0a3862a8-fc05-00c3-95b1-88f50119976e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/appliance-catalog/hpe-proliant-dl20-gen-11.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/appliance-catalog/hpe-proliant-dl20-gen-11
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/appliance-catalog/hpe-proliant-dl20-gen-11.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 70e4d654-d684-d667-fcb2-48c05176faf9
---

# HPE ProLiant DL20 Gen 11 (4SFF) for OT monitoring in SMB/ E1800 deployments - Microsoft Defender for IoT | Microsoft Learn

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
| Physical Characteristics | HPE DL20 Gen11 4SFF Ht Plg CTO Server |
| Processor | Intel Xeon E-2434 3.4-GHz 4-core 55 W FIO Processor for HPE |
| Chipset | Intel C262 |
| Memory | HPE 16 GB (1 x 16 GB) Single Rank x8 DDR5-4800 CAS-40-39-39 Unbuffered Standard Memory |
| Storage | HPE 1.2 TB SAS 12 G Mission Critical 10 K SFF |
| Network controller | On-board: 2 x 1 Gb |
| External | 1 x HPE Ethernet 1-Gb 4-port 366FLR Adapter |
| On-board | On-board: 4x 1 Gb |
| Management | HPE iLO Advanced |
| Device access | Front: One USB 3.0 1 x USB iLO Service Port Rear: Two USBs 3.0 |
| External | 1 x Broadcom BCM5719 Ethernet 1 Gb 4-port BASE-T Adapter for HPE |
| Internal | One USB 3.2 |
| Power | HPE 1,000 W Flex Slot Titanium Hot Plug Power Supply Kit |
| Rack support | HPE 1U Short Friction Rail Kit |

## DL20 Gen11 (4SFF) - Bill of materials

| Quantity | PN | Description |
| --- | --- | --- |
| 1 | P65392-B21 | HPE ProLiant DL20 Gen 11 4SFF Hot Plug Configure-to-order Server |
| 1 | P65392-B21 B19 | HPE DL20 Gen11 4SFF Ht Plg CTO Server |
| 1 | P65224-B21 | Intel Xcon E-2434 3.4-GHz 4-core 55 W FIO Processor for HPE |
| 2 | P64336-B21 | HPE 16 GB (1 x 16 GB) Single Rank x8 DDR5-4800 CAS-40-39-39 Unbuffered Standard Memory Kit |
| 4 | P28586-B21 | HPE 1.2 TB SAS 12 G Mission Critical 10K SFF BC 3-year Warranty Multi Vendor HDD |
| 1 | P52753-B21 | HPE ProLiant DL320 Genll x 16 FHHL Riser Kit |
| 1 | P51178-B21 | Broadcom BCM5719 Ethernet 1-Gb 4-port BASE-T Adapter for HPE |
| 1 | P47789-B21 | HPE MRi-o Gen11 x 16 Lanes without Cache OCP SPDM Storage Controller |
| 2 | P03178-B21 | HPE 1,000 W Flex Slot Titanium Hot Plug Power Supply Kit |
| 1 | BD505A | HPE iLO Advanced 1-server License with 3 yr Support on iLO Licensed Features |
| 1 | P65412-B21 | HPE ProLiant DL20 Gen11 2LFF/4SFF OCP Cable Kit |
| 1 | P64576-B21 | HPE Easy Install Rail 12 Kit |
| 1 | P65407-B21 | HPE ProLiant DL20 Gen 11 LP iLO/M.2 Enablement Kit |

### Install Defender for IoT software on the HPE ProLiant DL20 Gen 11 (4SFF)

This procedure describes how to install Defender for IoT software on the HPE ProLiant DL20 Gen 11 (4SFF).

The installation process takes about 20 minutes. After the installation, the system is restarted several times.

**To install Defender for IoT software**:

1. Connect the screen and keyboard to the appliance, and then connect to the CLI.
2. Connect an external CD or disk-on-key that contains the software you downloaded from the Azure portal.
3. Start the appliance.
4. Continue with the generic procedure for installing Defender for IoT software. For more information, see [Defender for IoT software installation](../how-to-install-software).