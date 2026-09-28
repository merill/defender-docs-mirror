---
layout: Conceptual
title: Enable Microsoft Defender for SQL Servers on Machines government - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-sql-usage-gov
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
description: Learn how to protect your Microsoft SQL Servers on Azure VMs, on government clouds with Microsoft Defender for Cloud.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: eee3db52-8095-3582-b3bb-ab968c69433e
document_version_independent_id: c2bcc152-4461-2a87-987c-daa735dbe2c3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-sql-usage-gov.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-sql-usage-gov
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-sql-usage-gov.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cbe4ca68-43ac-4375-aba5-5945a6394c20
- https://authoring-docs-microsoft.poolparty.biz/devrel/beac614b-f66d-40ed-a947-3996de709333
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ced846cc-6a3c-4c8f-9dfb-3de0e90e2742
- https://authoring-docs-microsoft.poolparty.biz/devrel/9da05372-4706-43ec-a899-f436adab380d
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 41cb21a2-cce2-5ffd-8d96-bc3e9a56ec40
---

# Enable Microsoft Defender for SQL Servers on Machines government - Microsoft Defender for Cloud | Microsoft Learn

Important

This article applies to government clouds. If you're using commercial clouds, see the [Enable Defender for SQL servers on Machines](defender-for-sql-usage) article.

The Defender for SQL Servers on Machines plan is one of the Defender for Databases plans in Microsoft Defender for Cloud. Use Defender for SQL Servers on Machines to protect SQL Server databases hosted on Azure VMs and Azure Arc-enabled VMs.

## Prerequisites

| Requirement | Details |
| --- | --- |
| **Permissions** | To deploy the plan on a subscription including Azure Policy, you need **Subscription Owner** permissions.  The Windows user on the SQL VM must have the **Sysadmin** role on the database. |
| **Multicloud machines** | Multicloud machines (AWS and GCP) must be onboarded as Azure Arc-enabled VMs. They can be automatically onboarded as Azure Arc machines when onboarded with the connector. [Onboard your AWS connector](quickstart-onboard-aws) and automatically provision Azure Arc. [Onboard your GCP connector](quickstart-onboard-gcp) and automatically provision Azure Arc. |
| **On-premises machines** | On-premises machines must be onboarded as Azure Arc-enabled VMs. [Onboard on-premises machines and install Azure Arc](/en-us/azure/azure-arc/servers/learn/quick-enable-hybrid-vm). |
| **Azure Arc** | Review Azure Arc deployment requirements  - [Plan and deploy Azure Arc-enabled servers](/en-us/azure/azure-arc/servers/plan-at-scale-deployment) - [Connected Machine agent prerequisites](/en-us/azure/azure-arc/servers/prerequisites) - [Connected Machine agent network requirements](/en-us/azure/azure-arc/servers/network-requirements) - [Roles specific to SQL Server enabled by Azure Arc](/en-us/sql/relational-databases/security/authentication-access/server-level-roles#roles-specific-to-sql-server-enabled-by-azure-arc) |
| **Extensions** | Ensure these extensions aren't blocked in your environment. |
| Defender for SQL (IaaS and Arc) | - Publisher: Microsoft.Azure.AzureDefenderForSQL - Type: AdvancedThreatProtection.Windows |
| SQL IaaS Extension (IaaS) | - Publisher: Microsoft.SqlServer.Management - Type: SqlIaaSAgent |
| SQL IaaS Extension (Arc) | - Publisher: Microsoft.AzureData - Type: WindowsAgent.SqlServer |
| AMA extension (IaaS and Arc) | - Publisher: Microsoft.Azure.Monitor - Type: AzureMonitorWindowsAgent |
| **Region requirement** | When you enable the plan, a resource group is created in the East US. Ensure East US isn't blocked in your environment. |
| **Resource naming conventions** | Defender for SQL uses the following naming convention when creating our resources:  - Data Collection Rule: `MicrosoftDefenderForSQL--dcr` - DCRA: `/Microsoft.Insights/MicrosoftDefenderForSQL-RulesAssociation` - Resource group: `DefaultResourceGroup-` - Log analytics workspace: `D4SQL--` - Defender for SQL uses *MicrosoftDefenderForSQL* as a *createdBy* database tag.  Ensure that Deny policies don't block the Defender for SQL resource naming convention listed above. |
| **Supported SQL Server Versions** | SQL Server 2012 or later is supported for SQL instances. |
| **Supported Operating Systems** | Windows Server 2012 R2 or later. |

## Enable Defender for SQL Servers on Machines

1. In the Azure portal, search for and select **Microsoft Defender for Cloud**.
2. In the Defender for Cloud menu, select **Environment settings**.
3. Select the relevant subscription.
4. On the Defender plans page, locate the Databases plan and select **Select types**.

    [![Screenshot that shows you where to select types on the Defender plans page.](media/tutorial-enabledatabases-plan/select-types.png)](media/tutorial-enabledatabases-plan/select-types.png#lightbox)
5. In the Resource types selection window, toggle the **SQL Servers on Machines** plan to **On**.
6. Select **Continue** &gt; **Save**.

## Select a Log Analytics workspace

Select a Log Analytics workspace to work with the Defender for SQL on Machines plan.

1. In the **Defender plans** page, in **Databases**, **Monitoring Coverage** column select **Settings**.
2. In the **Azure Monitoring Agent for SQL Server on Machines** section, in the **Configurations** column select **Edit Configurations**.
3. In the **Autoprovisioning Configuration** page, select the **Default Workspace** or specify a **Custom Workspace**.
4. In SQL Server automatic registration, make sure that you leave the **Register Azure SQL Server instances by enabling SQL IaaS extension automatic registration** option enabled.

    [![Screenshot that shows where to leave the register Azure SQL Server instances enabled.](media/defender-for-sql-usage-gov/leave-enabled.png)](media/defender-for-sql-usage-gov/leave-enabled.png#lightbox)

    Registration ensures that all SQL instances can be discovered and configured correctly.
5. Select **Apply**.

## Verify that your machines are protected

Important

Don't skip this step. Verification confirms that your deployment is protected.

Depending on your environment, it can take a few hours to discover and protect SQL instances.

As a required final step, [verify that all machines are protected](verify-machine-protection-gov). Verification confirms that the deployment completed and that your SQL instances are protected.