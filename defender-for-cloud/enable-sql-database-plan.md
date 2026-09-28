---
layout: Conceptual
title: Deploy Defender for Azure SQL Databases - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/enable-sql-database-plan
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
description: Enable Defender for Azure SQL Databases as part of the Databases plan to protect SQL resources with threat detection and response in Defender for Cloud.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 2a8dcf46-2a2a-2479-e30b-ae7f7d304db1
document_version_independent_id: 258a7eef-2aac-a3e7-a94d-0e173df84e5b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/enable-sql-database-plan.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/enable-sql-database-plan
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/enable-sql-database-plan.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab7faaf-d791-4a26-96a2-3b11738538e7
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/302e28b0-1f09-4811-9a9b-2a72e0770581
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 9f08e234-0e3e-a869-620c-70dbc468e94e
---

# Deploy Defender for Azure SQL Databases - Microsoft Defender for Cloud | Microsoft Learn

Defender for Azure SQL Databases in Microsoft Defender for Cloud helps protect your Azure SQL databases with attack detection and threat response. Defender for Cloud protects Azure SQL database engines and data types based on their attack surface and security risks.

## Prerequisites

Before you enable Defender for Azure SQL Databases, make sure you have the following prerequisites:

- You need a Microsoft Azure subscription. If you don't have one, [sign up for a free Azure subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- You must [enable Microsoft Defender for Cloud](get-started#enable-defender-for-cloud-on-your-azure-subscription) on your Azure subscription.
- You must connect [non-Azure machines](quickstart-onboard-machines), an [Amazon Web Services (AWS) account](quickstart-onboard-aws), or a [Google Cloud Platform (GCP) project](quickstart-onboard-gcp).
- You must [enable the Defender for Databases plan](tutorial-enable-databases-plan) on your Defender for Cloud subscription.

## Enable Defender for Azure SQL Databases

Enabling the Defender for Azure SQL Databases plan activates protection for all Azure SQL databases in your subscription.

1. Open the [Azure portal](https://portal.azure.com) and sign in.
2. Search for and select **Microsoft Defender for Cloud**.
3. In the Defender for Cloud menu, select **Environment settings**.
4. Select the Azure subscription, AWS account, or GCP project where you want to enable Defender for Azure SQL Databases.
5. Locate the Databases plan and select **Select types**.

    [![Screenshot of the environment settings page that shows you where the select types button is located.](media/enable-sql-database-plan/select-type.png)](media/enable-sql-database-plan/select-type.png#lightbox)
6. Switch Azure SQL Databases to **On**.

    [![Screenshot that shows you where to select, to enable the Azure SQL Databases plan.](media/enable-sql-database-plan/toggle-on.png)](media/enable-sql-database-plan/toggle-on.png#lightbox)
7. Select **Continue**.
8. Select **Save**.