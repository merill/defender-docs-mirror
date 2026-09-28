---
layout: Conceptual
title: Remediation activity methods and properties - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/get-remediation-methods-properties
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: The API response contains Microsoft Defender Vulnerability Management remediation activities created in your tenant. You can request all the remediation activities, only one remediation activity, or information about exposed devices for a selected remediation task.
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
document_id: ae05519d-e0be-4974-a297-6d86c6ac6b1a
document_version_independent_id: ae05519d-e0be-4974-a297-6d86c6ac6b1a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/get-remediation-methods-properties.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/get-remediation-methods-properties
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/get-remediation-methods-properties.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: c95c92ec-b3ca-b1c0-d9e7-6d8414b5f749
---

# Remediation activity methods and properties - Microsoft Defender for Endpoint | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

The API response contains [Microsoft Defender Vulnerability Management](/en-us/defender-vulnerability-management/defender-vulnerability-management) remediation activities that have been created in your tenant. For more information,see: [remediation activities](/en-us/defender-vulnerability-management/tvm-remediation).

## Properties

| Property ID | Data type | Description |
| --- | --- | --- |
| Category | String | Category of the remediation activity (Software/Security configuration) |
| completerEmail | String | If the remediation activity was manually completed by someone, this column contains their email |
| completerId | String | If the remediation activity was manually completed by someone, this column contains their object ID |
| completionMethod | String | A remediation activity can be completed "automatically" (if all the devices are patched) or "manually" by a person who selects "mark as completed." |
| createdOn | DateTime | Time this remediation activity was created |
| Description | String | Description of this remediation activity |
| dueOn | DateTime | Due date the creator set for this remediation activity |
| fixedDevices |  | The number of devices that have been fixed |
| ID | String | ID of this remediation activity |
| nameId | String | Related product name |
| Priority | String | Priority the creator set for this remediation activity (High\Medium\Low) |
| productId | String | Related product ID |
| productivityImpactRemediationType | String | A few configuration changes could be requested only for devices that don't affect users. This value indicates the selection between "all exposed devices" or "only devices with no user impact." |
| rbacGroupNames | String | Related device group names |
| recommendedProgram | String | Recommended program to upgrade to |
| recommendedVendor | String | Recommended vendor to upgrade to |
| recommendedVersion | String | Recommended version to update/upgrade to |
| relatedComponent | String | Related component of this remediation activity (similar to the related component for a security recommendation) |
| requesterEmail | String | Creator email address |
| requesterId | String | Creator object ID |
| requesterNotes | String | The notes (free text) the creator added for this remediation activity |
| Scid | String | SCID of the related security recommendation |
| Status | String | Remediation activity status (Active/Completed) |
| statusLastModifiedOn | DateTime | Date when the status field was updated |
| targetDevices | Long | Number of exposed devices that this remediation is applicable to |
| Title | String | Title of this remediation activity |
| Type | String | Remediation type |
| vendorId | String | Related vendor name |