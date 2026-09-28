---
layout: Conceptual
title: DeviceNetworkEvents table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-devicenetworkevents-table
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about network connection events you can query from the DeviceNetworkEvents table of the advanced hunting schema
ms.service: defender-xdr
ms.pagetype: security
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
document_id: 43789567-3146-b28f-d8c5-1eb718827287
document_version_independent_id: 43789567-3146-b28f-d8c5-1eb718827287
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-devicenetworkevents-table.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-devicenetworkevents-table
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-devicenetworkevents-table.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: f66042d4-d643-912a-1ba0-4f9da3147f43
---

# DeviceNetworkEvents table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn

The `DeviceNetworkEvents` table in the [advanced hunting](advanced-hunting-overview) schema contains information about network connections and related events. Use this reference to construct queries that return information from this table.

Tip

For detailed information about the events types (`ActionType` values) supported by a table, use the built-in schema reference available in the Defender portal.

This advanced hunting table is populated by records from Microsoft Defender for Endpoint. If your organization hasn't deployed the service in Microsoft Defender, queries that use the table aren't going to work or return any results. For more information about how to deploy Defender for Endpoint in the Defender portal, read [Deploy supported services](deploy-supported-services).

For information on other tables in the advanced hunting schema, [see the advanced hunting reference](advanced-hunting-schema-tables).

| Column name | Data type | Description |
| --- | --- | --- |
| `Timestamp` | `datetime` | Date and time when the event was recorded |
| `DeviceId` | `string` | Unique identifier for the device in the service |
| `DeviceName` | `string` | Fully qualified domain name (FQDN) of the device |
| `ActionType` | `string` | Type of activity that triggered the event. See the [in-portal schema reference](advanced-hunting-schema-tables?#get-schema-information-in-the-security-center) for details. |
| `RemoteIP` | `string` | IP address that was being connected to |
| `RemotePort` | `int` | TCP port on the remote device that was being connected to |
| `RemoteUrl` | `string` | URL or fully qualified domain name (FQDN) that was being connected to |
| `LocalIP` | `string` | Source IP, or the IP address where the communication came from |
| `LocalPort` | `int` | TCP port on the local device used during communication |
| `Protocol` | `string` | Protocol used during the communication |
| `LocalIPType` | `string` | Type of IP address, for example Public, Private, Reserved, Loopback, Teredo, FourToSixMapping, and Broadcast |
| `RemoteIPType` | `string` | Type of IP address, for example Public, Private, Reserved, Loopback, Teredo, FourToSixMapping, and Broadcast |
| `InitiatingProcessSHA1` | `string` | SHA-1 of the process (image file) that initiated the event |
| `InitiatingProcessSHA256` | `string` | SHA-256 of the process (image file) that initiated the event. This field is usually not populated — use the SHA1 column when available. |
| `InitiatingProcessMD5` | `string` | MD5 hash of the process (image file) that initiated the event |
| `InitiatingProcessFileName` | `string` | Name of the process file that initiated the event; if unavailable, the name of the process that initiated the event might be shown instead |
| `InitiatingProcessFileSize` | `long` | Size of the file that ran the process responsible for the event |
| `InitiatingProcessVersionInfoCompanyName` | `string` | Company name from the version information of the process (image file) responsible for the event |
| `InitiatingProcessVersionInfoProductName` | `string` | Product name from the version information of the process (image file) responsible for the event |
| `InitiatingProcessVersionInfoProductVersion` | `string` | Product version from the version information of the process (image file) responsible for the event |
| `InitiatingProcessVersionInfoInternalFileName` | `string` | Internal file name from the version information of the process (image file) responsible for the event |
| `InitiatingProcessVersionInfoOriginalFileName` | `string` | Original file name from the version information of the process (image file) responsible for the event |
| `InitiatingProcessVersionInfoFileDescription` | `string` | Description from the version information of the process (image file) responsible for the event |
| `InitiatingProcessId` | `long` | Process ID (PID) of the process that initiated the event |
| `InitiatingProcessCommandLine` | `string` | Command line used to run the process that initiated the event |
| `InitiatingProcessCreationTime` | `datetime` | Date and time when the process that initiated the event was started |
| `InitiatingProcessFolderPath` | `string` | Folder containing the process (image file) that initiated the event |
| `InitiatingProcessParentFileName` | `string` | Name of the parent process that spawned the process responsible for the event |
| `InitiatingProcessParentId` | `long` | Process ID (PID) of the parent process that spawned the process responsible for the event |
| `InitiatingProcessParentCreationTime` | `datetime` | Date and time when the parent of the process responsible for the event was started |
| `InitiatingProcessAccountDomain` | `string` | Domain of the account that ran the process responsible for the event |
| `InitiatingProcessAccountName` | `string` | User name of the account that ran the process responsible for the event; if the device is registered in Microsoft Entra ID, the Entra ID user name of the account that ran the process responsible for the event might be shown instead |
| `InitiatingProcessAccountSid` | `string` | Security Identifier (SID) of the account that ran the process responsible for the event |
| `InitiatingProcessAccountUpn` | `string` | User principal name (UPN) of the account that ran the process responsible for the event; if the device is registered in Microsoft Entra ID, the Entra ID UPN of the account that ran the process responsible for the event might be shown instead |
| `InitiatingProcessAccountObjectId` | `string` | Microsoft Entra object ID of the user account that ran the process responsible for the event |
| `InitiatingProcessIntegrityLevel` | `string` | Integrity level of the process that initiated the event. Windows assigns integrity levels to processes based on certain characteristics, such as if they were launched from an internet download. These integrity levels influence permissions to resources. |
| `InitiatingProcessTokenElevation` | `string` | Token type indicating the presence or absence of User Access Control (UAC) privilege elevation applied to the process that initiated the event |
| `ReportId` | `long` | Event identifier based on a repeating counter. To identify unique events, this column must be used in conjunction with the DeviceName and Timestamp columns. |
| `AppGuardContainerId` | `string` | Identifier for the virtualized container used by Application Guard to isolate browser activity |
| `AdditionalFields` | `string` | Additional information about the event in JSON array format |
| `InitiatingProcessSessionId` | `long` | Windows session ID of the initiating process |
| `IsInitiatingProcessRemoteSession` | `bool` | Indicates whether the initiating process was run under a remote desktop protocol (RDP) session (true) or locally (false) |
| `InitiatingProcessRemoteSessionDeviceName` | `string` | Device name of the remote device from which the initiating process's RDP session was initiated |
| `InitiatingProcessRemoteSessionIP` | `string` | IP address of the remote device from which the initiating process's RDP session was initiated |
| `InitiatingProcessUniqueId` | `string` | Unique identifier of the initiating process; this is equal to the Process Start Key in Windows devices |
| `LogonID` | `long` | A unique identifier for the user initiating the event, enabling attribution of network activity to the originating interactive user across privilege escalation and session transitions. This field is located inside AdditionalFields/InitiatingProcessPosixEffectiveUser |