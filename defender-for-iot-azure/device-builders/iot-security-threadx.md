---
layout: Conceptual
title: Defender-IoT-micro-agent for Eclipse ThreadX overview - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/iot-security-threadx
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
description: Learn more about the Defender-IoT-micro-agent for Eclipse ThreadX support and implementation as part of Microsoft Defender for IoT.
ms.topic: overview
ms.date: 2024-04-17T00:00:00.0000000Z
locale: en-us
document_id: 72399ad6-a102-fbf6-30a5-fc18d2d22708
document_version_independent_id: fa65bcb0-dd8a-5dfe-008b-06c64f1c30f1
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/iot-security-threadx.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/iot-security-threadx
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/iot-security-threadx.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/45f51b57-72c2-4c0b-ab6c-cde4f0bed5d8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/0888e80f-d6a8-407d-b2ed-e325482a4715
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 6c412991-e7a9-b098-0dd5-90fe0343f21a
---

# Defender-IoT-micro-agent for Eclipse ThreadX overview - Microsoft Defender for IoT | Microsoft Learn

The Microsoft Defender for IoT micro module provides a comprehensive security solution for devices that use Eclipse ThreadX. It provides coverage for common threats and potential malicious activities on real-time operating system (FileX) devices. Eclipse ThreadX now ships with the Azure IoT Defender-IoT-micro-agent built in.

![Diagram of the visualization of Defender for IoT Eclipse ThreadX.](media/iot-security-threadx/threadx-security-monitoring.png)

The micro module for Eclipse ThreadX offers the following features:

- Malicious network activity detection
- Custom alert-based device behavior baselining
- Improved device security hygiene

## Detect malicious network activities

Inbound and outbound network activity of each device is monitored. Supported protocols are TCP, UDP, and ICMP on IPv4 and IPv6. Defender for IoT inspects each of these network activities against the Microsoft threat intelligence feed. The feed gets updated in real time with millions of unique threat indicators collected worldwide.

## Device behavior baselining based on custom alerts

Baselining allows for clustering of devices into security groups and defining the expected behavior of each group. Because IoT devices are typically designed to operate in well-defined and limited scenarios, it's easy to create a baseline that defines their expected behavior by using a set of parameters. Any deviation from the baseline triggers an alert.

## Improve your device security hygiene

By using the recommended infrastructure Defender for IoT provides, you can gain knowledge and insights about issues in your environment that affect and damage the security posture of your devices. A weak IoT-device security posture can allow potential attacks to succeed if it's left unchanged. Security is always measured by the weakest link within any organization.

## Get started protecting Eclipse ThreadX devices

Defender-IoT-micro-agent for Eclipse ThreadX is provided as a free download for your devices. The Defender for IoT cloud service is available with a 30-day trial per Azure subscription. To get started, download the [Defender-IoT-micro-agent for Eclipse ThreadX](https://github.com/eclipse-threadx).