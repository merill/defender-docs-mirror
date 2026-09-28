---
layout: Conceptual
title: Get started with OT monitoring - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/getting-started
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
description: Learn how to set up an OT plan with Microsoft Defender for IoT and configure your network sensors.
ms.topic: get-started
ms.date: 2026-05-31T00:00:00.0000000Z
locale: en-us
document_id: c8b51c7a-dbe0-5ab2-d489-4d4de13ef5bc
document_version_independent_id: 27b832c9-ee2e-d1eb-d57d-e5f41ede09c6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/getting-started.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/getting-started
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/getting-started.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 461d3aae-a710-67c4-798e-354dcd80c2f0
---

# Get started with OT monitoring - Microsoft Defender for IoT | Microsoft Learn

This article describes how to set up an OT plan for Microsoft Defender for IoT. Use Defender for IoT to monitor network traffic across your OT networks.

## Prerequisites

Before you start, you need:

1. A Microsoft tenant, with Global or Billing admin access to the tenant.

    For more information, see [Buy or remove licenses for a Microsoft business subscription](/en-us/microsoft-365/commerce/licenses/buy-licenses) and [About admin roles in the Microsoft 365 admin center](/en-us/microsoft-365/admin/add-users/about-admin-roles).
2. An Azure subscription linked to your tenant.

For current licensing and onboarding options, see [Defender for IoT licenses overview](license-and-trial-license-extention).

## Purchase a Defender for IoT license

To purchase a Defender for IoT license through the Microsoft 365 admin center:

1. Go to the [Microsoft 365 admin center](https://portal.office.com/AdminPortal/Home#/catalog)**Billing &gt; Purchase services**. If you don't have this option, select **Marketplace** instead.
2. Search for **Defender for IoT**.
3. Choose the license appropriate for the size of your site.
4. Complete the purchasing instructions.

For more information, see [purchase a Defender for IoT license](how-to-manage-subscriptions#purchase-a-defender-for-iot-license) and the [Microsoft 365 admin center help](/en-us/microsoft-365/admin/).

## Add an OT plan

This procedure describes how to add an OT plan for Defender for IoT in the Azure portal, based on your license.

**To add an OT plan in Defender for IoT**:

1. Open [Defender for IoT](https://portal.azure.com/#view/Microsoft_Azure_IoT_Defender/IoTDefenderDashboard/%7E/Getting_started) in the Azure portal, select **Plans and pricing**, where you're prompted to create a new subscription.

    [![Screenshot of the Go to subscriptions message for creating a Defender for IoT subscription.](media/getting-started/subscriptions.png)](media/getting-started/subscriptions.png#lightbox)
2. Select **Go to subscriptions** to create a new subscription on the [Azure **Subscriptions** page](https://portal.azure.com/?quickstart=True#view/Microsoft_Azure_Billing/SubscriptionsBlade).
3. Back in the Defender for IoT's **Plans and pricing** page, select **Add plan**. In the **Plan settings** pane, select your new subscription.

    The **Price plan** value is updated automatically to read **Microsoft 365**, reflecting your Microsoft 365 license.

    [![Screenshot of the Plan settings pane for completing the set up of a license and site for Defender for IoT in the Azure portal.](media/getting-started/plan-set-up.png)](media/getting-started/plan-set-up.png#lightbox)
4. Select **Next** and review the details for your licensed site.
5. Select the terms and conditions, and then select **Save**.

Your new plan is listed under the relevant subscription on the **Plans and pricing** &gt; **Plans** page. For more information, see [Manage your subscriptions](how-to-manage-subscriptions).

## Onboard an OT sensor

If you already have a network plan ready, you can onboard the OT sensor and associate it with a plan and the assign the relevant site and zone settings. For more information, see [onboard an OT sensor to the Azure portal](onboard-sensors).