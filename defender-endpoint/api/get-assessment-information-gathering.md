---
layout: Conceptual
title: Export information gathering assessment - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/get-assessment-information-gathering
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Returns a table with an entry for every unique combination of DeviceId, DeviceName, Additional fields.
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
ms.date: 2025-12-11T00:00:00.0000000Z
locale: en-us
document_id: a9b9b6ee-22ed-4890-d1e9-668b6ee80014
document_version_independent_id: a9b9b6ee-22ed-4890-d1e9-668b6ee80014
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/get-assessment-information-gathering.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/get-assessment-information-gathering
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/get-assessment-information-gathering.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/de8ce683-cbe1-461b-bae7-77db0888ec6d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/a06cf482-4ca9-4582-a142-bcf842258d42
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 2ed9af57-e2e7-3414-21c4-4b0623aefe62
---

# Export information gathering assessment - Microsoft Defender for Endpoint | Microsoft Learn

This API response returns all information gathering assessments for all devices, on a per-device basis. It returns a table with a separate entry for every DeviceId.

Unless indicated otherwise, all export assessment methods listed are ***full export*** and ***by device*** (also referred to as ***per device***).

It pulls all relevant data in your organization as a download file. The response contains URLs to download all the data from Azure Storage. This API enables you to download all your data from Azure Storage as follows:

- Call the API to get a list of download URLs with all your organization data.
- Download all the files using the download URLs and process the data as you like.

Data that is collected (using *via files*) is the current snapshot of the current state. It doesn't contain historic data. To collect historic data, customers must save the data in their own data storages.

## 1. Export information gathering assessment (via files)

### 1.1 API method description

Returns all information gathering assessments for all devices, on a per-device basis. It returns a table with a separate entry for every DeviceId.

#### Limitations

Rate limitations for this API are 5 calls per minute and 20 calls per hour.

### 1.2 Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs for details](apis-intro).

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Vulnerability.Read.All | 'Read Threat and Vulnerability Management vulnerability information' |
| Delegated (work or school account) | Vulnerability.Read | 'Read Threat and Vulnerability Management vulnerability information' |

### 1.3 URL

```http
GET /api/Machines/InfoGatheringExport
```

### 1.4 Parameters

- `sasValidHours`: The number of hours that the download URLs are valid for Maximum is 6 hours.

### 1.5 Properties

- The files are GZIP compressed & in multiline JSON format.
- The download URLs are valid for 1 hour unless the `sasValidHours` parameter is used.
- To maximize download speeds, make sure you are downloading the data from the same Azure region where your data resides.
- Some additional columns might be returned in the response. These columns are temporary and might be removed. Only use the documented columns.

| Property (ID) | Data type | Description |
| --- | --- | --- |
| Export files | String[array] | A list of download URLs for files holding the current snapshot of the organization. |
| GeneratedTime | DateTime | The time the export was generated. |

### 1.6 Examples

#### 1.6.1 Request example

```http
GET https://api.security.microsoft.com/api/machines/InfoGatheringExport?$sasValidHours=1
```

#### 1.6.2 Response example

```json
{
    "@odata.context": "https://api.security.microsoft.com/api/$metadata#microsoft.windowsDefenderATP.api.ExportFilesResponse",
    "exportFiles": [
        "https://tvmexportexternalprdcanc.blob.core.windows.net/temp-43b2fdb7-c985-4f14-bed5-ae66959a95a5/2022-07-26/1001/InfoGatheringExport/json/OrgId=47d41a0c-188d-46d3-bbea-a93dbc0bfcaa/_RbacGroupId=0/part-00001-42240b35-4a40-45f7-9b46-96a5ce6d23b8.c000.json.gz?sv=2020-08-04&st=2022-07-26T13%3A36%3A30Z&se=2022-07-26T16%3A36%3A30Z&sr=b&sp=r&sig=9GVFFNbgkLc69u32nO944SosmcTUj0usPJqkJwx5iow%3D",
        "https://tvmexportexternalprdcanc.blob.core.windows.net/temp-43b2fdb7-c985-4f14-bed5-ae66959a95a5/2022-07-26/1001/InfoGatheringExport/json/OrgId=47d41a0c-188d-46d3-bbea-a93dbc0bfcaa/_RbacGroupId=1/part-00002-42240b35-4a40-45f7-9b46-96a5ce6d23b8.c000.json.gz?sv=2020-08-04&st=2022-07-26T13%3A36%3A30Z&se=2022-07-26T16%3A36%3A30Z&sr=b&sp=r&sig=BJ3SfwcyI7JnoTVhHAgiyvqWviA%2BUKdF80KeVIUc%2FIU%3D",
        "https://tvmexportexternalprdcanc.blob.core.windows.net/temp-43b2fdb7-c985-4f14-bed5-ae66959a95a5/2022-07-26/1001/InfoGatheringExport/json/OrgId=47d41a0c-188d-46d3-bbea-a93dbc0bfcaa/_RbacGroupId=1001/part-00005-42240b35-4a40-45f7-9b46-96a5ce6d23b8.c000.json.gz?sv=2020-08-04&st=2022-07-26T13%3A36%3A30Z&se=2022-07-26T16%3A36%3A30Z&sr=b&sp=r&sig=6ZsI%2FysPufyNgx234GX8A5xVuz%2FtCtq%2FQ42R2P%2F3XO4%3D",
        "https://tvmexportexternalprdcanc.blob.core.windows.net/temp-43b2fdb7-c985-4f14-bed5-ae66959a95a5/2022-07-26/1001/InfoGatheringExport/json/OrgId=47d41a0c-188d-46d3-bbea-a93dbc0bfcaa/_RbacGroupId=12275/part-00010-42240b35-4a40-45f7-9b46-96a5ce6d23b8.c000.json.gz?sv=2020-08-04&st=2022-07-26T13%3A36%3A30Z&se=2022-07-26T16%3A36%3A30Z&sr=b&sp=r&sig=iqJUkdUsR%2FvGL6hSA2Vqnv02%2BkRJtDhUReJHYd5TOdM%3D"
    ],
    "generatedTime": "2022-07-26T10:01:00Z"
}
```