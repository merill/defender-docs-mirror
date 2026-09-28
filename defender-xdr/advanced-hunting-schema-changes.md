---
layout: Conceptual
title: Naming changes in the Microsoft Defender XDR advanced hunting schema - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-schema-changes
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Track and review naming changes tables and columns in the advanced hunting schema
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
ms.date: 2026-06-03T00:00:00.0000000Z
locale: en-us
document_id: 072050e1-2d81-43d8-3785-1fd92a2c6615
document_version_independent_id: 072050e1-2d81-43d8-3785-1fd92a2c6615
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-schema-changes.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-schema-changes
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-schema-changes.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 0a3661d8-4dd2-8c28-dc94-3f4808ca14b0
---

# Naming changes in the Microsoft Defender XDR advanced hunting schema - Microsoft Defender XDR | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

The [advanced hunting schema](advanced-hunting-schema-tables) is updated regularly to add new tables and columns. In some cases, existing columns names are renamed or replaced to improve the user experience. Refer to this article to review naming changes that could impact your queries.

Naming changes are automatically applied to queries that are saved in Microsoft Defender, including queries used by custom detection rules. You don't need to update these queries manually. However, you will need to update the following queries:

- Queries that are run using the API
- Queries that are saved elsewhere outside Microsoft Defender

## June 2026

- The [`AIAgentsInfo`](advanced-hunting-aiagentsinfo-table) table is transitioning to the [`AgentsInfo`](advanced-hunting-agentsinfo-table) table. The `AIAgentsInfo` table was originally built for Copilot Studio scenarios, and many of its columns were specific to that platform. The new `AgentsInfo` table provides a unified schema that supports agent inventory and governance for all agent types, including Copilot Studio, Microsoft Foundry, Microsoft Copilot, third-party agents, and endpoint-discovered agents. Microsoft Agent 365 customers should use the `AgentsInfo` table today.

    Key changes in the new table include expanded coverage for agent identity, authentication, permissions, lifecycle, and configuration. The new schema also includes a `RawAgentInfo` column that stores additional agent data in JSON format, ensuring no data loss as the schema evolves.

    To prepare for this change:

    - Update your advanced hunting queries to use the `AgentsInfo` table instead of `AIAgentsInfo`.
    - Review and update any filters, projections, or joins that reference `AIAgentsInfo` column names, as column names have changed in the new table.
    - Update any queries run through the API or saved outside Microsoft Defender XDR. Saved queries in Microsoft Defender XDR, including custom detection rules, are updated automatically.

    The `AIAgentsInfo` table remains accessible until July 1, 2026, to allow time for migration.

## November 2025

- The Boolean field values in advanced hunting results will change from numeric (`1` and `0`) to textual (`True` and `False`) on February 25, 2026. While your queries and custom detection rules won't be affected by this change, you might want to update your automated processes (for example, scripts, playbooks, or integrations) parsing these values.
- The [`AADSignInEventsBeta`](advanced-hunting-aadsignineventsbeta-table) and [`AADSpnSignInEventsBeta`](advanced-hunting-aadspnsignineventsbeta-table) tables are being replaced by [`EntraIdSignInEvents`](advanced-hunting-entraidsigninevents-table) and [`EntraIdSpnSignInEvents`](advanced-hunting-entraidspnsigninevents-table), respectively. These changes are being made to remove the former tables' preview status and to align them with the existing product branding.

    The `EntraIdSignInEvents` and `EntraIdSpnSignInEvents` tables are now available. The legacy `AADSignInEventsBeta`and `AADSpnSignInEventsBeta` tables will remain in the schema for 30 days to allow time for updating your queries. Your custom detections will be updated automatically and won't require any changes. On December 9, 2025, `AADSignInEventsBeta`and `AADSpnSignInEventsBeta` will be removed from the schema.

## September 2025

In the [AADSignInEventsBeta](advanced-hunting-aadspnsignineventsbeta-table) table, the `AadDeviceId` column is being replaced with a new column, called `EntraIdDeviceId`, to align with current product branding. The legacy `AadDeviceId` column will remain in the schema for 30 days to allow time for updating in your queries. After this period of 30 days, `AadDeviceId` will be removed from the schema.

## May 2025

In the [`IdentityInfo`](advanced-hunting-identityinfo-table) table, the `SourceProvider` column was replaced by the `IdentityEnvironment` column. This change was made to streamline the unified `IdentityInfo` table with a similar table in Microsoft Sentinel log analytics. Note that a new column, `SourceProviders` (with an *s*) was added in the unified table. This column refers to the source providers of the accounts for the identity.

## May 2021

The `AppFileEvents` table has been deprecated. The `CloudAppEvents` table includes information that used to be in the `AppFileEvents` table, along with other activities in cloud services.

