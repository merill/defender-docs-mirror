---
layout: Conceptual
title: machineAction resource type - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/machineaction
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn about the methods and properties of the MachineAction resource type in Microsoft Defender for Endpoint.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.topic: reference
ms.custom: api
ms.subservice: reference
ms.date: 2025-11-13T00:00:00.0000000Z
locale: en-us
document_id: 4ba8e5f6-c6a4-e39a-01dc-fc74d71f166f
document_version_independent_id: 4ba8e5f6-c6a4-e39a-01dc-fc74d71f166f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/machineaction.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/machineaction
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/machineaction.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: bace6047-3ea2-f9b6-587b-e83bc0e73f78
---

# machineAction resource type - Microsoft Defender for Endpoint | Microsoft Learn

- For more information, see [Response Actions](../respond-machine-alerts).

## Properties

| Property | Type | Description |
| --- | --- | --- |
| ID | Guid | Identity of the [Machine Action](machineaction) entity. |
| type | Enum | Type of the action. Possible values are: `RunAntiVirusScan`, `Offboard`, `LiveResponse`, `CollectInvestigationPackage`, `Isolate`, `Unisolate`, `StopAndQuarantineFile`, `RestrictCodeExecution`, and `UnrestrictCodeExecution`. |
| scope | string | Scope of the action. `Full` or `Selective` for Isolation, `Quick` or `Full` for antivirus scan. |
| requestor | String | Identity of the person that executed the action. |
| externalID | String | Id the customer can submit in the request for custom correlation. |
| requestSource | string | The name of the user/application that submitted the action. |
| commands | array | Commands to run. Allowed values are PutFile, RunScript, GetFile. |
| cancellationRequestor | String | Identity of the person that canceled the action. |
| requestorComment | String | Comment that was written when issuing the action. |
| cancellationComment | String | Comment that was written when canceling the action. |
| status | Enum | Current status of the command. Possible values are: `Pending`, `InProgress`, `Succeeded`, `Failed`, `TimeOut`, and `Cancelled`. |
| machineId | String | ID of the [machine](machine) on which the action was executed. |
| computerDnsName | String | Name of the [machine](machine) on which the action was executed. |
| creationDateTimeUtc | DateTimeOffset | The date and time when the action was created. |
| cancellationDateTimeUtc | DateTimeOffset | The date and time when the action was canceled. |
| lastUpdateDateTimeUtc | DateTimeOffset | The last date and time when the action status was updated. |
| title | String | Machine action title. |
| relatedFileInfo | Class | Contains two Properties. string `fileIdentifier`, Enum `fileIdentifierType` with the possible values: `Sha1`, `Sha256`, and `Md5`. |

## Json representation

```json
{
        "id": "5382f7ea-7557-4ab7-9782-d50480024a4e",
        "type": "Isolate",
        "scope": "Selective",
        "requestor": "Analyst@TestPrd.onmicrosoft.com",
        "requestorComment": "test for docs",
        "status": "Succeeded",
        "machineId": "7b1f4967d9728e5aa3c06a9e617a22a4a5a17378",
        "computerDnsName": "desktop-test",
        "creationDateTimeUtc": "2019-01-02T14:39:38.2262283Z",
        "lastUpdateDateTimeUtc": "2019-01-02T14:40:44.6596267Z",
        "relatedFileInfo": null
}
```