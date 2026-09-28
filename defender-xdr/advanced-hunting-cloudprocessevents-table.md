---
layout: Conceptual
title: CloudProcessEvents table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-cloudprocessevents-table
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about the CloudProcessEvents table in the advanced hunting schema, which contains information about process events in multicloud hosted environments.
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
document_id: d390b1e8-af94-b294-a76d-ea31e47cbb5e
document_version_independent_id: d390b1e8-af94-b294-a76d-ea31e47cbb5e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-cloudprocessevents-table.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-cloudprocessevents-table
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-cloudprocessevents-table.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 4fc1a037-89b8-c9ab-fba4-2dc04167fa27
---

# CloudProcessEvents table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn

The `CloudProcessEvents` table in the [advanced hunting](advanced-hunting-overview) schema contains information about process events in multicloud hosted environments such as Azure Kubernetes Service, Amazon Elastic Kubernetes Service, and Google Kubernetes Engine as protected by the organization's [Microsoft Defender for Cloud](/en-us/azure/defender-for-cloud/concept-integration-365#advanced-hunting-in-xdr). Use this reference to construct queries that return information from this table.

This advanced hunting table is populated by records from Microsoft Defender for Cloud. If your organization doesn't have Microsoft Defender for Cloud, queries that use the table aren’t going to work or return any results. For more information about prerequisites in integrating Defender for Cloud with Defender, read [Microsoft Defender XDR integration](/en-us/azure/defender-for-cloud/concept-integration-365).

For information on other tables in the advanced hunting schema, see the [advanced hunting reference](advanced-hunting-schema-tables).

| Column name | Data type | Description |
| --- | --- | --- |
| `Timestamp` | `datetime` | Date and time when the event was recorded |
| `AzureResourceId` | `string` | Unique identifier of the Azure resource associated with the process |
| `AwsResourceName` | `string` | Unique identifier specific to Amazon Web Services devices, containing the Amazon resource name |
| `GcpFullResourceName` | `string` | Unique identifier specific to Google Cloud Platform devices, containing a combination of zone and ID for GCP |
| `ContainerImageName` | `string` | The container image name or ID, if it exists |
| `KubernetesNamespace` | `string` | The Kubernetes namespace name |
| `KubernetesPodName` | `string` | The Kubernetes pod name |
| `KubernetesResource` | `string` | Identifier value that includes namespace, resource type and name |
| `ContainerName` | `string` | Name of the container in Kubernetes or another runtime environment |
| `ContainerId` | `string` | The container identifier in Kubernetes or another runtime environment |
| `ActionType` | `string` | Type of activity that triggered the event. See the in-portal schema reference for details. |
| `FileName` | `string` | Name of the file that the recorded action was applied to |
| `FolderPath` | `string` | Folder containing the file that the recorded action was applied to |
| `ProcessId` | `long` | Process ID (PID) of the newly created process |
| `ProcessName` | `string` | The name of the process |
| `ParentProcessName` | `string` | The name of the parent process |
| `ParentProcessId` | `string` | The process ID (PID) of the parent process |
| `ProcessCommandLine` | `string` | Command line used to create the new process |
| `ProcessCreationTime` | `datetime` | Date and time the process was created |
| `ProcessCurrentWorkingDirectory` | `string` | Current working directory of the running process |
| `AccountName` | `string` | User name of the account |
| `LogonId` | `long` | Identifier for a logon session. This identifier is unique on the same pod or container between restarts. |
| `InitiatingProcessId` | `string` | Process ID (PID) of the process that initiated the event |
| `ImageDigest` | `string` | The container's image digest |
| `AgentId` | `string` | The unique identifier of the agent, which is the sensor instance on a node |
| `Region` | `string` | The geographical region where the cluster is located |
| `HostName` | `string` | The node's hostname |
| `AdditionalFields` | `string` | Additional information about the event in JSON array format |

## Sample queries

You can use this table to get detailed information on processes invoked in a cloud environment. The information is useful in hunting scenarios and can discover threats that can be observed through process details, like malicious processes or command-line signatures.

You can also investigate security alerts provided by Defender for Cloud that make use of the cloud process events data in advanced hunting to understand details in the process tree for processes that include a security alert.

### Process events by command-line arguments

To hunt for process events including a given term (represented by "x" in the query below) in the command-line arguments:

```kusto
CloudProcessEvents | where ProcessCommandLine has "x"
```

### Rare process events for a pod in a Kubernetes cluster

To investigate unusual process events invoked as part of a pod in a Kubernetes cluster:

```kusto
CloudProcessEvents | where AzureResourceId = "x" and KubernetesNamespace = "y" and KubernetesPodName = "z" | summarize count() by ProcessName | top 10 by count_ asc
```