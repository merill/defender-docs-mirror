---
layout: Conceptual
title: GetFirstSeenBehaviors() function in advanced hunting for Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-getfirstseenbehaviors-function
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to use the GetFirstSeenBehaviors() function to find UEBA behaviors that contain FirstSeen insights.
ms.service: defender-xdr
ms.subservice: adv-hunting
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.custom:
- cx-ti
- cx-ah
ms.topic: reference
ms.date: 2026-07-15T00:00:00.0000000Z
locale: en-us
document_id: e4312a04-5201-a835-7a9d-d1fe609b1835
document_version_independent_id: e4312a04-5201-a835-7a9d-d1fe609b1835
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-getfirstseenbehaviors-function.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-getfirstseenbehaviors-function
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-getfirstseenbehaviors-function.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 557c4b98-e4e9-e8fb-62ef-2870e27fbaee
---

# GetFirstSeenBehaviors() function in advanced hunting for Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn

Use the `GetFirstSeenBehaviors()` function in [advanced hunting](advanced-hunting-overview) to return behaviors that contain at least one `FirstSeen` insight in the `Insights` column.

A `FirstSeen` insight indicates that a behavior, entity, value, or combination of values was observed for the first time.

## Syntax

```kusto
invoke GetFirstSeenBehaviors()
```

## Parameters

This function has no explicit parameters. Invoke it as part of a query on a tabular input that contains an `Insights` column of type `string`.

## Return value

Returns the rows from the input table that contain at least one `FirstSeen` insight. All columns from the input table are preserved.

## Example

### Find recent Microsoft Sentinel behaviors with FirstSeen insights

```kusto
BehaviorInfo
| where ServiceSource == "Microsoft Sentinel"
| where TimeGenerated > ago(1d)
| invoke GetFirstSeenBehaviors()
| project TimeGenerated, BehaviorId, Title, Insights
```