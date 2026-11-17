---
layout: Conceptual
title: Update Microsoft Sentinel content to use Advanced Hunting tables | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/transition-advanced-hunting-tables
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
description: Learn how to update Microsoft Sentinel queries and dependent content to use Microsoft Defender XDR Advanced Hunting tables when transitioning an existing Microsoft Sentinel deployment to ISOC.
author: mberdugo
ms.author: monaberdugo
ms.localizationpriority: high
ms.collection:
- m365-security
- tier1
- usx-security
ms.topic: how-to
ai-usage: ai-assisted
ms.date: 2026-11-15T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1032
locale: en-us
document_id: a6b1c2de-7bed-2f65-c84c-97b8836ba90d
document_version_independent_id: 98eb7ef5-b61b-b623-521d-538a6e87bc16
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/transition-advanced-hunting-tables.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/transition-advanced-hunting-tables
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/transition-advanced-hunting-tables.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 98c9781d-cf1c-7618-3360-5f3f85200bb9
---

# Update Microsoft Sentinel content to use Advanced Hunting tables | Microsoft Learn

When you transition Microsoft Sentinel content from workspace-based Microsoft Defender data to Microsoft Defender XDR Advanced Hunting data, review the queries and dependent content that use the affected tables.

Most Microsoft Defender tables have the same name in Microsoft Sentinel and Advanced Hunting, so table references usually don't change. However, some columns and data types work differently and require updates.

Important

Before you stop ingestion, update and validate all dependent queries, detections, workbooks, and automation for all Defender XDR tables. **Configure workspace** stops ingestion for the supported Defender XDR tables at the same time. If ingestion stops first, dependent content might reference data that is no longer arriving in the Microsoft Sentinel workspace.

For the full Advanced Hunting schema, see [Understand the Advanced Hunting schema](/en-us/defender-xdr/advanced-hunting-schema-tables).

## Summary of required updates by workload

The following sections group the affected tables by Microsoft Defender workload. Use the **Update pattern** column to identify the changes that apply to your content.

### Microsoft Defender for Endpoint

| Updates required | Tables | Update pattern |
| --- | --- | --- |
| More content updates | `DeviceInfo` | Pattern 1 and Other column changes |
| More content updates | `DeviceNetworkInfo` | Pattern 2 |
| Some content updates | `DeviceEvents`, `DeviceFileEvents`, `DeviceProcessEvents`, `DeviceLogonEvents`, `DeviceNetworkEvents` | Pattern 1 |
| Minor content updates | `DeviceFileCertificateInfo`, `DeviceImageLoadEvents`, `DeviceRegistryEvents` | Changes that apply to all tables |
| More content updates | [`DisruptionAndResponseEvents`](/en-us/defender-xdr/advanced-hunting-disruptionandresponseevents-table) | Other column changes |

The `MachineGroup` column isn't consistently available or populated across Microsoft Defender XDR endpoint tables. Don't rely on `MachineGroup` for filtering or scoping outside `DeviceInfo`. If your queries, workbooks, analytics rules, or automation use this column, review and validate those implementations in Advanced Hunting before you stop ingestion.

### Microsoft Defender for Office 365

| Updates required | Tables | Update pattern |
| --- | --- | --- |
| More content updates | `EmailEvents` | Pattern 1 and Other column changes |
| Minor content updates | `EmailAttachmentInfo`, `EmailUrlInfo`, `UrlClickEvents` | Changes that apply to all tables |
| More content updates | `EmailPostDeliveryEvents` | Other column changes |
| More content updates | `MessageEvents`, `MessagePostDeliveryEvents`, `MessageUrlInfo` | Microsoft Teams message tables |
| More content updates | [`CallActivityEvents`](/en-us/defender-xdr/advanced-hunting-callactivityevents-table), [`FileMaliciousContentInfo`](/en-us/defender-xdr/advanced-hunting-filemaliciouscontentinfo-table) | Other column changes |
| Minor content updates | [`CampaignInfo`](/en-us/defender-xdr/advanced-hunting-campaigninfo-table) | Changes that apply to all tables |

