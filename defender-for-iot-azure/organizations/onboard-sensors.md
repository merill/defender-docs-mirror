---
layout: Conceptual
title: Onboard sensors to Defender for IoT in the Azure portal - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/onboard-sensors
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
description: Learn how to onboard sensors to Defender for IoT in the Azure portal.
ms.date: 2024-11-17T00:00:00.0000000Z
ms.topic: install-set-up-deploy
ms.collection:
- zerotrust-extra
locale: en-us
document_id: 1228d7cc-47d3-bf17-0c22-83623cbc31fc
document_version_independent_id: 659d4b27-b19b-bc25-4562-d6e3d5251caf
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/onboard-sensors.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/onboard-sensors
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/onboard-sensors.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: dc613f59-8cf6-bccd-7c76-d2724899d0ef
---

# Onboard sensors to Defender for IoT in the Azure portal - Microsoft Defender for IoT | Microsoft Learn

This article is one in a series of articles describing the [deployment path](ot-deploy/ot-deploy-path) for OT monitoring with Microsoft Defender for IoT, and describes how to onboard OT network sensors to [Microsoft Defender for IoT in the Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_IoT_Defender/IoTDefenderDashboard/Getting_Started).

[![Diagram of a progress bar with Onboard sensors highlighted.](media/deployment-paths/progress-onboard-sensors.png)](media/deployment-paths/progress-onboard-sensors.png#lightbox)

## Prerequisites

Before you onboard an OT network sensor to Defender for IoT, make sure that you have the following:

- An [OT plan onboarded](getting-started) to Defender for IoT
- Access to the Azure portal as a [Security Admin](/en-us/azure/role-based-access-control/built-in-roles#security-admin), [Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor), or [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) user.
- An understanding of which [site and zone](best-practices/plan-corporate-monitoring#plan-ot-sites-and-zones) you'll want to assign to your sensor.

    Assigning sensors to specific sites and zones is an integral part of implementing a [Zero Trust security strategy](concept-zero-trust), and will help you monitor for unauthorized traffic crossing segments. For more information, see [List your planned OT sensors](best-practices/plan-prepare-deploy#list-your-planned-ot-sensors).

This step is performed by your deployment teams.

## Onboard an OT sensor

This procedure describes how to onboard an OT network sensor with Defender for IoT and download a sensor activation file.

**To onboard your OT sensor to Defender for IoT**:

1. In the Azure portal, go to **Defender for IoT** &gt; **Getting started** and select **Set up OT/ICS Security**.

    Alternately, from the Defender for IoT **Sites and sensors** page, select **Onboard OT sensor** &gt; **OT**.
2. By default, on the **Set up OT/ICS Security** page, **Step 1: Did you set up a sensor?** and **Step 2: Configure SPAN port or TAP​** of the wizard are collapsed.

    You'll install software and configure traffic mirroring later on in the deployment process, but should have your appliances ready and traffic mirroring method planned. For more information, see:

    - [Prepare on-premises appliances](best-practices/plan-prepare-deploy#prepare-on-premises-appliances)
    - [Choose a traffic mirroring method for traffic monitoring](best-practices/traffic-mirroring-methods)
3. In **Step 3: Register this sensor with Microsoft Defender for IoT** enter or select the following values for your sensor:

    1. In the **Sensor name** field, enter a meaningful name for your OT sensor.

        We recommend including your OT sensor's IP address as part of the name, or using another easily identifiable name. You'll want to keep track of the registration name in the Azure portal and the IP address of the sensor shown in the OT sensor console.
    2. In the **Subscription** field, select your Azure subscription.

        If you don't yet have a subscription to select, select **Onboard subscription** to [add an OT plan to your Azure subscription](getting-started).
    3. (Optional) Toggle on the **Cloud connected** option to view detected data and manage your sensor from the Azure portal, and to connect your data to other Microsoft services, such as Microsoft Sentinel.

        For more information, see [Cloud-connected vs. local OT sensors](architecture#cloud-connected-vs-local-ot-sensors).
    4. (Optional) Toggle on the **Automatic Threat Intelligence updates** to have Defender for IoT automatically push [threat intelligence packages](how-to-work-with-threat-intelligence-packages) to your OT sensor.
    5. In the **Site** section, enter the following details:

        | Field name | Description |
        | --- | --- |
        | **Resource name** | Select the site you want to attach your sensors to, or select **Create site** to create a new site. **If you're creating a new site**: 1. In the **New site** field, enter your site's name and select the checkmark button. 2. From the **Site size** menu, select your site's size. The sizes listed in this menu are the sizes that you're licensed for, based on the licenses [you'd purchased](how-to-manage-subscriptions) in the Microsoft 365 admin center. If you're working with a legacy OT plan, the **Site size** field isn't included. |
        | **Display name** | Enter a meaningful name for your site to be shown across Defender for IoT. |
        | **Tags** | Enter tag key and values to help you identify and locate your site and sensor in the Azure portal. |
        | **Zone** | Select the zone you want to use for your OT sensor, or select **Create zone** to create a new one. |

    For example:

    [![Screenshot of the process for onboarding an OT sensor, assigning the site and zone setting.](media/onboard-sensors/onboard-ot-sensor.png)](media/onboard-sensors/onboard-ot-sensor.png#lightbox)
4. When you're done with all other fields, select **Register**. A success message appears and your activation file is automatically downloaded.
5. Select **Finish**. Your sensor is now shown under the selected site on the Defender for IoT **Sites and sensors** page.

Until you activate your sensor, the sensor's status shows as **Pending Activation**. Make the downloaded activation file accessible to the sensor console admin so that they can [activate the sensor](ot-deploy/activate-deploy-sensor).

All files downloaded from the Azure portal are signed by root of trust so that your machines use signed assets only.

Note

If you're working with a large deployment, we recommend that you use the Azure portal to manage cloud-connected sensors, and an OT sensor to manage locally-managed sensors.