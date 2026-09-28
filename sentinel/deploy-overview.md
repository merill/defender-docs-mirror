---
layout: Conceptual
title: Deployment guide for Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/deploy-overview
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
description: Learn about the steps to deploy Microsoft Sentinel including the phases to plan and prepare, deploy, and fine tune.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: abhiag
ms.topic: concept-article
ms.date: 2025-07-09T00:00:00.0000000Z
locale: en-us
document_id: 75d96cee-c991-a77b-220e-3135a9cb5668
document_version_independent_id: befbeb27-11dd-a5e1-0c0a-fc386e7b4fcb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/deploy-overview.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/deploy-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/deploy-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: cefa04b2-6f68-d519-d55d-f03b24d3ac54
---

# Deployment guide for Microsoft Sentinel | Microsoft Learn

This article introduces the activities that help you plan, deploy, and fine tune your Microsoft Sentinel deployment.

## Plan and prepare overview

This section introduces the activities and prerequisites that help you plan and prepare before deploying Microsoft Sentinel.

The plan and prepare phase is typically performed by a SOC architect or related roles.

| Step | Details |
| --- | --- |
| **1. Plan and prepare overview and prerequisites** | Review the [Azure tenant prerequisites](prerequisites). |
| **2. Plan workspace architecture** | Design your Log Analytics workspace enabled for Microsoft Sentinel. Regardless of whether you'll be onboarding to the Microsoft Defender portal, you'll still need a Log Analytics workspace. Consider parameters such as:- Whether you'll use a single tenant or multiple tenants- Any compliance requirements you have for data collection and storage- How to control access to Microsoft Sentinel dataReview these articles:1. [Design workspace architecture](/en-us/azure/azure-monitor/logs/workspace-design?toc=/azure/sentinel/TOC.json&amp;bc=/azure/sentinel/breadcrumb/toc.json)2. [Review sample workspace designs](sample-workspace-designs)3. [Prepare for multiple workspaces](prepare-multiple-workspaces) |
| **3. [Prioritize data connectors](prioritize-data-connectors)** | Determine which data sources you need and the data size requirements to help you accurately project your deployment's budget and timeline.You might determine this information during your business use case review, or by evaluating a current SIEM that you already have in place. If you already have a SIEM in place, analyze your data to understand which data sources provide the most value and should be ingested into Microsoft Sentinel. |
| **4. [Plan roles and permissions](roles)** | Use Azure role based access control (RBAC) to create and assign roles within your security operations team to grant appropriate access to Microsoft Sentinel. The different roles give you fine-grained control over what Microsoft Sentinel users can see and do. Azure roles can be assigned in the workspace directly, or in a subscription or resource group that the workspace belongs to, which Microsoft Sentinel inherits. |
| **5. [Plan costs](billing)** | Start planning your budget, considering cost implications for each planned scenario. Make sure that your budget covers the cost of data ingestion for both Microsoft Sentinel and Azure Log Analytics, any playbooks that will be deployed, and so on. |

## Deployment overview

The deployment phase is typically performed by a SOC analyst or related roles.

| Step | Details |
| --- | --- |
| [**1. Enable Microsoft Sentinel, health and audit, and content**](enable-sentinel-features-content) | Enable Microsoft Sentinel, enable the health and audit feature, and enable the solutions and content you've identified according to your organization's needs.  To onboard to Microsoft Sentinel by using the API, see the latest supported version of [Sentinel Onboarding States](/en-us/rest/api/securityinsights/sentinel-onboarding-states). |
| [**2. Configure content**](configure-content) | Configure the different types of Microsoft Sentinel security content, which allow you to detect, monitor, and respond to security threats across your systems: Data connectors, analytics rules, automation rules, playbooks, workbooks, and watchlists. |
| [**3. Set up a cross-workspace architecture**](use-multiple-workspaces) | If your environment requires multiple workspaces, you can now set them up as part of your deployment. In this article, you learn how to set up Microsoft Sentinel to extend across multiple workspaces and tenants. |
| [**4. Enable User and Entity Behavior Analytics (UEBA)**](enable-entity-behavior-analytics) | Enable and use the UEBA feature to streamline the analysis process. |
| [**5. Configure Microsoft Sentinel data lake**](datalake/sentinel-lake-onboarding) | Configure interactive and data retention settings to ensure your organization retains critical long-term data, leveraging the Microsoft Sentinel data lake for cost-effective storage, enhanced visibility, and seamless integration with advanced analytics tools. |

