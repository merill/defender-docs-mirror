---
layout: Conceptual
title: Use Advanced Security Information Model (ASIM) parsers | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/normalization-about-parsers
breadcrumb_path: breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
ms.reviewer: ofshezaf
description: This article explains how to use Kusto Query Language (KQL) functions as query-time parsers to implement the Advanced Security Information Model (ASIM)
ms.author: edbaynash
author: EdB-MSFT
ms.topic: concept-article
ms.date: 2026-10-07T00:00:00.0000000Z
locale: en-us
document_id: 02c4e393-775d-e665-7b81-2c6d8bc45ce9
document_version_independent_id: 89fa9f69-c787-f12b-d4a3-203d04f638ac
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/normalization-about-parsers.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/normalization-about-parsers
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/normalization-about-parsers.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/26e1a60c-4ce1-41de-b2d1-e5f3b7e68e6e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c6f99e62-1cf6-4b71-af9b-649b05f80cce
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad3bd485-5ca9-4865-afde-baec02586899
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3f56b378-07a9-4fa1-afe8-9889fdc77628
platformId: 26f9b0fe-eebc-2272-a9f5-0f9a59358f1f
---

# Use Advanced Security Information Model (ASIM) parsers | Microsoft Learn

Use Advanced Security Information Model (ASIM) parsers instead of table names in your Microsoft Sentinel queries to view data in a normalized format and to include all data relevant to the schema in your query. Refer to the table below to find the relevant parser for each schema.

## Unifying parsers

When using ASIM in your queries, use **unifying parsers** to combine all sources, normalized to the same schema, and query them using normalized fields. The unifying parser name is `_Im_<schema>`, where `<schema>` stands for the specific schema it serves.

For example, the following query uses the built-in unifying DNS parser to query DNS events using the `ResponseCodeName`, `SrcIpAddr`, and `TimeGenerated` normalized fields:

```kusto
_Im_Dns(starttime=ago(1d), responsecodename='NXDOMAIN')
  | summarize count() by SrcIpAddr, bin(TimeGenerated,15m)
```

The example uses filtering parameters, which improve ASIM performance. The same example without filtering parameters would look like this:

```kusto
_Im_Dns
  | where TimeGenerated > ago(1d)
  | where ResponseCodeName =~ "NXDOMAIN"
  | summarize count() by SrcIpAddr, bin(TimeGenerated,15m)
```

The following table lists the available unifying parsers:

| Schema | Unifying parser |
| --- | --- |
| Agent Event | \_Im\_AgentEvent |
| Alert Event | \_Im\_AlertEvent |
| Asset Entity | \_Im\_AssetEntity |
| Audit Event | \_Im\_AuditEvent |
| Authentication | \_Im\_Authentication |
| DHCP Event | \_Im\_DhcpEvent |
| Dns | \_Im\_Dns |
| Email Event | \_Im\_EmailEvent |
| File Event | \_Im\_FileEvent |
| Network Session | \_Im\_NetworkSession |
| Process Event | \_Im\_ProcessEvent\_Im\_ProcessCreate\_Im\_ProcessTerminate |
| Registry Event | \_Im\_RegistryEvent |
| User Management | \_Im\_UserManagement |
| Web Session | \_Im\_WebSession |

## Optimizing parsing using parameters

Using parsers might affect your query performance, primarily from filtering the results after parsing. For this reason, many parsers have optional filtering parameters, which enable you to filter before parsing and enhance query performance. With query optimization and prefiltering efforts, ASIM parsers often provide better performance when compared to not using normalization at all.

When invoking the parser, always use available filtering parameters by adding one or more named parameters to ensure optimal performance of the ASIM parsers.

Each schema has a standard set of filtering parameters documented in the relevant schema documentation. Filtering parameters are entirely optional.

For an example of using filtering parsers, see Unifying parsers.

## The pack parameter

To ensure efficiency, parsers maintain only normalized fields. Fields that aren't normalized have less value when combined with other sources. Some parsers support the *pack* parameter. When the *pack* parameter is set to `true`, the parser will pack extra data into the *AdditionalFields* dynamic field.

The [parsers list](normalization-parsers-list) article notes parsers that support the *pack* parameter.