#### Microsoft Teams message tables

In addition to the changes that apply to all tables, check these column differences:

| Table | Microsoft Sentinel | Advanced Hunting | What to do |
| --- | --- | --- | --- |
| `MessageEvents` | `MessageSubject`, `MessageFormatType`, `MessageFormatSubtype` | Not available | Remove these columns. Use `Subject` for the message subject. |
| `MessageEvents` | `LastEditedTime` (string) | `LastEditedTime` (datetime) | For text comparisons, use `tostring(LastEditedTime)`. |
| `MessagePostDeliveryEvents` | `DetectionMethods` (string) | `DetectionMethods` (dynamic) | For text comparisons, use `tostring(DetectionMethods)`. |
| `MessageUrlInfo` | `ThreatTypes` | Not available | Join with `MessageEvents` on `TeamsMessageId` to get the threat verdict. |
| `MessageUrlInfo` | Not available | `UrlLocation` | You can use this new column. |

This table reflects the schema that Advanced Hunting returns. Columns not listed work the same in both. If a column differs from the schema reference page, run `<TableName> | getschema` in Advanced Hunting to confirm.

For the full schemas, see [MessageEvents](/en-us/defender-xdr/advanced-hunting-messageevents-table), [MessagePostDeliveryEvents](/en-us/defender-xdr/advanced-hunting-messagepostdeliveryevents-table), and [MessageUrlInfo](/en-us/defender-xdr/advanced-hunting-messageurlinfo-table).

### Microsoft Defender for Identity

| Updates required | Tables | Update pattern |
| --- | --- | --- |
| More content updates | `IdentityLogonEvents`, `IdentityDirectoryEvents`, `IdentityQueryEvents` | Pattern 3 |
| Minor content updates | [`IdentityEvents`](/en-us/defender-xdr/advanced-hunting-identityevents-table) | Changes that apply to all tables |

### Microsoft Defender for Cloud Apps and Defender alerts

| Updates required | Tables | Update pattern |
| --- | --- | --- |
| More content updates | `AlertEvidence` | Pattern 1, Pattern 4, and Other column changes |
| Minor content updates | `CloudAppEvents`, `AlertInfo` | Changes that apply to all tables |
| Minor content updates | [`OAuthAppInfo`](/en-us/defender-xdr/advanced-hunting-oauthappinfo-table) | Changes that apply to all tables |

### Microsoft Defender for Cloud

| Updates required | Tables | Update pattern |
| --- | --- | --- |
| More content updates | [`CloudAuditEvents`](/en-us/defender-xdr/advanced-hunting-cloudauditevents-table), [`CloudDnsEvents`](/en-us/defender-xdr/advanced-hunting-clouddnsevents-table), [`CloudProcessEvents`](/en-us/defender-xdr/advanced-hunting-cloudprocessevents-table) | Other column changes |

Note

Defender is still building up 90 days of history for Defender for Cloud tables. Until it does, Advanced Hunting might have less than 90 days of past data for these tables. If you need older data, keep it in Microsoft Sentinel until Advanced Hunting has the history you need.

## Changes that apply to all tables

Review the following changes for every query, detection, workbook, and playbook that you update:

