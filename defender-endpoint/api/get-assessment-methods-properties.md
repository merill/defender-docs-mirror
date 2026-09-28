---
layout: Conceptual
title: Export assessment methods and properties per device - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/get-assessment-methods-properties
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Provides information about the APIs that pull "Microsoft Defender Vulnerability Management" data. There are different API calls to get different types of data. In general, each API call contains the requisite data for devices in your organization.
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
document_id: d536c30b-9605-4968-3209-22e1f64253e7
document_version_independent_id: d536c30b-9605-4968-3209-22e1f64253e7
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/get-assessment-methods-properties.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/get-assessment-methods-properties
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/get-assessment-methods-properties.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/de8ce683-cbe1-461b-bae7-77db0888ec6d
- https://authoring-docs-microsoft.poolparty.biz/devrel/e0ffb20c-01c6-407b-a9bd-29111652a1dc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/19ec6774-09b8-473e-a17e-b17b518bbad7
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/a06cf482-4ca9-4582-a142-bcf842258d42
- https://authoring-docs-microsoft.poolparty.biz/devrel/3904bce4-d817-48cf-85fd-b6146fca83b7
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ade36b61-c646-4bd8-87ee-f3a843461962
platformId: b17fedf0-6750-8992-471a-cea356061170
---

# Export assessment methods and properties per device - Microsoft Defender for Endpoint | Microsoft Learn

## API description

Provides methods and property details about the APIs that pull vulnerability management data on a per-device basis. There are different API calls to get different types of data.Each API call contains the requisite data for devices in your organization.

Unless indicated otherwise, all export assessment methods listed are ***full export*** and ***by device*** (also referred to as ***per device***).

You can use the export assessment APIs to retrieve (export) different types of information:

- 1. Export secure configurations assessment
- 2. Export software inventory assessment
- 3. Export software vulnerabilities assessment
- 4. Export non product code software inventory assessment

The APIs that correspond to the export information types are described in sections 1, 2, and 3.

Each method has different API calls to get different types of data. Because the amount of data can be large, there are two ways it can be retrieved:

- **JSON** The API pulls all data in your organization as JSON responses. This method is best for *small organizations with less than 100-K devices*. The response is paginated, so you can use the @odata.nextLink field from the response to fetch the next results.
- **Files** This API solution enables pulling larger amounts of data faster and more reliably. It's recommended for large organizations, with more than 100-K devices. This API pulls all data in your organization as download files. The response contains URLs to download all the data from Azure Storage. This API enables you to download all your data from Azure Storage as follows:

    - Call the API to get a list of download URLs with all your organization data.
    - Download all the files using the download URLs and process the data as you like.

Data that is collected using either '*JSON response* or *via files*' is the current snapshot of the current state. It doesn't contain historic data. To collect historic data, customers must save the data in their own data storages.

## 1. Export secure configurations assessment

Returns all of the configurations and their status, on a per-device basis.

### 1.1 Methods

| Method | Data type | Description |
| --- | --- | --- |
| Export secure configuration assessment **(JSON response)** | Secure configuration by device collection. See: 1.2 Properties (JSON response) | Returns a table with an entry for every unique combination of DeviceId, ConfigurationId. The API pulls all data in your organization as JSON responses. This method is best for small organizations with less than 100-K devices. The response is paginated, so you can use the @odata.nextLink field from the response to fetch the next results. |
| Export secure configuration assessment **(via files)** | Secure configuration by device collection. See: 1.3 Properties (via files) | Returns a table with an entry for every unique combination of DeviceId, ConfigurationId. This API solution enables pulling larger amounts of data faster and more reliably. So, it's recommended for large organizations, with more than 100-K devices. This API pulls all data in your organization as download files. The response contains URLs to download all the data from Azure Storage. This API enables you to download all your data from Azure Storage as follows: <br>1. Call the API to get a list of download URLs with all your organization data.<br>2. Download all the files using the download URLs and process the data as you like. |

### 1.2 Properties (JSON response)

