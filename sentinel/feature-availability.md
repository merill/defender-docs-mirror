---
layout: Conceptual
title: Microsoft Sentinel feature support for Azure commercial/other clouds | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/feature-availability
breadcrumb_path: breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
description: This article describes feature availability in Microsoft Sentinel across different Azure environments.
ms.author: bagol
author: batamig
ms.reviewer: noak
ms.topic: feature-availability
ms.custom: references_regions
ms.date: 2026-09-29T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 4c31fbee-c47b-13bf-008c-625983560b8f
document_version_independent_id: a5817daf-fabf-95ae-3628-d4e4b6e02a9d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/feature-availability.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/feature-availability
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/feature-availability.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/15545907-caea-48c1-a546-e84930c5b845
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fd70c557-2c67-40b8-b517-cf047ce6d0c3
platformId: f411eb92-137c-c7a4-367e-6c21f6991a90
---

# Microsoft Sentinel feature support for Azure commercial/other clouds | Microsoft Learn

This article describes the features available in Microsoft Sentinel across different Azure environments. Features are listed as GA (generally available), public preview, or shown as not available.

Note

These lists and tables do not include feature or bundle availability in the Azure Government Secret or Azure Government Top Secret clouds. For more information about specific availability for air-gapped clouds, please contact your account team.

Important

