---
layout: Conceptual
title: GetAnomalousBehaviorsByValue() function in advanced hunting for Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-getanomalousbehaviorsbyvalue-function
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to use the GetAnomalousBehaviorsByValue() function to find UEBA behavior insights involving a specific entity or context value.
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
document_id: 8ee9af79-a8ca-89a7-172d-623eeb504cfc
document_version_independent_id: 8ee9af79-a8ca-89a7-172d-623eeb504cfc
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-getanomalousbehaviorsbyvalue-function.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-getanomalousbehaviorsbyvalue-function
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-getanomalousbehaviorsbyvalue-function.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 9c0b6aa3-5a90-80e8-e65d-b3d695e4f7a3
---

# GetAnomalousBehaviorsByValue() function in advanced hunting for Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn

Use the `GetAnomalousBehaviorsByValue()` function in [advanced hunting](advanced-hunting-overview) to return behaviors containing an insight that involves a specific entity or contextual value.

The function searches the `Value` fields in each insight's `About` array. You can optionally limit the results to a specific insight type.

## Syntax

```kusto
invoke GetAnomalousBehaviorsByValue(entityValue, insightType)
```

## Parameters

- **entityValue**—Required. A `string` containing the exact `Value` to match in the insight's `About` array. The value can represent an account, country, IP address, ISP, device, resource, or other contextual value.
- **insightType**—Optional. A `string` containing the exact insight type to match, such as `FirstSeen`, `UncommonValue`, or `HighVolumeAnomaly`. If you omit this parameter or specify an empty string, the function matches all insight types.

Invoke the function as part of a query on a tabular input that contains an `Insights` column of type `string`.

## Return value

Returns the rows from the input table containing an insight whose `About` array includes an entry with the specified `Value`. When `insightType` is provided, only insights of that type are evaluated. All columns from the input table are preserved.

## Examples

### Find FirstSeen insights involving a specific account

```kusto
BehaviorInfo
| where ServiceSource == "Microsoft Sentinel"
| invoke GetAnomalousBehaviorsByValue(
    "jsmith@contoso.com",
    "FirstSeen"
)
| project TimeGenerated, BehaviorId, Title, Insights
| order by TimeGenerated desc
```

### Find all insights involving a specific country

Omit the `insightType` parameter to return matching insights of any type.

```kusto
BehaviorInfo
| where ServiceSource == "Microsoft Sentinel"
| invoke GetAnomalousBehaviorsByValue("Sweden")
| project TimeGenerated, BehaviorId, Title, Insights
```