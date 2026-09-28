---
layout: Conceptual
title: Microsoft Defender XDR streaming event types supported in Event Streaming API - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/supported-event-types
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn which streaming event types (tables) are supported by the streaming API
ms.service: defender-xdr
ms.author: edbaynash
author: EdB-MSFT
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.topic: concept-article
ms.date: 2021-09-09T00:00:00.0000000Z
locale: en-us
document_id: c5817d35-6c60-9731-d092-6c3bfc721a6f
document_version_independent_id: c5817d35-6c60-9731-d092-6c3bfc721a6f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/supported-event-types.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: supported-event-types
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/supported-event-types.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d774b87-7dcb-40bf-a0b9-5a7a9efff0d1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/89dc5f37-0e4e-4b05-ad87-5fcd2b941a8a
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: fe1a33de-1ce4-4177-7a18-51dddb0d5242
---

# Microsoft Defender XDR streaming event types supported in Event Streaming API - Microsoft Defender XDR | Microsoft Learn

**Applies to:**

- [Microsoft Defender XDR](microsoft-365-defender)

Note

**Try our new APIs using MS Graph security API**. Find out more at: [Use the Microsoft Graph security API - Microsoft Graph | Microsoft Learn](/en-us/graph/api/resources/security-api-overview).

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

The Event Streaming API is constantly being expanded to support more event types. Learn which hunting tables are generally available, currently in public preview, or not yet supported.

## Hunting tables support status in Event Streaming API

The following table includes that status of support for tables in the streaming API, and is not inclusive of all AH schema. For a full list of the API see, [Learn the schema tables](advanced-hunting-schema-tables#learn-the-schema-tables).

Note

Streaming data is only available for columns or fields that are in general availability in Microsoft Defender.

| Table name | Status(Commercial) | GCC | GCC High | DoD |
| --- | --- | --- | --- | --- |
| **[AlertEvidence](advanced-hunting-alertevidence-table)** | GA | GA | GA | GA |
| **[AlertInfo](advanced-hunting-alertinfo-table)** | GA | GA | GA | GA |
| **[BehaviorEntities](advanced-hunting-behaviorentities-table)** | Not available | Not available | Not available | Not available |
| **[BehaviorInfo](advanced-hunting-behaviorinfo-table)** | Not available | Not available | Not available | Not available |
| **[CloudAppEvents](advanced-hunting-cloudappevents-table)** | GA | GA | GA | GA |
| **[DeviceEvents](advanced-hunting-deviceevents-table)** | GA | GA | GA | GA |
| **[DeviceFileCertificateInfo](advanced-hunting-devicefilecertificateinfo-table)** | GA | GA | GA | GA |
| **[DeviceFileEvents](advanced-hunting-devicefileevents-table)** | GA | GA | GA | GA |
| **[DeviceImageLoadEvents](advanced-hunting-deviceimageloadevents-table)** | GA | GA | GA | GA |
| **[DeviceInfo](advanced-hunting-deviceinfo-table)** | GA | GA | GA | GA |
| **[DeviceLogonEvents](advanced-hunting-devicelogonevents-table)** | GA | GA | GA | GA |
| **[DeviceNetworkEvents](advanced-hunting-devicenetworkevents-table)** | GA | GA | GA | GA |
| **[DeviceNetworkInfo](advanced-hunting-devicenetworkinfo-table)** | GA | GA | GA | GA |
| **[DeviceProcessEvents](advanced-hunting-deviceprocessevents-table)** | GA | GA | GA | GA |
| **[DeviceRegistryEvents](advanced-hunting-deviceregistryevents-table)** | GA | GA | GA | GA |
| **[EmailAttachmentInfo](advanced-hunting-emailattachmentinfo-table)** | GA | GA | GA | GA |
| **[EmailEvents](advanced-hunting-emailevents-table)** | GA | GA | GA | GA |
| **[EmailPostDeliveryEvents](advanced-hunting-emailpostdeliveryevents-table)** | GA | GA | GA | GA |
| **[EmailUrlInfo](advanced-hunting-emailurlinfo-table)** | GA | GA | GA | GA |
| **[IdentityLogonEvents](advanced-hunting-identitylogonevents-table)** | GA | GA | GA | GA |
| **[IdentityQueryEvents](advanced-hunting-identityqueryevents-table)** | GA | GA | GA | GA |
| **[IdentityDirectoryEvents](advanced-hunting-identitydirectoryevents-table)** | GA | GA | GA | GA |
| **[UrlClickEvents](advanced-hunting-urlclickevents-table)** | GA | GA | GA | GA |