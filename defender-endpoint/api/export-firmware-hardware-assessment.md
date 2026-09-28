---
layout: Conceptual
title: Hardware and firmware assessment methods and properties per device - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/export-firmware-hardware-assessment
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Provides information about the Firmware and Hardware APIs that pull "Microsoft Defender Vulnerability Management" data. There are different API calls to get different types of data. In general, each API call contains the requisite data for devices in your organization.
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
ms.date: 2025-01-22T00:00:00.0000000Z
locale: en-us
document_id: 8b45bcef-d931-68e0-01c7-6f848d595cd6
document_version_independent_id: 8b45bcef-d931-68e0-01c7-6f848d595cd6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/export-firmware-hardware-assessment.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/export-firmware-hardware-assessment
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/export-firmware-hardware-assessment.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/de8ce683-cbe1-461b-bae7-77db0888ec6d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/a06cf482-4ca9-4582-a142-bcf842258d42
platformId: 0068ab3a-5cfd-522d-674c-86adced7a7b0
---

# Hardware and firmware assessment methods and properties per device - Microsoft Defender for Endpoint | Microsoft Learn

> 
> Want to experience Microsoft Defender Vulnerability Management? Learn more about how you can sign up to the [Microsoft Defender Vulnerability Management public preview trial](/en-us/defender-vulnerability-management/get-defender-vulnerability-management).

There are different API calls to get different types of data. In general, each API call contains the requisite data for devices in your organization.

- **JSON response** The API pulls all data in your organization as JSON responses. This method is best for *small organizations with less than 100-K devices*. The response is paginated, so you can use the @odata.nextLink field from the response to fetch the next results.
- **via files** This API solution enables pulling larger amounts of data faster and more reliably. So, it's recommended for large organizations, with more than 100-K devices. This API pulls all data in your organization as download files. The response contains URLs to download all the data from Azure Storage. You can download data from Azure Storage as follows:

    - Call the API to get a list of download URLs with all your organization data.
    - Download all the files using the download URLs and process the data as you like.

Data that is collected using either '*JSON response* or *via files*' is the current snapshot of the current state. It doesn't contain historic data. To collect historic data, customers must save the data in their own data storages.

Note

Unless indicated otherwise, all export hardware and firmware assessment methods listed are ***full export*** and ***by device*** (also referred to as ***per device***)

## 1. Export hardware and firmware assessment (JSON response)

### 1.1 API method description

Returns all hardware and firmware assessments for all devices, on a per-device basis. It returns a table with a separate entry for every unique combination of deviceId and componentType.

#### 1.1.1 Limitations

- Maximum page size is 200,000.
- Rate limitations for this API are 30 calls per minute and 1000 calls per hour.

### 1.2 Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs for details.](apis-intro)

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Software.Read.All | 'Read Threat and Vulnerability Management software information' |
| Delegated (work or school account) | Software.Read | 'Read Threat and Vulnerability Management software information' |

### 1.3 URL

```http
GET api/machines/HardwareFirmwareInventoryByMachine
```

### 1.4 Parameters

- pageSize (default = 50,000): Number of results in response.
- $top: Number of results to return (doesn't return @odata.nextLink and so doesn't pull all the data).

### 1.5 Properties (JSON response)

Note

Each record is approximately 1 KB of data. You should take this into account when choosing the correct pageSize parameter.

Some additional columns might be returned in the response. These columns are temporary and might be removed. Only use the documented columns.

The properties defined in the following table are listed alphabetically by property ID. When running this API, the resulting output will not necessarily be returned in the same order listed in this table.

| Property (ID) | Data type | Description |
| --- | --- | --- |
| deviceId | String | Unique identifier for the device in the service. |
| rbacGroupId | Int | The role-based access control (RBAC) group Id. If the device isn't assigned to any RBAC group, the value will be "Unassigned." If the organization doesn't contain any RBAC groups, the value will be "None." |
| rbacGroupName | String | The role-based access control (RBAC) group. If the device isn't assigned to any RBAC group, the value will be "Unassigned." If the organization doesn't contain any RBAC groups, the value will be "None." |
| deviceName | String | Fully qualified domain name (FQDN) of the device. |
| componentType | String | Type of hardware or firmware component. |
| manufacturer | String | Manufacturer of a specific hardware or firmware component. |
| componentName | String | Name of a specific hardware or firmware component. |
| componentVersion | String | Version of a specific hardware or firmware component. |
| additionalFields | String | Additional information about the components in JSON array format. |

## 1.6 Example

### 1.6.1 Request example

```http
GET https://api.security.microsoft.com/api/machines/HardwareFirmwareInventoryByMachine
```

### 1.6.2 Response example

