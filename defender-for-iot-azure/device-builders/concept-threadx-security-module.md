---
layout: Conceptual
title: Conceptual explanation of the basics of the Defender-IoT-micro-agent for Eclipse ThreadX - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/concept-threadx-security-module
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
description: Learn the basics about the Defender-IoT-micro-agent for Eclipse ThreadX concepts and workflow.
ms.topic: concept-article
ms.date: 2024-04-17T00:00:00.0000000Z
locale: en-us
document_id: bf114867-3eb7-e6c0-ad24-baa55854c84c
document_version_independent_id: a0d8b0ab-0f0d-242e-90b7-a2491bc0f311
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/concept-threadx-security-module.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/concept-threadx-security-module
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/concept-threadx-security-module.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/45f51b57-72c2-4c0b-ab6c-cde4f0bed5d8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/0888e80f-d6a8-407d-b2ed-e325482a4715
platformId: 4a653c08-2357-2d48-b556-fa93650f2289
---

# Conceptual explanation of the basics of the Defender-IoT-micro-agent for Eclipse ThreadX - Microsoft Defender for IoT | Microsoft Learn

Use this article to get a better understanding of the Defender-IoT-micro-agent for Eclipse ThreadX, including features and benefits as well as links to relevant configuration and reference resources.

Note

Defender for IoT plans to retire the micro agent on June 1, 2027.

## Eclipse ThreadX IoT Defender-IoT-micro-agent

Defender-IoT-micro-agent for Eclipse ThreadX provides a comprehensive security solution for Eclipse ThreadX devices as part of the NetX Duo offering. Within the NetX Duo offering, Eclipse ThreadX ships with the Azure IoT Defender-IoT-micro-agent built-in, and provides coverage for common threats on your real-time operating system devices once activated.

The Defender-IoT-micro-agent for Eclipse ThreadX runs in the background, and provides a seamless user experience, while sending security messages using each customer's unique connections to their IoT Hub. The Defender-IoT-micro-agent for Eclipse ThreadX is enabled by default.

## Eclipse ThreadX NetX Duo

Eclipse ThreadX NetX Duo is an advanced, industrial-grade TCP/IP network stack designed specifically for deeply embedded real-time and IoT applications. Eclipse ThreadX NetX Duo is a dual IPv4 and IPv6 network stack providing a rich set of protocols, including security and cloud. Learn more about [Eclipse ThreadX NetX Duo](https://github.com/eclipse-threadx) solutions.

The module offers the following features:

- **Detect malicious network activities**
- **Device behavior baselines based on custom alerts**
- **Improve device security hygiene**

## Defender-IoT-micro-agent for Eclipse ThreadX architecture

The Defender-IoT-micro-agent for Eclipse ThreadX is initialized by the Azure IoT middleware platform and uses IoT Hub clients to send security telemetry to the Hub.

![Micro agent state diagram and information flow.](media/concept-threadx-security-module/security-module-state-diagram.png)

The Defender-IoT-micro-agent for Eclipse ThreadX monitors the following device activity and information using three collectors:

- Device network activity **TCP**, **UDP**, and **ICM**
- System information as **Threadx** and **NetX Duo** versions
- Heartbeat events

Each collector is linked to a priority group and each priority group has its own interval with possible values of **Low**, **Medium**, and **High**. The intervals affect the time interval in which the data is collected and sent.

Each time interval is configurable and the IoT connectors can be enabled and disabled in order to further [customize your solution](how-to-threadx-security-module).

## Supported security alerts and recommendations

The Defender-IoT-micro-agent for Eclipse ThreadX supports specific security alerts and recommendations. Make sure to [review and customize the relevant alert and recommendation values](concept-threadx-security-alerts-recommendations) for your service after completing the initial configuration.

## Ready to begin?

Defender-IoT-micro-agent for Eclipse ThreadX is provided as a free download for your IoT devices. The Defender for IoT cloud service is available with a 30-day trial per Azure subscription. [Download the Defender-IoT-micro-agent now](https://github.com/eclipse-threadx) and let's get started.