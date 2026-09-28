---
layout: Conceptual
title: Security baselines assessment profiles - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/get-security-baselines-assessment-profiles
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Provides information about the security baselines assessment profiles APIs that pull "Microsoft Defender Vulnerability Management" data. There are different API calls to get different types of data. In general, each API call contains the requisite data for devices in your organization.
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
ms.date: 2025-11-16T00:00:00.0000000Z
locale: en-us
document_id: 5eff4399-92f7-1ad3-137a-b7e494c4b873
document_version_independent_id: 5eff4399-92f7-1ad3-137a-b7e494c4b873
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/get-security-baselines-assessment-profiles.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/get-security-baselines-assessment-profiles
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/get-security-baselines-assessment-profiles.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 6a00d20a-e128-203c-fd05-15fb2552decc
---

# Security baselines assessment profiles - Microsoft Defender for Endpoint | Microsoft Learn

## 1. Get security baselines assessment profiles

This API retrieves a list of all security baselines assessment profiles created by the organization.

### 1.1 Parameters

Supports [OData V4 queries](https://www.odata.org/documentation/). OData supported operators:

- `$filter`on the following properties:
    - `id`
    - `name`
    - `operatingSystem`
    - `operatingSystemVersion`
    - `status`
    - `settingsNumber`
    - `passedDevices`
    - `totalDevices`
- `$top` with max value of 10,000.
- `$skip`

### 1.2 HTTP request

```http
GET:/api/baselineProfiles
```

### 1.3 Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer {token}. **Required**. |

### 1.4 Properties

| Property | Type | Description |
| --- | --- | --- |
| Id | String | Unique identifier for the specific baseline profile. |
| name | String | The profile name. |
| description | String | The profile description. |
| benchmark | String | The profile benchmark. |
| version | String | The profile version. |
| operatingSystem | String | The profile applicable operating system. |
| operatingSystemVersion | String | The profile applicable operating system version. |
| status | Boolean | Indicates whether the profile is active or not |
| complianceLevel | String | The compliance level chosen for the profile. |
| settingsNumber | Int | Number of selected configurations in the profile. |
| createdBy | String | The user that created this profile. |
| lastUpdatedBy | DateTime | The last user to modify this profile. |
| createdOnTimeOffset | DateTime | The date and time the profile was created. |
| lastUpdateTimeOffset | DateTime | The date and time the profile was last updated. |
| passedDevices | Int | The number of devices applicable to this profile that are compliant with all of the profile configurations. |
| totalDevices | Int | Number of devices applicable to this profile. |

## 1.5 Example

### 1.5.1 Request example

```http
GET https://api.security.microsoft.com/api/baselineProfiles
```

### 1.6.2 Response example

```json
{
    "@odata.context": "https:// api.security.microsoft.com/api/$metadata#Collection(microsoft.windowsDefenderATP.api.PublicBaselineProfileDto)",
    "value":
    [
        {
            "id": "02bcbb9d-d197-479e-811e-1cd5a6f9f8fa",
            "name": "Windows 10 build 1909 CIS profile",
            "description": "important",
            "benchmark": "CIS",
            "version": "1.0.0",
            "operatingSystem": "Windows 10",
            "operatingSystemVersion": "1909",
            "status": true,
            "complianceLevel": "Level 1 (L1) - Corporate/Enterprise Environment (general use)",
            "settingsNumber": 51,
            "createdBy": "user@org.net",
            "lastUpdatedBy": null,
            "createdOnTimestampUTC": "0001-01-01T00:00:00Z",
            "lastUpdateTimestampUTC": "0001-01-01T00:00:00Z",
            "passedDevices": 0,
            "totalDevices": 10
        }
     ]
}
```