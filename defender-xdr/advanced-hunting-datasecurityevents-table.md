---
layout: Conceptual
title: DataSecurityEvents table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-datasecurityevents-table
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about the DataSecurityEvents table of the advanced hunting schema, which contains information about user activities that violate user-defined or default policies in the Microsoft Purview suite of solutions.
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
document_id: 0fd8643c-f866-5b75-eb88-a7987fd3b509
document_version_independent_id: 0fd8643c-f866-5b75-eb88-a7987fd3b509
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-datasecurityevents-table.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-datasecurityevents-table
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-datasecurityevents-table.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/57eae111-0f3b-497e-be07-450fd1409dea
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac8bf8ab-8134-4c9a-9f2e-58b31575b492
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
platformId: 1e9a5a17-b5c6-9f4f-bb37-be22817edc2b
---

# DataSecurityEvents table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn

The `DataSecurityEvents` table in the [advanced hunting](advanced-hunting-overview) schema contains information about user activities that violate user-defined or default policies in the Microsoft Purview suite of solutions. Each log represents a single user activity enriched with proprietary Microsoft detections (like sensitive info types) and user-defined enrichment labels like domain categories, sensitivity labels, and others.

This advanced hunting table is populated by records from Microsoft Purview Insider Risk Management. If your organization hasn't opted in to share insider risk alerts with Microsoft Defender, queries that use the table aren't going to work or return any results. For more information, read [Investigate insider risk threats](irm-investigate-alerts-defender).

Use this reference to construct queries that return information from this table. For information on other tables in the advanced hunting schema, [see the advanced hunting reference](advanced-hunting-schema-tables).

