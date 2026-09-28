---
layout: Conceptual
title: Export secure configuration assessment per device - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/get-assessment-secure-config
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Returns  an entry for every unique combination of DeviceId, ConfigurationId.
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
ms.date: 2025-11-04T00:00:00.0000000Z
locale: en-us
document_id: 3ba5fe93-3536-12b5-1bfe-1012ac97f9c0
document_version_independent_id: 3ba5fe93-3536-12b5-1bfe-1012ac97f9c0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/get-assessment-secure-config.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/get-assessment-secure-config
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/get-assessment-secure-config.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/de8ce683-cbe1-461b-bae7-77db0888ec6d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/a06cf482-4ca9-4582-a142-bcf842258d42
platformId: 7493f1e7-06e7-e5b1-ea61-769dc8c3d456
---

# Export secure configuration assessment per device - Microsoft Defender for Endpoint | Microsoft Learn

Returns all of the configurations and their status, on a per-device basis. Unless indicated otherwise, all export assessment methods listed are ***full export*** and ***by device*** (also referred to as ***per device***)

There are different API calls to get different types of data. Because the amount of data can be large, there are two ways it can be retrieved:

- Export secure configuration assessment **JSON response**: The API pulls all data in your organization as Json responses. This method is best for *small organizations with less than 100-K devices*. The response is paginated, so you can use the @odata.nextLink field from the response to fetch the next results.
- Export secure configuration assessment **via files**: This API solution enables pulling larger amounts of data faster and more reliably. Therefore, it is recommended for large organizations, with more than 100-K devices. This API pulls all data in your organization as download files. The response contains URLs to download all the data from Azure Storage. This API enables you to download all your data from Azure Storage as follows:

    - Call the API to get a list of download URLs with all your organization data.
    - Download all the files using the download URLs and process the data as you like.

Data that is collected (using either *JSON response* or *via files*) is the current snapshot of the current state, and does not contain historic data. In order to collect historic data, customers must save the data in their own data storages.

## 1. Export secure configuration assessment (JSON response)

### 1.1 API method description

This API response contains the Secure Configuration Assessment on your exposed devices, and returns an entry for every unique combination of DeviceId, ConfigurationId.

#### 1.1.1 Limitations

- Maximum page size is 200,000.
- Rate limitations for this API are 30 calls per minute and 1000 calls per hour.

### 1.2 Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro) for details.

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Vulnerability.Read.All | 'Read Threat and Vulnerability Management vulnerability information' |
| Delegated (work or school account) | Vulnerability.Read | 'Read Threat and Vulnerability Management vulnerability information' |

### 1.3 URL

```http
GET /api/machines/SecureConfigurationsAssessmentByMachine
```

### 1.4 Parameters

- pageSize (default = 50,000): Number of results in response.
- $top: Number of results to return (doesn't return @odata.nextLink and therefore doesn't pull all the data).

### 1.5 Properties

- The properties defined in the following table are listed alphabetically, by property ID. When running this API, the resulting output will not necessarily be returned in the same order listed in this table.
- Some additional columns might be returned in the response. These columns are temporary and might be removed, please use only the documented columns.

| Property (ID) | Data type | Description | Example of a returned value |
| --- | --- | --- | --- |
| ConfigurationCategory | string | Category or grouping to which the configuration belongs: Application, OS, Network, Accounts, Security controls | Security controls |
| ConfigurationId | string | Unique identifier for a specific configuration | scid-10000 |
| ConfigurationImpact | string | Rated impact of the configuration to the overall configuration score (1-10) | 9 |
| ConfigurationName | string | Display name of the configuration | Onboard devices to Microsoft Defender for Endpoint |
| ConfigurationSubcategory | string | Subcategory or subgrouping to which the configuration belongs. In many cases, this describes specific capabilities or features. | Onboard Devices |
| DeviceId | string | Unique identifier for the device in the service. | 9eaf3a8b5962e0e6b1af9ec756664a9b823df2d1 |
| DeviceName | string | Fully qualified domain name (FQDN) of the device. | johnlaptop.europe.contoso.com |
| IsApplicable | bool | Indicates whether the configuration or policy is applicable | true |
| IsCompliant | bool | Indicates whether the configuration or policy is properly configured | false |
| IsExpectedUserImpact | bool | Indicates whether there will be user impact if the configuration will be applied | true |
| OSPlatform | string | Platform of the operating system running on the device. This indicates specific operating systems, including variations within the same family, such as Windows 10 and Windows 11. See Microsoft Defender Vulnerability Management (MDVM) supported operating systems and platforms for details. | Windows10 and Windows 11 |
| RbacGroupName | string | The role-based access control (RBAC) group. If this device is not assigned to any RBAC group, the value will be "Unassigned." If the organization doesn't contain any RBAC groups, the value will be "None." | Servers |
| RecommendationReference | string | A reference to the recommendation ID related to this software. | sca-\_-scid-20000 |
| Timestamp | string | Last time the configuration was seen on the device | 2020-11-03 10:13:34.8476880 |

