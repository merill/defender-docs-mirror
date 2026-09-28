---
layout: Conceptual
title: Microsoft Sentinel data lake Microsoft Sentinel Provider class reference | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/sentinel-provider-class-reference
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
description: Reference documentation for the Microsoft Sentinel Provider class, which allows you to connect to the Microsoft Sentinel data lake and perform various operations.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: zeinam
ms.topic: reference
ms.date: 2026-02-08T00:00:00.0000000Z
locale: en-us
document_id: ea7c3aa1-8371-1300-8fb9-ea92a47ec4c6
document_version_independent_id: a01378d6-f0f2-9928-24dd-6aeb04030993
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/sentinel-provider-class-reference.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/sentinel-provider-class-reference
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/sentinel-provider-class-reference.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
platformId: e887954b-02a9-adb3-8fbf-420bdb39666a
---

# Microsoft Sentinel data lake Microsoft Sentinel Provider class reference | Microsoft Learn

The `MicrosoftSentinelProvider` class provides a way to interact with the Microsoft Sentinel data lake, allowing you to perform operations such as listing databases, reading tables, and saving data. This class is designed to work with the Spark sessions in Jupyter notebooks and provides methods to access and manipulate data stored in the Microsoft Sentinel data lake.

This class is part of the `sentinel.datalake` module and provides methods to interact with the data lake. To use this class, import it and create an instance of the class using the `spark` session.

```python
from sentinel_lake.providers import MicrosoftSentinelProvider
data_provider = MicrosoftSentinelProvider(spark)      
```

You must have the necessary permissions to perform operations such as reading and writing data. For more information on permissions, see [Microsoft Sentinel data lake permissions](../roles#roles-and-permissions-for-the-microsoft-sentinel-data-lake).

## Methods

The `MicrosoftSentinelProvider` class provides several methods to interact with the Microsoft Sentinel data lake. Each method listed below assumes the `MicrosoftSentinelProvider` class has been imported and an instance has been created using the `spark` session as follows:

```python
from sentinel_lake.providers import MicrosoftSentinelProvider
data_provider = MicrosoftSentinelProvider(spark) 
```

### list\_databases

List all available databases / Microsoft Sentinel workspaces.

```python
data_provider.list_databases()    
```

Returns:

- `list[str]`: A list of database names (workspaces) available in the Microsoft Sentinel data lake.

### list\_tables

List all tables in a given database.

```python
data_provider.list_tables([database_name],[database_id])
   
```

Parameters:

- `database_name` (str, optional): The name of the database (workspace) to list tables from. IF not specified the system tables database is used.
- `database_id` (str, optional): The unique identifier of the database if workspace names aren't unique.

Returns:

- `list[str]`: A list of table names in the specified database.

Examples:

List all tables in the system tables database:

```python
data_provider.list_tables() 
```

List all tables in a specific database. Specify the `database_id` of the database if your workspace names aren't unique:

```python
data_provider.list_tables("workspace1", database_id="ab1111112222ab333333")
```

### read\_table

Load a DataFrame from a table in Lake.

```python
data_provider.read_table({table}, [database_name], [database_id])
```

Parameters:

- `table_name` (str): The name of the table to read.
- `database_name` (str, optional): The name of the database (workspace) containing the table. Defaults to `System tables`.
- `database_id` (str, optional): The unique identifier of the database if workspace names aren't unique.

Returns:

- `DataFrame`: A DataFrame containing the data from the specified table.

Example:

```python
df = data_provider.read_table("EntraGroups", "Workspace001")
```

### save\_as\_table

Write a DataFrame as a managed table. You can write to the lake tier by using the `_SPRK` suffix in your table name, or to the analytics tier by using the `_SPRK_CL` suffix.

Note

For the analytics tier, `save_as_table` supports `append` mode only. `overwrite` mode is only supported in the lake tier.

```python
data_provider.save_as_table({DataFrame}, {table_name}, [database_name], [database_id], [write_options])
```

Parameters:

- `DataFrame` (DataFrame): The DataFrame to write as a table.
- `table_name` (str): The name of the table to create or overwrite.
- `database_name` (str, optional): The name of the database (workspace) to save the table in. Defaults to `System tables`.
- `database_id` (str, optional, analytics tier only): The unique identifier of the database in the analytics tier if workspace names aren't unique.
- `write_options` (dict, optional): Options for writing the table. Supported options: - mode: `append` or `overwrite` (default: `append`) `overwrite` mode is only supported in the lake tier. - partitionBy: list of columns to partition by Example: {'mode': 'append', 'partitionBy': ['date']}

Returns:

- `str`: The run ID of the write operation.

Note

The partitioning option only applies to custom tables in system tables database (workspace) in the data lake tier. It isn't supported for tables in the analytics tier or for tables in databases other than the system tables database in the data lake tier.

Examples:

Create new custom table in the data lake tier in the `System tables` workspace.

```python
data_provider.save_as_table(dataframe, "CustomTable1_SPRK", "System tables")
```

Overwrite a table in the system tables database (workspace) in the data lake tier.

```python
write_options = {
    'mode': 'overwrite'
}
data_provider.save_as_table(dataframe, "CustomTable1_SPRK", write_options=write_options)
```

Create new custom table in the analytics tier.

```python
data_provider.save_as_table(dataframe, "CustomTable1_SPRK_CL", "analyticstierworkspace")
```

Append to an existing custom table in the analytics tier.

```python
write_options = {
    'mode': 'append'
}
data_provider.save_as_table(dataframe, "CustomTable1_SPRK_CL", "analyticstierworkspace", write_options)
```

Append to the system tables database with partitioning on the `TimeGenerated` column.

```python
data_loader.save_as_table(dataframe, "table1", write_options: {'mode': 'append', 'partitionBy': ['TimeGenerated']})
```

### delete\_table

Deletes the table from the lake tier. You can delete table from lake tier by using the `_SPRK` suffix in your table name. You can't delete a table from the analytics tier using this function. To delete a custom table in the analytics tier, use the Log Analytics API functions. For more information, see [Add or delete tables and columns in Azure Monitor Logs](/en-us/azure/azure-monitor/logs/create-custom-table?tabs=azure-portal-1%2Cazure-portal-2%2Cazure-portal-3#delete-a-table).

```python
data_provider.delete_table({table_name}, [database_name], [database_id])
```

Parameters:

- `table_name` (str): The name of the table to delete.
- `database_name` (str, optional): The name of the database (workspace) containing the table. Defaults to `System tables`.
- `database_id` (str, optional): The unique identifier of the database if workspace names aren't unique.

Returns:

- `dict`: A dictionary containing the result of the delete operation.

Example:

```python
data_provider.delete_table("customtable_SPRK", "System tables")
```