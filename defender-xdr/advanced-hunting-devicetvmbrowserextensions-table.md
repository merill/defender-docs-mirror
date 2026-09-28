---
layout: Conceptual
title: DeviceTvmBrowserExtensions table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-devicetvmbrowserextensions-table
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about browser extension installations found on devices as shown in Microsoft Defender Vulnerability Management.
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
document_id: ece000ca-a928-d1f0-2d22-0bbf57304e57
document_version_independent_id: ece000ca-a928-d1f0-2d22-0bbf57304e57
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-devicetvmbrowserextensions-table.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-devicetvmbrowserextensions-table
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-devicetvmbrowserextensions-table.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: fbec952a-7aac-ac58-909f-19b03abd73db
---

# DeviceTvmBrowserExtensions table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn

Important

Some information relates to prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

Each row in the `DeviceTvmBrowserExtensions` table contains information about browser extension installations found on devices from [Microsoft Defender Vulnerability Management](/en-us/windows/security/threat-protection/microsoft-defender-atp/next-gen-threat-and-vuln-mgt).

This advanced hunting table is populated by records from Microsoft Defender for Endpoint. If your organization hasn't deployed the service in Microsoft Defender, queries that use the table aren't going to work or return any results. For more information about how to deploy Defender for Endpoint in the Defender portal, read [Deploy supported services](deploy-supported-services).

For information on other tables in the advanced hunting schema, see [the advanced hunting reference](advanced-hunting-schema-tables).

Important

**This Defender Vulnerability Management (TVM) table isn't ingested into Microsoft Sentinel.** In Microsoft Sentinel, this table is exposed for schema visibility only (for example, autocomplete and query validation), not for data ingestion. As a result, Microsoft Sentinel can accept queries that reference this table, but those queries return no results.

To query this table’s data, run the query in Defender XDR Advanced Hunting, where the data is available. Using TVM table data directly in Microsoft Sentinel analytics and detections isn't currently supported unless you build a [custom ingestion path](/en-us/azure/sentinel/create-custom-connector). For more information, see [Which Defender XDR tables aren't supported in Microsoft Sentinel](/en-us/azure/sentinel/connect-microsoft-365-defender#which-defender-xdr-tables-arent-supported-in-microsoft-sentinel).

| Column name | Data type | Description |
| --- | --- | --- |
| `DeviceId` | `string` | Unique identifier for the device in the service |
| `BrowserName` | `string` | Name of the web browser with the extension |
| `ExtensionId` | `string` | Unique identifier for the browser extension |
| `ExtensionName` | `string` | Name of the extension |
| `ExtensionDescription` | `string` | Description from the publisher about the extension |
| `ExtensionVersion` | `string` | Version number of the extension |
| `ExtensionRisk` | `string` | Risk level for the extension based on the permissions it has requested |
| `ExtensionVendor` | `string` | Name of the vendor offering the extension |
| `IsActivated` | `string` | Whether the extension is turned on or off on the devices |
| `InstallationTime` | `datetime` | Date and time when the browser extension was first installed |