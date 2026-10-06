---
layout: Conceptual
title: Normalization and the Advanced Security Information Model (ASIM) | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/normalization
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
description: This article explains how Microsoft Sentinel normalizes data from many different sources using the Advanced Security Information Model (ASIM)
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: vakohl
ms.topic: concept-article
ms.date: 2026-09-10T00:00:00.0000000Z
locale: en-us
document_id: 54d58780-a978-3776-469c-10c15f1d322b
document_version_independent_id: fe3df63b-d4cc-be79-b7f0-608d65337c6f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/normalization.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/normalization
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/normalization.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: e4a257be-5365-6d2b-4919-56ec234b6025
---

# Normalization and the Advanced Security Information Model (ASIM) | Microsoft Learn

Microsoft Sentinel ingests data from many sources. Working with various data types and tables together requires you to understand each of them, and write and use unique sets of data for analytics rules, workbooks, and hunting queries for each type or schema.

Sometimes, you'll need separate rules, workbooks, and queries, even when data types share common elements, such as firewall devices. Correlating between different types of data during an investigation and hunting can also be challenging.

The Advanced Security Information Model (ASIM) is a layer that is located between these diverse sources and the user. ASIM follows the [robustness principle](https://en.wikipedia.org/wiki/Robustness_principle): **"Be strict in what you send, be flexible in what you accept"**. Using the robustness principle as design pattern, ASIM transforms the proprietary source telemetry collected by Microsoft Sentinel to user friendly data to facilitate exchange and integration.

This article provides an overview of the Advanced Security Information Model (ASIM), its use cases, and major components.

Tip

Also watch the [ASIM Webinar](https://www.youtube.com/watch?v=WoGD-JeC7ng) or review the [webinar slides](https://1drv.ms/b/s!AnEPjr8tHcNmjDY1cro08Fk3KUj-?e=murYHG).

## Common ASIM usage

ASIM provides a seamless experience for handling various sources in uniform, normalized views, by providing the following functionality:

- **Cross source detection**. Normalized analytics rules work across sources, on-premises and cloud, and detect attacks such as brute force or impossible travel across systems, including Okta, AWS, and Azure.
- **Source agnostic content**. The coverage of both built-in and custom content using ASIM automatically expands to any source that supports ASIM, even if the source was added after the content was created. For example, process event analytics support any source that a customer may use to bring in the data, such as Microsoft Defender for Endpoint, Windows Events, and Sysmon.
- **Support for your custom sources**, in built-in analytics
- **Ease of use**. After an analyst learns ASIM, writing queries is much simpler as the field names are always the same.

### ASIM and the Open Source Security Events Metadata

ASIM aligns with the [Open Source Security Events Metadata (OSSEM)](https://ossemproject.com/intro.html) common information model, allowing for predictable entities correlation across normalized tables.

OSSEM is a community-led project that focuses primarily on the documentation and standardization of security event logs from diverse data sources and operating systems. The project also provides a Common Information Model (CIM) that can be used for data engineers during data normalization procedures to allow security analysts to query and analyze data across diverse data sources.

For more information, see the [OSSEM reference documentation](https://ossemproject.com/cdm/guidelines/entity_structure.html).

## ASIM components

The following image shows how non-normalized data can be translated into normalized content and used in Microsoft Sentinel. For example, you can start with a custom, product-specific, non-normalized table, and use a parser and a normalization schema to convert that table to normalized data. Use your normalized data in both Microsoft and custom analytics, rules, workbooks, queries, and more.

![Diagram showing non-normalized to normalized data conversion flow and usage in Microsoft Sentinel.](media/normalization/asim-architecture.png)

ASIM includes the following components:

### Normalized schemas

Normalized schemas cover standard sets of predictable event types that you can use when building unified capabilities. Each schema defines the fields that represent an event, a normalized column naming convention, and a standard format for the field values.

ASIM currently defines the following schemas:

- [Agent Event](normalization-schema-agent)
- [Alert Event](normalization-schema-alert)
- [Audit Event](normalization-schema-audit)
- [Authentication Event](normalization-schema-authentication)
- [DHCP Activity](normalization-schema-dhcp)
- [DNS Activity](normalization-schema-dns)
- [Email Event](normalization-schema-email)
- [File Activity](normalization-schema-file-event)
- [Network Session](normalization-schema-network)
- [Process Event](normalization-schema-process-event)
- [Registry Event](normalization-schema-registry-event)
- [User Management](normalization-schema-user-management)
- [Web Session](normalization-schema-web)

ASIM also defines the [Asset Entity](normalization-schema-asset) schema for normalizing asset inventories and change feeds.

For more information, see [ASIM schemas](normalization-about-schemas).

### Query time parsers

ASIM uses query time parsers to map existing data to the normalized schemas using [KQL functions](/en-us/kusto/query/functions/user-defined-functions?view=microsoft-sentinel&amp;preserve-view=true). Many ASIM parsers are available out of the box with Microsoft Sentinel. More parsers, and versions of the built-in parsers that can be modified can be deployed from the [Microsoft Sentinel GitHub repository](https://aka.ms/AzSentinelASim).

For more information, see [ASIM parsers](normalization-parsers-overview).

### Ingest time normalization

Query time parsers have many advantages:

- They do not require the data to be modified, thus preserving the source format.
- Since they do not modify the data, but rather presents a view of the data, they are easy to develop. Developing, testing and fixing a parser can all be done on existing data. Moreover, parsers can be fixed when an issue is discovered and the fix will apply to existing data.

On the other hand, while ASIM parsers are optimized, query time parsing can slow down queries, especially on large data sets. To resolve this, Microsoft Sentinel complements query time parsing with ingest time parsing. Using ingest transformation the events are normalized to normalized table, accelerating queries that use normalized data.

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

For more information, see [Ingest Time Normalization](normalization-ingest-time).

### Content for each normalized schema

Content which uses ASIM includes solutions, analytics rules, workbooks, hunting queries, and more. Content for each normalized schema works on any normalized data without the need to create source-specific content.

For more information, see [ASIM content](normalization-content).

## Getting started with ASIM

To start using ASIM:

- Deploy an ASIM based domain solution such as the [Network Threat Protection Essentials](https://azuremarketplace.microsoft.com/marketplace/apps/azuresentinel.azure-sentinel-solution-networkthreatdetection?tab=Overview) domain solution.
- Activate analytics rule templates that use ASIM. For more information, see the [ASIM content list](normalization-content#builtin).
- Use the ASIM hunting queries from the Microsoft Sentinel GitHub repository, when querying logs in KQL in the Microsoft Sentinel **Logs** page. For more information, see the [ASIM content list](normalization-content#builtin).
- Write your own analytics rules using ASIM or [convert existing ones](normalization-content#builtin).
- Enable your custom data to use built-in analytics by [writing parsers](normalization-develop-parsers) for your custom sources and [adding](normalization-manage-parsers) them to the relevant source agnostic parser.