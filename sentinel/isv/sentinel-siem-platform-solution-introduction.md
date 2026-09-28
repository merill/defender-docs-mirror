---
layout: Conceptual
title: Microsoft Sentinel SIEM and platform solution overview | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/isv/sentinel-siem-platform-solution-introduction
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
description: Learn how Microsoft Sentinel SIEM and platform solutions differ, find the right build and publish guidance for each path, and get support when you need it.
author: EdB-MSFT
ms.author: edbaynash
ms.topic: concept-article
ms.custom: msecd-doc-authoring-101
ms.date: 2026-06-28T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: ac772ca8-9733-8f3b-7816-a24def53ce5e
document_version_independent_id: aa3f0617-7fc0-a1b7-c861-59df4de94155
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/isv/sentinel-siem-platform-solution-introduction.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/isv/sentinel-siem-platform-solution-introduction
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/isv/sentinel-siem-platform-solution-introduction.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: a6787d6a-11d4-9c80-2ff9-90363046107d
---

# Microsoft Sentinel SIEM and platform solution overview | Microsoft Learn

Microsoft Sentinel ISV solutions are partner-built integrations and content that extend Microsoft Sentinel for customer scenarios. As an independent software vendor (ISV), you package your product's connectors, detections, automation, and analytics experiences into a solution that customers discover, install, and use directly inside Microsoft Sentinel. A well-built solution lets customers onboard your product in minutes instead of building integrations themselves, and it gives your product a presence in the marketplaces that security teams already use.

You can build two solution types, and they target different parts of the Microsoft Sentinel experience:

- **SIEM solutions** deliver detection, investigation, and automated response content for Security Operations Center (SOC) teams. They bring your product's logs into Microsoft Sentinel and turn that data into ready-to-use analytics rules, hunting queries, workbooks, playbooks, and parsers.
- **Platform solutions** deliver large-scale data analysis and AI-driven experiences built on the Microsoft Sentinel data lake and graph. They include Security Copilot agents, Model Context Protocol (MCP) tools, custom graphs, and notebook jobs for scenarios that analyze large volumes of security data.

The two paths use different content types, build tooling, quality requirements, and publishing flows. Understanding the differences early helps you choose the right content path, scope your work accurately, and avoid rework before you start development and publishing. The rest of this article compares the two solution types and links to the detailed build and publish guidance for each.

## Compare SIEM and platform solutions

The two solution types serve different customer needs, use different content, and publish through different stores.

| - | SIEM solutions | Platform solutions |
| --- | --- | --- |
| **Purpose** | Detection, investigation, and automated response for Security Operations Center (SOC) teams | Large-scale data analysis and AI-driven scenarios that use the Microsoft Sentinel data lake and graph |
| **Primary audience** | SOC analysts, threat hunters, and detection engineers | Security data scientists, threat researchers, and teams building AI-assisted investigations |
| **Typical content** | Data connectors, analytics rules, hunting queries, summary rules, workbooks, playbooks, and Advanced Security Information Model (ASIM) parsers | Security Copilot agents, Model Context Protocol (MCP) tools, custom graphs, and notebook jobs |
| **Foundation** | Microsoft Sentinel workspace and content hub | Microsoft Sentinel data lake and graph |
| **Data scope** | Real-time and near-real-time analytics on workspace tables | Large historical and high-volume datasets stored in the data lake |
| **Build tooling** | AI connector builder agent, Codeless Connector Framework (CCF), YAML content templates, and the V3 solution packaging tool | KQL jobs, VS Code notebook and graph development tools, and the platform packaging flow |

If you're not sure which content your scenario needs, start with [Decide which components to include in your solution](siem-components-to-include) for SIEM solutions .

## Build and publish SIEM solutions

SIEM solutions focus on detections, investigations, and automation for SOC teams. Use the following articles to plan, build content, publish, and maintain a SIEM solution.

### Plan and understand the lifecycle

- [Build and publish Microsoft Sentinel SIEM solutions](sentinel-integration-guide)
- [Develop a SIEM solution for Microsoft Sentinel](develop-siem-solutions-overview)
- [Decide which components to include in your solution](siem-components-to-include)
- [Microsoft Sentinel SIEM solution quality guidelines](sentinel-siem-solution-quality-guidance)

### Build data connectors

- [Build custom connectors with AI in Microsoft Sentinel](create-custom-connector-builder-agent)
- [Create a pull codeless connector (CCF)](create-codeless-connector)
- [Create push codeless connectors (CCF)](create-push-codeless-connector)

### Build detection, hunting, and visualization content

- [Create analytics rules](sentinel-analytic-rules-creation)
- [Create hunting queries](sentinel-hunting-rules-creation)
- [Create summary rules](sentinel-summary-rules-creation)
- [Create workbooks](sentinel-workbook-creation)
- [Create parsers](sentinel-parsers-creation)
- [Create playbooks](sentinel-playbook-creation)
- [Develop Advanced Security Information Model (ASIM) parsers](../normalization-develop-parsers)

### Publish and maintain

- [Publish SIEM solutions to Microsoft Sentinel](publish-sentinel-solutions)
- [Microsoft Sentinel solution lifecycle in Partner Center](sentinel-solutions-post-publish-tracking)

## Troubleshoot solutions

If you run into data ingestion, analytics, packaging, or agent integration issues while building or publishing either solution type, see [Troubleshoot solutions in Microsoft Sentinel](troubleshoot-sentinel-solutions).

## Contact App Assure

If you're an independent software vendor (ISV) and need support when building a Microsoft Sentinel integration by using the Microsoft Sentinel Codeless Connector Framework, the Microsoft App Assure team might be able to assist. To engage the App Assure team, send an email to AzureSentinelPartner@microsoft.com for assistance.