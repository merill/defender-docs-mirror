---
layout: Conceptual
title: Defender-IoT-micro-agent for Eclipse ThreadX built-in & customizable alerts and recommendations - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/concept-threadx-security-alerts-recommendations
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
description: Learn about security alerts and recommended remediation using the Azure IoT Defender-IoT-micro-agent - Eclipse ThreadX.
ms.topic: reference
ms.date: 2024-04-17T00:00:00.0000000Z
locale: en-us
document_id: cac653d5-2ce1-db32-6c63-11fe7f573d95
document_version_independent_id: 7ab6c5cd-64e3-a85d-5f86-3d5de758ea4d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/concept-threadx-security-alerts-recommendations.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/concept-threadx-security-alerts-recommendations
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/concept-threadx-security-alerts-recommendations.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/45f51b57-72c2-4c0b-ab6c-cde4f0bed5d8
- https://authoring-docs-microsoft.poolparty.biz/devrel/816835a3-1c5d-4536-835c-4b59dc9c9d97
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/0888e80f-d6a8-407d-b2ed-e325482a4715
- https://authoring-docs-microsoft.poolparty.biz/devrel/a98c4e96-5248-4755-860b-6c76f1933f0c
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: c2738ec7-389f-6330-21ae-d823d8bc3113
---

# Defender-IoT-micro-agent for Eclipse ThreadX built-in & customizable alerts and recommendations - Microsoft Defender for IoT | Microsoft Learn

Defender-IoT-micro-agent for Eclipse ThreadX continuously analyzes your IoT solution using advanced analytics and threat intelligence to alert you to potential malicious activity and suspicious system modifications. You can also create custom alerts based on your knowledge of expected device behavior and baselines.

A Defender-IoT-micro-agent for Eclipse ThreadX alert acts as an indicator of potential compromise, and should be investigated and remediated. A Defender-IoT-micro-agent for Eclipse ThreadX recommendation identifies weak security posture to be remediated and updated.

In this article, you find a list of built-in alerts and recommendations that are triggered based on the default ranges, and customizable with your own values, based on expected or baseline behavior.

For more information on how alert customization works in the Defender for IoT service, see [customizable alerts](concept-customizable-security-alerts). The specific alerts and recommendations available for customization when using the Defender-IoT-micro-agent for Eclipse ThreadX are detailed in the following tables.

Note

Defender for IoT plans to retire the micro agent on June 1, 2027.

## Defender-IoT-micro-agent for Eclipse ThreadX supported security alerts

### Device-related security alerts

| Device-related security alert activity | Alert name |
| --- | --- |
| IP address | Communication with a suspicious IP address detected |
| X.509 device certificate thumbprint | X.509 device certificate thumbprint mismatch |
| X.509 certificate | X.509 certificate expired |
| SAS Token | Expired SAS Token |
| SAS Token | Invalid SAS Token signature |

### IoT Hub-related security alerts

| IoT Hub security alert activity | Alert name |
| --- | --- |
| Add a certificate | Detected unsuccessful attempt to add a certificate to an IoT Hub |
| Addition or editing of a diagnostic setting | Detected an attempt to add or edit a diagnostic setting of an IoT Hub |
| Delete a certificate | Detected unsuccessful attempt to delete a certificate from an IoT Hub |
| Delete a diagnostic setting | Detected attempt to delete a diagnostic setting from an IoT Hub |
| Deleted certificate | Detected deletion of a certificate from an IoT Hub |
| New certificate | Detected addition of new certificate to an IoT Hub |

## Defender-IoT-micro-agent for Eclipse ThreadX supported customizable alerts

### Device related customizable alerts

| Device related activity | Alert name |
| --- | --- |
| Active connections | Number of active connections isn't in the allowed range |
| Cloud to device messages in **MQTT** protocol | Number of cloud to device messages in **MQTT** protocol isn't in the allowed range |
| Outbound connection | Outbound connection to an IP that isn't allowed |

### Hub related customizable alerts

| Hub related activity | Alert name |
| --- | --- |
| Command queue purges | Number of command queue purges outside the allowed range |
| Cloud to device messages in **MQTT** protocol | Number of Cloud to device messages in **MQTT** protocol outside the allowed range |
| Device to cloud messages in **MQTT** protocol | Number of device to cloud messages in **MQTT** protocol outside the allowed range |
| Direct method invokes | Number of direct method invokes outside the allowed range |
| Rejected cloud to device messages in **MQTT** protocol | Number of rejected cloud to device messages in **MQTT** protocol outside the allowed range |
| Updates to twin modules | Number of updates to twin modules outside the allowed range |
| Unauthorized operations | Number of unauthorized operations outside the allowed range |

## Defender-IoT-micro-agent for Eclipse ThreadX supported recommendations

### Device-related recommendations

| Device-related activity | Recommendation name |
| --- | --- |
| Authentication credentials | Identical authentication credentials used by multiple devices |

### Hub-related recommendations

| IoT Hub-related activity | Recommendation name |
| --- | --- |
| IP filter policy | The Default IP filter policy should be set to **deny** |
| IP filter rule | IP filter rule includes a large IP range |
| Diagnostics logs | Suggestion to enable diagnostics logs in IoT Hub |

### All Defender for IoT alerts and recommendations

For a complete list of all Defender for IoT service related alerts and recommendations, see IoT [security alerts](concept-security-alerts), IoT security [recommendations](concept-recommendations).