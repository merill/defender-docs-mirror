---
layout: Conceptual
title: IdentityDirectoryEvents table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-identitydirectoryevents-table
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about domain controller and Active Directory events in the IdentityDirectoryEvents table of the advanced hunting schema
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
document_id: 1cb48f85-f08d-2cd1-5ada-0a08d04e15ec
document_version_independent_id: 1cb48f85-f08d-2cd1-5ada-0a08d04e15ec
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-identitydirectoryevents-table.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-identitydirectoryevents-table
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-identitydirectoryevents-table.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 0d0f6591-1708-756e-0bf3-36b8d8d001fb
---

# IdentityDirectoryEvents table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn

The `IdentityDirectoryEvents` table in the [advanced hunting](advanced-hunting-overview) schema contains events involving an on-premises domain controller running Active Directory (AD). This table captures various identity-related events, like password changes, password expiration, and user principal name (UPN) changes. It also captures system events on the domain controller, like scheduling of tasks and PowerShell activity. Use this reference to construct queries that return information from this table.

This advanced hunting table is populated by records from Microsoft Defender for Identity. If your organization hasn't deployed the service in Microsoft Defender, queries that use the table aren't going to work or return any results. For more information about how to deploy Defender for Identity in the Defender portal, read [Deploy supported services](deploy-supported-services).

Tip

For detailed information about the events types (`ActionType` values) supported by a table, use the built-in schema reference available in the Defender portal.

For information on other tables in the advanced hunting schema, [see the advanced hunting reference](advanced-hunting-schema-tables).

| Column name | Data type | Description |
| --- | --- | --- |
| `Timestamp` | `datetime` | Date and time when the event was recorded |
| `ActionType` | `string` | Type of activity that triggered the event. See the [in-portal schema reference](advanced-hunting-schema-tables?#get-schema-information-in-the-security-center) for details |
| `Application` | `string` | Application that performed the recorded action |
| `TargetAccountUpn` | `string` | User principal name (UPN) of the account that the recorded action was applied to |
| `TargetAccountDisplayName` | `string` | Display name of the account that the recorded action was applied to |
| `TargetDeviceName` | `string` | Fully qualified domain name (FQDN) of the device that the recorded action was applied to |
| `DestinationDeviceName` | `string` | Name of the device running the server application that processed the recorded action |
| `DestinationIPAddress` | `string` | IP address of the device running the server application that processed the recorded action |
| `DestinationPort` | `int` | Destination port of the activity |
| `Protocol` | `string` | Protocol used during the communication |
| `AccountName` | `string` | User name of the account |
| `AccountDomain` | `string` | Domain of the account |
| `AccountUpn` | `string` | User principal name (UPN) of the account |
| `AccountSid` | `string` | Security Identifier (SID) of the account |
| `AccountObjectId` | `string` | Unique identifier for the account in Microsoft Entra ID |
| `AccountDisplayName` | `string` | Name of the account user displayed in the address book. Typically a combination of a given or first name, a middle initial, and a last name or surname. |
| `DeviceName` | `string` | Fully qualified domain name (FQDN) of the device |
| `IPAddress` | `string` | IP address assigned to the device during communication |
| `Port` | `int` | TCP port used during communication |
| `Location` | `string` | City, country/region, or other geographic location associated with the event |
| `ISP` | `string` | Internet service provider associated with the IP address |
| `ReportId` | `string` | Unique identifier for the event |
| `AdditionalFields` | `dynamic` | Additional information about the entity or event |