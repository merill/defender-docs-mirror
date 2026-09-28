---
layout: Conceptual
title: Microsoft Defender Antivirus Device Health export device antivirus health reporting - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/device-health-export-antivirus-health-report-api
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Presents methods to retrieve Microsoft Defender Antivirus device health details.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.date: 2026-02-05T00:00:00.0000000Z
ms.collection:
- m365-security
- tier3
- must-keep
ms.topic: reference
ms.subservice: reference
ms.custom: api
locale: en-us
document_id: 1956950c-19d0-9f87-8f29-0c70b75873fc
document_version_independent_id: 1956950c-19d0-9f87-8f29-0c70b75873fc
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/device-health-export-antivirus-health-report-api.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/device-health-export-antivirus-health-report-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/device-health-export-antivirus-health-report-api.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/de8ce683-cbe1-461b-bae7-77db0888ec6d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/a06cf482-4ca9-4582-a142-bcf842258d42
platformId: 8cc589e1-7011-0548-679a-03d929074446
---

# Microsoft Defender Antivirus Device Health export device antivirus health reporting - Microsoft Defender for Endpoint | Microsoft Learn

This API has two methods to retrieve Microsoft Defender Antivirus device antivirus health details:

- **Method one:**1 Export health reporting (**JSON response**) The method pulls all data in your organization as JSON responses. This method is best for *small organizations with less than 100-K devices*. The response is paginated, so you can use the @odata.nextLink field from the response to fetch the next results.
- **Method two:**2 Export health reporting (**via files**) This method enables pulling larger amounts of data faster and more reliably. So, it's recommended for large organizations, with more than 100-K devices. This API pulls all data in your organization as download files. The response contains URLs to download all the data from Azure Storage. This API enables you to download all your data from Azure Storage as follows:

    - Call the API to get a list of download URLs with all your organization data.
    - Download all the files using the download URLs and process the data as you like.

Data that is collected using either '*JSON response* or *via files*' is the current snapshot of the current state. It doesn't contain historic data. To collect historic data, customers must save the data in their own data storages. See [Export device health details API methods and properties](device-health-api-methods-properties).

For information about using the **Device health and antivirus compliance** reporting tool in the Microsoft Defender portal, see: [Device health and antivirus compliance report in Microsoft Defender for Endpoint](../device-health-reports).

## Prerequisites