| Property (ID) | Data type | Description |
| --- | --- | --- |
| configurationCategory | String | Category or grouping to which the configuration belongs: Application, OS, Network, Accounts, Security controls. |
| configurationId | String | Unique identifier for a specific configuration. |
| configurationImpact | String | Rated effect of the configuration to the overall configuration score (1-10). |
| configurationName | String | Display name of the configuration. |
| configurationSubcategory | String | Subcategory or subgrouping to which the configuration belongs. In many cases, specific capabilities or features. |
| deviceId | String | Unique identifier for the device in the service. |
| deviceName | String | Fully qualified domain name (FQDN) of the device. |
| isApplicable | Bool | Indicates whether the configuration or policy is applicable. |
| isCompliant | Bool | Indicates whether the configuration or policy is properly configured. |
| isExpectedUserImpact | Bool | Indicates whether the user gets affected if the configuration will be applied. |
| osPlatform | String | Platform of the operating system running on the device. Specific operating systems with variations within the same family, such as Windows 10 and Windows 11. See [Supported operating systems, platforms and capabilities](/en-us/defender-vulnerability-management/tvm-supported-os) for details. |
| osVersion | String | Specific version of the operating system running on the device. |
| rbacGroupName | String | The role-based access control (RBAC) group. If the device isn't assigned to any RBAC group, the value will be "Unassigned." If the organization doesn't contain any RBAC groups, the value will be "None." |
| rbacGroupId | String | The role-based access control (RBAC) group ID. |
| recommendationReference | String | A reference to the recommendation ID related to the software. |
| timestamp | String | Last time the configuration was seen on the device. |

### 1.3 Properties (via files)

| Property (ID) | Data type | Description |
| --- | --- | --- |
| Export files | array[string] | A list of download URLs for files holding the current snapshot of the organization. |
| GeneratedTime | String | The time that the export was generated. |

## 2. Export software inventory assessment

Returns all of the installed software and their details on each device.

### 2.1 Methods

| Method | Data type | Description |
| --- | --- | --- |
| Export software inventory assessment **(JSON response)** | Software inventory by device collection. See: 2.2 Properties (JSON response) | Returns a table with an entry for every unique combination of DeviceId, SoftwareVendor, SoftwareName, SoftwareVersion. The API pulls all data in your organization as JSON responses. This method is best for small organizations with less than 100-K devices. The response is paginated, so you can use the @odata.nextLink field from the response to fetch the next results. |
| Export software inventory assessment **(via files)** | Software inventory by device files. See: 2.3 Properties (via files) | Returns a table with an entry for every unique combination of DeviceId, SoftwareVendor, SoftwareName, SoftwareVersion. This API solution enables pulling larger amounts of data faster and more reliably. So, it's recommended for large organizations, with more than 100-K devices. This API pulls all data in your organization as download files. The response contains URLs to download all the data from Azure Storage. This API enables you to download data from Azure Storage as follows: <br>1. Call the API to get a list of download URLs with your organization data<br>2. Download the files using the download URLs and process the data as you like. |

### 2.2 Properties (JSON response)

| Property (ID) | Data type | Description |
| --- | --- | --- |
| DeviceId | String | Unique identifier for the device in the service. |
| DeviceName | String | Fully qualified domain name (FQDN) of the device. |
| DiskPaths | Array[string] | Disk evidence that the product is installed on the device. |
| EndOfSupportDate | String | The date in which support for this software has or will end. |
| EndOfSupportStatus | String | End of support status. Can contain these possible values: None, EOS Version, Upcoming EOS Version, EOS Software, Upcoming EOS Software. |
| NumberOfWeaknesses | Int | Number of weaknesses on this software on this device. |
| OSPlatform | String | Platform of the operating system running on the device; specific operating systems with variations within the same family, such as Windows 10 and Windows 11. See [Supported operating systems, platforms and capabilities](/en-us/defender-vulnerability-management/tvm-supported-os) for details. |
| RbacGroupName | String | The role-based access control (RBAC) group. If this device isn't assigned to any RBAC group, the value will be "Unassigned." If the organization doesn't contain any RBAC groups, the value will be "None." |
| rbacGroupId | String | The role-based access control (RBAC) group ID. |
| RegistryPaths | Array[string] | Registry evidence that the product is installed in the device. |
| SoftwareFirstSeenTimestamp | String | The first time this software was seen on the device. |
| SoftwareName | String | Name of the software product. |
| SoftwareVendor | String | Name of the software vendor. |
| SoftwareVersion | String | Version number of the software product. |

### 2.3 Properties (via files)

| Property (ID) | Data type | Description |
| --- | --- | --- |
| Export files | array[string] | A list of download URLs for files holding the current snapshot of the organization. |
| GeneratedTime | String | The time that the export was generated. |

## 3. Export software vulnerabilities assessment

Returns all the known vulnerabilities on a device and their details, for all devices.

### 3.1 Methods

