---
layout: Conceptual
title: Microsoft Defender for IoT billing - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/billing
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
description: Learn how you're billed for the Microsoft Defender for IoT service.
ms.topic: concept-article
ms.date: 2025-11-05T00:00:00.0000000Z
ms.custom: enterprise-iot
locale: en-us
document_id: 6c8da745-e678-0248-ba65-6355e95fc783
document_version_independent_id: fb427162-f847-6d3e-4dab-ac62ddbafe01
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/billing.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/billing
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/billing.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: c58c2470-04f8-82e8-d7ef-19ba5c46ddf8
---

# Microsoft Defender for IoT billing - Microsoft Defender for IoT | Microsoft Learn

Note

This article is relevant for commercial Defender for IoT customers. If you're a government customer, contact your Microsoft sales representative for more information.

As you plan your Microsoft Defender for IoT deployment, you typically want to understand the Defender for IoT pricing plans and billing models so you can optimize your costs.

**OT monitoring** is billed using site-based licenses, where each license applies to an individual site, based on the site size. A site is a physical location, such as a facility, campus, office building, hospital, rig, and so on. Each site can contain any number of network sensors, all of which monitor devices detected in connected networks.

**Enterprise IoT monitoring** supports 5 devices per Microsoft 365 E5 (ME5) or E5 Security license, or is available as standalone, per-device licenses for Microsoft Defender for Endpoint P2 customers.

## Enterprise IoT free trial

To evaluate Defender for IoT for Enterprise IoT networks, use a trial, standalone license as an add-on to Microsoft Defender for Endpoint. Trial licenses support 100 devices. For more information, see [Securing IoT devices in the enterprise](concept-enterprise) and [Enable Enterprise IoT security with Defender for Endpoint](eiot-defender-for-endpoint).

For current OT licensing and onboarding options, see [Defender for IoT licenses overview](license-and-trial-license-extention).

## Defender for IoT devices

We recommend that you have a sense of how many devices you want to monitor so that you know how many OT sites you need to license, or if you need any standalone licenses for enterprise IoT security.

- **OT monitoring**: Purchase a license for each site that you're planning to monitor. License fees differ based on the site size, each which covers a different number of devices.

    Note

    When the license for one or more of your sites is about to expire, a note is visible at the top of Defender for IoT in the Azure portal, reminding you to renew your licenses. To continue to get security value from Defender for IoT, select the link in the note to renew the relevant licenses in the Microsoft 365 admin center.
- **Enterprise IoT monitoring**: Five devices are supported for each ME5/E5 Security user license. If you have more devices to monitor, and are a Defender for Endpoint P2 customer, purchase extra, standalone licenses for each device you want to monitor.

Defender for IoT can discover all devices, of all types, across all environments. Devices are listed in the Defender for IoT **Device inventory** pages based on a unique IP and MAC address coupling.

Defender for IoT identifies single and unique devices as follows:

| Type | Description |
| --- | --- |
| **Identified as individual devices** | Devices identified as *individual* devices include:**IT, OT, or IoT devices with one or more NICs**, including network infrastructure devices such as switches and routers**Note**: A device with modules or backplane components, such as racks or slots, is counted as a single device, including all modules or backplane components. |
| **Not identified as individual devices** | The following items *aren't* considered as individual devices, and do not count against your license:- **Public internet IP addresses**- **Multi-cast groups**- **Broadcast groups**- **Inactive devices** Network-monitored devices are marked as *inactive* when there's no network activity detected within a specified time: In **OT networks**, no network activity is detected for more than 60 days.**Note**: Endpoints already managed by Defender for Endpoint are not considered as separate devices by Defender for IoT. |