---
layout: Conceptual
title: 'Microsoft Sentinel Migration: Ingest Data into Target Platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/migration-export-ingest
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
description: Learn how to ingest historical data into your selected target platform.
author: EdB-MSFT
ms.author: edbaynash
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 61328fff-0a59-e4ff-c364-1eb0d45dd0e7
document_version_independent_id: 722fbd8f-21b6-0d93-4d95-bdc9fb58f802
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/migration-export-ingest.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/migration-export-ingest
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/migration-export-ingest.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/26e1a60c-4ce1-41de-b2d1-e5f3b7e68e6e
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad3bd485-5ca9-4865-afde-baec02586899
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
platformId: 7134e317-cf8b-07f7-f8f3-1390896b6e32
---

# Microsoft Sentinel Migration: Ingest Data into Target Platform | Microsoft Learn

To ingest exported historical SIEM data into a target platform, first ensure you have chosen a [target platform for historical data](migration-ingestion-target-platform), selected a [data transfer tool for migration ingestion](migration-ingestion-tool), and stored the data in a staging location.

This article describes how to export data from your legacy SIEM and ingest historical data into Microsoft Sentinel data lake, Azure Data Explorer, or Azure Blob Storage.

## Export data from the legacy SIEM

In general, SIEMs can export or dump data to a file in your local file system, so you can use this method to extract the historical data. It’s also important to set up a staging location for your exported files. The tool you use to transfer the data ingestion can copy the files from the staging location to the target platform. For information about the tools you can use for data ingestion, see [Select a target Microsoft platform to host the exported historical data](migration-ingestion-target-platform).

This diagram shows the high-level export and ingestion process.

[![Diagram illustrating steps involved in export and ingestion.](media/migration-export-ingest/export-data.png)](media/migration-export-ingest/export-data.png#lightbox)

To export data from your current SIEM, see one of the following sections:

- [Export data from ArcSight](migration-arcsight-historical-data)
- [Export data from Splunk](migration-splunk-historical-data)
- [Export data from QRadar](migration-qradar-historical-data)

## Ingest data to Microsoft Sentinel data lake

Microsoft Sentinel data lake is the native data layer of the Microsoft Sentinel platform. It's the simplest path to a unified, queryable history of your security data inside Microsoft Sentinel and the recommended platform for long-term data retention.

To ingest your historical data into Microsoft Sentinel data lake (as shown in the export and ingestion process diagram), use the [Custom Log Ingestion tool](/en-us/azure/azure-monitor/logs/tutorial-logs-ingestion-portal).

## Ingest to Azure Data Explorer (ADX)

Azure Data Explorer (ADX) is a fast, scalable data exploration service. To ingest your historical data into ADX:

1. LightIngest supports Windows only. [Install and configure LightIngest](/en-us/azure/data-explorer/lightingest) on the Windows system where logs are exported, or install LightIngest on another Windows system that has access to the exported logs.
2. If you don't have an existing ADX cluster, create a new cluster and copy the connection string. Learn how to [set up ADX](/en-us/azure/data-explorer/create-cluster-database-portal).
3. In ADX, create tables and define a schema for the CSV or JSON format (for QRadar). Learn how to [create a table and define a schema using sample data](/en-us/azure/data-explorer/ingest-sample-data) or [create a table and define a schema without sample data](/en-us/azure/data-explorer/one-click-table).
4. [Run LightIngest](/en-us/azure/data-explorer/lightingest#run-lightingest) with the folder path that includes the exported logs as the path, and the ADX connection string as the output. When you run LightIngest, ensure that you provide the target ADX table name, that the argument pattern is set to `*.csv`, and the format is set to `.csv` (or `json` for QRadar).

## Ingest to Azure Blob Storage

To ingest your historical data into Azure Blob Storage:

1. [Install and configure AzCopy](/en-us/azure/storage/common/storage-use-azcopy-v10) on the system to which you exported the logs. Alternatively, install AzCopy on another system that has access to the exported logs.
2. [Create an Azure Blob Storage account](/en-us/azure/storage/common/storage-account-create) and copy the authorized [Microsoft Entra ID](/en-us/azure/storage/common/storage-use-azcopy-v10#option-1-use-azure-active-directory) credentials or [Shared Access Signature](/en-us/azure/storage/common/storage-use-azcopy-v10#option-2-use-a-sas-token) token.
3. [Run AzCopy](/en-us/azure/storage/common/storage-use-azcopy-v10#run-azcopy) with the folder path that includes the exported logs as the source, and the Azure Blob Storage connection string as the output.