---
layout: Conceptual
title: Troubleshoot Defender for SQL on Machines Deployment in Government Clouds - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/troubleshoot-sql-machines-guide-gov
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
description: Troubleshoot deployment issues for SQL Servers on machines using the Azure Monitoring Agent (AMA) autoprovisioning process.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: references_regions, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 6a90b967-8692-467c-b8cb-d55765c103f8
document_version_independent_id: 6cd27136-dbdb-b696-b235-1fafd3b7275c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/troubleshoot-sql-machines-guide-gov.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/troubleshoot-sql-machines-guide-gov
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/troubleshoot-sql-machines-guide-gov.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cbe4ca68-43ac-4375-aba5-5945a6394c20
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ced846cc-6a3c-4c8f-9dfb-3de0e90e2742
platformId: 15274799-3f66-7fe2-16d9-b72546efcf10
---

# Troubleshoot Defender for SQL on Machines Deployment in Government Clouds - Microsoft Defender for Cloud | Microsoft Learn

Important

This article applies to government clouds. If you're using commercial clouds, see the [Troubleshoot Defender for SQL on Machines deployment](troubleshoot-sql-machines-guide) article.

If you enable Defender for SQL Server on Machines and some SQL instances aren't in a protected state, use this article to troubleshoot deployment issues.

Before starting the troubleshooting steps, ensure that you have:

- Followed the steps to [enable Defender for SQL on Machines](defender-for-sql-usage-gov).
- Reviewed the [protection status of databases running on protected machines](verify-machine-protection-gov).

## Step 1: Understand how resources are created

Defender for SQL Servers on Machines automatically creates resources as shown in the diagram.

