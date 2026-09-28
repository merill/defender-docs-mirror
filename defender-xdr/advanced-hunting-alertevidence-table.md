---
layout: Conceptual
title: AlertEvidence table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-alertevidence-table
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about information associated with alerts in the AlertEvidence table of the advanced hunting schema
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
- msecd-doc-authoring-1015
ms.topic: reference
ms.date: 2026-08-07T00:00:00.0000000Z
locale: en-us
document_id: 301b2621-a2e4-e44d-6906-eafd5c6585f0
document_version_independent_id: 301b2621-a2e4-e44d-6906-eafd5c6585f0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-alertevidence-table.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-alertevidence-table
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-alertevidence-table.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
platformId: 84487e5d-a7ca-16c0-7848-5f402ee1edfa
---

# AlertEvidence table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn

The `AlertEvidence` table in the [advanced hunting](advanced-hunting-overview) schema contains entities associated with alerts from Microsoft Defender for Endpoint, Microsoft Defender for Office 365, Microsoft Defender for Cloud Apps, Microsoft Defender for Identity, and onboarded Microsoft Sentinel workspaces. Entities can include files, IP addresses, URLs, users, and devices. Use this reference to construct queries that return information from this table.

Data availability depends on the Microsoft Defender services deployed and the Microsoft Sentinel workspaces you can access in the Defender portal. Join `AlertEvidence` with [`AlertInfo`](advanced-hunting-alertinfo-table) on the `AlertId` column to retrieve alert metadata with its related entities and evidence. For more information, see [Deploy supported services](deploy-supported-services) and [Transition your Microsoft Sentinel environment to the Defender portal](/en-us/azure/sentinel/move-to-defender).

For information on other tables in the advanced hunting schema, [see the advanced hunting reference](advanced-hunting-schema-tables).

| Column name | Data type | Description |
| --- | --- | --- |
| `Timestamp` | `datetime` | Date and time when the event was recorded |
| `AlertId` | `string` | Unique identifier for the alert |
| `Title` | `string` | Title of the alert |
| `Categories` | `string` | List of categories that the information belongs to, in JSON array format |
| `AttackTechniques` | `string` | MITRE ATT&CK techniques associated with the activity that triggered the alert |
| `ServiceSource` | `string` | Product or service that provided the alert information |
| `DetectionSource` | `string` | Detection technology or sensor that identified the notable component or activity |
| `EntityType` | `string` | Type of object, such as a file, a process, a device, or a user |
| `EvidenceRole` | `string` | How the entity is involved in an alert, indicating whether it is impacted or is merely related |
| `EvidenceDirection` | `string` | Indicates whether the entity is the source or the destination of a network connection |
| `FileName` | `string` | Name of the file that the recorded action was applied to |
| `FolderPath` | `string` | Folder containing the file that the recorded action was applied to |
| `SHA1` | `string` | SHA-1 of the file that the recorded action was applied to |
| `SHA256` | `string` | SHA-256 of the file that the recorded action was applied to. This field is usually not populated—use the SHA1 column when available. |
| `FileSize` | `long` | Size of the file in bytes |
| `ThreatFamily` | `string` | Malware family that the suspicious or malicious file or process has been classified under |
| `RemoteIP` | `string` | IP address that was being connected to |
| `RemoteUrl` | `string` | URL or fully qualified domain name (FQDN) that was being connected to |
| `AccountName` | `string` | User name of the account |
| `AccountDomain` | `string` | Domain of the account |
| `AccountSid` | `string` | Security Identifier (SID) of the account |
| `AccountObjectId` | `string` | Unique identifier for the account in Microsoft Entra ID |
| `AccountUpn` | `string` | User principal name (UPN) of the account |
| `DeviceId` | `string` | Unique identifier for the device in the service |
| `DeviceName` | `string` | Fully qualified domain name (FQDN) of the device |
| `LocalIP` | `string` | IP address assigned to the local device used during communication |
| `NetworkMessageId` | `string` | Unique identifier for the email, generated by Office 365 |
| `EmailSubject` | `string` | Subject of the email |
| `Application` | `string` | Application that performed the recorded action |
| `ApplicationId` | `int` | Unique identifier for the application |
| `OAuthApplicationId` | `string` | Unique identifier of the third-party OAuth application |
| `ProcessCommandLine` | `string` | Command line used to create the new process |
| `RegistryKey` | `string` | Registry key that the recorded action was applied to |
| `RegistryValueName` | `string` | Name of the registry value that the recorded action was applied to |
| `RegistryValueData` | `string` | Data of the registry value that the recorded action was applied to |
| `AdditionalFields` | `string` | Additional information about the entity or event |
| `Severity` | `string` | Indicates the potential impact (high, medium, or low) of the threat indicator or breach activity identified by the alert |
| `CloudResource` | `string` | Cloud resource name |
| `CloudPlatform` | `string` | The cloud platform that the resource belongs to, can be Azure, Amazon Web Services, or Google Cloud Platform |
| `ResourceType` | `string` | Type of cloud resource |
| `ResourceID` | `string` | Unique identifier of the cloud resource accessed |
| `SubscriptionId` | `string` | Unique identifier of the cloud service subscription |