- You don't have to replace `TimeGenerated`. When your Microsoft Sentinel workspace is connected to the Microsoft Defender portal, `TimeGenerated` in Advanced Hunting returns the same value as the table's event time column. In Microsoft Sentinel, `TimeGenerated` can differ slightly from the event time, so results that depend on exact time windows might not match exactly. For new queries, and for custom detections that run in near real time (**Continuous (NRT)** frequency), use `Timestamp`. `CallActivityEvents` doesn't have a `Timestamp` column. For that table, use `ActivityTimestamp`.
- Remove dependencies on Sentinel-only metadata columns such as `TenantId`, `SourceSystem`, `_IsBillable`, and `_BilledSize`.
- For device tables, review dependencies on `MachineGroup`. Don't rely on `MachineGroup` for filtering or scoping outside `DeviceInfo`.
- Update playbooks that query Log Analytics to use the Advanced Hunting API. For more information, see [Update Logic App playbook automation](transition-logic-app-playbooks).
- Validate Microsoft Defender permissions and scoping for analysts, workbook viewers, and automation identities. For more information, see [Update permissions and roles with Unified RBAC](transition-unified-rbac).
- Advanced Hunting tables don't include custom columns that end in `_CF`. These columns are added by a [data collection rule (DCR)](transition-soc-optimization-recommendations#dcr-xdr-tables) in your workspace. If your content uses a `_CF` column, update it before you move it to Advanced Hunting.

## Common update patterns

Only a few schema patterns change between Microsoft Sentinel and Advanced Hunting. Update your content based on the patterns that apply to each table.

### Pattern 1: Dynamic fields become strings

This pattern applies to:

- `DeviceEvents`
- `DeviceFileEvents`
- `DeviceProcessEvents`
- `DeviceLogonEvents`
- `DeviceNetworkEvents`
- `DeviceInfo`
- `EmailEvents`
- `AlertEvidence`

`AdditionalFields`, and `LoggedOnUsers` in `DeviceInfo`, are `dynamic` in Microsoft Sentinel but strings in Advanced Hunting.

Before member access or `mv-expand`, parse the value by using `todynamic()` and `tostring()`.

For example:

```kusto
DeviceInfo
| where Timestamp > ago(24h)
| extend Users = todynamic(tostring(LoggedOnUsers))
| mv-expand Users
| project Timestamp, DeviceName, AccountName = tostring(Users.UserName)
```

### Pattern 2: Dynamic array fields become strings

This pattern applies to the following `DeviceNetworkInfo` fields:

- `IPAddresses`
- `DnsAddresses`
- `ConnectedNetworks`
- `DefaultGateways`

Parse these fields before using `mv-expand` or accessing individual elements.

For example:

```kusto
DeviceNetworkInfo
| where Timestamp > ago(24h)
| extend IPs = todynamic(tostring(IPAddresses))
| mv-expand IPs
| project Timestamp, DeviceName, IPAddress = tostring(IPs.IPAddress)
```

### Pattern 3: Port fields become integers

This pattern applies to:

- `IdentityLogonEvents`
- `IdentityDirectoryEvents`
- `IdentityQueryEvents`

The `Port` and `DestinationPort` fields are strings in Microsoft Sentinel and integers in Advanced Hunting.

For example, a Microsoft Sentinel query might use:

```kusto
| where Port == "3389" or DestinationPort == "445"
```

In Advanced Hunting, normalize the fields by using `toint()`:

```kusto
IdentityLogonEvents
| where Timestamp > ago(24h)
| where toint(Port) == 3389 or toint(DestinationPort) == 445
```

### Pattern 4: SecurityAlert splits into AlertInfo and AlertEvidence

Microsoft Sentinel's `SecurityAlert` table doesn't have a single equivalent in Advanced Hunting.

Alert data is split between:

- `AlertInfo`, which contains one row per alert.
- `AlertEvidence`, which contains one row per entity associated with an alert.

The following fields map between the schemas:

| `SecurityAlert`field | Advanced Hunting | Notes |
| --- | --- | --- |
| `SystemAlertId` | `AlertId` | Join key between `AlertInfo` and `AlertEvidence` |
| `AlertName` | `Title` |  |
| `ProviderName` | `ServiceSource` |  |
| `Entities` | `AlertEvidence` rows | Join the tables instead of using `mv-expand` on `Entities` |

Join `AlertInfo` and `AlertEvidence` on `AlertId` when you need alert information together with related entities.

For example:

```kusto
AlertInfo
| where Timestamp > ago(1h)
| where Title == "Suspicious PowerShell"
| join kind=inner (
    AlertEvidence
    | where Timestamp > ago(1h)
) on AlertId
| extend Fields = todynamic(tostring(AdditionalFields))
| project Timestamp, AlertId, Title, Severity, ServiceSource, EntityType, DeviceId, AccountName
```

### Other column changes

In addition to the changes that apply to all tables, some tables have renamed, removed, or retyped columns in Advanced Hunting. Column names are case-sensitive.

| Table | Microsoft Sentinel | Advanced Hunting |
| --- | --- | --- |
| `CallActivityEvents` | `TimeGenerated` | `TimeGenerated` works and returns the same value as `ActivityTimestamp`. The table doesn't have a `Timestamp` column, so don't change `TimeGenerated` to `Timestamp`. In new queries, use `ActivityTimestamp`. |
| `CallActivityEvents` | `OriginatorUserObjectId` | `OriginatorObjectId` |
| `FileMaliciousContentInfo` | `DetectionMethods` (string) | `DetectionMethods` (dynamic) |
| `EmailEvents` | `LastEventExecutionTime` | Not available. Remove this column from your queries. |
| `EmailPostDeliveryEvents` | `ApproverUpn` | Not available in most tenants. Remove this column from your queries, or use `column_ifexists("ApproverUpn", "")`. |
| `DeviceInfo` | `DeviceObjectId` | Not available. Remove this column from your queries. |
| `AlertEvidence` | `AzureResourceId`, `AzureResourceType`, `AzureSubscriptionId` | `ResourceID`, `ResourceType`, `SubscriptionId` |
| `DisruptionAndResponseEvents` | `DataSources` | `DataSource`. Queries that already use `DataSource` don't need to change. |
| `DisruptionAndResponseEvents` | `InitiatingProcessId` (int) | `InitiatingProcessId` (long) |
| `DisruptionAndResponseEvents` | `Port` (string) | `Port` (int) |
| `DisruptionAndResponseEvents` | `ReportId` (string) | `ReportId` (long) |
| `DisruptionAndResponseEvents` | `MachineGroup` | Present but always empty. Don't use it for filtering or scoping. |
| `CloudAuditEvents` | `CloudResourceId` | Not available. Use `AzureResourceId`, `AwsResourceName`, or `GcpFullResourceName`. |
| `CloudDnsEvents` | `ImageDigest`, `HostName`, `Region` | Might not be available. To check, run `CloudDnsEvents \| getschema` in Advanced Hunting. |
| `CloudProcessEvents` | `ParentProcessId` (string), `InitiatingProcessId` (string) | `ParentProcessId` (long), `InitiatingProcessId` (long) |
| `CloudProcessEvents` | `AdditionalFields` (string) | `AdditionalFields` (dynamic) |

Some `CallActivityEvents` columns, including `OriginatorObjectId`, `CallType`, `CallName`, and the `ActivityRecipient` columns, are available in Advanced Hunting only if your organization has preview features turned on. Before you update content that uses these columns, run `CallActivityEvents | getschema` in Advanced Hunting to check which columns you have.

This table reflects the schema that Advanced Hunting returns. If a column name or type differs from the table's schema reference page, run `<TableName> | getschema` in Advanced Hunting to confirm.

## Validate your updates

Before you stop ingestion in Microsoft Sentinel:

1. **Update queries.** Update hunting and saved queries for the applicable parsing logic, port conversions, and alert joins.
2. **Validate detections.** Confirm that analytics rules and custom detections return the expected results.
3. **Validate workbooks.** Check tiles, filters, and parameters that reference changed columns or data types.
4. **Validate automation.** Test playbooks, Logic Apps, and API integrations against the Advanced Hunting response format, and confirm Microsoft Defender permissions and workload scoping for automation identities.
5. **Stop ingestion.** When all content is updated and validated, stop ingestion for the supported Defender XDR tables. For steps, see [Optimize Microsoft Defender XDR data ingestion](transition-optimize-xdr-ingestion).