### 1.6 Examples

#### 1.6.1 Request example

```http
GET https://api.security.microsoft.com/api/machines/SecureConfigurationsAssessmentByMachine?pageSize=5
```

#### 1.6.2 Response example

```json
{
    "@odata.context": "api.security.microsoft.com/api/$metadata#Collection(microsoft.windowsDefenderATP.api.AssetConfiguration)",
    "value": [
        {
            "deviceId": "00013ee62c6b12345b10214e1801b217b50ab455c293d",
            "rbacGroupName": "hhh",
            "deviceName": "ComputerPII_5d96860d69c73fdd06fc8d1679e1eb73eceb8330",
            "osPlatform": "Windows10" "Windows11",
            "osVersion": "NT kernel 6.x",
            "timestamp": "2021-01-11 09:47:58.854",
            "configurationId": "scid-10000",
            "configurationCategory": "Network",
            "configurationSubcategory": "",
            "configurationImpact": 5,
            "isCompliant": true,
            "isApplicable": true,
            "isExpectedUserImpact": false,
            "configurationName": "Disable insecure administration protocol - Telnet",
            "recommendationReference": "sca-_-scid-10000"
        },
        {
            "deviceId": "0002a1be533813b9a8c6de739785365bce7910",
            "rbacGroupName": "hhh",
            "deviceName": null,
            "osPlatform": "Windows10" "Windows11",
            "osVersion": "10.0",
            "timestamp": "2021-01-11 09:47:58.854",
            "configurationId": "scid-20000",
            "configurationCategory": "Security controls",
            "configurationSubcategory": "Onboard Devices",
            "configurationImpact": 9,
            "isCompliant": false,
            "isApplicable": true,
            "isExpectedUserImpact": false,
            "configurationName": "Onboard devices to Microsoft Defender for Endpoint",
            "recommendationReference": "sca-_-scid-20000"
        },
        {
            "deviceId": "0002a1de123456a8c06de736785395d4ce7610",
            "rbacGroupName": "hhh",
            "deviceName": null,
            "osPlatform": "Windows10" "Windows11",
            "osVersion": "10.0",
            "timestamp": "2021-01-11 09:47:58.854",
            "configurationId": "scid-10000",
            "configurationCategory": "Network",
            "configurationSubcategory": "",
            "configurationImpact": 5,
            "isCompliant": true,
            "isApplicable": true,
            "isExpectedUserImpact": false,
            "configurationName": "Disable insecure administration protocol - Telnet",
            "recommendationReference": "sca-_-scid-10000"
        },
        {
            "deviceId": "00044f912345bdaf756492dbe6db733b6a9c59ab4",
            "rbacGroupName": "hhh",
            "deviceName": "ComputerPII_18663d45912eed224b2be2f5ea3142726e63f16a.DomainPII_21eeb80b086e76bdfa178eadfa25e8de9acfa346.corp.contoso.com",
            "osPlatform": "Windows10" "Windows11",
            "osVersion": "10.0.17763.1637",
            "timestamp": "2021-01-11 09:47:58.854",
            "configurationId": "scid-39",
            "configurationCategory": "OS",
            "configurationSubcategory": "",
            "configurationImpact": 5,
            "isCompliant": true,
            "isApplicable": true,
            "isExpectedUserImpact": false,
            "configurationName": "Enable 'Domain member: Digitally sign secure channel data (when possible)'",
            "recommendationReference": "sca-_-scid-39"
        },
        {
            "deviceId": "00044f912345daf759462bde6bd733d6a9c56ab4",
            "rbacGroupName": "hhh",
            "deviceName": "ComputerPII_18663b45612eeb224d2de2f5ea3142726e63f16a.DomainPII_21eed80d086e76dbfa178eadfa25e8be9acfa346.corp.contoso.com",
            "osPlatform": "Windows10" "Windows11",
            "osVersion": "10.0.17763.1637",
            "timestamp": "2021-01-11 09:47:58.854",
            "configurationId": "scid-6093",
            "configurationCategory": "Security controls",
            "configurationSubcategory": "Antivirus",
            "configurationImpact": 5,
            "isCompliant": false,
            "isApplicable": false,
            "isExpectedUserImpact": false,
            "configurationName": "Enable Microsoft Defender Antivirus real-time behavior monitoring for Linux",
            "recommendationReference": "sca-_-scid-6093"
        }
    ],
    "@odata.nextLink": "https://api.security.microsoft.com/api/machines/SecureConfigurationsAssessmentByMachine?pagesize=5&$skiptoken=eyJFeHBvcnREZWZpbml0aW9uIjp7IlRpbWVQYXRoIjoiMjAyMS0wMS0xMS8xMTAxLyJ9LCJFeHBvcnRGaWxlSW5kZXgiOjAsIkxpbmVTdG9wcGVkQXQiOjV9"
}
```

