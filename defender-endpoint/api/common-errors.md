---
layout: Conceptual
title: Common Microsoft Defender for Endpoint API errors - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/common-errors
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: List of common Microsoft Defender for Endpoint API errors with descriptions.
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
ms.date: 2020-12-18T00:00:00.0000000Z
locale: en-us
document_id: fb3ee406-4940-eb55-b8b2-21898abfb629
document_version_independent_id: fb3ee406-4940-eb55-b8b2-21898abfb629
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/common-errors.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/common-errors
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/common-errors.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/86a4b315-a9f1-4577-b985-6fb0e0e67420
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/96ac410d-d052-4707-8007-df31dd0fe041
platformId: 88a9e83f-837c-9573-0473-9c1114175589
---

# Common Microsoft Defender for Endpoint API errors - Microsoft Defender for Endpoint | Microsoft Learn

HTTP error responses are divided into two categories:

- Client error (400-code level) – the client sent an invalid request or the request isn't in accordance with definitions.
- Server error (500-level) – the server temporarily failed to fulfill the request or a server error occurred. Try sending the HTTP request again.

The error codes listed in the following table may be returned by an operation on any of Microsoft Defender for Endpoint APIs.

- In addition to the error code, every error response contains an error message, which can help resolve the problem.
- The message is a free text that can be changed.
- At the bottom of the page, you can find response examples.

| Error code | HTTP status code | Message |
| --- | --- | --- |
| BadRequest | BadRequest (400) | General Bad Request error message. |
| ODataError | BadRequest (400) | Invalid OData URI query (the specific error is specified). |
| InvalidInput | BadRequest (400) | Invalid input {the invalid input}. |
| InvalidRequestBody | BadRequest (400) | Invalid request body. |
| InvalidHashValue | BadRequest (400) | Hash value {the invalid hash} is invalid. |
| InvalidDomainName | BadRequest (400) | Domain name {the invalid domain} is invalid. |
| InvalidIpAddress | BadRequest (400) | IP address {the invalid IP} is invalid. |
| InvalidUrl | BadRequest (400) | URL {the invalid URL} is invalid. |
| MaximumBatchSizeExceeded | BadRequest (400) | Maximum batch size exceeded. Received: {batch size received}, allowed: {batch size allowed}. |
| MissingRequiredParameter | BadRequest (400) | Parameter {the missing parameter} is missing. |
| OsPlatformNotSupported | BadRequest (400) | OS Platform {the client OS Platform} isn't supported for this action. |
| ClientVersionNotSupported | BadRequest (400) | {The requested action} is supported on client version {supported client version} and above. |
| Unauthorized | Unauthorized (401) | Unauthorized (invalid or expired authorization header). |
| Forbidden | Forbidden (403) | Forbidden (valid token but insufficient permission for the action). |
| DisabledFeature | Forbidden (403) | Tenant feature isn't enabled. |
| DisallowedOperation | Forbidden (403) | {the disallowed operation and the reason}. |
| NotFound | Not Found (404) | General Not Found error message. |
| ResourceNotFound | Not Found (404) | Resource {the requested resource} wasn't found. |
| TooManyRequests | Too Many Requests (429) | Response represents reaching quota limit either by number of requests or by CPU. |
| InternalServerError | Internal Server Error (500) | (No error message, retry the operation.) |

## Throttling

The HTTP client may receive a 'Too Many Requests error (429)' when the number of HTTP requests in a given time frame exceeds the allowed number of calls per API.

The HTTP client should delay resubmitting further HTTPS requests and then submit them in a way that complies with the rate limitations. A Retry-After in the response header indicating how long to wait (in seconds) before making a new request

Ignoring the 429 response or trying to resubmit HTTP requests in a shorter time frame gives a return of the 429 error code.

## Body parameters are case-sensitive

The submitted body parameters are currently case-sensitive.

If you experience an **InvalidRequestBody** or **MissingRequiredParameter** errors, it might be caused from a wrong parameter capital or lower-case letter.

Review the API documentation page and check that the submitted parameters match the relevant example.

## Correlation request ID

Each error response contains a unique ID parameter for tracking.

The property name of this parameter is "target".

When contacting us about an error, attaching this ID helps find the root cause of the problem.

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

Tip

Do you want to learn more? Engage with the Microsoft Security community in our Tech Community: [Microsoft Defender for Endpoint Tech Community](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/bd-p/MicrosoftDefenderATP).