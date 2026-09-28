---
layout: Conceptual
title: Create a DefenderforIoTMicroAgent module twin - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/tutorial-create-micro-agent-module-twin
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
description: In this tutorial, you'll learn how to create a DefenderIotMicroAgent module twin for new devices.
ms.date: 2022-01-16T00:00:00.0000000Z
ms.topic: tutorial
ms.custom: mode-other
locale: en-us
document_id: e5a2a483-2e07-bd77-54bb-4e0a812c0deb
document_version_independent_id: 427a1623-c111-c060-ade2-b04ce88171b3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/tutorial-create-micro-agent-module-twin.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/tutorial-create-micro-agent-module-twin
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/tutorial-create-micro-agent-module-twin.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/816835a3-1c5d-4536-835c-4b59dc9c9d97
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/a98c4e96-5248-4755-860b-6c76f1933f0c
platformId: d43a6dd8-bcb2-fb8d-967e-86d50b061f88
---

# Create a DefenderforIoTMicroAgent module twin - Microsoft Defender for IoT | Microsoft Learn

This tutorial will help you learn how to create an individual `DefenderIotMicroAgent` module twin for new devices.

Note

Defender for IoT plans to retire the micro agent on June 1, 2027.

## Device twins

Device twins play a key role in both device management and process automation, for IoT solutions that are built in to Azure.

Defender for IoT offers the capability to fully integrate your existing IoT device management platform, enabling you to manage your device security status and make use of the existing device control capabilities. You can integrate your Defender for IoT by using the IoT Hub twin mechanism.

To learn more about the general concept of module twins in Azure IoT Hub, see [Understand and use module twins in IoT Hub](/en-us/azure/iot-hub/iot-hub-devguide-module-twins).

Defender for IoT uses the module twin mechanism, and maintains a Defender-IoT-micro-agent twin named `DefenderIotMicroAgent` for each of your devices.

To take full advantage of all Defender for IoT features, you need to create, configure, and use the Defender-IoT-micro-agent twins for every device in the service.

## Defender-IoT-micro-agent twin

Defender for IoT uses a Defender-IoT-micro-agent twin for each device. The Defender-IoT-micro-agent twin holds all of the information that is relevant to device security for each specific device in your solution. Device security properties are configured through a dedicated Defender-IoT-micro-agent twin for safer communication, to enable updates, and maintenance that requires fewer resources.

In this tutorial you'll learn how to:

- Create a DefenderIotMicroAgent module twin
- Verify the creation of a module twin

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Verify you are running one of the following [operating systems](concept-agent-portfolio-overview-os-support).
- An [IoT hub](/en-us/azure/iot-hub/iot-hub-create-through-portal).
- You must have [enabled Microsoft Defender for IoT on your Azure IoT Hub](quickstart-onboard-iot-hub).
- You must have [added a resource group to your IoT solution](quickstart-configure-your-solution).

## Create a DefenderIotMicroAgent module twin

A `DefenderIotMicroAgent` module twin can be created by manually editing each module twin to include specific configurations for each device.

**To create a DefenderIotMicroAgent module twin for a device**:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Navigate to **IoT Hub** &gt; **`Your hub`** &gt; **Device management** &gt; **Devices**.
3. Select your device from the list.
4. Select **Add module identity**.
5. In the **Module Identity Name** field, enter `DefenderIotMicroAgent`.
6. Select **Save**.

## Verify the creation of a module twin

**To verify the creation of a DefenderIotMicroAgent module twin on a specific device**:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Navigate to **IoT Hub** &gt; **`Your hub`** &gt; **Device management** &gt; **Devices**.
3. Select your device.
4. Under the **Module Identities** tab, confirm the existence of the `DefenderIotMicroAgent` module in the list of module identities associated with the device.

    ![Select module identities from the tab.](media/quickstart-create-micro-agent-module-twin/device-details-module.png)