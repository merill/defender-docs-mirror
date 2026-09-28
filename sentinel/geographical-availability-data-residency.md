---
layout: Conceptual
title: Geographical availability and data residency in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/geographical-availability-data-residency
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
description: Learn about privacy, data residency, and geographical availability in Microsoft Sentinel.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: concept-article
ms.date: 2026-08-18T00:00:00.0000000Z
ms.custom: references_regions
locale: en-us
document_id: 61e5a8c4-456d-cb08-452f-19bf7026b89d
document_version_independent_id: c4d1f0cd-48ec-cc55-bd54-a29e94478c19
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/geographical-availability-data-residency.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/geographical-availability-data-residency
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/geographical-availability-data-residency.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: b41c1dab-4595-b5a3-dc24-e1543d962d56
---

# Geographical availability and data residency in Microsoft Sentinel | Microsoft Learn

After your data is collected, stored, and processed, compliance can become an important design requirement, with a significant impact on your Microsoft Sentinel architecture. Having the ability to validate and prove who has access to what data under all conditions is a critical data sovereignty requirement in many countries and regions, and assessing risks and getting insights in Microsoft Sentinel workflows is a priority for many customers.

This article can help you meet compliance requirements by describing where Microsoft Sentinel data is stored.

Important

Microsoft Sentinel was retired in Azure operated by 21Vianet on August 18, 2026, as described in the [announcement posted by 21Vianet](https://aka.ms/sentinelretirementinchina). Microsoft Sentinel is no longer available in this region.

We recommend that customers work with their account representatives for Microsoft Azure operated by 21Vianet to assess the impact of this retirement on their own operations.

## Collected data

Microsoft Sentinel collects the following types of data:

- **Raw data**, such as event data collected from connected Microsoft services and partner systems. Data from multiple clouds and sources are streamed to the customer’s Azure Log Analytics workspace associated with Microsoft Sentinel, under the customer’s tenant’s subscription. This approach gives the customer the ability to choose region and retention and deletion policies.
- **Processed data**, such as incidents, alerts, behaviors, and so on.
- **Configuration data**, such as connector settings, rules, and so on.

## Data storage location

Microsoft Sentinel stores data used by the service, including customer data, in the same region as the associated Azure Log Analytics workspace. For more information, see Supported regions.

Microsoft Sentinel processes data in one of the following locations:

- For Log Analytics workspaces located in Europe, Microsoft Sentinel processes customer data in Europe.
- For Log Analytics workspaces located in Israel, Microsoft Sentinel processes customer data in Israel.
- For workspaces located in any other location, Microsoft Sentinel processes customer data in a US region.

When you onboard Microsoft Sentinel from the Defender portal, the service might process data in the destination regions specified during onboarding, or in the existing Microsoft Defender XDR regions if applicable. The raw data storage location, however, remains unchanged. For more information, see [Data security and retention in Microsoft Defender XDR](/en-us/defender-xdr/data-privacy).

### Supported regions

The following table shows the supported regions supporting Microsoft Sentinel SIEM and data lake.

| Continent | Country/Region | SIEM supported region | Data lake supported region |
| --- | --- | --- | --- |
| **North America** | **Canada** | • Canada Central• Canada East | • Canada Central |
|  | **United States** | • Central US• East US• East US 2• East US 2 EUAP• North Central US• South Central US• West US• West US 2• West US 3• West Central US**Azure government**• USGov Arizona• USGov Virginia• USNat East• USNat West• USSec East• USSec West | • Central US• East US• East US 2• South Central US• West US 2 |
| **South America** | **Brazil** | • Brazil South• Brazil Southeast |  |
| **Asia and Middle East** |  | • East Asia• Southeast Asia | • Southeast Asia |
|  | **India** | • Central India• Jio India West• Jio India Central | • Central India |
|  | **Israel** | • Israel Central | • Israel Central |
|  | **Japan** | • Japan East• Japan West | • Japan East |
|  | **Korea** | • Korea Central• Korea South |  |
|  | **Qatar** | • Qatar Central |  |
|  | **UAE** | • UAE Central• UAE North |  |
| **Europe** |  | • North Europe• West Europe | • North Europe• West Europe |
|  | **France** | • France Central• France South | • France Central |
|  | **Germany** | • Germany West Central |  |
|  | **Italy** | • Italy North | • Italy North |
|  | **Norway** | • Norway East• Norway West |  |
|  | **Sweden** | • Sweden Central |  |
|  | **Switzerland** | • Switzerland North• Switzerland West | • Switzerland North |
|  | **UK** | • UK South• UK West | • UK South |
| **Australia** | **Australia** | • Australia CentralAustralia Central 2• Australia East• Australia Southeast | • Australia East |
| **Africa** | **South Africa** | • South Africa North |  |

Important

Microsoft Sentinel data lake must be deployed in the same Azure region as the associated primary Sentinel workspace.

## Data retention

Data from Microsoft Sentinel is retained until the earliest of the following dates:

- The customer [removes Microsoft Sentinel from their workspace](offboard)
- As per a retention policy set by the customer

Until that time, customers can always delete their data.

Customer data is kept and is available while the license is under a grace period or in suspended mode. At the end of this period, and no later than 90 days from contract termination or expiration, the data is erased from Microsoft's systems to make it unrecoverable.

## Data sharing for Microsoft Sentinel

Microsoft Sentinel may share data, including customer data, among the following Microsoft products:

- Microsoft Defender XDR
- Azure Log Analytics
- Security Copilot