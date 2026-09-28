---
layout: Conceptual
title: Stream Microsoft Defender for Endpoint event - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/raw-data-export
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to configure Microsoft Defender for Endpoint to stream Advanced Hunting events to Event Hubs or Azure storage account
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- must-keep
ms.topic: reference
ms.subservice: reference
ms.custom: api
ms.date: 2020-12-18T00:00:00.0000000Z
locale: en-us
document_id: 047f3dae-0140-ba37-2b87-612d6935205b
document_version_independent_id: 047f3dae-0140-ba37-2b87-612d6935205b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/raw-data-export.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/raw-data-export
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/raw-data-export.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d774b87-7dcb-40bf-a0b9-5a7a9efff0d1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/f0234678-3067-4edc-abf7-8142d54bb7d2
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/89dc5f37-0e4e-4b05-ad87-5fcd2b941a8a
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/b0f4f6b9-28ed-4892-be4e-517310289c68
platformId: 97454742-feb7-279a-7b74-a4bb993dab29
---

# Stream Microsoft Defender for Endpoint event - Microsoft Defender for Endpoint | Microsoft Learn

Tip

For the full data streaming experience available, see [Stream Microsoft Defender XDR events](/en-us/defender-xdr/streaming-api). If you're using Microsoft Defender for Business, see [Use the streaming API with Microsoft Defender for Business](/en-us/defender-business/mdb-streaming-api).

## Stream Advanced Hunting events to Event Hubs and/or Azure storage account

Microsoft Defender for Endpoint supports streaming events available through [Advanced Hunting](/en-us/defender-xdr/advanced-hunting-overview) to an [Event Hubs](/en-us/azure/event-hubs/) and/or [Azure storage account](/en-us/azure/storage/common/storage-account-overview).