---
layout: Conceptual
title: Use Federated Data Sources in Microsoft Sentinel - Microsoft Security | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/using-data-federation
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
description: Learn how to view, query, and work with federated data sources in Microsoft Sentinel data lake using the portal, KQL queries, and Jupyter notebooks.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: amyhari
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: ms-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 1bae895c-a826-1708-ea20-acbef4bcae76
document_version_independent_id: 12258c7e-8e20-b168-3b04-2c3ba461108e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/using-data-federation.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/using-data-federation
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/using-data-federation.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
platformId: 84edac41-001a-661d-34d7-c1f83182449f
---

# Use Federated Data Sources in Microsoft Sentinel - Microsoft Security | Microsoft Learn

After setting up federated data connectors, you can access your federated tables through multiple interfaces in Microsoft Sentinel. Federated tables are used in the same way as other data lake tables. This article explains how to view federated tables, query them using KQL (Kusto Query Language), and work with them in Jupyter notebooks.

## Prerequisites

Before you begin, ensure:

- Your tenant must be onboarded to the Sentinel data lake. For more information, see [Onboard to Microsoft Sentinel data lake](sentinel-lake-onboard-defender)
- You have appropriate permissions to query data in the Sentinel data lake. For more information,see [Roles and permissions in the Microsoft Sentinel platform](../roles#microsoft-sentinel-data-lake-read-permissions).

## Understand federated table naming

Federated table names follow the pattern `<tableName>_<connectorInstanceName>`. For example:

| Original table name | Connector instance name | Federated table name |
| --- | --- | --- |
| `widgets` | `ADLS01` | `widgets_ADLS01` |
| `sales_data` | `AzureDBX01` | `sales_data_AzureDBX01` |
| `inventory` | `Fabric01` | `inventory_Fabric01` |

If multiple tables in the connector instance have the same table name, a numerical identifier is appended to the connector instance name, for example `widgets_ADLS01_1` when two tables within the `ADLS01` connector instance are called `widgets`.

Use the federated table name when querying data from the Sentinel data lake.

## View federated tables in table management

The table management view provides an overview of all tables in your Sentinel data lake, including federated tables.

1. Navigate to **Microsoft Sentinel** &gt; **Configuration** &gt; **Tables**.
2. Select the **Type** filter.
3. Select **Federated** and select **Apply**.

[![Screenshot showing the table management view filtered to show federated tables.](media/using-data-federation/defender-portal-federated-tables.png)](media/using-data-federation/defender-portal-federated-tables.png#lightbox)

### View table details

Select a table row to open the details panel. The table details panel contains three tabs:

| Tab | Description |
| --- | --- |
| **Overview** | Basic information about the federated table, including the source type and connection status. |
| **Data Sources** | Shows which connector instances provide data for this table. |
| **Schema** | Displays the columns, data types, and descriptions for the table's columns. Users with permissions to write to the data lake System tables can select **Refresh schema** to update columns and other schema metadata from the source. |

[![Screenshot showing the federated table details flyout with overview, data sources, and schema tabs.](media/using-data-federation/federated-table-details.png)](media/using-data-federation/federated-table-details.png#lightbox)

## Query federated tables using KQL

The KQL queries page in Microsoft Sentinel allows you to query federated tables alongside native Sentinel data. Federated tables are supported for KQL jobs, interactive and async queries, and MCP tools.

1. Navigate to **Microsoft Sentinel** &gt; **Data lake exploration** &gt; **KQL queries**.
2. Select the **Selected workspace** button in the information bar.
3. Select **System Tables** as one of the workspaces.
4. In the **Schema** tab, expand the **System tables** section.
5. Expand the **Federated tables** section.
6. Find the federation type for your data source, such as Microsoft Fabric, Azure Databricks, or Azure Data Lake Storage Gen2.
7. Expand the federation type to see your federated tables.
8. Expand a table to view its columns.

Note

Due to query performance optimization in KQL, it can take up to 15 minutes for new data in a federated table to become available for query.

[![Screenshot showing the KQL queries schema tab with federated tables expanded.](media/using-data-federation/kql-schema-federated.png)](media/using-data-federation/kql-schema-federated.png#lightbox)

### Write and execute queries

Queries against federated tables work like queries against native lake tables with a few important differences:

- It's possible for a change to occur to the schema of a table in the external source. This can result in a failure during a query that indicates a column isn’t present. Refresh columns on Table management page by selecting the federated table, selecting the **Schema** tab and selecting **Refresh Schema**.
- Federated tables without a `TimeGenerated` column, or where a `TimeGenerated` column is present with data in the wrong format, can't be used in data lake explorer to select time ranges using the time picker in the user interface. Define date filters in the body of the KQL that match your federated table's date format.

### Create KQL jobs from federated queries

You can create KQL jobs based on queries that use federated tables:

1. Write and test your KQL query using federated tables.
2. Select the **Create job** button in the upper right corner of the query panel.
3. Configure the job settings, including schedule and output destination.
4. Save the job.

Note

- Writing data to a federated table isn't supported. KQL output is created based on the same criteria used today when creating a KQL job, where it can write out to a new or existing table based on your selected destination.
- If federated tables don't contain `TimeGenerated` columns, or your output doesn’t contain a `TimeGenerated` column with a properly formatted date value for each row, KQL queries won't function on the table once its created in the lake.

Federated tables are fully supported for KQL jobs, async queries, and MCP tools.

## Create an MCP tool with federated table queries

You can create MCP tools based on queries that use federated tables:

1. Write and test your KQL query using federated tables.
2. Select the **Save as tool** button above the query editor.
3. Adjust the query as needed, for example, parameterize values.
4. For any reference of a federated table, ensure you prefix the table name with `workspace("default").`. For example, if your table was `widgets_ADLS01`, your code shows `workspace("default").widgets_ADLS01` for that table.
5. Save the tool.

## Use federated tables in Jupyter notebooks

Federated tables are accessible in Jupyter notebooks through the Microsoft Sentinel VS Code extension.

In the Microsoft Sentinel VS Code extension, federated tables appear under: **Lake tables** &gt; **System tables** &gt; **Federated tables**

[![Screenshot showing federated tables in the Microsoft Sentinel VS Code extension under System tables Federated tables.](media/using-data-federation/vscode-federated-tables.png)](media/using-data-federation/vscode-federated-tables.png#lightbox)

Working with federated tables in Jupyter notebooks follows the same patterns as native System tables:

1. **Use the full table name**: Reference tables using the `<tableName>_<connectorInstance>` format.
2. **Don't specify a workspace name**: Read operations don't require a workspace specification.
3. **Read-only access**: Federated tables are read-only; you can't write data back to federated sources.

Note

After enabling data federation the first time, it can take up to 24 hours before you see federated tables within Jupyter notebooks.

### Jupyter notebook jobs

You can create scheduled Jupyter notebook jobs that utilize federated tables in the same way that you would create a notebook job for native data lake tables:

1. Develop your notebook with federated table queries.
2. Test the notebook to ensure federated queries execute correctly.
3. Create a job from the notebook.
4. Configure the job schedule and parameters.

Note

Notebook jobs can only write to Sentinel workspaces or system tables as destinations. You can't write data to a federated table.

## Best practices

Follow these query optimization, join strategy, and error handling guidelines to get the best performance from federated tables.

### Query optimization

Use the following practices to improve federated query performance.

- **Apply filters early**: Filter data at the source when possible to reduce data transfer.
- **Limit result sets**: Use `take` or `limit` clauses during development.
- **Use projections**: Select only the columns you need to improve performance.

#### Example: Optimized query

The following query demonstrates filtering a large federated dataset early to reduce data volume and selecting only the necessary columns to improve query performance.

```kusto
large_dataset_adls_connector
| where EventTime >= ago(1h)           // Filter early
| where EventType == "Login"           // Reduce data volume
| project EventTime, UserId, SourceIP  // Select needed columns
| take 10000                           // Limit results
```

### Join strategies

Use the following query performance practices when joining federated and native tables.

- **Use appropriate join kinds**: Choose `inner`, `leftouter`, or `rightouter` based on your needs.
- **Filter before joining**: Reduce the data volume before join operations.
- **Consider data sizes**: Place the smaller table on the right side of the join.

### Error handling

Consider the following practices to diagnose and handle common federated query issues.

- **Check connection status**: Verify federated connector instances are connected before querying.
- **Handle null values**: External data may contain unexpected nulls; use `coalesce()` or `isnull()` functions.
- **Monitor query performance**: Track execution times for federated queries to identify performance issues.

## Troubleshooting

### Query returns no results

- Verify the connector instance is in a connected state.
- Verify the external data source is available, along with the tables targeted in the query.
- Verify permissions weren't removed from the service principal or Sentinel managed identity based on the targeted data source.
- Check that you're using the correct federated table name format.
- Ensure System Tables is available in the navigation pane for your KQL queries or Notebook session.

### Query is slow

- Apply filters to reduce the data volume queried from external sources.
- Check the external source's performance and availability.
- Consider creating summary tables for frequently accessed data.

### Schema mismatch

- Review the table schema in the table management view.
- Adjust your query to handle schema differences.
- Check if the external table schema has changed since connector creation.

### Not able to run MCP tools for federated tables

Ensure you prefixed the table name with `workspace("default").` wherever you reference a federated table within the MCP tool.