Microsoft Sentinel was retired in Azure operated by 21Vianet on August 18, 2026, as described in the [announcement posted by 21Vianet](https://aka.ms/sentinelretirementinchina). Microsoft Sentinel is no longer available in this region.

We recommend that customers work with their account representatives for Microsoft Azure operated by 21Vianet to assess the impact of this retirement on their own operations.

## Experience in the Defender portal

Microsoft Sentinel is also available in the [Microsoft Defender portal](microsoft-sentinel-defender-portal). In the Defender portal, all features in general availability are available in commercial, GCC, GCC High and DoD clouds. Features still in preview are available only in the commercial cloud.

For more information, see [Microsoft Defender XDR for US Government customers](/en-us/defender-xdr/usgov).

## Analytics

| Feature | Feature stage | Azure commercial | Azure Government |
| --- | --- | --- | --- |
| [Analytics rules health](monitor-analytics-rule-integrity) | Public preview | Yes | Yes |
| [MITRE ATT&CK dashboard](mitre-coverage) | Public preview | Yes | Yes |
| [NRT rules](near-real-time-rules) | GA | Yes | Yes |
| [Recommendations](detection-tuning) | Public preview | Yes | Yes |
| [Scheduled](detect-threats-built-in) and [Microsoft rules](create-incidents-from-alerts) | GA | Yes | Yes |

## Content and content management

| Feature | Feature stage | Azure commercial | Azure Government |
| --- | --- | --- | --- |
| [Content hub](sentinel-solutions) and [solutions](sentinel-solutions-catalog) | GA | Yes | Yes |
| [Repositories](ci-cd?tabs=github) | Public preview | Yes | No |
| [Workbooks](monitor-your-data) | GA | Yes | Yes |

## Data collection

| Feature | Feature stage | Azure commercial | Azure Government |
| --- | --- | --- | --- |
| [Amazon Web Services](connect-aws?tabs=ct) | GA | Yes | Yes |
| [Amazon Web Services S3](connect-aws?tabs=s3) | GA | Yes | Yes |
| [Microsoft Entra ID](connect-azure-active-directory) | GA | Yes | Yes |
| [Microsoft Entra ID Protection](connect-services-api-based) | GA | Yes | Yes |
| [Azure Activity](data-connectors-reference#azure-activity) | GA | Yes | Yes |
| [Azure DDoS Protection](connect-services-diagnostic-setting-based) | GA | Yes | Yes |
| [Azure Firewall](data-connectors-reference#azure-firewall) | GA | Yes | Yes |
| [Azure Information Protection (Preview)](data-connectors-reference#microsoft-purview-information-protection) | Deprecated | No | No |
| [Azure Key Vault](data-connectors-reference#azure-key-vault) | Public preview | Yes | Yes |
| [Azure Kubernetes Service (AKS)](data-connectors-reference#azure-kubernetes-service-aks) | Public preview | Yes | Yes |
| [Azure SQL Databases](https://techcommunity.microsoft.com/t5/microsoft-sentinel-blog/azure-sentinel-sql-solution-query-deep-dive/ba-p/2597961) | GA | Yes | Yes |
| [Azure Web Application Firewall (WAF)](data-connectors-reference#azure-web-application-firewall-waf) | GA | Yes | Yes |
| [Cisco ASA](data-connectors-reference#cisco-asaftd-via-ama) | GA | Yes | Yes |
| [Codeless Connectors Platform](isv/create-codeless-connector?tabs=deploy-via-arm-template,connect-via-the-azure-portal) | Public preview | Yes | Yes |
| [Common Event Format (CEF)](connect-common-event-format) | GA | Yes | Yes |
| [Common Event Format (CEF) via AMA](connect-cef-syslog-ama) | GA | Yes | Yes |
| [DNS](data-connectors-reference#dns) | Public preview | Yes | No |
| [GCP Pub/Sub Audit Logs](connect-google-cloud-platform) | Public preview | Yes | Yes |
| [Microsoft Defender XDR](connect-microsoft-365-defender?tabs=MDE) | GA | Yes | Yes |
| [Microsoft Purview Insider Risk Management (Preview)](sentinel-solutions-catalog#domain-solutions) | Public preview | Yes | Yes |
| [Microsoft Defender for Cloud](connect-defender-for-cloud) | GA | Yes | Yes |
| [Microsoft Defender for IoT](connect-services-api-based) | GA | Yes | Yes |
| [Microsoft Power BI (Preview)](data-connectors-reference#microsoft-powerbi) | Public preview | Yes | Yes |
| [Microsoft Project (Preview)](data-connectors-reference#microsoft-project) | Public preview | Yes | Yes |
| [Microsoft Purview (Preview)](connect-services-diagnostic-setting-based) | Public preview | Yes | No |
| [Microsoft Purview Information Protection](connect-microsoft-purview) | Public preview | Yes | No |
| [Microsoft Sentinel solution for Microsoft Business Apps](business-applications/solution-overview) | GA | Yes | Yes |
| [Office 365](connect-services-api-based) | GA | Yes | Yes |
| [Summary rules](summary-rules) | GA | Yes | No |
| [Syslog](connect-syslog) | GA | Yes | Yes |
| [Syslog via AMA](connect-cef-syslog-ama) | GA | Yes | Yes |
| [Windows DNS Events via AMA](connect-dns-ama) | GA | Yes | Yes |
| [Windows Firewall](data-connectors-reference#windows-firewall) | GA | Yes | Yes |
| [Windows Forwarded Events](connect-services-windows-based) | GA | Yes | Yes |
| [Windows Security Events via AMA](connect-services-windows-based) | GA | Yes | Yes |

## Hunting

| Feature | Feature stage | Azure commercial | Azure Government |
| --- | --- | --- | --- |
| [Bookmarks](bookmarks) | GA | Yes | Yes |
| [Hunts](hunts) | Public preview | Yes | No |
| [Livestream](livestream) | GA | Yes | Yes |
| [Queries](hunts) | GA | Yes | Yes |
| [Restore historical data](restore) | GA | Yes | Yes |
| [Search large datasets](search-jobs) | GA | Yes | Yes |

## Incidents

| Feature | Feature stage | Azure commercial | Azure Government |
| --- | --- | --- | --- |
| [Add entities to threat intelligence](add-entity-to-threat-intelligence?tabs=incidents) | Public preview | Yes | Yes |
| [Advanced and/or conditions](add-advanced-conditions-to-automation-rules) | GA | Yes | Yes |
| [Automation rules](automate-incident-handling-with-automation-rules) | GA | Yes | Yes |
| [Automation rules health](monitor-automation-health) | Public preview | Yes | Yes |
| [Create incidents manually](create-incident-manually) | GA | Yes | Yes |
| [Cross-tenant/Cross-workspace incidents view](multiple-workspace-view) | GA | Yes | Yes |
| [Incident advanced search](investigate-cases#search-for-incidents) | GA | Yes | Yes |
| [Incident tasks](incident-tasks) | GA | Yes | Yes |
| [Microsoft Defender XDR incident integration](microsoft-365-defender-sentinel-integration#working-with-microsoft-defender-xdr-incidents-in-microsoft-sentinel-and-bi-directional-sync) | GA | Yes | Yes |
| [Microsoft Teams integrations](collaborate-in-microsoft-teams) | Public preview | Yes | Yes |
| [Playbook template gallery](use-playbook-templates) | Public preview | Yes | Yes |
| [Run playbooks on entities](respond-threats-during-investigation) | GA | Yes | Yes |
| [Run playbooks on incidents](automate-responses-with-playbooks) | GA | Yes | Yes |
| [SOC incident audit metrics](manage-soc-with-incident-metrics) | GA | Yes | Yes |

## Machine Learning

| Feature | Feature stage | Azure commercial | Azure Government |
| --- | --- | --- | --- |
| [Anomalous RDP login detection - built-in ML detection](configure-connector-login-detection) | Public preview | Yes | Yes |
| [Anomalous SSH login detection - built-in ML detection](connect-syslog#configure-the-syslog-connector-for-anomalous-ssh-login-detection) | Public preview | Yes | Yes |
| [Fusion](fusion) - advanced multistage attack detections ^1^ | GA | Yes | Yes |

^1^ Partially GA: The ability to disable specific findings from vulnerability scans is in public preview.

## Managing Microsoft Sentinel

| Feature | Feature stage | Azure commercial | Azure Government |
| --- | --- | --- | --- |
| [Workspace manager](workspace-manager) | Public preview | Yes | Yes |
| [SIEM migration experience](siem-migration) | GA | Yes | No |

## Normalization

| Feature | Feature stage | Azure commercial | Azure Government |
| --- | --- | --- | --- |
| [Advanced Security Information Model (ASIM)](normalization) | Public preview | Yes | Yes |

## Notebooks

| Feature | Feature stage | Azure commercial | Azure Government |
| --- | --- | --- | --- |
| [Notebooks](notebooks) | GA | Yes | Yes |
| [Notebook integration with Azure Synapse](notebooks-with-synapse) | Public preview | Yes | Yes |

## SOC optimizations

| Feature | Feature stage | Azure commercial | Azure Government |
| --- | --- | --- | --- |
| [SOC optimizations](soc-optimization/soc-optimization-access) | Supported for production use | Yes | No |

## SAP

| Feature | Feature stage | Azure commercial | Azure Government |
| --- | --- | --- | --- |
| [Threat protection for SAP](sap/deployment-overview) | GA | Yes | Yes |
| [Agentless data connector](sap/deployment-overview#data-connector) | Limited preview | Yes | No |

## Threat intelligence support

| Feature | Feature stage | Azure commercial | Azure Government |
| --- | --- | --- | --- |
| [GeoLocation and WhoIs data enrichment](work-with-threat-indicators) | Public preview | Yes | No |
| [Import TI from flat file](indicators-bulk-file-import) | Public preview | Yes | Yes |
| [Threat Intelligence Platform data connector](understand-threat-intelligence) | Public preview | Yes | Yes |
| [Threat Intelligence Research page](https://techcommunity.microsoft.com/t5/microsoft-sentinel-blog/what-s-new-threat-intelligence-menu-item-in-public-preview/ba-p/1646597) | GA | Yes | Yes |
| [Threat Intelligence - TAXII data connector](understand-threat-intelligence) | GA | Yes | Yes |
| [Microsoft Defender for Threat Intelligence connector](connect-mdti-data-connector) | Public preview | Yes | Yes |
| [Microsoft Defender Threat intelligence matching analytics](use-matching-analytics-to-detect-threats) | Public preview | Yes | No |
| [Threat Intelligence workbook](/en-us/azure/architecture/example-scenario/data/sentinel-threat-intelligence) | GA | Yes | Yes |
| [URL detonation](https://techcommunity.microsoft.com/t5/microsoft-sentinel-blog/using-the-new-built-in-url-detonation-in-azure-sentinel/ba-p/996229) | Public preview | Yes | No |
| [Threat Intelligence Upload Indicators API](connect-threat-intelligence-upload-api) | Public preview | Yes | Yes |

## UEBA

| Feature | Feature stage | Azure commercial | Azure Government |
| --- | --- | --- | --- |
| [Active Directory sync via MDI](enable-entity-behavior-analytics#access-ueba-from-ueba-tab) | Public preview | Yes | Yes |
| [Azure resource entity pages](entity-pages) | Public preview | Yes | Yes |
| [Entity insights](identify-threats-with-entity-behavior-analytics) | GA | Yes | Yes |
| [Entity pages](entity-pages) | GA | Yes | Yes |
| [Identity info table data ingestion](investigate-with-ueba) | GA | Yes | Yes |
| [IoT device entity page](/en-us/azure/defender-for-iot/organizations/iot-advanced-threat-monitoring#investigate-further-with-iot-device-entities) | Public preview | Yes | Yes |
| [Peer/Blast radius enrichments](identify-threats-with-entity-behavior-analytics#how-ueba-works) | Public preview | Yes | No |
| [SOC-ML anomalies](soc-ml-anomalies#what-are-customizable-anomalies) | GA | Yes | Yes |
| [UEBA anomalies](soc-ml-anomalies#ueba-anomalies) | GA | Yes | Yes |
| [UEBA enrichments\insights](investigate-with-ueba) | GA | Yes | Yes |

## Watchlists

| Feature | Feature stage | Azure commercial | Azure Government |
| --- | --- | --- | --- |
| [Large watchlists from Azure Storage](watchlists) | Public preview | Yes | Yes |
| [Watchlists](watchlists) | GA | Yes | Yes |
| [Watchlist templates](watchlist-schemas) | Public preview | Yes | Yes |