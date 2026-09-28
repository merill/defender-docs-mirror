---
layout: Conceptual
title: DELL XE4 SFF for OT monitoring in SMB/ L500 deployments - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/appliance-catalog/dell-xe4-sff
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
description: Learn about the DELL XE4 SFF appliance when used for OT monitoring with Microsoft Defender for IoT in SMB/ L500 deployments.
ms.date: 2024-02-25T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: f6ea3568-c5bc-5e56-8539-357e05f5f9fd
document_version_independent_id: 363ebd14-d2d5-6a29-5ed3-127911e5b7e5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/appliance-catalog/dell-xe4-sff.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/appliance-catalog/dell-xe4-sff
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/appliance-catalog/dell-xe4-sff.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/97159432-14a9-4307-a469-d2f2c75f0e33
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/50565c62-5f6b-4687-be38-323113c72c2e
platformId: 4d324bfe-78db-8bf5-83e6-b379e20ad803
---

# DELL XE4 SFF for OT monitoring in SMB/ L500 deployments - Microsoft Defender for IoT | Microsoft Learn

This article describes the **DELL XE4 SFF** appliance deployment and installation for OT sensors monitoring production lines.

| Appliance characteristic | Details |
| --- | --- |
| **Hardware profile** | L500 |
| **Performance** | Max bandwidth: 25 Mbps  Max devices: 1,000 |
| **Physical specifications** | Mounting: Small Form Factor  Ports: 1x1Gbps (builtin) and optional expansion PCIe cards for copper and SFP connectors  1x RJ45 monitoring port |
| **Status** | Supported, available preconfigured |

The following image shows a sample of the DELL XE4 SFF front panel:

![Picture of the front view of the DELL XE4 SFF.](../media/tutorial-install-components/dell-xe4-sff-front-view.png)

The following image shows a sample of the DELL XE4 SFF back panel:

![Picture of the back view of the DELL XE4 SFF.](../media/tutorial-install-components/dell-xe4-sff-rear-view.png)

The following image shows the DELL XE4 SFF dust filter installation and maintenance:

![Picture of the dust filter of the DELL XE4 SFF.](../media/tutorial-install-components/dell-xe4-sff-dust-filter.png)

Note

For this appliance to operate properly, install a secondary NIC. For more information, see optional port expansion.

## Specifications

| Component | Technical specifications |
| --- | --- |
| Construction | Small Form Factor |
| Dimensions | 1. Width: 6.65 in. (169.00 mm) 2. Depth: 11.84 in. (300.80 mm) 3. Height: 14.45 in. (367.00 mm) |
| Weight | Weight (min): 14.13 lb (6.41 kg) Weight (max): 21.03 lb (9.54 kg) |
| CPU | 12th Generation Intel Core i5-12600 (6 Cores/18MB/12T/3.3GHz to 4.8GHz/65W) |
| Memory | 8 GB (1x8GB) DDR4 Non-ECC Memory |
| Storage | M.2 2280 512-GB PCIe NVMe Class 40 Solid State Drive |
| Network controller | Built-in 1x1Gbps |
| Power Adapter | 300-W internal power supply unit (PSU), 92% Efficient PSU, 80 Plus Platinum |
| PWS | 300-W internal power supply unit (PSU), 92% Efficient, 80 Plus Platinum, V3, TCO9 |
| Temperature | 5°C to 45°C (41°F to 113°F) |
| Dust Filter | Dell XE4 optional dust filter fits over the front of the chassis and safeguards internal components in areas such as factory, warehouse, and retail environments without impeding air flow. |
| Humidity | 20% to 80% (non-condensing, Max dew point temperature = 26°C) |
| Vibration | 0.26 GRMS random at 5 Hz to 350 Hz |
| Shock | Bottom/Right half-sine pulse 40G, 2 ms |
| EMC | Product Safety, EMC, and Environmental Datasheets https://www.dell.com/learn/us/en/uscorp1/product-info-datasheets-safety-emc-environmental |

## DELL XE4 SFF - Bill of materials

