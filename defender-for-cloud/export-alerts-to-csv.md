---
layout: Conceptual
title: Download a CSV report - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/export-alerts-to-csv
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Learn how to download and export your alerts and recommendations to a CSV file from Microsoft Defender for Cloud.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 548f9038-c861-5a4d-3deb-71c9cd6289dc
document_version_independent_id: 33cb6ab0-5d50-b9ca-7bad-d89b382952a4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/export-alerts-to-csv.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/export-alerts-to-csv
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/export-alerts-to-csv.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: d7259c0e-cb5f-a6fe-5f4d-066d955e32ce
---

# Download a CSV report - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud has the ability to export all alerts and recommendations to a CSV file. This feature is useful when you want to analyze the data in a different tool or share it with others.

Tip

Due to Azure Resource Graph limitations, the reports are limited to a file size of 25,000 rows. If you see errors related to too much data being exported, try limiting the output by selecting a smaller set of subscriptions to be exported.

Note

These reports contain alerts and recommendations for resources from the currently selected subscriptions.

## Prerequisites

Before you export alerts or recommendations, make sure you meet the following prerequisites:

- You need a Microsoft Azure subscription. If you don't have an Azure subscription, you can [sign up for a free subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- You must [enable Microsoft Defender for Cloud](get-started#enable-defender-for-cloud-on-your-azure-subscription) on your Azure subscription.

## Export alerts to a CSV file

To export your security alerts to a CSV file, follow these steps:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Search for and select **Microsoft Defender for Cloud**.
3. Select **Security alerts**.
4. Select **Download CSV report**.

    [![Screenshot that shows how to download alerts data as a CSV file.](media/export-alerts-to-csv/download-report.png)](media/export-alerts-to-csv/download-report.png#lightbox)

## Export recommendations to a CSV file

To export your security recommendations to a CSV file, follow these steps:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Search for and select **Microsoft Defender for Cloud**.
3. Select **Recommendations**.
4. Select **Download CSV report**.