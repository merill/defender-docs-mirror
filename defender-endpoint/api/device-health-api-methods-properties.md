---
layout: Conceptual
title: Microsoft Defender Antivirus export device antivirus health details API methods and properties - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/device-health-api-methods-properties
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to export a list of Microsoft Defender Antivirus device health details.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.date: 2025-11-11T00:00:00.0000000Z
ms.reviewr: mkaminska
ms.collection:
- m365-security
- must-keep
- tier3
ms.topic: reference
ms.subservice: reference
ms.custom: api
locale: en-us
document_id: e10ab58c-7e85-ae7b-5339-6aaa80ae2981
document_version_independent_id: e10ab58c-7e85-ae7b-5339-6aaa80ae2981
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/device-health-api-methods-properties.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/device-health-api-methods-properties
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/device-health-api-methods-properties.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/de8ce683-cbe1-461b-bae7-77db0888ec6d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/a06cf482-4ca9-4582-a142-bcf842258d42
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
platformId: 72a34953-a197-dee1-7c83-6564f46943fd
---

# Microsoft Defender Antivirus export device antivirus health details API methods and properties - Microsoft Defender for Endpoint | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Export device antivirus health details API description

Retrieves a list of Microsoft Defender Antivirus device health details. This API has different API calls (methods) to get different types of data. Because the amount of data can be large, there are two ways it can be retrieved:

- **JSON** The API pulls all data in your organization as JSON responses. This method is best for *small organizations with less than 100-K devices*. The response is paginated, so you can use the @odata.nextLink field from the response to fetch the next results.
- **Files** This API solution enables pulling larger amounts of data faster and more reliably, and is recommended for large organizations who have more than 100,000 devices. This API pulls all data in your organization as download files. The response contains URLs to download all the data from Azure Storage. This API enables you to download all your data from Azure Storage as follows:

    1. Call the API to get a list of download URLs with all your organization data.
    2. Download all the files using the download URLs and process the data as you like.

Data that is collected using either `JSON response` or by using files is a snapshot of the current state. This data doesn't contain historical data. To collect historical data, you must save the data in your own data storage.

For information about using the **Device health and antivirus compliance** reporting tool in the Microsoft Defender portal, see: [Device health and antivirus report in Microsoft Defender for Endpoint](../device-health-reports).

### Prerequisites