| Type | Description | PN | Quantity |
| --- | --- | --- | --- |
| Processor | 12th Generation Intel Core i5-12600 (6 Cores/18MB/12T/3.3GHz to 4.8GHz/65W) | 338-CCYL | 1 |
| Memory | 8 GB (1x8GB) DDR4 Non-ECC Memory | 370-AGFP | 1 |
| Storage | M.2 2280 512-GB PCIe NVMe Class 40 Solid State Drive | 400-BMWH | 1 |
| Storage | M.2 22x30 Thermal Pad | 412-AAQT | 1 |
| Storage | M2X3.5 Screw for SSD/DDPE | 773-BBBC | 1 |
| Speakers | Internal Speaker | 520-AARD | 1 |
| Graphics | Intel Integrated Graphics | 490-BBFG | 1 |
| Optical Drive | No Optical Drive | 429-ABKF | 1 |
| Network Adapters (NIC) | No Additional Network Card Selected (Integrated NIC included) | 555-BBJO | 1 |
| Power Cord | System Power Cord (UK/MY/SG/HK/Bangladesh/Brunei/Pakistan/Sri Lanka/Maldives) | 450-AANJ | 1 |
| Documentation | End User License Agreement (MUI) OEM | 340-ABMB | 1 |
| Keyboard | Dell Multimedia Keyboard-KB216 - UK (QWERTY) - Black | 580-ADDF | 1 |
| Mouse | Dell Optical Mouse-MS116 - Black | 570-ABJO | 1 |
| System Monitoring Options | System Monitoring not selected in this configuration | 817-BBSI | 1 |
| Additional Video Ports | No Additional Video Ports | 492-BCKH | 1 |
| Add-in Cards | No Additional Add In Cards | 382-BBHX | 1 |
| Additional Storage Devices - Media Reader | No Media Card Reader | 385-BBCR | 1 |
| Dust Protection | Dust Filter | 325-BDSX | 1 |
| Chassis Options | 300-W internal power supply unit (PSU), 92% Efficient, 80 Plus Platinum, V3, TCO9 | 329-BJVV | 1 |
| Systems Management | In-Band Systems Management | 631-ADFK | 1 |
| EPEAT 2018 | EPEAT 2018 Registered (Silver) | 379-BDTO | 1 |
| ENERGY STAR | ENERGY STAR Qualified | 387-BBLW | 1 |
| TPM Security | Trusted Platform Module (Discrete TPM Enabled) | 329-BBJL | 1 |
| Consolidation Fees - (EM-EMEA Only) | Consolidation Fee Desktop | 546-10007 | 1 |
| Shipping Material | OptiPlex OEM Small Form Factor Packaging and Labels | 328-BFCV | 1 |
| Optical Software | CMS Software not included | 632-BBBJ | 1 |
| Processor Label | Intel Core i5 Processor Label | 340-CUEW | 1 |
| Raid Connectivity | NO RAID | 817-BBBN | 1 |
| Transportation from ODM to region | Desktop BTO Standard shipment | 800-BBIO | 1 |
| Bezel | OEM, BRAND, XE4SFF, RM7WS2MN-V2, NOM, AVIGILON | 325-BFBS | 1 |
| Bezel | OEM Badge Small Form Factor | 340-DBRM | 1 |
| Bezel | Client ID Module info mod for no apps on OEM Client platform projects | 750-ABLB | 1 |
| OEMR XE4 Small Form Factor | OptiPlex XE4 Small Form Factor OEM-Ready | 210-BDLO | 1 |
| Hard Drive Cables and Brackets | No Hard Drive Bracket, Dell OptiPlex | 575-BBKX | 1 |
| Order Information | Dell Order | 799-AANV | 1 |
| BIOS Configuration - Standard | BIOS: NIC Set To On w/ PXE | 696-10356 | 1 |
| BIOS Configuration - Standard | BIOS Wake-On-Lan Set To Enabled-Same As Remote wake up | 696-10362 | 1 |
| BIOS Configuration - Standard | BIOS Setting Mandatory Enablement SKU | 696-10421 | 1 |
| Label | Regulatory Label XE4 OEM SFF EMEA | 389-EEGP | 1 |
| Operating System | Ubuntu Linux 20.04 | 605-BBNY | 1 |
| Operating System Recovery Options | No Media | 620-AAOH | 1 |
| Dell Services: Extended Service | ProSupport and Next Business Day Onsite Service Initial (Emerging only), 15 Months | 199-BINT | 1 |
| Dell Services: Extended Service | ProSupport and Next Business Day Onsite Service Extension (Emerging only), 21 Months | 199-BINU | 1 |
| Dell Services: Hardware Support | Parts Only Warranty 15 Months | 709-BDHS | 1 |
| Dell Services: GCP/ OEM PM | CSO OEM Solution Client Program Support, EMEA | 683-17925 | 1 |

## Optional port expansion

For this appliance to operate properly, install one of these secondary NICs.

Optional modules for port expansion include:

| Description | PN | Quantity |
| --- | --- | --- |
| Dell Intel Ethernet i350 Quad Port 1-GbE Base-T Adapter PCIe Full Height | 540-BDLF | 1 |
| Intel 1 GB Single Port PCIe Network card (half height) | 540-BBMO | 1 |
| Intel X710 Dual Port 10 GbE SFP+ Adapter | 540-BDQZ | 1 |

## Set up the Dell XE4 BIOS

This procedure describes how to configure the BIOS configuration for an unconfigured sensor appliance. If any of the steps are missing in the BIOS, make sure that the hardware matches the specifications above. Set up the Dell XE4 BIOS to achieve optimal performance for sensors.

**To configure the Dell XE4 BIOS**:

1. Set up **Boot Mode**

    1. Select **System setup options** &gt; **Boot Configuration menu** &gt; **Boot Mode**
    2. Set to **UEFI Only**
2. Set up **Installation boot from USB/DVD (as applicable)**

    1. Select **System setup options** &gt; **Boot Configuration menu** &gt; **Boot Sequence**
    2. Select the installation disk drive as the first option
3. Set up **Restart on Power Loss**

    1. Select **System setup options** &gt; **Power Menu** &gt; **AC Behavior**
    2. Set to **Restart**
4. Disable Sleep/Hibernation

    1. Select **System setup options** &gt; **Power Menu** &gt; **Block Sleep**
    2. Enable **Block Sleep**

## Dell XE4 software setup

This procedure describes how to install Defender for IoT software on the Dell XE4. The installation process takes about 20 minutes. After the installation, the system restarts several times.

To install Defender for IoT software:

1. Connect the screen and keyboard to the appliance, and then connect to the CLI.
2. Connect an external CD or disk-on-key that contains the software you downloaded from the Azure portal.
3. Switch on the appliance.
4. Continue by installing your Defender for IoT software. For more information, see [Defender for IoT software installation](../ot-deploy/install-software-ot-sensor#install-defender-or-iot-software-on-ot-sensors).