---
layout: Conceptual
title: List vulnerabilities by recommendation - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/get-recommendation-vulnerabilities
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Retrieves a list of vulnerabilities associated with the security recommendation.
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
ms.date: 2025-11-13T00:00:00.0000000Z
locale: en-us
document_id: 12973d19-47c4-0c7e-8249-37502bf7213c
document_version_independent_id: 12973d19-47c4-0c7e-8249-37502bf7213c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/get-recommendation-vulnerabilities.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/get-recommendation-vulnerabilities
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/get-recommendation-vulnerabilities.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 55efb024-6c15-897e-8e19-9ed5db66278e
---

# List vulnerabilities by recommendation - Microsoft Defender for Endpoint | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

Retrieves a list of vulnerabilities associated with the security recommendation.

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro) for details.

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Vulnerability.Read.All | 'Read Threat and Vulnerability Management security recommendation information' |
| Delegated (work or school account) | Vulnerability.Read | 'Read Threat and Vulnerability Management security recommendation information' |

## HTTP request

```http
GET /api/recommendations/{id}/vulnerabilities
```

## Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer {token}. **Required**. |

## Request body

Empty

## Response

If successful, this method returns 200 OK, with the list of vulnerabilities associated with the security recommendation.

## Example

### Request example

Here's an example of the request.

```http
GET https://api.security.microsoft.com/api/recommendations/va-_-google-_-chrome/vulnerabilities
```

### Response example

Here is an example of the response.

```json
{
    "@odata.context": "https://api.security.microsoft.com/api/$metadata#Collection(Analytics.Contracts.PublicAPI.PublicVulnerabilityDto)",
    "value": [
        {
            "id": "CVE-2019-13748",
            "name": "CVE-2019-13748",
            "description": "Insufficient policy enforcement in developer tools in Google Chrome prior to 79.0.3945.79 allowed a local attacker to obtain potentially sensitive information from process memory via a crafted HTML page.",
            "severity": "Medium",
            "cvssV3": 6.5,
            "exposedMachines": 0,
            "publishedOn": "2019-12-10T00:00:00Z",
            "updatedOn": "2019-12-16T12:15:00Z",
            "publicExploit": false,
            "exploitVerified": false,
            "exploitInKit": false,
            "exploitTypes": [],
            "exploitUris": []
        }
        ...
     ]
}
```