- For Windows Server 2012 R2 and Windows Server 2016 to appear in device health reports, these devices must be onboarded using the modern unified solution package. For more information, see [New functionality in the modern unified solution for Windows Server 2012 R2 and 2016](../onboard-server#functionality-in-the-modern-unified-solution-for-windows-server-2016-and-windows-server-2012-r2).

### 1.1 Export device antivirus health details API methods

| Method | Data type | Description |
| --- | --- | --- |
| **(JSON response)** | Microsoft Defender Antivirus health per device collection. See: 1.2 Export device antivirus health details API properties (JSON response) | Returns a table with an entry for every unique combination of DeviceId, ConfigurationId.  The API pulls all data in your organization as JSON responses. This method is best for small organizations with less than 100-K devices. The response is paginated, so you can use the @odata.nextLink field from the response to fetch the next results. |
| **(via files)** | Microsoft Defender Antivirus health per device collection. See: 1.3 Export device antivirus health details API properties (via files) | Returns a table with an entry for every unique combination of DeviceId, ConfigurationId.  This API solution enables pulling larger amounts of data faster and more reliably. So, it's recommended for large organizations, with more than 100-K devices. This API pulls all data in your organization as download files. The response contains URLs to download all the data from Azure Storage. This API enables you to download all your data from Azure Storage as follows: <br>1. Call the API to get a list of download URLs with all your organization data.<br>2. Download all the files using the download URLs and process the data as you like. |

### 1.2 Limitations

- Maximum page size: 200,000
- Rate limitations for this API: 30 calls per minute and 1,000 calls per hour

### 1.3 Export device antivirus health details API properties (JSON response)

- The properties defined in the following table are listed alphabetically, by property ID. When you use this API, the resulting output won't necessarily be returned in the same order listed in this table.
- Note that **rbacgroupname** and **Id** aren't supported filter operators.
- Some more columns might be returned in the response. These columns can be temporary and might be removed; use only the documented columns.

| Property (ID) | Data type | Description | Example of a returned value |
| --- | --- | --- | --- |
| `avEngineUpdateTime` | DateTimeOffset | Datetime when the antivirus engine was last updated on device | "2022-08-04T12:44:02Z" |
| `avEngineVersion` | String | Antivirus engine version | `1.1.19400.3` |
| `avIsEngineUpToDate` | String | Up-to-date status of antivirus engine | `True`, `False`, or `Unknown` |
| `avIsPlatformUpToDate` | String | Up-to-date status of antivirus platform | `True`, `False`, or `Unknown` |
| `avIsSignatureUpToDate` | String | Up-to-date status of antivirus signature | `True`, `False`, or `Unknown` |
| `avMode` | String | Antivirus mode. | Each mode is a string typed integer value ranging from 0 to 5. `''` = `Other``0` = `Active``1` = `Passive``2` = `Disabled``3` = `Other``4` = `EDRBlocked``5` = `PassiveAudit` |
| `avPlatformUpdateTime` | DateTimeOffset | Datetime when antivirus platform was last updated on device | "2022-08-04T12:44:02Z" |
| `avPlatformVersion` | String | Antivirus platform version | `4.18.2203.5` |
| `avSignaturePublishTime` | DateTimeOffset | Datetime when antivirus security intelligence build was released | "2022-08-04T12:44:02Z" |
| `avSignatureUpdateTime` | DateTimeOffset | Datetime when antivirus security intelligence was last updated on device | "2022-08-04T12:44:02Z" |
| `avSignatureVersion` | String | Antivirus security intelligence version | `1.371.1323.0` |
| `computerDnsName` | String | DNS name | `SampleDns` |
| `dataRefreshTimestamp` | DateTimeOffset | Datetime when data is refreshed for this report | `2022-08-04T12:44:02Z` |
| `fullScanError` | String | Error codes from the full scan | "0x80508023" |
| `fullScanResult` | String | Full scan result of the device | `Completed`, `Canceled`, or `Failed` |
| `fullScanTime` | DateTimeOffset | Datetime when the full scan completed | `2022-08-04T12:44:02Z` |
| `id` | String | Machine GUID | `30a8fa2826abf24d24379b23f8a44d471f00feab` |
| `lastSeenTime` | DateTimeOffset | Last seen datetime of this machine | `2022-08-04T12:44:02Z` |
| `machineId` | String | Machine GUID | `30a8fa2826abf24d24379b23f8a44d471f00feab` |
| `osKind` | String | Operating system kind | `windows`, `mac`, or `linux` |
| `osPlatform` | String | Operating system major version name | `Windows 10` or `macOS` |
| `osVersion` | String | Operating system version | `10.0.18363.1440, 12.4.0.0` |
| `quickScanError` | String | Error codes from quick scan | `0x80508023` |
| `quickScanResult` | String | Quick scan result of this device | `Completed`, `Canceled`, or `Failed` |
| `quickScanTime` | DateTimeOffset | Datetime when quick scan completed | `2022-08-04T12:44:02Z` |
| `rbacGroupId` | Long | Device group ID that this machine belongs to | `712` |
| `rbacGroupName` | String | Name of device group that this machine belongs to | `SampleGroup` |

### 1.4 Export device antivirus health details API properties (via files)

Important

Information in this section relates to prereleased product which can be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

In each of the export files, there's a property called `DeviceGatheredInfo`, which contains antivirus data. Each of its attributes can provide you with information on the device's health and its status.

- The files are gzip-compressed and in multiline `.json` format.
- The download URLs are only valid for 3 hours; otherwise you can use the parameter.
- For maximum download speed of your data, you can make sure you're downloading from the same Azure region that your data resides.
- Each record uses approximately 1KB of data. You should take this into account when choosing the correct `pageSize` parameter.
- More columns might be returned in the response. These columns are temporary and might be removed, so use only the documented columns.

| Property (ID) | Data type | Description | Example of a returned value |
| --- | --- | --- | --- |
| Export files | array[string] | A list of download URLs for files holding the current snapshot of the organization. | ["https://tvmexportstrstgeus.blob.core.windows.net/tvm-export...1", "https://tvmexportstrstgeus.blob.core.windows.net/tvm-export...2"] |
| GeneratedTime | String | The time that the export was generated. | 2022-05-20T08:00:00Z |