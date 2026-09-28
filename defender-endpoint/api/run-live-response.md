---
layout: Conceptual
title: Run live response commands on a device - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/run-live-response
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to run a sequence of live response commands on a device.
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
ms.date: 2025-12-31T00:00:00.0000000Z
locale: en-us
document_id: b4401b01-f376-47a7-5f09-e4adc66af0b7
document_version_independent_id: b4401b01-f376-47a7-5f09-e4adc66af0b7
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/run-live-response.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/run-live-response
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/run-live-response.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/e0ffb20c-01c6-407b-a9bd-29111652a1dc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/3904bce4-d817-48cf-85fd-b6146fca83b7
platformId: 3378c379-2d52-50f4-603a-0c202c89a74d
---

# Run live response commands on a device - Microsoft Defender for Endpoint | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Prerequisites

Before you can initiate a session on a device, make sure you fulfill the following requirements:

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
- macOS [(requires other configuration profiles)](../microsoft-defender-endpoint-mac)

    - 13 (Ventura)
    - 12 (Monterey)
    - 11 (Big Sur)
- Linux servers

    - [Supported Linux distributions](../mde-linux-prerequisites#supported-linux-distributions)

## API description

Runs a sequence of live response commands on a device

## Limitations

- Rate limitations for this API are 10 calls per minute (more requests are responded with HTTP 429).
- 50 concurrently running sessions (requests exceeding the throttling limit receives a "429 - Too many requests" response).
- If the machine isn't available, the session is queued for up to 2 hours.
- RunScript command time-outs after 10 minutes.
- Live response commands can't be queued up and can only be executed one at a time.
- If the machine that you're trying to run this API call is in an RBAC device group that doesn't have an automated remediation level assigned to it, you need to at least enable the minimum Remediation Level for a given Device Group.
- Multiple live response commands can be run on a single API call. However, when a live response command fails all the subsequent actions won't be executed.
- Multiple live response sessions can't be executed on the same machine (if live response action is already running, subsequent requests are responded to with HTTP 400 - ActiveRequestAlreadyExists).
- Live response actions initiated from the Device page aren't available in the `machineactions` API.

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Get started](apis-intro).

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Machine.LiveResponse | Run live response on a specific machine |
| Delegated (work or school account) | Machine.LiveResponse | Run live response on a specific machine |

## HTTP request

```HTTP
POST https://api.security.microsoft.com/API/machines/{machine_id}/runliveresponse
```

## Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer&lt;token&gt;. Required. |
| Content-Type | string | application/json. Required. |

## Request body

| Parameter | Type | Description |
| --- | --- | --- |
| Comment | String | Comment to associate with the action. |
| Commands | Array | Commands to run. Allowed values are PutFile, RunScript, GetFile (must be in this order with no limit on repetitions). |

## Commands

| Command Type | Parameters | Description |
| --- | --- | --- |
| PutFile | Key: FileName  Value: &lt;file name&gt; | Puts a file from the library to the device. Files are saved in a working folder and are deleted when the device restarts by default. NOTE: Doesn't have a response result. |
| RunScript | Key: ScriptName  Value: &lt;Script from library&gt;  Key: Args  Value: &lt;Script arguments&gt; | Runs a script from the library on a device.  The Args parameter is passed to your script.  Time-outs after 10 minutes. |
| GetFile | Key: Path  Value: &lt;File path&gt; | Collect file from a device. NOTE: Backslashes in path must be escaped. |

## Response

- If successful, this method returns `201 Created`.
- Action entity. If machine with the specified ID wasn't found, you see `404 Not Found`.

## Example

### Request example

Here's an example of the request.

```HTTP
POST https://api.security.microsoft.com/api/machines/1e5bc9d7e413ddd7902c2932e418702b84d0cc07/runliveresponse

```JSON
{
   "Commands":[
      {
         "type":"RunScript",
         "params":[
            {
               "key":"ScriptName",
               "value":"minidump.ps1"
            },
            {
               "key":"Args",
               "value":"OfficeClickToRun"
            }

         ]
      },
      {
         "type":"GetFile",
         "params":[
            {
               "key":"Path",
               "value":"C:\\windows\\TEMP\\OfficeClickToRun.dmp.zip"
            }
         ]
      }
   ],
   "Comment":"Testing Live Response API"
}
```

### Response example

Here's an example of the response.

Possible values for each command status are "Created", "Completed", and "Failed".

```HTTP
HTTP/1.1 201 Created
```

Content-type: application/json

```JSON
{
    "@odata.context": "https://api.security.microsoft.com/api/$metadata#MachineActions/$entity",
    "id": "{machine_action_id}",
    "type": "LiveResponse",
    "requestor": "analyst@microsoft.com",
    "requestorComment": "Testing Live Response API",
    "status": "Pending",
    "machineId": "{machine_id}",
    "computerDnsName": "hostname",
    "creationDateTimeUtc": "2021-02-04T15:36:52.7788848Z",
    "lastUpdateDateTimeUtc": "2021-02-04T15:36:52.7788848Z",
    "errorHResult": 0,
    "commands": [
        {
            "index": 0,
            "startTime": null,
            "endTime": null,
            "commandStatus": "Created",
            "errors": [],
            "command": {
                "type": "RunScript",
                "params": [
                    {
                        "key": "ScriptName",
                        "value": "minidump.ps1"
                    },{
                        "key": "Args",
                        "value": "OfficeClickToRun"
                    }
                ]
            }
        }, {
            "index": 1,
            "startTime": null,
            "endTime": null,
            "commandStatus": "Created",
            "errors": [],
            "command": {
                "type": "GetFile",
                "params": [{
                        "key": "Path", "value": "C:\\windows\\TEMP\\OfficeClickToRun.dmp.zip"
                    }
                ]
            }
        }
    ]
}
```