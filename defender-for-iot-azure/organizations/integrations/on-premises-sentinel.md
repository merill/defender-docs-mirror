---
layout: Conceptual
title: Connect Defender for IoT On-premises Resources to Microsoft Sentinel (Legacy) - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/integrations/on-premises-sentinel
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
description: This article describes the legacy method for connecting your OT sensor to Microsoft Sentinel.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: template-how-to-pattern, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: deb7e98b-8c04-1269-3783-3a6727c4b782
document_version_independent_id: c0c2f376-14b1-3466-bde7-034a9d90c48e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/integrations/on-premises-sentinel.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/integrations/on-premises-sentinel
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/integrations/on-premises-sentinel.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: aba0e2b6-ba4c-7030-3653-b93fb6fc294f
---

# Connect Defender for IoT On-premises Resources to Microsoft Sentinel (Legacy) - Microsoft Defender for IoT | Microsoft Learn

This article describes the legacy method for connecting your OT sensor to Microsoft Sentinel. Before you begin, review the prerequisites. Stream data into Microsoft Sentinel whenever you want to use Microsoft Sentinel's advanced threat hunting, security analytics, and automation features when responding to security incidents and threats across your network.

Important

The legacy OT sensor integration with Microsoft Sentinel will be deprecated in **January 2025**.

If you're using a cloud connected sensor, we recommend that you connect Defender for IoT data using the Microsoft Sentinel solution instead of the legacy OT sensor to Microsoft Sentinel connection method described in this article. For more information, see:

- [OT threat monitoring in enterprise SOCs](../concept-sentinel-integration)
- [Tutorial: Connect Microsoft Defender for IoT with Microsoft Sentinel](../iot-solution)
- [Tutorial: Investigate and detect threats for IoT devices](../iot-advanced-threat-monitoring)

## Prerequisites

Before you start, make sure that you have the following prerequisites as needed:

- Access to the OT network sensor as an **Admin** user. For more information, see [On-premises users and roles for OT monitoring with Defender for IoT](../roles-on-premises).
- A proxy machine prepared to send data to Microsoft Sentinel. For more information, see [Get CEF-formatted logs from your device or appliance into Microsoft Sentinel](/en-us/azure/sentinel/connect-common-event-format).
- If you want to encrypt the data you send to Microsoft Sentinel using TLS, make sure to generate a valid TLS certificate from the proxy server to use when you create the OT sensor forwarding alert rule.

## Set up forwarding alert rules

1. Sign into your OT network sensor and create a forwarding rule. For more information, see [Forward on-premises OT alert information](../how-to-forward-alert-information-to-partners).
2. When creating your forwarding rule, make sure to select **Microsoft Sentinel** as the **Server** value. For example, on the OT sensor:

    [![Screenshot of the Microsoft Sentinel option from the OT sensor.](../media/integration-on-premises-sentinel/sensor-sentinel.png)](../media/integration-on-premises-sentinel/sensor-sentinel.png#lightbox)
3. If you're using TLS encryption, make sure to select **Enable encryption** and upload your certificate and key files.

After you finish configuring the forwarding rule, select **Save**. Make sure to test the rule to make sure that it works as expected.

Important

To forward alert details to multiple Microsoft Sentinel instances, make sure to create a separate forwarding rule for each instance. Don't use the **Add server** option in the same forwarding rule to send data to multiple Microsoft Sentinel instances.