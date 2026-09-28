---
layout: Conceptual
title: Get live response results - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/get-live-response-result
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to retrieve a specific live response command result by its index.
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
document_id: 583ccb92-9242-b25c-f89b-085e7ff5435e
document_version_independent_id: 583ccb92-9242-b25c-f89b-085e7ff5435e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/get-live-response-result.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/get-live-response-result
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/get-live-response-result.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: f9835d10-2a08-cd0a-45b3-aa9fc4faf156
---

# Get live response results - Microsoft Defender for Endpoint | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Prerequisites

Devices must be running one of the following versions of Windows:

### Supported operating systems

- Windows 11
- Windows 10

    - [Version 1909](/en-us/windows/whats-new/whats-new-windows-10-version-1909) or later
    - [Version 1903](/en-us/windows/whats-new/whats-new-windows-10-version-1903) with [KB4515384](https://support.microsoft.com/servicing/os/windows-10/2019/09/september-10-2019-kb4515384-os-build-18362-356)
    - [Version 1809 (RS 5)](/en-us/windows/whats-new/whats-new-windows-10-version-1809) with [KB4537818](https://support.microsoft.com/servicing/os/windows-10/2020/02/february-25-2020-kb4537818-os-build-17763-1075)
    - [Version 1803 (RS 4)](/en-us/windows/whats-new/whats-new-windows-10-version-1803) with [KB4537795](https://support.microsoft.com/topic/february-25-2020-kb4537795-os-build-17134-1345-36b35e62-d897-2dc3-289c-44a1327c2d8e)
    - [Version 1709 (RS 3)](/en-us/windows/whats-new/whats-new-windows-10-version-1709) with [KB4537816](https://support.microsoft.com/servicing/os/windows-10/2020/02/february-25-2020-kb4537816-os-build-16299-1717)
- Windows Server 2019 - Only applicable for Public preview

    - Version 1903 or (with [KB4515384](https://support.microsoft.com/servicing/os/windows-10/2019/09/september-10-2019-kb4515384-os-build-18362-356)) later
    - Version 1809 (with [KB4537818](https://support.microsoft.com/servicing/os/windows-10/2020/02/february-25-2020-kb4537818-os-build-17763-1075))
- Windows Server 2022 and later
- Azure Stack HCI OS, version 23H2 and later

## API description

Retrieves a specific live response command result by its index.

## Limitations

Rate limitations for this API are 100 calls per minute and 1500 calls per hour.

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Get started](apis-intro).

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Machine.ReadWrite.All | Read and write all machine information |
| Delegated (work or school account) | Machine.LiveResponse | Run live response on a specific machine |

## HTTP request

```HTTP
GET https://api.security.microsoft.com/api/machineactions/{machine action
id}/GetLiveResponseResultDownloadLink(index={command-index})
```

## Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer {token}. Required. |

## Request body

Empty

## Response

If successful, this method returns 200, Ok response code with object that holds the link to the command result in the *value* property. This link is valid for 30 minutes and should be used immediately for downloading the package to a local storage. An expired link can be re-created by another call, and there's no need to run live response again.

*Runscript transcript properties:*

| Property | Description |
| --- | --- |
| script\_name | Executed script name |
| exit\_code | Executed script exit code |
| script\_output | Executed script standard output |
| script\_errors | Executed script standard error output |

## Example

### Request example

Here's an example of the request.

```HTTP
GET https://api.security.microsoft.com/api/machineactions/aaaabbbb-0000-cccc-1111-dddd2222eeee/GetLiveResponseResultDownloadLink(index=0)
```

### Response example

Here's an example of the response.

HTTP/1.1 200 Ok

Content-type: application/json

```JSON
{
    "@odata.context": "https://api.security.microsoft.com/api/$metadata#Edm.String",
    "value": "https://core.windows.net/investigation-actions-data/ID/CustomPlaybookCommandOutput/4ed5e7807ad1fe59b00b664fe06a0f07?se=2021-02-04T16%3A13%3A50Z&sp=r&sv=2019-07-07&sr=b&sig=1dYGe9rPvUlXBPvYSmr6/OLXPY98m8qWqfIQCBbyZTY%3D"
}
```

*File content:*

```JSON
{
    "script_name": "minidump.ps1",
    "exit_code": 0,
    "script_output": "Transcript started, output file is C:\\ProgramData\\Microsoft\\Windows Defender Advanced Threat Protection\\Temp\\PSScriptOutputs\\PSScript_Transcript_{TRANSCRIPT_ID}.txt
C:\\windows\\TEMP\\OfficeClickToRun.dmp.zip\n51 MB\n\u0000\u0000\u0000",
    "script_errors":""
}
```