---
layout: Conceptual
title: Configure a Micro Agent T#### win - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/how-to-configure-micro-agent-twin
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
description: Learn how to view and update Microsoft Defender for IoT micro agent twin configuration properties, such as message frequency and collector settings, through the Azure portal.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: ea766723-eed1-b318-bd23-8b0791b69be9
document_version_independent_id: 371dd0c5-6c46-906a-cc2a-bb359e0a6983
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/how-to-configure-micro-agent-twin.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/how-to-configure-micro-agent-twin
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/how-to-configure-micro-agent-twin.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/816835a3-1c5d-4536-835c-4b59dc9c9d97
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/a98c4e96-5248-4755-860b-6c76f1933f0c
platformId: f3ae872f-a07c-f2f2-0a81-b643046429f8
---

# Configure a Micro Agent T#### win - Microsoft Defender for IoT | Microsoft Learn

The Microsoft Defender for IoT micro agent twin lets you customize the security agent's behavior for each device. By editing the module identity twin's desired properties in the Azure portal, you can control settings such as message frequency, collector enablement, and cache sizes. This article walks you through viewing and updating those configuration properties in IoT Hub. Before you begin, make sure you have the required Azure account, Defender for IoT subscription, and IoT Hub setup described in the Prerequisites.

Note

Defender for IoT plans to retire the micro agent on June 1, 2027.

## Prerequisites

Before you configure the micro agent twin, make sure you have the following prerequisites:

- An Azure account. If you do not already have an Azure account, you can [create your Azure free account today](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- A Defender for IoT subscription.
- An existing IoT Hub with: [A connected device](tutorial-standalone-agent-binary-installation), and [A micro agent module twin](tutorial-create-micro-agent-module-twin).

## Micro agent configuration

To view and update the micro agent twin configuration:

1. Navigate to the [Azure portal](https://portal.azure.com).
2. Search for, and select **IoT Hub**.

    ![Screenshot of searching for the IoT hub in the search bar.](media/tutorial-micro-agent-configuration/iot-hub.png)
3. Select your IoT Hub from the list.
4. Under the Device management section, select **Devices**.

    ![Screenshot of the device management section of the IoT hub.](media/tutorial-micro-agent-configuration/devices.png)
5. Select your device from the list.
6. Select the module ID.

    ![Screenshot of the device's module ID selection screen.](media/tutorial-micro-agent-configuration/module-id.png)
7. In the Module Identity Details screen, select **Module Identity Twin**.

    ![Screenshot of the Module Identity Details screen.](media/tutorial-micro-agent-configuration/module-identity-twin.png)
8. Change the value of any field by adding the field to the `"desired"` section with the new value.

    ![Screenshot of the sample output of the module identity twin.](media/tutorial-micro-agent-configuration/desired.png)

    For example:

    ```
    "desired": {
        "Baseline_Disabled": false,
        "Baseline_MessageFrequency": "Low",
        "Baseline_GroupsDisabled": "",
        "Baseline_ChecksDisabled": "",
        "SystemInformation_Disabled": false,
        "SystemInformation_MessageFrequency": "Low",
        "SBoM_Disabled": false,
        "SBoM_MessageFrequency": "Low",
        "NetworkActivity_Disabled": false,
        "NetworkActivity_MessageFrequency": "Medium",
        "NetworkActivity_Devices": "eth0",
        "NetworkActivity_CacheSize": 256,
        "Process_Disabled": false,
        "Process_MessageFrequency": "Medium",
        "Process_PollingInterval": 100000,
        "Process_Mode": 1,
        "Process_CacheSize": 256,
        "LogCollector_Disabled": false,
        "LogCollector_MessageFrequency": "Low",
        "Heartbeat_Disabled": false,
        "Heartbeat_MessageFrequency": "Low",
        "Login_Disabled": false,
        "Login_MessageFrequency": "Medium",
        "IothubModule_MessageTimeout": 2880,
        "CollectorsCore_PriorityIntervals": "30,120,1440"
    }
    ```

    For the full list of supported properties, see [Micro agent configurations](concept-micro-agent-configuration).

    The micro agent successfully set the new configuration if the value of `"latest_state"`, under the `"reported"` section shows `"success"`.

    ![Screenshot of a successful configuration change.](media/tutorial-micro-agent-configuration/reported-success.png)

    If the micro agent fails to set the new configuration, the value of `"latest_state"`, under the `"reported"` section will show `"failed"`. If the configuration update fails, the `"latest_invalid_fields"` will contain a list of the fields that are invalid.