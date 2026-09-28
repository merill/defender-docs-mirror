---
layout: Conceptual
title: Update Defender for SQL Servers on Machines Configuration for Automatic Registration - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/update-sql-machine-configuration
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
description: Learn how to update the Defender for SQL Servers on Machines configuration to enable automatic registration for Azure VMs, on-premises, and hybrid environments.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 96afff7c-cc48-1157-58e1-049057b012f3
document_version_independent_id: 41bafd37-8ab7-e5cc-ea49-ed991cfd2d94
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/update-sql-machine-configuration.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/update-sql-machine-configuration
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/update-sql-machine-configuration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cbe4ca68-43ac-4375-aba5-5945a6394c20
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ced846cc-6a3c-4c8f-9dfb-3de0e90e2742
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: fa51a8bc-08ed-00fb-aadc-fd89c728900e
---

# Update Defender for SQL Servers on Machines Configuration for Automatic Registration - Microsoft Defender for Cloud | Microsoft Learn

Important

This article applies to existing customers who enabled the plan on a subscription before April 21, 2025.

The Defender for SQL Servers on Machines plan includes an updated agent architecture that simplifies onboarding and improves SQL protection. To gain visibility and provide protection, the plan requires each SQL server instance to be registered within Azure.

Registration occurs automatically with the SQL Server IaaS Agent extension, which [automates registration for Azure VMs](/en-us/azure/azure-sql/virtual-machines/windows/sql-server-iaas-agent-extension-automate-management?tabs=azure-portal). Arc-enabled SQL Server instances are [automatically connected by the Azure extension for SQL Servers](/en-us/sql/sql-server/azure-arc/manage-autodeploy).

If automatic registration is disabled, manually register each SQL server instance to protect it with the Defender for SQL Server on Machines plan.

Existing customers must follow these steps to update the Defender for SQL Servers on Machines configuration to enable auto-registration through the SQL extension.

Important

The Defender for SQL servers on Machines plan is undergoing a transition to the new agent architecture. For more information, see [Defender for SQL servers on Machines plan transition](release-notes-archive#update-to-defender-for-sql-servers-on-machines-plan).

## Update the plan on multiple subscriptions

To update the plan configuration for multiple subscriptions at once, follow these steps:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Search for and select **Microsoft Defender for Cloud**.
3. On the **Overview** page, select **[Update the configuration in Defender for SQL Servers on Machines plan for multiple subscriptions](https://portal.azure.com/#view/Microsoft_Azure_Security_AzureDefenderForData/vNextUpgradeContextBlade)**.
4. Select all the relevant subscriptions.
5. Select **Update**.

## Update the plan on a single subscription

To update the plan configuration for a single subscription, follow these steps:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Search for and select **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select the relevant subscription.
4. Locate the Defender for Databases plan and select **Settings**.
5. Select **Update** in the pop-up window.

    [![Screenshot that shows where to locate the update button.](media/update-sql-machine-configuration/update-notification.png)](media/update-sql-machine-configuration/update-notification.png#lightbox)