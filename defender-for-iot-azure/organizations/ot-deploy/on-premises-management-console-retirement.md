---
layout: Conceptual
title: On-premises management console retirement - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/ot-deploy/on-premises-management-console-retirement
breadcrumb_path: ../../breadcrumb/toc.json
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
description: This article describes the retirement of the on-premises management console from **January 1, 2025**.
ms.topic: retired
ms.date: 2024-12-17T00:00:00.0000000Z
locale: en-us
document_id: 2fd10ecb-63df-000a-5812-aa9e3513adaa
document_version_independent_id: 7f9febe0-0fc4-c09a-5589-a5ba5b83f85f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/ot-deploy/on-premises-management-console-retirement.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/ot-deploy/on-premises-management-console-retirement
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/ot-deploy/on-premises-management-console-retirement.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 1cf5e8a5-9b2a-9ee8-fcf9-a737037a5a12
---

# On-premises management console retirement - Microsoft Defender for IoT | Microsoft Learn

This article describes the retirement of the on-premises management console from **January 1, 2025**.

## Retirement details

The on-premises management console will be retired on **January 1, 2025** with the following updates/changes:

- Sensor versions released after **January 1, 2025** won't connect to the on-premises management console.
- For versions released prior to **January 1, 2025**:
    - You can still use the on-premises management console.
    - Defender for IoT no longer provides support service or maintains the on-premises management console.

        For a list of supported versions, see [OT monitoring software versions](../release-notes)

## Air-gapped sensor support

Air-gapped sensor support isn't affected by the on-premises management console retirement. We continue to support air-gapped deployments and assist with the [transition to the cloud](transition-on-premises-management-console-to-cloud). The sensors retain a full user interface so that they can be used in "lights out" scenarios and continue to analyze and secure the network in the event of an outage.

If your organization enforces a policy where sensors can't access the internet (air-gapped), you can continue to manage sensors using:

- [The sensor console UI](../how-to-investigate-sensor-detections-in-a-device-inventory) or the [CLI](../cli-ot-sensor) to directly manage individual sensors.
- [APIs](../references-work-with-defender-for-iot-apis) to send data to third-party management systems, such as a Security Information and Event Management (SIEM).