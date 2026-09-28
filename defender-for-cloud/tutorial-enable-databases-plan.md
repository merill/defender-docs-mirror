---
layout: Conceptual
title: Protect your Databases with Defender for Databases - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/tutorial-enable-databases-plan
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
description: Learn how to enable the Databases plan on your Azure subscription for Microsoft Defender for Cloud to enhance your database security.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: d1ddbc4c-49ce-2228-4976-2c11e6e2f7a8
document_version_independent_id: 6b1f4988-2f71-4527-ad4d-8f48169a0325
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/tutorial-enable-databases-plan.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/tutorial-enable-databases-plan
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/tutorial-enable-databases-plan.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: a0be4ebd-f983-5a53-2ba6-1198c0993a73
---

# Protect your Databases with Defender for Databases - Microsoft Defender for Cloud | Microsoft Learn

Defender for Databases in Microsoft Defender for Cloud helps you protect your entire database estate. It provides attack detection and threat response for the most popular database types in Azure. Defender for Cloud protects database engines and data types based on their attack surface and security risks.

Defender for Databases includes four offerings that relate to database types:

- [Microsoft Defender for Azure SQL Databases](defender-for-sql-introduction): Offers threat protection for Azure SQL databases by detecting and responding to potential security threats.
- [Microsoft Defender for SQL Servers on Machines](defender-for-sql-usage): Offers security for SQL servers that run on virtual machines or physical servers. You can also [enable it on a Log Analytics workspace](enable-plan-workspace) for enhanced monitoring and threat detection.
- [Microsoft Defender for Open-Source Relational Databases](defender-for-databases-introduction): Offers security for open-source relational databases such as PostgreSQL and MySQL by providing continuous monitoring and threat detection.
- [Microsoft Defender for Azure Cosmos DB](concept-defender-for-cosmos): Offers security for Azure Cosmos DB by providing threat protection and real-time alerts to help safeguard your data.

Each of these database protection plans is priced separately. For more information, see the [Defender for Cloud pricing page](https://azure.microsoft.com/pricing/details/defender-for-cloud/). You can also [estimate costs with the Defender for Cloud cost calculator](cost-calculator).

## Prerequisites

- You need a Microsoft Azure subscription. If you don't have an Azure subscription, [sign up for a free subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- You must [enable Microsoft Defender for Cloud](get-started#enable-defender-for-cloud-on-your-azure-subscription) on your Azure subscription.
- Connect your [non-Azure machines](quickstart-onboard-machines), [Amazon Web Service (AWS) account](quickstart-onboard-aws), or [Google Cloud Platform (GCP) projects](quickstart-onboard-gcp).

## Enable the Databases plan

Enabling database protection activates all four Defender plans and protects all supported databases on your subscription.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Microsoft Defender for Cloud**.
3. In the **Defender for Cloud** menu, select **Environment settings**.
4. Select the relevant Azure subscription, AWS account, or GCP project.
5. On the Defender plans page, switch the Databases plan to **On**.

    [![Screenshot that shows you where to select, to enable the databases plan.](media/tutorial-enabledatabases-plan/enable-databases.png)](media/tutorial-enabledatabases-plan/enable-databases.png#lightbox)

## Enable and modify specific database plans

Enabling database protection activates the following four Defender plans:

- [Enable Defender for Azure SQL Databases](enable-sql-database-plan)
- [Enable Defender for SQL Servers on Machines](defender-for-sql-usage) (You can also [enable on a Log Analytics workspace](enable-plan-workspace))
- [Enable Defender for open-source relational databases on Azure](enable-defender-for-databases-azure)
- [Enable Defender for Azure Cosmos DB](defender-for-databases-enable-cosmos-protections)

These plans protect all supported databases in your subscription.

## View your current coverage

Defender for Cloud provides access to [Defender for Cloud workbooks](custom-dashboards-azure-workbooks) through [Azure workbooks](/en-us/azure/azure-monitor/visualize/workbooks-overview). Workbooks are customizable reports that provide insights into your security posture.

The [Defender for Cloud coverage workbook](custom-dashboards-azure-workbooks#coverage-workbook) helps you understand your current coverage by showing which plans are enabled on your subscriptions and resources.