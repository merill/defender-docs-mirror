---
layout: Conceptual
title: Azure Storage Blob data connector reference for the Codeless Connector Framework - Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/data-connection-rules-reference-azure-storage
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
description: This article provides reference JSON fields and properties for creating the Azure Storage Blob data connector type and its data connection rules as part of the Codeless Connector Framework.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: krishsa
ms.topic: reference
ms.date: 2026-08-07T00:00:00.0000000Z
locale: en-us
document_id: 0d0ea407-0760-9210-4631-c17e726c8040
document_version_independent_id: 7fd8f790-5513-8a1b-b1a1-7f431890219e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/data-connection-rules-reference-azure-storage.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/data-connection-rules-reference-azure-storage
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/data-connection-rules-reference-azure-storage.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/de8ce683-cbe1-461b-bae7-77db0888ec6d
- https://authoring-docs-microsoft.poolparty.biz/devrel/3439c05e-99ce-45d1-b266-9322ea647316
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/a06cf482-4ca9-4582-a142-bcf842258d42
- https://authoring-docs-microsoft.poolparty.biz/devrel/23472108-2f8d-47d2-b07a-c0b1e9d492b6
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: b491c529-572d-6036-cb3d-fbaab7428e6f
---

# Azure Storage Blob data connector reference for the Codeless Connector Framework - Microsoft Sentinel | Microsoft Learn

To create an Azure Storage Blob data connector with the Codeless Connector Framework (CCF), use this reference in addition to the [Microsoft Sentinel REST API for Data Connectors](/en-us/rest/api/securityinsights/data-connectors/create-or-update) article.

In this ingestion pattern, a producer writes data to Azure Blob Storage. Azure Event Grid sends blob creation events to an Azure Storage queue, where they're buffered until the connector processes them. The connector then reads the blobs and routes their contents through an Azure Monitor data collection rule (DCR) to the destination table. This durable queue-based design supports backpressure handling and resilient ingestion for high-volume data sources.

Each `dataConnector` represents a specific *connection* of a Microsoft Sentinel data connector. One data connector might have multiple connections, which fetch data from different endpoints. The JSON configuration built using this reference document is used to complete the deployment template for the CCF data connector.

