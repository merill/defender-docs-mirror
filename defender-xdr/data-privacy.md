---
layout: Conceptual
title: Data retention and data security in Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/data-privacy
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Describes data retention, security, and privacy of the service.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
- essentials-security
- essentials-privacy
- essentials-compliance
ms.topic: concept-article
ms.date: 2025-08-24T00:00:00.0000000Z
locale: en-us
document_id: 76b9c968-118e-b5c2-4ebe-67435e002b96
document_version_independent_id: 76b9c968-118e-b5c2-4ebe-67435e002b96
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/data-privacy.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: data-privacy
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/data-privacy.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 1ead6a2c-114d-7fba-3fe2-e7a3188ec2e1
---

# Data retention and data security in Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn

Microsoft Defender XDR integrates with several different Microsoft security services, which collect data using various technologies. Integrated services allow Microsoft Defender XDR to access their data for the purpose of identifying cross-product correlations.

## Collected data

Customer data collected from integrated services includes *processed data*, such as incidents and alerts, and *configuration data*, such as connector settings, rules, and so on.

## Data storage location

Microsoft Defender operates in Microsoft Azure data centers in the following geographical regions:

- **European Union**: North Europe and West Europe
- **United Kingdom**: UK South and UK West
- **United States**: East US 2 and Central US
- **Australia**: Australia East and Australia Southeast
- **Switzerland**: Switzerland North and Switzerland West
- **India**: Central India and South India
- **UAE**: UAE North and UAE Central

Once created, the Microsoft Defender tenant can't be moved to a different region. Your geographical region is shown in the Microsoft Defender portal, under **Settings &gt; Microsoft Defender XDR &gt; Account**.

Customer data stored by integrated services might also be stored in the following locations:

- The original location for the relevant service.
- A region defined by data storage rules of an integrated service, if Microsoft Defender shares data with that service.

## Data retention

Microsoft Defender data is retained for 180 days, and is visible across the Microsoft Defender portal during that time, except for in **Advanced hunting** queries. Cases are an exception and are not deleted.

In the Microsoft Defender portal's **Advanced hunting** page, data is accessible via queries for only 30 days, unless it's streamed through [Microsoft Sentinel](/en-us/azure/sentinel/microsoft-365-defender-sentinel-integration?toc=%2Fdefender-xdr%2Ftoc.json&amp;bc=%2Fdefender-xdr%2Fbreadcrumb%2Ftoc.json&amp;tabs=defender-portal), where retention periods may be longer.

Data continues to be retained and visible, even when a license is under a grace period or in suspended mode. At the end of any grace period or suspension, and no later than 180 days from a contract termination or expiration, data is deleted from Microsoft's systems and is unrecoverable.

Most Defender services also have a default data retention period of 180 days. More information on data retention period per product is found in relevant service docs.

## Data sharing

Microsoft Defender shares data among the following Microsoft products, also licensed by the customer. For customers in the Government Community Cloud (GCC), data sharing between government and commercial cloud environments may occur, depending on the location of the service offering.

- Microsoft Defender for Cloud
- Microsoft Defender for Identity
- Microsoft Defender for Endpoint
- Microsoft Defender for Cloud Apps
- Microsoft Defender for Office 365
- Microsoft Defender for IoT
- Microsoft Sentinel
- Microsoft Intune
- Microsoft Purview
- Microsoft Entra
- Microsoft Defender Vulnerability Management
- Microsoft Copilot for Security