---
layout: Conceptual
title: Understand Inventory Assets | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/external-attack-surface-management/understanding-inventory-assets
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
description: Learn how Microsoft Defender External Attack Surface Management (Defender EASM) uses proprietary discovery technology to recursively searches for infrastructure with observed connections to known legitimate assets.
author: danielledennis
ms.author: dandennis
ms.date: 2022-07-14T00:00:00.0000000Z
ms.topic: concept-article
ms.custom: sfi-image-nochange
locale: en-us
document_id: ac6f2cbd-fb9f-32b3-45af-51405824988b
document_version_independent_id: b7d730ff-5c98-174b-2d35-c28283f5b8db
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/easm/understanding-inventory-assets.md
site_name: Docs
depot_name: Azure.easm-azure
page_type: conceptual
toc_rel: toc.json
asset_id: external-attack-surface-management/understanding-inventory-assets
moniker_range_name: 
monikers: []
item_type: Content
source_path: easm/understanding-inventory-assets.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 4f4ed143-e687-4ba6-be3b-90e7fa08918a
---

# Understand Inventory Assets | Microsoft Learn

Microsoft Defender External Attack Surface Management (Defender EASM) uses Microsoft proprietary discovery technology to recursively search for infrastructure through observed connections to known legitimate assets (*discovery seeds*). It makes inferences about that infrastructure's relationship to the organization to uncover previously unknown and unmonitored properties.

Defender EASM discovery includes the following kinds of assets:

- Domains
- IP address blocks
- Hosts
- Email contacts
- Autonomous system numbers (ASNs)
- Whois organizations

These asset types make up your attack surface inventory in Defender EASM. The solution discovers externally facing assets that are exposed to the open internet outside of traditional firewall protection. The external assets need to be monitored and maintained to minimize risk and improve the organization’s security posture. Defender EASM actively discovers and monitors the assets, and then surfaces key insights that help you efficiently address any vulnerabilities to your organization.

![Screenshot of the Inventory changes pane with approved inventory numbers of changes by type.](media/inventory-changes-all.png)

## Asset states

All assets are labeled with one of the following states:

| State name | Description |
| --- | --- |
| **Approved Inventory** | An item that is part of your owned attack surface. It's an item that you're directly responsible for. |
| **Dependency** | Infrastructure that is owned by a third party, but it's part of your attack surface because it directly supports the operation of your owned assets. For example, you might depend on an IT provider to host your web content. The domain, host name, and pages would be part of your approved inventory, so you might want to treat the IP address that runs the host as a dependency. |
| **Monitor Only** | An asset that is relevant to your attack surface, but it's not directly controlled or a technical dependency. For example, independent franchisees or assets that belong to related companies might be labeled **Monitor Only** rather than **Approved Inventory** to separate the groups for reporting purposes. |
| **Candidate** | An asset that has some relationship to your organization's known seed assets, but which doesn't have a strong enough connection to immediately label it **Approved Inventory**. You must manually review these candidate assets to determine ownership. |
| **Requires Investigation** | A state similar to the **Candidate** state, but this value is applied to assets that require manual investigation to validate. The state is determined based on our internally generated confidence scores that assess the strength of detected connections between assets. It doesn't indicate the infrastructure's exact relationship to the organization, but it flags the asset for more review to determine how it should be categorized. |

## Handle different asset states

These asset states are uniquely processed and monitored to ensure that you have clear visibility into your most critical assets by default. For example, assets in the **Approved Inventory** state are always represented in dashboard charts, and they're scanned daily to ensure data recency. All other types of assets aren't included in dashboard charts by default. But you can adjust your inventory filters to view assets in different states as needed. Similarly, **Candidate** state assets are scanned only during the discovery process. If these types of assets are owned by your organization, it’s important to review these assets and change their state to **Approved Inventory**.

## Track inventory changes

Your attack surface constantly changes. Defender EASM continuously analyzes and updates your inventory to ensure accuracy. Assets are frequently added and removed from inventory, so it's important to track these changes to understand your attack surface and identify key trends. The inventory changes dashboard provides an overview of these changes. You can easily view *added* and *removed* counts for each asset type. You can filter the dashboard by two date ranges: either the last 7 days or the last 30 days. For a more granular view of inventory changes, see the **Changes by date** section of the dashboard.

[![Screenshot of inventory changes grouped by date.](media/inventory-changes-date.png)](media/inventory-changes-date.png#lightbox)