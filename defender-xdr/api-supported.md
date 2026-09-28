---
layout: Conceptual
title: Supported Microsoft Defender XDR APIs - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/api-supported
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about the specific supported Microsoft Defender XDR entities where you can create API calls to.
ms.service: defender-xdr
ms.author: edbaynash
author: EdB-MSFT
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- must-keep
ms.topic: reference
ms.custom: api
ms.date: 2025-04-18T00:00:00.0000000Z
locale: en-us
document_id: acf0384c-22a3-616e-74a0-1999d59579c5
document_version_independent_id: acf0384c-22a3-616e-74a0-1999d59579c5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/api-supported.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api-supported
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/api-supported.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 2eec628c-a006-ce2e-b222-090657bf2914
---

# Supported Microsoft Defender XDR APIs - Microsoft Defender XDR | Microsoft Learn

Note

**Try our new APIs using MS Graph security API**. Find out more at: [Use the Microsoft Graph security API - Microsoft Graph | Microsoft Learn](/en-us/graph/api/resources/security-api-overview).

Important

Some information relates to prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

## List of available APIs

| Article | Description |
| --- | --- |
| [Advanced Hunting API](api-advanced-hunting) | Run Advanced Hunting queries. |
| [Incident APIs](api-incident) | List and update incidents, along with other practical tasks. |
| [Streaming API](streaming-api) | Ship real-time events and alerts as they occur in a single data stream. |

### Endpoint URIs

The base URI for both of the main APIs is: https://api.security.microsoft.com. For better performance, use a server closer to your geolocation:

- The United States: api-us.security.microsoft.com
- Europe: api-eu.security.microsoft.com
- The United Kingdom: api-uk.security.microsoft.com

Tokens can be acquired by accessing https://api.security.microsoft.com.

All APIs along the `/api` path use the [OData](/en-us/odata/overview) Protocol; for example, https://api.security.microsoft.com/api/incidents.