| Column name | Data type | Description |
| --- | --- | --- |
| `ApplicationNames` | `string` | List of application names used or related to the event |
| `DeviceId` | `string` | Unique identifier for the device in Microsoft Defender for Endpoint |
| `DeviceName` | `string` | Fully qualified domain name (FQDN) of the device |
| `AadDeviceId` | `guid` | Unique identifier for the device in Microsoft Entra ID |
| `IsManagedDevice` | `bool` | Indicates if the device is managed by the organization (True) or not (False) |
| `DlpPolicyMatchInfo` | `string` | Information around the list of data loss prevention (DLP) policies matching this event |
| `DlpPolicyEnforcementMode` | `int` | Indicates the Data Loss Prevention policy that was enforced; value can be: 0 (None), 1 (Audit), 2 (Warn), 3 (Warn and bypass), 4 (Block), 5 (Allow) |
| `DlpPolicyRuleMatchInfo` | `dynamic` | Details of the data loss prevention (DLP) rules that matched with this event; in JSON array format |
| `FileRenameInfo` | `string` | Details of the file (file name and extension) before this event |
| `PhysicalAccessPointInfo` | `object` | Information about the physical access in the event, including the physical access point's unique identifier, name, status, and the tag assigned to the asset |
| `PhysicalAccessPointId` | `string` | Unique identifier for the physical access point |
| `PhysicalAccessPointName` | `string` | Name of the physical access point |
| `PhysicalAccessStatus` | `string` | Status of physical access, whether it succeeded or failed |
| `PhysicalAssetTag` | `string` | Tag assigned to the asset as configured in Microsoft Insider Risk Management global settings |
| `RemovableMediaInfo` | `object` | List of any removable media involved in the behavior, including the serial number of the removable media device, the manufacturer of the removable media device, and the model of the removable device |
| `RemovableMediaManufacturer` | `string` | Manufacturer name of the removable device |
| `RemovableMediaModel` | `string` | Model name of the removable device |
| `RemovableMediaSerialNumber` | `string` | Serial number of the removable device |
| `TeamsChannelName` | `string` | Name of the Teams channel |
| `TeamsChannelType` | `string` | Type of the Teams channel |
| `TeamsTeamName` | `string` | Name of the Teams team |
| `UserAlternateEmails` | `string` | Alternate emails or aliases of the user |
| `AccountUpn` | `string` | User principal name (UPN) of the account |
| `AccountObjectId` | `string` | Unique identifier for the account in Microsoft Entra ID |
| `Department` | `string` | Name of the department that the account user belongs to |
| `SourceCodeInfo` | `string` | Details of the source code repository involved in the event |
| `CcPolicyMatchInfo` | `dynamic` | Details of the Communications Compliance policy matches for this event; in JSON array format |
| `IPAddress` | `string` | IP addresses of the clients on which the activity was performed; can contain multiple IPs if related to Microsoft Defender for Cloud Apps alerts |
| `Timestamp` | `datetime` | Date and time when the event was recorded |
| `DeviceSourceLocationType` | `int` | Indicates the type of location where the endpoint signals originated from; values can be: 0 (Unknown), 1 (Local), 2 (Remote), 3 (Removable), 4 (Cloud), 5 (File share) |
| `DeviceDestinationLocationType` | `int` | Indicates the type of location where the endpoint signals connected to; values can be: 0 (Unknown), 1 (Local), 2 (Remote), 3 (Removable), 4 (Cloud), 5 (File share) |
| `IrmPolicyMatchInfo` | `dynamic` | Details of Insider Risk Management policy matches for the content involved in the event; in JSON array format |
| `ExternalUrlDomains` | `string` | Websites or service URLs involved in this event that is classified as External in Insider Risk Management global settings |
| `InternetMessageId` | `string` | Public-facing identifier for the email or Teams message that is set by the sending email system |
| `NetworkMessageId` | `guid` | Unique identifier for the email, generated by Microsoft 365 |
| `EmailSubject` | `string` | Subject of the email |
| `ObjectId` | `string` | Unique identifier of the object that the recorded action was applied to, in case of files, it includes the extension |
| `ObjectName` | `string` | Name of the object that the recorded action was applied to, in case of files, it includes the extension |
| `ObjectType` | `string` | Type of object, such as a file or a folder, that the recorded action was applied to |
| `ObjectSize` | `int` | Size of the object in bytes |
| `IsHidden` | `bool` | Indicates whether the user has marked the content as hidden (True) or not (False) |
| `ActivityId` | `guid` | Unique identifier of the activity log |
| `ActionType` | `string` | Type of activity that triggered the event |
| `SensitiveInfoTypeInfo` | `dynamic` | Details of Data Loss Prevention sensitive info types detected in the impacted asset |
| `SensitivityLabelId` | `string` | The current Microsoft Information Protection sensitivity label ID associated with the item |
| `SharepointSiteSensitivityLabelIds` | `string` | The current Microsoft Information Protection sensitivity label ID assigned to the parent site of the item related to SharePoint activities |
| `PreviousSensitivityLabelId` | `string` | The previous Microsoft Information Protection sensitivity label ID associated with the item in case of activities where the sensitivity label was changed |
| `Operation` | `string` | Name of the admin activity |
| `RecipientEmailAddress` | `string` | Email address of the recipient, or email address of the recipient after distribution list expansion |
| `SiteUrl` | `string` | The URL of the site where the file or folder accessed by the user is located |
| `SourceRelativeUrl` | `string` | The URL of the folder that contains the file accessed by the user |
| `PrinterName` | `string` | List of printers involved in the behavior |
| `IrmActionCategory` | `enum` | A unique enumeration value indicating the activity category in Microsoft Purview Insider Risk Management |
| `RiskyAIUsageAccessedResourceInfo` | `object` | Details of the resources accessed or referenced by the application involved in the risky AI usage event |
| `RiskyAIUsageAppCategory` | `string` | Details of the category of the application involved in the risky AI usage event |
| `RiskyAIUsageSensitivityLabelsInfo` | `object` | Information regarding the sensitivity labels of entities involved in the risky AI usage event |
| `SequenceCorrelationId` | `string` | Details of the sequence activity |