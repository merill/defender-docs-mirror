---
layout: Conceptual
title: Microsoft Sentinel SIEM solution quality guidelines | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/isv/sentinel-siem-solution-quality-guidance
breadcrumb_path: ../breadcrumb/toc.json
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
description: Learn quality requirements and best practices to build, publish, and maintain Microsoft Sentinel SIEM solutions that deliver immediate customer value.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: 
ms.topic: concept-article
ms.date: 2026-06-02T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1012
ai-usage: ai-assisted
locale: en-us
document_id: eb10339e-2551-19f2-2ffb-7e2a49762003
document_version_independent_id: d9e4b285-0626-aa91-844c-1ea33ed0b6ee
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/isv/sentinel-siem-solution-quality-guidance.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/isv/sentinel-siem-solution-quality-guidance
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/isv/sentinel-siem-solution-quality-guidance.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/3439c05e-99ce-45d1-b266-9322ea647316
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/23472108-2f8d-47d2-b07a-c0b1e9d492b6
platformId: e654b808-6edc-8886-31f5-755342352c52
---

# Microsoft Sentinel SIEM solution quality guidelines | Microsoft Learn

Use these guidelines to build Microsoft Sentinel SIEM solutions that deliver value as soon as customers install them.

## SIEM solution components

A Microsoft Sentinel SIEM solution consists of multiple content items, each serving a specific purpose.

This section describes requirements for each content type that can be included in a Sentinel SIEM solution.

## Data connectors

Use the Codeless Connector Framework (CCF) to create data connectors. CCF lets partners, advanced users, and developers create custom connectors for Microsoft Sentinel without deploying service infrastructure. CCF includes health monitoring, Microsoft Sentinel support, and automatic scaling to support changing ingestion volume. Customers configure ingestion in a guided UI and pay only for ingested data. For more information on CCF connectors, see [Create a codeless connector for Microsoft Sentinel](/en-us/azure/sentinel/create-codeless-connector)

Important

Partners are required to use the Codeless Connector Framework (CCF), instead of Azure Functions, for all new data connectors. If you find blockers during data connector development because of CCF limitations, log an issue titled **CCF Limitations** in the [Azure-Sentinel GitHub repository](https://github.com/Azure/Azure-Sentinel/issues). The Microsoft Sentinel team works with you to resolve the issue or provide a workaround. If the issue remains a blocker, the Microsoft Sentinel team can create an exception for your data connector. To contact the Microsoft Sentinel team for assistance, email Microsoft Sentinel Partners at AzureSentinelPartner@microsoft.com.

## Analytics rules

Analytics rules must include appropriate MITRE mappings so customers can monitor and visualize threat coverage in their security infrastructure. For more information, see [View MITRE coverage for your organization from Microsoft Sentinel](/en-us/azure/sentinel/mitre-coverage?tabs=azure-portal).

Scope rules to cover key data columns that each data connector pulls. This helps customers see value from ingested data.

Map entities to rule output where applicable. Standardized entities help correlate output with other Microsoft Sentinel data points. Common entities include user accounts, hosts, mailboxes, IP addresses, files, cloud applications, processes, and URLs. For more information, see [Entities in Microsoft Sentinel](/en-us/azure/sentinel/entities).

Important

Partners must create at least one analytics rule as part of their Microsoft Sentinel SIEM solution.

Analytics rules are central to SIEM value. Ingestion is only the first step. Customers need detections to monitor their environment and receive actionable alerts. Include prebuilt analytics rules so customers can start monitoring right after setup.

## Playbooks

A playbook is an Azure Logic App that runs automated response actions when a Microsoft Sentinel incident or alert is triggered. Playbooks help SOC analysts automate tactical tasks such as notifying teams, blocking users, or enriching incidents with external data, so analysts can focus on deeper investigation and response. As you design your solution, identify automated actions that can resolve incidents created by your analytics rules. For more information, see [Automate response with playbooks in Microsoft Sentinel](/en-us/azure/sentinel/automation/automate-responses-with-playbooks).

## Hunting queries

Hunting queries aren't required, but Microsoft strongly recommends including them. Hunting queries help SOC analysts understand the schema and build new investigation scenarios.

When you build hunting queries, use these best practices:

- **Use MITRE mappings** to align queries with common tactics, techniques, and procedures (TTPs).
- **Cover key connector columns** so queries remain useful and highlight data gaps.
- **Use threat intelligence context** to improve analyst decisions. For more information, see [Threat intelligence in Microsoft Sentinel](/en-us/azure/sentinel/understand-threat-intelligence).

## Parsers

Review available ASIM schemas and map your data to one or more relevant schemas. This speeds onboarding for SOC analysts and helps existing ASIM-based content work with your product data. For more information, see [Advanced Security Information Model (ASIM) schemas](/en-us/azure/sentinel/normalization-about-schemas).

ASIM supports two approaches to normalization:

- Ingest-time normalization: Data is normalized as it arrives and written directly to a dedicated ASIM table, such as ASimDnsActivityLogs or ASimAuthenticationEventLogs. This approach improves query performance because data is already in normalized form when queried. If your CCF connector writes to one of these native ASIM tables, no additional parser is needed.
- Query-time parsers: Data is stored in its original form (for example, in CommonSecurityLog or a custom table), and a KQL function transforms it into the normalized schema at query time. These are the source-specific parsers named `_Im_<schema>_<source>`. The unifying parser `_Im_<schema>` automatically includes both native ASIM table data and all source-specific query-time parsers.

Microsoft Sentinel provides many built-in source-specific parsers. You might need to modify or create parsers when:

- Your device events fit an ASIM schema, but no source-specific parser exists for that schema.
- A source-specific parser exists, but your device sends events in a different format.
- Your source device is configured to send nonstandard events. -To understand parser placement in ASIM architecture, see the ASIM architecture diagram.

Note

Microsoft doesn't mandate the availability of parsers in your solution. However if our certification team identifies that your data maps closely to an existing ASIM schema, our team may mandate the creation of parsers to avail the benefits of normalization.

## Workbooks

Workbooks aren't required because requirements vary by use case. If you include workbooks, ensure each workbook aligns with ingested data and delivers customer value.

When you create workbooks, use these best practices:

- **Use clear titles and descriptions** so users quickly understand each workbook purpose.
- **Use appropriate visualizations** such as line charts for trends, bar charts for comparisons, and tables for detail.
- **Use filters and parameters** so users can focus on relevant time ranges and sources.
- **Optimize performance** by using summary rules when workbook queries process large volumes of data.
- **Provide built-in guidance** through documentation or tooltips.

## Maintaining solutions

After publication, maintain and update your SIEM solution regularly:

- **Plan for feature deprecations** and update at least six months before end-of-life or end-of-service milestones.
- **Keep the solution description page accurate** and fix broken links quickly.
- **Address GitHub CodeQL alerts** in a timely manner.