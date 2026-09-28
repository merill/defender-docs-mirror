---
layout: Conceptual
title: Run KQL queries against the Microsoft Sentinel data lake - Microsoft Security | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/kql-queries
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
description: Use the Defender portal's Data lake exploration KQL queries to query and interact with the Microsoft Sentinel data lake. Create, edit, and run KQL queries to explore your data lake resources
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: zeinam
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: ms-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 52a560ec-4dce-6ec0-c18c-c4bf7aea6eb5
document_version_independent_id: 65253265-4df6-de67-920e-805b91d482e7
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/kql-queries.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/kql-queries
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/kql-queries.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: ee3fe85c-4cb3-ac6b-bd86-c09615f3e274
---

# Run KQL queries against the Microsoft Sentinel data lake - Microsoft Security | Microsoft Learn

Data lake exploration in the Microsoft Defender portal provides a unified interface to analyze your data lake. It lets you run KQL (Kusto Query Language) queries, create jobs, and manage them. Before you begin, make sure you meet the prerequisites for querying the data lake, including data lake onboarding and required permissions.

The **KQL queries** page under **Data lake exploration** lets you edit and run KQL queries on data lake resources and federated tables. Create jobs to promote data from the data lake to the analytics tier, or create aggregate tables in the data lake tier. Run jobs on demand or schedule them. The **Jobs** page lets you manage jobs; enable, disable, edit, or delete. For more information, see [Create jobs in the Microsoft Sentinel data lake](kql-jobs).

## Prerequisites

The following prerequisites are needed to run KQL queries in the Microsoft Sentinel data lake.

### Onboard to the data lake

You can run KQL queries in the Microsoft Defender portal after completing the onboarding process. For more information on onboarding, see [Onboarding to Microsoft Sentinel data lake](sentinel-lake-onboarding).

### Permissions

