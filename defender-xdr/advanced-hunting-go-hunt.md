---
layout: Conceptual
title: Get relevant info about an entity with go hunt - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-go-hunt
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Use the go hunt action in Microsoft Defender XDR to automatically run advanced hunting queries for selected events and entities during investigations.
ms.service: defender-xdr
ms.subservice: adv-hunting
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.custom:
- msecd-doc-authoring-1014
- cx-ti
- cx-ah
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 60a04e77-59ce-9643-ca0d-d3082079513a
document_version_independent_id: 60a04e77-59ce-9643-ca0d-d3082079513a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-go-hunt.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-go-hunt
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-go-hunt.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: c0501ab6-dc33-0285-3598-a0bf0d6bfafb
---

# Get relevant info about an entity with go hunt - Microsoft Defender XDR | Microsoft Learn

With the *go hunt* action, you can quickly investigate events and various entity types using powerful query-based [advanced hunting](advanced-hunting-overview) capabilities. The *go hunt* action automatically runs an advanced hunting query to find relevant information about the selected event or entity.

The *go hunt* action is available in various sections of Microsoft Defender XDR. The *go hunt* action appears once event or entity details are displayed. For example, you can use the *go hunt* option from the following sections:

- In the [incident summary page](investigate-incidents#summary), you can review details about users, devices, and many other entities associated with an incident. As you select an entity, you get additional information and the various actions you could take on that entity. In the example below, a mailbox is selected, showing details about the mailbox and the option to hunt for more information about the mailbox.

    [![The Mailboxes page with the Go hunt option in the Microsoft Defender portal ](media/advanced-hunting-go-hunt/go-hunt-1-incident.png)](media/advanced-hunting-go-hunt/go-hunt-1-incident.png#lightbox)
- In the incident page, you can also access a list of entities under the **Evidence** tab. Selecting one of those entities provides an option to quickly hunt for information about that entity.

    [![The Go hunt option for a piece of evidence in the Incident page in Microsoft Defender portal](media/advanced-hunting-go-hunt/go-hunt-2-entity.png)](media/advanced-hunting-go-hunt/go-hunt-2-entity.png#lightbox)
- When viewing the timeline for a device, you can select an event in the timeline to view additional information about that event. Once an event is selected, you get the option to hunt for other relevant events in advanced hunting.

    [![The Hunt for related events option on an event's page in the Timelines tab in Microsoft Defender portal](media/advanced-hunting-go-hunt/go-hunt-3-event.png)](media/advanced-hunting-go-hunt/go-hunt-3-event.png#lightbox)

Selecting **Go hunt** or **Hunt for related events** passes different queries, depending on whether you've selected an entity or an event.

## Query for entity information

You can use *go hunt* to query for information about a user, device, or any other type of entity; the query checks all relevant schema tables for any events involving that entity to return information. To keep the results manageable, the query is:

- scoped to around the same time period as the earliest activity in the past 30 days that involves the entity
- associated with the incident that includes the entity.

Here is an example of the go hunt query for a device:

```kusto
let selectedTimestamp = datetime(2020-06-02T02:06:47.1167157Z);
let deviceName = "fv-az770.example.com";
let deviceId = "device-guid";
search in (DeviceLogonEvents, DeviceProcessEvents, DeviceNetworkEvents, DeviceFileEvents, DeviceRegistryEvents, DeviceImageLoadEvents, DeviceEvents, DeviceImageLoadEvents, IdentityLogonEvents, IdentityQueryEvents)
Timestamp between ((selectedTimestamp - 1h) .. (selectedTimestamp + 1h))
and DeviceName == deviceName
// or RemoteDeviceName == deviceName
// or DeviceId == deviceId
| take 100
```

### Supported entity types

You can use the *go hunt* option after selecting any of these entity types:

- Devices
- Email clusters
- Emails
- Files
- Groups
- IP addresses
- Mailboxes
- Users
- URLs

## Query for event information

When using *go hunt* to query for information about a timeline event, the query checks all relevant schema tables for other events around the time of the selected event. For example, the following query lists events in various schema tables that occurred around the same time period on the same device:

```kusto
// List relevant events 30 minutes before and after selected LogonAttempted event
let selectedEventTimestamp = datetime(2020-06-04T01:29:09.2496688Z);
search in (DeviceFileEvents, DeviceProcessEvents, DeviceEvents, DeviceRegistryEvents, DeviceNetworkEvents, DeviceImageLoadEvents, DeviceLogonEvents)
    Timestamp between ((selectedEventTimestamp - 30m) .. (selectedEventTimestamp + 30m))
    and DeviceId == "079ecf9c5798d249128817619606c1c47369eb3e"
| sort by Timestamp desc
| extend Relevance = iff(Timestamp == selectedEventTimestamp, "Selected event", iff(Timestamp < selectedEventTimestamp, "Earlier event", "Later event"))
| project-reorder Relevance
```

## Adjust the generated hunt query

With some knowledge of the [advanced hunting query language](advanced-hunting-query-language), you can adjust the query to your preference. For example, you can adjust the `Timestamp between` line, which determines the size of the time window:

```kusto
Timestamp between ((selectedTimestamp - 1h) .. (selectedTimestamp + 1h))
```

In addition to modifying the query to get more relevant results, you can also:

- [View the results as charts](advanced-hunting-query-results#view-query-results-as-a-table-or-chart)
- [Create a custom detection rule](custom-detection-rules)

Note

Some tables in this article might not be available in Microsoft Defender for Endpoint. [Turn on Microsoft Defender](m365d-enable) to hunt for threats using more data sources. You can move your advanced hunting workflows from Microsoft Defender for Endpoint to Microsoft Defender by following the steps in [Migrate advanced hunting queries from Microsoft Defender for Endpoint](advanced-hunting-migrate-from-mde).