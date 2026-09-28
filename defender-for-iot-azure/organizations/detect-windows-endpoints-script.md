---
layout: Conceptual
title: Enrich Windows workstation and server data with a local script - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/detect-windows-endpoints-script
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
description: Learn about how to enrich Windows workstation and server data on your OT sensor using a local script.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 801d44e0-e871-d1ef-c84e-e4fe02257285
document_version_independent_id: 214cff1f-42be-84d7-dc4c-797e0dd78935
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/detect-windows-endpoints-script.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/detect-windows-endpoints-script
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/detect-windows-endpoints-script.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 8c4ea4a5-4bd3-4c2a-8588-98f15db023af
---

# Enrich Windows workstation and server data with a local script - Microsoft Defender for IoT | Microsoft Learn

Note

This feature is in PREVIEW. The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include other legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

In addition to detecting OT devices on your network, use Defender for IoT to discover Microsoft Windows workstations and servers and enrich workstation and server data for devices already detected. Same as other detected devices, detected Windows workstations and servers are displayed in the Device inventory. The **Device inventory** pages on the sensor show enriched data about Windows devices, including data about the Windows operating system and applications installed, patch-level data, open ports, and more.

This article describes how to use a Defender for IoT Windows-based WMI tool to get extended information from Windows devices, such as workstations, servers, and more. Run the WMI script on your Windows devices to get extended information, increasing your device inventory and security coverage. While you can also use [scheduled WMI scans](configure-windows-endpoint-monitoring) to obtain this data, scripts can be run locally for regulated networks with waterfalls and one-way elements if WMI connectivity isn't possible.

The script described in this article returns the following details about each detected device:

- IP address
- MAC address
- Operating system
- Service pack
- Installed programs
- Last knowledge base update

If an OT network sensor has already detected a Windows workstation or server, running the script outlined in this article retrieves that device's information and enrichment data.

## Prerequisites

Before performing the procedures in this article, you must have:

- An OT network sensor with the [OT sensor software installed](ot-deploy/install-software-ot-sensor) and [configured and activated](ot-deploy/activate-deploy-sensor).
- Access to your OT network sensor as an **Admin** user. For more information, see [On-premises users and roles for OT monitoring with Defender for IoT](roles-on-premises).
- Administrator permissions on any devices where you intend to run the script.

### Supported operating systems

The script described in this article is supported for the following Windows operating systems:

- Windows XP
- Windows 7
- Windows 10
- Windows 11
- Windows Server 2003/2008/2012/2016/2019/2022

## Download and run the script

This procedure describes how to deploy and run a script on the Windows workstation and servers that you want to monitor in Defender for IoT.

The script detects enriched Windows data, and is run as a utility and not an installed program. Running the script doesn't affect the endpoint. You may want to deploy the script once, or using ongoing automation, using standard automated deployment methods and tools.

1. Sign into your OT sensor console, and select **System Settings** &gt; **Import Settings** &gt; **Windows Information**.
2. Select **Download script**. Your browser might ask you if you want to keep the file, select **Keep** or any similar options.

    [![Screenshot of where to download WMI script.](media/detect-windows-endpoints-script/download-wmi-script.png)](media/detect-windows-endpoints-script/download-wmi-script.png#lightbox)
3. Copy the file to a local drive and unzip it. The following file appears:

    - `Extract_system_info.bat`
4. Run the `Extract_system_info.bat` file.
5. You'll be asked whether you want to display errors on screen or not. Make you own selection.

After the script runs to probe the registry, an output file appears with the registry information. The filename indicates the current date and time of the snapshot with the following syntax: `[current date time]_system_info_extractor`.

Files generated by the script:

- Remain on the local drive until you delete them.
- Are overwritten if you run the script again on the same day.
- Include an errorOutput file that is empty if no errors occurred during the running of the script.

## Import device details

After running the script as described in Download and run the script, import the generated data to your sensor to view the device details in the **Device inventory**.

**To import device details to your sensor**:

1. Use standard, automated methods and tools to move the generated files from each Windows endpoint to a location accessible from your OT sensors.

    Don't update filenames or separate the files from each other.
2. Sign into your OT sensor console, and select **System Settings** &gt; **Import Settings** &gt; **Windows Information**.
3. Select **Import File**, and then select the relevant file.

    [![Screenshot of where to import WMI script.](media/detect-windows-endpoints-script/import-wmi-script.png)](media/detect-windows-endpoints-script/import-wmi-script.png#lightbox)

## View the device applications report

After you download and run the script, then import the device details to your sensor, you can view your devices' applications with a custom data mining report.

To view the devices' applications:

1. Sign into your OT sensor console, and select **Data mining**.
2. Select **+ Create report** to [create an OT sensor custom data mining report](how-to-create-data-mining-queries#create-an-ot-sensor-custom-data-mining-report). In the **Choose Category** field, select **Devices Applications**. For example:

    [![Screenshot of creating devices applications custom report.](media/detect-windows-endpoints-script/devices-applications-report.png)](media/detect-windows-endpoints-script/devices-applications-report.png#lightbox)
3. Your devices applications report is shown in the **My reports** area.