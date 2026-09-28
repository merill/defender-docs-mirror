---
layout: Conceptual
title: Configure active monitoring for OT networks - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/configure-active-monitoring
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
description: Describes the available methods for configuring active monitoring on your OT network with Microsoft Defender for IoT.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 6eddb3fd-d8c8-ca3b-8375-b80853f17004
document_version_independent_id: 435d9891-475e-c756-ac15-0143e6bf418f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/configure-active-monitoring.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/configure-active-monitoring
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/configure-active-monitoring.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 8271d6ae-fd2a-85cd-65d4-271ab28bed0f
---

# Configure active monitoring for OT networks - Microsoft Defender for IoT | Microsoft Learn

This article describes how to configure active monitoring on OT networks with Microsoft Defender for IoT, including methods for Windows Event monitoring and reverse DNS lookup.

## Plan your active monitoring

Important

Active monitoring runs detection activity directly in your network and may cause some downtime. Take care when configuring active monitoring so that you only scan necessary resources.

When planning active monitoring:

- **Verify the following questions**:

    - Can the devices you want to scan be discovered by the default Defender for IoT monitoring? If so, active monitoring may be unnecessary.
    - Are you able to run active queries on your network and on the devices you want to scan? To make sure, try running an active query on a staging environment.

    Use the answers to these questions to determine exactly which sites and address ranges you want to monitor.
- **Identify maintenance windows** where you can schedule active monitoring intervals safely.
- **Identify active monitoring owners**, which are personnel who can supervise the active monitoring activity and stop the monitoring process if needed.
- **Determine which active monitoring method to use**:

    - Use [Windows Endpoint Monitoring](configure-windows-endpoint-monitoring) to monitor WMI events
    - Use [DNS lookup](configure-reverse-dns-lookup) for device data enrichment

## Configure network access

Before you configure active monitoring, you must also set up your network to allow the sensor's management port IP address to reach the OT network where your devices are.

For example, the following image highlights in grey the extra network access you must configure from the management interface to the OT network.

![Diagram highlighting the extra management network configuration required for active monitoring.](media/configure-active-monitoring/architecture.png)