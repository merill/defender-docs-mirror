---
layout: Conceptual
title: Stop SAP data collection - Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/sap/stop-collection
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
description: Learn how to stop Microsoft Sentinel from collecting data from your SAP applications when you use the agentless data connector.
ms.author: monaberdugo
author: mberdugo
ms.topic: how-to
ms.date: 2026-08-04T00:00:00.0000000Z
ai-usage: ai-assisted
ms.collection: usx-security
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 2188db19-5dfb-6599-ece6-3a23423ccd83
document_version_independent_id: 23c95022-d8b8-1be4-9fec-efdb71974f2d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/sap/stop-collection.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/sap/stop-collection
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/sap/stop-collection.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: e90da198-9b2c-c7e1-3a58-3572a6d3e84f
---

# Stop SAP data collection - Microsoft Sentinel | Microsoft Learn

There might be instances where you need to halt data collection from your SAP applications by the Microsoft Sentinel agentless data connector, whether for maintenance, troubleshooting, or other administrative reasons.

Stopping data collection has two parts:

1. Disable or remove the agentless data connector so Microsoft Sentinel stops polling your SAP system.
2. Reverse the SAP-side configuration you applied when you [prepared your SAP system](preparing-sap), if you no longer plan to ingest SAP data.

## Prerequisites

Before you stop data collection from your SAP applications, ensure you have administrative access to:

- The Log Analytics workspace that's enabled for Microsoft Sentinel. For more information, see [Roles and permissions in Microsoft Sentinel](../roles).
- Your SAP system, so you can reverse the ABAP role and connectivity configuration.
- Your SAP Cloud Integration tenant, so you can pause or undeploy the **Data Collector** integration flow.

## Stop log ingestion

To stop ingestion without permanently removing the connector, pause the **Data Collector** integration flow in SAP Cloud Integration. Microsoft Sentinel stops receiving new records until you redeploy the integration flow.

To stop ingestion permanently:

1. In Microsoft Sentinel, select **Configuration** &gt; **Data connectors** and search for **Microsoft Sentinel for SAP - agentless**.
2. Select the data connector row and then select **Open connector page** in the side pane.
3. Under **Configuration**, remove each configured SAP system (SID). Removing every SID stops ingestion and billing for those systems.
4. Undeploy the **Data Collector** integration flow from SAP Cloud Integration.
5. Optionally, delete the data collection rule (DCR), data collection endpoint (DCE), and the Entra ID app registration that were created for the connector.

## Remove the user role from your ABAP system

If you're stopping ingestion and don't plan to reconnect, remove the ABAP user, the **MSFTSEN\_SENTINEL\_READER** role, and any optional Change Requests you installed while preparing your SAP system.