## 2. Export secure configuration assessment (via files)

### 2.1 API method description

This API response contains the Secure Configuration Assessment on your exposed devices, and returns an entry for every unique combination of DeviceId, ConfigurationId.

#### 2.1.1 Limitations

Rate limitations for this API are 5 calls per minute and 20 calls per hour.

### 2.2 Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs for details.](apis-intro)

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Vulnerability.Read.All | 'Read Threat and Vulnerability Management vulnerability information' |
| Delegated (work or school account) | Vulnerability.Read | 'Read Threat and Vulnerability Management vulnerability information' |

### 2.3 URL

```http
GET /api/machines/SecureConfigurationsAssessmentExport
```

### 2.4 Parameters

- `sasValidHours`: The number of hours that the download URLs are valid for. Maximum is 6 hours.

### 2.5 Properties

- The files are GZIP compressed & in multiline JSON format.
- The download URLs are valid for 1 hour unless the `sasValidHours` parameter is used.
- For maximum download speed of your data, you can make sure you are downloading from the same Azure region in which your data resides.

| Property (ID) | Data type | Description | Example of a returned value |
| --- | --- | --- | --- |
| Export files | array[string] | A list of download URLs for files holding the current snapshot of the organization | ["Https://tvmexportstrstgeus.blob.core.windows.net/tvm-export...1", "https://tvmexportstrstgeus.blob.core.windows.net/tvm-export...2"] |
| GeneratedTime | string | The time that the export was generated. | 2021-05-20T08:00:00Z |

### 2.6 Examples

#### 2.6.1 Request example

```http
GET https://api.security.microsoft.com/api/machines/SecureConfigurationsAssessmentExport
```

#### 2.6.2 Response example

```json
{
    "@odata.context": "https://api.security.microsoft.com/api/$metadata#contoso.windowsDefenderATP.api.ExportFilesResponse",
    "exportFiles": [
        "https://tvmexportstrstgeus.blob.core.windows.net/tvm-export/2021-01-11/1101/ScaExport/json/OrgId=12345678-195f-4223-9c7a-99fb420fd000/part-00393-e423630d-4c69-4490-8769-a4f5468c4f25.c000.json.gz?sv=2019-12-12&st=2021-01-11T11%3A55%3A51Z&se=2021-01-11T14%3A55%3A51Z&sr=b&sp=r&sig=...",
        "https://tvmexportstrstgeus.blob.core.windows.net/tvm-export/2021-01-11/1101/ScaExport/json/OrgId=12345678-195f-4223-9c7a-99fb420fd000/part-00394-e423630d-4c69-4490-8769-a4f5468c4f25.c000.json.gz?sv=2019-12-12&st=2021-01-11T11%3A55%3A51Z&se=2021-01-11T14%3A55%3A51Z&sr=b&sp=r&sig=...",
        "https://tvmexportstrstgeus.blob.core.windows.net/tvm-export/2021-01-11/1101/ScaExport/json/OrgId=12345678-195f-4223-9c7a-99fb420fd000/part-00394-e423630d-4c69-4490-8769-a4f5468c4f25.c001.json.gz?sv=2019-12-12&st=2021-01-11T11%3A55%3A51Z&se=2021-01-11T14%3A55%3A51Z&sr=b&sp=r&sig=..."
    ],
    "generatedTime": "2021-01-11T11:01:00Z"
}
```