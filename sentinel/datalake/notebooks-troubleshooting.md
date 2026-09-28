---
layout: Conceptual
title: Troubleshoot notebooks on the Microsoft Sentinel data lake - Microsoft Security | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/notebooks-troubleshooting
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
description: Find solutions for common errors when working with Jupyter notebooks in the Microsoft Sentinel data lake, including database, table, authorization, and ingestion errors.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: zeinam
ms.topic: troubleshooting
ms.date: 2026-04-27T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 2da3b7f5-fdd8-98aa-2804-918f8989e98d
document_version_independent_id: a74ce688-511a-bfe6-21c5-2c123529e312
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/notebooks-troubleshooting.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/notebooks-troubleshooting
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/notebooks-troubleshooting.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 888854c6-a892-e3ed-048f-d9170c5b6f32
---

# Troubleshoot notebooks on the Microsoft Sentinel data lake - Microsoft Security | Microsoft Learn

This article lists common errors you might encounter when working with Jupyter notebooks in the Microsoft Sentinel data lake, their root causes, and suggested actions to resolve them.

For information on running notebooks, see [Run notebooks on the Microsoft Sentinel data lake](notebooks).

## Common errors

The following table lists common errors, their error codes, and suggested actions to resolve them.

| Error Category | Error Name | Error Code | Error Message | Suggested Action |
| --- | --- | --- | --- | --- |
| DatabaseError | DatabaseNotFound | 2001 | Database {DatabaseName} not found. | Verify that the database exists. If the database is new, wait for a metadata refresh. |
| DatabaseError | AmbiguousDatabaseName | 2002 | Several databases (IDs: {DatabaseID1}, {DatabaseID2}, ...) share the name {DatabaseName}. Provide a specific database ID. | Specify a database ID when multiple databases have the same name. |
| DatabaseError | DatabaseIdMismatch | 2003 | Database ({DatabaseName}, ID {DatabaseID}) not found. | Check both the database name and ID. To obtain database IDs, list all the databases. |
| DatabaseError | ListDatabasesFailure | 2004 | Can't fetch databases. Restart the session and try again. | Restart the session and retry the operation after a few minutes. |
| TableError | TableDoesNotExist | 2100 | Table {TableName} not found in the database {DatabaseName}. | Verify that the table exists in the database. If the table or database is new, wait a few minutes and try again. |
| TableError | ProvisioningIncomplete | 2101 | Table {TableName} is not ready. Wait a few minutes before trying again. | The table is being provisioned. Wait a few minutes before trying again. |
| TableError | DeltaTableMissing | 2102 | Table {TableName} is empty. New tables can take up to a few hours to be ready. | It can take a few hours to fully synchronize an analytics table into the data lake. For tables that are only in the data lake, check if the data needs to be loaded or restored. |
| TableError | TableDoesNotExistForDelete | 2103 | Can't delete table. Table {TableName} not found. | Verify that the table exists in the database. If the table or database is new, wait a few minutes and try again. |
| AuthorizationFailure | MissingSASToken | 2201 | Can't access table. Restart the session and try again. | Authorization failed while trying to fetch the access token for the table. Restart the session and try again. |
| AuthorizationFailure | InvalidSASToken | 2202 | Can't access table. Restart the session and try again. | Authorization failed while trying to fetch the access token for the table. Restart the session and try again. |
| AuthorizationFailure | TokenExpired | 2203 | Can't access table. Restart the session and try again. | Authorization failed while trying to fetch the access token for the table. Restart the session and try again. |
| AuthorizationFailure | TableInsufficientPermissions | 2204 | Access needed for the table {TableName} in the database {DatabaseName}. | Contact an administrator to request access to the table or the database (workspace). |
| AuthorizationFailure | InternalTableAccessDenied | 2205 | Access to the table {TableName} is restricted. | Only system or user-defined tables can be accessed from a notebook. |
| AuthorizationFailure | TableAuthFailure | 2206 | Can't save data to the table. Restart the session and try again. | Authorization failed while trying to save data to the table. Restart the session and try again. |
| ConfigurationError | HadoopConfigFailure | 2301 | Can't update session configuration. Restart the session and try again. | This problem is transient and can be resolved by restarting the session and trying again. If this problem persists, contact support. |
| DataError | JsonParsingFailure | 2302 | Table metadata has been corrupted. Contact support for assistance. | Contact support for assistance. Provide your tenant ID, the table name, and the database name. |
| TableSchemaError | TableSchemaMismatch | 2401 | Column not found in the destination table. Align the DataFrame schema and the destination table or use overwrite mode. | Update the DataFrame schema to match the table in your target database. You can also replace the table entirely in overwrite mode. |
| TableSchemaError | MissingRequiredColumns | 2402 | Column {ColumnName} is missing from the DataFrame. Check the DataFrame schema and align it with the destination table. | Update the DataFrame schema to match the table in your target database. You can also replace the table entirely in overwrite mode. |
| TableSchemaError | ColumnTypeChangeNotAllowed | 2403 | Can't change the data type of the column {ColumnName}. | A data type change is not allowed for the column. Check existing columns in the destination table and align all data types in the DataFrame. |
| TableSchemaError | ColumnNullabilityChangeNotAllowed | 2404 | Can't change nullability of the column {ColumnName}. | Can't update nullability settings of the column. Check the destination table and align the settings with the DataFrame. |
| IngestionError | FolderCreationFailure | 2501 | Can't create storage for the table {TableName}. | This problem is transient and can be resolved by restarting the session and trying again. If this problem persists, contact support. |
| IngestionError | SubJobRequestFailure | 2502 | Can't create ingestion job for the table {TableName}. | This problem is transient and can be resolved by restarting the session and trying again. If this problem persists, contact support. |
| IngestionError | SubJobCreationFailure | 2503 | Can't create ingestion job for the table {TableName}. | This problem is transient and can be resolved by restarting the session and trying again. If this problem persists, contact support. |
| InputError | InvalidWriteMode | 2601 | Invalid write mode. Use append or overwrite. | Specify a valid write mode (append or overwrite) before saving the DataFrame. |
| InputError | PartitioningNotAllowed | 2602 | Can't partition analytics tables. | Remove any partitioning for all columns in analytics tables. |
| InputError | MissingTableSuffixLake | 2603 | Invalid custom table name. All names of custom tables in the data lake must end with \_SPRK. | Add \_SPRK as a suffix to the table name before writing it to the data lake. |
| InputError | MissingTableSuffixLA | 2604 | Invalid custom table name. All names of custom analytics tables must end with \_SPRK\_CL. | Add \_SPRK\_CL as a suffix to the table name before writing it to analytics storage. |
| UnknownError | InternalServerError | 2901 | Something went wrong. Restart the session and try again. | This problem is transient and can be resolved by restarting the session and trying again. If this problem persists, contact support. |

Note

Querying legacy tables such as AzureDiagnostics is not supported.