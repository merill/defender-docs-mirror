---
layout: Conceptual
title: 'Microsoft Sentinel Migration: Select a Data Ingestion Tool | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/migration-ingestion-tool
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
description: Select a tool to transfer your historical data to the selected target platform.
author: EdB-MSFT
ms.author: edbaynash
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 0b607d96-3659-5e73-3a44-34f5ec7da041
document_version_independent_id: 7e9de93c-15f1-cf99-5c30-193bc8b0c67c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/migration-ingestion-tool.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/migration-ingestion-tool
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/migration-ingestion-tool.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/26e1a60c-4ce1-41de-b2d1-e5f3b7e68e6e
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad3bd485-5ca9-4865-afde-baec02586899
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 82e7c134-ff91-9fcf-ac94-49ffcb28b195
---

# Microsoft Sentinel Migration: Select a Data Ingestion Tool | Microsoft Learn

After you [select a target platform for your migration](migration-ingestion-target-platform), select a tool to transfer your historical data.

The following tools can transfer historical data to Azure Monitor, Azure Data Explorer, or Azure Blob Storage. The table lists the tools available for each target platform, along with general tools to help you with the ingestion process.

| Microsoft Sentinel data lake | Azure Data Explorer | Azure Blob Storage | General tools |
| --- | --- | --- | --- |
| - Azure Monitor custom log ingestion tool- Direct API | - LightIngest- Logstash | - Azure Data Factory or Azure Synapse- AzCopy | - Azure Data Box - SIEM data migration accelerator |

## Microsoft Sentinel data lake

Microsoft Sentinel data lake is the native data layer of the Microsoft Sentinel platform. It's the simplest path to a unified, queryable history of your security data inside Microsoft Sentinel and the recommended platform for long-term data retention.

To learn more, see [What is Microsoft Sentinel data lake?](/en-us/azure/sentinel/datalake/sentinel-lake-overview) and [Onboard to Microsoft Sentinel data lake](/en-us/azure/sentinel/datalake/sentinel-lake-onboarding).

### Azure Monitor custom log ingestion tool