Microsoft Entra ID roles let you access all workspaces in the data lake. Alternatively, you can grant access to individual workspaces using Azure role-based access control (Azure RBAC) roles. Users with Azure RBAC permissions for Microsoft Sentinel workspaces can run KQL queries against those workspaces in the data lake tier. For more information on roles and permissions, see [Microsoft Sentinel data lake roles and permissions](../roles#roles-and-permissions-for-the-microsoft-sentinel-data-lake).

Optionally, Microsoft Sentinel scoping or row-level RBAC can be configured to further restrict data access within a workspace. When enabled, row-level scoping limits the data returned by queries based on the user’s assigned scope. If row-level scoping isn’t configured, the existing workspace-level permission model applies unchanged. [Configure Microsoft Sentinel scoping (row-level RBAC) (preview)](../scoping).

## Write KQL queries

Writing queries for the data lake is similar to writing queries in the advanced hunting experience. You can use the same KQL syntax and functions. KQL supports advanced analytics and machine learning functions. The query editor offers an interface for running KQL queries with features like IntelliSense and autocomplete to help you write efficiently. For a detailed overview of KQL syntax and functions, see [Kusto Query Language (KQL) overview](/en-us/azure/data-explorer/kusto/query/).

## KQL queries in the Defender portal

Select **New query** to create a new query tab. The portal saves the last query in each tab. Switch between tabs to work on multiple queries simultaneously.

The **Query history** tab shows a list of your previously run queries, query processing time, and completion state. You can open a previous query in a new tab by selecting it from the list. The portal saves the query history for 30 days. Select a query to edit or run it again.

[![Screenshot of the KQL queries page in the Defender portal.](media/kql-queries/query-editor.png)](media/kql-queries/query-editor.png#lightbox)

### Select workspaces

You can run queries against a single workspace or multiple workspaces. Select workspaces in the upper right corner of the query editor by using the **Selected workspaces** dropdown. The workspaces you select determine the tables available for querying. The selected workspaces apply to all query tabs in the query editor. When you use multiple workspaces, the `union()` operator is applied by default to tables with the same name and schema from different workspaces. Use the `workspace()` operator to query a table from a specific workspace, for example `workspace("MyWorkspace").AuditLogs`.

To query federated tables, select **System tables** when choosing workspaces. For more information on federated tables, see [Using federated tables in the Microsoft Sentinel data lake](using-data-federation).

If you select a single, empty workspace or a workspace in the process of onboarding, the schema browser doesn't display any tables.

[![A screenshot showing the workspaces selection panel.](media/kql-queries/select-a-workspace.png)](media/kql-queries/select-a-workspace.png#lightbox)

### Time range selection

Note

Queries are limited to 500,000 rows or 64 MB of data and time out after 8 minutes. Broad time ranges can exceed these limits. For long-running queries, consider using async queries.

Use the time picker above the query editor to select the time range for your query. By using the **Custom time range** option, you can set a specific start and end time. Time ranges can be up to 12 years in duration.

[![A screenshot showing the time range selector.](media/kql-queries/time-range-selector.png)](media/kql-queries/time-range-selector.png#lightbox)

Important

The time range selector doesn't work for federated tables that don't have a `TimeGenerated` column or where the `TimeGenerated` column isn't in the correct format. When querying these tables, specify the time range in your KQL query using the appropriate column for time filtering.

You can also specify a time range in the KQL query syntax, for example:

- `where TimeGenerated between (datetime(2020-01-01) .. datetime(2020-12-31))`
- `where TimeGenerated between(ago(180d)..ago(90d))`

Note

Queries are limited to 500,000 rows or 64 MB of data and timeout after 8 minutes. When selecting a broad time range, your query might exceed these limits. Consider using asynchronous queries for long-running queries. For more information, see Async queries.

### View schema information

The schema browser provides a list of available tables and their columns for the selected workspaces, grouped by category. System tables appear in the **Assets** category. Custom tables with `_CL`, `_KQL_CL`, `_SPARK`, and `_SPARK_CL` are grouped in the **Custom logs** category. Use the schema browser to explore the data available in your data lake and discover tables and columns. Use the search box to quickly find specific tables.

[![A screenshot showing the schema browser panel in the KQL editor.](media/kql-queries/schema-browser.png)](media/kql-queries/schema-browser.png#lightbox)

### Result window

The result window displays the results of your query. You can view the results in a table format, and you can export the results to a CSV file using the **Export** button in the upper left corner of the result window. Toggle the visibility of empty columns using the **Show empty columns** button. The **Customize columns** button allows you to select which columns to display in the result window.

You can search the results using the search box in the upper right corner of the result window.

[![A screenshot showing the results window in a KQL query editor.](media/kql-queries/results-window.png)](media/kql-queries/results-window.png#lightbox)

## Out-of-the-box queries

The **Queries** tab provides a collection of out-of-the-box KQL queries. These queries cover common scenarios and use cases, such as security incident investigation and threat hunting. You can use these queries as-is or modify them to suit your specific needs.

Select a query from the list using the **...** icon. You can open it in a new query tab for editing or run it immediately.

For more information on sample queries, see [Sample KQL queries for Microsoft Sentinel data lake](kql-sample-queries#out-of-the-box-queries).

[![Screenshot of the Sample queries tab in the KQL query editor.](media/kql-queries/out-of-the-box-queries.png)](media/kql-queries/out-of-the-box-queries.png#lightbox)

## Async queries

Async queries let you run long-running KQL queries in the background so you can continue working in the portal while the query processes on the server. Use async queries when your query might exceed the 8-minute synchronous timeout or when working with broad time ranges.

### Run async queries

You can run long-running queries asynchronously, so you can keep working while the query runs on the server. To run a query asynchronously:

1. Select the down arrow on the **Run query** button, then select **Run async query**.
2. Enter a query name to identify your async query.
3. After submitting the query, monitor its status in the **Async Queries** tab.
4. When the query completes, select the query name from the list to view the results.

[![A screenshot showing the Async Queries tab in the KQL query editor.](media/kql-queries/run-async-query.png)](media/kql-queries/run-async-query.png#lightbox)

If a synchronous query takes longer than 2 minutes to run, a prompt appears asking if you want to run the query asynchronously. Select **Run async** to change the query to run asynchronously.

[![A screenshot showing the prompt to change a long-running query to an async query.](media/kql-queries/change-to-async-query.png)](media/kql-queries/change-to-async-query.png#lightbox)

### Fetch async query results

To view the async query results, select the completed async query from the **Async Queries** tab and select **Fetch results**. The query is displayed in comments in the query editor and results are displayed in the **Results tab**.

Results are stored for 24 hours and can be accessed multiple times. You can export the results to a CSV file by using the **Export** button in the upper left corner of the result window.

[![A screenshot showing the results of an async query in the KQL query editor.](media/kql-queries/fetch-async-query-results.png)](media/kql-queries/fetch-async-query-results.png#lightbox)

## Service parameters and limits for KQL async queries

The following table lists the service parameters and limits for KQL async queries in the Microsoft Sentinel data lake.

Note

All limits in this table apply **per tenant**. There's no per-user limit. Asynchronous KQL queries share the same rate-limit and concurrency counters as interactive KQL queries; KQL jobs have their own separate quota.

When either the rate limit or the concurrency limit is exceeded, the request is **rejected** and not queued. The concurrency counter decrements as soon as a running query finishes, and the rate-limit counter resets every minute.

| Category | Parameter/limit |
| --- | --- |
| Rate limit per tenant | 30 queries per minute (combined with interactive KQL queries) |
| Concurrency per tenant | 10 concurrent queries (combined with interactive KQL queries) |
| Async query execution timeout | 1 hour |
| Cache duration | 24 hours |
| Number of times users can fetch cached results | Unlimited |
| Query scope | Multiple workspaces |
| Query time range | Up to 12 years |

## Create and manage KQL query jobs

Jobs are used to run KQL queries against the data in the data lake tier and promote the results to the analytics tier. You can create one-time or scheduled jobs, and you can enable, disable, edit, or delete jobs from the **Jobs** page. To create a job based on your current query, select the **Create job** button. For more information on creating and managing jobs, see [Create jobs in the Microsoft Sentinel data lake](kql-jobs).

## Query the data lake with Azure Data Explorer

You can run KQL queries against the Microsoft Sentinel data lake using Azure Data Explorer (ADX). ADX provides a powerful query engine and advanced analytics capabilities. To connect to the data lake using ADX, create a new connection using the following URI: `https://api.securityplatform.microsoft.com/lake/kql`

When querying tables in the data lake using ADX, you must use the `external_table()` function to access the data. The following example query retrieves a sample of 100 records from the `AADRiskyUsers` external table:

```kql
external_table("AADRiskyUsers")
| take 100
```

## Query considerations and limitations

Keep the following limitations and considerations in mind when running KQL queries against the data lake.

- Querying legacy tables such as AzureDiagnostics is not supported.
- Empty tables don’t appear in schema view, and queries aren’t supported until the table contains data.
- Queries are run against the workspaces you selected. Make sure you select the correct workspaces before running a query.
- Executing KQL queries on the Microsoft Sentinel data lake incurs charges based on query billing meters. For more information, see [Plan costs and understand Microsoft Sentinel pricing and billing](../billing#data-lake-tier).
- Review data ingestion and table retention policy. Before setting query time range, be aware of data retention on your data lake tables and whether data is available for selected time range. For more information, see [Manage data tiers and retention in Microsoft Defender portal](https://aka.ms/manage-data-defender-portal-overview).
- KQL queries against the data lake are less performant than queries on analytics tier. Use KQL queries against the data lake only when exploring historical data or when tables are stored in data lake-only mode.
- The following KQL control commands are currently supported:

    - `.show version`
    - `.show databases`
    - `.show databases entities`
    - `.show database`
- When you use the `stored_query_results` command, provide the time range in the KQL query. The query editor time range selector doesn't work with the `stored_query_results` command.
- Using out-of-the-box or custom functions isn't supported in KQL queries against the data lake.
- Calling external data via KQL query against the data lake isn't supported.
- All KQL operators and functions are supported except for the following:

    - `adx()`
    - `arg()`
    - `externaldata()`
    - `ingestion_time()`
    - `estimate_data_size()`
- There is a 15-minute latency between when data is ingested into the data lake or federated tables, and when it becomes available for querying. This means that newly ingested data may not be immediately queryable.

## Service parameters and limits for KQL queries in the lake tier

The following service parameters and limits apply when writing queries in the Microsoft Sentinel data lake.

Note

All limits in this table apply **per tenant**. There's no per-user limit. Interactive KQL queries and asynchronous KQL queries share the same rate-limit and concurrency counters.

When either the rate limit or the concurrency limit is exceeded, the request is **rejected** and not queued. The concurrency counter decrements as soon as a running query finishes, and the rate-limit counter resets every minute.

| Category | Parameter/limit |
| --- | --- |
| Rate limit per tenant | 30 queries per minute (combined interactive and async) |
| Concurrency per tenant | 10 concurrent queries (combined interactive and async) |
| Query result data | 64 MB. To override the default for a specific query, see [Query limits](/en-us/azure/data-explorer/kusto/concepts/querylimits) in the Kusto Query Language reference. |
| Query result rows | 500,000 rows. To override the default for a specific query, see [Query limits](/en-us/azure/data-explorer/kusto/concepts/querylimits) in the Kusto Query Language reference. |
| Query scope | Multiple workspaces |
| Query timeout | 4 minutes |
| Queryable time range | Up to 12 years, depending on data retention. |

For troubleshooting KQL queries, see [Troubleshoot KQL queries in the Microsoft Sentinel data lake](kql-troubleshoot).