For more information, see [Create a codeless connector for Microsoft Sentinel](isv/create-codeless-connector#create-the-deployment-template).

## Build the Azure Storage Blob CCF data connector

Simplify the development of connecting your Azure Storage Blob data source with a sample Storage Blob CCF data connector deployment template. For more information see [Connector StorageBlob CCF template](https://github.com/Azure/Azure-Sentinel/blob/master/DataConnectors/Templates/Connector_StorageBlob_CCF_template.json).

With most of the deployment template sections filled out, you only need to build the first two components, the output table and the DCR. For more information, see the [Output table definition](isv/create-codeless-connector#output-table-definition) and [Data Collection Rule (DCR)](isv/create-codeless-connector#data-collection-rule) sections.

## Data Connectors - Create or update

Reference the [Create or Update](/en-us/rest/api/securityinsights/data-connectors/create-or-update) operation in the REST API docs to find the latest stable or preview API version. The difference between the *create* and the *update* operation is the update requires the **etag** value.

**PUT** method

```http
https://management.azure.com/subscriptions/{{subscriptionId}}/resourceGroups/{{resourceGroupName}}/providers/Microsoft.OperationalInsights/workspaces/{{workspaceName}}/providers/Microsoft.SecurityInsights/dataConnectors/{{dataConnectorId}}?api-version={{apiVersion}}
```

## URI parameters

For more information about the latest API version, see [Data Connectors - Create or Update URI Parameters](/en-us/rest/api/securityinsights/data-connectors/create-or-update#uri-parameters).

| Name | Description |
| --- | --- |
| **dataConnectorId** | The data connector ID must be a unique name and is the same as the `name` parameter in the request body. |
| **resourceGroupName** | The name of the resource group, not case sensitive. |
| **subscriptionId** | The ID of the target subscription. |
| **workspaceName** | The *name* of the workspace, not the ID.Regex pattern: `^[A-Za-z0-9][A-Za-z0-9-]+[A-Za-z0-9]$` |
| **api-version** | The API version to use for this operation. |

## Request body

The request body for a `StorageAccountBlobContainer` CCF data connector has the following structure:

```json
{
   "name": "{{dataConnectorId}}",
   "kind": "StorageAccountBlobContainer",
   "etag": "",
   "properties": {
        "connectorDefinitionName": "",
        "auth": {},
        "request": {},
        "dcrConfig": {},
        "response": {}
   }
}
```

### StorageAccountBlobContainer

**StorageAccountBlobContainer** represents a CCF data connector where the expected response payloads for your Azure Storage Blob data source have already been configured. Configuring your producer to send data to Storage Blob must be done separately.

| Name | Required | Type | Description |
| --- | --- | --- | --- |
| **name** | True | string | The unique name of the connection matching the URI parameter |
| **kind** | True | string | Must be `StorageAccountBlobContainer` |
| **etag** |  | GUID | Leave empty for creation of new connectors. For update operations, the etag must match the existing connector's etag (GUID). |
| properties.**connectorDefinitionName** |  | string | The name of the DataConnectorDefinition resource that defines the UI configuration of the data connector. For more information, see [Data Connector Definition](isv/create-codeless-connector#data-connector-user-interface). |
| properties.**auth** | True | Nested JSON | Describes the credentials for ingesting Azure Storage Blob data. For more information, see authentication configuration. |
| properties.**request** | True | Nested JSON | Describes the Azure Storage queues receiving in-scope blob created events. For more information, see request configuration. |
| properties.**dcrConfig** |  | Nested JSON | Required parameters when the data is sent to a Data Collection Rule (DCR). For more information, see DCR configuration. |
| properties.**response** | True | Nested JSON | Describes the response object and nested message returned from the API when pulling the data. For more information, see response configuration. |

## Authentication configuration

The Azure Storage Blob connector relies on a service principal created in your tenant associated with a Microsoft-managed multitenant application (service principal blueprint). The tenant admin needs to grant consent to create this service principal. The ARM template provides the ability to confirm if the service principal associated with the application already exists in your tenant, and if not, provides an option to create the service principal with the user's consent.

The ARM template example includes operations to apply all necessary role-based access on the storage account to read blobs and contribute to queues. Ensure that the template and the service principals used are associated with the application for your environment and that tenant admin consent has been granted.

The following table lists the application IDs per Azure environment:

| Azure Environment | ApplicationId |
| --- | --- |
| AzureCloud | `4f05ce56-95b6-4612-9d98-a45c8cc33f9f` |

StorageAccountBlobContainer auth example:

```json
"auth": {
    "type": "ServicePrincipal"
}
```

## Request configuration

The request section describes the Azure Storage queues that receive blob created event messages.

Before you configure this section, create the notification and dead-letter queues. Configure an Azure Event Grid subscription on the storage account to send `Microsoft.Storage.BlobCreated` events to the notification queue specified by **QueueUri**. For more information, see [Quickstart: Route Blob storage events to a web endpoint with the Azure portal](/en-us/azure/storage/blobs/storage-blob-event-quickstart).

| Field | Required | Type | Description |
| --- | --- | --- | --- |
| **QueueUri** | True | String | The URI of the Azure Storage queue that receives blob created events. |
| **DlqUri** | True | String | The URI of the dead-letter queue for failed messages. |
| **StorageAccountSubscriptionId** | True | String | The subscription id of the storage account. |
| **StorageAccountResourceGroupName** | True | String | The resource group of the storage account. |

StorageAccountBlobContainer request example:

```json
"request": {
    "QueueUri": "[[concat('https://', variables('storageAccountName'), '.queue.core.windows.net/', variables('queueName'))]",
    "DlqUri": "[[concat('https://', variables('storageAccountName'), '.queue.core.windows.net/', variables('dlqName'))]",
    "StorageAccountSubscriptionId": "[[parameters('StorageAccountSubscription')]",
    "StorageAccountResourceGroupName": "[[parameters('StorageAccountResourceGroupName')]"
}
```

## Response configuration

Define the response handling of your data connector with the following parameters:

| Field | Required | Type | Description |
| --- | --- | --- | --- |
| **EventsJsonPaths** | True | List of Strings | Defines the path to the message in the response JSON. A JSON path expression specifies a path to an element, or a set of elements, in a JSON structure. |
| **IsGzipCompressed** |  | Boolean | Determines whether the response is compressed in a gzip file. |
| **format** | True | String | `json`, `csv`, `xml`, or `parquet` |
| **CompressionAlgo** |  | String | The compression algorithm, either `multi-gzip` or `deflate`. For gzip compression, configure **IsGzipCompressed** to `True` instead of setting a value for this parameter. |
| **CsvDelimiter** |  | String | If the response format is CSV and you want to change the default CSV delimiter of `,`. |
| **HasCsvBoundary** |  | Boolean | Indicates if the CSV data has a boundary. |
| **HasCsvHeader** |  | Boolean | Indicates if the CSV data has a header. Defaults to: `True`. |
| **CsvEscape** |  | String | Escape character for a field boundary. Defaults to: `"`. For example, a CSV with headers `id,name,avg` and a row of data containing spaces like `1,"my name",5.5` requires the `"` field boundary. |

Note

CSV format type is parsed by the [RFC 4180](https://www.rfc-editor.org/rfc/rfc4180) specification.

### Response configuration examples

**Uncompressed JSON:**

```json
"response": {
    "EventsJsonPaths": ["$"],
    "format": "json"
}
```

**Compressed CSV:**

```json
"response": {
    "EventsJsonPaths": ["$"],
    "format": "csv",
    "IsGzipCompressed": true
}
```

**Parquet (compression can be inferred):**

```json
"response": {
    "EventsJsonPaths": ["$"],
    "format": "parquet"
}
```

## DCR configuration

| Field | Required | Type | Description |
| --- | --- | --- | --- |
| **DataCollectionEndpoint** | True | String | DCE (Data Collection Endpoint), for example: `https://example.ingest.monitor.azure.com`. |
| **DataCollectionRuleImmutableId** | True | String | The DCR immutable ID. Find it by viewing the DCR creation response or using the [DCR API](/en-us/rest/api/monitor/data-collection-rules/get). |
| **StreamName** | True | string | This value is the `streamDeclaration` defined in the DCR (prefix must begin with *Custom-*). |

## Example CCF data connector

Here's an example of all the components of the `StorageAccountBlobContainer` CCF data connector JSON together.

```json
{
    "kind": "StorageAccountBlobContainer",
    "properties": {
        "connectorDefinitionName": "[[parameters('connectorDefinitionName')]",
        "dcrConfig": {
            "streamName": "[variables('streamName')]",
            "dataCollectionEndpoint": "[[parameters('dcrConfig').dataCollectionEndpoint]",
            "dataCollectionRuleImmutableId": "[[parameters('dcrConfig').dataCollectionRuleImmutableId]"
        },
        "auth": {
            "type": "ServicePrincipal"
        },
        "request": {
            "QueueUri": "[[concat('https://', variables('storageAccountName'), '.queue.core.windows.net/', variables('queueName'))]",
            "DlqUri": "[[concat('https://', variables('storageAccountName'), '.queue.core.windows.net/', variables('dlqName'))]"
        }
    }
}
```

For more information, see [Create data connector REST API example](/en-us/rest/api/securityinsights/data-connectors/create-or-update).