---
layout: Conceptual
title: List machines API - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/get-machines
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use the List machines API to retrieve a collection of machines that have communicated with Microsoft Defender for Endpoint cloud.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.topic: reference
ms.collection:
- m365-security
- tier3
- must-keep
ms.subservice: reference
ms.custom: api
ms.date: 2026-06-28T00:00:00.0000000Z
locale: en-us
document_id: ce8128a9-d304-d687-fc58-963875dba352
document_version_independent_id: ce8128a9-d304-d687-fc58-963875dba352
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/get-machines.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/get-machines
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/get-machines.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: a0a4cc50-f35b-4050-44b2-6f1874743d64
---

# List machines API - Microsoft Defender for Endpoint | Microsoft Learn

## API description

Retrieves a collection of [Machines](machine) that have communicated with Microsoft Defender for Endpoint.

Supports [OData V4 queries](https://www.odata.org/documentation/). OData supported operators:

- `$filter`on the following properties:
    - `computerDnsName`
    - `id`
    - `version`
    - `deviceValue`
    - `aadDeviceId`
    - `machineTags`
    - `lastSeen`
    - `exposureLevel`
    - `onboardingStatus`
    - `lastIpAddress`
    - `healthStatus`
    - `osPlatform`
    - `riskScore`
    - `rbacGroupId`
- `$top` with max value of 10,000.
- `$skip`

See examples at [OData queries with Defender for Endpoint](exposed-apis-odata-samples)

## Limitations

- You can get devices last seen according to your configured retention period.
- Maximum page size is 10,000.
- Rate limitations for this API are 100 calls per minute and 1,500 calls per hour.

## Permissions

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Machine.Read.All | 'Read all machine profiles' |
| Application | Machine.ReadWrite.All | 'Read and write all machine information' |
| Delegated (work or school account) | Machine.Read | 'Read machine information' |
| Delegated (work or school account) | Machine.ReadWrite | 'Read and write machine information' |

When obtaining a token using user credentials, the user needs to have at least the following role permission: `View Data` (see [Create and manage roles](../user-roles)).

Responses include only devices that the user has access to, based on device group settings (See [Create and manage device groups](../machine-groups)).

Device group creation is supported in Defender for Endpoint Plan 1 and Plan 2.

## HTTP request

```http
GET https://api.security.microsoft.com/api/machines
```

## Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer {token}. **Required**. |

## Request body

Empty

## Response

If successful, and the machines exist, you see `200 OK` with list of [machine](machine) entities in the body. If there are no recent machines, you see `404 Not Found`.

## Example

### Request example

Here's an example of the request.

```http
GET https://api.security.microsoft.com/api/machines
```

### Response example

Here's an example of the response.

```http
HTTP/1.1 200 OK
Content-type: application/json
{
    "@odata.context": "https://api.security.microsoft.com/api/$metadata#Machines",
    "value": [
        {
            "id": "1e5bc9d7e413ddd7902c2932e418702b84d0cc07",
            "computerDnsName": "mymachine1.contoso.com",
            "firstSeen": "2018-08-02T14:55:03.7791856Z",
            "lastSeen": "2018-08-02T14:55:03.7791856Z",
            "osPlatform": "Windows10" "Windows11",
            "version": "1709",
            "osProcessor": "x64",
            "lastIpAddress": "172.17.230.209",
            "lastExternalIpAddress": "167.220.196.71",
            "osBuild": 18209,
            "healthStatus": "Active",
            "rbacGroupId": 140,
            "rbacGroupName": "The-A-Team",
            "riskScore": "Low",
            "exposureLevel": "Medium",
            "isAadJoined": true,
            "aadDeviceId": "80fe8ff8-2624-418e-9591-41f0491218f9",
            "machineTags": [ "test tag 1", "test tag 2" ]
        }
        ...
    ]
}
```