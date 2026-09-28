---
layout: Conceptual
title: DeviceBaselineComplianceAssessmentKB table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-devicebaselinecomplianceassessmentkb-table
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about the various security configurations used by baseline compliance to assess devices in the DeviceBaselineComplianceAssessmentKB table in the advanced hunting schema.
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
document_id: 1d9c6198-4be3-11cf-cad7-103c09bdd0fe
document_version_independent_id: 1d9c6198-4be3-11cf-cad7-103c09bdd0fe
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-devicebaselinecomplianceassessmentkb-table.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-devicebaselinecomplianceassessmentkb-table
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-devicebaselinecomplianceassessmentkb-table.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 7007c945-cc07-ea20-a014-bceb41f75992
---

# DeviceBaselineComplianceAssessmentKB table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn

Important

Some information relates to prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

The `DeviceBaselineComplianceAssessmentKB` table in the advanced hunting schema contains information about various security configurations used by baseline compliance to assess devices.

This advanced hunting table is populated by records from Microsoft Defender for Endpoint. If your organization hasn't deployed the service in Microsoft Defender, queries that use the table aren't going to work or return any results. For more information about how to deploy Defender for Endpoint in the Defender portal, read [Deploy supported services](deploy-supported-services).

For information on other tables in the advanced hunting schema, see [the advanced hunting reference](advanced-hunting-schema-tables).

| Column name | Data type | Description |
| --- | --- | --- |
| `ConfigurationId` | `string` | Identifier for a configuration within a specific benchmark and benchmark version |
| `ConfigurationName` | `string` | Display name of the configuration |
| `ConfigurationDescription` | `string` | Description of the configuration |
| `ConfigurationRationale` | `string` | Description of any associated risks and rationale behind the configuration |
| `ConfigurationCategory` | `string` | Category or grouping to which the configuration belongs |
| `BenchmarkProfileLevels` | `dynamic` | List of benchmark compliance levels for which the configuration is applicable |
| `CCEReference` | `string` | Unique Common Configuration Enumeration (CCE) identifier for the configuration |
| `RemediationOptions` | `string` | Recommended actions to reduce or address any associated risks |
| `ConfigurationBenchmark` | `string` | Industry benchmark recommending the configuration |
| `ConfigurationBenchmarkVersion` | `string` | Version of the industry benchmark recommending the configuration |
| `Source` | `dynamic` | The registry path or other location used to determine the current device setting |
| `RecommendedValue` | `dynamic` | Set of expected values for the current device setting to be compliant |