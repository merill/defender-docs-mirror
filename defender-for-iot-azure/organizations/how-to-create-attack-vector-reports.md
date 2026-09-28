---
layout: Conceptual
title: Create attack vector reports in Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/how-to-create-attack-vector-reports
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
description: Attack vector reports provide a graphical representation of a vulnerability chain of exploitable devices.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 0e6ad4c3-127d-d391-35c0-afcbac1ec799
document_version_independent_id: b74e9220-6712-4d48-f957-1546f081617e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/how-to-create-attack-vector-reports.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/how-to-create-attack-vector-reports
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/how-to-create-attack-vector-reports.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 390e9d8a-ecd0-48a1-8fcf-00bab5b56005
---

# Create attack vector reports in Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn

Attack vector reports show a chain of vulnerable devices in a specified attack path, for devices detected by a specific OT network sensor. Simulate an attack on a specific target in your network to discover vulnerable devices and analyze attack vectors in real time.

Attack vector reports can also help evaluate mitigation activities to ensure that you're taking all required steps to reduce the risk to your network. For example, use an attack vector report to understand whether a software update would disrupt a potential attack path, or if an alternate attack path still remains.

## Prerequisites

To create attack vector reports, you must be able to access the OT network sensor you want to generate data for, as an **Admin** or **Security Analyst** user.

For more information, see [On-premises users and roles for OT monitoring with Defender for IoT](roles-on-premises)

## Generate an attack vector simulation

Generate an attack vector simulation so that you can view the resulting report.

To generate an attack vector simulation:

1. Sign into the sensor console and select **Attack vector** on the left.
2. Select **Add simulation** and enter the following values:

    | Property | Description |
    | --- | --- |
    | **Name** | Simulation name |
    | **Maximum Vectors** | The maximum number of attack vectors you want to include in the simulation. |
    | **Show in Device Map** | Select to show the attack vector as a group in the **Device map**. |
    | **Show All Source Devices** | Select to consider all devices as a possible attack source. |
    | **Attack Source** | Appears only, and required, if the **Show All Source Devices** option is toggled off. Select one or more devices to consider as the attack source. |
    | **Show All Target Devices** | Select to consider all devices as possible attack targets. |
    | **Attack Target** | Appears only, and required, if the **Show All Target Devices** option is toggled off. Select one or more devices to consider as the attack target. |
    | **Exclude Devices** | Select one or more devices to exclude from the attack vector simulation. |
    | **Exclude Subnets** | Select one or more subnets to exclude from the attack vector simulation. |
3. Select **Save**. Your simulation is added to the list, with the number of attack paths indicated in parenthesis.
4. Expand your simulation to view the list of possible attack vectors, and select one to view more details on the right.

    For example:

    [![Screen shot of Attack vectors report.](media/how-to-generate-reports/sample-attack-vectors.png)](media/how-to-generate-reports/sample-attack-vectors.png#lightbox)

## View an attack vector in the Device Map

The Device map provides a graphical representation of vulnerable devices detected in attack vector reports. To view an attack vector in the Device map:

1. In the **Attack vector** page, make sure your simulation has **Show in Device map** toggled on.
2. Select **Device map** from the side menu.
3. Select your simulation and then select an attack vector to visualize the devices in your map.

    For example:

    [![Screen shot of Device map.](media/how-to-generate-reports/sample-device-map.png)](media/how-to-generate-reports/sample-device-map.png#lightbox)

For more information, see [Investigate sensor detections in the Device map](how-to-work-with-the-sensor-device-map).