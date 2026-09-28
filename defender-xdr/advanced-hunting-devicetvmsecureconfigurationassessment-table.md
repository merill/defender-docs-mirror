---
layout: Conceptual
title: DeviceTvmSecureConfigurationAssessment table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-devicetvmsecureconfigurationassessment-table
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about security assessment events in the DeviceTvmSecureConfigurationAssessment table of the advanced hunting schema. These events provide device information, security configuration details, impact, and compliance information.
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
document_id: ee0c8195-39b0-88c6-a512-256915de4d59
document_version_independent_id: ee0c8195-39b0-88c6-a512-256915de4d59
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-devicetvmsecureconfigurationassessment-table.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-devicetvmsecureconfigurationassessment-table
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-devicetvmsecureconfigurationassessment-table.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: c68fe375-e149-7bc4-04a5-c27afd98bdab
---

# DeviceTvmSecureConfigurationAssessment table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn

Each row in the `DeviceTvmSecureConfigurationAssessment` table contains an assessment event for a specific security configuration from [Microsoft Defender Vulnerability Management](/en-us/windows/security/threat-protection/microsoft-defender-atp/next-gen-threat-and-vuln-mgt). Use this reference to check the latest assessment results and determine whether devices are compliant.

You can join this table with the [DeviceTvmSecureConfigurationAssessmentKB](advanced-hunting-devicetvmsecureconfigurationassessmentkb-table) table using `ConfigurationId` so you can, for example, view the text description of the configuration from the `ConfigurationDescription` column of the `DeviceTvmSecureConfigurationAssessmentKB` table, in the configuration assessment results.

This advanced hunting table is populated by records from Microsoft Defender for Endpoint. If your organization hasn't deployed the service in Microsoft Defender, queries that use the table aren't going to work or return any results. For more information about how to deploy Defender for Endpoint in the Defender portal, read [Deploy supported services](deploy-supported-services).

For information on other tables in the advanced hunting schema, see [the advanced hunting reference](advanced-hunting-schema-tables).

Important

**This Defender Vulnerability Management (TVM) table isn't ingested into Microsoft Sentinel.** In Microsoft Sentinel, this table is exposed for schema visibility only (for example, autocomplete and query validation), not for data ingestion. As a result, Microsoft Sentinel can accept queries that reference this table, but those queries return no results.

To query this table’s data, run the query in Defender XDR Advanced Hunting, where the data is available. Using TVM table data directly in Microsoft Sentinel analytics and detections isn't currently supported unless you build a [custom ingestion path](/en-us/azure/sentinel/create-custom-connector). For more information, see [Which Defender XDR tables aren't supported in Microsoft Sentinel](/en-us/azure/sentinel/connect-microsoft-365-defender#which-defender-xdr-tables-arent-supported-in-microsoft-sentinel).

| Column name | Data type | Description |
| --- | --- | --- |
| `DeviceId` | `string` | Unique identifier for the device in the service |
| `DeviceName` | `string` | Fully qualified domain name (FQDN) of the device |
| `OSPlatform` | `string` | Platform of the operating system running on the device. Indicates specific operating systems, including variations within the same family, such as Windows 11, Windows 10, and Windows 7. |
| `Timestamp` | `datetime` | Date and time when the record was generated |
| `ConfigurationId` | `string` | Unique identifier for a specific configuration |
| `ConfigurationCategory` | `string` | Category or grouping to which the configuration belongs: Application, OS, Network, Accounts, Security controls |
| `ConfigurationSubcategory` | `string` | Subcategory or subgrouping to which the configuration belongs. In many cases, string describes specific capabilities or features. |
| `ConfigurationImpact` | `real` | Rated impact of the configuration to the overall configuration score (1-10) |
| `IsCompliant` | `boolean` | Indicates whether the configuration or policy is properly configured  \* A value of True is Compliant \* A value of False is Not Compliant |
| `IsApplicable` | `boolean` | Indicates whether the configuration or policy applies to the device  \* A value of True is Applicable \* A value of False is Not Applicable |
| `Context` | `dynamic` | Additional contextual information about the configuration or policy |
| `IsExpectedUserImpact` | `boolean` | Indicates whether there will be user impact if the configuration or policy is applied |

You can try this example query to return information on devices with non-compliant antivirus configurations along with the relevant configuration metadata from the `DeviceTvmSecureConfigurationAssessmentKB` table:

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