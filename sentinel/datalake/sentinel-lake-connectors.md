---
layout: Conceptual
title: Set Up Connectors for the Microsoft Sentinel Data Lake - Microsoft Security | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/sentinel-lake-connectors
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
ms.subservice: sentinel-platform
search.appverid: met150
description: Set up connectors for the Microsoft Sentinel data lake and configure data retention across analytics and data lake tiers.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: sourinpaul
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: ms-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: ca577723-1dda-f656-2169-92139b720a5e
document_version_independent_id: b3790a9a-da26-5991-7121-77cdc8b80f7a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/sentinel-lake-connectors.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/sentinel-lake-connectors
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/sentinel-lake-connectors.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: acff9b8f-6aaf-976c-0a36-22d22d79eb88
---

# Set Up Connectors for the Microsoft Sentinel Data Lake - Microsoft Security | Microsoft Learn

The Microsoft Sentinel data lake mirrors data from Microsoft Sentinel workspaces. When you onboard to Microsoft Sentinel data lake, your existing Microsoft Sentinel data connectors are configured to send data to both the analytics tier - your Microsoft Sentinel workspaces, and mirror the data to the data lake tier for longer term storage. After onboarding, configure your connectors to retain data in each tier according to your requirements.

This article explains how to configure retention and data tiering, manage XDR data, custom log tables, auxiliary log tables, and direct ingestion for the Microsoft Sentinel data lake. For more information on onboarding, see [Onboarding to Microsoft Sentinel data lake](sentinel-lake-onboarding).

## Configure retention and data tiering

After onboarding, you can enable new connectors and configure retention for existing connectors. You can choose to send the data to the analytics tier and mirror the data to the data lake tier or send the data only to the data lake tier. You manage retention and tiering from the connector setup pages, or by using the **Table management** page in the Defender portal. For more information on table management and retention, see [Manage data tiers and retention in Microsoft Defender portal](../manage-data-overview).

[![A diagram showing the analytics and data lake tiers.](media/setting-up-sentinel-data-lake/data-tiers.png)](media/setting-up-sentinel-data-lake/data-tiers.png#lightbox)

When you enable a connector, by default the data is sent to the analytics tier and mirrored in the data lake tier. When you enable Microsoft Sentinel data lake, the mirroring is automatically enabled for all the tables from onboarding forward. Mirrored data in the data lake with the same retention as the analytics tier doesn't incur extra billing charges. Preexisting data in the tables isn't mirrored. The retention of the data lake tier is set to the same value as the analytics tier. You can switch to ingest data to data lake tier only. When you configure to ingest only to the data lake tier, ingestion to the analytics tier stops and the existing data in the analytics tier is retained according to the retention settings.

The data retained in the Archive tier is still available and can be restored by using Search and Restore functionality.

To configure retention and tiering for your connectors, see [Configure data connector](../configure-data-connector).

## Microsoft Sentinel XDR data

By default, Microsoft Defender XDR retains threat hunting data in the Analytics tier for 30 days. This data is always available. Some XDR tables can be ingested into the analytics and data lake tiers by increasing the retention time to more than 30 days. You can also ingest XDR data directly into the data lake tier without the analytics tier. For more information, see [Manage XDR data in Microsoft Sentinel](../manage-data-overview#manage-xdr-data-in-microsoft-sentinel).

## Understand custom log table support for the Microsoft Sentinel data lake

Microsoft Monitoring Agent(MMA) and Log analytics Agent (CLV1) custom tables aren't mirrored to the data lake.

Tables created by using the Logs Ingestion API or Azure Monitor Agent (AMA) and DCR-based custom tables are mirrored. For more information, see [Logs Ingestion API in Azure Monitor](/en-us/azure/azure-monitor/logs/logs-ingestion-api-overview).

## Auxiliary log tables

When you onboard to both Microsoft Defender and Microsoft Sentinel and then onboard to the data lake, you no longer see auxiliary log tables in Microsoft Defender’s Advanced hunting or in the Microsoft Sentinel Azure portal. The auxiliary table data is available in the data lake and you can query it by using KQL queries or Jupyter notebooks. Find KQL queries under **Microsoft Sentinel** &gt; **Data lake exploration** in the Defender portal.

## Direct ingestion to the data lake

You can ingest data directly into the Microsoft Sentinel data lake without routing it through the analytics tier. This approach is useful when you want to store security data for long-term analysis without the associated analytics tier costs. For more information, see [Direct log ingestion to the Microsoft Sentinel data lake](sentinel-lake-log-ingestion-guidance).