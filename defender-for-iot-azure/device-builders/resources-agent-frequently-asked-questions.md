---
layout: Conceptual
title: Microsoft Defender for IoT for device builders frequently asked questions - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/resources-agent-frequently-asked-questions
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
description: Find answers to the most frequently asked questions about Microsoft Defender for IoT agent.
ms.topic: faq
ms.date: 2023-01-01T00:00:00.0000000Z
locale: en-us
document_id: 008ea26b-1774-eec6-14e8-e41e2491bff0
document_version_independent_id: f3d7f649-e0b6-1d21-8f0a-0d2fb2e9f88f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/resources-agent-frequently-asked-questions.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/resources-agent-frequently-asked-questions
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/resources-agent-frequently-asked-questions.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: a47bc0cc-5409-7d61-fabe-37c0d201fcce
---

# Microsoft Defender for IoT for device builders frequently asked questions - Microsoft Defender for IoT | Microsoft Learn

This article provides a list of frequently asked questions and answers about the Defender for IoT agent.

## Do I have to install an embedded security agent?

Agent installation on your IoT devices isn't mandatory in order to enable Defender for IoT. You can choose between the following two options There are four different levels of security monitoring, and management capabilities, which will provide different levels of protection:

- Install the Defender for IoT embedded security agent with or without modifications. This option provides the highest level of enhanced security insights into device behavior and access.
- No security agent installation on your IoT devices. This option enables IoT Hub communication monitoring, with reduced security monitoring, and management capabilities.

## What does the Defender for IoT agent do?

Defender for IoT agent provides device level threat coverage for device configuration, behavior, and access (by scanning the configuration), process & connectivity. The Defender for IoT security agent does not scan business-related data or activity.

The Defender for IoT security agent is open source and available on GitHub in 32 bit and 64-bit Windows and Linux versions: https://github.com/Azure/Azure-IoT-Security.

## What are the dependencies and prerequisites of the agent?

Defender for IoT supports a wide variety of platforms. See [Supported Device platforms](how-to-deploy-agent) to verify support for your specific devices.

## Which data is collected by the agent?

Connectivity, access, firewall configuration, process list & OS baseline are collected by the agent.

## How much data will the agent generate?

Agent data generation is driven by device, application, connectivity type, and customer agent configuration. Due to the high variability between devices and IoT solutions, we recommend first deploying the agent in a lab or test setting to observe, learn, and set the specific configuration that fits your needs, while measuring the amount of generated data. After starting the service, the Defender for IoT agent provides operational recommendations for optimizing agent throughput to help you with the configuration and customization process.

## Do agent messages use up quota from IoT Hub?

Yes. Agent transmitted data is counted in your IoT Hub quota.

## What next? I've installed an agent and don't see any activities or logs...

1. Check the [agent type fits the designated OS platform of your device](how-to-deploy-agent)
2. Confirm the [agent is running on the device](how-to-agent-configuration).
3. Check the [service was enabled successfully](quickstart-onboard-iot-hub) to **Security** in your IoT Hub.
4. Check that the device is [configured in IoT Hub with the Defender for IoT module](quickstart-create-security-twin).

If the activities or logs are still unavailable, contact your Defender for IoT partner for additional help.

## What happens when the internet connection stops working?

The sensors and agents continue to run and store data as long as the device is running. Data is stored in the security message cache according to size configuration. When the device regains connectivity, security messages resume sending.

## Can the agent affect the performance of the device or other installed software?

The agent consumes machine resources as any other application/process and should not disrupt normal device activity. Resource consumption on the device the agent runs on is coupled with its setup and configuration. We recommend testing your agent configuration in a contained environment, along with interoperability with your other IoT applications and functionality, before attempting to deploy in a production environment.

## I'm making some maintenance on the device. Can I turn off the agent?

The agent cannot be turned off.

## Is there a way to test if the agent is working correctly?

If the agent stops communicating or fails to send security messages, a **Device is silent** alert is generated.

## Can I create my own alerts?

Yes, you can create custom alerts based on multiple parameters including IP/MAC address, protocol type, class, service, function, command, and so on, as well as values of custom tags contained in the payloads. See [Create custom alerts](quickstart-create-custom-alerts) to learn more about custom alerts and how to create them.