---
layout: Conceptual
title: Microsoft Purview Information Protection connector reference - audit log record types and activities support in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/microsoft-purview-record-types-activities
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
description: This article lists supported audit log record types and activities when using the Microsoft Purview Information Protection connector with Microsoft Sentinel.
ms.author: guywild
author: guywi-ms
ms.reviewer: ofshezaf
ms.topic: reference
ms.date: 2023-01-02T00:00:00.0000000Z
locale: en-us
document_id: ce8e619d-1af1-e154-6589-49c96ddeaa56
document_version_independent_id: 79931202-2176-8464-1ff8-43dc628c0a2b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/microsoft-purview-record-types-activities.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/microsoft-purview-record-types-activities
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/microsoft-purview-record-types-activities.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/57eae111-0f3b-497e-be07-450fd1409dea
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac8bf8ab-8134-4c9a-9f2e-58b31575b492
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: c66ac898-e428-f66a-4cd2-3124cb007a79
---

# Microsoft Purview Information Protection connector reference - audit log record types and activities support in Microsoft Sentinel | Microsoft Learn

This article lists supported audit log record types and activities when using the Microsoft Purview Information Protection connector with Microsoft Sentinel.

When you use the [Microsoft Purview Information Protection connector](connect-microsoft-purview), you stream audit logs into the`MicrosoftPurviewInformationProtection` standardized table. Data is gathered through the [Office Management API](/en-us/office/office-365-management-api/office-365-management-activity-api-schema), which uses a structured schema.

## Supported audit log record types

| Value | Member | Name | Description | Operations |
| --- | --- | --- | --- | --- |
| 93 | `AipDiscover` | Microsoft Purview scanner events. | Describes the type of access. |  |
| 94 | `AipSensitivityLabelAction` | Microsoft Purview sensitivity label event. | The operation type for the audit log. The name of the user or admin activity for a description of the most common operations: <br>- `SensitivityLabelApplied`<br>- `SensitivityLabelUpdated`<br>- `SensitivityLabelRemoved`<br>- `SensitivityLabelPolicyMatched`<br>- `SensitivityLabeledFileOpened` |  |
| 95 | `AipProtectionAction` | Microsoft Purview protection events. | Contains information related to Microsoft Purview protection events. |  |
| 96 | `AipFileDeleted` | Microsoft Purview file deletion event. | Contains information related to Microsoft Purview file deletion events. |  |
| 97 | `AipHeartBeat` | Microsoft Purview heartbeat event. | The operation type for the audit log. The name of the user or admin activity for a description of the most common operations or activities:<br>- `SensitivityLabelApplied`<br>`SensitivityLabelUpdated`- `SensitivityLabelRemoved`<br>- `SensitivityLabelPolicyMatched`<br>- `SensitivityLabeledFileOpened` |  |
| 43 | `MipLabel` | Events detected in the transport pipeline of email messages that are tagged (manually or automatically) with sensitivity labels. |  |  |
| 82 | `SensitivityLabelPolicyMatch` | Events generated when a file labeled with a sensitive label is opened or renamed. |  |  |
| 83 | `SensitivityLabelAction` | Event generated when sensitivity labels are applied, updated or removed. |  |  |
| 84 | `SensitivityLabeledFileAction` | Events generated when a file labeled with a sensitivity label is opened or renamed. |  |  |
| 71 | `MipAutoLabelSharePointItem` | Auto-labeling events in SharePoint |  |  |
| 72 | `MipAutoLabelSharePointPolicyLocation` | Auto-labeling policy events in SharePoint. |  |  |
| 75 | `MipAutoLabelExchangeItem` | Auto-labeling events in Microsoft Exchange. |  |  |

## Supported activities

| Friendly name | Operation | Description |
| --- | --- | --- |
| Applied sensitivity label to file | `FileSensitivityLabelApplied` | A sensitivity label was applied to a document via Microsoft 365 apps, Office on the web, or an auto-labeling policy. |
| Changed sensitivity label applied to file | `FileSensitivityLabelChanged` | A different sensitivity label was applied to a document. An Office on the web or an auto-labeling policy changed. |
| Removed sensitivity label from file | `FileSensitivityLabelRemoved` | A sensitivity label was removed from a document via Microsoft 365 apps, Office on the web, an auto-labeling policy, or the [Unlock-SPOSensitivityLabelEncryptedFile](/en-us/powershell/module/sharepoint-online/unlock-sposensitivitylabelencryptedFile) cmdlet. |
| Applied sensitivity label to site | `SensitivityLabelApplied` | A sensitivity label was applied to a SharePoint or Teams site. |
| Changed sensitivity label applied to file | `SensitivityLabelUpdated` | A different sensitivity label was applied to a document. |
| Removed sensitivity label from site | `SensitivityLabelRemoved` | A sensitivity label was removed from a SharePoint or Teams site. |
|  | `SiteSensitivityLabelApplied` | A sensitivity label was applied to a SharePoint or Teams site. |
| Changed sensitivity label on a site | `SensitivityLabelChanged` | A different sensitivity label was applied to a SharePoint or Teams site. |
| Removed sensitivity label from site | `SiteSensitivityLabelRemoved` | A sensitivity label was removed from a SharePoint or Teams site. |
| Document | `DocumentSensitivityMismatchDetected` | Non auditable activity. Signals to Substrate that the item was removed from the SharedWithMe view. This is the same as the `RemovedFromSharedWithMe` operation, but without audit. |