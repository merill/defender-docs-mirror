---
layout: Conceptual
title: YS-techsystems YS-FIT2 for OT monitoring - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/appliance-catalog/ys-techsystems-ys-fit2
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
description: Learn about the YS-techsystems YS-FIT2 appliance when used for OT monitoring with Microsoft Defender for IoT.
ms.date: 2022-04-24T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: 323a682a-e5b7-0430-0953-f4840d772d92
document_version_independent_id: 2b55e2df-ba88-3d91-b5b0-8d946b80ce78
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/appliance-catalog/ys-techsystems-ys-fit2.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/appliance-catalog/ys-techsystems-ys-fit2
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/appliance-catalog/ys-techsystems-ys-fit2.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 0d7f6111-dedf-dfdf-312a-657dccbcf458
---

# YS-techsystems YS-FIT2 for OT monitoring - Microsoft Defender for IoT | Microsoft Learn

This article describes the **YS-techsystems YS-FIT2** appliance deployment and installation for OT sensors.

| Appliance characteristic | Details |
| --- | --- |
| **Hardware profile** | L100 |
| **Performance** | Max bandwidth: 10 MbpsMax devices: 100 |
| **Physical specifications** | Mounting: DIN/VESAPorts: 2x RJ45 |
| **Status** | Supported; Available as pre-configured |

The following image shows a view of the YS-FIT2 front panel:

![A photo of the front panel of the YS-FIT2.](../media/tutorial-install-components/fitlet-front-panel.png)

The following image shows a view of the YS-FIT2 back panel:

![A photo of the back panel of the YS-FIT2.](../media/tutorial-install-components/fitlet2-back-panel.png)

## Specifications

| Components | Technical specifications |
| --- | --- |
| Construction | Aluminum or zinc die-cast parts, fanless and dust-proof design |
| Dimensions | 112 mm (W) x 112 mm (D) x 25 mm (H)4.41in (W) x 4.41in (D) x 0.98 in (H) |
| Weight | 0.35 kg |
| CPU | Intel Atom® x7-E3950 Processor |
| Memory | 8 GB SODIMM 1 x 204-pin DDR3L non-ECC 1866 (1.35 V) |
| Storage | 128 GB M.2 M-key 2260\* or 2242 (SATA 3 6 Gbps) PLP |
| Network controller | Two 1 GbE LAN Ports |
| Device access | Two USB 2.0, Two USB 3.0 |
| Power Adapter | 7V-20V (Optional 9V-36V) DC / 5W-15W Power AdapterVehicle DC cable for YS-FIT2 (Optional) |
| UPS | Fit-uptime Miniature 12 V UPS for miniPCs (Optional) |
| Mounting | VESA / wall or Din Rail mounting kit |
| Temperature | 0°C ~ 60°C |
| Humidity | 5% ~ 95%, non-condensing |
| Vibration | IEC TR 60721-4-7:2001+A1:03, Class 7M1, test method IEC 60068-2-64 (up to 2 KHz, 3 axis) |
| Shock | IEC TR 60721-4-7:2001+A1:03, Class 7M1, test method IEC 60068-2-27 (15 g , 6 directions) |
| EMC | CE/FCC Class B |

## YS-FIT2 installation

This section describes how to install OT sensor software on the YS-FIT2 appliance. Before you install the OT sensor software, you must adjust the appliance's BIOS configuration.

Note

Installation procedures are only relevant if you need to re-install software on a pre-configured device, or if you buy your own hardware and configure the appliance yourself.

### Configure the YS-FIT2 BIOS

This procedure describes how to update the YS-FIT2 BIOS configuration for your OT sensor deployment.

**To configure the YS-FIT2 BIOS**:

1. Power on the appliance and go to **Main** &gt; **OS Selection**.
2. Press **+/-** to select **Linux**.

    ![Screenshot of setting the OS to Linux on your YS-FIT2.](../media/tutorial-install-components/fitlet-linux.png)
3. Verify that the system date and time are updated with the installation date and time.
4. Go to **Advanced**, and select **ACPI Settings**.
5. Select **Enable Hibernation**, and press **+/-** to select **Disabled**.

    ![Screenshot of turning off the hibernation mode on your YS-FIT2.](../media/tutorial-install-components/disable-hibernation.png)
6. Press **Esc**.
7. Go to **Advanced** &gt; **TPM Configuration**.
8. Select **fTPM**, and press **+/-** to select **Disabled**.
9. Press **Esc**.
10. Go to **CPU Configuration** &gt; **VT-d**.
11. Press **+/-** to select **Enabled**.
12. Go to **CSM Configuration** &gt; **CSM Support**.
13. Press **+/-** to select **Enabled**.
14. Go to **Advanced** &gt; **CSM Configuration** and change the setting in the following fields to **Legacy**:

    - Network
    - Storage
    - Video
    - Other PCI

    ![Screenshot of setting all fields to Legacy.](../media/tutorial-install-components/legacy-only.png)
15. Press **Esc**.
16. Go to **Security** &gt; **Secure Boot Customization**.
17. Press **+/-** to select **Disabled**.
18. Press **Esc**.
19. Go to **Boot** &gt; **Boot mode** select, and select **UEFI**.
20. Select **Boot Option #1 – [USB CD/DVD]**.
21. Select **Save & Exit**.

### Install OT sensor software on the YS-FIT2

This procedure describes how to install OT sensor software on the YS-FIT2.

The installation takes approximately 20 minutes. After the installation is complete, the system restarts several times.

**To install OT sensor software**:

1. Connect an external CD or disk-on-key that contains the sensor software you downloaded from the Azure portal.
2. Boot the appliance.
3. Select **English**.
4. Select **XSENSE-RELEASE-&lt;version&gt; Office...**.
5. Define the appliance architecture, and network properties:

    | Parameter | Configuration |
    | --- | --- |
    | **Hardware profile** | Select **office**. |
    | **Management interface** | **em1** |
    | **Management network IP address** | **IP address provided by the customer** |
    | **Management subnet mask** | **IP address provided by the customer** |
    | **DNS** | **IP address provided by the customer** |
    | **Default gateway IP address** | **0.0.0.0** |
    | **Input interface** | The list of input interfaces is generated for you by the system.  To mirror the input interfaces, copy all the items presented in the list with a comma separator. |
    | **Bridge interface** | - |

    For more information, see [Install OT monitoring software](../how-to-install-software#install-ot-monitoring-software).
6. Accept the settings and continue by entering `Y`.

After approximately 10 minutes, sign-in credentials are automatically generated. Save the username and passwords, you'll need these credentials to access the platform the first time you use it.