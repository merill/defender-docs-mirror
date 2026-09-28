---
layout: Conceptual
title: CloudStorageAggregatedEvents table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-cloudstorageaggregatedevents-table
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about the CloudStorageAggregatedEvents table in the advanced hunting schema, which contains information about storage activity and related events.
ms.service: defender-xdr
ms.subservice: adv-hunting
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.custom:
- cx-ti
- cx-ah
ms.topic: reference
ms.date: 2025-08-05T00:00:00.0000000Z
locale: en-us
document_id: fe5d078a-2737-6eae-1d32-f62047ba1731
document_version_independent_id: fe5d078a-2737-6eae-1d32-f62047ba1731
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-cloudstorageaggregatedevents-table.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-cloudstorageaggregatedevents-table
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-cloudstorageaggregatedevents-table.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 3f20f50c-027e-5cc6-9322-54256d616e9f
---

# CloudStorageAggregatedEvents table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn

The `CloudStorageAggregatedEvents` table in the [advanced hunting](advanced-hunting-overview) schema contains information about storage activity and related events. Use this reference to construct queries that return information from this table.

Important

Some information relates to prereleased product, which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

This advanced hunting table is populated by records from [Microsoft Defender for Cloud](/en-us/azure/defender-for-cloud/concept-integration-365#advanced-hunting-in-xdr). If your organization doesn't have Microsoft Defender for Cloud, queries that use the table aren’t going to work or return any results. For more information about prerequisites in integrating Defender for Cloud with Defender, read [Microsoft Defender XDR integration](/en-us/azure/defender-for-cloud/concept-integration-365).

For information on other tables in the advanced hunting schema, see the [advanced hunting reference](advanced-hunting-schema-tables).

| Column name | Data type | Description |
| --- | --- | --- |
| `DataAggregationStartTime` | `datetime` | The start time during which the data was aggregated |
| `DataAggregationEndTime` | `datetime` | The end time during which the data was aggregated |
| `DataSource` | `string` | The source of the aggregated logs |
| `SubscriptionId` | `string` | Unique identifier assigned to the Azure subscription |
| `ResourceGroup` | `string` | Name of the resource group where the storage account resides |
| `StorageAccount` | `string` | The identifier for the storage account |
| `StorageContainer` | `string` | The identifier for the storage container |
| `StorageFileShare` | `string` | The identifier for the storage file share |
| `ServiceType` | `string` | Specifies the type of storage service (for example, Blob, ADLS Gen2, Files.REST, Files.SMB) |
| `IpAddress` | `string` | The IP addresses from which the storage was accessed |
| `UserAgentHeader` | `string` | Details of the user agent accessing the storage (for example, browser or application) |
| `OperationNamesList` | `object` | A list of storage operations performed (for example, CreateContainer, DeleteContainer) |
| `AuthenticationType` | `string` | The authentication method used to access the storage (for example, AccountKey, SAS, Oauth) |
| `AccountObjectId` | `string` | The unique identifier of the object is making the storage access |
| `AccountTenantId` | `long` | The unique identifier of the Azure tenant |
| `AccountApplicationId` | `string` | The application ID associated with the storage access |
| `AccountUpn` | `string` | The user principal name of the accessing user |
| `AccountType` | `long` | The account type used |
| `OperationsCount` | `int` | The total number of storage operations performed |
| `SuccessfulOperationsCount` | `int` | The count of successful storage operations |
| `FailedOperationsCount` | `int` | The count of failed storage operations |
| `TotalResponseLength` | `int` | The total response length of all GET operations during the aggregation period |
| `SuccessfulReadOperations` | `int` | The count of successful read operations |
| `DistinctGetOperations` | `int` | The count of distinct GET operations performed |
| `AnonymousSuccessfulOperations` | `int` | The count of successful anonymous operations |
| `HasAnonymousResourceNotFoundFailures` | `bool` | Indicates whether anonymous resource not found failures occurred |
| `Md5Hashes` | `object` | A list of all objects written and additional information (for example, MD5 hashes, object name, etc) |
| `AzureResourceId` | `string` | The Azure Resource ID of the storage account |
| `Location` | `string` | The location of the storage account (region) |
| `Timestamp` | `datetime` | Indicate the time when the record was generated |
| `ReportId` | `string` | GUID to identify the record in the specific table |
| `ActionType` | `string` | Type of action (aggregated logs) |
| `AdditionalFields` | `dynamic` | Additional information about the event in JSON array format |

## Sample queries

To detect failed anonymous authentication attempts:

```kusto
CloudStorageAggregatedEvents
| where FailedOperationsCount > 0
| where AuthenticationType == "Anonymous"
| project StorageAccount, FailedOperationsCount, OperationNamesList, AdditionalFields
```

To list unusual authentication methods used:

```kusto
// Define a list of expected authentication types
let ExpectedAuthTypes = dynamic(["AccountKey", "SAS", "Oauth"]);
CloudStorageAggregatedEvents
| where DataAggregationEndTime >= ago(7d)
| where not(AuthenticationType in (ExpectedAuthTypes))
| summarize TotalOperations = sum(OperationsCount) by StorageAccount, AuthenticationType
```

To find storage accounts with a high number of failed operations:

```kusto
CloudStorageAggregatedEvents
| where DataAggregationEndTime >= ago(7d)
| summarize TotalFailedOperations = sum(FailedOperationsCount) by StorageAccount
| where TotalFailedOperations > 100
| order by TotalFailedOperations desc
```

To monitor anonymous successful operations:

```kusto
CloudStorageAggregatedEvents
| where DataAggregationEndTime >= ago(7d)
| where AuthenticationType == "Anonymous" and SuccessfulOperationsCount > 0
| project StorageAccount, SuccessfulOperationsCount, OperationNamesList, AdditionalFields
```

To detect access to sensitive containers or file shares:

```kusto
CloudStorageAggregatedEvents
| where DataAggregationEndTime >= ago(7d)
| where AuthenticationType == "Anonymous" and SuccessfulOperationsCount > 0
| project StorageAccount, SuccessfulOperationsCount, OperationNamesList, AdditionalFields
```

To detect suspicious file uploads with known malicious hashes:

```kusto
CloudStorageAggregatedEvents
| where DataAggregationEndTime >= ago(7d)
| where isnotempty(Md5Hashes)
| mv-expand HashReputation = Md5Hashes
| extend HashDetails = parse_json(HashReputation)
| project StorageAccount, AccountUpn, OperationNamesList, HashMd5 = HashDetails.md5Hash, ResourcePath = HashDetails.resourcePath, OperationType = HashDetails.operationType, ETag = HashDetails.etag
```