---
layout: Conceptual
title: CloudKeyVaultEvents table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-cloudkeyvaultevents-table
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about the CloudKeyVaultEvents table, which contains Azure Key Vault operations for investigation and threat hunting in Microsoft Defender XDR.
author: EitanBr-2025
ms.author: eitanbremler
ms.service: defender-xdr
ms.subservice: adv-hunting
ms.topic: reference
ms.date: 2026-10-28T00:00:00.0000000Z
ai-usage: ai-assisted
ms.collection:
- m365-security
ms.custom:
- cx-ti
- cx-ah
- msecd-doc-authoring-1032
locale: en-us
document_id: 26e0ebca-4d65-ffba-3dc9-3bcf42423362
document_version_independent_id: 26e0ebca-4d65-ffba-3dc9-3bcf42423362
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-cloudkeyvaultevents-table.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-cloudkeyvaultevents-table
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-cloudkeyvaultevents-table.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f488294d-f483-456e-94e3-755f933b811b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/02662057-0b9b-40f4-a3c7-537125b6d283
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
platformId: f2d1dd14-b747-0940-77bd-4e22695fc838
---

# CloudKeyVaultEvents table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn

The `CloudKeyVaultEvents` table in the [advanced hunting](advanced-hunting-overview) schema contains information about operations performed against Azure Key Vault resources. Use this reference and the sample queries to investigate Key Vault access, caller identities, and operation results in Microsoft Defender XDR.

Important

Some information relates to a prereleased product that might be substantially modified before commercial release. Microsoft makes no warranties, express or implied, with respect to this information.

This advanced hunting table is populated by records from [Microsoft Defender for Cloud](/en-us/azure/defender-for-cloud/concept-integration-365#advanced-hunting-in-xdr). If your organization doesn't have Microsoft Defender for Cloud, queries that use the table won't work or return any results. [Microsoft Defender for Key Vault](/en-us/azure/defender-for-cloud/defender-for-key-vault-introduction) protection must be enabled for the relevant Azure subscriptions. For more information about prerequisites for integrating Defender for Cloud with Microsoft Defender XDR, see [Microsoft Defender XDR integration](/en-us/azure/defender-for-cloud/concept-integration-365).

For information on other tables in the advanced hunting schema, see the [advanced hunting reference](advanced-hunting-schema-tables).

| Column name | Data type | Description |
| --- | --- | --- |
| `Timestamp` | `datetime` | Date and time when the record was generated. |
| `ReportId` | `string` | GUID that identifies the record in this table. |
| `DataSource` | `string` | Source of the Key Vault logs. |
| `SubscriptionId` | `string` | Unique identifier of the Azure subscription. |
| `AzureResourceId` | `string` | Azure resource ID of the key vault. |
| `Location` | `string` | Azure region where the key vault is located. |
| `ActivityName` | `string` | Name of the Key Vault operation performed. |
| `IPAddress` | `string` | IP address from which the key vault was accessed. |
| `HttpStatusCode` | `int` | HTTP status code returned by the Key Vault operation. |
| `ResultSignature` | `string` | Result signature of the Key Vault operation. |
| `AccountTenantId` | `string` | Unique identifier of the Microsoft Entra tenant associated with the accessing account. |
| `AccountApplicationId` | `string` | Application ID associated with the Key Vault access. |
| `AccountType` | `string` | Type of account used to access the key vault. |
| `AccountObjectId` | `string` | Object ID of the identity accessing the key vault. |
| `AccountUpn` | `string` | User principal name of the user accessing the key vault. |
| `RequestUri` | `string` | URI of the Key Vault request. |
| `VaultName` | `string` | Name of the key vault. |
| `UserAgentHeader` | `string` | User-agent string from the HTTP request. |
| `AdditionalFields` | `dynamic` | Additional information about the event in JSON format. |

## Sample queries

These queries are investigation examples, not validated detection rules. A failed request or a high operation count doesn't by itself establish malicious activity.

### Review recent Key Vault operations

List the 100 most recent operations from the past day, including the accessing identity and operation result.

```kusto
CloudKeyVaultEvents
| where Timestamp > ago(1d)
| top 100 by Timestamp desc
| project Timestamp, ReportId, SubscriptionId, AzureResourceId,
    VaultName, ActivityName, AccountType, AccountObjectId,
    AccountUpn, AccountApplicationId, IPAddress,
    HttpStatusCode, ResultSignature, RequestUri
```

### Discover operation names in your environment

Identify the operation names present in the data before creating operation-specific queries.

```kusto
CloudKeyVaultEvents
| where Timestamp > ago(7d)
| summarize Operations = count() by ActivityName
| order by Operations desc
```

### Investigate unauthorized and forbidden requests

Review operations that returned HTTP status code `401` (Unauthorized) or `403` (Forbidden). Use the caller identity, source IP address, and request URI to investigate whether the failures are expected.

```kusto
CloudKeyVaultEvents
| where Timestamp > ago(7d)
| where HttpStatusCode in (401, 403)
| project Timestamp, ReportId, AzureResourceId, VaultName,
    ActivityName, AccountObjectId, AccountUpn,
    AccountApplicationId, IPAddress, HttpStatusCode,
    ResultSignature, RequestUri
| order by Timestamp desc
```

### Find callers with frequent request failures

Find caller and vault combinations with more than 20 requests returning HTTP `4xx` or `5xx` status codes in an hour. Adjust the illustrative threshold to match normal activity in your environment. Group by the resource ID as well as the vault name to distinguish resources across subscriptions.

```kusto
CloudKeyVaultEvents
| where Timestamp > ago(7d)
| where HttpStatusCode between (400 .. 599)
| summarize FailedOperations = count(),
    Activities = make_set(ActivityName, 50)
    by bin(Timestamp, 1h), AzureResourceId, VaultName,
    AccountObjectId, AccountApplicationId, IPAddress
| where FailedOperations > 20
| order by FailedOperations desc
```

### Summarize successful operations by identity and vault

Review successful requests by caller and vault. HTTP `2xx` responses are treated as successful requests in this example.

```kusto
CloudKeyVaultEvents
| where Timestamp > ago(7d)
| where HttpStatusCode between (200 .. 299)
| summarize SuccessfulOperations = count(),
    Activities = make_set(ActivityName, 50),
    SourceIPs = make_set(IPAddress, 50)
    by AzureResourceId, VaultName, AccountObjectId,
    AccountUpn, AccountApplicationId
| order by SuccessfulOperations desc
```