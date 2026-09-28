---
layout: Conceptual
title: Optimize Costs with a Prepurchase Plan - Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/billing-pre-purchase-plan
breadcrumb_path: breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
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
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
description: Learn how to save costs and buy a Microsoft Sentinel prepurchase plan
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: daniha
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 74197c4e-7d65-2076-3bf5-e392cc1f2a4a
document_version_independent_id: ce40137c-6367-6893-d52f-38670f95c892
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/billing-pre-purchase-plan.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/billing-pre-purchase-plan
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/billing-pre-purchase-plan.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: c8a7da06-db1e-9367-6e60-64b86ed5f497
---

# Optimize Costs with a Prepurchase Plan - Microsoft Sentinel | Microsoft Learn

Save on your Microsoft Sentinel analytics tier costs when you buy a pre-purchase plan. Pre-purchase plans are commit units (CUs) bought at discounted tiers in your purchasing currency for a specific product. The more you buy, the greater the discount. Purchased CUs pay down qualifying costs in US dollars (USD). So, if Microsoft Sentinel generates a retail cost of $100, then 100 Microsoft Sentinel CUs (SCUs) are consumed.

Your Microsoft Sentinel pre-purchase plan automatically uses your SCUs to pay for eligible analytics tier costs during its one-year term or until the SCUs run out. Your pre-purchase plan SCUs start paying for your Microsoft Sentinel workspace costs without having to redeploy or reassign the plan. By default, plans are configured to renew at the end of the one year term.

## Prerequisites

To buy a pre-purchase plan, you must have one of the following Azure subscriptions and roles:

- For an Azure subscription, the owner role or reservation purchaser role is required.
- For an Enterprise Agreement (EA) subscription, the [**Reserved Instances** policy option](/en-us/azure/cost-management-billing/manage/direct-ea-administration#view-and-manage-enrollment-policies) must be enabled. To enable that policy option, you must be an EA administrator of the subscription.
- For a Cloud Solution Provider (CSP) subscription, follow one of these articles:
    - [Buy Azure reservations on behalf of a customer](/en-us/partner-center/customers/azure-reservations-buying)
    - [Allow the customer to buy their own reservations](/en-us/partner-center/customers/give-customers-permission)

Note

Microsoft Sentinel Commit Units are different from Security Compute Units in Security Copilot. Customers can't use Microsoft Sentinel Commit Units to run Copilot workloads and vice versa. Microsoft Sentinel billable capabilities costs, such as data lake, aren't included in pre-purchase plans or commitment tiers.

## Determine the right size to buy

Pre-purchase plans work well alongside Microsoft Sentinel commitment tiers. To get started, estimate your expected analytics tier ingestion volume and select the right commitment tier. Estimating your expected volume and selecting the right commitment tier helps you determine the appropriate size for your pre-purchase plan. Each pre-purchase plan has a one-year term.

For example, suppose you choose a 200 GB/day commitment tier. With simplified pricing, the estimated monthly cost for both data ingestion and analysis is $20,000 USD—a 39% savings compared to the pay-as-you-go rate for the same volume.

A $100,000 USD pre-purchase plan covers five months of the 200 GB/day commitment tier but is valid for paying Microsoft Sentinel costs for 12 months. The pre-purchase plan is bought at a 22% discount for $78,000 USD.

The savings from the 200 GB/day commitment tier and the pre-purchase plan combine. The original pay-as-you-go price for five months of 200 GB/day ingestion and analysis costs is, for example, about $160,000 USD. With an accurate commitment tier and a pre-purchase plan, the cost is reduced to $78,000 USD for a combined savings of over 51%. Since the example plan is depleted after just five months, the best way to ensure continued savings is to purchase more SCUs with another plan.

For more information, see the following articles:

- [Switch to simplified pricing](enroll-simplified-pricing-tier)
- [Set or change commitment tier](billing-reduce-costs#set-or-change-pricing-tier)

Important

The prices mentioned are for the purposes of example purposes only. To determine the latest commitment tier prices, see [Microsoft Sentinel pricing](https://azure.microsoft.com/pricing/details/microsoft-sentinel/).

All Microsoft Sentinel pricing tiers qualify for Microsoft Sentinel pre-purchase plans. From your Microsoft Sentinel bill, these costs are the entries with the **Sentinel** service name in the invoice details. These costs don't include Azure Monitor tiers, retention, restore, and search costs. Eligible Microsoft Sentinel usage is deducted from the prepurchased Microsoft Sentinel CUs automatically.

For more information on how to view Microsoft Sentinel simplified or classic pricing tiers in your invoice details, see [Understand your Microsoft Sentinel bill](billing#understand-your-microsoft-sentinel-bill).

Keep in mind, Microsoft Sentinel integrates with many other Azure services that have separate costs not eligible to use with the pre-purchase SCUs. For more information, see [Costs and pricing for other services](billing#costs-and-pricing-for-other-services).

## Purchase Microsoft Sentinel commit units

Warning

Microsoft Sentinel Pre-Purchase Plan purchases are final. Cancellations and exchanges aren't supported.

Purchase Microsoft Sentinel pre-purchase plans in the [Azure portal reservations](https://portal.azure.com/#view/Microsoft_Azure_Reservations/ReservationsBrowseBlade/productType/Reservations).

1. Go to the [Azure portal home page](https://portal.azure.com).
2. Navigate to the **Reservations** service.
3. On the **Purchase reservations page**, select **Microsoft Sentinel Pre-Purchase Plan**.[![Screenshot showing Microsoft Sentinel pre-purchase plan.](media/sentinel-plan.png)](media/sentinel-plan.png#lightbox)
4. On the **Select the product you want to purchase** page, select a subscription. Use the **Subscription** list to select the subscription used to pay for the reserved capacity. The payment method of the subscription is charged the upfront costs for the reserved capacity. Charges are deducted from the enrollment's Azure Prepayment (previously called monetary commitment) balance or charged as overage.
5. Select a scope.

    - **Single resource group scope**: Applies the reservation discount to the matching resources in the selected resource group only.
    - **Single subscription scope**: Applies the reservation discount to the matching resources in the selected subscription.
    - **Shared scope**: Applies the reservation discount to matching resources in eligible subscriptions that are in the billing context. For Enterprise Agreement customers, the billing context is the enrollment.
    - **Management group**: Applies the reservation discount to the matching resource in the list of subscriptions that are a part of both the management group and billing scope.
6. Select how many Microsoft Sentinel commit units you want to purchase.

    [![Screenshot showing Microsoft Sentinel pre-purchase plan discount tiers and their term lengths.](media/sentinel-pre-purchase-plan.png)](media/sentinel-pre-purchase-plan.png#lightbox)
7. Choose to automatically renew the pre-purchase reservation. *The setting is configured to renew automatically by default*. For more information, see [Renew a reservation](/en-us/azure/cost-management-billing/reservations/reservation-renew).

## Change scope and ownership

You can make the following types of changes to a reservation after purchase:

- Update reservation scope
- Update who can view or manage the reservation. For more information, see [Who can manage a reservation by default](/en-us/azure/cost-management-billing/reservations/manage-reserved-vm-instance#who-can-manage-a-reservation-by-default).

You can't split or merge a **Microsoft Sentinel Pre-Purchase Plan**. For more information about managing reservations, see [Manage reservations after purchase](/en-us/azure/cost-management-billing/reservations/manage-reserved-vm-instance).

## Cancellations and exchanges

Cancel and exchange operations aren't supported for **Microsoft Sentinel Pre-Purchase Plans**. All purchases are final.