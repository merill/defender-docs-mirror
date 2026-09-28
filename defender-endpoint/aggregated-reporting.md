---
layout: Conceptual
title: Aggregated reporting in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/aggregated-reporting
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how you collect important telemetry in Microsoft Defender for Endpoint by turning on aggregated reporting.
ms.service: defender-endpoint
ms.author: chrisda
author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.topic: article
ms.date: 2025-10-20T00:00:00.0000000Z
locale: en-us
document_id: 118910ce-fbfb-6db9-4864-bc844759810a
document_version_independent_id: 118910ce-fbfb-6db9-4864-bc844759810a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/aggregated-reporting.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: aggregated-reporting
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/aggregated-reporting.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
platformId: f98f50c4-8b66-fd7f-b59f-8f9189f493ec
---

# Aggregated reporting in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Aggregated reporting addresses constraints on event reporting in Microsoft Defender for Endpoint. Aggregated reporting extends signal reporting intervals to significantly reduce the size of reported events while preserving essential event properties.

Defender for Endpoint reduces noise in collected data to improve the signal-to-noise ratio while balancing product performance and efficiency. It limits data collection to maintain this balance.

With aggregated reporting, Defender for Endpoint ensures that all essential event properties valuable to investigation and threat hunting activities are continuously collected. It does this by extended reporting intervals of one hour, which reduces the size of reported events and enables efficient yet valuable data collection.

When aggregated reporting is turned on, you can query for a summary of all supported event types, including low-efficacy telemetry, that you can use for investigation and hunting activities.

## Prerequisites

The following requirements must be met before turning on aggregated reporting:

- Permissions to enable advanced features

### Supported operating systems:

- Windows 10 (20H2, 21H1, 21H2)
- Windows 11 (22H2, Enterprise)
- Windows Server 2019 and later
- Windows Server version 20H2 or Azure Stack HCI OS, version 23H2 and later
- Client version: Windows version 24H and later

## Turn on aggregated reporting

To turn aggregated reporting on, go to **Settings &gt; Endpoints &gt; Advanced features**. Toggle on the **Aggregated reporting** feature.

![Screenshot of the aggregated reporting toggle in the Microsoft Defender portal settings page.](media/reports/aggregated-reporting/aggregated-reporting-toggle.png)

Once aggregated reporting is turned on, it can take up to seven days for aggregated reports to become available. You can then begin to query new data after the feature is turned on.

When you turn off aggregated reporting, the changes take a few hours to be applied. All previously collected data remains.

## Query aggregated reports

Aggregated reporting supports the following event types:

| Action type | Advanced hunting table | Device timeline presentation | Properties |
| --- | --- | --- | --- |
| FileCreatedAggregatedReport | DeviceFileEvents | {ProcessName} created {Occurrences} {FilePath} files | 1. File path  2. File extension  3. Process name |
| FileRenamedAggregatedReport | DeviceFileEvents | {ProcessName} renamed {Occurrences} {FilePath} files | 1. File path  2. File extension  3. Process name |
| FileModifiedAggregatedReport | DeviceFileEvents | {ProcessName} modified {Occurrences} {FilePath} files | 1. File path  2. File extension  3. Process name |
| ProcessCreatedAggregatedReport | DeviceProcessEvents | {InitiatingProcessName} created {Occurrences} {ProcessName} processes | 1. Initiating process command line  2. Initiating process SHA1  3. Initiating process file path  4. Process command line  5. Process SHA1  6. Folder path |
| ConnectionSuccessAggregatedReport | DeviceNetworkEvents | {InitiatingProcessName} established {Occurrences} connections with {RemoteIP}:{RemotePort} | 1. Initiating process name  2. Source IP  3. Remote IP  4. Remote port |
| ConnectionFailedAggregatedReport | DeviceNetworkEvents | {InitiatingProcessName} failed to establish {Occurrences} connections with {RemoteIP:RemotePort} | 1. Initiating process name  2. Source IP  3. Remote IP  4. Remote port |
| LogonSuccessAggregatedReport | DeviceLogonEvents | {Occurrences} {LogonType} logons by {UserName}\{DomainName} | 1. Target username  2. Target user SID  3. Target domain name  4. Logon type |
| LogonFailedAggregatedReport | DeviceLogonEvents | {Occurrences}{LogonType} logons failed by {UserName}\{DomainName} | 1. Target username  2. Target user SID  3. Target domain name  4. Logon type |

Note

Turning on aggregated reporting improves signal visibility, which might incur higher storage costs if you are streaming Defender for Endpoint advanced hunting tables to your SIEM or storage solutions.

To query new data with aggregated reports:

1. Go to **Investigation & response &gt; Hunting &gt; Custom detection rules**.
2. Review and modify [existing rules and queries](/en-us/defender-xdr/custom-detection-rules) that might be affected by aggregated reporting.
3. When necessary, create new custom rules to incorporate new action types.
4. Go to the **Advanced Hunting** page and query the new data.

    Here is an example of advanced hunting query results with aggregated reports.

    [![Screenshot of advanced hunting query results with aggregated reports.](media/reports/aggregated-reporting/sample-results-aggregated-reports-small.png)](media/reports/aggregated-reporting/sample-results-aggregated-reports.png#lightbox)

## Sample advanced hunting queries

You can use the following KQL queries to gather specific information using aggregated reporting.

### Query for noisy process activity

The following query highlights noisy process activity, which can be correlated with malicious signals.

```Kusto
DeviceProcessEvents
| where Timestamp > ago(1h)
| where ActionType == "ProcessCreatedAggregatedReport"
| extend uniqueEventsAggregated = toint(todynamic(AdditionalFields).uniqueEventsAggregated)
| project-reorder Timestamp, uniqueEventsAggregated, ProcessCommandLine, InitiatingProcessCommandLine, ActionType, SHA1, FolderPath, InitiatingProcessFolderPath, DeviceName
| sort by uniqueEventsAggregated desc
```

### Query for repeated sign in attempt failures

The following query identifies repeated sign-in attempt failures.

```Kusto
DeviceLogonEvents
| where Timestamp > ago(30d)
| where ActionType == "LogonFailedAggregatedReport"
| extend uniqueEventsAggregated = toint(todynamic(AdditionalFields).uniqueEventsAggregated)
| where uniqueEventsAggregated > 10
| project-reorder Timestamp, DeviceId, uniqueEventsAggregated, LogonType, AccountName, AccountDomain, AccountSid
| sort by uniqueEventsAggregated desc
```

### Query for suspicious RDP connections

The following query identifies suspicious RDP connections, which might indicate malicious activity.

```Kusto
DeviceNetworkEvents
| where Timestamp > ago(1d)
| where ActionType endswith "AggregatedReport"
| where RemotePort == "3389"
| extend uniqueEventsAggregated = toint(todynamic(AdditionalFields).uniqueEventsAggregated)
| where uniqueEventsAggregated > 10
| project-reorder ActionType, Timestamp, uniqueEventsAggregated 
| sort by uniqueEventsAggregated desc
```