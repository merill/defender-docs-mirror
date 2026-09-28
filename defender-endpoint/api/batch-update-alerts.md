---
layout: Conceptual
title: Batch Update alert entities API - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/batch-update-alerts
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to update Microsoft Defender for Endpoint alerts in a batch by using this API. You can update the status, determination, classification, and assignedTo properties.
ms.service: defender-endpoint
ms.subservice: reference
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- must-keep
ms.topic: reference
ms.custom: api
ms.date: 2025-11-11T00:00:00.0000000Z
locale: en-us
document_id: 77b9e805-0b65-2925-3f5f-65d2987b1197
document_version_independent_id: 77b9e805-0b65-2925-3f5f-65d2987b1197
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/batch-update-alerts.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/batch-update-alerts
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/batch-update-alerts.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86a4b315-a9f1-4577-b985-6fb0e0e67420
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/96ac410d-d052-4707-8007-df31dd0fe041
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 30e33b04-48cd-f360-d610-53947744d6c7
---

# Batch Update alert entities API - Microsoft Defender for Endpoint | Microsoft Learn

## API description

Updates properties of a batch of existing [Alerts](alerts).

Submission of **comment** is available with or without updating properties.

Updatable properties are: `status`, `determination`, `classification`, and `assignedTo`.

## Limitations

- You can update alerts that are available in the API. For more information, see [List Alerts](get-alerts).
- Rate limitations for this API are 10 calls per minute and 500 calls per hour.

## Permissions

When obtaining a token using user credentials:

- The user needs to have at least the following role permission: 'Alerts investigation'. For more information, see [Create and manage roles](../user-roles).
- The user needs to have access to the device associated with the alert, based on device group settings. For more information, see [Create and manage device groups](../machine-groups).

One of the following permissions is required to call this API. For more information on how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro)

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Alert.ReadWrite.All | 'Read and write all alerts' |
| Delegated (work or school account) | Alert.ReadWrite | 'Read and write alerts' |

## HTTP request

```http
POST /api/alerts/batchUpdate
```

## Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer {token}. **Required**. |
| Content-Type | String | application/json. **Required**. |

## Request body

In the request body, supply the IDs of the alerts to be updated and the values of the relevant fields that you wish to update for these alerts.

Existing properties that aren't included in the request body will maintain their previous values or be recalculated based on changes to other property values.

For best performance you shouldn't include existing values that haven't changed.

| Property | Type | Description |
| --- | --- | --- |
| alertIds | List&lt;String&gt; | A list of the IDs of the alerts to be updated. **Required** |
| status | String | Specifies the updated status of the specified alerts. The property values are: 'New', 'InProgress' and 'Resolved'. |
| assignedTo | String | Owner of the specified alerts |
| classification | String | Specifies the specification of the specified alerts. The property values are: `TruePositive`, `Informational, expected activity`, and `FalsePositive`. |
| determination | String | Specifies the determination of the specified alerts. <br>Possible determination values for each classification are: <br>- **True positive**: `Multistage attack` (MultiStagedAttack), `Malicious user activity` (MaliciousUserActivity), `Compromised account` (CompromisedUser) – consider changing the enum name in public API accordingly, `Malware` (Malware), `Phishing` (Phishing), `Unwanted software` (UnwantedSoftware), and `Other` (Other).<br>- **Informational, expected activity:**`Security test` (SecurityTesting), `Line-of-business application` (LineOfBusinessApplication), `Confirmed activity` (ConfirmedUserActivity) - consider changing the enum name in public API accordingly, and `Other` (Other).<br>- **False positive:**`Not malicious` (Clean) - consider changing the enum name in public API accordingly, `Not enough data to validate` (InsufficientData), and `Other` (Other). |
| comment | String | Comment to be added to the specified alerts. |

Note

Around August 29, 2022, previously supported alert determination values ('Apt' and 'SecurityPersonnel') will be deprecated and no longer available via the API.

## Response

If successful, this method returns 200 OK, with an empty response body.

## Example

### Request

Here's an example of the request.

```http
POST https://api.security.microsoft.com/api/alerts/batchUpdate
```

```json
{
    "alertIds": ["da637399794050273582_760707377", "da637399989469816469_51697947354"],
    "status": "Resolved",
    "assignedTo": "secop2@contoso.com",
    "classification": "FalsePositive",
    "determination": "Malware",
    "comment": "Resolve my alert and assign to secop2"
}
```