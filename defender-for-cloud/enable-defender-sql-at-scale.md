---
layout: Conceptual
title: Enable Microsoft Defender for SQL Servers on Machines at Scale - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/enable-defender-sql-at-scale
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
description: Enable Defender for SQL Servers on Machines across multiple subscriptions by using PowerShell, including auto-provisioning and custom configuration options.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 019eb4df-77a8-0482-5af5-1415b007025c
document_version_independent_id: 70f5d260-da78-68a8-c65e-74f08771b8cd
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/enable-defender-sql-at-scale.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/enable-defender-sql-at-scale
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/enable-defender-sql-at-scale.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cbe4ca68-43ac-4375-aba5-5945a6394c20
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/5cf46315-b33f-4e99-8224-a1592697eff9
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ced846cc-6a3c-4c8f-9dfb-3de0e90e2742
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/715d24c3-3683-4219-82c5-1e3c813fb7fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 060ba674-1f2b-52e7-d8e1-4d1a6b1a9ab7
---

# Enable Microsoft Defender for SQL Servers on Machines at Scale - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud's SQL Servers on Machines component of the Defender for Databases plan protects SQL IaaS and Defender for SQL extensions. This component identifies and mitigates potential database vulnerabilities and detects anomalous activity that could indicate threats to your databases.

When you enable the SQL Servers on Machines component of the Defender for Databases plan, auto-provisioning starts. Auto-provisioning installs and configures the required components, including the Azure Monitor Agent (AMA), SQL IaaS extension, and Defender for SQL extensions. It also configures the workspace, Data Collection Rules (DCRs), and identity when needed.

This article explains how to enable auto-provisioning for Defender for SQL across multiple subscriptions by using a PowerShell script. This auto-provisioning procedure applies to SQL servers hosted on Azure Virtual Machines (VMs), on-premises environments, and Azure Arc-enabled SQL servers. It also covers optional configurations such as:

- Custom data collection rules
- Custom identity management
- Default workspace integration
- Custom workspace configuration

## Prerequisites

Before you begin:

- Review [SQL Server on Azure VMs](https://azure.microsoft.com/products/virtual-machines/sql-server/), [SQL Server enabled by Azure Arc](/en-us/sql/sql-server/azure-arc/overview), and [how to migrate to Azure Monitor Agent from Log Analytics agent](/en-us/azure/azure-monitor/agents/azure-monitor-agent-migration).
- Connect [Amazon Web Services (AWS) accounts to Microsoft Defender for Cloud](quickstart-onboard-aws).
- Connect [Google Cloud Platform (GCP) to Microsoft Defender for Cloud](quickstart-onboard-gcp).
- Install PowerShell for your platform: [Install PowerShell on Windows](/en-us/powershell/scripting/install/installing-powershell-on-windows), [Install PowerShell on Linux](/en-us/powershell/scripting/install/installing-powershell-on-linux), [Install PowerShell on macOS](/en-us/powershell/scripting/install/installing-powershell-on-macos), or [Install PowerShell on ARM](/en-us/powershell/scripting/install/powershell-on-arm).
- Install these PowerShell modules. For installation instructions, see the [Install-Module cmdlet reference](/en-us/powershell/module/powershellget/install-module):

    - `Az.Resources`
    - `Az.OperationalInsights`
    - `Az.Accounts`
    - `Az`
    - `Az.PolicyInsights`
    - `Az.Security`
- Have **Virtual Machine Contributor**, **Contributor**, or **Owner** permissions.

## PowerShell script parameters and samples

The PowerShell script that enables Microsoft Defender for SQL on Machines on a given Azure subscription has several parameters that you can customize to fit your needs. The following table lists the parameters and their descriptions:

| Parameter name | Required | Description |
| --- | --- | --- |
| `SubscriptionId` | Required | The Azure subscription ID that you want to enable Defender for SQL Servers on Machines for. |
| `RegisterSqlVmAgnet` | Required | A value that indicates whether to register the SQL VM Agent in bulk. This parameter name matches the current upstream script.  You can register multiple SQL VMs in Azure with the SQL IaaS Agent extension in bulk. For details, see [Register multiple SQL VMs with SQL IaaS Agent extension](/en-us/azure/azure-sql/virtual-machines/windows/sql-agent-extension-manually-register-vms-bulk). |
| `WorkspaceResourceId` | Optional | The resource ID of the Log Analytics workspace, if you want to use a custom workspace instead of the default one. |
| `DataCollectionRuleResourceId` | Optional | The resource ID of the data collection rule, if you want to use a custom Data Collection Rule (DCR) instead of the default one. |
| `UserAssignedIdentityResourceId` | Optional | The resource ID of the user assigned identity, if you want to use a custom user assigned identity instead of the default one. |

The following example enables Defender for SQL on Machines with bulk SQL VM Agent registration (`RegisterSqlVmAgnet = $true`) and uses the default Log Analytics workspace, data collection rule, and managed identity.

```powershell
Write-Host "------ Enable Defender for SQL on Machines example ------" 
$SubscriptionId = "<SubscriptionID>"
$RegisterSqlVmAgnet = $true
.\EnableDefenderForSqlOnMachines.ps1 -SubscriptionId $SubscriptionId -RegisterSqlVmAgnet $RegisterSqlVmAgnet 
```

The following example enables Defender for SQL on Machines without bulk SQL VM Agent registration (`RegisterSqlVmAgnet = $false`) and specifies a custom Log Analytics workspace, data collection rule, and managed identity.

```powershell
Write-Host "------ Enable Defender for SQL on Machines example ------" 
$SubscriptionId = "<SubscriptionID>" 
$RegisterSqlVmAgnet = $false 
$WorkspaceResourceId = "/subscriptions/<SubscriptionID>/resourceGroups/someResourceGroup/providers/Microsoft.OperationalInsights/workspaces/someWorkspace" 
$DataCollectionRuleResourceId = "/subscriptions/<SubscriptionID>/resourceGroups/someOtherResourceGroup/providers/Microsoft.Insights/dataCollectionRules/someDcr" 
$UserAssignedIdentityResourceId = "/subscriptions/<SubscriptionID>/resourceGroups/someElseResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/someManagedIdentity" 
.\EnableDefenderForSqlOnMachines.ps1 -SubscriptionId $SubscriptionId -RegisterSqlVmAgnet $RegisterSqlVmAgnet -WorkspaceResourceId $WorkspaceResourceId -DataCollectionRuleResourceId $DataCollectionRuleResourceId -UserAssignedIdentityResourceId $UserAssignedIdentityResourceId
```

## Enable Defender for SQL Servers on Machines at scale

To enable Defender for SQL Servers on Machines at scale:

1. Open a PowerShell window.
2. Copy the **EnableDefenderForSqlOnMachines.ps1** script from the [Defender for Cloud GitHub repository](https://github.com/Azure/Microsoft-Defender-for-Cloud/blob/fd04330a79a4bcd48424bf7a4058f44216bc40e4/Powershell%20scripts/Enable%20Defender%20for%20SQL%20servers%20on%20machines/EnableDefenderForSqlOnMachines.ps1).
3. Paste the script into PowerShell.
4. Enter parameter information as needed.
5. Run the script.