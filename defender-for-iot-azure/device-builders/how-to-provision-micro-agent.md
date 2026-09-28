---
layout: Conceptual
title: Provision the Microsoft Defender for IoT Micro Agent by using DPS - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/how-to-provision-micro-agent
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
description: Learn how to provision the Microsoft Defender for IoT micro agent using DPS.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: f959bcf2-e353-6ce0-2a17-cc05cbac1695
document_version_independent_id: 02878ffb-3cd2-2130-178f-87e06886a407
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/how-to-provision-micro-agent.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/how-to-provision-micro-agent
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/how-to-provision-micro-agent.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/816835a3-1c5d-4536-835c-4b59dc9c9d97
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/a98c4e96-5248-4755-860b-6c76f1933f0c
platformId: 8dc0c3db-cfe6-4484-dd26-5c3ec7e46c55
---

# Provision the Microsoft Defender for IoT Micro Agent by using DPS - Microsoft Defender for IoT | Microsoft Learn

This article explains how to provision the standalone Microsoft Defender for IoT micro agent by using [Azure IoT Hub Device Provisioning Service](/en-us/azure/iot-dps/about-iot-dps) with [X.509 certificate attestation](/en-us/azure/iot-dps/concepts-x509-attestation). Follow this procedure to enroll a standalone device through DPS, create and configure a micro agent module, and verify that the agent connects successfully. If you're provisioning IoT Edge devices instead, see the Edge-device guidance linked below.

To learn how to configure the Microsoft Defender for IoT micro agent for Edge devices see [Create and provision IoT Edge devices at scale](/en-us/azure/iot-edge/how-to-provision-devices-at-scale-linux-tpm)

Note

Defender for IoT plans to retire the micro agent on June 1, 2027.

## Prerequisites

Before you begin, make sure you have the following prerequisites:

- An Azure account with an active subscription. For more information, see [Create an Azure account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- An [IoT hub](/en-us/azure/iot-hub/iot-hub-create-through-portal).
- [IoT Hub Device Provisioning Service](/en-us/azure/iot-dps/quick-setup-auto-provision).

## Provision the device through DPS

Perform the following steps to provision the device through DPS:

1. In the [Azure portal](https://portal.azure.com), go to your instance of the IoT Hub device provisioning service.
2. Under **Settings**, select **Manage enrollments**.
3. Select **Add individual enrollment**, and then complete the steps to configure the enrollment:

    - In the **Mechanism** field, select **X.509** at the identity attestation Mechanism and choose your CA.
4. Navigate into your destination IoT Hub.
5. [Create a Defender for IoT micro agent module twin](tutorial-create-micro-agent-module-twin) issued by the same X.509 certificate used for the DPS enrollment.
6. [Configure the micro agent to use the created module](tutorial-standalone-agent-binary-installation#authenticate-using-a-module-identity-connection-string) (note that the device does not have to exist yet).
7. Navigate back to DPS and [provision the device through DPS](/en-us/azure/iot-dps/quick-create-simulated-device-x509).
8. Navigate to the configured device in the destination IoT Hub.
9. Create a new module for the device issued by the same CA certificate used for the DPS enrollment.
10. Run the micro agent that you configured to use the created module to confirm it connects to the device.

Note

While you don't need the device to exist before configuring the agent when using this procedure, you do need to know the device name in advance in order to issue the certificate for the final module correctly.