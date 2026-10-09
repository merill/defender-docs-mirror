---
layout: Conceptual
title: Tenable data connector in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/tenable-data-connector
author: DebLanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Learn how to the Tenable data connector in Microsoft Security Exposure Management.
ms.topic: overview
ms.date: 2024-09-24T00:00:00.0000000Z
locale: en-us
document_id: f11301c7-38f1-f425-e965-bbf788f43b93
document_version_independent_id: f11301c7-38f1-f425-e965-bbf788f43b93
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/Tenable-data-connector.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: tenable-data-connector
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/Tenable-data-connector.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://authoring-docs-microsoft.poolparty.biz/devrel/2ed91286-6cf7-4b83-810d-75d0ee3b09dd
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/6735bd7e-4f7b-457d-b58c-29e6f0198677
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 2145ae6c-5614-9c22-d3c9-9a1cb3b411bb
---

# Tenable data connector in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn

To integrate with Tenable, you need Tenable Vulnerability Management API access and secret keys for authentication. To generate the secret keys, you must have Basic, Scan Operator, Standard, Scan Manager, or Administrator user roles in Tenable Vulnerability Management.

## Tenable configuration

Instructions for generating API keys for Tenable Vulnerability Management can be found [here](https://docs.tenable.com/vulnerability-management/Content/Settings/my-account/GenerateAPIKey.htm).

1. To generate API keys for your own account, access the My Account page.
2. Select the API Keys tab to view the API Keys section.
3. Select Generate, and note that the **Generate API Keys** window appears with a warning that Any existing API keys are replaced when you select the Generate button
4. Select **Generate.** Tenable Vulnerability Management generates new access and secret keys, and displays the new keys in the **Custom API Keys** section of the page.
5. Copy the new access and secret keys to a safe location.

Caution

Be sure to copy the access and secret keys before you close the API Keys tab. After you close this tab, you cannot retrieve the keys from Tenable Vulnerability Management.

 6. If you have an Administrator account, you can generate API keys for any user account.

### For more information

To understand the Tenable API authorization model, see: [Authorization (tenable.com)](https://developer.tenable.com/docs/authorization)

## Establish Tenable connection in Exposure Management

To establish a connection with Tenable in Exposure Management, follow these steps:

1. Open the [Data Connectors](https://security.microsoft.com/exposure-data-connectors) from the Exposure Management navigation and select **Connect** in the Tenable tile.
2. Enter your Tenable Access key and Secret key details and select **Connect**.

## Retrieved data

Exposure Management retrieves data on compute devices from Tenable, including machines and virtual machines. It also retrieves some networking data to identify those devices.

Exposure Management also retrieves vulnerability findings from Tenable on those assets.

The vulnerability data retrieved for Tenable is applicable to CVEs only, and not other types of vulnerabilities or misconfigurations. Tenable shows total vulnerability counts that include other non-CVE misconfigurations as well, so these counts aren't applicable to the numbers of vulnerabilities ingested to Exposure Management.

| Category | Properties |
| --- | --- |
| **Assets/devices** | - biosUuid- Net Bios names- Operating systems- Cloud Provider ID (for example, Azure VM ID)- System Types- Tenable Criticality- Network interfaces (see below) |
| **Network interface** | - IP information- Mac address- FQDNs |

Note

To retrieve the data on criticality of your Tenable assets (Tenable [Asset Criticality Rating](https://developer.tenable.com/docs/lumin-tio)), you must have a [Tenable Lumin license](https://docs.tenable.com/vulnerability-management/Content/Lumin/Lumin.htm?_gl=1*129gx63*_ga*OTMzMjE4NDQ4LjE3MzE5MzcxOTM.*_ga_HSJ1XWV6ND*MTczMTkzNzE5Mi4xLjEuMTczMTkzNzMyMS41OS4wLjEyNDQzNzMzOTc.) with Tenable. Criticality on devices is used by Exposure Management to discover attack paths to the most critical devices in your environment.

## Troubleshooting the connector

Here are some common issues that might arise when configuring the Tenable Connector, and suggestions for how to resolve them.

| **Error Type** | **Troubleshooting Action** |
| --- | --- |
| **Error code** 401: Authorization failure | An authorization failure indicates that credentials might not be correct, or there might not be sufficient permissions to access the Tenable data. Check your credentials and make sure they're correct and valid. Make sure your Tenable.io account has sufficient permissions to read the data. See the Tenable configuration section for details on how to properly generate the API keys. |
| **Error code 403:** Access forbidden error | This error indicates that the provided credentials lack the necessary permissions to run the requested APIs. Update your credentials/ API keys with the proper permissions as described in the configuration section. |
| **Error code 409**: Possible insufficient permissions or temporary connection error | In the case where this error message appears without any additional information, verify the connector configuration (API endpoint and Keys). If these are valid and the issue doesn't resolve on its own, contact Support. |
| **Error code 429** 'Too many requests" | The system periodically pulls data from the configured external providers, which might have a limit on the number of concurrent requests. We recommend creating a dedicated account for the connector to avoid reaching this limit. |
| Not seeing my assets or the vulnerabilities reported by Tenable in the ingested data | See Retrieved data for a description of the data expected to be retrieved by the Tenable connector. Note that Tenable counts the number of reported vulnerabilities differently than Exposure Management (since only CVEs are ingested to Exposure Management), so these numbers might not match. If there's still missing data, contact Support. |
| Seeing only vulnerability management data imported, not data from other Tenable products | The Tenable connector currently supports only vulnerability data from Tenable Vulnerability Management. If you're interested in other types of data, enter a request through the Request new connectors feedback option on the Data Connectors page. |
| Not seeing any Tenable data ingested | Ensure you Tenable connector is properly connected and not in an error state. Run queries on the Exposure Graph via Advanced Hunting (as described in Getting value from your data connectors, [Advanced Hunting](value-data-connectors#advanced-hunting)) to check for the Tenable sourced data. If you're still not seeing any data ingested, contact Support. |
| Configure Tenable allowed IPs to enable Exposure Management connectors to access Tenable | Read how to add the set of IPs to add to your allowlist here: [Allowlist IP addresses](configure-data-connectors#allowlist-ip-addresses) |
| I'm using Tenable Security Center (the on-premises version), can I connect to that via the Tenable connector? | We currently support only Tenable Vulnerability Management and don't support Tenable SC. We're working to add Tenable.sc in the future. |