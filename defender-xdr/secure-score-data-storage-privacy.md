---
layout: Conceptual
title: Microsoft Secure score data storage and privacy - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/secure-score-data-storage-privacy
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about how Microsoft Secure score handles privacy and data that it collects.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
audience: ITPro
ms.collection:
- m365-security
- tier2
ms.topic: concept-article
search.appverid: met150
ms.date: 2025-04-28T00:00:00.0000000Z
locale: en-us
document_id: 2f6fad38-0465-2932-f431-0a0507e4c19d
document_version_independent_id: 2f6fad38-0465-2932-f431-0a0507e4c19d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/secure-score-data-storage-privacy.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: secure-score-data-storage-privacy
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/secure-score-data-storage-privacy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cd48b104-e308-4e08-a405-66f04a7df418
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ac23bdb5-c078-4620-8ee2-60eba45e97f8
platformId: b6410d4b-8f95-2d79-0966-5d85f5a0135b
---

# Microsoft Secure score data storage and privacy - Microsoft Defender XDR | Microsoft Learn

This section covers frequently asked questions regarding privacy and data handling for Secure Score.

## Data storage location

Secure score operates in the Microsoft Azure datacenters in the European Union, the United Kingdom, or in the United States. Customer data collected by the service may be stored in: (a) the geo-location of the tenant as identified during provisioning or, (b) if Secure Score uses another Microsoft online service to process such data, the geolocation as defined by the data storage rules of that other online service.

Customer data in pseudonymized form may also be stored in the central storage and processing systems in the United States.

Once configured, you can't change the location where your data is stored. This provides a convenient way to minimize compliance risk by actively selecting the geographic locations where your data resides.

## How long does Microsoft store my data? What is Microsoft's data retention policy?

### At service onboarding

By default, data is retained for 90 days based on your active licenses.

### At contract termination or expiration

Your data is kept and is available to you while the license is under grace period or suspended mode. At the end of this period, data that is associated to an expired or terminated license is erased from Microsoft's systems to make it unrecoverable, no later than 90 days from the associated contract termination or expiration.

Tip

Do you want to learn more? Engage with the Microsoft Security community in our Tech Community: [Microsoft Defender XDR Tech Community](https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection).