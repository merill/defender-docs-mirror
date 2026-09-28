---
layout: Conceptual
title: Getting value from your data connectors in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/value-data-connectors
author: dlanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Learn about using the data connectors in Microsoft Security Exposure Management.
ms.topic: overview
ms.date: 2025-09-21T00:00:00.0000000Z
locale: en-us
document_id: 1c536965-3f6b-d1b3-6e2c-f517913e9402
document_version_independent_id: 1c536965-3f6b-d1b3-6e2c-f517913e9402
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/value-data-connectors.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: value-data-connectors
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/value-data-connectors.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
platformId: 9a768a58-f490-7e6e-9929-d4b6b53c3e77
---

# Getting value from your data connectors in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn

[Microsoft Security Exposure Management](microsoft-security-exposure-management) consolidates security posture data from all your digital assets enabling you to map your attack surface and focus your security efforts on areas at greatest risk. The data from Microsoft products gets ingested automatically once connected to Exposure Management, and you can add more data connectors from external data sources.

## Imported assets and data types

The intent of connecting to external products is to create complete visibility across all your digital assets and any security context that could impact your attack surface.

Note

At this time, devices are onboarded into the unified inventory only when they include sufficient identifying attributes (such as, MAC address, cloud resource identifiers, or other supported unique identifiers). If this information is not present or is incomplete, the system may not be able to confidently match or represent those assets in the Device Inventory page.

In such cases, assets may still be visible in Advanced Hunting. This is a **known** **limitation** of the current onboarding and normalization process, and we are actively working on enhancing data coverage and improve how these assets are represented across experiences.

The following asset types, context enrichment, and vulnerability information are ingested for this purpose:

- Devices
- Cloud assets
- Vulnerabilities
- Asset Criticality information
- Asset risk assessment
- Network details
- Exposure insights (for example, Internet exposure)
- Users (future)
- SaaS apps (future)

The asset information and security context are imported into Exposure Management and consolidated to provide a comprehensive view of the security posture across all digital assets. Currently supported external data sources include Qualys, Rapid7 InsightVM, Tenable Vulnerability Management, and ServiceNow CMDB.

Data ingested from the connectors gets normalized and incorporated into the Exposure Graph and Device Inventory. Exposure Management uses the valuable context and insights gained to generate a more accurate assessment of your attack surface, and provide you with a deeper understanding of your exposure risk. This data can be consumed in the Device Inventory, in Exposure Graph exploration tools like the Attack Surface Map and Advanced Hunting, and within Attack Paths that are discovered based on enrichment data ingested by the connectors.

Eventually this data will additionally serve to enhance security metrics that measure your exposure risk against a particular criteria, and it will also impact broader organizational initiatives that measure exposure risk across a workload or related to a specific threat area.

[![Screenshot of device inventory with discovery source](media/value-data-connectors/device inventory with 3p.png)](media/value-data-connectors/device%20inventory%20with%203p.png#lightbox)

Benefits of using the external data connectors include:

- Normalized within exposure graph
- Enhancing device inventory
- Mapping relationships
- Revealing new attack paths
- Providing comprehensive attack surface visibility
- Incorporating asset criticality
- Enriching context with business application or operational affiliation
- Visualizing through the Attack Map tool
- Exploring using advanced hunting queries via KQL

Note

Currently vulnerabilities retrieved from data connectors only appear in the Exposure Graph, and can be explored in the Attack Surface Map or using Advanced Hunting.

### Connectors data in the Device Inventory

In the Device Inventory, you'll see the discovery sources for each device, which are the products from which we got any report on this device. These might include Microsoft Security products like MDE, MDC, and MDI, and also external data sources like Qualys or ServiceNow CMDB. You can filter on one or more discovery sources within the inventory to view devices that were discovered specifically by those sources.

[![Screenshot of device inventory with discovery source highlighted](media/value-data-connectors/di data connectors.png)](media/value-data-connectors/di%20data%20connectors.png#lightbox)

### Critical Asset Management

Identifying critical assets is key in helping ensure that the most important assets in your organization are protected against risk of data breaches and operational disruptions.

Enrichment information on criticality of assets is retrieved from the data connectors, based on the criticality assessments calculated in those external products. As this data is ingested, Critical Asset Management contains built-in rules to transform the criticality value retrieved from the third-party product to the Exposure Management criticality value for each asset. You can view these classifications and enable or disable them in the Critical Asset Management experience.

[![Screenshot of data connector info in critical asset management](media/value-data-connectors/critical asset management data connectors.png)](media/value-data-connectors/critical%20asset%20management%20data%20connectors.png#lightbox)

### Exposure graph

To explore your assets and enrichment data retrieved from external data products, you can also view this information in the Exposure Graph. Within the Attack Surface map, you can view the nodes representing assets discovered by your connectors, with built-in icons showing the discovery sources for each asset.

[![Screenshot of data connectors in exposure graph shown](media/value-data-connectors/exposure graph data connectors main.png)](media/value-data-connectors/exposure%20graph%20data%20connectors%20main.png#lightbox)

By opening the side pane for the asset, you can also view the detailed data retrieved from the connector for each asset.

[![Screenshot of data connectors in exposure graph](media/value-data-connectors/exposure graph data connectors.png)](media/value-data-connectors/exposure%20graph%20data%20connectors.png#lightbox)

[![Screenshot of data connectors in exposure graph side pane](media/value-data-connectors/exposure graph data connectors all data.png)](media/value-data-connectors/exposure%20graph%20data%20connectors%20all%20data.png#lightbox)

### Advanced Hunting

To explore your discovered and ingested data from the external data sources, you can [run queries](query-enterprise-exposure-graph) on the Exposure Graph in Advanced Hunting.

**Examples**:

This query will return all assets retrieved from ServiceNow CMDB and their detailed metadata.

```kusto
ExposureGraphNodes
| where NodeProperties contains ("serviceNowCmdbAssetInfo")
| extend SnowInfo = NodeProperties.rawData.serviceNowCmdbAssetInfo
```

This query will return all assets retrieved from Qualys.

```kusto
ExposureGraphNodes
| where EntityIds contains ("QualysAssetId")
```

This query will return all vulnerabilities (CVEs) reported by Rapid7 on ingested assets.

```kusto
ExposureGraphEdges
| where EdgeLabel == "affecting" 
| where SourceNodeLabel == "Cve" 
| where isnotempty(EdgeProperties.rawData.rapid7ReportInfo)
| project AssetName = TargetNodeName, CVE = SourceNodeName
```

This query will return all vulnerabilities (CVEs) reported by Tenable on ingested assets.

```kusto
ExposureGraphEdges
| where EdgeLabel == "affecting" 
| where SourceNodeLabel == "Cve" 
| where isnotempty(EdgeProperties.rawData.tenableReportInfo)
| project AssetName = TargetNodeName, CVE = SourceNodeName
```

Note

When troubleshooting Advanced Hunting (AH) queries that don't work or yield no results, note that the "reportedBy" field is case-sensitive. For example, valid values include "rapid7", "tenable", etc.

### Attack paths

Security Exposure Management automatically generates attack paths based on the data collected across assets and workloads, including data from external connectors. It simulates attack scenarios, and identifies vulnerabilities and weaknesses that an attacker could exploit.

Note

Attack paths aren't currently supported for OT data connectors.

As you explore attack paths in your environment, you can view the discovery sources that contributed to this attack path based on the graphical view of the path.

[![Screensot of attach path with discovery source](media/value-data-connectors/attack paths data connectors.png)](media/value-data-connectors/attack%20paths%20data%20connectors.png#lightbox)