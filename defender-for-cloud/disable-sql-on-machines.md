---
layout: Conceptual
title: Disable Defender for SQL Servers on Machines - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/disable-sql-on-machines
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
description: Disable the Defender for SQL Servers on Machines plan to stop SQL alerts and recommendations for selected scopes in Microsoft Defender for Cloud.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: d36464e2-3e1c-5517-c916-f1e0a083ca85
document_version_independent_id: f8dd803b-d910-e54a-f1c0-01d10d387b65
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/disable-sql-on-machines.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/disable-sql-on-machines
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/disable-sql-on-machines.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cbe4ca68-43ac-4375-aba5-5945a6394c20
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ced846cc-6a3c-4c8f-9dfb-3de0e90e2742
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 66a4c739-ee1c-90bd-6c00-5f9e5c58406d
---

# Disable Defender for SQL Servers on Machines - Microsoft Defender for Cloud | Microsoft Learn

Use this article to disable Defender for SQL Servers on Machines in Microsoft Defender for Cloud.

The Defender for SQL Servers on Machines plan is part of Defender for Databases. It protects SQL Server databases hosted on Azure virtual machines (VMs) and Azure Arc-enabled VMs.

## What happens when you disable this plan

When you disable the plan, Defender for Cloud stops providing SQL alerts and recommendations for the selected machines.

## Prerequisites

- You must have **Subscription Owner** permissions.
- You must have the Defender for SQL Servers on Machines plan enabled in your Defender for Cloud environment.

## Disable Defender for SQL Servers on Machines

To disable Defender for SQL Servers on Machines, follow these steps:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select the relevant subscription.
4. On **Defender plans**, find the Databases plan and select **Select types**.

    [![Screenshot that shows you where to select types on the Defender plans page.](media/disable-sql-on-machines/select-types.png)](media/disable-sql-on-machines/select-types.png#lightbox)
5. In **Resource types selection**, set the **SQL Servers on Machines** plan to **Off**.

    [![Screenshot that shows where the Off button is located for SQL servers on machines.](media/disable-sql-on-machines/sql-servers-off.png)](media/disable-sql-on-machines/sql-servers-off.png#lightbox)
6. Select **Continue** &gt; **Save**.

## Disable Defender for SQL Servers on Machines at the resource level

To disable Defender for SQL Servers on Machines at the resource level for an individual SQL Server instance or SQL virtual machine, follow these steps:

1. In the [Azure portal](https://portal.azure.com/), go to one of the following options:

    - **Azure Arc** &gt; **Data services** &gt; **SQL Server instances**
    - **SQL virtual machines**
2. Select the relevant SQL Server instance.
3. Locate the security menu and select **Extensions + applications**.

    [![Screenshot that shows where to locate Defender for Cloud under the security section.](media/disable-sql-on-machines/extension-application.png)](media/disable-sql-on-machines/extension-application.png#lightbox)
4. Select the **Defender for SQL (IaaS and Arc)** extension.

    Confirm that the extension details match the following values:

    - Extension: Defender for SQL (IaaS and Arc)
    - Publisher: Microsoft.Azure.AzureDefenderForSQL
    - Type: AdvancedThreatProtection.Windows
5. Select **Uninstall**.