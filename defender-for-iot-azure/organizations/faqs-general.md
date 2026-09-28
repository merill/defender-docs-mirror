---
layout: Conceptual
title: General FAQs - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/faqs-general
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
description: Find answers to the most frequently asked questions about Microsoft Defender for IoT features and service.
ms.topic: faq
ms.date: 2022-07-07T00:00:00.0000000Z
locale: en-us
document_id: 7374753c-3118-91c6-6403-0279a9c9cdcc
document_version_independent_id: c9a06e13-f609-237f-707b-621516d4eab4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/faqs-general.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/faqs-general
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/faqs-general.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 2fb840c7-8a93-14e6-f524-d537b57ff747
---

# General FAQs - Microsoft Defender for IoT | Microsoft Learn

This article provides a list of frequently asked questions and answers about Defender for IoT.

## What is Azure's unique value proposition for IoT security?

Defender for IoT enables enterprises to extend their existing cyber security view to their entire IoT solution. Azure provides an end to end view of your business solution, enabling you to take business-related actions and decisions based on your enterprise security posture and collected data. Combined security using Azure IoT, Azure IoT Edge, and Microsoft Defender for Cloud enable you to create the solution you want with the security you need.

## How does Defender for IoT compare to the competition?

Microsoft Defender for IoT delivers comprehensive security across all your IoT/OT devices. For **end-user organizations**, Microsoft Defender for IoT offers agentless, network-layer security that is rapidly deployed, works with diverse proprietary OT equipment and legacy Windows systems, and interoperates with Microsoft Sentinel and other SOC tools. It can be deployed on-premises or in Azure-connected environments. For **IoT device builders**, Microsoft Defender for IoT offers lightweight agents to embed device-layer security into new IoT/OT initiatives.

## Do I have to be an Azure customer?

You must be an Azure customer to use Microsoft Defender for IoT. However, OT sensors installed for air-gapped networks can be managed locally, and don't need to connect to the cloud.

For more information, see [Defender for IoT subscription billing](billing).

## What happens when the internet connection stops working?

The sensors and agents continue to run and store data as long as the device is running. Data is stored in the security message cache according to size configuration. When the device regains connectivity, security messages resume sending.