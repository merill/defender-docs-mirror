---
layout: Conceptual
title: Data federation overview in Microsoft Sentinel data lake - Microsoft Security | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/data-federation-overview
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
description: Learn how data federation in Microsoft Sentinel data lake enables seamless querying of external data sources including Azure Databricks, ADLS Gen 2, and Microsoft Fabric.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: sourinpaul
ms.topic: concept-article
ms.date: 2026-07-29T00:00:00.0000000Z
ms.collection: ms-security
locale: en-us
document_id: 1464d7f7-c2bc-1759-28f6-3cb5c4891b73
document_version_independent_id: 0e80e97d-8ae4-4049-15f7-6d95ec3eeaad
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/data-federation-overview.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/data-federation-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/data-federation-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
- https://authoring-docs-microsoft.poolparty.biz/devrel/5c1f3bfc-fced-4ad1-b4e6-b7200832734d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
- https://authoring-docs-microsoft.poolparty.biz/devrel/5017978e-5a12-4c31-bdfd-1880eb1a780b
platformId: c93acc8a-60b4-2cd8-29f4-00b9b37e906f
---

# Data federation overview in Microsoft Sentinel data lake - Microsoft Security | Microsoft Learn

Data federation in Microsoft Sentinel enables seamless querying of multiple external data sources from within the Microsoft Sentinel data lake environment. By federating data sources such as Azure Databricks, Azure Data Lake Storage (ADLS) Gen 2, and Microsoft Fabric, organizations can enhance their security analytics and operational insights without moving or duplicating data.

## What is data federation?

Data federation allows you to query external data sources directly from the Microsoft Sentinel data lake using Kusto Query Language (KQL) or Jupyter notebooks using the Microsoft Sentinel Visual Studio Code extension. Instead of ingesting the data into Sentinel, federation creates connections to external data stores, enabling:

- **Unified analytics**: Query federated sources alongside native Microsoft Sentinel data lake tables.
- **Preserve governance and compliance controls**: Maintain data security and compliance by querying data in place without moving it.
- **Enhanced insights**: Combine security data with business data, logs, or other datasets stored in external systems.
- **Flexible data access**: Access historical or specialized datasets that complement your security operations.

Important

Data federation is one-directional from the Sentinel data lake to the federated target. You can query a federated source from the data lake, but you can't access the data lake from a federated source.

## Available federation sources

The following federation sources are available:

| Source | Description |
| --- | --- |
| **Azure Databricks** | Connect to Databricks Unity Catalog tables and query data from Sentinel. |
| **Azure Data Lake Storage Gen 2** | Query data stored in ADLS Gen 2 storage accounts directly from the Sentinel data lake. |
| **Microsoft Fabric** | Connect to Microsoft Fabric Lakehouse tables for integrated analytics. |

## Key concepts

### Federated connections

A federated connection is a configured link between the Sentinel data lake and an external data source. Each connection specifies:

- The target data source (Databricks, ADLS Gen 2, or Fabric).
- Authentication credentials stored securely in Azure Key Vault for ADLS and Azure Databricks.
- The specific tables to federate.

### Federated tables

Federated tables are tables that come from a federated connection. Federated tables appear in the Sentinel data lake **Table Management** page and can be queried like native tables. Federated table names follow the pattern `<tableName>_<connectorInstanceName>`. For example, if your connector instance is named `ADLS01` and you federate with a table named `widgets`, the federated table name is `widgets_ADLS01`.

### Connector instances

Each configured connection to an external data source is called a connector instance. You can create multiple instances for the same federation source type, each connecting to different external resources.

## Prerequisites

Before setting up data federation, ensure you meet the following requirements:

- Sentinel data lake onboarding: Your tenant must be onboarded to the Sentinel data lake. For more information, see [Onboard to Microsoft Sentinel data lake](sentinel-lake-onboard-defender).
- Public accessibility: The external source must be publicly accessible. Private endpoints aren't supported currently.
- Data format: The external source tables must be in delta parquet format.
- Service principal: A service principal with appropriate permissions in the data source you want to connect with is required for Azure Databricks and Azure Data Lake Storage Gen2 sources.
- Azure Key Vault: An Azure Key Vault to store authentication secrets for the service principal. You need to configure permissions for Microsoft Sentinel managed identity to read secrets from the key vault.

## How federation works

1. **Configure authentication**: Create a service principal and store its credentials in Azure Key Vault.
2. **Create a federated connection**: Use the Data connectors page in Microsoft Sentinel to create a connector instance for your chosen data federation source.
3. **Select tables**: Choose which tables from the external source to federate.
4. **Query federated data**: Use data lake experiences such as KQL queries, Notebooks, or MCP tools to access federated tables alongside native Sentinel data.

## Common scenarios for data federation

Data federation lets you access data that resides outside of the data lake. This is especially valuable in the following scenarios:

- Data sources that are operationalized across multiple teams and systems.
- Years of historical data that you want to naturally age out and isn't cost effective to ingest.
- Regional or compliance regulations that constrain data from being copied.
- Data that isn't frequently accessed and is only contextually relevant in limited scenarios.

## Benefits of data federation

### Unified security analytics

Combine security event data in Sentinel with context from external sources, such as:

- Analytics outputs from Databricks
- Historical logs stored in ADLS Gen 2
- Business application data from Microsoft Fabric

### Operational flexibility

- Access data across organizational boundaries
- Integrate data from different teams or business units
- Support complex investigations that span multiple data sources

## Limitations

- Data sources must be publicly accessible. Private endpoints aren't supported.
- Azure Key Vault networking needs to be set for **Allow public access from all networks**, which is the default for Key Vault, during configuration of ADLS or Azure Databricks connection instances. Once you complete creating or editing a connection, the associated Key Vault can have a different networking setting configured.
- Federated connections to Microsoft Fabric support schema-enabled lakehouses, where workspaces aren't enabled for outbound access protection.
- Federated connections to Azure Databricks support hybrid workspace; serverless workspaces are not supported.
- Data federation is read-only; you can't write data back to federated sources.
- Query performance depends on the external source's responsiveness and data volume.
- Federated connections to a Fabric source can have a maximum of 100 tables within the connection instance.
- You can have a maximum of 100 connector instances. Azure Databricks and ADLS use one connector instance per federated connection. Microsoft Fabric uses one connector instance per lakehouse schema in a federated connection.