| Method | Data type | Description |
| --- | --- | --- |
| Export software vulnerabilities assessment **(JSON response)** | Investigation collection See: 3.2 Properties (JSON response) | Returns a table with an entry for every unique combination of DeviceId, SoftwareVendor, SoftwareName, SoftwareVersion, CveId. The API pulls all data in your organization as JSON responses. This method is best for small organizations with less than 100-K devices. The response is paginated, so you can use the @odata.nextLink field from the response to fetch the next results. |
| Export software vulnerabilities assessment **(via files)** | Investigation entity See: 3.3 Properties (via files) | Returns a table with an entry for every unique combination of DeviceId, SoftwareVendor, SoftwareName, SoftwareVersion, CveId. This API solution enables pulling larger amounts of data faster and more reliably. So, it's recommended for large organizations, with more than 100-K devices. This API pulls all data in your organization as download files. The response contains URLs to download all the data from Azure Storage. This API enables you to download all your data from Azure Storage as follows: <br>1. Call the API to get a list of download URLs with all your organization data.<br>2. Download all the files using the download URLs and process the data as you like. |
| **Delta export** software vulnerabilities assessment **(JSON response)** | Investigation collection See: 3.4 Properties Delta export (JSON response) | Returns a table with an entry for every unique combination of: DeviceId, SoftwareVendor, SoftwareName, SoftwareVersion, CveId, and EventTimestamp. <br> The API pulls data in your organization as JSON responses. The response is paginated, so you can use the @odata.nextLink field from the response to fetch the next results. The full software vulnerabilities assessment (JSON response) is used to obtain an entire snapshot of the software vulnerabilities assessment of your organization by device. However, the delta export API call is used to fetch only the changes that have happened between a selected date and the current date (the "delta" API call). Instead of getting a full export with a large amount of data every time, you'll only get specific information on new, fixed, and updated vulnerabilities. Delta export API call can also be used to calculate different KPIs such as "how many vulnerabilities were fixed?" or "how many new vulnerabilities were added to my organization?" <br><br> Because the Delta export API call for software vulnerabilities returns data for only a targeted date range, it isn't considered a *full export*. |

### 3.2 Properties (JSON response)

| Property (ID) | Data type | Description |
| --- | --- | --- |
| CveId | String | Unique identifier assigned to the security vulnerability under the Common Vulnerabilities and Exposures (CVE) system. |
| CvssScore | String | The CVSS score of the CVE. |
| DeviceId | String | Unique identifier for the device in the service. |
| DeviceName | String | Fully qualified domain name (FQDN) of the device. |
| DiskPaths | Array[string] | Disk evidence that the product is installed on the device. |
| ExploitabilityLevel | String | The exploitability level of this vulnerability (NoExploit, ExploitIsPublic, ExploitIsVerified, ExploitIsInKit) |
| FirstSeenTimestamp | String | First time the CVE of this product was seen on the device. |
| Id | String | Unique identifier for the record. |
| LastSeenTimestamp | String | Last time the CVE was seen on the device. |
| OSPlatform | String | Platform of the operating system running on the device; specific operating systems with variations within the same family, such as Windows 10 and Windows 11. See [Supported operating systems, platforms and capabilities](/en-us/defender-vulnerability-management/tvm-supported-os) for details. |
| RbacGroupName | String | The role-based access control (RBAC) group. If this device isn't assigned to any RBAC group, the value will be "Unassigned." If the organization doesn't contain any RBAC groups, the value will be "None." |
| rbacGroupId | String | The role-based access control (RBAC) group ID. |
| RecommendationReference | String | A reference to the recommendation ID related to this software. |
| RecommendedSecurityUpdate | String | Name or description of the security update provided by the software vendor to address the vulnerability. |
| RecommendedSecurityUpdateId | String | Identifier of the applicable security updates or identifier for the corresponding guidance or knowledge base (KB) articles. |
| Registry Paths | Array[string] | Registry evidence that the product is installed in the device. |
| SecurityUpdateAvailable | Boolean | Indicates whether a security update is available for the software. |
| SoftwareName | String | Name of the software product. |
| SoftwareVendor | String | Name of the software vendor. |
| SoftwareVersion | String | Version number of the software product. |
| VulnerabilitySeverityLevel | String | Severity level that is assigned to the security vulnerability based on the CVSS score. |

### 3.3 Properties (via files)

| Property (ID) | Data type | Description |
| --- | --- | --- |
| Export files | array[string] | A list of download URLs for files holding the current snapshot of the organization. |
| GeneratedTime | String | The time that the export was generated. |

### 3.4 Properties (delta export JSON response)

