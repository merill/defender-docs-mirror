---
layout: Conceptual
title: Microsoft Defender XDR advanced hunting API - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/api-advanced-hunting
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to run advanced hunting queries using Microsoft Defender XDR's advanced hunting API
ms.service: defender-xdr
ms.author: edbaynash
author: EdB-MSFT
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- must-keep
ms.topic: reference
ms.custom: api, msecd-doc-authoring-1015
ms.date: 2026-08-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 58e88b5b-18be-39d6-ad39-625a80651631
document_version_independent_id: 58e88b5b-18be-39d6-ad39-625a80651631
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/api-advanced-hunting.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api-advanced-hunting
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/api-advanced-hunting.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 519b3427-8570-e1e7-212e-a90ad9d2ee0a
---

# Microsoft Defender XDR advanced hunting API - Microsoft Defender XDR | Microsoft Learn

Warning

This advanced hunting API is an older version with limited capabilities. A more comprehensive version of the advanced hunting API is available in the **[Microsoft Graph security API](/en-us/graph/api/resources/security-api-overview)**. For more information, see **[Advanced hunting using Microsoft Graph security API](/en-us/graph/api/resources/security-api-overview#advanced-hunting)**.

The Microsoft Defender XDR advanced hunting API is transitioning to the Microsoft Graph security API, which provides broader data coverage, improved consistency, and better scalability for automation and security workflows. Retirement began in January 2026. After retirement completes, the Microsoft Defender XDR advanced hunting API no longer functions. For the retirement timeline, see [MC1220762](https://admin.microsoft.com/Adminportal/Home#/MessageCenter/:/messages/MC1220762). For migration guidance, see [Use the Microsoft Graph security API](/en-us/graph/api/resources/security-api-overview).

Important

Some information relates to prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

[Advanced hunting](advanced-hunting-overview) is a threat-hunting tool that uses [specially constructed queries](advanced-hunting-query-language) to examine the past 30 days of event data in Microsoft Defender. You can use advanced hunting queries to inspect unusual activity, detect possible threats, and even respond to attacks. The advanced hunting API allows you to programmatically query event data.

## Quotas and resource allocation

The following conditions relate to all queries.

1. Queries explore and return data from the past 30 days.
2. Results can return up to 100,000 rows.
3. You can make up to at least 45 calls per minute per tenant. The number of calls varies per tenant based on its size.
4. Each tenant is allocated CPU resources, based on the tenant size. Queries are blocked if the tenant has reached 100% of the allocated resources until after the next 15-minute cycle. To avoid blocked queries due to excess consumption, follow the guidance in [Optimize your queries to avoid hitting CPU quotas](advanced-hunting-best-practices).
5. If a single request runs for more than three minutes, it times out and returns an error.
6. A `429` HTTP response code indicates that you've reached the allocated CPU resources, either by number of requests sent, or by allotted running time. Read the response body to understand the limit you have reached.

## Permissions

One of the following permissions is required to call the advanced hunting API. To learn more, including how to choose permissions, see [Access the Microsoft Defender Protection APIs](api-access).

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | AdvancedHunting.Read.All | Run advanced queries |
| Delegated (work or school account) | AdvancedHunting.Read | Run advanced queries |

Note

When obtaining a token using user credentials:

- The user needs to have the 'View Data' role.
- The user needs to have access to the device, based on device group settings.

## HTTP request

```HTTP
POST https://api.security.microsoft.com/api/advancedhunting/run
```

## Request headers

| Header | Value |
| --- | --- |
| Authorization | Bearer {token} **Note: required** |
| Content-Type | application/json |

## Request body

In the request body, supply a JSON object with the following parameters:

| Parameter | Type | Description |
| --- | --- | --- |
| Query | Text | The query to run. **(required)** |

## Response

If successful, this method will return `200 OK`, and a *QueryResponse* object in the response body.

The response object contains three top-level properties:

1. Stats - A dictionary of query performance statistics.
2. Schema - The schema of the response, a list of Name-Type pairs for each column.
3. Results - A list of advanced hunting events.

## Example

In the following example, a user sends the query below and receives an API response object containing `Stats`, `Schema`, and `Results`.

### Query

```json
{
    "Query":"DeviceProcessEvents | where InitiatingProcessFileName =~ \"powershell.exe\" | project Timestamp, FileName, InitiatingProcessFileName | order by Timestamp desc | limit 2"
}

```

### Response object

```json
{
    "Stats": {
        "ExecutionTime": 4.621215,
        "resource_usage": {
            "cache": {
                "memory": {
                    "hits": 773461,
                    "misses": 4481,
                    "total": 777942
                },
                "disk": {
                    "hits": 994,
                    "misses": 197,
                    "total": 1191
                }
            },
            "cpu": {
                "user": "00:00:19.0468750",
                "kernel": "00:00:00.0156250",
                "total cpu": "00:00:19.0625000"
            },
            "memory": {
                "peak_per_node": 236822432
            }
        },
        "dataset_statistics": [
            {
                "table_row_count": 2,
                "table_size": 102
            }
        ]
    },
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
        }
    ],
    "Results": [
        {
            "Timestamp": "2020-08-30T06:38:35.7664356Z",
            "FileName": "conhost.exe",
            "InitiatingProcessFileName": "powershell.exe"
        },
        {
            "Timestamp": "2020-08-30T06:38:30.5163363Z",
            "FileName": "conhost.exe",
            "InitiatingProcessFileName": "powershell.exe"
        }
    ]
}
```