[![Diagram that shows resources and the levels that they're created on.](media/troubleshoot-sql-machines-guide-gov/resource-level.png)](media/troubleshoot-sql-machines-guide-gov/resource-level.png#lightbox)

Resources are summarized in the table:

| Resource type | Level created |
| --- | --- |
| **Resource group**. Created in East US Azure region. | Subscription level |
| **Managed identity**. A user-assigned managed identity is created in each Azure region. | Subscription level |
| **Log Analytics workspace**. Use the default or a custom workspace. | Subscription level |
| **Data collection rule (DCR)**. Created for each workspace. | Subscription level |
| **Data collection rule association (DCRA)** | Defined on each SQL Server instance |
| **Azure Monitoring Agent (AMA)** | The extension is installed on each SQL Server instance |
| **Defender for SQL extension** | The extension is installed on each SQL Server instance |

## Step 2: Make sure extensions are allowed

To ensure protection works as expected, make sure your organizational deny policy doesn't block these extensions:

- Defender for SQL (IaaS and Arc)

    - Publisher: Microsoft.Azure.AzureDefenderForSQL
    - Type: AdvancedThreatProtection.Windows
- SQL IaaS Extension (IaaS)

    - Publisher: Microsoft.SqlServer.Management
    - Type: SqlIaaSAgent
- SQL IaaS Extension (Arc)

    - Publisher: Microsoft.AzureData
    - Type: WindowsAgent.SqlServer
- AMA extension (IaaS and Arc)

    - Publisher: Microsoft.Azure.Monitor
    - Type: AzureMonitorWindowsAgent

## Step 3: Ensure East US region is allowed

When you enable the plan, Azure creates a resource group in the East US region. Ensure no deny policies block this region.

## Step 4: Verify resource naming conventions

Defender for SQL Server on Machines uses specific naming conventions for resources. Ensure your organization doesn't block these naming conventions and don't modify any automatically created resources.

- DCR: `MicrosoftDefenderForSQL--dcr`
- DCRA: `/Microsoft.Insights/MicrosoftDefenderForSQL-RulesAssociation`
- Resource group: `DefaultResourceGroup-`
- Log Analytics workspace: `D4SQL--`

Defender for SQL uses *MicrosoftDefenderForSQL* as a *createdBy* database tag.

## Step 5: Identify misconfigurations at subscription level

To identify which subscriptions have misconfigurations, use the [SQL Servers on Machines AMA Helper workbook](https://ms.portal.azure.com/#view/AppInsightsExtension/UsageNotebookBlade/ComponentId/Azure%20Security%20Center/ConfigurationId/community-Workbooks%2FAzure%20Security%20Center%2FSQL%20Servers%20on%20Machines%20AMA%20Helper/WorkbookTemplateName/SQL%20Servers%20on%20Machines%20AMA%20Helper).

1. Open the [SQL Servers on Machines AMA Helper workbook](https://ms.portal.azure.com/#view/AppInsightsExtension/UsageNotebookBlade/ComponentId/Azure%20Security%20Center/ConfigurationId/community-Workbooks%2FAzure%20Security%20Center%2FSQL%20Servers%20on%20Machines%20AMA%20Helper/WorkbookTemplateName/SQL%20Servers%20on%20Machines%20AMA%20Helper).

    [![Screenshot of the SQL Servers on Machines AMA Helper workbook main page.](media/troubleshoot-sql-machines-guide-gov/ama-helper-workbook.png)](media/troubleshoot-sql-machines-guide-gov/ama-helper-workbook.png#lightbox)
2. In **Subscriptions Overview** review misconfigurations at subscription level.

    - **SQL Servers on Azure Virtual Machines** shows subscriptions that contain Azure virtual machines (VMs).
    - **Arc-Enabled SQL Servers** shows subscriptions that contain Azure Arc-enabled VMs.

    Subscriptions appear on these tabs in accordance with your specific environment.

    [![Screenshot that shows where to navigate to on the SQL Servers on Azure Virtual Machines workbook page.](media/troubleshoot-sql-machines-guide-gov/navigate-sections.png)](media/troubleshoot-sql-machines-guide-gov/navigate-sections.png#lightbox)
3. Review component configurations for each subscription.

    - The number of SQL Server instances in the subscription.
    - Instances with the Defender for SQL extension installed.
    - Instances with the AMA extension installed.
    - DCRs created for each workspace in the subscription for all regions.
    - DCRAs created for each SQL instance.
    - Managed identity created for each region at the subscription level.
    - Log Analytics workspace created for each region at the subscription level.
    - AMA autoprovisioning enabled for the subscription.
    - Defender for SQL enabled for the subscription.
4. For each subscription, check which component doesn't match the expected configuration, such as 0/1, 10/15, or No. In our example screenshot, the Demo subscription has misconfigurations in DCRA 0/1.

    [![Screenshot of the SQL Servers on Machines AMA Helper workbook results.](media/troubleshoot-sql-machines-guide-gov/ama-helper-workbook-results.png)](media/troubleshoot-sql-machines-guide-gov/ama-helper-workbook-results.png#lightbox)

After you find a subscription with misconfigurations, resolve the misconfigurations first at the subscription level, then at the resource level and extension installation level.

## Step 6: Resolve misconfigurations at the subscription level

After you identify misconfigurations, start by fixing DCR issues, then workspace issues, and finally identity issues at the subscription level.

Fix misconfigurations in the correct order. DCR resolution relies on workspace resolution, and workspace resolution relies on identity resolution. If you try to resolve these misconfigurations out of order, the misconfigurations aren't resolved.

1. Navigate to **Policy** &gt; **Compliance**.
2. Select **Scope**.

    [![Screenshot that shows where to select scope on the policy and compliance page.](media/troubleshoot-sql-machines-guide-gov/scope.png)](media/troubleshoot-sql-machines-guide-gov/scope.png#lightbox)
3. In **Scope**, select the relevant subscription.
4. On the **Compliance** page, select the policy in accordance with your workspace configuration:

    - Default workspace: **Defender for SQL on SQL VMs and Arc-enabled SQL Servers**.
    - Custom workspace: **Defender for SQL on SQL VMs and Arc-enabled SQL Servers-custom**.

    [![Screenshot that shows where the misconfiguration is found on the page.](media/troubleshoot-sql-machines-guide-gov/select-misconfiguration.png)](media/troubleshoot-sql-machines-guide-gov/select-misconfiguration.png#lightbox)
5. Search for and resolve each noncompliant issue in this order **Identity** &gt; **Workspace** &gt; **DCR**.
6. Fix each issue as follows:

    - **Identity**. `Create and assign a built-in user-assigned managed identity`.
    - **Workspace**. `Configure the Microsoft Defender for SQL Log Analytics workspace`.
    - **DCR**. `Configure SQL Virtual Machines to automatically install Microsoft Defender for SQL and DCR with a Log Analytics workspace` or `Configure Arc-enabled SQL Servers to automatically install Microsoft Defender for SQL and DCR with a Log Analytics workspace`.
7. For each policy that is noncompliant, review the compliance reason and select **Create remediation task** to resolve it.

    [![Screenshot that shows where to create a remediation task on the page.](media/troubleshoot-sql-machines-guide-gov/remediation-task.png)](media/troubleshoot-sql-machines-guide-gov/remediation-task.png#lightbox)
8. Fill in the relevant information.
9. Select **Remediate**.
10. Repeat the remediation-task process for each noncompliant policy and subscription.

### Input custom values with PowerShell deployment script

If you couldn't resolve subscription issues with the workbook, Defender for SQL Servers on Machines provides a PowerShell deployment script that enables you to input your own values for workspace, DCR, and user Identity. To use the PowerShell script, follow the [instructions in Enable Defender for SQL at scale](enable-defender-sql-at-scale).

## Step 7: Resolve misconfigurations at the resource level

After resolving misconfigurations at the subscription level, resolve misconfigurations at the resource level, including DCRA misconfigurations and incomplete AMA or Defender for SQL extension deployment.

### Troubleshoot extension misconfigurations

Use the following steps to troubleshoot extension-related policy misconfigurations.

1. In the Azure portal, navigate to **Policy** &gt; **Compliance**.
2. Select **Scope**.
3. In the dropdown menu, select the subscription with misconfigurations.
4. Search for and select **Defender for SQL on SQL VMs and Arc-enabled SQL Servers initiative**.
5. Select the noncompliant policy name.

    - **Defender for SQL extension**. `Create and assign a built-in user-assigned managed identity`.
    - **AMA extension**. `Configure SQL Virtual Machines to automatically install Azure Monitor Agent` or `Configure Arc-enabled SQL Servers to automatically install Azure Monitor Agent`.
6. For each policy that is noncompliant, review the compliance reason and select **Create remediation task** to resolve it.

### Troubleshoot DCRA misconfigurations

Use the following steps to troubleshoot DCRA misconfigurations for the affected subscription.

1. In the Azure portal, search for and select **[Data collection rules](https://ms.portal.azure.com/#browse/microsoft.insights%2Fdatacollectionrules)**.
2. Select **Subscription equals**, then select the relevant subscription.

    [![Screenshot that shows where to select subscription equals.](media/troubleshoot-sql-machines-guide-gov/subscription-equals.png)](media/troubleshoot-sql-machines-guide-gov/subscription-equals.png#lightbox)
3. Select **Apply**.
4. Find and select the relevant DCR. The DCR naming convention follows this format: `MicrosoftDefenderForSQL-region-dcr`.
5. Select **Configuration** &gt; **Resources**.

    [![Screenshot that shows you where to select configuration and resources.](media/troubleshoot-sql-machines-guide-gov/resources.png)](media/troubleshoot-sql-machines-guide-gov/resources.png#lightbox)
6. Select **+ Add**.

    [![Screenshot that shows where the add button is located.](media/troubleshoot-sql-machines-guide-gov/add.png)](media/troubleshoot-sql-machines-guide-gov/add.png#lightbox)
7. In the **Resource types** dropdown table, select **Machines - Azure Arc** and **Virtual machines** in accordance with your deployment.

    [![Screenshot that shows where to filter by Machines Azure Arc and Virtual machines.](media/troubleshoot-sql-machines-guide-gov/resource-type-filter.png)](media/troubleshoot-sql-machines-guide-gov/resource-type-filter.png#lightbox)
8. Expand each resource group and select each machine.

    [![Screenshot that shows each machine selected individually.](media/troubleshoot-sql-machines-guide-gov/select-machines.png)](media/troubleshoot-sql-machines-guide-gov/select-machines.png#lightbox)
9. Select **Apply**.

## Step 8: Reverify protection status

After completing all the steps on this page, [reverify the protection status of each SQL Server instance](verify-machine-protection-gov).