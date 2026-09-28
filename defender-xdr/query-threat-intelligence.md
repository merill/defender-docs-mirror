---
layout: Conceptual
title: Query threat intelligence in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/query-threat-intelligence
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to query built-in Microsoft threat intelligence in advanced hunting with the ThreatIntelEntities table.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
- usx-security
ms.topic: how-to
ai-usage: ai-assisted
ms.date: 2026-08-23T00:00:00.0000000Z
locale: en-us
document_id: 20e0581f-709f-3e91-3f8b-7fc0e517173e
document_version_independent_id: 20e0581f-709f-3e91-3f8b-7fc0e517173e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/query-threat-intelligence.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: query-threat-intelligence
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/query-threat-intelligence.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
platformId: c05636a1-3fa0-17d1-b0a4-b597023df803
---

# Query threat intelligence in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn

Use the `ThreatIntelEntities` table in advanced hunting to query Microsoft's built-in threat intelligence, including known indicators of compromise (IOCs), threat actors, and malicious infrastructure. Correlate this intelligence with activity in your environment to support threat hunting, custom detections, and response.

## Query threat intelligence in advanced hunting

Built-in threat intelligence is available in the `ThreatIntelEntities` table.

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
2. Select **Advanced hunting**.
3. Select **Schema**.
4. Expand the **Threat intelligence** group.
5. Select the `ThreatIntelEntities` table.

## ThreatIntelEntities table columns

The `ThreatIntelEntities` table includes the following columns:

| Column | Type | Description |
| --- | --- | --- |
| `TenantId` | string | The Log Analytics workspace ID. |
| `Id` | string | A value that uniquely identifies the indicator STIX object. |
| `SourceSystem` | string | The source system that collected the entity. |
| `LastUpdateMethod` | string | The component that last updated the entity. |
| `AdditionalFields` | dynamic | Type-specific fields associated with the entity. |
| `Data` | dynamic | All object properties, formatted according to the [STIX 2.1 specification](https://docs.oasis-open.org/cti/stix/v2.1/os/stix-v2.1-os.html). |
| `IsActive` | bool | Indicates whether the indicator is active and valid for detections. |
| `Revoked` | bool | Indicates whether the indicator was revoked. |
| `ValidUntil` | datetime | The time at which the indicator is no longer considered valid for the behaviors it represents. |
| `ValidFrom` | datetime | The time from which the indicator is considered valid for the behaviors it represents. |
| `Created` | datetime | The date and time when the indicator was created. |
| `Modified` | datetime | The date and time when the indicator was last modified. |
| `Tags` | string | Tags associated with the indicator. |
| `Confidence` | int | The creator's confidence in the correctness of the data. The value must be from 0 through 100. |
| `Pattern` | string | The detection pattern for the indicator, which might be expressed as a STIX pattern. |
| `ObservableKey` | string | The entire left-hand side of an equality comparison in the pattern. |
| `ObservableValue` | string | The entire right-hand side of an equality comparison in the pattern. |
| `Type` | string | The name of the table. |

## Expand threat intelligence coverage

Use Microsoft Sentinel to integrate external threat intelligence feeds with your Microsoft Defender data.

For more information, see [Threat intelligence in Microsoft Sentinel](/en-us/azure/sentinel/understand-threat-intelligence).