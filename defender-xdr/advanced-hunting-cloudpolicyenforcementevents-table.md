---
layout: Conceptual
title: CloudPolicyEnforcementEvents table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-cloudpolicyenforcementevents-table
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about the CloudPolicyEnforcementEvents table in the advanced hunting schema, which contains policy enforcement evaluation decisions and metadata of security gating events.
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
ms.date: 2026-03-30T00:00:00.0000000Z
locale: en-us
document_id: ea521e62-f0fa-eda8-881a-273ab5158f11
document_version_independent_id: ea521e62-f0fa-eda8-881a-273ab5158f11
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-cloudpolicyenforcementevents-table.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-cloudpolicyenforcementevents-table
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-cloudpolicyenforcementevents-table.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 1004059b-8c8c-369d-85b8-65586b753e0b
---

# CloudPolicyEnforcementEvents table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn

The `CloudPolicyEnforcementEvents` table in the [advanced hunting](advanced-hunting-overview) schema contains policy enforcement evaluation decisions and metadata of security gating events for various cloud platforms protected by the organization's [Microsoft Defender for Cloud](/en-us/azure/defender-for-cloud/concept-integration-365#advanced-hunting-in-xdr). Use this reference to construct queries that return information from this table.

Important

Some information relates to prereleased product, which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

Defender for Cloud populates this advanced hunting table with records. If your organization doesn't have Microsoft Defender for Cloud, queries that use the table won't work or return any results. For more information about prerequisites in integrating Defender for Cloud with Defender, see [Microsoft Defender XDR integration](/en-us/azure/defender-for-cloud/concept-integration-365).

For information on other tables in the advanced hunting schema, see the [advanced hunting reference](advanced-hunting-schema-tables).

| Column name | Data type | Description |
| --- | --- | --- |
| `Timestamp` | `datetime` | Date and time when the record was generated |
| `ReportId` | `string` | Unique identifier for the event |
| `DataSource` | `string` | Data source of the cloud events; possible values: Google Kubernetes Engine, Elastic Kubernetes Service, or Azure Kubernetes Service |
| `SubscriptionId` | `string` | Unique identifier assigned to the Azure subscription |
| `ActionType` | `string` | Type of activity that resulted from the policy enforcement operation; possible values: Audit, Deny, or Allow |
| `AzureResourceId` | `string` | Unique identifier of the Azure resource associated with the event |
| `AwsResourceName` | `string` | Unique identifier specific to Amazon Web Services devices, containing the Amazon resource name |
| `GcpFullResourceName` | `string` | Unique identifier specific to Google Cloud Platform devices, containing a combination of zone and ID for GCP |
| `Region` | `string` | The region associated with the Kubernetes cluster |
| `ResourceKind` | `string` | Type or kind of Kubernetes resource created or managed (for example, pod or deployment) |
| `ResourceName` | `string` | Name of the Kubernetes resource |
| `KubernetesNamespace` | `string` | The Kubernetes namespace name |
| `Reason` | `string` | Information explaining the action result |
| `AdditionalFields` | `string` | Additional information about the entity or event |