---
layout: Conceptual
title: DeviceBaselineComplianceProfiles table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-devicebaselinecomplianceprofiles-table
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about the baseline profiles used for monitoring device baseline compliance in the DeviceBaselineComplianceProfiles table in the advanced hunting schema.
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
document_id: f949dd4b-1663-8de2-e89f-f36a9d2c7344
document_version_independent_id: f949dd4b-1663-8de2-e89f-f36a9d2c7344
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-devicebaselinecomplianceprofiles-table.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-devicebaselinecomplianceprofiles-table
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-devicebaselinecomplianceprofiles-table.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 9443e8c0-f3e8-92e1-7a63-af6099634c6b
---

# DeviceBaselineComplianceProfiles table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn

Important

Some information relates to prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

The `DeviceBaselineComplianceProfiles` table in the advanced hunting schema contains baseline profiles used for monitoring device baseline compliance. Use this reference to construct queries that return information from the table.

This advanced hunting table is populated by records from Microsoft Defender for Endpoint. If your organization hasn't deployed the service in Microsoft Defender, queries that use the table aren't going to work or return any results. For more information about how to deploy Defender for Endpoint in the Defender portal, read [Deploy supported services](deploy-supported-services).

For information on other tables in the advanced hunting schema, see [the advanced hunting reference](advanced-hunting-schema-tables).

| Column name | Data type | Description |
| --- | --- | --- |
| `ProfileId` | `string` | Unique identifier for the profile |
| `ProfileName` | `string` | Display name of the profile |
| `ProfileDescription` | `string` | Optional description providing additional information related to the profile |
| `OSPlatform` | `dynamic` | Platform of the operating system running on the device. This indicates specific operating systems, including variations within the same family, such as Windows 11, Windows 10 and Windows 7. |
| `OSVersion` | `string` | Version of the operating system running on the device |
| `BaseBenchmark` | `string` | Industry benchmark on top of which the profile was created |
| `BenchmarkVersion` | `string` | Version of the industry benchmark on top of which the profile was created |
| `BenchmarkProfileLevel` | `string` | Benchmark compliance level set for the profile |
| `Status` | `boolean` | Indicator of the profile status - can be Enabled or Disabled |
| `CreatedBy` | `string` | Identity of the user account who created the profile |
| `CreatedOn` | `datetime` | Date and time when the profile was created |
| `LastUpdatedBy` | `string` | Identity of the user account who last updated the profile |
| `LastUpdatedOn` | `datetime` | Date and time when the profile was last updated |