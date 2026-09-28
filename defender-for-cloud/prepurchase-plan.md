---
layout: Conceptual
title: Optimize Microsoft Defender for Cloud Costs with a Pre-purchase Plan - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/prepurchase-plan
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Save on Microsoft Defender for Cloud by prepurchasing one-year Defender Cloud Units (DCUs). Learn how prepaid units are applied during the purchase term.
ms.topic: how-to
ms.reviewer: liuyizhu
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 6d93d578-fdaa-dfef-6fa4-86f9e9329df5
document_version_independent_id: 093b9865-7e23-ffd4-0306-57140574b5af
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/prepurchase-plan.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/prepurchase-plan
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/prepurchase-plan.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: a4a38c64-83cf-d129-86d5-308d3946967f
---

# Optimize Microsoft Defender for Cloud Costs with a Pre-purchase Plan - Microsoft Defender for Cloud | Microsoft Learn

You can save on your Microsoft Defender for Cloud costs when you [pre-purchase Microsoft Defender for Cloud commit units (DCU) for one year](https://azure.microsoft.com/pricing/details/defender-for-cloud/#pricing). You can use the prepurchased DCUs at any time during the purchase term. Unlike virtual machines (VMs), the prepurchased units don't expire on an hourly basis. You can use them at any time during the term of the purchase.

Any eligible Microsoft Defender for Cloud usage deducts from the prepurchased DCUs automatically. You don't need to redeploy or assign a pre-purchased plan to your Microsoft Defender for Cloud workspaces for the DCU usage to get the prepurchase discounts.

This article explains how to determine the right amount of commit units to buy, how to purchase a pre-purchase plan, and how discounts are applied to eligible usage.

## Determine the right size to buy

A Defender for Cloud prepurchase applies to all Defender for Cloud plans. A prepurchase is a pool of prepaid Defender for Cloud commit units. Usage is deducted from the pool, regardless of the workload.

There's no ratio on which the DCUs are applied. DCUs are equivalent to the purchase currency value and are deducted at retail prices. Like other reservations, the benefit of a prepurchase plan is discounted pricing by committing to a purchase term. The more you buy, the larger the discount you receive.

For example, if you purchase 5,000 Commit Units for a one-year term, you get a 10% discount on Defender for Cloud products at this tier, so you pay only 4,500 USD. You can choose to use these units with Microsoft Defender for Servers P2, and Defender Cloud Security Posture Management plans on 20 virtual machines (Azure VMs) for one year, which uses up 4800 Commit units.

As another example, an enterprise customer has an Annual Commitment Discount (ACD) of 10%. This customer typically consumes 120,000 USD worth of Microsoft Defender for Cloud at retail prices annually. With the ACD applied, their actual usage cost is 108,000 USD.

This year, the customer decided to purchase 100,000 Defender Credit Units (DCUs) for 82,000 USD, which includes an 18% discount off the retail prices. This discount isn't combined with the ACD, effectively making the actual discount rate 8%.

As DCUs are consumed at retail prices, the customer would still need to use 20,000 USD worth of Defender for Cloud at the pay-as-you-go rates, applying the ACD discount.

At the end of the commitment period, the actual Defender for Cloud usage cost for the customer would be 82,000 USD for the DCUs, reflecting the price with the 18% discount, plus 18,000 USD for the pay-as-you-go consumption, reflecting the 10% ACD discount. This total is 100,000 USD.

Note

The mentioned prices are for example purposes only. They aren't intended to represent actual costs.

The Microsoft Defender for Cloud prepurchase discount applies to usage from the following products:

- Microsoft Defender for Servers
- Microsoft Defender for App Service
- Microsoft Defender for Storage
- Microsoft Defender for Key Vault
- Microsoft Defender for SQL
- Microsoft Defender for DNS
- Microsoft Defender for Resource Manager
- Microsoft Defender for PostgreSQL
- Microsoft Defender for Azure Cosmos DB
- Microsoft Defender for Containers
- Microsoft Defender CSPM
- Microsoft Defender for APIs
- Microsoft Defender for AI

For more information about available DCU tiers and pricing discounts, see Purchase Defender for Cloud commit units.

## Purchase Defender for Cloud commit units

You can buy Defender for Cloud plans in the [Azure portal reservations page](https://portal.azure.com/). To buy a prepurchase plan, you must have the owner role for at least one enterprise or Microsoft Customer Agreement or an individual subscription with pay-as-you-go rates subscription, or the required role for Cloud Solution Provider (CSP) subscriptions.

- To buy a reservation, you must have owner role or reservation purchaser role on an Azure subscription.
- For Enterprise Agreement (EA) subscriptions, the **Reserved Instances** policy option must be enabled in the [EA enrollment policies page](/en-us/azure/cost-management-billing/manage/direct-ea-administration#view-and-manage-enrollment-policies). Or if that setting is disabled, you must be an EA Admin of the subscription.
- For CSP subscriptions, follow the steps in [Acquire, provision, and manage Azure reserved VM instances (RI) + server subscriptions for customers](/en-us/partner-center/azure-ri-server-subscriptions).

**To Purchase:**

1. Go to the [Azure portal Reservations page](https://portal.azure.com/).
2. Go to **Reservations** and then at the top of the page, select **+ Add**.
3. On the **Purchase reservations** page, select **Microsoft Defender for Cloud Pre-Purchase Plan**.
4. On the **Select the product you want to purchase** page, select a subscription. Use the **Subscription** list to select the subscription used to pay for the reserved capacity.

    The payment method of the subscription is charged the upfront costs for the reserved capacity. Charges are deducted from the enrollment's Azure Prepayment, previously called *monetary commitment*, balance or charged as overage.
5. Select a scope. Use the **Scope** list to select a subscription scope:

    - **Single resource group scope**: Applies the reservation discount to the matching resources in the selected resource group only.
    - **Single subscription scope**: Applies the reservation discount to the matching resources in the selected subscription.
    - **Shared scope**: Applies the reservation discount to matching resources in eligible subscriptions that are in the billing context. For Enterprise Agreement customers, the billing context is the enrollment.
    - **Management group**: Applies the reservation discount to the matching resource in the list of subscriptions that are a part of both the management group and billing scope.
6. Select how many Microsoft Defender for Cloud commit units you want to purchase and complete the purchase.

    [![Screenshot of purchase reservations for Defender for Cloud.](media/prepay-reserved-capacity/purchase-reservations.png)](media/prepay-reserved-capacity/purchase-reservations.png#lightbox)

Note

- The prices listed on the **Reservation** page are always presented in USD.
- Defender Credit Units are deducted at USD retail prices.

## View plan utilization after purchase

To view reservation plan utilization in the Azure portal, sign in, go to the **Reservations** section, and review the list of reservations where you have **Owner** or **Reader** access.

You can also access reservation utilization through APIs, PowerShell, or the CLI.

For more information, see [Reservation utilization](/en-us/azure/cost-management-billing/reservations/reservation-utilization).

## Change the purchase scope

You can make the following types of changes to a reservation after purchase:

- Update reservation scope
- Azure role-based access control (Azure RBAC)

You can't split or merge the Defender for Cloud pre-purchase plan. For more information about managing reservations, see [Manage reservations after purchase](/en-us/azure/cost-management-billing/reservations/manage-reserved-vm-instance).

## Cancel or exchange Defender for Cloud commit units

Cancel and exchange isn't supported for Defender for Cloud prepurchase plans. All purchases are final.