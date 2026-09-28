---
layout: Conceptual
title: Ingest time normalization | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/normalization-ingest-time
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
description: This article explains how Microsoft Sentinel normalizes data at ingest
ms.author: edbaynash
author: EdB-MSFT
ms.topic: concept-article
ms.date: 2022-12-28T00:00:00.0000000Z
locale: en-us
document_id: 1e93db86-2130-1d5f-9b6c-7e231ee383b5
document_version_independent_id: 2e402ef3-1265-f51b-a77a-53abb03e95e3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/normalization-ingest-time.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/normalization-ingest-time
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/normalization-ingest-time.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: e275d878-511c-ec14-a269-0771cc43afb1
---

# Ingest time normalization | Microsoft Learn

## Query time parsing

As discussion in the [ASIM overview](normalization), Microsoft Sentinel uses both query time and ingest time normalization to take advantage of the benefits of each.

To use query time normalization, use the [query time unifying parsers](normalization-about-parsers#unifying-parsers), such as `_Im_Dns` in your queries. Normalizing using query time parsing has several advantages:

- **Preserving the original format**: Query time normalization doesn't require the data to be modified, thus preserving the original data format sent by the source.
- **Avoiding potential duplicate storage**: Since the normalized data is only a view of the original data, there's no need to store both original and normalized data.
- **Easier development**: Since query time parsers present a view of the data and don't modify the data, they're easy to develop. Developing, testing, and fixing a parser can all be done on existing data. Moreover, parsers can be fixed when an issue is discovered, and the fix is applied to existing data.

## Ingest time parsing

While ASIM query time parsers are optimized, query time parsing can slow down queries, especially on large data sets.

Ingest time parsing enables transforming events to a normalized schema as they are ingested into Microsoft Sentinel and storing them in a normalized format. Ingest time parsing is less flexible and parsers are harder to develop, but since the data is stored in a normalized format, offers better performance.

Normalized data can be stored in Microsoft Sentinel's native normalized tables, or in a custom table that uses an ASIM schema. A custom table that has a schema close to, but not identical, to an ASIM schema, also provides the performance benefits of ingest time normalization.

Currently, ASIM supports the following native normalized tables as a destination for ingest time normalization:

- [**ASimAuditEventLogs**](/en-us/azure/azure-monitor/reference/tables/asimauditeventlogs) for the [Audit Event](normalization-schema-audit) schema.
- [**ASimAuthenticationEventLogs**](/en-us/azure/azure-monitor/reference/tables/asimauthenticationeventlogs) for the [Authentication](normalization-schema-authentication) schema.
- [**ASimDhcpEventLogs**](/en-us/azure/azure-monitor/reference/tables/asimdhcpeventlogs) for the [DHCP Event](normalization-schema-dhcp) schema.
- [**ASimDnsActivityLogs**](/en-us/azure/azure-monitor/reference/tables/asimdnsactivitylogs) for the [DNS](normalization-schema-dns) schema.
- [**ASimFileEventLogs**](/en-us/azure/azure-monitor/reference/tables/asimfileeventlogs) for the [File Event](normalization-schema-file-event) schema.
- [**ASimNetworkSessionLogs**](/en-us/azure/azure-monitor/reference/tables/asimnetworksessionlogs) for the [Network Session](normalization-schema-network) schema.
- [**ASimProcessEventLogs**](/en-us/azure/azure-monitor/reference/tables/asimprocesseventlogs) for the [Process Event](normalization-schema-process-event) schema.
- [**ASimRegistryEventLogs**](/en-us/azure/azure-monitor/reference/tables/asimregistryeventlogs) for the [Registry Event](normalization-schema-registry-event) schema.
- [**ASimUserManagementActivityLogs**](/en-us/azure/azure-monitor/reference/tables/asimusermanagementactivitylogs) for the [User Management](normalization-schema-user-management) schema.
- [**ASimWebSessionLogs**](/en-us/azure/azure-monitor/reference/tables/asimwebsessionlogs) for the [Web Session](normalization-schema-web) schema.

The advantage of native normalized tables is that they're included by default in the ASIM unifying parsers. Custom normalized tables can be included in the unifying parsers, as discussed in [Manage Parsers](normalization-manage-parsers).

## Combining ingest time and query time normalization

Queries should always use the [query time unifying parsers](normalization-about-parsers#unifying-parsers), such as `_Im_Dns` to take advantage of both query time and ingest time normalization. Native normalized tables are included in the queried data by using a stub parser.

The stub parser is a query time parser that uses as input the normalized table. Since the normalized table doesn't require parsing, the stub parser is efficient.

The stub parser presents a view to the calling query that adds to the ASIM native table:

- **Aliases** - in order to not waste storage on repeating values, aliases are not stored in ASIM native tables and are added at query time by the stub parsers.
- **Constant values** - Like aliases, and for the same reason, ASIM normalized tables also don't store constant values such as [EventSchema](normalization-common-fields#eventschema). The stub parser adds those fields. ASIM normalized table is shared by many sources, and ingest time parsers can change their output version. Therefore, fields such as [EventProduct](normalization-common-fields#eventproduct), [EventVendor](normalization-common-fields#eventvendor), and [EventSchemaVersion](normalization-common-fields#eventschemaversion) are not constant and are not added by the stub parser.
- **Filtering** - the stub parser also implements filtering. While ASIM native tables don't need filtering parsers to achieve better performance, filtering is needed to support inclusion in the unifying parser.
- **Updates and fixes** - Using a stub parser enables fixing issues faster. For example if data was ingested incorrectly, an IP address might not have been extracted from the message field during ingest. The IP address can be extracted by the stub parser at query time.

When using custom normalized tables, create your own stub parser to implement this functionality, and add it to the unifying parsers as discussed in [Manage Parsers](normalization-manage-parsers). Use the stub parser for the native table, such as the [DNS native table stub parser](https://github.com/Azure/Azure-Sentinel/blob/master/Parsers/ASimDns/Parsers/ASimDnsNative.yaml) and its [filtering counterpart](https://github.com/Azure/Azure-Sentinel/blob/master/Parsers/ASimDns/Parsers/vimDnsNative.yaml), as a starting point. If your table is semi-normalized, use the stub parser to perform the additional parsing and normalization needed.

Learn more about writing parsers in [Developing ASIM parsers](normalization-develop-parsers).

## Implementing ingest time normalization

To normalize data at ingest, you need to use a [Data Collection Rule (DCR)](/en-us/azure/azure-monitor/essentials/data-collection-rule-overview). The procedure for implementing the DCR depends on the method used to ingest the data. For more information, see the article [Transform or customize data at ingestion time in Microsoft Sentinel](configure-data-transformation).

A [KQL](/en-us/kusto/query/?toc=/azure/sentinel/TOC.json&amp;bc=/azure/sentinel/breadcrumb/toc.json) transformation query is the core of a DCR. The KQL version used in DCRs is slightly different than the version used elsewhere in Microsoft Sentinel to accommodate for requirements of pipeline event processing. Therefore, you need to modify any query-time parser to use it in a DCR. For more information on the differences, and how to convert a query-time parser to an ingest-time parser, read about the [DCR KQL limitations](/en-us/azure/azure-monitor/essentials/data-collection-transformations-structure#kql-limitations).