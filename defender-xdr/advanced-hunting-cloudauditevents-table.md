---
layout: Conceptual
title: CloudAuditEvents table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-cloudauditevents-table
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about events from Microsoft Defender for Cloud in the CloudAuditEvents table of the advanced hunting schema
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
ms.date: 2026-06-01T00:00:00.0000000Z
locale: en-us
document_id: 8a3255cd-03c3-b609-16cc-14e9c8ba51ff
document_version_independent_id: 8a3255cd-03c3-b609-16cc-14e9c8ba51ff
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-cloudauditevents-table.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-cloudauditevents-table
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-cloudauditevents-table.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 7e74195b-bea6-a855-7cc6-e09bc7cdaaca
---

# CloudAuditEvents table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn

The `CloudAuditEvents` table in the [advanced hunting](advanced-hunting-overview) schema contains information about cloud audit events for various cloud platforms protected by the organization's [Microsoft Defender for Cloud](/en-us/azure/defender-for-cloud/concept-integration-365#advanced-hunting-in-xdr). Use this reference to construct queries that return information from this table.

This advanced hunting table is populated by records from Microsoft Defender for Cloud. If your organization doesn't have Microsoft Defender for Cloud, queries that use the table aren’t going to work or return any results. For more information about prerequisites in integrating Defender for Cloud with Defender, read [Microsoft Defender integration](/en-us/azure/defender-for-cloud/concept-integration-365).

For information on other tables in the advanced hunting schema, [see the advanced hunting reference](advanced-hunting-schema-tables).

| Column name | Data type | Description |
| --- | --- | --- |
| `Timestamp` | `datetime` | Date and time when the event was recorded |
| `ReportId` | `string` | Unique identifier for the event |
| `DataSource` | `string` | Data source for the cloud audit events, can be GCP (for Google Cloud Platform), AWS (for Amazon Web Services), Azure (for Azure Resource Manager), Kubernetes Audit (for Kubernetes), or other cloud platforms |
| `ActionType` | `string` | Type of activity that triggered the event, can be: Unknown, Create, Read, Update, Delete, Other |
| `OperationName` | `string` | Audit event operation name as it appears in the record, usually includes both resource type and operation |
| `ResourceId` | `string` | Unique identifier of the cloud resource accessed |
| `IPAddress` | `string` | The client IP address used to access the cloud resource or control plane |
| `IsAnonymousProxy` | `boolean` | Indicates whether the IP address belongs to a known anonymous proxy (1) or no (0) |
| `CountryCode` | `string` | Two-letter code indicating the country where the client IP address is geolocated |
| `City` | `string` | City where the client IP address is geolocated |
| `Isp` | `string` | Internet service provider (ISP) associated with the IP address |
| `UserAgent` | `string` | User agent information from the web browser or other client application |
| `RawEventData` | `dynamic` | Full raw event information from the data source in JSON format |
| `AdditionalFields` | `dynamic` | Additional information about the audit event |

## Sample query

To get a sample list of VM creation commands performed in the last seven days:

```kusto
CloudAuditEvents
| where Timestamp > ago(7d)
| where OperationName startswith "Microsoft.Compute/virtualMachines/write"
| extend Status = RawEventData["status"], SubStatus = RawEventData["subStatus"]
| sample 10
```