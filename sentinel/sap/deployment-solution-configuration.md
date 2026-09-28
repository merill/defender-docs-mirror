---
layout: Conceptual
title: Enable SAP detections and threat protection with Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/sap/deployment-solution-configuration
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
description: This article shows you how to configure initial security content for the Microsoft Sentinel solution for SAP applications in order to start enabling SAP detections and threat protection.
ms.author: monaberdugo
author: mberdugo
ms.topic: how-to
ms.date: 2026-08-04T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: c7c49ee7-d729-c254-9298-6dcff9c0b0c8
document_version_independent_id: 3eb375e7-e279-a69f-e698-08d15b824023
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/sap/deployment-solution-configuration.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/sap/deployment-solution-configuration
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/sap/deployment-solution-configuration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: b7376784-aae4-90d7-acfd-b4ccf5f25f51
---

# Enable SAP detections and threat protection with Microsoft Sentinel | Microsoft Learn

Deploying the Microsoft Sentinel data collector and solution for SAP lets you monitor SAP systems for suspicious activities and identify threats. However, extra configuration steps are needed to optimize the solution for your SAP deployment. Configure the security content delivered with the Microsoft Sentinel solution for SAP applications as the final step in deploying the SAP integration.

![Diagram of the SAP solution deployment flow, highlighting the Configure solution settings step.](media/deployment-steps/settings-agentless.png)

Content in this article is relevant for your **security** team.

## Prerequisites

Before you configure the settings described in this article, make sure you have:

- A Microsoft Sentinel SAP solution installed
- A data connector configured

For more information, see [Deploy the Microsoft Sentinel solution for SAP applications from the content hub](deploy-sap-security-content) and [Deploy Microsoft Sentinel solution for SAP applications](deployment-overview).

Tip

Use the blog series "[How to successfully evaluate the SAP for Sentinel solution and implement it in production](https://techcommunity.microsoft.com/blog/microsoftsentinelblog/how-to-successfully-evaluate-the-sap-for-sentinel-solution-and-implement-it-in-p/4357962)" for a detailed walk through with best practices.

## Start enabling analytics rules

By default, all analytics rules in the Microsoft Sentinel solution for SAP are provided as [alert rule templates](../manage-analytics-rule-templates#manage-template-versions-for-your-scheduled-analytics-rules-in-microsoft-sentinel). We recommend a staged approach. Use the templates to create a few rules at a time, and allow time to fine-tune each scenario.

Start with the following analytics rules, which are simpler to test:

- [Change in Sensitive privileged user](sap-solution-security-content#suspicious-privileges-operations)
- [Sensitive privileged user logged in](sap-solution-security-content#suspicious-privileges-operations)
- [Sensitive privileged user makes a change in other user](sap-solution-security-content#suspicious-privileges-operations)
- [Sensitive Users Password Change and Login](sap-solution-security-content#suspicious-privileges-operations)
- [Client Configuration Change](sap-solution-security-content#attempts-to-bypass-sap-security-mechanisms)
- [Function Module tested](sap-solution-security-content#persistency)

For more information, see [Built-in analytics rules](sap-solution-security-content#built-in-analytics-rules) and [Threat detection in Microsoft Sentinel](../threat-detection).

## Configure watchlists

Configure your Microsoft Sentinel solution for SAP applications by providing customer-specific information in the following watchlists:

| Watchlist name | Configuration details |
| --- | --- |
| **SAP - Systems** | The **SAP - Systems** watchlist defines the SAP systems that are present in the monitored environment. For every system, specify: - The SID- Whether it's a production system or a dev/test environment. Defining this in your watchlist doesn't affect billing, and only influences your analytics rule. For example, you might want to use a test system as a production system while testing.- A meaningful description Configured data is used by some analytics rules, which might react differently if relevant events appear in a development or a production system. |
| **SAP - Networks** | The **SAP - Networks** watchlist outlines all networks used by the organization. It's primarily used to identify whether or not user sign-ins originate from within known segments of the network, or if a user's sign-in origin changes unexpectedly. There are many approaches for documenting network topology. You could define a broad range of addresses, like *172.16.0.0/16*, and name it *Corporate Network*, which is good enough for tracking sign-ins from outside that range. However, a more segmented approach, allows you better visibility into potentially atypical activity. For example, you might define the following segments and geographical locations: - 192.168.10.0/23: Western Europe - 10.15.0.0/16: Australia In such cases, Microsoft Sentinel can differentiate a sign-in from *192.168.10.15* in the first segment from a sign-in from *10.15.2.1* in the second segment. Microsoft Sentinel alerts you if such behavior is identified as atypical. |
| **SAP - Sensitive Function Modules** **SAP - Sensitive Tables** **SAP - Sensitive ABAP Programs** **SAP - Sensitive Transactions** | **Sensitive content watchlists** identify sensitive actions or data that can be carried out or accessed by users. While several well-known operations, tables, and authorizations are preconfigured in the watchlists, we recommend that you consult with your SAP BASIS team to identify the operations, transactions, authorizations and tables are considered to be sensitive in your SAP environment, and update the lists as needed. |
| **SAP - Sensitive Profiles** **SAP - Sensitive Roles** **SAP - Privileged Users** **SAP - Critical Authorizations** | The Microsoft Sentinel solution for SAP applications uses user data gathered in **user data watchlists** from SAP systems to identify which users, profiles, and roles should be considered sensitive. While sample data is included in the watchlists by default, we recommend that you consult with your SAP BASIS team to identify the sensitive users, roles, and profiles in your organization and update the lists as needed. |

After the initial solution deployment, it might take some time until the watchlists are populated with data. If you open a watchlist for editing and find that it's empty, wait a few minutes and try again.

For more information, see [Available watchlists](sap-solution-security-content#available-watchlists).

## Use a workbook to check compliance for your SAP security controls

The Microsoft Sentinel solution for SAP applications includes the **SAP - Security Audit Controls** workbook, which helps you check compliance for your SAP security controls. The workbook provides a comprehensive view of the security controls that are in place and the compliance status of each control.

For more information, see [Check compliance for your SAP security controls with the SAP - Security Audit Controls workbook](sap-audit-controls-workbook).