```json
      {
        "@odata.context": "https://api.security.microsoft.com/api/$metadata#Collection(microsoft.windowsDefenderATP.api.AssetHardwareFirmware)",
        "value":[
        {
            "deviceId": "49126b9e4a5473b5229c73799e9e55c48668101b",
            "rbacGroupId": 39,
            "rbacGroupName": "testO6343398Gq31",
            "deviceName": "testmachine5",
            "componentType": "Hardware",
            "manufacturer": "razer",
            "componentName": "blade_15_advanced_model_(mid_2021)_-_rz09-0409",
            "componentVersion": "7.04",
            "additionalFields": "{\"SystemSKU\":\"RZ09-0409CE53\",\"BaseBoardManufacturer\":\"Razer\",\"BaseBoardProduct\":\"CH570\",\"BaseBoardVersion\":\"4\",\"DeviceFamily\":\"Workstation\"}"
          }
        ]
      },
```

## 2. Export hardware and firmware assessment (via files)

### 2.1 API method description

Returns all hardware and firmware assessments for all devices, on a per-device basis. It returns a table with a separate entry for every unique combination of DeviceId, ComponentType and ComponentName.

#### 2.1.1 Limitations

- Rate limitations for this API are 5 calls per minute and 20 calls per hour.

### 2.2 Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs for details.](apis-intro)

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Software.Read.All | 'Read Threat and Vulnerability Management software information' |
| Delegated (work or school account) | Software.Read | 'Read Threat and Vulnerability Management software information' |

### 2.3 URL

```http
GET /api/machines/HardwareFirmwareInventoryExport
```

### 2.4 Parameters

- `sasValidHours`: The number of hours that the download URLs are valid for. Maximum is 6 hours.

### 2.5 Properties (JSON response)

Note

- The files are GZIP compressed & in multiline JSON format.
- The download URLs are valid for 1 hour unless the `sasValidHours` parameter is used.
- To maximize download speeds, make sure you are downloading the data from the same Azure region where your data resides.
- Each record is approximately 1KB of data. You should take this into account when choosing the pageSize parameter that works for you.
- Some additional columns might be returned in the response. These columns are temporary and might be removed. Only use the documented columns.

| Property (ID) | Data type | Description |
| --- | --- | --- |
| Export files | String[array] | A list of download URLs for files holding the current snapshot of the organization. |
| GeneratedTime | DateTime | The time the export was generated. |

## 2.6 Examples

### 2.6.1 Request example

```http
GET https://api.security.microsoft.com/api/machines/HardwareFirmwareInventoryExport
```

### 2.6.2 Response example

```json
    {
        "@odata.context":"https://api.security.microsoft.com/api/$metadata#microsoft.windowsDefenderATP.api.ExportFilesResponse",
    "exportFiles": [
        "https://tvmexportstrprdcane.blob.core.windows.net/tvm-firmware-export/2022-07-11/1101/FirmwareHardwareExport/json/OrgId=3837d1f5-0d51-40cb-a99d-69ebedc9dcc8/_RbacGroupId=39/part-00999-71eea973-1bb1-4d0a-829d-80cb07aff5d8.c000.json.gz?sv=2020-08-04&st=2022-07-11T13%3A10%3A06Z&se=2022-07-11T16%3A10%3A06Z&sr=b&sp=r&sig=muN8Sq6rVN6bFMtR0u3S5Wzh3D9qNPgN5vpU7lWvULg%3D",
        "https://tvmexportstrprdcane.blob.core.windows.net/tvm-firmware-export/2022-07-11/1101/FirmwareHardwareExport/json/OrgId=3837d1f5-0d51-40cb-a99d-69ebedc9dcc8/_RbacGroupId=9/part-00968-71eea973-1bb1-4d0a-829d-80cb07aff5d8.c000.json.gz?sv=2020-08-04&st=2022-07-11T13%3A10%3A06Z&se=2022-07-11T16%3A10%3A06Z&sr=b&sp=r&sig=%2BA0%2B4qOOBCS5E4UenJPbMdLM%2FkbXHnz%2F1pvfSOCq%2F2s%3D",
        "https://tvmexportstrprdcane.blob.core.windows.net/tvm-firmware-export/2022-07-11/1101/FirmwareHardwareExport/json/OrgId=3837d1f5-0d51-40cb-a99d-69ebedc9dcc8/_RbacGroupId=9/part-00969-71eea973-1bb1-4d0a-829d-80cb07aff5d8.c000.json.gz?sv=2020-08-04&st=2022-07-11T13%3A10%3A06Z&se=2022-07-11T16%3A10%3A06Z&sr=b&sp=r&sig=sZUgYMwSr5zk6BZvS%2BoYIWlHJWk2oJ7YjiC8R26S1X4%3D"
    ],
    "generatedTime": "2022-07-11T11:01:00Z"

   }
```