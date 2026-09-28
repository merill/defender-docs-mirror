---
layout: Conceptual
title: Get browser extensions permission info - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/get-browser-extensions-permission-info
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Retrieves a list of all permissions required for a browser extension
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
ms.date: 2025-11-10T00:00:00.0000000Z
locale: en-us
document_id: fc12aab8-28aa-b97f-1be9-8c0adb517d1c
document_version_independent_id: fc12aab8-28aa-b97f-1be9-8c0adb517d1c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/get-browser-extensions-permission-info.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/get-browser-extensions-permission-info
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/get-browser-extensions-permission-info.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 3c8e89e9-31ac-200d-03c3-e57adee96f7c
---

# Get browser extensions permission info - Microsoft Defender for Endpoint | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## API description

Retrieves a list of all the permissions requested by a specific browser extension. This is a static data description and would mainly be used to enhance the data returned by the [Export browser extensions assessment API](get-assessment-browser-extensions).

By combining these APIs, you'll be able to see a description of the permissions requested by the browser extensions that come up in the [Export browser extensions assessment](get-assessment-browser-extensions) results.

Supports [OData V4 queries](https://www.odata.org/documentation/). OData supported operators:

- `$filter`on the following properties:
    - `id`
    - `name`
    - `description`
    - `cvssV3`
    - `publishedOn`
    - `severity`
    - `updatedOn`
- `$top` with max value of 10,000.
- `$skip`

See examples at [OData queries with Microsoft Defender for Endpoint](exposed-apis-odata-samples).

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro) for details.

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Software.Read.All | 'Read Threat and Vulnerability Management software information' |
| Delegated (work or school account) | Software.Read | 'Read Threat and Vulnerability Management software information' |

## HTTP request

```http
GET api/browserextensions/permissionsinfo
```

## Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer {token}. **Required**. |

## Request body

Empty

## Response

If successful, this method returns 200 OK with the list of all permissions requested by a browser extension in the body.

## Example

### Request example

Here's an example of the request.

```http
GET https://api.security.microsoft.com/api/browserextensions/permissionsinfo
```

### Response example

Here's an example of the response.

```json
{
    "@odata.context": "https://api.security.microsoft.com/api/$metadata#BrowserExtension",
    "value": [
{
  "value": [
    {
      "key": "audioCapture",
      "permissionName": "Capture audio from attached mic or webcam",
      "description": "Capture audio from attached mic or webcam. Could be used to listen in on use."
    },
    {
      "key": "app.window.fullscreen.overrideEsc",
      "permissionName": "Prevent escape button from exiting fullscreen",
      "description": "Can prevent escape button from exiting fullscreen."
    },
    {
      "key": "browsingData",
      "permissionName": "Clear browsing data",
      "description": "Clears browsing data which could result in a forensics/logging issues."
    },
    {
      "key": "content_security_policy",
      "permissionName": "Can manipulate default Content Security Policy (CSP)",
      "description": "CSP works as a block/allow listing mechanism for resources loaded or executed by your extensions. Can manipulate default CSP."
    }

            ]
}
    ]
```