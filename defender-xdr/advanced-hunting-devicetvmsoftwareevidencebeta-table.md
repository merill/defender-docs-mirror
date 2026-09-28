---
layout: Conceptual
title: DeviceTvmSoftwareEvidenceBeta table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-devicetvmsoftwareevidencebeta-table
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to use the DeviceTvmSoftwareEvidenceBeta table in the advanced hunting schema.
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
ms.date: 2026-06-14T00:00:00.0000000Z
locale: en-us
document_id: cf176cae-1ceb-6a20-877d-e7fc846f4f56
document_version_independent_id: cf176cae-1ceb-6a20-877d-e7fc846f4f56
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-devicetvmsoftwareevidencebeta-table.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-devicetvmsoftwareevidencebeta-table
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-devicetvmsoftwareevidencebeta-table.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: ade9f60f-ced7-f374-d410-7057f24830a7
---

# DeviceTvmSoftwareEvidenceBeta table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn

Important

The `DeviceTvmSoftwareEvidenceBeta` table is currently in beta. Once it leaves beta, the final table name changes and column names might also change. The modifications are likely to break queries that are still using previous names. Users are advised to review and adjust their queries when this table is finalized.

The `DeviceTvmSoftwareEvidenceBeta` table in the advanced hunting schema contains data from [Microsoft Defender Vulnerability Management](/en-us/windows/security/threat-protection/microsoft-defender-atp/next-gen-threat-and-vuln-mgt) related to the [software evidence section](/en-us/defender-vulnerability-management/tvm-software-inventory#software-evidence). This table allows you to view evidence of where a specific software was detected on a device. You can use this table, for example, to identify the file paths of specific software. Use this reference to construct queries that return information from the table.

Microsoft Defender for Endpoint data populates this advanced hunting table. If your organization didn't deploy the service in Microsoft Defender, queries that use the table aren't going to work or return any results. For more information about how to deploy Defender for Endpoint in the Defender portal, read [Deploy supported services](deploy-supported-services).

For information on other tables in the advanced hunting schema, see [the advanced hunting reference](advanced-hunting-schema-tables).

Important

**This Defender Vulnerability Management (TVM) table isn't ingested into Microsoft Sentinel.** In Microsoft Sentinel, this table is exposed for schema visibility only (for example, autocomplete and query validation), not for data ingestion. As a result, Microsoft Sentinel can accept queries that reference this table, but those queries return no results.

To query this table’s data, run the query in Defender XDR Advanced Hunting, where the data is available. Using TVM table data directly in Microsoft Sentinel analytics and detections isn't currently supported unless you build a [custom ingestion path](/en-us/azure/sentinel/create-custom-connector). For more information, see [Which Defender XDR tables aren't supported in Microsoft Sentinel](/en-us/azure/sentinel/connect-microsoft-365-defender#which-defender-xdr-tables-arent-supported-in-microsoft-sentinel).

| Column name | Data type | Description |
| --- | --- | --- |
| `DeviceId` | `string` | Unique identifier for the device in the service |
| `SoftwareVendor` | `string` | Name of the software publisher |
| `SoftwareName` | `string` | Name of the software product |
| `SoftwareVersion` | `string` | Version number of the software product |
| `RegistryPaths` | `dynamic` | Registry paths where evidence indicating the existence of the software on a device was detected |
| `DiskPaths` | `dynamic` | Disk paths where file-level evidence indicating the existence of the software on a device was detected |
| `LastSeenTime` | `string` | Date and time when the device was last seen by this service |

## Read more

- [Microsoft Defender Vulnerability Management](/en-us/windows/security/threat-protection/microsoft-defender-atp/next-gen-threat-and-vuln-mgt)
- [Proactively hunt for threats](advanced-hunting-overview)
- [Learn the query language](advanced-hunting-query-language)
- [Use shared queries](advanced-hunting-shared-queries)
- [Hunt across devices, emails, apps, and identities](advanced-hunting-query-emails-devices)
- [Understand the schema](advanced-hunting-schema-tables)
- [Apply query best practices](advanced-hunting-best-practices)