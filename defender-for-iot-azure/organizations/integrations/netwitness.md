---
layout: Conceptual
title: Integrate RSA NetWitness with Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/integrations/netwitness
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
description: Learn how to send Microsoft Defender for IoT alerts to RSA NetWitness.
ms.topic: integration
ms.date: 2022-08-02T00:00:00.0000000Z
locale: en-us
document_id: 09d3060b-c273-1c70-79ff-5870cf8010dd
document_version_independent_id: 5c096a89-67b2-1786-9096-3382ea236745
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/integrations/netwitness.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/integrations/netwitness
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/integrations/netwitness.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: ce27f5ed-ef35-a3d7-71b5-6b67cd28fd46
---

# Integrate RSA NetWitness with Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn

This article describes how to send Microsoft Defender for IoT alerts to RSA NetWitness. Integrating Defender for IoT with NetWitness provides visibility into the security and resiliency of OT networks and a unified approach to IT and OT security.

Note

Defender for IoT plans to retire the NetWitness integration on December 1, 2025

## Prerequisites

Before you begin, make sure that you have the following prerequisites:

- Access to a Defender for IoT OT sensor as an Admin user. For more information, see [On-premises users and roles for OT monitoring with Defender for IoT](../roles-on-premises).
- NetWitness configuration to collect events from sources that support Common Event Format (CEF). For more information, see the [CyberX Platform - RSA NetWitness CEF Parser Implementation Guide](https://community.netwitness.com//t5/netwitness-platform-integrations/cyberx-platform-rsa-netwitness-cef-parser-implementation-guide/ta-p/554364).

## Create a Defender for IoT forwarding rule

This procedure describes how to create a forwarding rule from your OT sensor to send Defender for IoT alerts from that sensor to NetWitness.

Forwarding alert rules run only on alerts triggered after the forwarding rule is created. Alerts already in the system from before the forwarding rule was created aren't affected by the rule.

For more information, see [Forward alert information](../how-to-forward-alert-information-to-partners).

1. Sign in to your OT sensor console and select **Forwarding**.
2. Select **+ Create new rule**.
3. In the **Add forwarding rule** pane, define the rule parameters:

    [![Screenshot of creating a new forwarding rule.](../media/integrate-netwitness/create-new-forwarding-rule.png)](../media/integrate-netwitness/create-new-forwarding-rule.png#lightbox)

    | Parameter | Description |
    | --- | --- |
    | **Rule name** | Enter a meaningful name for your rule. |
    | **Minimal alert level** | The minimal security level incident to forward. For example, if you select Minor, you're notified about all minor, major and critical incidents. |
    | **Any protocol detected** | Toggle off to select the protocols you want to include in the rule. |
    | **Traffic detected by any engine** | Toggle off to select the traffic you want to include in the rule. |
4. In the **Actions** area, define the following values:

    | Parameter | Description |
    | --- | --- |
    | **Server** | Select **NetWitness**. |
    | **Host** | The NetWitness hostname. |
    | **Port** | The NetWitness port. |
    | **Timezone** | Enter your NetWitness timezone. |
5. Select **Save** to save your forwarding rule.