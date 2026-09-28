---
layout: Conceptual
title: Advanced Hunting API - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/run-advanced-query-api
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
ms.reviewer: 
description: Learn to use the advanced hunting API to run advanced queries on Microsoft Defender for Endpoint. Find out about limitations and see an example.
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
search.appverid: met150
ms.date: 2026-07-28T00:00:00.0000000Z
locale: en-us
document_id: b8bb6415-23ed-02e1-95d6-d78a093f012c
document_version_independent_id: b8bb6415-23ed-02e1-95d6-d78a093f012c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/run-advanced-query-api.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/run-advanced-query-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/run-advanced-query-api.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 5e2d0198-027c-7bac-ed7b-7f81ed783961
---

# Advanced Hunting API - Microsoft Defender for Endpoint | Microsoft Learn

Warning

The Microsoft Defender for Endpoint advanced hunting API is old and has limited capabilities. A more comprehensive version of the advanced hunting API that can query more tables is already available in the **[Microsoft Graph security API](/en-us/graph/api/resources/security-api-overview)**. For more information, see **[Advanced hunting using Microsoft Graph security API](/en-us/graph/api/resources/security-api-overview#advanced-hunting)**.

The Microsoft Defender for Endpoint advanced hunting API is transitioning to the Microsoft Graph security API, which includes advanced hunting capabilities. The Microsoft Graph security API provides broader data coverage, improved consistency, and better scalability for automation and security workflows. Retirement began in January 2026. After retirement completes, the Microsoft Defender for Endpoint advanced hunting API no longer functions. For the retirement timeline, see [MC1220762](https://admin.microsoft.com/Adminportal/Home#/MessageCenter/:/messages/MC1220762). For more information to help with your migration, see **[Use the Microsoft Graph security API](/en-us/graph/api/resources/security-api-overview)**.

Note

If you're a US Government customer, use the URIs listed in [Microsoft Defender for Endpoint for US Government customers](/en-us/defender-endpoint/gov#api).

Tip

For better performance, instead of using api.security.microsoft.com, use a server closer to your geolocation:

- us.api.security.microsoft.com
- eu.api.security.microsoft.com
- uk.api.security.microsoft.com
- au.api.security.microsoft.com
- swa.api.security.microsoft.com
- ina.api.security.microsoft.com
- aea.api.security.microsoft.com

## Limitations

- You can only run a query on data from the last 30 days.
- The results include a maximum of 100,000 rows.
- The number of executions is limited per tenant:

    - API calls: Up to 45 calls per minute, and up to 1,500 calls per hour.
    - Execution time: 10 minutes of running time every hour and 3 hours of running time a day.
- The maximal execution time of a single request is 200 seconds.
- `429` response represents reaching quota limit either by number of requests or by CPU. Read response body to understand what limit was reached.
- The maximum query result size of a single request can't exceed 50 MB. If exceeded, an HTTP 400 Bad Request with the message "Query execution has exceeded the allowed result size. Optimize your query by limiting the number of results and try again" occurs.

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro)

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | AdvancedQuery.Read.All | `Run advanced queries` |
| Delegated (work or school account) | AdvancedQuery.Read | `Run advanced queries` |

Note

When obtaining a token using user credentials:

- The user needs to have the `View Data` role assigned in Microsoft Entra ID.
- The user needs to have access to the device, based on device group settings (See [Create and manage device groups](../machine-groups) for more information).

    Device group creation is supported in Defender for Endpoint Plan 1 and Plan 2.

## HTTP request

```http
POST https://api.security.microsoft.com/api/advancedqueries/run
```

## Request headers

| Header | Value |
| --- | --- |
| Authorization | Bearer {token}. **Required**. |
| Content-Type | application/json |

## Request body

In the request body, supply a JSON object with the following parameters:

| Parameter | Type | Description |
| --- | --- | --- |
| Query | Text | The query to run. **Required**. |

## Response

If successful, this method returns 200 OK, and *QueryResponse* object in the response body.

## Example

### Request example

Here's an example of the request.

```http
POST https://api.security.microsoft.com/api/advancedqueries/run
```

```json
{"Query":"DeviceProcessEvents |where InitiatingProcessFileName =~ 'powershell.exe' |where ProcessCommandLine contains 'appdata'|project Timestamp, FileName, InitiatingProcessFileName, DeviceId|limit 2"}
```

### Response example

Here's an example of the response.

Note

The response object shown here may be truncated for brevity. All of the properties will be returned from an actual call.

```json
{
    "Schema": [
        {
            "Name": "Timestamp",
            "Type": "DateTime"
        },
        {
            "Name": "FileName",
            "Type": "String"
        },
        {
            "Name": "InitiatingProcessFileName",
            "Type": "String"
        },
        {
            "Name": "DeviceId",
            "Type": "String"
        }
    ],
    "Results": [
        {
            "Timestamp": "2020-02-05T01:10:26.2648757Z",
            "FileName": "csc.exe",
            "InitiatingProcessFileName": "powershell.exe",
            "DeviceId": "10cbf9182d4e95660362f65cfa67c7731f62fdb3"
        },
        {
            "Timestamp": "2020-02-05T01:10:26.5614772Z",
            "FileName": "csc.exe",
            "InitiatingProcessFileName": "powershell.exe",
            "DeviceId": "10cbf9182d4e95660362f65cfa67c7731f62fdb3"
        }
    ]
}
```