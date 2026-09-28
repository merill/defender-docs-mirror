---
layout: Conceptual
title: Microsoft Sentinel solutions for SAP - Partner Add-ons | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/sap/solution-partner-overview
breadcrumb_path: ../breadcrumb/toc.json
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
ms.reviewer: mapankra
description: Discover partners specializing in Microsoft Sentinel for SAP integration solutions, consulting, and managed services.
ms.author: edbaynash
author: EdB-MSFT
ms.topic: partner-tools
ms.date: 2025-07-10T00:00:00.0000000Z
ms.collection: usx-security
locale: en-us
document_id: dc27419f-0e62-bdc1-7bef-ad048418c939
document_version_independent_id: 529a4e08-8124-8536-37f6-3aa84cc08c87
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/sap/solution-partner-overview.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/sap/solution-partner-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/sap/solution-partner-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/5e44decf-e201-4396-9baa-d26b1372789f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/66922d0c-a09e-47eb-8764-2aa2d787014d
platformId: f0fe81ad-f613-d569-4958-0e5573b0dba5
---

# Microsoft Sentinel solutions for SAP - Partner Add-ons | Microsoft Learn

Microsoft Sentinel provides a flexible platform that enables SAP and Microsoft partners to deliver integrated security solutions through the Microsoft Sentinel Content Hub.

Add-ons enable further correlational capabilities for the Microsoft Sentinel Solution for SAP applications. SAP signals are correlated with signals from other Microsoft and third-party solutions, enabling comprehensive threat detection and response across the entire IT landscape using the Microsoft unified Security Operations platform.

