---
layout: Conceptual
title: Prerequisites for deploying Microsoft Sentinel solution for SAP applications | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/sap/prerequisites-for-deploying-sap-continuous-threat-monitoring
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
description: This article lists the prerequisites required for deployment of the Microsoft Sentinel solution for SAP applications.
ms.author: monaberdugo
author: mberdugo
ms.topic: reference
ms.date: 2026-08-04T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
locale: en-us
document_id: 63a9d2dc-e99d-c84a-68da-e93fc1d5e40d
document_version_independent_id: 956d8159-ba5a-07db-0215-9a2a3fcc58d2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/sap/prerequisites-for-deploying-sap-continuous-threat-monitoring.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/sap/prerequisites-for-deploying-sap-continuous-threat-monitoring
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/sap/prerequisites-for-deploying-sap-continuous-threat-monitoring.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 0279eb14-602d-9525-42fb-e223152c9f10
---

# Prerequisites for deploying Microsoft Sentinel solution for SAP applications | Microsoft Learn

This article lists the prerequisites required for deployment of the Microsoft Sentinel solution for SAP applications with the agentless data connector and the SAP Cloud Connector.

Reviewing and ensuring that you have or understand all the prerequisites is the first step in deploying the Microsoft Sentinel solution for SAP applications. Select a connection type to list the prerequisites for your environment.

![Diagram of the steps included in deploying the Microsoft Sentinel solution for SAP applications, with the prerequisites step highlighted.](media/deployment-steps/prerequisites-agentless.png)

Content in this article is relevant for your **security** and **SAP BASIS** teams.

## Azure prerequisites

Typically, Azure prerequisites are managed by your **security** teams.

| Prerequisite | Description | Required/optional |
| --- | --- | --- |
| **Permissions to create Azure resources** | You must have: - The necessary permissions to deploy solutions from the Microsoft Sentinel content hub. For more information, see [Prerequisites for deploying Microsoft Sentinel solutions](../sentinel-solutions-deploy#prerequisites) and [Microsoft Entra built-in roles](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator). Owner on the Microsoft Sentinel resource group, required for:- Creation of data collection rule and data collection endpoint.- Monitoring Metrics Publisher role assignment on data collection rule. | Required |
| **Permissions in Microsoft Entra** | You must have permissions in Microsoft Entra ID required to create app registrations. This permission can be obtained through membership of built-in Microsoft Entra ID role:- Application Developer. | Required |

## SAP prerequisites for the agentless data connector

We recommend that your **SAP BASIS** team verify and ensure SAP system prerequisites. The SAP BASIS admin should review SAP notes 3390051 and 382318 to ensure that NetWeaver is set up for integration.

We strongly recommend that any management of your SAP system is carried out by an experienced SAP system administrator.

| Prerequisite | Description |
| --- | --- |
| **Supported SAP versions** | The **Agentless** solution supports SAP NetWeaver systems with [SAP_BASIS versions 750](https://userapps.support.sap.com/sap%28bD1kZSZjPTAwMQ==%29/support/pam/pam.html?smpsrv=https%3a%2f%2fwebsmp201.sap-ag.de#ts=60&amp;s=netweaver%207.5&amp;o=most_viewed%7Cdesc&amp;st=l&amp;rpp=20&amp;page=1&amp;pvnr=73554900100900000414&amp;pt=g%7Cd) and above. This includes SAP S/4HANA Cloud private edition systems operated by SAP ECS in RISE. For SAP S/4HANA Cloud public edition (SaaS) use [SAP's connector](https://azuremarketplace.microsoft.com/marketplace/apps/sap_jasondau.azure-sentinel-solution-s4hana-public?tab=Overview) instead. Change Docs logs running on Sybase aren't supported. If you're using Sybase, we recommend that you customize your system to turn off ingestion for Change Docs logs. For more information, see [Customize data connector behavior (optional)](deploy-data-connector-agentless#customize-data-connector-behavior-optional). |
| **SAP environment** | Your SAP environment must have:  The **RSAU\_API\_GET\_LOG\_DATA** function module, remote enabled on your SAP System. For more information, see the [SAP documentation](https://me.sap.com/notes/3054326/E). An SAP BTP Subaccount with following services enabled:  - SAP Integration Suite - SAP Process Integration Runtime - Cloud Foundry Runtime For more information, see the [SAP documentation](https://help.sap.com/docs/sap-hana-spatial-services/onboarding/creating-subaccount-on-sap-business-technology-platform-sap-btp). [Trial accounts](https://developers.sap.com/tutorials/hcp-create-trial-account.html) are supported.The [SAP Cloud Connector](https://help.sap.com/docs/connectivity/sap-btp-connectivity-cf/installation?locale=en-US) deployed SAP NetWeaver version 7.5 or higher |
| **SAP roles and permissions** | You must have the following roles in your SAP systems: **In SAP NetWeaver 7.5+**: SAP Netweaver Administrator **In SAP BTP, all of the following roles**:- Subaccount administrator - Integration Provisioner - PI\_Administrator - PI\_Integration\_Developer - PI\_Business\_Expert |

## Plan your ingestion

We recommend that you test your systems to determine the number of logs that each of your SAP systems sends to Microsoft Sentinel. Microsoft Sentinel billing depends on log ingestion size, which in turn depends on factors such as system usage, modules deployed, number of users, running use cases, network traffic, and log types.

For more information, see:

- [Solution pricing](sap-applications-overview#solution-pricing)
- [Plan costs and understand Microsoft Sentinel pricing and billing](../billing)
- [Reduce costs for Microsoft Sentinel](../billing-reduce-costs)
- [Manage and monitor costs for Microsoft Sentinel](../billing-monitor-costs)