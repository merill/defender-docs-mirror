---
layout: Conceptual
title: Get all vulnerabilities by machine and software - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/get-all-vulnerabilities-by-machines
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Retrieves a list of all the vulnerabilities affecting the organization by Machine and Software
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
ms.date: 2025-11-16T00:00:00.0000000Z
locale: en-us
document_id: 27577b46-c2ba-b2b4-3614-390f040c7232
document_version_independent_id: 27577b46-c2ba-b2b4-3614-390f040c7232
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/get-all-vulnerabilities-by-machines.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/get-all-vulnerabilities-by-machines
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/get-all-vulnerabilities-by-machines.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/d3197845-b4ce-44c6-a237-cd4be160e76c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/aea905fb-0a9d-4d46-b30f-e9cbaf772d1b
platformId: a87ed1bc-7c62-3d7c-d937-f3763f7f9c32
---

# Get all vulnerabilities by machine and software - Microsoft Defender for Endpoint | Microsoft Learn

Retrieves a list of all the vulnerabilities affecting the organization per [machine](machine) and [software](software).

This API can be used for [Power BI integration](api-power-bi).

- If the vulnerability has a fixing KB, it will appear in the response.
- Supports [OData V4 queries](https://www.odata.org/documentation/). OData supported operators:

    - `$filter`is supported on the following properties:
        - `id`
        - `cveId`
        - `machineId`
        - `fixingKbId`
        - `productName`
        - `productVersion`
        - `severity`
        - `productVendor`
    - `$stop` with max value of 10,000.
    - `$skip`

    See examples at [OData queries with Microsoft Defender for Endpoint](exposed-apis-odata-samples).

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro) for details.

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Vulnerability.Read.All | 'Read Threat and Vulnerability Management vulnerability information' |
| Delegated (work or school account) | Vulnerability.Read | 'Read Threat and Vulnerability Management vulnerability information' |

## HTTP request

```http
GET /api/vulnerabilities/machinesVulnerabilities
```

## Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer {token}. **Required**. |

## Request body

Empty

## Response

If successful, this method returns 200 OK with the list of vulnerabilities in the body.

## Example

### Request example

Here's an example of the request.

```http
GET https://api.security.microsoft.com/api/vulnerabilities/machinesVulnerabilities
```

### Response example

Here's an example of the response.

```json
{
    "@odata.context": "https://api.security.microsoft.com/api/$metadata#Collection(microsoft.windowsDefenderATP.api.PublicAssetVulnerabilityDto)",
    "value": [
        {
            "id": "5afa3afc92a7c63d4b70129e0a6f33f63a427e21-_-CVE-2020-6494-_-microsoft-_-edge_chromium-based-_-81.0.416.77-_-",
            "cveId": "CVE-2020-6494",
            "machineId": "5afa3afc92a7c63d4b70129e0a6f33f63a427e21",
            "fixingKbId": null,
            "productName": "edge_chromium-based",
            "productVendor": "microsoft",
            "productVersion": "81.0.416.77",
            "severity": "Low"
        },
        {
            "id": "7a704e17d1c2977c0e7b665fb18ae6e1fe7f3283-_-CVE-2016-3348-_-microsoft-_-windows_server_2012_r2-_-6.3.9600.19728-_-3185911",
            "cveId": "CVE-2016-3348",
            "machineId": "7a704e17d1c2977c0e7b665fb18ae6e1fe7f3283",
            "fixingKbId": "3185911",
            "productName": "windows_server_2012_r2",
            "productVendor": "microsoft",
            "productVersion": "6.3.9600.19728",
            "severity": "Low"
        },
        ...
    ]

}
```