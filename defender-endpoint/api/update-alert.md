---
layout: Conceptual
title: Update alert entity API - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/update-alert
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to update a Microsoft Defender for Endpoint alert by using this API. You can update the status, determination, classification, and assignedTo properties.
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
document_id: f0c2b662-f879-2e60-5907-a2673bccb83c
document_version_independent_id: f0c2b662-f879-2e60-5907-a2673bccb83c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/update-alert.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/update-alert
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/update-alert.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 9c612f98-beb0-3b91-93e6-58a4af8a10aa
---

# Update alert entity API - Microsoft Defender for Endpoint | Microsoft Learn

## API description

Updates properties of existing [Alert](alerts).

Submission of **comment** is available with or without updating properties.

Updatable properties are: `status`, `determination`, `classification`, and `assignedTo`.

## Limitations

- You can update alerts that available in the API. For more information, see [List Alerts](get-alerts).
- Rate limitations for this API are 100 calls per minute and 1,500 calls per hour.

## Permissions

When obtaining a token using user credentials:

- The user needs to have at least the following role permission: 'Alerts investigation'. For more information, see [Create and manage roles](../user-roles).
- The user needs to have access to the device associated with the alert, based on device group settings. For more information, see [Create and manage device groups](../machine-groups).

One of the following permissions is required to call this API. For more information on how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro)

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Alerts.ReadWrite.All | 'Read and write all alerts' |
| Delegated (work or school account) | Alert.ReadWrite | 'Read and write alerts' |

## HTTP request

```http
PATCH /api/alerts/{id}
```

## Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer {token}. **Required**. |
| Content-Type | String | application/json. **Required**. |

## Request body

In the request body, supply the values for the relevant fields that should be updated.

Existing properties that aren't included in the request body will maintain their previous values or be recalculated based on changes to other property values.

For best performance, you shouldn't include existing values that haven't change.

| Property | Type | Description |
| --- | --- | --- |
| Status | String | Specifies the current status of the alert. The property values are: 'New', 'InProgress' and 'Resolved'. |
| assignedTo | String | Owner of the alert |
| Classification | String | Specifies the specification of the alert. The property values are: `TruePositive`, `InformationalExpectedActivity`, and `FalsePositive`. |
| Determination | String | Specifies the determination of the alert. <br>Possible determination values for each classification are: <br>- **True positive**: `Multistage attack` (MultiStagedAttack), `Malicious user activity` (MaliciousUserActivity), `Compromised account` (CompromisedUser) – consider changing the enum name in public API accordingly, `Malware` (Malware), `Phishing` (Phishing), `Unwanted software` (UnwantedSoftware), and `Other` (Other).<br>- **Informational, expected activity:**`Security test` (SecurityTesting), `Line-of-business application` (LineOfBusinessApplication), `Confirmed activity` (ConfirmedActivity) - consider changing the enum name in public API accordingly, and `Other` (Other).<br>- **False positive:**`Not malicious` (NotMalicious) - consider changing the enum name in public API accordingly, `Not enough data to validate` (InsufficientData), and `Other` (Other). |
| Comment | String | Comment to be added to the alert. |

Note

Around August 29, 2022, previously supported alert determination values ('Apt' and 'SecurityPersonnel') will be deprecated and no longer available via the API.

## Response

If successful, this method returns 200 OK, and the [alert](alerts) entity in the response body with the updated properties. If alert with the specified ID wasn't found - 404 Not Found.

## Example

### Request

Here's an example of the request.

```http
PATCH https://api.security.microsoft.com/api/alerts/121688558380765161_2136280442
```

```json
{
    "status": "Resolved",
    "assignedTo": "secop2@contoso.com",
    "classification": "FalsePositive",
    "determination": "Malware",
    "comment": "Resolve my alert and assign to secop2"
}
```