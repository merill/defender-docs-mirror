---
layout: Conceptual
title: GetAnomalousBehaviorsAbout() function in advanced hunting for Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-getanomalousbehaviorsabout-function
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to use the GetAnomalousBehaviorsAbout() function to find UEBA behavior insights that match multiple entity or context criteria.
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
document_id: 2b88223e-d264-5001-fcaa-324d547b0797
document_version_independent_id: 2b88223e-d264-5001-fcaa-324d547b0797
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-getanomalousbehaviorsabout-function.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-getanomalousbehaviorsabout-function
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-getanomalousbehaviorsabout-function.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 99dc29d0-b6b4-c8d0-bc5e-4a2c06d11fd3
---

# GetAnomalousBehaviorsAbout() function in advanced hunting for Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn

Use the `GetAnomalousBehaviorsAbout()` function in [advanced hunting](advanced-hunting-overview) to return behaviors whose insights match multiple entity or contextual criteria.

The function searches the `About` array of each insight. All supplied filters must be satisfied within the same insight for the behavior to be returned.

The function supports up to three filter objects.

## Syntax

```kusto
invoke GetAnomalousBehaviorsAbout(filters)
```

## Parameters

- **filters**—Required. A `dynamic` JSON array containing one to three filter objects.

Each filter object supports the following properties:

| Property | Required | Description |
| --- | --- | --- |
| `Kind` | Yes | The exact entity or context type to match, such as `Account`, `Country`, `IP`, `Host`, or `ISP`. |
| `Value` | No | The exact value to match for the specified `Kind`. Omit `Value` or specify an empty string to match any value of that `Kind`. |

All filter objects use AND logic. A behavior is returned only when every filter is matched within the same insight's `About` array.

Invoke the function as part of a query on a tabular input that contains an `Insights` column of type `string`.

## Return value

Returns the rows from the input table containing at least one insight whose `About` array satisfies all specified filter criteria. All columns from the input table are preserved.

## Examples

### Find insights involving a specific account and any country

```kusto
BehaviorInfo
| where ServiceSource == "Microsoft Sentinel"
| invoke GetAnomalousBehaviorsAbout(
    dynamic([
        {
            "Kind": "Account",
            "Value": "jsmith@contoso.com"
        },
        {
            "Kind": "Country"
        }
    ])
)
| project TimeGenerated, BehaviorId, Title, Insights
| order by TimeGenerated desc
```

### Find insights involving an exact country, account, and IP address

```kusto
BehaviorInfo
| where ServiceSource == "Microsoft Sentinel"
| invoke GetAnomalousBehaviorsAbout(
    dynamic([
        {
            "Kind": "Country",
            "Value": "Brazil"
        },
        {
            "Kind": "Account",
            "Value": "jsmith@contoso.com"
        },
        {
            "Kind": "IP",
            "Value": "1.2.3.4"
        }
    ])
)
| project TimeGenerated, BehaviorId, Title, Insights
```