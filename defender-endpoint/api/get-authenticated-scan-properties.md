---
layout: Conceptual
title: Authenticated scan methods and properties - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/get-authenticated-scan-properties
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: The API response contains Microsoft Defender Vulnerability Management authenticated scans created in your tenant. You can request all the scans, all the scan definitions or add a new network our authenticated scan.
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
ms.date: 2025-11-10T00:00:00.0000000Z
locale: en-us
document_id: 7f01aa2a-4b77-c22e-709c-f2940fb3a848
document_version_independent_id: 7f01aa2a-4b77-c22e-709c-f2940fb3a848
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/get-authenticated-scan-properties.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/get-authenticated-scan-properties
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/get-authenticated-scan-properties.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: b82432bb-1057-9fff-8b32-a9ee8feb615b
---

# Authenticated scan methods and properties - Microsoft Defender for Endpoint | Microsoft Learn

Learn more about [Network authenticated scans](../network-devices).

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Properties

| Property | Data type | Description |
| --- | --- | --- |
| id | String | Scan ID. |
| scanType | Enum | The type of scan. Possible value is: `Network`. |
| scanName | String | Name of the scan. |
| isActive | Boolean | Status of whether the scan actively running. |
| orgId | String | Related organization ID. |
| intervalInHours | Int | The interval at which the scan runs. |
| createdBy | String | Unique identity of the user that created the scan. |
| targetType | String | The target type in the target field. Possible types are `IP Address` or `Hostname`. Default value is IP Address. |
| target | String | A comma separated list of targets to scan, either IP addresses or hostnames. |
| scanAuthenticationParams | Object | An object representing the authentication parameters, see Authentication parameters object properties for expected fields. This property is mandatory when creating a new scan and is optional when updating a scan. |
| scannerAgent | Object | An object representing the scanner agent, contains the machine Id of the scanning device. |

### Authentication parameters object properties

| Property | Data type | Description |
| --- | --- | --- |
| @odata.type | Enum | The scan type authentication parameters. Possible value is: `#microsoft.windowsDefenderATP.api.SnmpAuthParams` for the `Network` scan type. |
| type | Enum | The authentication method. Possible values vary based on @odata.type property.  - If @odata.type is `SnmpAuthParams`, possible values are `CommunityString`, `NoAuthNoPriv`, `AuthNoPriv`, `AuthPriv`. |
| KeyVaultUrl | String (Optional) | An optional property that specifies from which KeyVault the scanner should retrieve credentials. If KeyVault is specified there's no need to specify username, password. |
| KeyVaultSecretName | String (Optional) | An optional property that specifies KeyVault secret name from which the scanner should retrieve credentials. If KeyVault is specified there's no need to specify username, password. |
| Username | String (Optional) | Username when choosing `SnmpAuthParams` with any type other than `CommunityString`. |
| CommunityString | String (Optional) | Community string to use when choosing `SnmpAuthParams` with `CommunityString` |
| AuthProtocol | String (Optional) | Auth protocol to use with `SnmpAuthParams` and `AuthNoPriv` or `AuthPriv`. Possible values are `MD5`, `SHA1`. |
| AuthPassword | String (Optional) | Auth password to use with `SnmpAuthParams` and `AuthNoPriv` or `AuthPriv`. |
| PrivProtocol | String (Optional) | Priv protocol to use with `SnmpAuthParams` and `AuthPriv`. Possible values are `DES`, `3DES`, `AES`. |
| PrivPassword | String (Optional) | Priv password to use with `SnmpAuthParams` and `AuthPriv`. |