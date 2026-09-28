---
layout: Conceptual
title: CloudDnsEvents table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-clouddnsevents-table
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about the CloudDnsEvents table in the advanced hunting schema, which contains information about DNS activity events from cloud infrastructure environments.
search.appverid: met150
ms.service: defender-xdr
ms.subservice: adv-hunting
f1.keywords:
- NOCSH
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
audience: ITPro
ms.collection:
- m365-security
- tier3
ms.custom:
- cx-ti
- cx-ah
ms.topic: reference
ms.date: 2026-06-01T00:00:00.0000000Z
locale: en-us
document_id: 461aa784-4513-3b5f-4bd5-1b0d6f38504f
document_version_independent_id: 461aa784-4513-3b5f-4bd5-1b0d6f38504f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-clouddnsevents-table.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-clouddnsevents-table
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-clouddnsevents-table.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: d360a9a3-a69f-a4c4-4b62-fa3f29bf0144
---

# CloudDnsEvents table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn

The `CloudDnsEvents` table in the [advanced hunting](advanced-hunting-overview) schema contains information about DNS activity events from cloud infrastructure environments. Use this reference to construct queries that return information from this table.

[Microsoft Defender for Cloud](/en-us/azure/defender-for-cloud/concept-integration-365#advanced-hunting-in-xdr) populates this advanced hunting table with records. If your organization doesn't have Defender for Cloud, queries that use the table won't work or return any results. For more information about prerequisites in integrating Defender for Cloud with Defender, see [Microsoft Defender integration](/en-us/azure/defender-for-cloud/concept-integration-365).

For information on other tables in the advanced hunting schema, see [advanced hunting reference](advanced-hunting-schema-tables).

| Column name | Data type | Description |
| --- | --- | --- |
| `Timestamp` | `datetime` | Date and time when the event was recorded |
| `ReportId` | `string` | Unique identifier for the event |
| `ActionType` | `string` | Type of activity that triggered the event |
| `AzureResourceId` | `string` | Unique identifier of the Azure resource associated with the process |
| `AwsResourceName` | `string` | Unique identifier specific to Amazon Web Services devices, containing the Amazon resource name |
| `GcpFullResourceName` | `string` | Unique identifier specific to Google Cloud Platform devices, containing a combination of zone and ID for GCP |
| `KubernetesResource` | `string` | Unique identifier for the Kubernetes resource that includes the namespace, resource type and name |
| `KubernetesNamespace` | `string` | The Kubernetes namespace name |
| `KubernetesPodName` | `string` | The Kubernetes pod name |
| `ContainerName` | `string` | Name of the container in Kubernetes or another runtime environment |
| `ContainerId` | `string` | The container identifier in Kubernetes or another runtime environment |
| `ImageName` | `string` | Container image name or ID |
| `ProcessName` | `string` | The name of the process that initiated the DNS query |
| `ProcessId` | `long` | Process ID that initiated the DNS query |
| `DnsEventType` | `string` | Type of event associated with DNS operation (for example, query) |
| `DnsEventSubType` | `string` | Either request or response |
| `DnsQuery` | `string` | The domain that needs to be resolved |
| `DnsQueryTypeName` | `string` | The DNS resource record type name as defined by the Internet Assigned Numbers Authority (IANA) |
| `DnsResponseCodeName` | `string` | The DNS response code name as defined by the Internet Assigned Numbers Authority (IANA). |
| `DnsNetworkDuration` | `long` | The DNS request duration in milliseconds |
| `TransactionIdHex` | `string` | The DNS unique hex transaction ID |
| `ImageDigest` | `string` | The container's image digest |
| `Region` | `string` | The geographical region where the cluster is located |
| `HostName` | `string` | The node's hostname |
| `AdditionalFields` | `dynamic` | Additional information about the entity or event |

## Sample query

To get the most common DNS queries by a pod in a Kubernetes cluster:

```kusto
CloudDnsEvents
| where AzureResourceId == "<Azure resource ID>"
| where KubernetesNamespace == "<namespace>"
| where KubernetesPodName == "<pod name>"
| where DnsEventSubType == "request"
| summarize count() by DnsQuery
| top 10 by count_ desc
```