---
layout: Conceptual
title: Connect Data Sources to Microsoft Sentinel by using Data Connectors | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/configure-data-connector
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
description: Learn how to connect data sources to Microsoft Sentinel using data connectors for improved threat detection.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: krishsa
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 7accbfb3-42d0-a690-62c1-f2da782fb6aa
document_version_independent_id: 56e8657a-d134-bf7c-5b81-176487a2d850
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/configure-data-connector.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/configure-data-connector
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/configure-data-connector.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 4579db48-04de-976b-3104-121f185be0d9
---

# Connect Data Sources to Microsoft Sentinel by using Data Connectors | Microsoft Learn

To connect data sources to Microsoft Sentinel, you need to install and configure data connectors. This article generally explains how to install data connectors available in the Microsoft Sentinel **Content hub** to ingest and analyze data for improved threat detection.

- [Microsoft Sentinel data connectors](connect-data-sources)
- [Find your Microsoft Sentinel data connector](data-connectors-reference)
- [Discover and manage Microsoft Sentinel out-of-the-box content](sentinel-solutions-deploy)

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Prerequisites

Before you begin, make sure you have the appropriate access and you or someone in your organization installs the related solution.

- You must have read and write permissions on the Microsoft Sentinel workspace.
- Install the solution that includes the data connector from the **Content Hub** in Microsoft Sentinel. For more information, see [Discover and manage Microsoft Sentinel out-of-the-box content](sentinel-solutions-deploy).

## Enable a data connector

After you or someone in your organization installs the solution that includes the data connector you need, configure the data connector to start ingesting data.

1. For Microsoft Sentinel in the [Defender portal](https://security.microsoft.com/), select **Microsoft Sentinel** &gt; **Configurations** &gt; **Data connectors**. For Microsoft Sentinel in the [Azure portal](https://portal.azure.com), under **Configuration**, select **Data connectors**.
2. Search for and select the connector. If you don't see the data connector you want, check again that the relevant solution is installed in the **Content hub**.
3. Select **Open connector page**.

# [Defender portal](#tab/defender-portal)
![Screenshot of data connector details page in the Defender portal.](media/configure-data-connector/open-connector-page-option-defender-portal.png)

# [Azure portal](#tab/azure-portal)
## ![Screenshot of data connector details page with open connector page button.](media/configure-data-connector/open-connector-page-option.png)

---
4. Review the **Prerequisites** for your data connector and ensure that they're fulfilled.
5. Follow the steps outlined in the **Configurations** section for your data connector.

    For some connectors, find more specific configuration information in the **Collect data** section of the relevant connector article in [Find your Microsoft Sentinel data connector](data-connectors-reference).

    - [Connect Microsoft Sentinel to Azure, Windows, Microsoft, and Amazon services](connect-azure-windows-microsoft-services)
    - [Data connector prerequisites](data-connectors-reference#windows-security-events-via-ama)

### Configure data retention and tiering

If you have onboarded to the Microsoft Sentinel data lake, you can configure data retention and tiering for the data connector. The data lake consists of an analytics tier - your current Microsoft Sentinel workspaces, and a data lake tier where you can store data for up to 12 years. For more information on onboarding, see [Onboarding to Microsoft Sentinel data lake](datalake/sentinel-lake-onboarding).

When you enable a connector, by default the data is sent to the analytics tier and mirrored in the data lake tier. Configure data retention in each tier or send the data only to the data lake tier. Retention and tiering are managed from the connector setup pages, or using the **Table management** page in the Defender portal. For more information on table management and retention, see [Manage data tiers and retention in Microsoft Defender Portal](manage-data-overview).

Once you have set up your connector, configure data retention and tiering using the following steps:

1. On the **Connector details** page, in the **Table management** section, select the table you want to manage.

    [![A screenshot showing a connector details page.](media/configure-data-connector/connector-details.png)](media/configure-data-connector/connector-details.png#lightbox)
2. The table panel is displayed showing the current retention settings.
3. To configure retention, select **Manage table**. [![A screenshot showing the manage table panel.](media/configure-data-connector/manage-table.png)](media/configure-data-connector/manage-table.png#lightbox)
4. The **Manage table** panel is displayed, showing the current retention settings. You can change the retention settings for the analytics tier and the data lake tier. The default is to mirror the data to the data lake tier with the same retention as the analytics tier.
5. Under **Analytics retention** select the retention period for the analytics tier.
6. To configure the data lake tier, select a retention period from the **Total retention** drop-down list. [![A screenshot showing the analytics and data lake tier options.](media/configure-data-connector/analytics-and-data-lake-tier.png)](media/configure-data-connector/analytics-and-data-lake-tier.png#lightbox)
7. To change the tier to data lake only, select the **Data lake tier** and select a retention period from the **Retention** drop-down list. Selecting this option stops further ingestion to the analytics tier.
8. Select **Save** to save the changes.

[![A screenshot showing the data lake tier retention only option.](media/configure-data-connector/data-lake-tier-only.png)](media/configure-data-connector/data-lake-tier-only.png#lightbox)

After you configure the data connector, it might take some time for the data to be ingested into Microsoft Sentinel. It takes 90 to 120 minutes for data to be ingested into the data lake. When the data connector is connected, you see a summary of the data in the **Data received** graph, and the connectivity status of the data types.

![Screenshot of a data connector page with status connected and graph that shows the data received.](media/configure-data-connector/connected-data-connector.png)

## Enable User and Entity Behavior Analytics (UEBA) from supported connectors

[User and Entity Behavior Analytics (UEBA) in Microsoft Sentinel](identify-threats-with-entity-behavior-analytics) analyzes logs and alerts from connected data sources to build baseline behavioral profiles of your organization's entities—such as users, hosts, IP addresses, and applications. Using machine learning, UEBA identifies anomalous activity that may indicate a compromised asset.

To enable UEBA from supported data connectors in Microsoft Defender portal:

1. From the Microsoft Defender portal navigation menu, select **Microsoft Sentinel &gt; Configuration &gt; Data connectors**.
2. Select a UEBA supported data connector that supports UEBA. For more information about UEBA supported data connectors and tables, see [Microsoft Sentinel UEBA reference](ueba-reference#ueba-data-sources).
3. From the data connector pane, select **Open connector page**.
4. On the **Connector details** page, select **Advanced options**.
5. Under **Configure UEBA**, toggle on the tables you want to enable for UEBA.

    [![Screenshot of UEBA configuration in data connector.](media/enable-entity-behavior-analytics/entity-behavior-analytics-data-connector.png)](media/enable-entity-behavior-analytics/entity-behavior-analytics-data-connector.png#lightbox)

## Find your data

After you enable the connector successfully, the connector begins to stream data to the table schemas related to the data types you configured.

In the Defender portal, query data in the **Advanced hunting** page, or in the Azure portal, query data in the **Logs** page.

Navigate to **Data lake explorer** &gt; **KQL queries** to query data in the data lake. For more information, see [KQL and the Microsoft Sentinel data lake](datalake/kql-overview).

## Find support for a data connector

Both Microsoft and other organizations author Microsoft Sentinel data connectors. Find the support contact on the connector's details page in Microsoft Sentinel.

1. In the Microsoft Sentinel **Data connectors** page, select the relevant connector.
2. To access support and maintenance for the connector, use the support contact link in the **Supported by** field on the side panel for the connector.

    [![Screenshot showing the Supported by field for a data connector in Microsoft Sentinel.](media/configure-data-connector/support.png)](media/configure-data-connector/support.png#lightbox)

For more information, see [Data connector support](connect-data-sources#data-connector-support).