---
layout: Conceptual
title: Stream Microsoft Defender XDR events - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/streaming-api
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to configure Microsoft Defender XDR to stream Advanced Hunting events to Event Hubs or Azure storage account
ms.service: defender-xdr
ms.author: edbaynash
author: EdB-MSFT
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.topic: concept-article
ms.date: 2023-07-25T00:00:00.0000000Z
locale: en-us
document_id: 19d433cd-fc59-b3ce-7e11-d436ea4c2dbe
document_version_independent_id: 19d433cd-fc59-b3ce-7e11-d436ea4c2dbe
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/streaming-api.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: streaming-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/streaming-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d774b87-7dcb-40bf-a0b9-5a7a9efff0d1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/f0234678-3067-4edc-abf7-8142d54bb7d2
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/89dc5f37-0e4e-4b05-ad87-5fcd2b941a8a
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/b0f4f6b9-28ed-4892-be4e-517310289c68
platformId: f101ddac-4742-2c8c-10fd-a6417612a066
---

# Stream Microsoft Defender XDR events - Microsoft Defender XDR | Microsoft Learn

**Applies to:**

- [Microsoft Defender XDR](https://go.microsoft.com/fwlink/p/?linkid=2118804)

Note

**Try our new APIs using MS Graph security API**. Find out more at: [Use the Microsoft Graph security API - Microsoft Graph | Microsoft Learn](/en-us/graph/api/resources/security-api-overview?view=graph-rest-1.0&amp;preserve-view=true). If you're using Microsoft Defender for Business, see [Use the streaming API (preview) with Microsoft Defender for Business](/en-us/defender-business/mdb-streaming-api).

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Stream Advanced Hunting events to Event Hubs and/or Azure storage account

Microsoft Defender XDR supports streaming events through [Advanced Hunting](advanced-hunting-overview) to an [Event Hubs](/en-us/azure/event-hubs/) and/or [Azure storage account](/en-us/azure/event-hubs/).

For more information on Microsoft Defender XDR streaming API, see the [video](https://learn-video.azurefd.net/vod/player?id=56edfb3f-b612-4e4c-acb9-4bbd141bd535).