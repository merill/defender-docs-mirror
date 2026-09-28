---
layout: Conceptual
title: Enable Defender for Open-source Relational Databases on Azure - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/enable-defender-for-databases-azure
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
description: Detect anomalous activity and attempts to exploit Azure Database for PostgreSQL and MySQL with Microsoft Defender for open-source relational databases.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: b84fc073-882c-525d-7989-64ee23944cc9
document_version_independent_id: 5f7757b9-4b86-979a-8fa1-25f529bf0fa5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/enable-defender-for-databases-azure.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/enable-defender-for-databases-azure
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/enable-defender-for-databases-azure.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 234d8983-50b6-4e22-99a0-37c3319c4eae
---

# Enable Defender for Open-source Relational Databases on Azure - Microsoft Defender for Cloud | Microsoft Learn

Use Microsoft Defender for open-source relational databases to detect anomalous activity on Azure Database for PostgreSQL and Azure Database for MySQL. This article explains the prerequisites and the steps to enable the plan in Azure.

Microsoft Defender for Cloud detects anomalous activities that indicate unusual and potentially harmful attempts to access or exploit databases for the following services:

- [Azure Database for PostgreSQL](/en-us/azure/postgresql/)
- [Azure Database for MySQL](/en-us/azure/mysql/)

To get alerts from this Microsoft Defender plan, enable Defender for open-source relational databases in Azure.

Learn more about Microsoft Defender for open-source relational databases in [Overview of Microsoft Defender for open-source relational databases](defender-for-databases-introduction).

## Prerequisites

Before you enable Defender for open-source relational databases, make sure you meet the following requirements:

- An Azure subscription. If you don't have one, sign up for a [free Azure subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Microsoft Defender for Cloud enabled on your Azure subscription. For instructions, see [Enable Defender for Cloud](get-started#enable-defender-for-cloud-on-your-azure-subscription).
- (Optional) Connect your non-Azure machines. For more information, see [Onboard non-Azure machines](quickstart-onboard-machines).

## Enable Defender for open-source relational databases on your Azure subscription

To enable Defender for open-source relational databases on your Azure subscription:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Azure Database for MySQL servers** or **Azure Database for PostgreSQL servers**.
3. Select the relevant database server.
4. Expand the **Security** menu.
5. Select **Microsoft Defender for Cloud**.
6. If Defender for open-source relational databases isn't enabled, select **Enable Microsoft Defender for [Database type]**, for example, *Microsoft Defender for PostgreSQL*.

    [![Screenshot of the Microsoft Defender for open-source relational databases page with the Enable button highlighted.](media/enable-defender-for-databases-azure/enable-defender-open-source-relational-databases.png)](media/enable-defender-for-databases-azure/enable-defender-open-source-relational-databases.png#lightbox)

    Tip

    This page in the Azure portal is the same for PostgreSQL and MySQL.
7. Select **Save**.