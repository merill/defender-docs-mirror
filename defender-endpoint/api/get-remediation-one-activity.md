---
layout: Conceptual
title: Get one remediation activity by ID - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/get-remediation-one-activity
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Returns information for the specified remediation activity.
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
document_id: ff727981-1cf1-87c7-f9c1-65ac0d8b7986
document_version_independent_id: ff727981-1cf1-87c7-f9c1-65ac0d8b7986
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/get-remediation-one-activity.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/get-remediation-one-activity
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/get-remediation-one-activity.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e7ed706-f5d7-4411-be22-6fcf98d10e44
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/b4084e3b-5e61-4e73-886a-780c8f7b0fa1
platformId: 797a202b-9482-680b-c65e-9e471505cfa3
---

# Get one remediation activity by ID - Microsoft Defender for Endpoint | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## API description

Returns information for the specified remediation activity. Presents the same columns as [Get all remediation activity](get-remediation-all-activities)", but returns results *only for the one specified remediation activity*.

[Learn more about remediation activities](/en-us/defender-vulnerability-management/tvm-remediation).

## List a specified remediation activity for (ID)

**URL:** GET: /api/remediationTasks/{id}

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs for details.](apis-intro)

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | RemediationTasks.Read.All | 'Read Threat and Vulnerability Management vulnerability information' |
| Delegated (work or school account) | RemediationTask.Read.Read | 'Read Threat and Vulnerability Management vulnerability information' |

## Properties

| Property (ID) | Data type | Description | Example of a returned value |
| --- | --- | --- | --- |
| Category | String | Category of the remediation activity (Software/Security configuration) | Software |
| completerEmail | String | If the remediation activity was manually completed by someone, this column contains their email | Null |
| completerId | String | If the remediation activity was manually completed by someone, this column contains their object ID | Null |
| completionMethod | String | A remediation activity can be completed "automatically" (if all the devices are patched) or "manually" by a person who selects "mark as completed" | Automatic |
| createdOn | DateTime | Time this remediation activity was created | 2021-01-12T18:54:11.5499478Z |
| Description | String | Description of this remediation activity | Update Microsoft Silverlight to a later version to mitigate known vulnerabilities affecting your devices. |
| dueOn | DateTime | Due date the creator set for this remediation activity | 2021-01-13T00:00:00Z |
| fixedDevices |  | The number of devices that have been fixed | 2 |
| ID | String | ID of this remediation activity | 097d9735-5479-4899-b1b7-77398899df92 |
| nameId | String | Related product name | Microsoft Silverlight |
| Priority | String | Priority the creator set for this remediation activity (High\Medium\Low) | High |
| productId | String | Related product ID | microsoft-\_-silverlight |
| productivityImpactRemediationType | String | A few configuration changes could be requested only for devices that don't affect users. This value indicates the selection between "all exposed devices" or "only devices with no user impact." | AllExposedAssets |
| rbacGroupNames | String | Related device group names | [ "Windows Servers", "Windows 11", "Windows 10" ] |
| recommendedProgram | String | Recommended program to upgrade to | Null |
| recommendedVendor | String | Recommended vendor to upgrade to | Null |
| recommendedVersion | String | Recommended version to update/upgrade to | Null |
| relatedComponent | String | Related component of this remediation activity (similar to the related component for a security recommendation) | Microsoft Silverlight |
| requesterEmail | String | Creator email address | globaladmin@UserName.contoso.com |
| requesterId | String | Creator object ID | r647211f-2e16-43f2-a480-16ar3a2a796r |
| requesterNotes | String | The notes (free text) the creator added for this remediation activity | Null |
| Scid | String | SCID of the related security recommendation | Null |
| Status | String | Remediation activity status (Active/Completed) | Active |
| statusLastModifiedOn | DateTime | Date when the status field was updated | 2021-01-12T18:54:11.5499487Z |
| targetDevices | Long | Number of exposed devices that this remediation is applicable to | 43 |
| Title | String | Title of this remediation activity | Microsoft Silverlight |
| Type | String | Remediation type | Update |
| vendorId | String | Related vendor name | Microsoft |

## Example

### Request example

```http
GET https://api.security.microsoft.com/api/remediationtasks/aaaabbbb-0000-cccc-1111-dddd2222eeee
```

### Response example

```json
{
    "@odata.context": "https://api.security.microsoft.com/api/$metadata#RemediationTasks/$entity",
    "id": "aaaabbbb-0000-cccc-1111-dddd2222eeee",
    "title": "Update Microsoft Silverlight",
    "createdOn": "2021-02-10T13:20:36.4718166Z",
    "requesterId": "65548a1d-efo0-4a7a-8d19-1b967b5c36f4",
    "requesterEmail": "user1@contoso.com",
    "status": "Active",
    "statusLastModifiedOn": "2021-02-10T13:20:36.4719698Z",
    "description": "Update Silverlight to a later version to mitigate 55 known vulnerabilities affecting your devices. Doing so can help lessen the security risk to your organization due to versions which have reached their end-of-support.",
    "relatedComponent": "Microsoft Silverlight",
    "targetDevices": 18511,
    "rbacGroupNames": [
        "UnassignedGroup",
        "hhh"
    ],
    "fixedDevices": 2866,
    "requesterNotes": "test",
    "dueOn": "2021-02-11T00:00:00Z",
    "category": "Software",
    "productivityImpactRemediationType": null,
    "priority": "Medium",
    "completionMethod": null,
    "completerId": null,
    "completerEmail": null,
    "scid": null,
    "type": "Update",
    "productId": "microsoft-_-silverlight",
    "vendorId": "microsoft",
    "nameId": "silverlight",
    "recommendedVersion": null,
    "recommendedVendor": null,
    "recommendedProgram": null
}
```