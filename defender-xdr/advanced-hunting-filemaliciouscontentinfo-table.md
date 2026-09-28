---
layout: Conceptual
title: FileMaliciousContentInfo table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-filemaliciouscontentinfo-table
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about the FileMaliciousContentInfo table of the advanced hunting schema
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
ms.date: 2025-12-04T00:00:00.0000000Z
locale: en-us
document_id: e5efd235-f98f-abaa-7a2e-2be3fc0c2448
document_version_independent_id: e5efd235-f98f-abaa-7a2e-2be3fc0c2448
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-filemaliciouscontentinfo-table.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-filemaliciouscontentinfo-table
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-filemaliciouscontentinfo-table.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
platformId: 0c42408d-25b4-d8bd-8508-cd80d1a362ca
---

# FileMaliciousContentInfo table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn

Important

Some information relates to prereleased product which might be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

The `FileMaliciousContentInfo` table in the [advanced hunting](advanced-hunting-overview) schema contains information about files that were processed by Microsoft Defender for Office 365 in SharePoint Online, OneDrive, and Microsoft Teams. Use this reference to construct queries that return information from this table.

Tip

For detailed information about the events types (`ActionType` values) supported by a table, use the built-in schema reference available in the Defender portal.

This advanced hunting table is populated by records from Defender for Office 365. If your organization didn't deploy the service in Microsoft Defender, queries that use the table aren't going to work or return any results. For more information about how to deploy Defender for Office 365 in the Defender portal, read [Deploy supported services](deploy-supported-services).

For information on other tables in the advanced hunting schema, [see the advanced hunting reference](advanced-hunting-schema-tables).

| Column name | Data type | Description |
| --- | --- | --- |
| `Timestamp` | `datetime` | Date and time when the event was generated |
| `Workload` | `string` | Information about the workload from which the URL originated from |
| `FileName` | `string` | Name of the file that the recorded action was applied to |
| `FolderPath` | `string` | Path of the folder containing the file that the recorded action was applied to |
| `FileSize` | `long` | Size of the file in bytes |
| `SHA256` | `string` | SHA-256 of the file that the recorded action was applied to |
| `FileOwnerDisplayName` | `string` | Account recorded as owner of the file |
| `FileOwnerUpn` | `string` | Account recorded as owner of the file |
| `DocumentId` | `string` | Unique identifier of the file |
| `ThreatTypes` | `dynamic` | Verdict from the email filtering stack on whether the email contains malware, phishing, or other threats |
| `ThreatNames` | `string` | Detection name for malware or other threats found |
| `DetectionMethods` | `string` | Methods used to detect malware, phishing, or other threats found in the email |
| `LastModifyingAccountUpn` | `string` | Account that last modified this file |
| `LastModifiedTime` | `datetime` | Date and time the item or related metadata was last modified |
| `FileCreationTime	` | `datetime` | Timestamp of the file creation |
| `ReportId` | `string` | Unique identifier for the event |

## Read more

- [Advanced hunting overview](advanced-hunting-overview)
- [Learn the query language](advanced-hunting-query-language)
- [Use shared queries](advanced-hunting-shared-queries)
- [Hunt across devices, emails, apps, and identities](advanced-hunting-query-emails-devices)
- [Understand the schema](advanced-hunting-schema-tables)
- [Apply query best practices](advanced-hunting-best-practices)