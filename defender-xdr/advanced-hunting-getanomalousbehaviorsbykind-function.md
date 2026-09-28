---
layout: Conceptual
title: GetAnomalousBehaviorsByKind() function in advanced hunting for Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-getanomalousbehaviorsbykind-function
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to use the GetAnomalousBehaviorsByKind() function to find UEBA behavior insights involving a specific entity or context type.
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
document_id: 32365911-8960-1f29-dbb4-bdc48d3884fd
document_version_independent_id: 32365911-8960-1f29-dbb4-bdc48d3884fd
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-getanomalousbehaviorsbykind-function.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-getanomalousbehaviorsbykind-function
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-getanomalousbehaviorsbykind-function.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 7412bb31-db13-7138-dd0c-29ba90dab63f
---

# GetAnomalousBehaviorsByKind() function in advanced hunting for Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn

Use the `GetAnomalousBehaviorsByKind()` function in [advanced hunting](advanced-hunting-overview) to return behaviors containing an insight that involves a specific entity or contextual type.

The function searches the `Kind` values in each insight's `About` array. You can optionally limit the results to a specific insight type.

## Syntax

```kusto
invoke GetAnomalousBehaviorsByKind(entityKind, insightType)
```

## Parameters

- **entityKind**—Required. A `string` containing the exact `Kind` value to match in the insight's `About` array. Examples include `Account`, `Country`, `IP`, `Host`, `ISP`, and `Device`.
- **insightType**—Optional. A `string` containing the exact insight type to match, such as `FirstSeen`, `UncommonValue`, or `HighVolumeAnomaly`. If you omit this parameter or specify an empty string, the function matches all insight types.

Invoke the function as part of a query on a tabular input that contains an `Insights` column of type `string`.

## Return value

Returns the rows from the input table containing an insight whose `About` array includes an entry with the specified `Kind`. When `insightType` is provided, only insights of that type are evaluated. All columns from the input table are preserved.

## Examples

### Find FirstSeen insights involving a country

```kusto
BehaviorInfo
| where ServiceSource == "Microsoft Sentinel"
| invoke GetAnomalousBehaviorsByKind("Country", "FirstSeen")
| project TimeGenerated, BehaviorId, Title, Insights
| order by TimeGenerated desc
```

### Find all insights involving an IP address

Omit the `insightType` argument to return matching insights of any type.

```kusto
BehaviorInfo
| where ServiceSource == "Microsoft Sentinel"
| invoke GetAnomalousBehaviorsByKind("IP")
| project TimeGenerated, BehaviorId, Title, Insights
```