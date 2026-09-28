---
layout: Conceptual
title: Microsoft Sentinel MCP server pricing, limits, and availability - Microsoft Security | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/sentinel-mcp-billing
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
ms.subservice: sentinel-platform
search.appverid: met150
description: Learn about the pricing, limits, and availability of using the different MCP collection of tools in Microsoft Sentinel
ms.author: pauloliveria
author: poliveria
ms.reviewer: macasgra
ms.topic: concept-article
ms.date: 2026-05-04T00:00:00.0000000Z
ms.custom: references_regions
locale: en-us
document_id: 10248018-4063-caab-4492-e617eadc2dbd
document_version_independent_id: ad83605e-cf4a-ce87-f07b-99a5f333222a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/sentinel-mcp-billing.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/sentinel-mcp-billing
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/sentinel-mcp-billing.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
platformId: 595de2ce-399b-849f-db4f-5c9a6e75830d
---

# Microsoft Sentinel MCP server pricing, limits, and availability - Microsoft Security | Microsoft Learn

Important

Some information relates to a prerelease product that may be substantially modified before it's released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

This article provides information on pricing, limits, and availability when setting up and using Microsoft Sentinel's Model Context Protocol (MCP) collection of security tools.

## Pricing and billing

### Microsoft Sentinel data lake tools

Microsoft Sentinel pricing is based on the tier that you ingest data into. The **data lake tier** is a cost-effective option for ingesting secondary security data and querying security data over the long term. In this tier, Microsoft Sentinel's unified MCP server interface is offered **at no extra cost**. You pay for invoking tools that search and retrieve data by using Kusto Query Language (KQL) queries from Microsoft Sentinel data lake. With Microsoft Sentinel data lake's billing model, you pay as you go for queries that retrieve data. [Read more about Microsoft Sentinel data lake’s pricing here](../billing#data-lake-tier).

### Microsoft Sentinel entity analyzer tool

You pay for the KQL queries the [entity analyzer](sentinel-mcp-data-exploration-tool#entity-analyzer) performs over the Microsoft Sentinel data lake. You're charged for the [Security Compute Units (SCUs)](/en-us/copilot/security/manage-usage) required to deliver the reasoned entity risk analysis based on prevalence, threat intelligence, and relationships.

### Triage tool

You can use the [triage tool collection](sentinel-mcp-triage-tool) at no extra cost, if you're onboarded to the required products and services.

### Graph tool

Installing and configuring the [graph tool collection](sentinel-mcp-data-exploration-tool#graph-tools-preview) carries no cost. However, you invoke the graph meter when you start using the tools to query a Microsoft Sentinel graph. For more information, see: [Plan costs and understand Microsoft Sentinel pricing and billing](../billing#graph-charges).

## Quotas and limits

### Microsoft Sentinel data lake tools

All [service parameters and limits for Microsoft Sentinel data lake](sentinel-lake-service-limits#service-parameters-and-limits-for-tables-data-management-and-ingestion) also apply when you use Microsoft Sentinel's MCP collection of tools.

The following limits are specific to Microsoft Sentinel data lake MCP tools:

| Feature | Limits |
| --- | --- |
| MCP streaming | 120 seconds |
| Query window for tools | 800 characters |

### Microsoft Sentinel entity analyzer tool

Each tenant can use the entity analyzer MCP tool up to the following limits:

- 200 total runs an hour
- 500 total runs a day
- Around 15 concurrent runs every five minutes (based on available service capacity)

Results generated by the entity analyzer are available for one hour. You need to run a new query after the tool's analysis expires.

### Triage tool

Regular API throttling applies to the tools in the triage tool collection. In addition, tools that call the advanced hunting API are bound by the existing advanced hunting quotas and service limits. [Learn more about advanced hunting quotas and usage parameters](/en-us/defender-xdr/advanced-hunting-limits#understand-advanced-hunting-quotas-and-usage-parameters)

## Language and region availability

Microsoft Sentinel’s collection of MCP tools supports English prompts only. For optimal performance, customers located in the following countries and regions can use Microsoft Sentinel's collection of MCP tools:

- Australia
- Canada
- Europe
- India
- Japan
- Norway
- Southeast Asia
- Switzerland
- United Kingdom
- United States