For Windows Server 2012 R2 and Windows Server 2016 to appear in device health reports, these devices must be onboarded using the modern unified solution package. For more information, see [New functionality in the modern unified solution for Windows Server 2012 R2 and 2016](../onboard-server#functionality-in-the-modern-unified-solution-for-windows-server-2016-and-windows-server-2012-r2).

## 1 Export health reporting (JSON response)

### 1.1 API method description

This API retrieves a list of Microsoft Defender Antivirus device antivirus health details. Returns a table with an entry for every unique combination of:

- DeviceId
- Device name
- AV mode
- Up-to-date status
- Scan results

#### 1.1.1 Limitations

- maximum page size is 200,000
- Rate limitations for this API are 30 calls per minute and 1000 calls per hour.

Supports [OData V4 queries](https://www.odata.org/documentation/). OData supported operators:

- `$filter`on the following properties:
    - `machineId`
    - `computerDnsName`
    - `osKind`
    - `osPlatform`
    - `osVersion`
    - `avMode`
    - `avSignatureVersion`
    - `avEngineVersion`
    - `avPlatformVersion`
    - `quickScanResult`
    - `quickScanError`
    - `fullScanResult`
    - `fullScanError`
    - `avIsSignatureUpToDate`
    - `avIsEngineUpToDate`
    - `avIsPlatformUpToDate`
    - `rbacGroupId`
- `$top` with max value of 10,000.
- `$skip`

See examples at [OData queries with Microsoft Defender for Endpoint](exposed-apis-odata-samples).

Important

`rbacgroupname` and `Id` aren't supported filter operators.

### 1.2 Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see Use Microsoft Defender for Endpoint APIs for details.

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Machine.Read.All | 'Read all machine profiles' |
| Delegated (work or school account) | Machine.Read | 'Read machine information' |

If you need to call the API without a user (Service-to-Service), refer to the official documentation: [Create an app to access Microsoft Defender for Endpoint without a user](exposed-apis-create-app-webapp#get-an-access-token).

Use the script below to ensure the scope is correctly defined for the Device Health in Defender for Endpoint API.

Tip

Some Microsoft Defender for Endpoint APIs continue to require access tokens issued for the legacy resource `https://api.securitycenter.microsoft.com`. If the token audience doesn't match the resource expected by the API, requests fail with `403 Forbidden`, even if the API endpoint uses `https://api.security.microsoft.com`. Use `https://api.securitycenter.microsoft.com` as the resource or scope when acquiring tokens.

```powershell
# This script acquires the App Context Token and stores it in the variable $token for later use.
# Paste your Tenant ID, App ID, and App Secret (App key) into the quotes below.

$tenantId    = '' ### Paste your Tenant ID here
$appId       = '' ### Paste your Application ID here
$appSecret   = '' ### Paste your Application key here

# Corrected Source App ID URI
$sourceAppIdUri = '[https://api.securitycenter.microsoft.com/.default](https://api.securitycenter.microsoft.com/.default)'
$oAuthUri       = "[https://login.microsoftonline.com/$tenantId/oauth2/v2.0/token](https://login.microsoftonline.com/$tenantId/oauth2/v2.0/token)"

$authBody = [Ordered] @{
    scope         = "$sourceAppIdUri"
    client_id     = "$appId"
    client_secret = "$appSecret"
    grant_type    = 'client_credentials'
}

$authResponse = Invoke-RestMethod -Method Post -Uri $oAuthUri -Body $authBody -ErrorAction Stop
$token = $authResponse.access_token

# Output the token
$token
```

Important

If permission is defined under **WindowsDefenderATP**, the scope must be set to: `https://api.securitycenter.microsoft.com/.default`

### 1.3 URL (HTTP request)

```http
URL: GET: /api/deviceavinfo
```

#### 1.3.1 Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer {token}. **Required**. |

#### 1.3.2 Request body

Empty

#### 1.3.3 Response

If successful, this method returns 200 OK with a list of device health details.

### 1.4 Parameters

- Default page size is 20
- See examples at [OData queries with Microsoft Defender for Endpoint](exposed-apis-odata-samples).

### 1.5 Properties

See: [1.3 Export device antivirus health details API properties (JSON response)](device-health-api-methods-properties#13-export-device-antivirus-health-details-api-properties-json-response)

Supports [OData V4 queries](https://www.odata.org/documentation/).

### 1.6 Example

#### Request example

Here's an example request:

```http
GET https://api.security.microsoft.com/api/deviceavinfo
```

#### Response example

Here's an example response:

```json
{

    @odata.context: "https://api.security.microsoft.com/api/$metadata#DeviceAvInfo",

"value": [{

            "id": "Sample Guid",

            "machineId": "Sample Machine Guid",

            "computerDnsName": "appblockstg1",

            "osKind": "windows",

            "osPlatform": "Windows10",

            "osVersion": "10.0.19044.1865",

            "avMode": "0",

            "avSignatureVersion": "1.371.1279.0",

            "avEngineVersion": "1.1.19428.0",

            "avPlatformVersion": "4.18.2206.108",

            "lastSeenTime": "2022-08-02T19:40:45Z",

            "quickScanResult": "Completed",

            "quickScanError": "",

            "quickScanTime": "2022-08-02T18:40:15.882Z",

            "fullScanResult": "",

            "fullScanError": "",

            "fullScanTime": null,

            "dataRefreshTimestamp": "2022-08-02T21:16:23Z",

            "avEngineUpdateTime": "2022-08-02T00:03:39Z",

            "avSignatureUpdateTime": "2022-08-02T00:03:39Z",

            "avPlatformUpdateTime": "2022-06-20T16:59:35Z",

            "avIsSignatureUpToDate": "True",

            "avIsEngineUpToDate": "True",

            "avIsPlatformUpToDate": "True",

            "avSignaturePublishTime": "2022-08-02T00:03:39Z",

            "rbacGroupName": "TVM1",

            "rbacGroupId": 4415

        },

        ...

     ]

}
```

## 2 Export health reporting (via files)

Important

Information in this section relates to prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

### 2.1 API method description

This API response contains all the data of Antivirus health and status per device. Returns a table with an entry for every unique combination of:

- DeviceId
- device name
- AV mode
- Up-to-date status
- Scan results

#### 2.1.2 Limitations

- Maximum page size is 200,000.
- Rate limitations for this API are 30 calls per minute and 1000 calls per hour.

### 2.2 Permissions

One of the following permissions is required to call this API.

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Vulnerability.Read.All | 'Read "threat and vulnerability management" vulnerability information' |
| Delegated (work or school account) | Vulnerability.Read | 'Read "threat and vulnerability management" vulnerability information' |

To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs for details](apis-intro).

### 2.3 URL

```http
GET /api/machines/InfoGatheringExport
```

### 2.4 Parameters

- `sasValidHours`: The number of hours that the download URLs will be valid for (Maximum 24 hours).

### 2.5 Properties

See: [1.4 Export device antivirus health details API properties (via files)](device-health-api-methods-properties#14-export-device-antivirus-health-details-api-properties-via-files).

### 2.6 Examples

#### 2.6.1 Request example

Here's an example request:

```HTTP
GET https://api.security.windows.com/api/machines/InfoGatheringExport
```

#### 2.6.2 Response example

Here's an example response:

```json
{

   "@odata.context": "https://api.security.windows.com/api/$metadata#microsoft.windowsDefenderATP.api.ExportFilesResponse",

   "exportFiles": [

       "https://tvmexportexternalprdeus.blob.core.windows.net/temp-../2022-08-02/2201/InfoGatheringExport/json/OrgId=../_RbacGroupId=../part-00055-12fc2fcd-8f56-4e09-934f-e8efe7ce74a0.c000.json.gz?sv=2020-08-04&st=2022-08-02T22%3A47%3A11Z&se=2022-08-03T01%3A47%3A11Z&sr=b&sp=r&sig=..",

       "https://tvmexportexternalprdeus.blob.core.windows.net/temp-../2022-08-02/2201/InfoGatheringExport/json/OrgId=../_RbacGroupId=../part-00055-12fc2fcd-8f56-4e09-934f-e8efe7ce74a0.c000.json.gz?sv=2020-08-04&st=2022-08-02T22%3A47%3A11Z&se=2022-08-03T01%3A47%3A11Z&sr=b&sp=r&sig=.."

   ],

   "generatedTime": "2022-08-02T22:01:00Z"

}
```

Tip

**Performance tip** Due to a variety of factors (examples listed below) Microsoft Defender Antivirus, like other antivirus software, can cause performance issues on endpoint devices. In some cases, you might need to tune the performance of Microsoft Defender Antivirus to alleviate those performance issues. Microsoft's **Performance analyzer** is a PowerShell command-line tool that helps determine which files, file paths, processes, and file extensions might be causing performance issues; some examples are:

- Top paths that impact scan time
- Top files that impact scan time
- Top processes that impact scan time
- Top file extensions that impact scan time
- Combinations – for example:
    - top files per extension
    - top paths per extension
    - top processes per path
    - top scans per file
    - top scans per file per process

You can use the information gathered using Performance analyzer to better assess performance issues and apply remediation actions. See: [Performance analyzer for Microsoft Defender Antivirus](../tune-performance-defender-antivirus).