---
layout: Conceptual
title: Certificate assessment methods and properties per device - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/export-certificate-inventory-assessment
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Provides information about the certificates APIs that pull "Microsoft Defender Vulnerability Management" data. There are different API calls to get different types of data. In general, each API call contains the requisite data for devices in your organization.
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
ms.date: 2025-11-11T00:00:00.0000000Z
locale: en-us
document_id: bc7c1233-ddd8-2c49-99e0-ab6025ba38cd
document_version_independent_id: bc7c1233-ddd8-2c49-99e0-ab6025ba38cd
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/export-certificate-inventory-assessment.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/export-certificate-inventory-assessment
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/export-certificate-inventory-assessment.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/de8ce683-cbe1-461b-bae7-77db0888ec6d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/a06cf482-4ca9-4582-a142-bcf842258d42
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 33c7ddfb-f337-ccba-d0e3-b08d7b663310
---

# Certificate assessment methods and properties per device - Microsoft Defender for Endpoint | Microsoft Learn

There are different API calls to get different types of data. In general, each API call contains the requisite data for devices in your organization. Unless indicated otherwise, all export security baseline assessment methods listed are ***full export*** and ***by device*** (also referred to as ***per device***)

The data can be retrieved in two ways:

- **JSON** The API pulls all data in your organization as JSON responses. This method is best for *small organizations with less than 100-K devices*. The response is paginated, so you can use the @odata.nextLink field from the response to fetch the next results.
- **Files** This API solution enables pulling larger amounts of data faster and more reliably. So, it's recommended for large organizations, with more than 100-K devices. This API pulls all data in your organization as download files. The response contains URLs to download all the data from Azure Storage. You can download data from Azure Storage as follows:

    - Call the API to get a list of download URLs with all your organization data.
    - Download all the files using the download URLs and process the data as you like.

Data that is collected using either '*JSON response* or *via files*' is the current snapshot of the current state. It doesn't contain historic data. To collect historic data, customers must save the data in their own data storages.

## 1. Export certificate assessment (JSON response)

### 1.1 API method description

Returns all certificate assessments for all devices, on a per-device basis. It returns a table with a separate entry for every unique combination of DeviceId, Thumbprint and Path.

#### 1.1.1 Limitations

- Maximum page size is 200,000.
- Rate limitations for this API are 30 calls per minute and 1000 calls per hour.

### 1.2 Permissions

One of the following permissions is required to call this API. For more information on how to choose permissions, see [Use Microsoft Defender for Endpoint APIs for details.](apis-intro)

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Vulnerability.Read.All | 'Read Threat and Vulnerability Management software information' |
| Delegated (work or school account) | Vulnerability.Read | 'Read Threat and Vulnerability Management software information' |

### 1.3 URL

```http
GET /api/machines/certificateAssessmentByMachine
```

### 1.4 Parameters

- pageSize (default = 50,000): Number of results in response.
- $top: Number of results to return (doesn't return @odata.nextLink and so doesn't pull all the data).

### 1.5 Properties (JSON response)

- Each record is approximately 1 KB of data. You should take this into account when choosing the correct pageSize parameter.
- Some additional columns might be returned in the response. These columns are temporary and might be removed. Only use the documented columns.

The properties defined in the following table are listed alphabetically by property ID. When running this API, the resulting output will not necessarily be returned in the same order listed in this table.

| Property (ID) | Data type | Description |
| --- | --- | --- |
| DeviceId | String | Unique identifier for the device in the service. |
| DeviceName | String | Fully qualified domain name (FQDN) of the device. |
| Thumbprint | Boolean | Unique identifier for the certificate. |
| Path | String | The location of the certificate. |
| SignatureAlgorithm | String | Hashing algorithm and encryption algorithm used. |
| KeySize | String | Size of the key used in the signature algorithm. |
| ExpirationDate | String | The date and time beyond which the certificate is no longer valid. |
| IssueDate | String | The earliest date and time when the certificate became valid. |
| SubjectType | String | Indicates if the holder of the certificate is a CA or end entity. |
| SerialNumber | String | Unique identifier for the certificate within a certificate authority's systems. |
| IssuedTo | Object | Entity that a certificate belongs to; can be a device, an individual, or an organization. |
| IssuedBy | Object | Entity that verified the information and signed the certificate. |
| KeyUsage | String | The valid cryptographic uses of the certificate's public key. |
| ExtendedKeyUsage | String | Other valid uses for the certificate. |
| RbacGroupId | String | The role-based access control (RBAC) group id. |
| RbacGroupName | String | The role-based access control (RBAC) group. If this device isn't assigned to any RBAC groups, the value will be "Unassigned." If the organization doesn't contain any RBAC groups, the value will be "None." |

## 1.6 Example

### 1.6.1 Request example

```http
GET https://api.security.microsoft.com/api/machines/CertificateAssessmentByMachine
```

### 1.6.2 Response example

