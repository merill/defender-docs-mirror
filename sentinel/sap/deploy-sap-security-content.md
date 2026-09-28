---
layout: Conceptual
title: Install a Microsoft Sentinel solution for SAP applications | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/sap/deploy-sap-security-content
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
description: Learn how to install a Microsoft Sentinel solution for SAP applications from the content hub to your Log Analytics workspace enabled for Microsoft Sentinel.
ms.author: monaberdugo
author: mberdugo
ms.topic: how-to
ms.date: 2026-08-04T00:00:00.0000000Z
ms.collection: usx-security
ms.custom: sfi-image-nochange, msecd-doc-authoring-1014
ai-usage: ai-assisted
locale: en-us
document_id: 7ffdc379-3b2d-e191-2c1f-d64890ae7d87
document_version_independent_id: ae47f4b5-8286-be66-6848-85636271840f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/sap/deploy-sap-security-content.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/sap/deploy-sap-security-content
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/sap/deploy-sap-security-content.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 724c8a4c-4a6f-5ca5-0198-52dd36491a7d
---

# Install a Microsoft Sentinel solution for SAP applications | Microsoft Learn

This article shows you how to install the Microsoft Sentinel solution for SAP applications from the content hub. The solution includes an SAP data connector, which collects logs from your SAP systems and sends them to your Microsoft Sentinel workspace, and out-of-the-box security content—including workbooks and analytics rules—that helps you gain insight into your organization's SAP environment and detect and respond to security threats. Installing your solution is a required step before you can configure your data connector. Before you start, make sure you meet the [prerequisites for deploying the Microsoft Sentinel solution for SAP applications](prerequisites-for-deploying-sap-continuous-threat-monitoring).

![Diagram of the SAP solution deployment flow, highlighting the Install solution content step.](media/deployment-steps/install-solution-agentless.png)

Content in this article is relevant for your **security** team.

## Prerequisites

To deploy a Microsoft Sentinel solution for SAP applications from the content hub, you need:

- A Log Analytics workspace enabled for Microsoft Sentinel.
- Read and write permissions to the workspace. For more information, see [Roles and permissions in Microsoft Sentinel](../roles).

Make sure that you also review the [prerequisites for deploying Microsoft Sentinel solution for SAP applications](prerequisites-for-deploying-sap-continuous-threat-monitoring), especially [Azure prerequisites](prerequisites-for-deploying-sap-continuous-threat-monitoring#azure-prerequisites).

## Install the solution

Installing the **Microsoft Sentinel Solution for SAP** makes the agentless data connector available to you from the Microsoft Sentinel **Configuration &gt; Data connectors** page. The solution also deploys security content, such as the **SAP -Audit Controls** workbook and SAP-related analytics rules.

1. In the Microsoft Sentinel **Content hub**, search for **SAP** to install the **SAP applications** solution.
2. On the **Microsoft Sentinel solution for SAP applications** page, select **Create** to define deployment settings. For example:

    [![Screenshot that shows the Microsoft Sentinel solution for SAP applications solution pane.](media/deploy-sap-security-content/sap-solution.png)](media/deploy-sap-security-content/sap-solution.png#lightbox)
3. On the default **Basics** tab, scroll down to select where to install the solution.
4. Select **Review + create** or **Next** to browse through the solution components. When you're ready, select **Create**

    The deployment process can take a few minutes. After the deployment is finished, you can view the deployed content in Microsoft Sentinel.

For more information, see [Discover and manage Microsoft Sentinel out-of-the-box content](../sentinel-solutions-deploy).

## View deployed content

When the SAP applications solution deployment is finished, display your new content by browsing again to the Microsoft Sentinel for SAP applications solution from the **Content hub**. Alternatively, to view the deployed content without returning to the Content hub:

- For the [built-in SAP workbooks](sap-solution-security-content#built-in-workbooks), in Microsoft Sentinel, go to **Threat Management** &gt; **Workbooks** &gt; **Templates**.
- For a series of [SAP-related analytics rules](sap-solution-security-content#built-in-analytics-rules), go to **Configuration** &gt; **Analytics** **Rule templates**.

Your data connector doesn't appear as connected until you [configure your data connector](deploy-data-connector-agentless) and complete the connection.