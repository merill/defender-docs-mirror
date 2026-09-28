---
layout: Conceptual
title: Deploy the Microsoft Sentinel solution for SAP applications | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/sap/deployment-overview
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
description: Get an introduction to the process of deploying the Microsoft Sentinel solution for SAP applications.
ms.author: monaberdugo
author: mberdugo
ms.topic: overview
ms.date: 2026-08-04T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
locale: en-us
document_id: 834d52f7-23fe-8970-424e-cd58d728f2a7
document_version_independent_id: b4f5c826-7029-e43d-6df3-0268015f348f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/sap/deployment-overview.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/sap/deployment-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/sap/deployment-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: d311b441-3745-b216-f8b2-be7a39774e80
---

# Deploy the Microsoft Sentinel solution for SAP applications | Microsoft Learn

Use the Microsoft Sentinel solution for SAP applications to monitor your SAP systems with Microsoft Sentinel, detecting sophisticated threats throughout the business logic and application layers of your SAP applications.

This article introduces you to the Microsoft Sentinel solution for SAP applications deployment.

## Solution components

The Microsoft Sentinel solution for SAP applications includes a data connector, which collects logs from your SAP systems and sends them to your Microsoft Sentinel workspace, and out-of-the-box security content, which helps you gain insight into your organization's SAP environment and detect and respond to security threats.

### Data connector

The Microsoft Sentinel solution for SAP applications uses the agentless data connector, which collects application logs for all your onboarded SAP SIDs from across the SAP system landscape, and then sends those logs to your Log Analytics workspace in Microsoft Sentinel.

Important

The containerized data connector agent for SAP [retired on September 14, 2026](https://azure.microsoft.com/updates?id=571342), and is unsupported and unmaintained. Existing TLS-compliant agents might continue sending logs through the retired HTTP Data Collector API. On October 14, 2026, container images will be removed, preventing new pulls, installation, redeployment, scaling, replacement, and disaster recovery. [Migrate to the supported SAP agentless data connector](sap-agent-migrate) now. Customers who already use the agentless connector aren't affected.

The Microsoft Sentinel agentless data connector for SAP uses the SAP Cloud Connector and SAP Integration Suite to connect to your SAP system and pull logs from it, as shown in the following image:

[![Diagram that shows the Microsoft Sentinel agentless data connector in an SAP environment.](media/deployment-overview/agentless-connector.png)](media/deployment-overview/agentless-connector.png#lightbox)

By using the SAP Cloud Connector, the agentless data connector profits from already existing setups and established integration processes. This means you don't have to tackle network challenges again, as the people running your SAP Cloud Connector have already gone through that process.

For sizing, throughput tuning, and isolation guidance, see [Configure SAP Cloud Connector settings](preparing-sap#configure-sap-cloud-connector-settings) and [Optimize SAP Cloud Connector sizing, throughput, and isolation](preparing-sap#optimize-sap-cloud-connector-sizing-throughput-and-isolation).

The agentless data connector is compatible with [SAP NetWeaver based systems](https://help.sap.com/docs/SAP_NETWEAVER?state=PRODUCTION&amp;version=ALL). Among them SAP S/4HANA Cloud, Private Edition (RISE with SAP), SAP S/4HANA on-premises, SAP ERP Central Component (ECC), SAP Business Warehouse (BW), and more, ensuring continued functionality of existing security content, including detections, workbooks, and playbooks.

The agentless data connector ingests critical security logs such as the security audit log, change docs logs and user master data including user roles and authorizations.

### Security content

The Microsoft Sentinel solutions for SAP applications include the following types of security content to help you gain insight into your organization's SAP environment and detect and respond to security threats:

- **Analytics rules** and **watchlists** for threat detection.
- **Functions** for easy data access.
- **Workbooks** to create interactive data visualization.
- **Watchlists** for customization of the built-in solution parameters.
- **Playbooks** that you can use to automate responses to threats.

For more information, see [Microsoft Sentinel solution for SAP applications: security content reference](sap-solution-security-content).

## Deployment flow and personas

Deploying the Microsoft Sentinel solution for SAP applications involves several steps and requires collaboration across your **security** and **SAP BASIS** teams. The following image shows the steps in deploying the Microsoft Sentinel solution for SAP applications, with relevant teams indicated:

![Diagram showing the full steps in the deployment flow for the Microsoft Sentinel agentless data connector for SAP applications.](media/deployment-steps/full-flow-agentless.png)

We recommend that you involve both teams when planning your deployment to ensure that effort is allocated and the deployment can move smoothly.

**Deployment steps include**:

1. [Review the prerequisites for deploying the SAP agentless data connector](prerequisites-for-deploying-sap-continuous-threat-monitoring).
2. [Deploy the SAP applications solution from the content hub](deploy-sap-security-content). This step is handled by the security team on the Azure portal.
3. [Configure your SAP system for the Microsoft Sentinel solution](preparing-sap), including configuring SAP authorizations, configuring SAP auditing, and more. We recommend that these steps be done by your SAP BASIS team, and our documentation includes references to SAP documentation. Some of the procedures in this step can be done by the SAP BASIS team before installing the solution.
4. [Connect your SAP system](deploy-data-connector-agentless) using the agentless data connector with the SAP Cloud Connector. This step is handled by your security team on the Azure portal, using information provided by your SAP BASIS team.
5. [Enable SAP detections and threat protection](deployment-solution-configuration). This step is handled by the security team on the Azure portal.

**Extra options include:**

- [Collect SAP HANA audit logs](collect-sap-hana-audit-logs)
- [Deploy the Microsoft Sentinel solution for SAP BTP](deploy-sap-btp-solution)

## Stop SAP data collection

If you need to stop Microsoft Sentinel from collecting your SAP data, disable or remove the agentless data connector and then reverse the SAP-side preparation you applied.

For more information, see [Stop SAP data collection](stop-collection).