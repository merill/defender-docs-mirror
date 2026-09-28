---
layout: Conceptual
title: Custom data ingestion and transformation in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/data-transformation
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
description: Learn about how Azure Monitor's custom log ingestion and data transformation features can help you get any data into Microsoft Sentinel and shape it the way you want.
author: guywi-ms
ms.author: guywild
ms.topic: article
ms.date: 2026-08-10T00:00:00.0000000Z
locale: en-us
document_id: 45b0bc79-3d2f-12d4-79c7-0eddee7674a4
document_version_independent_id: e4dfd062-292a-0dff-8911-bd7faa232906
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/data-transformation.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/data-transformation
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/data-transformation.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 34279a80-0988-a983-585c-36536f68fe03
---

# Custom data ingestion and transformation in Microsoft Sentinel | Microsoft Learn

[Azure Monitor Logs](/en-us/azure/azure-monitor/logs/data-platform-logs) serves as the data platform for Microsoft Sentinel. All logs ingested into Microsoft Sentinel are stored in a [Log Analytics workspace](/en-us/azure/azure-monitor/logs/log-analytics-workspace-overview), and [log queries](/en-us/azure/azure-monitor/logs/log-query-overview) written in [Kusto Query Language (KQL)](/en-us/kusto/query/kusto-sentinel-overview?view=microsoft-sentinel&amp;preserve-view=true&amp;toc=%2Fazure%2Fsentinel%2FTOC.json&amp;bc=%2Fazure%2Fsentinel%2Fbreadcrumb%2Ftoc.json) are used to detect threats and monitor your network activity.

Log Analytics gives you a high level of control over the data that gets ingested to your workspace with custom data ingestion and [data collection rules (DCRs)](/en-us/azure/azure-monitor/essentials/data-collection-rule-overview). DCRs allow you to both collect and manipulate your data before it's stored in your workspace. DCRs both format and send data to both standard Log Analytics tables and customizable tables for data sources that produce unique log formats.

Filter and split transformations can be applied to data at ingestion time to reduce noise and route data to the appropriate storage tier. These transformations don't require you to create a DCR and are defined in the Microsoft Sentinel's table management page in the Defender portal. For more information, see [Filter and split transformations in Microsoft Sentinel](transformation-filter-split).

## Azure Monitor tools for custom data ingestion in Microsoft Sentinel

Microsoft Sentinel uses the following Azure Monitor tools to control custom data ingestion:

- [**Transformations**](/en-us/azure/azure-monitor/essentials/data-collection-transformations) are defined in DCRs and apply KQL queries to incoming data before it's stored in your workspace. These transformations can filter out irrelevant data, enrich existing data with analytics or external data, or mask sensitive or personal information.
- The [**Logs ingestion API**](/en-us/azure/azure-monitor/logs/logs-ingestion-api-overview) allows you to send custom-format logs from any data source to your Log Analytics workspace, and store those logs either in certain standard tables, or in custom-formatted tables that you create. You have full control over the creation of these custom tables, down to specifying the column names and types. The API uses [**DCRs**](/en-us/azure/azure-monitor/essentials/data-collection-rule-overview) to define, configure, and apply transformations to these data flows.

Note

