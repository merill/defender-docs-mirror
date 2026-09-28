---
layout: Conceptual
title: DeviceFileCertificateInfo table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-devicefilecertificateinfo-table
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about file signing information in the DeviceFileCertificateInfo table of the advanced hunting schema
ms.service: defender-xdr
ms.subservice: adv-hunting
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.custom:
- cx-ti
- cx-ah
ms.topic: reference
ms.date: 2025-03-28T00:00:00.0000000Z
locale: en-us
document_id: fe4e5378-e76f-ff64-378b-e1bec0650ddb
document_version_independent_id: fe4e5378-e76f-ff64-378b-e1bec0650ddb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-devicefilecertificateinfo-table.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-devicefilecertificateinfo-table
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-devicefilecertificateinfo-table.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 850ceb6a-3fb4-99f9-744e-ae72e02cda7b
---

# DeviceFileCertificateInfo table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn

The `DeviceFileCertificateInfo` table in the [advanced hunting](advanced-hunting-overview) schema contains information about file signing certificates. This table uses data obtained from certificate verification activities regularly performed on files on endpoints.

This advanced hunting table is populated by records from Microsoft Defender for Endpoint. If your organization hasn't deployed the service in Microsoft Defender, queries that use the table aren't going to work or return any results. For more information about how to deploy Defender for Endpoint in the Defender portal, read [Deploy supported services](deploy-supported-services).

For information on other tables in the advanced hunting schema, [see the advanced hunting reference](advanced-hunting-schema-tables).

| Column name | Data type | Description |
| --- | --- | --- |
| `Timestamp` | `datetime` | Date and time when the record was generated |
| `DeviceId` | `string` | Unique identifier for the device in the service |
| `DeviceName` | `string` | Fully qualified domain name (FQDN) of the device |
| `SHA1` | `string` | SHA-1 of the file that the recorded action was applied to |
| `IsSigned` | `bool` | Indicates whether the file is signed |
| `SignatureType` | `string` | Indicates whether signature information was read as embedded content in the file itself or read from an external catalog file |
| `Signer` | `string` | Information about the signer of the file |
| `SignerHash` | `string` | Unique hash value identifying the signer |
| `Issuer` | `string` | Information about the issuing certificate authority (CA) |
| `IssuerHash` | `string` | Unique hash value identifying issuing certificate authority (CA) |
| `CertificateSerialNumber` | `string` | Identifier for the certificate that is unique to the issuing certificate authority (CA) |
| `CrlDistributionPointUrls` | `string` | JSON array listing the URLs of network shares that contain certificates and certificate revocation lists (CRLs) |
| `CertificateCreationTime` | `datetime` | Date and time the certificate was created |
| `CertificateExpirationTime` | `datetime` | Date and time the certificate is set to expire |
| `CertificateCountersignatureTime` | `datetime` | Date and time the certificate was countersigned |
| `IsTrusted` | `bool` | Indicates whether the file is trusted based on the results of the WinVerifyTrust function, which checks for unknown root certificate information, invalid signatures, revoked certificates, and other questionable attributes |
| `IsRootSignerMicrosoft` | `boolean` | Indicates whether the signer of the root certificate is Microsoft and if the file is included in Windows operating system |
| `ReportId` | `long` | Event identifier based on a repeating counter. To identify unique events, this column must be used in conjunction with the DeviceName and Timestamp columns. |