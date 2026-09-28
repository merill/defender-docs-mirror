---
layout: Conceptual
title: BehaviorEntities table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-behaviorentities-table
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about behaviors in the BehaviorEntities table of the advanced hunting schema
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
ms.date: 2026-01-12T00:00:00.0000000Z
locale: en-us
document_id: a084797a-6862-196f-a539-21324e5b0cf9
document_version_independent_id: a084797a-6862-196f-a539-21324e5b0cf9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-behaviorentities-table.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-behaviorentities-table
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-behaviorentities-table.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 4d257f36-e64d-252c-a18d-cb68623b55a8
---

# BehaviorEntities table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn

The `BehaviorEntities` table in the [advanced hunting](advanced-hunting-overview) schema contains information about entities (file, process, device, user, and others) that are involved in a behavior in [Microsoft Defender for Cloud Apps](/en-us/defender-cloud-apps/what-is-defender-for-cloud-apps?toc=%2Fdefender-xdr%2Ftoc.json&amp;bc=%2Fdefender-xdr%2Fbreadcrumb%2Ftoc.json) and [User and Entity Behavior Analytics (UEBA)](/en-us/azure/sentinel/identify-threats-with-entity-behavior-analytics). Use this reference to construct queries that return information from this table.

Important

The `BehaviorEntities` table is in preview and is not available for GCC. The information here may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here. Have feedback to share? Fill out our [feedback form](https://forms.office.com/r/x0mX5hBkGu).

**Behaviors** are a type of data in Microsoft Defender XDR based on one or more raw events. Behaviors provide contextual insight into events and can, but not necessarily, indicate malicious activity. For more information, see the following articles:

- [Investigate behaviors with advanced hunting](/en-us/defender-cloud-apps/behaviors)
- [Translate raw security logs to behavioral insights using UEBA behaviors in Microsoft Sentinel](/en-us/azure/sentinel/entity-behaviors-layer)

This advanced hunting table is populated by records from both Defender for Cloud Apps and UEBA. If your organization doesn't deploy these services in Microsoft Defender, queries that use the table won't work or return any results. For more information about how to deploy services in Defender, see [Deploy supported services](deploy-supported-services).

To make sure Defender for Cloud Apps and UEBA data populate the `BehaviorEntities` table, follow the instructions in the following articles:

- [Connect Microsoft 365 to Microsoft Defender for Cloud Apps](/en-us/defender-cloud-apps/protect-office-365#prerequisites)
- [Enable the UEBA behaviors layer](/en-us/azure/sentinel/entity-behaviors-layer#enable-the-ueba-behaviors-layer)

For information on other tables in the advanced hunting schema, [see the advanced hunting reference](advanced-hunting-schema-tables).

| Column name | Data type | Description |
| --- | --- | --- |
| `Timestamp` | `datetime` | Date and time when the record was generated |
| `BehaviorId` | `string` | Unique identifier for the behavior |
| `Categories` | `string` | Type of threat indicator or breach activity identified by the behavior, as defined by the MITRE ATT&CK framework |
| `ServiceSource` | `string` | Product or service that identified the behavior |
| `DetectionSource` | `string` | Detection technology or sensor that identified the notable component or activity |
| `DataSources` | `string` | Products or services that provided information for the behavior |
| `EntityType` | `string` | Type of object, such as a file, a process, a device, or a user |
| `EntityRole` | `string` | Indicates whether the entity is impacted or merely related |
| `DetailedEntityRole` | `string` | The roles of the entity in the behavior |
| `FileName` | `string` | Name of the file that the behavior applies to |
| `FolderPath` | `string` | Folder containing the file that the behavior applies to |
| `SHA1` | `string` | SHA-1 of the file that the behavior applies to |
| `SHA256` | `string` | SHA-256 of the file that the behavior applies to |
| `FileSize` | `long` | Size, in bytes, of the file that the behavior applies to |
| `ThreatFamily` | `string` | Malware family that the suspicious or malicious file or process has been classified under |
| `RemoteIP` | `string` | IP address that was being connected to |
| `RemoteUrl` | `string` | URL or fully qualified domain name (FQDN) that was being connected to |
| `AccountName` | `string` | User name of the account |
| `AccountDomain` | `string` | Domain of the account |
| `AccountSid` | `string` | Security Identifier (SID) of the account |
| `AccountObjectId` | `string` | Unique identifier for the account in Microsoft Entra ID |
| `CloudPlatform ` | `string` | The cloud platform that the resource belongs to, can be Azure, Amazon Web Services, or Google Cloud Platform |
| `CloudResourceType ` | `string` | Type of cloud resource |
| `CloudResourceId` | `string` | Unique identifier of the cloud resource accessed |
| `CloudSubscriptionId ` | `string` | Unique identifier of the cloud service subscription |
| `AccountUpn` | `string` | User principal name (UPN) of the account |
| `DeviceId` | `string` | Unique identifier for the device in the service |
| `DeviceName` | `string` | Fully qualified domain name (FQDN) of the device |
| `LocalIP` | `string` | IP address assigned to the local device used during communication |
| `NetworkMessageId` | `string` | Unique identifier for the email, generated by Microsoft 365 |
| `EmailSubject` | `string` | Subject of the email |
| `EmailClusterId` | `string` | Identifier for the group of similar emails clustered based on heuristic analysis of their contents |
| `Application` | `string` | Application that performed the recorded action |
| `ApplicationId` | `int` | Unique identifier for the application |
| `OAuthApplicationId` | `string` | Unique identifier of the third-party OAuth application |
| `ProcessCommandLine` | `string` | Command line used to create the new process |
| `RegistryKey` | `string` | Registry key that the recorded action was applied to |
| `RegistryValueName` | `string` | Name of the registry value that the recorded action was applied to |
| `RegistryValueData` | `string` | Data of the registry value that the recorded action was applied to |
| `AdditionalFields` | `string` | Additional information about the behavior |
| `ActionType` | `string` | Type of behavior |