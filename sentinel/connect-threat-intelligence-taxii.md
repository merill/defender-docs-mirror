---
layout: Conceptual
title: Connect to STIX/TAXII threat intelligence feeds - Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/connect-threat-intelligence-taxii
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
description: Learn how to connect Microsoft Sentinel to STIX/TAXII threat intelligence feeds to import indicators and configure TAXII 2.1 export to share intelligence with external platforms.
ms.author: pauloliveria
author: poliveria
ms.reviewer: yoninave
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: usx-security
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 8aec840a-3984-3893-3f0b-fb0647dfc129
document_version_independent_id: 7a4278c4-86d5-b119-960b-b916036ac655
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/connect-threat-intelligence-taxii.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/connect-threat-intelligence-taxii
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/connect-threat-intelligence-taxii.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 888e6ee8-b24a-926e-52b8-ad680194832f
---

# Connect to STIX/TAXII threat intelligence feeds - Microsoft Sentinel | Microsoft Learn

[STIX and TAXII](https://oasis-open.github.io/cti-documentation/) are the most common open standards for sharing threat intelligence. Microsoft Sentinel has built-in connectors that use these standards to import and export threat data.

Use the Threat Intelligence – TAXII data connector to pull threat indicators from TAXII 2.0 or 2.1 servers. To send threat data to outside platforms, set up the Threat Intelligence – TAXII Export connector for TAXII 2.1 export.

This article shows you how to set up both import and export with TAXII servers.

Learn more about [threat intelligence](understand-threat-intelligence) and [TAXII feeds](threat-intelligence-integration#taxii-threat-intelligence-feeds) in Microsoft Sentinel.

Note

For information about feature availability in US Government clouds, see the Microsoft Sentinel tables in [Cloud feature availability for US Government customers](/en-us/azure/security/fundamentals/feature-availability).

For more information, see [Connect your threat intelligence platform (TIP) to Microsoft Sentinel](connect-threat-intelligence-tip).

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Prerequisites

Before you begin, make sure you have the following prerequisites:

- To install, update, and delete standalone content or solutions in the **Content hub**, you need the Microsoft Sentinel Contributor role at the resource group level.
- You must have a TAXII 2.0 or TAXII 2.1 API root URI and collection ID.

## Get the TAXII server API root and collection ID

TAXII 2.x servers advertise API roots, which are URLs that host collections of threat intelligence. You can usually find the API root and the collection ID in the documentation pages of the threat intelligence provider that hosts the TAXII server.

Note

In some cases, the provider only advertises a URL called a discovery endpoint. You can use the [cURL](https://en.wikipedia.org/wiki/CURL) utility to browse the discovery endpoint and request the API root.

## Install the Threat Intelligence solution in Microsoft Sentinel

To import or export threat indicators with a TAXII server, install the Threat Intelligence solution:

1. For Microsoft Sentinel in the [Azure portal](https://portal.azure.com), under **Content management**, select **Content hub**.

    For Microsoft Sentinel in the [Defender portal](https://security.microsoft.com/), select **Microsoft Sentinel** &gt; **Content management** &gt; **Content hub**.
2. Find and select the **Threat Intelligence** solution.
3. Select the ![](media/connect-mdti-data-connector/install-update-button.png)**Install/Update** button.

To manage solution parts, see [Discover and deploy out-of-the-box content](sentinel-solutions-deploy).

## Enable the Threat Intelligence - TAXII data connector

To configure the TAXII data connector:

1. Select the **Data connectors** menu.
2. Find and select the **Threat Intelligence - TAXII** data connector, and then select **Open connector page**.

    [![Screenshot that shows the Data connectors page with the TAXII data connector listed.](media/connect-threat-intelligence-taxii/taxii-data-connector.png)](media/connect-threat-intelligence-taxii/taxii-data-connector.png#lightbox)
3. In the **Friendly name** text box, enter a name for this TAXII server collection.
4. Fill in **API root URL**, **Collection ID**, **Username** (if needed), and **Password** (if needed).
5. Choose the group of indicators and the polling frequency.
6. Select **Add**.

    ![Screenshot that shows configuring TAXII servers.](media/connect-threat-intelligence-taxii/threat-intel-configure-taxii-servers.png)

You should receive confirmation that a connection to the TAXII server was established successfully. Repeat the last step as many times as you want to connect to multiple collections from one or more TAXII servers.

Within a few minutes, threat indicators should begin flowing into your Microsoft Sentinel workspace. Find the new indicators on the **Threat intelligence** pane. You can access the **Threat intelligence** pane from the Microsoft Sentinel menu.

### IP allowlisting for the Microsoft Sentinel TAXII client

Some TAXII servers, like FS-ISAC, have a requirement to keep the IP addresses of the Microsoft Sentinel TAXII client on the allowlist. Most TAXII servers don't have this requirement.

When relevant, the following IP addresses are the addresses to include in your allowlist:

- 20.193.17.32
- 20.197.219.106
- 20.48.128.36
- 20.199.186.58
- 40.80.86.109
- 52.158.170.36

- 20.52.212.85
- 52.251.70.29
- 20.74.12.78
- 20.194.150.139
- 20.194.17.254
- 51.13.75.153

- 102.133.139.160
- 20.197.113.87
- 40.123.207.43
- 51.11.168.197
- 20.71.8.176
- 40.64.106.65

## Enable the Threat intelligence - TAXII Export data connector

To configure the Threat Intelligence - TAXII Export connector:

1. Confirm you have the latest Threat Intelligence solution. For details, see Install the Threat Intelligence solution in Microsoft Sentinel.
2. Select the **Data connectors** menu.
3. Select the **Threat intelligence - TAXII Export** data connector. Then select **Open connector page** in the side pane.

    [![Screenshot that shows the Data connectors page with the TAXII Export data connector listed.](media/connect-threat-intelligence-taxii/taxii-export-data-connector.png)](media/connect-threat-intelligence-taxii/taxii-export-data-connector.png#lightbox)
4. In the **Configuration** area on the **Threat intelligence - TAXII Export** page:

    - In the **Friendly name (for server)** text box, enter a name for this server.
    - Fill in **API root URL** and **Collection ID**. For details, see Get the TAXII server API root and collection ID.
    - From the **Authentication type** dropdown, select **Basic authentication** or **API key**. Then enter your credentials.
    - Select **Enable rules** to apply the connector page rules to all exported threat data.

    For example:

# [Defender portal](#tab/defender-portal)
[![Screenshot that shows configuring the TAXII Export server for export in the Defender portal.](media/connect-threat-intelligence-taxii/add-taxii-export.png)](media/connect-threat-intelligence-taxii/add-taxii-export.png#lightbox)

# [Azure portal](#tab/azure-portal)
[![Screenshot that shows configuring the TAXII Export server for export in the Azure portal.](media/connect-threat-intelligence-taxii/add-taxii-export-azure.png)](media/connect-threat-intelligence-taxii/add-taxii-export-azure.png#lightbox)

---

    Note

    Editing existing connectors is currently not supported. To change the configuration of a TAXII server or its rules, reinstall the TAXII Export connector.
5. Select **Add** to add your server.

### IP allowlisting for the Threat Intelligence - TAXII Export connector

Add these IP addresses to your allowlist to ensure that your export operations don't get blocked:

- 68.218.134.151
- 4.237.173.121
- 68.218.191.192
- 68.218.191.208
- 74.163.73.85
- 74.163.73.84
- 108.140.47.197
- 108.140.47.196
- 130.107.0.17
- 130.107.0.16
- 52.242.47.153
- 52.242.47.152
- 4.186.93.129
- 4.186.93.128
- 57.158.18.39
- 57.158.18.38
- 128.203.32.17
- 20.232.93.192
- 128.24.7.173
- 128.24.7.172
- 4.251.60.81
- 4.251.60.80
- 20.111.81.65
- 20.111.81.64
- 20.218.50.5
- 20.218.50.4

- 72.144.227.117
- 72.144.227.116
- 51.4.37.231
- 20.217.163.215
- 72.146.91.160
- 4.232.40.176
- 74.176.2.247
- 74.176.2.246
- 74.226.38.228
- 4.190.136.176
- 4.181.55.53
- 4.181.55.52
- 20.200.167.49
- 20.200.167.48
- 4.207.244.69
- 132.164.237.192
- 4.235.51.87
- 4.235.51.86
- 51.120.182.208
- 4.220.173.230
- 4.171.25.225
- 4.171.25.224
- 4.253.54.45
- 4.253.54.44
- 172.209.40.109
- 172.209.40.108

- 172.188.182.119
- 172.188.182.118
- 20.207.217.212
- 74.224.83.8
- 135.225.179.229
- 135.225.179.228
- 20.91.127.183
- 20.91.127.182
- 4.226.56.22
- 74.242.228.97
- 74.242.60.137
- 74.242.4.65
- 74.243.66.228
- 74.243.66.227
- 74.243.225.230
- 74.243.225.229
- 74.177.108.204
- 172.187.102.73
- 51.142.135.18
- 51.142.135.17
- 50.85.238.240
- 132.220.84.130
- 172.184.49.127
- 172.184.49.126
- 4.149.254.64
- 172.179.34.64