[![Diagram that shows correlation of a user compromise involving SAP through Microsoft Sentinel solution for SAP.](media/partner/solution-overview.png)](media/partner/solution-overview.png#lightbox)

This article provides an overview of the partner ecosystem that builds upon and specializes in integration with the [Microsoft Sentinel Solution for SAP applications](solution-overview).

## Partner contributions

These solutions include ready-to-use connectors activating the Microsoft internal log streams such as AS ABAP Security Audit Log. Furthermore, specialized workbooks, dedicated analytics rules, and playbooks are provided.

### Solutions provided by SAP as vendor

Choose from Microsoft Sentinel solution add-ons build by SAP for SAP.

| Name | Description | Azure Marketplace link |
| --- | --- | --- |
| [SAP Enterprise Threat Detection, cloud edition (ETD)](https://community.sap.com/t5/enterprise-resource-planning-blog-posts-by-sap/sap-enterprise-threat-detection-cloud-edition-joins-forces-with-microsoft/ba-p/13942075) | The SAP Enterprise Threat Detection, cloud edition (ETD) solution enables ingestion of security alerts from ETD into Microsoft Sentinel, supporting cross-correlation, alerting, and threat hunting. ETD supplies curated alerts from SAP ERP, SuccessFactors, Ariba, and other SAP SaaS applications. | [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/sap_jasondau.azure-sentinel-solution-sapetd?tab=Overview) |
| [SAP LogServ (RISE), S/4HANA Cloud private edition](https://community.sap.com/t5/enterprise-resource-planning-blog-posts-by-sap/sap-logserv-integration-with-microsoft-sentinel-for-sap-rise-customers-is/bc-p/14089301) | SAP LogServ is an SAP Enterprise Cloud Services (ECS) service aimed at collection, storage, forwarding, and access of logs. LogServ centralizes the logs from all systems, and ECS services used by a registered customer. Main Features include: Near real-time log collection with ability to integrate into Microsoft Sentinel. LogServ complements the existing SAP application layer capabilities of the Microsoft Sentinel Solutions for SAP. SAP LogServ includes logs like: SAP HANA database, AS JAVA, SAP Web Dispatcher, SAP Cloud Connector, Operating System, third-party Databases, Network, DNS, Proxy, Firewall, etc. | [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/sap_jasondau.azure-sentinel-solution-saplogserv?tab=Overview) |
| [SAP S/4HANA Cloud public edition (GROW)](https://community.sap.com/t5/technology-blog-posts-by-sap/sap-s-4hana-cloud-public-edition-security-integrating-microsoft-sentinel/ba-p/14258811) | The SAP S/4HANA Cloud Public Edition add-on for the [Microsoft Sentinel Solution for SAP](sap-solution-security-content) will collect logs from sources like the SAP S/4HANA cloud security audit log, detect threats, suspicious activities, illegitimate activities, and more | [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/sap_jasondau.azure-sentinel-solution-s4hana-public?tab=Overview) |

### Solutions provided by specialized SAP security vendors

Add-ons streamline detection and response by translating SAP-specific risks into actionable insights using capabilities from Microsoft Sentinel Solution for SAP.

| Name | Description | Azure Marketplace link |
| --- | --- | --- |
| Onapsis | Onapsis provides comprehensive SAP security and compliance solutions with native integration into Microsoft Sentinel Solution for SAP. Onapsis supports ABAP code scanning, vulnerability management, and real-time monitoring across SAP environments. | [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/onapsis.azure-sentinel-solution-onapsis-defend?tab=Overview) |
| Pathlock | Pathlock provides native SAP Threat Detection and Response for Microsoft Sentinel Solution for SAP, forwarding only security-relevant, context-enriched events from 70+ SAP log sources to enhance detection accuracy and streamline SOC operations. | [Azure Marketplace](https://marketplace.microsoft.com/product/azure-applications/pathlockinc1631410274035.pathlock_tdnr?tab=Overview) |
| SecurityBridge | SecurityBridge provides advanced SAP security monitoring, threat detection, and compliance solutions with native integration into Microsoft Sentinel Solution for SAP and Microsoft Entra ID. Specialized in SAP vulnerability management, ABAP code scanning, and real-time security monitoring across SAP landscapes | [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/securitybridge1647511278080.securitybridge-sentinel-app-1?tab=Overview) |

### Solutions provided by the community

Extension patterns available for the agentless data connector of the Microsoft Sentinel Solution for SAP applications enable individual enhancements and extended scope of the Microsoft provided solution. Customers, partners, and individual community members share their artifacts via [this official repos](https://github.com/Azure-Samples/Sentinel-For-SAP-Community).

[![Diagram that shows the community extension pattern for the agentless Microsoft Sentinel solution for SAP.](media/partner/overview.png)](media/partner/overview.png#lightbox)

Get started from the [contribution guide](https://github.com/Azure-Samples/Sentinel-For-SAP-Community?tab=readme-ov-file#contributing-) or reach out via [GitHub issues](https://github.com/Azure-Samples/Sentinel-For-SAP-Community/issues).

## Implementation and managed services partners

Implementation and managed services partners apply above solutions in addition to your Sentinel solution for SAP applications and offer hands-on support. This involves helping set up the Microsoft Sentinel Solution for SAP and your chosen add-on, delivering managed Security Operations Center (SOC), compliance monitoring, and continuous improvement.

Discover partner solutions from the Azure marketplace or from the [Microsoft Solution Partner finder](https://appsource.microsoft.com/marketplace/partner-dir).

| Partner | Azure Marketplace link |
| --- | --- |
| Delaware | [Protecting SAP: 3 day workshop](https://azuremarketplace.microsoft.com/marketplace/consulting-services/delaware.sec_protect_sap?search=Delaware&amp;page=1) |
| EY | [EY Application Threat Detection and Response Service for SAP (TDR)](https://azuremarketplace.microsoft.com/marketplace/apps/ey_global.ey_application_tdr_for_sap?tab=Overview) |
| IBM | [IBM Threat Management with Microsoft’s SAP Threat Monitoring Solution for Microsoft Azure](https://azuremarketplace.microsoft.com/marketplace/consulting-services/ibm-ny-armonk-hq-6205522-ibmsecurity-xftm.ibm-security-svcs-threatmanagement-sapthreatmon?page=1&amp;search=ibm%20security%20services) |
| PWC | [Secure SAP on Microsoft Cloud](https://azuremarketplace.microsoft.com/marketplace/apps/pwc.secure_sap_on_microsoft_cloud?tab=Overview) |

Tip

You're a partner looking to expand your SAP Security offerings and get listed? Reach out to the Microsoft Sentinel for SAP team through [GitHub issues](https://github.com/Azure-Samples/Sentinel-For-SAP-Community/issues).