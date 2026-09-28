---
layout: Conceptual
title: Custom security alerts for IoT Hub - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/concept-customizable-security-alerts
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
description: Learn about customizable security alerts and recommended remediation using Defender for IoT Hub's features and service.
ms.topic: reference
ms.date: 2023-01-01T00:00:00.0000000Z
locale: en-us
document_id: 4e166dd3-75cc-4a59-2cf1-a203bf1b382a
document_version_independent_id: 0e23c7ff-9c7c-eb1c-403c-f711fb0e4232
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/concept-customizable-security-alerts.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/concept-customizable-security-alerts
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/concept-customizable-security-alerts.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/816835a3-1c5d-4536-835c-4b59dc9c9d97
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/a98c4e96-5248-4755-860b-6c76f1933f0c
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 9929c51f-37e0-15a4-bacb-e81726ed0802
---

# Custom security alerts for IoT Hub - Microsoft Defender for IoT | Microsoft Learn

Defender for IoT continuously analyzes your IoT solution using advanced analytics and threat intelligence to alert you to malicious activity.

Create custom alerts based on your knowledge of each expected device's behavior. These alerts act as the most efficient indicators of any potential changes to your organizational deployment, or landscape.

The following lists of Defender for IoT alerts are definable by you based on your expected IoT Hub behavior. For more information about how to customize each alert, see [create custom alerts](quickstart-create-custom-alerts).

## Built-in custom alerts in the IoT Hub

### Low severity

| Alert name | Severity | Data source | Description | Alert Type |
| --- | --- | --- | --- | --- |
| Custom alert - The number of cloud to device messages in AMQP protocol is outside the allowed range | Low | IoT Hub | The number of cloud to device messages (AMQP protocol) within a specific time window is outside the currently configured and allowable range. | IoT\_CA\_AmqpC2DMessagesNotInAllowedRange |
| Custom alert - The number of rejected cloud to device messages in AMQP protocol is outside the allowed range | Low | IoT Hub | The number of cloud to device messages (AMQP protocol) rejected by the device, within a specific time window is outside the currently configured and allowable range. | IoT\_CA\_AmqpC2DRejectedMessagesNotInAllowedRange |
| Custom alert - The number of device to cloud messages in AMQP protocol is outside the allowed range | Low | IoT Hub | The amount of device to cloud messages (AMQP protocol) within a specific time window is outside the currently configured and allowable range. | IoT\_CA\_AmqpD2CMessagesNotInAllowedRange |
| Custom alert - The number of direct method invokes are outside the allowed range | Low | IoT Hub | The amount of direct method invokes within a specific time window is outside the currently configured and allowable range. | IoT\_CA\_DirectMethodInvokesNotInAllowedRange |
| Custom alert - The number of file uploads is outside the allowed range | Low | IoT Hub | The amount of file uploads within a specific time window is outside the currently configured and allowable range. | IoT\_CA\_FileUploadsNotInAllowedRange |
| Custom alert - The number of cloud to device messages in HTTP protocol is outside the allowed range | Low | IoT Hub | The amount of cloud to device messages (HTTP protocol) in a time window isn't in the configured allowed range | IoT\_CA\_HttpC2DMessagesNotInAllowedRange |
| Custom alert - The number of rejected cloud to device messages in HTTP protocol isn't in the allowed range | Low | IoT Hub | The amount of cloud to device messages (HTTP protocol) within a specific time window is outside the currently configured and allowable range. | IoT\_CA\_HttpC2DRejectedMessagesNotInAllowedRange |
| Custom alert - The number of device to cloud messages in HTTP protocol is outside the allowed range | Low | IoT Hub | The amount of device to cloud messages (HTTP protocol) within a specific time window is outside the currently configured and allowable range. | IoT\_CA\_HttpD2CMessagesNotInAllowedRange |
| Custom alert - The number of cloud to device messages in MQTT protocol is outside the allowed range | Low | IoT Hub | The amount of cloud to device messages (MQTT protocol) within a specific time window is outside the currently configured and allowable range. | IoT\_CA\_MqttC2DMessagesNotInAllowedRange |
| Custom alert - The number of rejected cloud to device messages in MQTT protocol is outside the allowed range | Low | IoT Hub | The amount of cloud to device messages (MQTT protocol) rejected by the device within a specific time window is outside the currently configured and allowable range. | IoT\_CA\_MqttC2DRejectedMessagesNotInAllowedRange |
| Custom alert - The number of device to cloud messages in MQTT protocol is outside the allowed range | Low | IoT Hub | The amount of device to cloud messages (MQTT protocol) within a specific time window is outside the currently configured and allowable range. | IoT\_CA\_MqttD2CMessagesNotInAllowedRange |
| Custom alert - The number of command queue purges that are outside of the allowed range | Low | IoT Hub | The amount of command queue purges within a specific time window is outside the currently configured and allowable range. | IoT\_CA\_QueuePurgesNotInAllowedRange |
| Custom alert - The number of module twin updates is outside the allowed range | Low | IoT Hub | The number of module twin updates within a specific time window is outside the currently configured and allowable range. | IoT\_CA\_TwinUpdatesNotInAllowedRange |
| Custom alert - The number of unauthorized operations is outside the allowed range | Low | IoT Hub | The number of unauthorized operations within a specific time window is outside the currently configured and allowable range. | IoT\_CA\_UnauthorizedOperationsNotInAllowedRange |