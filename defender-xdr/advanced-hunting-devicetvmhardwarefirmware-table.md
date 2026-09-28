---
layout: Conceptual
title: DeviceTvmHardwareFirmware table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-devicetvmhardwarefirmware-table
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about the DeviceTvmHardwareFirmware table in the advanced hunting schema, which includes information on devices like processor, BIOS, and others, as checked in threat and vulnerability management in Microsoft Defender.
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
ms.date: 2026-06-14T00:00:00.0000000Z
locale: en-us
document_id: 8eff15cd-450b-617c-7c38-c4aa90e4e3b8
document_version_independent_id: 8eff15cd-450b-617c-7c38-c4aa90e4e3b8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-devicetvmhardwarefirmware-table.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-devicetvmhardwarefirmware-table
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-devicetvmhardwarefirmware-table.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 8e0ab790-5453-d613-9eae-1ed3ed6d1c6b
---

# DeviceTvmHardwareFirmware table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn

Important

Some information relates to prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

The `DeviceTvmHardwareFirmware` table in the advanced hunting schema contains hardware and firmware information of devices as checked by [Microsoft Defender Vulnerability Management](/en-us/windows/security/threat-protection/microsoft-defender-atp/next-gen-threat-and-vuln-mgt). The information includes the system model, processor, and BIOS, among others.

This advanced hunting table is populated by records from Microsoft Defender for Endpoint. If your organization hasn't deployed the service in Microsoft Defender, queries that use the table aren't going to work or return any results. For more information about how to deploy Defender for Endpoint in the Defender portal, read [Deploy supported services](deploy-supported-services).

For information on other tables in the advanced hunting schema, see [the advanced hunting reference](advanced-hunting-schema-tables).

Important

**This Defender Vulnerability Management (TVM) table isn't ingested into Microsoft Sentinel.** In Microsoft Sentinel, this table is exposed for schema visibility only (for example, autocomplete and query validation), not for data ingestion. As a result, Microsoft Sentinel can accept queries that reference this table, but those queries return no results.

To query this table’s data, run the query in Defender XDR Advanced Hunting, where the data is available. Using TVM table data directly in Microsoft Sentinel analytics and detections isn't currently supported unless you build a [custom ingestion path](/en-us/azure/sentinel/create-custom-connector). For more information, see [Which Defender XDR tables aren't supported in Microsoft Sentinel](/en-us/azure/sentinel/connect-microsoft-365-defender#which-defender-xdr-tables-arent-supported-in-microsoft-sentinel).

| Column name | Data type | Description |
| --- | --- | --- |
| `DeviceId` | `string` | Unique identifier for the device in the service |
| `DeviceName` | `string` | Fully qualified domain name (FQDN) of the device |
| `ComponentType` | `string` | Type of hardware or firmware component |
| `Manufacturer` | `string` | Manufacturer of hardware or firmware component |
| `ComponentName` | `string` | Name of hardware or firmware component |
| `ComponentFamily` | `string` | Component family or class, a grouping of components that have similar features or characteristics as determined by the manufacturer |
| `ComponentVersion` | `string` | Component version (for example, BIOS version) |
| `AdditionalFields` | `dynamic` | Additional information about the components in JSON array format |

You can try the following sample queries to use the information available in the `DeviceTvmHardwareFirmware` table:

```kusto
// Count the number of Lenovo devices
DeviceTvmHardwareFirmware
| where ComponentType == "Hardware" and Manufacturer == "lenovo"
| summarize count()
```

```kusto
// Find all devices with a specific BIOS version, replace ComponentVersion with what you are looking for
DeviceTvmHardwareFirmware
| where ComponentType == "Bios" and ComponentVersion contains "N2VET29W"
|project DeviceId, DeviceName
```