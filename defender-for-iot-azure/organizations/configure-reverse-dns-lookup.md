---
layout: Conceptual
title: Configure reverse DNS lookup for OT active monitoring - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/configure-reverse-dns-lookup
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
description: This article describes how to configure reverse DNS lookup for active monitoring with Microsoft Defender for IoT.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: c926e351-91d4-fcf9-1b78-95c4c7d279ab
document_version_independent_id: 16c85111-a917-9ebe-85b0-7e8ebcf2eaa5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/configure-reverse-dns-lookup.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/configure-reverse-dns-lookup
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/configure-reverse-dns-lookup.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 819008a5-eb1c-c77a-47dc-d4d98bcbbd74
---

# Configure reverse DNS lookup for OT active monitoring - Microsoft Defender for IoT | Microsoft Learn

This procedure describes how to enhance device data enrichment in Microsoft Defender for IoT by configuring multiple DNS servers to carryout reverse lookups.

Use reverse DNS lookup to resolve host names or FQDNs associated with the IP addresses detected in network subnets. For example, if a sensor discovers an IP address, it might query multiple DNS servers to resolve the host name. Host names appear in the Defender for IoT device inventory, device map, and reports.

All CIDR formats are supported.

## Prerequisites

Before configuring reverse DNS lookup, make sure you have:

- An OT network sensor with [OT sensor software installed](ot-deploy/install-software-ot-sensor) and [configured and activated your OT sensor](ot-deploy/activate-deploy-sensor).
- Access to your OT network sensor as an **Admin** user. For more information, see [On-premises users and roles for OT monitoring with Defender for IoT](roles-on-premises).
- Completed the prerequisites outlined in [Configure active monitoring for OT networks](configure-active-monitoring), and confirmed that active monitoring is right for your network.

## Define DNS servers

1. On your OT sensor console, select **System settings** &gt; **Network monitoring** and under **Active Discovery**, select **Reverse DNS Lookup**.
2. Use the **Schedule Reverse Lookup** options to define your scan as in fixed intervals, per hour, or at a specific time.

    If you select **By specific times**, use a 24-hour clock, such as **14:30** for **2:30 PM**. Select the **+** button on the side to add additional, specific times that you want the lookup to run.
3. Select **Add DNS Server**, and then populate your fields as needed to define the following fields:

    - **DNS server address**, which is the DNS server IP address
    - **DNS server port**
    - **Number of labels**, which is the number of domain labels you want to display. To determine the **Number of labels** value, resolve the network IP address to device FQDNs. You can enter up to 30 characters in this field.
    - **Subnets**, which is the subnets that you want the DNS server to query
4. Toggle on the **Enabled** option at the top to start the reverse lookup query as scheduled, and then select **Save** to finish the configuration.

## Test the DNS configuration

Use a test device to verify that the reverse DNS lookup schedule, DNS server, and subnet settings are configured correctly.

1. On your sensor console, select **System settings** &gt; **Network monitoring** and under **Active Discovery**, select **Reverse DNS Lookup**.
2. Make sure that the **Enabled** toggle is selected.
3. Select **Test**.
4. In the **DNS reverse lookup test for server** dialog, enter an address in the **Lookup Address** and then select **Test**.