## March 2021

The `DeviceTvmSoftwareInventoryVulnerabilities` table has been deprecated. Replacing it are the `DeviceTvmSoftwareInventory` and `DeviceTvmSoftwareVulnerabilities` tables.

## February 2021

- In the [EmailAttachmentInfo](advanced-hunting-emailattachmentinfo-table) and [EmailEvents](advanced-hunting-emailevents-table) tables, the `MalwareFilterVerdict` and `PhishFilterVerdict` columns have been replaced by the `ThreatTypes` column. The `MalwareDetectionMethod` and `PhishDetectionMethod` columns were also replaced by the `DetectionMethods` column. This streamlining allows us to provide more information under the new columns. The mapping is provided below.

    | Table name | Original column name | New column name | Reason for change |
    | --- | --- | --- | --- |
    | `EmailAttachmentInfo` | `MalwareDetectionMethod``PhishDetectionMethod` | `DetectionMethods` | Include more detection methods |
    | `EmailAttachmentInfo` | `MalwareFilterVerdict``PhishFilterVerdict` | `ThreatTypes` | Include more threat types |
    | `EmailEvents` | `MalwareDetectionMethod``PhishDetectionMethod` | `DetectionMethods` | Include more detection methods |
    | `EmailEvents` | `MalwareFilterVerdict``PhishFilterVerdict` | `ThreatTypes` | Include more threat types |
- In the `EmailAttachmentInfo` and `EmailEvents` tables, the `ThreatNames` column was added to give more information about the email threat. This column contains values like Spam or Phish.
- In the [DeviceInfo](advanced-hunting-deviceinfo-table) table, the `DeviceObjectId` column was replaced by the `AadDeviceId` column based on customer feedback.
- In the [DeviceEvents](advanced-hunting-deviceevents-table) table, several ActionType names were modified to better reflect the description of the action. Details of the changes can be found below.

    | Table name | Original ActionType name | New ActionType name | Reason for change |
    | --- | --- | --- | --- |
    | `DeviceEvents` | `UsbDriveMount` | `UsbDriveMounted` | Customer feedback |
    | `DeviceEvents` | `UsbDriveUnmount` | `UsbDriveUnmounted` | Customer feedback |
    | `DeviceEvents` | `WriteProcessMemoryApiCall` | `WriteToLsassProcessMemory` | Customer feedback |

## January 2021

| Column name | Original value name | New value name | Reason for change |
| --- | --- | --- | --- |
| `DetectionSource` | Defender for Cloud Apps | Microsoft Defender for Cloud Apps | Rebranding |
| `DetectionSource` | WindowsDefenderAtp | EDR | Rebranding |
| `DetectionSource` | WindowsDefenderAv | Antivirus | Rebranding |
| `DetectionSource` | WindowsDefenderSmartScreen | SmartScreen | Rebranding |
| `DetectionSource` | CustomerTI | Custom TI | Rebranding |
| `DetectionSource` | OfficeATP | Microsoft Defender for Office 365 | Rebranding |
| `DetectionSource` | MTP | Microsoft Defender XDR | Rebranding |
| `DetectionSource` | AzureATP | Microsoft Defender for Identity | Rebranding |
| `DetectionSource` | CustomDetection | Custom detection | Rebranding |
| `DetectionSource` | AutomatedInvestigation | Automated investigation | Rebranding |
| `DetectionSource` | ThreatExperts | Microsoft Threat Experts | Rebranding |
| `DetectionSource` | 3rd party TI | 3rd Party sensors | Rebranding |
| `ServiceSource` | Microsoft Defender ATP | Microsoft Defender for Endpoint | Rebranding |
| `ServiceSource` | Microsoft Threat Protection | Microsoft Defender XDR | Rebranding |
| `ServiceSource` | Office 365 ATP | Microsoft Defender for Office 365 | Rebranding |
| `ServiceSource` | Azure ATP | Microsoft Defender for Identity | Rebranding |

`DetectionSource` is available in the [AlertInfo](advanced-hunting-alertinfo-table) table. `ServiceSource` is available in the [AlertEvidence](advanced-hunting-alertevidence-table) and [AlertInfo](advanced-hunting-alertinfo-table) tables.

## December 2020

| Table name | Original column name | New column name | Reason for change |
| --- | --- | --- | --- |
| [EmailEvents](advanced-hunting-emailevents-table) | `FinalEmailAction` | `EmailAction` | Customer feedback |
| [EmailEvents](advanced-hunting-emailevents-table) | `FinalEmailActionPolicy` | `EmailActionPolicy` | Customer feedback |
| [EmailEvents](advanced-hunting-emailevents-table) | `FinalEmailActionPolicyGuid` | `EmailActionPolicyGuid` | Customer feedback |