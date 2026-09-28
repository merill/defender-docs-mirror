---
layout: Conceptual
title: Investigation resource type - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/investigation
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Microsoft Defender for Endpoint Investigation entity.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- must-keep
ms.topic: reference
ms.subservice: reference
ms.custom: api
ms.date: 2025-11-11T00:00:00.0000000Z
locale: en-us
document_id: ad4a6e93-8c12-d096-adf1-cb40bdeb7e2b
document_version_independent_id: ad4a6e93-8c12-d096-adf1-cb40bdeb7e2b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/investigation.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/investigation
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/investigation.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: f4220b52-cba0-5623-1611-d12aa02834bd
---

# Investigation resource type - Microsoft Defender for Endpoint | Microsoft Learn

Represent an Automated Investigation entity in Defender for Endpoint.

For more information, see [Overview of automated investigations](../automated-investigations).

## Properties

| Property | Type | Description |
| --- | --- | --- |
| ID | String | Identity of the investigation entity. |
| startTime | DateTime Nullable | The date and time when the investigation was created. |
| endTime | DateTime Nullable | The date and time when the investigation was completed. |
| cancelledBy | String | The ID of the user/application that canceled that investigation. |
| State | Enum | The current state of the investigation. Possible values are: 'Unknown', 'Terminated', 'SuccessfullyRemediated', 'Benign', 'Failed', 'PartiallyRemediated', 'Running', 'PendingApproval', 'PendingResource', 'PartiallyInvestigated', 'TerminatedByUser', 'TerminatedBySystem', 'Queued', 'InnerFailure', 'PreexistingAlert', 'UnsupportedOs', 'UnsupportedAlertType', 'SuppressedAlert'. |
| statusDetails | String | Additional information about the state of the investigation. |
| machineId | String | The ID of the device on which the investigation is executed. |
| computerDnsName | String | The name of the device on which the investigation is executed. |
| triggeringAlertId | String | The ID of the alert that triggered the investigation. |

## Json representation

```json
{
    "id": "63004",
    "startTime": "2020-01-06T13:05:15Z",
    "endTime": null,
    "state": "Running",
    "cancelledBy": null,
    "statusDetails": null,
    "machineId": "e828a0624ed33f919db541065190d2f75e50a071",
    "computerDnsName": "desktop-test123",
    "triggeringAlertId": "da637139127150012465_1011995739"
}
```