```json

  {
     "@odata.context":"https://127.0.0.1/api/$metadata#Collection(microsoft.windowsDefenderATP.api.AssetCertificateAssessment)",
      "value":[
        {
        "deviceId":"49126b9e4a5473b5229c73799e9e55c48668101b",
        "deviceName":"testmachine5",
        "thumbprint":"AA11BB22CC33DD44EE55FF66AA77BB88CC99DD00",
        "path":"LocalMachine\\TestSignRoot\\AA11BB22CC33DD44EE55FF66AA77BB88CC99DD00",
        "signatureAlgorithm":"sha384ECDSA",
        "keyLength":0,"notAfter":"0001-01-01T00:00:00Z",
        "notBefore":"0001-01-01T00:00:00Z",
        "subjectType":"CA",
        "serialNumber":"6086A185EAFA2B9943B4671603F40323",
        "subjectObject":null,
        "issuerObject":null,
        "keyUsageArray":null,
        "extendedKeyUsageArray":null,
        "isSelfSigned":false,
        "rbacGroupId":4226,
        "rbacGroupName":"testO6343398Gq31"}],
        "@odata.nextLink":"https://127.0.0.1/api/machines/CertificateAssessmentByMachine?pagesize=1&$skiptoken=eyJFeHBvcnREZWZpbml0aW9uIjp7IlRpbWVQYXRoIjoiMjAyMi0wMy0yMS8wNTAxLyJ9LCJFeHBvcnRGaWxlSW5kZXgiOjAsIkxpbmVTdG9wcGVkQXQiOjF9"
  }
```

## 2. Export certificate assessment (via files)

### 2.1 API method description

Returns all certificate assessments for all devices, on a per-device basis. It returns a table with a separate entry for every unique combination of DeviceId, Thumbprint and Path.

#### 2.1.1 Limitations

- Rate limitations for this API are 5 calls per minute and 20 calls per hour.

### 2.2 Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs for details.](apis-intro)

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Vulnerability.Read.All | 'Read Threat and Vulnerability Management software information' |
| Delegated (work or school account) | Vulnerability.Read | 'Read Threat and Vulnerability Management software information' |

### 2.3 URL

```http
GET /api/machines/certificateAssessmentExport
```

### 2.4 Parameters

- sasValidHours: The number of hours that the download URLs will be valid for (Maximum 24 hours).

### 2.5 Properties (JSON response)

- The files are gzip compressed & in multiline Json format.
- The download URLs are only valid for 3 hours; otherwise, you can use the parameter.
- To maximize download speeds, make sure you are downloading the data from the same Azure region where your data resides.
- Each record is approximately 1KB of data. You should take this into account when choosing the pageSize parameter that works for you.
- Some additional columns might be returned in the response. These columns are temporary and might be removed. Only use the documented columns.

| Property (ID) | Data type | Description |
| --- | --- | --- |
| Export files | String[array] | A list of download URLs for files holding the current snapshot of the organization. |
| GeneratedTime | DateTime | The time the export was generated. |

## 2.6 Example

### 2.6.1 Request example

```http
GET https://api.security.contoso.com/api/machines/certificateAssessmentExport
```

### 2.6.2 Response example

```json
    {
        "@odata.context":"https://127.0.0.1/api/$metadata#microsoft.windowsDefenderATP.api.ExportFilesResponse",
        "exportFiles":["https://tvmexportexternalstgeus.blob.core.windows.net/temp-5c080622-f613-42bb-9fee-e17ccdff90d3/2022-03-20/1318/CertificateAssessmentExport/json/OrgId=47d41a0c-188d-46d3-bbea-a93dbc0bfcaa/_RbacGroupId=4226/part-00000-65a62a9d-7a01-4d78-bbdb-6d3e07b34cc9.c000.json.gz?sv=2020-02-10&st=2022-03-20T13%3A35%3A37Z&se=2022-03-20T16%3A35%3A37Z&sr=b&sp=r&sig=IMmwTOYmGvU0ei5AHLNAxnFCmZkE2jvBHzRmuAu9xaA%3D","https://tvmexportexternalstgeus.blob.core.windows.net/temp-5c080622-f613-42bb-9fee-e17ccdff90d3/2022-03-20/1318/CertificateAssessmentExport/json/OrgId=47d41a0c-188d-46d3-bbea-a93dbc0bfcaa/_RbacGroupId=4414/part-00000-65a62a9d-7a01-4d78-bbdb-6d3e07b34cc9.c000.json.gz?sv=2020-02-10&st=2022-03-20T13%3A35%3A37Z&se=2022-03-20T16%3A35%3A37Z&sr=b&sp=r&sig=2r0y74WZsATa0DjQTwfBxNqL5vN2Wl0AZKHMNrxuJ30%3D","https://tvmexportexternalstgeus.blob.core.windows.net/temp-5c080622-f613-42bb-9fee-e17ccdff90d3/2022-03-20/1318/CertificateAssessmentExport/json/OrgId=47d41a0c-188d-46d3-bbea-a93dbc0bfcaa/_RbacGroupId=75/part-00000-65a62a9d-7a01-4d78-bbdb-6d3e07b34cc9.c000.json.gz?sv=2020-02-10&st=2022-03-20T13%3A35%3A37Z&se=2022-03-20T16%3A35%3A37Z&sr=b&sp=r&sig=uVdY4%2BBpMdPMwaD3G0RJTZkS4R9J8oN8I3tu%2FOcG35c%3D"],
        "generatedTime":"2022-03-20T13:18:00Z"
   }
```