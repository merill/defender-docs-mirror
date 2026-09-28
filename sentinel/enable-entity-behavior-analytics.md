---
layout: Conceptual
title: Enable entity behavior analytics to detect advanced threats | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/enable-entity-behavior-analytics
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
description: Enable User and Entity Behavior Analytics in Microsoft Sentinel, and configure data sources
ms.author: guywild
author: guywi-ms
ms.reviewer: mshechter
ms.topic: how-to
ms.date: 2026-08-07T00:00:00.0000000Z
ms.collection: usx-security
ms.custom: sfi-image-nochange, msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: 5857d241-7924-3cc9-a97b-6cb87529ed69
document_version_independent_id: 70fd12a8-7672-8aff-73f6-0edb455ffeb2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/enable-entity-behavior-analytics.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/enable-entity-behavior-analytics
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/enable-entity-behavior-analytics.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 47e10f79-0aca-09bc-87e7-aaabbce4fe04
---

# Enable entity behavior analytics to detect advanced threats | Microsoft Learn

User and Entity Behavior Analytics (UEBA) in Microsoft Sentinel analyzes logs and alerts from connected data sources to build baseline behavioral profiles of your organization's entities—such as users, hosts, IP addresses, and applications. Using machine learning, UEBA identifies anomalous activity that might indicate a compromised asset.

You can enable UEBA and configure data sources directly from the UEBA tab. See Access UEBA from the UEBA tab.

This article explains how to enable UEBA and configure data sources from your Microsoft Sentinel workspace settings and from supported data connectors. Before you begin, review the Prerequisites section for required roles and permissions.

For more information about UEBA, see [Identify threats with entity behavior analytics](identify-threats-with-entity-behavior-analytics).

Note

For information about feature availability in US Government clouds, see the Microsoft Sentinel tables in [Cloud feature availability for US Government customers](/en-us/azure/security/fundamentals/feature-availability).

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Prerequisites

To enable or disable User and Entity Behavior Analytics (UEBA) (these prerequisites aren't required to use UEBA):

- Your user must be assigned to the Microsoft Entra ID **Security Administrator** role in your tenant or the equivalent permissions.
- Your user must be assigned at least one of the following **Azure roles** ([Azure RBAC](roles)):

    - **Owner** at the resource group level or higher.
    - **Contributor** at the resource group level or higher.
    - (Least privileged) **Microsoft Sentinel Contributor** at the workspace level or higher and **Log Analytics Contributor** at the resource group level or higher.
- Your workspace must not have any Azure resource locks applied to it. For more information, see [Azure resource locking](/en-us/azure/azure-resource-manager/management/lock-resources).

Note

- No special license is required to add UEBA functionality to Microsoft Sentinel, and there's no extra cost for using it.
- However, since UEBA generates new data and stores it in new tables that UEBA creates in your Log Analytics workspace, **additional data storage charges** apply.

## Access UEBA from UEBA tab

To get to the **Entity behavior configuration** page:

1. From the Microsoft Defender portal navigation menu, select **System** &gt;**Settings** &gt; **Microsoft Sentinel**.
2. Select the **UEBA** tab.

![Screenshot of UEBA tab.](media/enable-entity-behavior-analytics/entity-behavior-analytics-tab.png)

## Configure UEBA

To configure UEBA on the **Entity behavior configuration** page, complete the following steps:

1. On the **Entity behavior configuration** page, toggle on **Turn on UEBA feature**.

    [![Screenshot of UEBA configuration settings.](media/enable-entity-behavior-analytics/entity-behavior-analytics-configuration.png)](media/enable-entity-behavior-analytics/entity-behavior-analytics-configuration.png#lightbox)
2. Select the directory services from which you want to synchronize user entities with Microsoft Sentinel.

    - **Active Directory** on-premises
    - **Microsoft Entra ID**

    To sync user entities from on-premises Active Directory, you must onboard your Azure tenant to Microsoft Defender for Identity (either standalone or as part of Microsoft Defender XDR) and you must have the MDI sensor installed on your Active Directory domain controller. For more information, see [Microsoft Defender for Identity prerequisites](/en-us/defender-for-identity/prerequisites).
3. Select **Connect all data sources** to connect all eligible data sources, or select specific data sources from the list.

    You can only enable these data sources from the Defender and the Azure portals:

    - Signin Logs
    - Audit Logs
    - Azure Activity
    - Security Events

    You can enable these data sources from the Defender portal only:

    - AAD Managed Identity Signin logs (Microsoft Entra ID)
    - AAD Service Principal Signin logs (Microsoft Entra ID)
    - AWS CloudTrail
    - Amazon GuardDuty
    - `CommonSecurityLog` for supported Check Point, Fortinet, and Zscaler events
    - Device Logon Events
    - Okta CL
    - GCP Audit Logs

    UEBA analyzes identity signals and supported network and cloud signals. For the authoritative list of sources, required tables, supported vendor logs, and field requirements, see [Microsoft Sentinel UEBA reference](ueba-reference). For anomaly details, see [UEBA anomalies](anomalies-reference#ueba-anomalies).

    Note

    After enabling UEBA, you can enable supported data sources for UEBA directly from the data connector pane, or from the Defender portal Settings page.
4. Select **Connect**.
5. Enable anomaly detection in your Microsoft Sentinel workspace:

    1. From the Microsoft Defender portal navigation menu, select **Settings** &gt; **Microsoft Sentinel** &gt; **SIEM workspaces**.
    2. Select the workspace you want to configure.
    3. From the workspace configuration page, select **Anomalies** and toggle on **Detect Anomalies**.

    UEBA investigation and hunting data is available in tables such as `BehaviorAnalytics` and `BehaviorInfo`. For table schemas and usage guidance, see [Microsoft Sentinel UEBA reference](ueba-reference) and [Translate raw security logs to behavioral insights using UEBA behaviors](entity-behaviors-layer).

## Install the UEBA Essentials solution (optional)

The **UEBA Essentials** solution is a collection of dozens of prebuilt hunting queries curated and maintained by Microsoft security experts. The solution includes multicloud anomaly detection queries across Azure, Amazon Web Services (AWS), Google Cloud Platform (GCP), and Okta.

Install the solution to get started quickly with threat hunting and investigations using UEBA data, instead of building these detection capabilities from scratch.

For more information, see [Install or update Microsoft Sentinel solutions](sentinel-solutions-deploy#install-or-update-content).

## Enable the UEBA behaviors layer

The UEBA behaviors layer generates enriched summaries of activity observed in multiple data sources. Unlike alerts or anomalies, behaviors don't necessarily indicate risk. They create an abstraction layer that optimizes your data for investigations, hunting, and detection by improving clarity, context, and correlation. Behavior records can also include anomaly insights and contextual enrichment associated with the activity.

For more information about the UEBA behaviors layer and how to enable it, see [Enable the UEBA behaviors layer in Microsoft Sentinel](entity-behaviors-layer).