The [Azure Monitor Custom Log Ingestion Tool on GitHub](https://github.com/Azure/Azure-Sentinel/tree/master/Tools/CustomLogsIngestion-DCE-DCR) is a PowerShell script that sends custom data to an Azure Monitor Logs workspace. You can point the script to the folder where all your log files reside, and the script pushes the files to that folder. The script accepts a CSV or JSON format for log files.

### Direct API

With this option, you ingest your custom logs into Azure Monitor Logs. For more information, see [Tutorial: Send data to Azure Monitor Logs with Logs ingestion API](/en-us/azure/azure-monitor/logs/tutorial-logs-ingestion-portal). You ingest the logs with a PowerShell script that uses a REST API. Alternatively, you can use any other programming language to perform the ingestion, and you can use other Azure services to abstract the compute layer, such as Azure Functions or Azure Logic Apps.

## Azure Data Explorer

Azure Data Explorer (ADX) supports several data ingestion methods. For more information, see [Azure Data Explorer data ingestion overview](/en-us/azure/data-explorer/ingest-data-overview).

The ingestion methods that ADX accepts are based on different components:

- SDKs for different languages, such as .NET, Go, Python, Java, NodeJS, and APIs.
- Managed pipelines, such as Event Grid or Storage Blob Event Hubs, and Azure Data Factory.
- Connectors or plugins, such as Logstash, Kafka, Power Automate, and Apache Spark.

Review the LightIngest and Logstash, two methods that are better tailored to the data migration use case.

### Use LightIngest for data ingestion

ADX has developed the [LightIngest utility](/en-us/azure/data-explorer/lightingest) specifically for the historical data migration use case. You can use LightIngest to copy data from a local file system or Azure Blob Storage to ADX.

Here are a few main benefits and capabilities of LightIngest:

- Because there's no time constraint on ingestion duration, LightIngest is most useful when you want to ingest large amounts of data.
- LightIngest is useful when you want to query records according to the time they were created, and not the time they were ingested.
- You don't need to deal with complex sizing for LightIngest, because the utility doesn't perform the actual copy. LightIngest informs ADX about the blobs that need to be copied, and ADX copies the data.

If you choose LightIngest, review these tips and best practices.

- To speed up your migration and reduce costs, increase the size of your ADX cluster to create more available nodes for ingestion. Decrease the size once the migration is over.
- For more efficient queries after you ingest the data to ADX, ensure that the copied data uses the timestamp for the original events. The data shouldn't use the timestamp from when the data is copied to ADX. You provide the timestamp to LightIngest as the path of file name as part of the [CreationTime property](/en-us/azure/data-explorer/lightingest#how-to-ingest-data-using-creationtime).
- If your path or file names don't include a timestamp, you can still instruct ADX to organize the data using a [partitioning policy](/en-us/kusto/management/partitioning-policy?view=azure-data-explorer&amp;preserve-view=true).

### Logstash

[Logstash](https://www.elastic.co/products/logstash) is an open source, server-side data processing pipeline that ingests data from many sources simultaneously, transforms the data, and then sends the data to your favorite "stash". Learn how to [ingest data from Logstash to Azure Data Explorer](/en-us/azure/data-explorer/ingest-data-logstash). Logstash runs on Windows, Linux and macOS Machines.

To optimize performance, [configure the Logstash tier size](https://www.elastic.co/guide/en/logstash/current/deploying-and-scaling.html) according to the events per second. We recommend that you use LightIngest wherever possible, because LightIngest relies on the ADX cluster computing to perform the copy.

## Ingest data into Azure Blob Storage

You can ingest data to Azure Blob Storage in several ways.

- [Azure Data Factory or Azure Synapse](/en-us/azure/data-factory/connector-azure-blob-storage)
- [AzCopy](/en-us/azure/storage/common/storage-use-azcopy-v10)
- [Azure Storage Explorer](/en-us/azure/architecture/data-science-process/move-data-to-azure-blob-using-azure-storage-explorer)
- [Python](/en-us/azure/storage/blobs/storage-quickstart-blobs-python)
- [SSIS](/en-us/azure/architecture/data-science-process/move-data-to-azure-blob-using-ssis)

Review Azure Data Factory or Azure Synapse, which are better tailored to the data migration use case.

### Use Azure Data Factory or Azure Synapse to copy data

To use the Copy activity in Azure Data Factory (ADF) or Synapse pipelines:

1. Create and configure a self-hosted integration runtime. This component is responsible for copying the data from your on-premises host.
2. Create linked services for the source data store ([filesystem](/en-us/azure/data-factory/connector-file-system?tabs=data-factory#create-a-file-system-linked-service-using-ui) and the sink data store [blob storage](/en-us/azure/data-factory/connector-azure-blob-storage?tabs=data-factory#create-an-azure-blob-storage-linked-service-using-ui).
3. To copy the data, use the [Copy data tool](/en-us/azure/data-factory/quickstart-hello-world-copy-data-tool). Alternatively, you can use method such as PowerShell, Azure portal, a .NET SDK, and so on.

### Use AzCopy to copy data

[AzCopy](/en-us/azure/storage/common/storage-use-azcopy-v10) is a simple command-line utility that copies files to or from storage accounts. AzCopy is available for Windows, Linux, and macOS. Learn how to [copy on-premises data to Azure Blob storage with AzCopy](/en-us/azure/storage/common/storage-use-azcopy-v10).

You can also use these options to copy the data:

- Learn how to [optimize AzCopy performance](/en-us/azure/storage/common/storage-use-azcopy-optimize).
- See [AzCopy configuration settings](/en-us/azure/storage/common/storage-ref-azcopy-configuration-settings).
- See the [AzCopy copy command reference](/en-us/azure/storage/common/storage-ref-azcopy-copy).

## Use Azure Data Box for large-scale data ingestion

In a scenario where the source SIEM doesn't have good connectivity to Azure, ingesting the data using tools such as AzCopy, LightIngest, or Azure Data Factory might be slow or even impossible. To address this scenario, you can use [Azure Data Box](/en-us/azure/databox/data-box-overview) to copy the data locally from the customer's data center into an appliance, and then ship that appliance to an Azure data center. While Azure Data Box isn't a replacement for AzCopy or LightIngest, you can use this tool to accelerate the data transfer between the customer data center and Azure.

Azure Data Box offers three different SKUs, depending on the amount of data to migrate:

- [Data Box Disk](/en-us/azure/databox/data-box-disk-overview)
- [Data Box](/en-us/azure/databox/data-box-overview)
- [Data Box Heavy](/en-us/azure/databox/data-box-heavy-overview)

After you complete the migration, the data is available in a storage account under one of your Azure subscriptions. You can then use AzCopy, LightIngest, or Azure Data Factory to ingest data from the storage account.

## Use the SIEM data migration accelerator

In addition to selecting an ingestion tool, your team needs to invest time in setting up the foundation environment. To ease environment setup, you can use the [SIEM data migration accelerator](https://aka.ms/siemdatamigration), which automates the following tasks:

- Deploys a Windows virtual machine that will be used to move the logs from the source to the target platform
- Downloads and extracts the following tools into the virtual machine desktop:
    - LightIngest: Used to migrate data to ADX
    - Azure Monitor Custom log ingestion tool: Used to migrate data to Log Analytics
    - AzCopy: Used to migrate data to Azure Blob Storage
- Deploys the target platform that will host your historical logs:
    - Azure Storage account (Azure Blob Storage)
    - Azure Data Explorer cluster and database
    - Azure Monitor Logs workspace (Basic Logs; enabled with Microsoft Sentinel)

To use the SIEM data migration accelerator:

1. From the [SIEM data migration accelerator page](https://aka.ms/siemdatamigration), click **Deploy to Azure** at the bottom of the page, and authenticate.
2. Select **Basics**, select your resource group and location, and then select **Next**.
3. Select **Migration VM**, and do the following:
    - Type the virtual machine name, username and password.
    - Select an existing vNet or create a new vNet for the virtual machine connection.
    - Select the virtual machine size.
4. Select **Target platform**and do one of the following:
    - Skip this step.
    - Provide the ADX cluster and database name, SKU, and number of nodes.
    - For Azure Blob Storage accounts, select an existing account. If you don't have an account, provide a new account name, type, and redundancy.
    - For Azure Monitor Logs, type the name of the new workspace.