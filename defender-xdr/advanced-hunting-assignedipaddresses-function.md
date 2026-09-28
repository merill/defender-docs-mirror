---
layout: Conceptual
title: AssignedIPAddresses() function in advanced hunting for Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-assignedipaddresses-function
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to use the AssignedIPAddresses() function to get the latest IP addresses assigned to a device
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
document_id: 52a19d65-31cf-ec50-ed72-8d9802c79135
document_version_independent_id: 52a19d65-31cf-ec50-ed72-8d9802c79135
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-assignedipaddresses-function.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-assignedipaddresses-function
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-assignedipaddresses-function.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: f8457652-7fcf-198a-d89b-4a57b8cc9ac1
---

# AssignedIPAddresses() function in advanced hunting for Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn

Use the `AssignedIPAddresses()` function in your [advanced hunting](advanced-hunting-overview) queries to quickly obtain the latest IP addresses that have been assigned to a device. If you specify a timestamp argument, this function obtains the most recent IP addresses at the specified time.

This function returns a table with the following columns:

| Column | Data type | Description |
| --- | --- | --- |
| `Timestamp` | `datetime` | Latest time when the device was observed using the IP address |
| `IPAddress` | `string` | IP address used by the device |
| `IPType` | `string` | Indicates whether the IP address is a public or private address |
| `NetworkAdapterType` | `int` | Network adapter type used by the device that has been assigned the IP address. For the possible values, refer to [this enumeration](/en-us/dotnet/api/system.net.networkinformation.networkinterfacetype) |
| `ConnectedNetworks` | `int` | Networks that the adapter with the assigned IP address is connected to. Each JSON array contains the network name, category (public, private, or domain), a description, and a flag indicating if it's connected publicly to the internet |

## Syntax

```kusto
AssignedIPAddresses(x, y)
```

## Arguments

- **x**—`DeviceId` or `DeviceName` value identifying the device
- **y**—`Timestamp` (datetime) value instructing the function to obtain the most recent assigned IP addresses from a specific time. If not specified, the function returns the latest IP addresses.

## Examples

### Get the list of IP addresses used by a device 24 hours ago

```kusto
AssignedIPAddresses('example-device-name', ago(1d))
```

### Get IP addresses used by a device and find devices communicating with it

This query uses the `AssignedIPAddresses()` function to get assigned IP addresses for the device (`example-device-name`) on or before a specific date (`example-date`). It then uses the IP addresses to find connections to the device initiated by other devices.

```kusto
let Date = datetime(example-date);
let DeviceName = "example-device-name";
// List IP addresses used on or before the specified date
AssignedIPAddresses(DeviceName, Date)
| project DeviceName, IPAddress, AssignedTime = Timestamp 
// Get all network events on devices with the assigned IP addresses as the destination addresses
| join kind=inner DeviceNetworkEvents on $left.IPAddress == $right.RemoteIP
// Get only network events around the time the IP address was assigned
| where Timestamp between ((AssignedTime - 1h) .. (AssignedTime + 1h))
```