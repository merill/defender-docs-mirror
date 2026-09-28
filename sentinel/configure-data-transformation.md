---
layout: Conceptual
title: Transform or customize data at ingestion time in Microsoft Sentinel (preview) | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/configure-data-transformation
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
description: Learn about how to configure Azure Monitor's ingestion-time data transformation for use with Microsoft Sentinel.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 20af570c-ac49-69fc-a336-e4918dc41c2f
document_version_independent_id: da7651c5-76cf-7c49-01d8-0ba0edc8f4aa
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/configure-data-transformation.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/configure-data-transformation
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/configure-data-transformation.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/4e834929-0ce1-4c1d-9c81-fcb14721edfb
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/75670257-a3f0-4627-9981-8046f99219e6
platformId: 3efa5e6d-6071-c1db-cf1c-947bf99f0fa5
---

# Transform or customize data at ingestion time in Microsoft Sentinel (preview) | Microsoft Learn

This article describes how to configure [ingestion-time data transformation and custom log ingestion](data-transformation) for use in Microsoft Sentinel.

Ingestion-time data transformation provides customers with more control over the ingested data. Supplementing the pre-configured, hardcoded workflows that create standardized tables, ingestion time-transformation adds the capability to filter and enrich the output tables, even before running any queries. Custom log ingestion uses the Custom Log API to normalize custom-format logs so they can be ingested into certain standard tables, or alternatively, to create customized output tables with user-defined schemas for ingesting these custom logs.

These two mechanisms are configured using Data Collection Rules (DCRs), either in the Log Analytics portal, or via API or ARM template. This article will help you choose which kind of DCR you need for your particular data connector, and direct you to the instructions for each scenario.

## Prerequisites

Before you start configuring DCRs for data transformation:

- **Learn more about data transformation and DCRs in Azure Monitor and Microsoft Sentinel**. For more information, see:

    - [Data collection rules in Azure Monitor](/en-us/azure/azure-monitor/essentials/data-collection-rule-overview)
    - [Logs ingestion API in Azure Monitor Logs (Preview)](/en-us/azure/azure-monitor/logs/logs-ingestion-api-overview)
    - [Transformations in Azure Monitor Logs (preview)](/en-us/azure/azure-monitor/essentials/data-collection-transformations)
    - [Data transformation in Microsoft Sentinel (preview)](data-transformation)
- **Verify data connector support**. Make sure that your data connectors are supported for data transformation.

    In our [data connector reference](data-connectors-reference) article, check the section for your data connector to understand which types of DCRs are supported. Continue in this article to understand how the DCR type you select affects the remaining steps to configure and transform your data.

## Determine your requirements

Use the following table to determine which DCR type you need based on your ingestion scenario.

| If you are ingesting | Ingestion-time transformation is... | Use this DCR type |
| --- | --- | --- |
| **Custom data** through the [**Log Ingestion API**](/en-us/azure/azure-monitor/logs/logs-ingestion-api-overview) | - Required<br>- Included in the DCR that defines the data model | Standard DCR |
| **Built-in data types**(Syslog, CommonSecurityLog, WindowsEvent, SecurityEvent) using the Azure Monitor Agent | - Optional<br>- If desired, added to the DCR that configures how this data is being ingested | Standard DCR |
| **Built-in data types**from most other sources | - Optional<br>- If desired, added to the DCR attached to the Workspace where this data is being ingested | Workspace transformation DCR |

## Configure your data transformation

Use the following procedures from the Log Analytics and Azure Monitor documentation to configure your data transformation DCRs.

### Direct ingestion through the Log Ingestion API

For [direct ingestion through the Log Ingestion API](/en-us/azure/azure-monitor/logs/logs-ingestion-api-overview), use the following tutorials:

- Walk through a tutorial for [ingesting logs using the Azure portal](/en-us/azure/azure-monitor/logs/tutorial-logs-ingestion-portal).
- Walk through a tutorial for [ingesting logs using Azure Resource Manager (ARM) templates and REST API](/en-us/azure/azure-monitor/logs/tutorial-logs-ingestion-api).

### Workspace transformations

For [workspace transformations](/en-us/azure/azure-monitor/essentials/data-collection-transformations-workspace), use the following tutorials:

- Walk through a tutorial for [configuring workspace transformation using the Azure portal](/en-us/azure/azure-monitor/logs/tutorial-workspace-transformations-portal).
- Walk through a tutorial for [configuring workspace transformation using Azure Resource Manager (ARM) templates and REST API](/en-us/azure/azure-monitor/logs/tutorial-workspace-transformations-api).

### Data collection rule structure and transformation reference

For more information, see [data collection rules](/en-us/azure/azure-monitor/essentials/data-collection-rule-overview):

- [Structure of a data collection rule in Azure Monitor (preview)](/en-us/azure/azure-monitor/essentials/data-collection-rule-structure)
- [Data collection transformations in Azure Monitor (preview)](/en-us/azure/azure-monitor/essentials/data-collection-transformations)

After you complete a Log Ingestion API or workspace transformation DCR configuration procedure, return to Microsoft Sentinel to verify that your data is being ingested based on the transformation you configured. It may take up to 60 minutes for the data transformation configurations to apply.

## Migrate to ingestion-time data transformation

If you currently have custom Microsoft Sentinel data connectors, or built-in, API-based data connectors, you may want to migrate to using ingestion-time data transformation.

Use one of the following methods:

- Configure a DCR to define, from scratch, the custom ingestion from your data source to a new table. You might use this option if you want to use a new schema that doesn't have the current column suffixes, and doesn't require query-time Kusto Query Language (KQL) functions to standardize your data.

    Warning

    Deleting the legacy table and custom data connector is irreversible and might affect existing queries, workbooks, or integrations that reference them.

    After you've verified that your data is properly ingested to the new table, you can delete the legacy table, as well as your legacy, custom data connector.
- Continue using the custom table created by your custom data connector. You might use this option if you have a lot of custom security content created for your existing table. In such cases, see [Migrate from Data Collector API and custom fields-enabled tables to DCR-based custom logs](/en-us/azure/azure-monitor/logs/custom-logs-migrate) in the Azure Monitor documentation.