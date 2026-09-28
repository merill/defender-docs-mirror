---
layout: Conceptual
title: Integrate ArcSight with Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/integrations/arcsight
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
description: Learn how to send Microsoft Defender for IoT alerts to ArcSight.
ms.topic: integration
ms.date: 2022-08-02T00:00:00.0000000Z
locale: en-us
document_id: 6de8ab8c-6d37-c64e-8b0c-bccf67196cd7
document_version_independent_id: bfd64b3d-5199-9a18-131b-a8d76f5edee9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/integrations/arcsight.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/integrations/arcsight
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/integrations/arcsight.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 097eff85-b51d-0b03-507e-28c5d7eddfdc
---

# Integrate ArcSight with Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn

This article describes how to send Microsoft Defender for IoT alerts to ArcSight. Integrating Defender for IoT with ArcSight provides visibility into the security and resiliency of OT networks and a unified approach to IT and OT security.

Note

Defender for IoT plans to retire the ArcSight integration on December 1, 2025

## Prerequisites

Before you begin, make sure that you have the following prerequisites:

- Access to a Defender for IoT OT sensor as an Admin user. For more information, see [On-premises users and roles for OT monitoring with Defender for IoT](../roles-on-premises).

## Configure the ArcSight receiver type

To configure your ArcSight server settings so that it can receive Defender for IoT alert information:

1. Sign in to your ArcSight server.
2. Configure your receiver type as a **CEF UDP Receiver**.

For more information, see the [ArcSight SmartConnectors Documentation](https://www.microfocus.com/documentation/arcsight/arcsight-smartconnectors-8.4/#gsc.tab=0).

## Create a Defender for IoT forwarding rule

This procedure describes how to create a forwarding rule from your OT sensor to send Defender for IoT alerts from that sensor to ArcSight.

Forwarding alert rules run only on alerts triggered after the forwarding rule is created. Alerts already in the system from before the forwarding rule was created aren't affected by the rule.

For more information, see [Forward alert information](../how-to-forward-alert-information-to-partners).

1. Sign in to your OT sensor console and select **Forwarding**.
2. Select **+ Create new rule**.
3. In the **Add forwarding rule** pane, define the rule parameters:

    [![Screenshot of creating a new forwarding rule.](../media/integrate-arcsight/create-new-forwarding-rule.png)](../media/integrate-arcsight/create-new-forwarding-rule.png#lightbox)

    | Parameter | Description |
    | --- | --- |
    | **Rule name** | Enter a meaningful name for your rule. |
    | **Minimal alert level** | The minimal security level incident to forward. For example, if you select Minor, you're notified about all minor, major and critical incidents. |
    | **Any protocol detected** | Toggle off to select the protocols you want to include in the rule. |
    | **Traffic detected by any engine** | Toggle off to select the traffic you want to include in the rule. |
4. In the **Actions** area, define the following values:

    | Parameter | Description |
    | --- | --- |
    | **Server** | Select **ArcSight**. |
    | **Host** | The ArcSight server address. |
    | **Port** | The ArcSight server port. |
    | **Timezone** | Enter the timezone of the ArcSight server. |
5. Select **Save** to save your forwarding rule.