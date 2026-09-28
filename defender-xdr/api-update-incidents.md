---
layout: Conceptual
title: Update incident API - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/api-update-incidents
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to update incidents using Microsoft Defender XDR API
ms.service: defender-xdr
ms.author: edbaynash
author: EdB-MSFT
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- must-keep
ms.topic: reference
ms.custom: api
ms.date: 2025-04-25T00:00:00.0000000Z
locale: en-us
document_id: 39ac86e7-f0cb-5674-a0f9-6906cb125d95
document_version_independent_id: 39ac86e7-f0cb-5674-a0f9-6906cb125d95
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/api-update-incidents.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api-update-incidents
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/api-update-incidents.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: e6831c87-fa02-d666-8511-23693679ac83
---

# Update incident API - Microsoft Defender XDR | Microsoft Learn

Note

**Try our new APIs using MS Graph security API**. Find out more at: [Use the Microsoft Graph security API - Microsoft Graph | Microsoft Learn](/en-us/graph/api/resources/security-api-overview). For information about the new *update incident* API using MS Graph security API, see [Update incident](/en-us/graph/api/security-incident-update).

Important

Some information relates to prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

## API description

Updates properties of existing incident. Updatable properties are: `status`, `determination`, `classification`, `assignedTo`, `tags`, and `comments`.

### Quotas, resource allocation, and other constraints

1. You can make up to 50 calls per minute or 1,500 calls per hour before you hit the throttling threshold.
2. You can set the `determination` property only if `classification` is set to TruePositive.

If your request is throttled, it returns a `429` response code. The response body indicates the time when you can begin making new calls.

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Access the Microsoft Defender APIs](api-access).

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Incident.ReadWrite.All | Read and write all incidents |
| Delegated (work or school account) | Incident.ReadWrite | Read and write incidents |

Note

When obtaining a token using user credentials, the user needs to have permission to update the incident in the portal.

## HTTP request

```HTTP
PATCH /api/incidents/{id}
```

## Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer {token}. **Required**. |
| Content-Type | String | application/json. **Required**. |

## Request body

In the request body, supply the values for the fields that should be updated. Existing properties that aren't included in the request body maintain their values, unless they have to be recalculated due to changes to related values. For best performance, you should omit existing values that didn't change.

| Property | Type | Description |
| --- | --- | --- |
| status | Enum | Specifies the current status of the incident. Possible values are: `Active`, `Resolved`, `InProgress`, and `Redirected`. |
| assignedTo | string | Owner of the incident. |
| classification | Enum | Specification of the incident. Possible values are: `TruePositive` (True positive), `InformationalExpectedActivity` (Informational, expected activity), and `FalsePositive` (False Positive). |
| determination | Enum | Specifies the determination of the incident. <br>Possible determination values for each classification are: <br>- **True positive**: `MultiStagedAttack` (Multi staged attack), `MaliciousUserActivity` (Malicious user activity), `CompromisedAccount` (Compromised account) – consider changing the enum name in public api accordingly, `Malware` (Malware), `Phishing` (Phishing), `UnwantedSoftware` (Unwanted software), and `Other` (Other).<br>- **Informational, expected activity:**`SecurityTesting` (Security test), `LineOfBusinessApplication` (Line-of-business application), `ConfirmedActivity` (Confirmed activity) - consider changing the enum name in public api accordingly, and `Other` (Other).<br>- **False positive:**`Clean` (Not malicious) - consider changing the enum name in public api accordingly, `NoEnoughDataToValidate` (Not enough data to validate), and `Other` (Other). |
| tags | string list | List of Incident tags. |
| comment | string | Comment to be added to the incident. |

Note

Around August 29, 2022, previously supported alert determination values ('Apt' and 'SecurityPersonnel') will be deprecated and no longer available via the API.

## Response

If successful, this method returns `200 OK`. The response body contains the incident entity with updated properties. If an incident with the specified ID wasn't found, the method returns `404 Not Found`.

## Example

### Request example

Here's an example of the request.

```HTTP
 PATCH https://api.security.microsoft.com/api/incidents/{id}
```

### Request data example

```json
{
    "status": "Resolved",
    "assignedTo": "secop2@contoso.com",
    "classification": "TruePositive",
    "determination": "Malware",
    "tags": ["Yossi's playground", "Don't mess with the Zohan"],
    "comment": "pen testing"
}
```