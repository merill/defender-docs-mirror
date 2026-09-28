---
layout: Conceptual
title: Security baseline assessment methods and properties per device - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/export-security-baseline-assessment
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Provides information about the security baselines APIs that pull "Microsoft Defender Vulnerability Management" data. There are different API calls to get different types of data. In general, each API call contains the requisite data for devices in your organization.
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
document_id: 68c991c3-5e13-c5ed-44dd-fb1947c2789d
document_version_independent_id: 68c991c3-5e13-c5ed-44dd-fb1947c2789d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/export-security-baseline-assessment.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/export-security-baseline-assessment
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/export-security-baseline-assessment.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/de8ce683-cbe1-461b-bae7-77db0888ec6d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/a06cf482-4ca9-4582-a142-bcf842258d42
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 6afb07b1-3a04-bf80-7867-7db0891cf831
---

# Security baseline assessment methods and properties per device - Microsoft Defender for Endpoint | Microsoft Learn

There are different API calls to get different types of data. In general, each API call contains the requisite data for devices in your organization.

- **JSON response** The API pulls all data in your organization as JSON responses. This method is best for *small organizations with less than 100-K devices*. The response is paginated, so you can use the @odata.nextLink field from the response to fetch the next results.
- **via files** This API solution enables pulling larger amounts of data faster and more reliably. So, it's recommended for large organizations, with more than 100-K devices. This API pulls all data in your organization as download files. The response contains URLs to download all the data from Azure Storage. You can download data from Azure Storage as follows:

    - Call the API to get a list of download URLs with all your organization data.
    - Download all the files using the download URLs and process the data as you like.

Data that is collected using either '*JSON response* or *via files*' is the current snapshot of the current state. It doesn't contain historic data. To collect historic data, customers must save the data in their own data storages.

Note

Unless indicated otherwise, all export security baseline assessment methods listed are ***full export*** and ***by device*** (also referred to as ***per device***)

## 1. Export security baselines assessment (JSON response)

### 1.1 API method description

Returns all security baselines assessments for all devices, on a per-device basis. It returns a table with a separate entry for every unique combination of DeviceId, ProfileId, ConfigurationId.

### 1.2 Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro) for details.

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | SecurityBaselinesAssessment.Read.All | 'Read all security baselines assessments information' |
| Delegated (work or school account) | SecurityBaselinesAssessment.Read | 'Read security baselines assessments information' |

### 1.3 Limitations

- Maximum page size is 200,000.
- Rate limitations for this API are 30 calls per minute and 1000 calls per hour.

### 1.4 Parameters

- pageSize (default = 50,000): Number of results in response.
- $top: Number of results to return (doesn't return @odata.nextLink and so doesn't pull all the data).

### 1.5 HTTP request

```http
GET /api/machines/baselineComplianceAssessmentByMachine
```

### 1.6 Properties (JSON response)

Note

Each record is approximately 1 KB of data. You should take this into account when choosing the correct pageSize parameter.

Some additional columns might be returned in the response. These columns are temporary and might be removed. Only use the documented columns.

The properties defined in the following table are listed alphabetically by property ID. When running this API, the resulting output will not necessarily be returned in the same order listed in this table.

| Property (ID) | Data type | Description |
| --- | --- | --- |
| configurationId | String | Unique identifier for a specific configuration in the baseline benchmark. |
| profileId | String | Unique identifier for the profile assessed. |
| deviceId | String | Unique identifier for the device in the service. |
| deviceName | String | Fully qualified domain name (FQDN) of the device. |
| isApplicable | Boolean | Indicates whether the configuration is applicable to this device. |
| isCompliant | Boolean | Indicates whether the device is compliant with configuration. |
| id | String | Unique identifier for the record, which is a combination of DeviceId, ProfileId, and ConfigurationId. |
| osVersion | String | Specific version of the operating system running on the device. |
| osPlatform | String | Operating system platform running on the device. Specific operating systems with variations within the same family, such as Windows 10 and Windows 11. See [MDVM supported operating systems and platforms](/en-us/defender-vulnerability-management/tvm-supported-os) for details. |
| rbacGroupId | Int | The role-based access control (RBAC) group Id. If the device isn't assigned to any RBAC group, the value will be "Unassigned." If the organization doesn't contain any RBAC groups, the value will be "None." |
| rbacGroupName | String | The role-based access control (RBAC) group. If the device isn't assigned to any RBAC group, the value will be "Unassigned." If the organization doesn't contain any RBAC groups, the value will be "None." |
| DataCollectionTimeOffset | DateTime | The time the data was collected from the device. This field may not appear if no data was collected. |
| ComplianceCalculationTimeOffset | DateTime | The time the assessment calculation was made. |
| RecommendedValue | String | Set of expected values for the current device setting to be complaint. |
| CurrentValue | String | Set of detected values found on the device. |
| Source | String | The registry path or other location used to determine the current device setting. |

