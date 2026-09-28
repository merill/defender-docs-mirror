---
layout: Conceptual
title: Understand billable assets in Microsoft Defender EASM - Microsoft Defender EASM | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/external-attack-surface-management/understanding-billable-assets
breadcrumb_path: breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/133/azure
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
ms.service: defender-easm
description: This article describes how users are billed for their Defender EASM resource usage, and guides them to the dashboard that displays their counts.
author: danielledennis
ms.author: dandennis
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 67bc1c1c-c407-08e9-bbc2-7b5be187b591
document_version_independent_id: e69a63ea-c55f-8fee-fc71-324b4c7422f8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/easm/understanding-billable-assets.md
site_name: Docs
depot_name: Azure.easm-azure
page_type: conceptual
toc_rel: toc.json
asset_id: external-attack-surface-management/understanding-billable-assets
moniker_range_name: 
monikers: []
item_type: Content
source_path: easm/understanding-billable-assets.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 291fc490-3a60-4aa0-64b3-c08d68b1e568
---

# Understand billable assets in Microsoft Defender EASM - Microsoft Defender EASM | Microsoft Learn

When customers create their first Microsoft Defender External Attack Surface Management (Defender EASM) resource, they're automatically granted a 30-day free trial. Once the trial completes, customers are automatically charged based on their count of billable assets. The charged amount appears on their core Azure billing, with *Defender EASM* appearing as separate line item on their invoice.

## What is a billable asset?

The following kinds of assets are considered billable:

- Approved host:IP combinations
- Approved domains
- Approved IP addresses Assets are only categorized as billable if they're placed in the Approved Inventory state. We don't charge for any other state. Additionally, duplicative host assets are NOT included in the billable asset count.

## Calculate billable assets

The following criteria determine when approved host:IP combinations, IP addresses, and domains are billable. The sum of these billable asset counts comprises your total number of billable assets and thus determines the cost of your subscription.

### Approved host:IP combinations

The Approved Inventory state is the inventory label that marks an asset as owned by your organization and therefore eligible for billing. Hosts in the Approved Inventory state are considered billable if the Defender EASM system observed resolutions within the last 30 days, and each host:IP combination is identified as a billable asset. All hosts in the Approved Inventory state are considered billable, regardless of the state of the coinciding IP address. The IP address doesn't need to be in the Approved Inventory state for the host:IP combination to be included in your billable asset count.

For example: if `www.contoso.com` resolved to 1.2.3.4 and 5.6.7.8 in the past 30 days, both combinations are added to the host count list:

- `www.contoso.com` / 1.2.3.4
- `www.contoso.com` / 5.6.7.8

The host:IP combination list is then analyzed to identify duplicate entries and eliminate duplicate hosts. If a host is a subdomain of a parent host that resolves to the same IP address, we exclude the child from the billable host count. For example, if both `www.contoso.com` and contoso.com resolve to 1.2.3.4, then we exclude `www.contoso.com` 1.2.3.4 from our Host Count list.

### Approved IP addresses

A *billable resolving host* is any host already counted as a billable host:IP combination. IP addresses that resolve to a billable resolving host are excluded from the billable IP address count. All other active IP addresses in the Approved Inventory state are part of the billable IP address count.

For an IP address to be considered active and therefore billable, it must have one of the following:

- A recent detected open port
- A recent detected SSL certificate

An open port or SSL certificate is considered *recent* if observed within the last 30 days.

### Approved domains

Hosts already counted as billable host:IP combinations are considered *billable resolving hosts*. Domains associated with those hosts are excluded from the billable domain count. All other domains in the Approved Inventory state are part of the billable domain count. If a billable host is registered to the domain in question, the domain isn't included in the billable asset count.

For example: if server1.contoso.com recently resolved to an IP address and is therefore included in your billable asset count, then contoso.com isn't added to the billable domain count.

## View billable asset data

Users can view their billable assets count within their Defender EASM resource to better understand how Microsoft determines their pricing. This dashboard displays the total number of assets that are billable and therefore comprise your total spend. Users should expect to see counts from the last 30 days when applicable, excluding the most recent couple days that haven't yet processed.

Prospective customers accessing Defender EASM with a 30-day trial can also see these billable asset counts. Although these users aren't charged until the trial expires, they can view the billable asset dashboard to better understand how they would be billed according to the size of their attack surface.

1. From the Defender EASM resource, select **Billable assets** from the **Manage** section of the left-hand navigation menu.

    ![Screenshot of Billable assets dashboard with left-hand Manage section highlighted in navigation pane.](media/billable-1a.png)
2. The chart displays billable asset counts over the past 30 days (if we have 30 days of data). The individual bars are segmented by asset type so users can quickly understand how their billable assets are distributed across their attack surface. Users can view the daily counts for each kind of asset by hovering their mouse over the chart.

    ![Screenshot of Billable assets chart showing asset counts when hovering over bar.](media/billable-2a.png)
3. Beneath the chart, users can view their current billable asset counts. These numbers are useful when approximating your monthly spend to best protect your organization’s attack surface.

    ![Screenshot of Billable assets counts beneath dashboard.](media/billable-3.png)