If Microsoft Sentinel is enabled for the Log Analytics workspace, transformations to Analytics tables aren't subject to Azure Monitor's [filtering ingestion charge](/en-us/azure/azure-monitor/data-collection/data-collection-transformations#analytics-or-basic-logs), regardless of how much data the transformation filters. This exemption doesn't extend to Basic tables, which incur the filtering charge when a transformation drops more than 50% of the incoming data. Transformations in Microsoft Sentinel otherwise have the same limitations as Azure Monitor. For more information, see [Limitations and considerations](/en-us/azure/azure-monitor/data-collection/data-collection-transformations-create#limitations-and-considerations).

### DCR support in Microsoft Sentinel

Ingestion-time transformations are defined in [data collection rules (DCRs)](/en-us/azure/azure-monitor/essentials/data-collection-rule-overview), which control the data flow in Azure Monitor. DCRs are used by AMA-based Sentinel connectors and workflows using the [Logs ingestion API](/en-us/azure/azure-monitor/logs/logs-ingestion-api-overview). Each DCR contains the configuration for a particular data collection scenario, and multiple connectors or sources can share a single DCR.

[Workspace transformation DCRs](/en-us/azure/azure-monitor/essentials/data-collection-transformations#workspace-transformation-dcr) support workflows that don't otherwise use DCRs. Workspace transformation DCRs contain transformations for any [supported tables](/en-us/azure/azure-monitor/logs/tables-feature-support) and are applied to all traffic sent to that table.

For more information, see:

- [Data collection transformations in Azure Monitor](/en-us/azure/azure-monitor/essentials/data-collection-transformations)
- [Logs ingestion API in Azure Monitor Logs](/en-us/azure/azure-monitor/logs/logs-ingestion-api-overview)
- [Data collection rules in Azure Monitor](/en-us/azure/azure-monitor/essentials/data-collection-rule-overview)

## Use cases and sample scenarios

The article [Sample transformations in Azure Monitor](/en-us/azure/azure-monitor/essentials/data-collection-transformations-samples) provides description and sample queries for common scenarios using ingestion-time transformations in Azure Monitor. Scenarios that are particularly useful for Microsoft Sentinel include:

- [Reduce data costs](/en-us/azure/azure-monitor/essentials/data-collection-transformations-samples#reduce-data-costs). Filter data collection by either rows or columns to reduce ingestion and storage costs.
- [Normalize data](/en-us/azure/azure-monitor/essentials/data-collection-transformations-samples#normalize-data). Normalize logs with the [Advanced Security Information Model (ASIM)](normalization) to improve the performance of normalized queries. For more information, see [Ingest-time normalization](normalization-ingest-time).
- [Enrich data](/en-us/azure/azure-monitor/essentials/data-collection-transformations-samples#enrich-data). Ingestion-time transformations let you improve analytics by enriching your data with extra columns added to the configured KQL transformation. Extra columns might include parsed or calculated data from existing columns.
- [Remove sensitive data](/en-us/azure/azure-monitor/essentials/data-collection-transformations-samples#remove-sensitive-data). Ingestion-time transformations can be used to mask or remove personal information such as masking all but the last digits of a social security number or credit card number.

## Data ingestion flow in Microsoft Sentinel

The following image shows where ingestion-time data transformation enters the data ingestion flow in Microsoft Sentinel. This data can be supported standard tables or in a [specific set of custom tables](/en-us/azure/azure-monitor/logs/tables-feature-support).

[![Diagram of the Microsoft Sentinel data transformation architecture.](media/data-transformation/data-transformation-architecture.png)](media/data-transformation/data-transformation-architecture.png#lightbox)

This image shows the cloud pipeline, which represents the data collection component of Azure Monitor. You can learn more about it along with other data collection scenarios in [Data collection rules (DCRs) in Azure Monitor](/en-us/azure/azure-monitor/essentials/data-collection-rule-overview#azure-monitor-pipeline).

Microsoft Sentinel collects data in the Log Analytics workspace from multiple sources.

- **Data collected from the Logs ingestion API endpoint or Azure Monitor agent (AMA)** is processed by a specific DCR that may include an ingestion-time transformation.
- **Data from built-in data connectors** is processed in Log Analytics using a combination of hardcoded workflows and ingestion-time transformations in the workspace DCR.

The following table describes DCR support for Microsoft Sentinel data connector types:

| Data connector type | DCR support |
| --- | --- |
| [**Azure Monitor agent (AMA) logs**](connect-services-windows-based), such as: - [Windows Security Events via AMA](data-connectors-reference#windows-security-events-via-ama)<br>- [Windows Forwarded Events](data-connectors-reference#windows-forwarded-events)<br>- [CEF data](connect-cef-ama)<br>- [Syslog data](connect-cef-syslog) | One or more DCRs associated with the agent |
| **Direct ingestion via [Logs ingestion API](/en-us/azure/azure-monitor/logs/logs-ingestion-api-overview)** | DCR specified in API call |
| **Built-in, API-based data connector**, such as: - [Codeless data connectors](isv/create-codeless-connector) | DCR created for connector |
| [**Diagnostic settings-based connections**](connect-services-diagnostic-setting-based) | Workspace transformation DCR with [supported output tables](/en-us/azure/azure-monitor/logs/tables-feature-support) |
| **Built-in, API-based data connectors**, such as: - [Legacy codeless data connectors](create-codeless-connector-legacy)<br>- [Azure Functions-based data connectors](connect-azure-functions-template) | Not currently supported |
| **Built-in, service-to-service data connectors**, such as:- [Microsoft Office 365](connect-services-api-based)<br>- [Microsoft Entra ID](connect-azure-active-directory)<br>- [Amazon S3](connect-aws) | Workspace transformation DCR for [tables that support transformations](/en-us/azure/azure-monitor/logs/tables-feature-support) |