## 1.7 Example

### 1.7.1 Request example

```http
GET https://api.security.microsoft.com/api/machines/BaselineComplianceAssessmentByMachine
```

### 1.7.2 Response example

```json
{
"@odata.context": " https://api.security.microsoft.com /api/$metadata#Collection(microsoft.windowsDefenderATP.api.AssetBaselineAssessment)",
"value": [
{
    "id": "0000682575d5d473e82ed4d8680425d152411251_9e1b90be-e83e-485b-a5ec-4a429412e734_1.1.1",
    "configurationId": "1.1.1",
    "deviceId": "0000682575d5d473242222425d152411251",
    "deviceName": " ComputerPII_365f5c0bb7202c163937dad3d017969b2d760eb4.DomainPII_29596 ",
    "profileId": "9e1b90be-e83e-485b-a5ec-4a429412e734",
    "osPlatform": "WindowsServer2019",
    "osVersion": "10.0.17763.2330",
    "rbacGroupId": 86,
    "rbacGroupName": "UnassignedGroup",
    "isApplicable": true,
    "isCompliant": false,
    "dataCollectionTimeOffset": "2021-12-22T00:08:02.478Z",
    "recommendedValue": [
                    "Greater than or equal '24'"
                ],
                "currentValue": [
                    "24"
                ],
                "source": [
                    "password_hist_len"
                ],
}
```

## 2. Export security baselines assessment (via files)

### 2.1 API method description

Returns all security baselines assessments for all devices, on a per-device basis. It returns a table with a separate entry for every unique combination of DeviceId, ProfileId, ConfigurationId.

### 2.2 Limitations

- Rate limitations for this API are 5 calls per minute and 20 calls per hour.

### 2.3 URL

```http
GET /api/machines/BaselineComplianceAssessmentExport
```

### 2.4 Parameters

- `sasValidHours`: The number of hours that the download URLs are valid for. Maximum is 6 hours.

### 2.5 Properties (via files)

Note

- The files are GZIP compressed & in multiline JSON format.
- The download URLs are valid for 1 hour unless the `sasValidHours` parameter is used.
- To maximize download speeds, make sure you are downloading the data from the same Azure region where your data resides.
- Some additional columns might be returned in the response. These columns are temporary and might be removed. Only use the documented columns.

| Property (ID) | Data type | Description |
| --- | --- | --- |
| Export files | array[string] | A list of download URLs for files holding the current snapshot of the organization. |
| GeneratedTime | String | The time that the export was generated. |

## 2.6 Examples

### 2.6.1 Request example

```http
GET https://api.security.microsoft.com/api/machines/BaselineComplianceAssessmentExport
```

### 2.6.2 Response example

```json
{
    "@odata.context": "https://api.security.microsoft.com/api/$metadata#microsoft.windowsDefenderATP.api.ExportFilesResponse",
    "exportFiles":
    [
    "https://tvmexportexternalstgeus.blob.core.windows.net/temp-1ebd3d09-d06a-4aad-ab80-ebc536cec61c/2021-12-22/0500/BaselineAssessmentExport/json/OrgId= OrgId=<Org Id>/_RbacGroupId=<Rbac Group Id>/part-00000-c09dfd00-2278-4735-b23a-71733751fcbc.c000.json.gz?sv=ABCD",
   "https://tvmexportexternalstgeus.blob.core.windows.net/temp-1ebd3d09-d06a-4aad-ab80-ebc536cec61c/2021-12-22/0500/BaselineAssessmentExport/json/OrgId=<Org Id>/_RbacGroupId=<Rbac Group Id>/part-00001-c09dfd00-2278-4735-b23a-71733751fcbc.c000.json.gz?sv= ABCD",
    ],
    "generatedTime": "2021-01-11T11:01:00Z"
}
```