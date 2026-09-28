---
layout: Conceptual
title: DeviceNetworkInfo table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-devicenetworkinfo-table
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about network configuration information in the DeviceNetworkInfo table of the advanced hunting schema
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
ms.date: 2025-04-03T00:00:00.0000000Z
locale: en-us
document_id: 162ee11d-7c51-16e0-a9db-bee306637d87
document_version_independent_id: 162ee11d-7c51-16e0-a9db-bee306637d87
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-devicenetworkinfo-table.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-devicenetworkinfo-table
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-devicenetworkinfo-table.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 3ae3c928-d076-7144-cd12-23745450883d
---

# DeviceNetworkInfo table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn

The `DeviceNetworkInfo` table in the [advanced hunting](advanced-hunting-overview) schema contains information about networking configuration of machines, including network adapters, IP and MAC addresses, and connected networks or domains. Use this reference to construct queries that return information from this table.

Important

Some information relates to prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

This advanced hunting table is populated by records from Microsoft Defender for Endpoint. If your organization hasn't deployed the service in Microsoft Defender, queries that use the table aren't going to work or return any results. For more information about how to deploy Defender for Endpoint in the Defender portal, read [Deploy supported services](deploy-supported-services).

For information on other tables in the advanced hunting schema, [see the advanced hunting reference](advanced-hunting-schema-tables).

| Column name | Data type | Description |
| --- | --- | --- |
| `Timestamp` | `datetime` | Date and time when the event was recorded |
| `DeviceId` | `string` | Unique identifier for the device in the service |
| `DeviceName` | `string` | Fully qualified domain name (FQDN) of the device |
| `NetworkAdapterName` | `string` | Name of the network adapter |
| `MacAddress` | `string` | MAC address of the network adapter |
| `NetworkAdapterType` | `string` | Network adapter type. For the possible values, refer to [this enumeration](/en-us/dotnet/api/system.net.networkinformation.networkinterfacetype). |
| `NetworkAdapterStatus` | `string` | Operational status of the network adapter. For the possible values, refer to [this enumeration](/en-us/dotnet/api/system.net.networkinformation.operationalstatus). |
| `TunnelType` | `string` | Tunneling protocol, if the interface is used for this purpose, for example 6to4, Teredo, ISATAP, PPTP, SSTP, and SSH |
| `ConnectedNetworks` | `string` | Networks that the adapter is connected to. Each JSON element in the array contains the network name, category (public, private or domain), a description, and a flag indicating if it's connected publicly to the internet. |
| `DnsAddresses` | `string` | DNS server addresses in JSON array format |
| `IPv4Dhcp` | `string` | IPv4 address of DHCP server |
| `IPv6Dhcp` | `string` | IPv6 address of DHCP server |
| `DefaultGateways` | `string` | Default gateway addresses in JSON array format |
| `IPAddresses` | `string` | JSON array containing all the IP addresses assigned to the adapter, along with their respective subnet prefix and IP address space, such as public, private, or link-local |
| `ReportId` | `long` | Event identifier based on a repeating counter. To identify unique events, this column must be used in conjunction with the DeviceName and Timestamp columns. |
| `NetworkAdapterVendor` | `string` | Name of the manufacturer or vendor of the network adapter |
| `OnboardingStatus` | `string` | Indicates whether the device is currently onboarded to Microsoft Defender for Endpoint or if the device is not supported |
| `NetworkAdapterDnsSuffix` | `string` | Domain suffix assigned to the device’s network adapter, indicating the network environment the network adapter is connected to |