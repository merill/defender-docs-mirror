---
layout: Conceptual
title: DeviceTvmSecureConfigurationAssessmentKB table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-devicetvmsecureconfigurationassessmentkb-table
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about the various secure configurations assessed by Microsoft Defender Vulnerability Management in the DeviceTvmSecureConfigurationAssessmentKB table of the advanced hunting schema.
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
document_id: a6cdc229-0d2f-4a63-9cbb-66490a7b30f7
document_version_independent_id: a6cdc229-0d2f-4a63-9cbb-66490a7b30f7
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-devicetvmsecureconfigurationassessmentkb-table.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-devicetvmsecureconfigurationassessmentkb-table
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-devicetvmsecureconfigurationassessmentkb-table.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 1857e231-d0fc-295e-ee8d-3839df9cdd90
---

# DeviceTvmSecureConfigurationAssessmentKB table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn

The `DeviceTvmSecureConfigurationAssessmentKB` table in the advanced hunting schema contains information about the various secure configurations checked by [Microsoft Defender Vulnerability Management](/en-us/windows/security/threat-protection/microsoft-defender-atp/next-gen-threat-and-vuln-mgt). It also includes risk information, related industry benchmarks, and applicable MITRE ATT&CK techniques and tactics.

This table doesn't return events or records. We recommend joining this table to the [DeviceTvmSecureConfigurationAssessment](advanced-hunting-devicetvmsecureconfigurationassessment-table) table using `ConfigurationId` to view text information about the security configurations in the returned assessments.

For example, when you query the `DeviceTvmSecureConfigurationAssessment` table you might want to view the `ConfigurationDescription` for the security configurations that come up in the assessment results. You can see this information by joining this table to `DeviceTvmSecureConfigurationAssessment` using `ConfigurationId` and project `ConfigurationDescription`.

For information on other tables in the advanced hunting schema, see [the advanced hunting reference](advanced-hunting-schema-tables).

Important

**This Defender Vulnerability Management (TVM) table isn't ingested into Microsoft Sentinel.** In Microsoft Sentinel, this table is exposed for schema visibility only (for example, autocomplete and query validation), not for data ingestion. As a result, Microsoft Sentinel can accept queries that reference this table, but those queries return no results.

To query this table’s data, run the query in Defender XDR Advanced Hunting, where the data is available. Using TVM table data directly in Microsoft Sentinel analytics and detections isn't currently supported unless you build a [custom ingestion path](/en-us/azure/sentinel/create-custom-connector). For more information, see [Which Defender XDR tables aren't supported in Microsoft Sentinel](/en-us/azure/sentinel/connect-microsoft-365-defender#which-defender-xdr-tables-arent-supported-in-microsoft-sentinel).

| Column name | Data type | Description |
| --- | --- | --- |
| `ConfigurationId` | `string` | Unique identifier for a specific configuration |
| `ConfigurationImpact` | `real` | Rated impact of the configuration to the overall configuration score (1-10) |
| `ConfigurationName` | `string` | Display name of the configuration |
| `ConfigurationDescription` | `string` | Description of the configuration |
| `RiskDescription` | `string` | Description of the associated risk |
| `ConfigurationCategory` | `string` | Category or grouping to which the configuration belongs: Application, OS, Network, Accounts, Security controls |
| `ConfigurationSubcategory` | `string` | Subcategory or subgrouping to which the configuration belongs. In many cases, this describes specific capabilities or features. |
| `ConfigurationBenchmarks` | `dynamic` | List of industry benchmarks recommending the same or similar configuration |
| `Tags` | `dynamic` | Labels representing various attributes used to identify or categorize a security configuration |
| `RemediationOptions` | `string` | Recommended actions to reduce or address any associated risks |

You can try this example query to return relevant configuration metadata along with information on devices with non-compliant antivirus configurations from the `DeviceTvmSecureConfigurationAssessment` table:

```kusto
// Get information on devices with antivirus configurations issues
DeviceTvmSecureConfigurationAssessment
| where ConfigurationSubcategory == 'Antivirus' and IsApplicable == 1 and IsCompliant == 0
| join kind=leftouter (
    DeviceTvmSecureConfigurationAssessmentKB
    | project ConfigurationId, ConfigurationName, ConfigurationDescription, RiskDescription, Tags, ConfigurationImpact
) on ConfigurationId
| project DeviceName, OSPlatform, ConfigurationId, ConfigurationName, ConfigurationCategory, ConfigurationSubcategory, ConfigurationDescription, RiskDescription, ConfigurationImpact, Tags
```