| Property (ID) | Data type | Description |
| --- | --- | --- |
| CveId | String | Unique identifier assigned to the security vulnerability under the Common Vulnerabilities and Exposures (CVE) system. |
| CvssScore | String | The CVSS score of the CVE. |
| DeviceId | String | Unique identifier for the device in the service. |
| DeviceName | String | Fully qualified domain name (FQDN) of the device. |
| DiskPaths | Array[string] | Disk evidence that the product is installed on the device. |
| EventTimestamp | String | The time the delta event was found. |
| ExploitabilityLevel | String | The exploitability level of the vulnerability (NoExploit, ExploitIsPublic, ExploitIsVerified, ExploitIsInKit) |
| FirstSeenTimestamp | String | First time the CVE of the product was seen on the device. |
| Id | String | Unique identifier for the record. |
| LastSeenTimestamp | String | Last time the CVE was seen on the device. |
| OSPlatform | String | Platform of the operating system running on the device; specific operating systems with variations within the same family, such as Windows 10 and Windows 11. See [Supported operating systems, platforms and capabilities](/en-us/defender-vulnerability-management/tvm-supported-os) for details. |
| RbacGroupName | String | The role-based access control (RBAC) group. If this device isn't assigned to any RBAC group, the value will be "Unassigned." If the organization doesn't contain any RBAC groups, the value will be "None." |
| RecommendationReference | String | A reference to the recommendation ID related to this software. |
| RecommendedSecurityUpdate | String | Name or description of the security update provided by the software vendor to address the vulnerability. |
| RecommendedSecurityUpdateId | String | Identifier of the applicable security updates or identifier for the corresponding guidance or knowledge base (KB) articles |
| RegistryPaths | Array[string] | Registry evidence that the product is installed in the device. |
| SoftwareName | String | Name of the software product. |
| SoftwareVendor | String | Name of the software vendor. |
| SoftwareVersion | String | Version number of the software product. |
| Status | String | **New** (for a new vulnerability introduced on a device). **Fixed** (for a vulnerability that doesn't exist anymore on the device, which means it was remediated). **Updated** (for a vulnerability on a device that has changed. The possible changes are: CVSS score, exploitability level, severity level, DiskPaths, RegistryPaths, RecommendedSecurityUpdate). |
| VulnerabilitySeverityLevel | String | Severity level assigned to the security vulnerability based on the CVSS score. |

## 4. Export non product code software inventory assessment

Returns all of the installed software that does not have a [Common Platform Enumeration(CPE)](https://nvd.nist.gov/products/cpe) and their details on each device.

### 4.1 Methods

| Method | Data type | Description |
| --- | --- | --- |
| Export non product code software inventory assessment **(JSON response)** | Non product code software inventory by device collection. See: 4.2 Properties (JSON response) | Returns a table with an entry for every unique combination of DeviceId, SoftwareVendor, SoftwareName, SoftwareVersion. The API pulls all data in your organization as JSON responses. This method is best for small organizations with less than 100-K devices. The response is paginated, so you can use the @odata.nextLink field from the response to fetch the next results. |
| Export non product code software inventory assessment **(via files)** | Non product code software inventory by device files. See: 4.3 Properties (via files) | Returns a table with an entry for every unique combination of DeviceId, SoftwareVendor, SoftwareName, SoftwareVersion. This API solution enables pulling larger amounts of data faster and more reliably. So, it's recommended for large organizations, with more than 100-K devices. This API pulls all data in your organization as download files. The response contains URLs to download all the data from Azure Storage. This API enables you to download data from Azure Storage as follows: <br>1. Call the API to get a list of download URLs with your organization data<br>2. Download the files using the download URLs and process the data as you like. |

### 4.2 Properties (JSON response)

| Property (ID) | Data type | Description |
| --- | --- | --- |
| DeviceId | string | Unique identifier for the device in the service. |
| DeviceName | string | Fully qualified domain name (FQDN) of the device. |
| OSPlatform | string | Platform of the operating system running on the device. These are specific operating systems with variations within the same family, such as Windows 10 and Windows 11. See [Supported operating systems, platforms and capabilities](/en-us/defender-vulnerability-management/tvm-supported-os) for details. |
| RbacGroupName | string | The role-based access control (RBAC) group. If this device isn't assigned to any RBAC group, the value will be "Unassigned." If the organization doesn't contain any RBAC groups, the value will be "None." |
| RbacGroupId | string | The role-based access control (RBAC) group ID. |
| SoftwareLastSeenTimestamp | string | The last time this software was seen on the device. |
| SoftwareName | string | Name of the software product. |
| SoftwareVendor | string | Name of the software vendor. |
| SoftwareVersion | string | Version number of the software product. |

### 4.3 Properties (via files)

| Property (ID) | Data type | Description |
| --- | --- | --- |
| Export files | array[string] | A list of download URLs for files holding the current snapshot of the organization. |
| GeneratedTime | String | The time that the export was generated. |