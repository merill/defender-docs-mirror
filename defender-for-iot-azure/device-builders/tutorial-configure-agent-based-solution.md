---
layout: Conceptual
title: Configure Microsoft Defender for IoT agent-based solution - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/tutorial-configure-agent-based-solution
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
ms.subservice: device-builders
description: Learn how to configure the Microsoft Defender for IoT agent-based solution
ms.date: 2022-01-12T00:00:00.0000000Z
ms.topic: tutorial
locale: en-us
document_id: 417babff-6259-0793-82fc-4c5c8ae719a6
document_version_independent_id: 36f411cc-c171-e76b-1292-15439cb6b9b5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/tutorial-configure-agent-based-solution.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/tutorial-configure-agent-based-solution
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/tutorial-configure-agent-based-solution.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 71df8deb-9ecb-3ee4-7990-e87aa005210b
---

# Configure Microsoft Defender for IoT agent-based solution - Microsoft Defender for IoT | Microsoft Learn

This tutorial will help you learn how to configure the Microsoft Defender for IoT agent-based solution.

In this tutorial you'll learn how to:

- Enable data collection
- Create a Log Analytics workspace
- Enable geolocation and IP address handling

Note

Defender for IoT plans to retire the micro agent on June 1, 2027.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- An [IoT hub](/en-us/azure/iot-hub/iot-hub-create-through-portal).
- You must have [enabled Microsoft Defender for IoT on your Azure IoT Hub](quickstart-onboard-iot-hub).
- You must have [added a resource group to your IoT solution](quickstart-configure-your-solution)
- You must have [created a Defender for IoT micro agent module twin](quickstart-create-micro-agent-module-twin).
- You must have [installed the Defender for IoT micro agent](quickstart-standalone-agent-binary-installation)

## Enable data collection

**To enable data collection**:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Navigate to **IoT Hub** &gt; **`Your hub`** &gt; **Defender for IoT** &gt; **Settings** &gt; **Data Collection**.

    ![Select data collection from the security menu settings.](media/how-to-configure-agent-based-solution/data-collection.png)
3. Under **Microsoft Defender for IoT**, ensure that **Enable Microsoft Defender for IoT** is enabled.

    ![Screenshot showing you how to enable data collection.](media/how-to-configure-agent-based-solution/enable-data-collection.png)
4. Select **Save**.

## Create a Log Analytics workspace

Defender for IoT allows you to store security alerts, recommendations, and raw security data, in your Log Analytics workspace. Log Analytics ingestion in IoT Hub is set to **off** by default in the Defender for IoT solution. It is possible, to attach Defender for IoT to a Log Analytics workspace, and to store the security data there as well.

There are two types of information stored by default in your Log Analytics workspace by Defender for IoT:

- Security alerts.
- Recommendations.

You can choose to add storage of an additional information type as `raw events`.

Note

Storing `raw events` in Log Analytics carries additional storage costs.

**To enable Log Analytics to work with micro agent**:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Navigate to **IoT Hub** &gt; **`Your hub`** &gt; **Defender for IoT** &gt; **Settings** &gt; **Data Collection**.
3. Under the **Workspace configuration**, switch the Log Analytics toggle to **On**.
4. Select a subscription from the drop-down menu.
5. Select a workspace from the drop-down menu. If you don't already have an existing Log Analytics workspace, you can select **Create New Workspace** to create a new one.
6. Verify that the **Access to raw security data** option is selected.

    ![Ensure Access to raw security data is selected.](media/how-to-configure-agent-based-solution/data-settings.png)
7. Select **Save**.

Every month, the first 5 gigabytes of data ingested, per customer to the Azure Log Analytics service, is free. Every gigabyte of data ingested into your Azure Log Analytics workspace, is retained at no charge for the first 31 days. For more information on pricing, see, [Log Analytics pricing](https://azure.microsoft.com/pricing/details/monitor/).

## Enable geolocation and IP address handling

In order to secure your IoT solution, the IP addresses of the incoming, and outgoing connections for your IoT devices, IoT Edge, and IoT Hub(s) are collected and stored by default. This information is essential, and used to detect abnormal connectivity from suspicious IP address sources. For example, when there are attempts made that try to establish connections from an IP address source of a known botnet, or from an IP address source outside your geolocation. The Defender for IoT service, offers the flexibility to enable, and disable the collection of the IP address data at any time.

**To enable the collection of IP address data**:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Navigate to **IoT Hub** &gt; **`Your hub`** &gt; **Defender for IoT** &gt; **Settings** &gt; **Data Collection**.
3. Ensure the IP data collection checkbox is selected.

    ![Screenshot that shows the checkbox needed to be selected to enable geolocation.](media/how-to-configure-agent-based-solution/geolocation.png)
4. Select **Save**.

## Clean up resources

There are no resources to clean up.