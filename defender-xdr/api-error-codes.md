---
layout: Conceptual
title: Common Microsoft Defender XDR REST API error codes - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/api-error-codes
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about the common Microsoft Defender XDRREST API error codes.
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
ms.date: 2025-04-18T00:00:00.0000000Z
locale: en-us
document_id: bfa1ef7a-821b-e81b-c0a5-875ee1292401
document_version_independent_id: bfa1ef7a-821b-e81b-c0a5-875ee1292401
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/api-error-codes.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api-error-codes
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/api-error-codes.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 0ad00b82-29a3-f6f7-25d7-8d2f58cb9a1f
---

# Common Microsoft Defender XDR REST API error codes - Microsoft Defender XDR | Microsoft Learn

Note

**Try our new APIs using MS Graph security API**. Find out more at: [Use the Microsoft Graph security API - Microsoft Graph | Microsoft Learn](/en-us/graph/api/resources/security-api-overview).

Important

Some information relates to prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

Error codes can be returned by an operation on any of the Microsoft Defender APIs. Every error response contains an error message, which can help resolve the problem. The error message column in the table section provides some sample messages. The content of actual messages varies based on the factors that triggered the response. Variable content is indicated by angle brackets (`< >`) in the following table:

## Error codes

| Error code | HTTP status code | Message |
| --- | --- | --- |
| BadRequest | BadRequest (400) | General Bad Request error message. |
| ODataError | BadRequest (400) | Invalid OData URI query &lt;the specific error is specified&gt;. |
| InvalidInput | BadRequest (400) | Invalid input &lt;the invalid input&gt;. |
| InvalidRequestBody | BadRequest (400) | Invalid request body. |
| InvalidHashValue | BadRequest (400) | Hash value &lt;the invalid hash&gt; is invalid. |
| InvalidDomainName | BadRequest (400) | Domain name &lt;the invalid domain&gt; is invalid. |
| InvalidIpAddress | BadRequest (400) | IP address &lt;the invalid IP&gt; is invalid. |
| InvalidUrl | BadRequest (400) | URL &lt;the invalid URL&gt; is invalid. |
| MaximumBatchSizeExceeded | BadRequest (400) | Maximum batch size exceeded. Received: &lt;batch size received&gt;, allowed: {batch size allowed}. |
| MissingRequiredParameter | BadRequest (400) | Parameter &lt;the missing parameter&gt; is missing. |
| OsPlatformNotSupported | BadRequest (400) | OS Platform &lt;the client OS Platform&gt; isn't supported for this action. |
| ClientVersionNotSupported | BadRequest (400) | &lt;The requested action&gt; is supported on client version &lt;supported client version&gt; and later. |
| Unauthorized | Unauthorized (401) | Unauthorized *This error is usually caused by an invalid or expired authorization header.* |
| Forbidden | Forbidden (403) | Forbidden *This error can occur with a valid token but insufficient permission for the action*. |
| DisabledFeature | Forbidden (403) | Tenant feature isn't enabled. |
| DisallowedOperation | Forbidden (403) | &lt;the disallowed operation and the reason&gt;. |
| NotFound | Not Found (404) | General Not Found error message. |
| ResourceNotFound | Not Found (404) | Resource &lt;the requested resource&gt; wasn't found. |
| InternalServerError | Internal Server Error (500) | *If there's no error message, retry the operation. [Contact Microsoft](/en-us/Microsoft-365/admin/get-help-support) if it doesn't get resolved*. |

## Examples

```json
{
    "error": {
        "code": "ResourceNotFound",
        "message": "Machine 123123123 was not found",
        "target": "43f4cb08-8fac-4b65-9db1-745c2ae65f3a"
    }
}
```

```json
{
    "error": {
        "code": "InvalidRequestBody",
        "message": "Request body is incorrect",
        "target": "1fa66c0f-18bd-4133-b378-36d76f3a2ba0"
    }
}
```

## Body parameters

Important

Body parameters are case-sensitive.

If you experience an *InvalidRequestBody* or *MissingRequiredParameter* error, it might be caused by a typo. Review the API documentation and check that the submitted parameters match the relevant example.

## Tracking ID

Each error response contains a unique ID parameter for tracking. The property name of this parameter is *target*. If you contact Microsoft about an error, attaching your tracking ID helps Microsoft find the root cause of the problem.