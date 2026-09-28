---
layout: Conceptual
title: Cancel machine action API - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/cancel-machine-action
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to cancel an already launched machine action
ms.service: defender-endpoint
ms.subservice: reference
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- must-keep
ms.topic: reference
ms.custom: api
ms.date: 2025-11-13T00:00:00.0000000Z
locale: en-us
document_id: 48edaea2-385b-fb34-3703-5e046ff4ff17
document_version_independent_id: 48edaea2-385b-fb34-3703-5e046ff4ff17
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/cancel-machine-action.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/cancel-machine-action
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/cancel-machine-action.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: b1427c2f-81ca-ca98-efa8-26771a5b956c
---

# Cancel machine action API - Microsoft Defender for Endpoint | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## API description

Cancel an already launched machine action that isn't yet in final state (completed, canceled, failed).

## Limitations

Rate limitations for this API are 100 calls per minute and 1500 calls per hour.

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Get started](apis-intro).

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Machine.CollectForensics  Machine.Isolate  Machine.RestrictExecution  Machine.Scan  Machine.Offboard  Machine.StopAndQuarantine  Machine.LiveResponse | Collect forensics Isolate machineRestrict code execution Scan machine Offboard machine Stop And Quarantine Run live response on a specific machine |
| Delegated (work or school account) | Machine.CollectForensics Machine.Isolate Machine.RestrictExecution Machine.Scan Machine.Offboard Machine.StopAndQuarantineMachine.LiveResponse | Collect forensics Isolate machine Restrict code execution Scan machineOffboard machine Stop And Quarantine Run live response on a specific machine |

## HTTP request

```http
POST https://api.security.microsoft.com/api/machineactions/<machineactionid>/cancel
```

## Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer {token}. Required. |
| Content-Type | string | application/json. Required. |

## Request body

| Parameter | Type | Description |
| --- | --- | --- |
| Comment | String | Comment to associate with the cancellation action. |

## Response

If successful, this method returns 200, OK response code with a Machine Action entity. If machine action entity with the specified id wasn't found - 404 Not Found.

## Example

### Request

Here's an example of the request.

```HTTP
POST
https://api.security.microsoft.com/api/machineactions/aaaabbbb-0000-cccc-1111-dddd2222eeee/cancel
```

```JSON
{
    "Comment": "Machine action was canceled by automation"
}
```