---
layout: Conceptual
title: DeviceFromIP() function in advanced hunting for Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-devicefromip-function
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to use the DeviceFromIP() function to get the devices that have been assigned a specific IP address
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
document_id: a08a18c3-2886-746b-59df-80786b60d820
document_version_independent_id: a08a18c3-2886-746b-59df-80786b60d820
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-devicefromip-function.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-devicefromip-function
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-devicefromip-function.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 4e6c4b49-2d7f-098f-83e2-02b5d2a853e2
---

# DeviceFromIP() function in advanced hunting for Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

Use the `DeviceFromIP()` function in your [advanced hunting](advanced-hunting-overview) queries to quickly obtain the list of devices that have been assigned to a certain IP address at a given point in time.

This function returns a table with the following columns:

| Column | Data type | Description |
| --- | --- | --- |
| `IP` | `string` | IP address |
| `DeviceId` | `string` | Unique identifier for the device in the service |

## Syntax

```kusto
invoke DeviceFromIP()
```

## Arguments

This function is invoked as part of a query.

- **x**—The first parameter is typically already a column in the query. In this case, it's the column named `IP`, the IP address for which you want to see a list of devices that have been assigned to it. It should be a local IP address. External IP addresses aren't supported.
- **y**—A second optional parameter is the `Timestamp`, which instructs the function to obtain the most recent assigned devices from a specific time. If not specified, the function returns the latest available records.

## Example

### Get the latest devices that have been assigned specific IP addresses

```kusto
DeviceNetworkEvents 
| limit 100 
| project IP = LocalIP 
| invoke DeviceFromIP()
```