## Fine tune and review: Checklist for post-deployment

Review the post-deployment checklist to helps you make sure that your deployment process is working as expected, and that the security content you deployed is working and protecting your organization according to your needs and use cases.

The fine tune and review phase is typically performed by a SOC engineer or related roles.

| Step | Actions |
| --- | --- |
| ✅ **Review incidents and incident process** | - Check whether the incidents and the number of incidents you're seeing reflect what's actually happening in your environment.- Check whether your SOC's incident process is working to efficiently handle incidents: Have you assigned different types of incidents to different layers/tiers of the SOC?Learn more about how to [navigate and investigate](investigate-incidents) incidents and how to [work with incident tasks](work-with-tasks). |
| ✅ **Review and fine-tune analytics rules** | - Based on your incident review, check whether your analytics rules are triggered as expected, and whether the rules reflect the types of incidents you're interested in.- [Handle false positives](false-positives), either by using automation or by modifying scheduled analytics rules.- Microsoft Sentinel provides built-in fine-tuning capabilities to help you analyze your analytics rules. [Review these built-in insights and implement relevant recommendations](detection-tuning). |
| ✅ **Review automation rules and playbooks** | - Similar to analytics rules, check that your automation rules are working as expected, and reflect the incidents you're concerned about and are interested in.- Check whether your playbooks are responding to alerts and incidents as expected. |
| ✅ **Add data to watchlists** | Check that your watchlists are up to date. If any changes have occurred in your environment, such as new users or use cases, [update your watchlists accordingly](watchlists-manage). |
| ✅ **Review commitment tiers** | [Review the commitment tiers](billing#analytics-tier) you initially set up, and verify that these tiers reflect your current configuration. |
| ✅ **Keep track of ingestion costs** | To keep track of ingestion costs, use one of these workbooks:- The [**Workspace Usage Report** workbook](billing-monitor-costs#deploy-a-workbook-to-visualize-data-ingestion-into-the-analytics-tier) provides your workspace's data consumption, cost, and usage statistics. The workbook gives the workspace's data ingestion status and amount of free and billable data. You can use the workbook logic to monitor data ingestion and costs, and to build custom views and rule-based alerts.- The **Microsoft Sentinel Cost** workbook gives a more focused view of Microsoft Sentinel costs, including ingestion and retention data, ingestion data for eligible data sources, Logic Apps billing information, and more. |
| ✅ **Fine-tune Data Collection Rules (DCRs)** | - Check that your [DCRs](/en-us/azure/azure-monitor/essentials/data-collection-rule-overview) reflect your data ingestion needs and use cases.- If needed, [implement ingestion-time transformation](data-transformation) to filter out irrelevant data even before it's first stored in your workspace. |
| ✅ **Check analytics rules against MITRE framework** | [Check your MITRE coverage in the Microsoft Sentinel MITRE page](mitre-coverage): View the detections already active in your workspace, and those available for you to configure, to understand your organization's security coverage, based on the tactics and techniques from the MITRE ATT&CK® framework. |
| ✅ **Hunt for suspicious activity** | Make sure that your SOC has a process in place for [proactive threat hunting](hunts). Hunting is a process where security analysts seek out undetected threats and malicious behaviors. By creating a hypothesis, searching through data, and validating that hypothesis, they determine what to act on. Actions can include creating new detections, new threat intelligence, or spinning up a new incident. |