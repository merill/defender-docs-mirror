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
ms.date: 2026-11-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1030
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
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ced846cc-6a3c-4c8f-9dfb-3de0e90e2742
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
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
- To configure an Arc-enabled server's local extension lists, you need an elevated PowerShell session on that server and the Azure Connected Machine agent.
- For the Azure VM policy example, install [Azure PowerShell](/en-us/powershell/azure/install-azure-powershell), including the `Az.Accounts`, `Az.Resources`, and `Az.Compute` modules.

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

Uninstalling the extension doesn't change the subscription-level Defender plan setting. The local extension lists described here apply only to Arc-enabled servers, not Azure VMs.

1. For an Arc-enabled server, add the extension to the local block list before uninstalling it. Alternatively, remove the extension from an existing allow list, keeping at least one other entry.

    Blocking installation doesn't remove an installed extension. Complete the uninstall steps after you configure the restriction.
2. For an Azure VM, assign a policy that blocks the extension on that VM before uninstalling it.
3. In the [Azure portal](https://portal.azure.com/), go to one of the following options:

    - **Azure Arc** &gt; **Data services** &gt; **SQL Server instances**
    - **SQL virtual machines**
4. Select the relevant SQL Server instance.
5. Locate the security menu and select **Extensions + applications**.

    [![Screenshot that shows where to locate Defender for Cloud under the security section.](media/disable-sql-on-machines/extension-application.png)](media/disable-sql-on-machines/extension-application.png#lightbox)
6. Select the **Defender for SQL (IaaS and Arc)** extension.

    Confirm that the extension details match the following values:

    - Extension: Defender for SQL (IaaS and Arc)
    - Publisher: Microsoft.Azure.AzureDefenderForSQL
    - Type: AdvancedThreatProtection.Windows
7. Select **Uninstall**.

### Block installation locally on an Arc-enabled server

Use the Azure Connected Machine agent's local extension block list to prevent reinstallation on a specific server. Run these commands in an elevated PowerShell session on the Arc-enabled Windows server. These are `azcmagent` commands invoked from PowerShell, not Az PowerShell cmdlets.

1. Add the Defender for SQL extension to the block list. The `--add` flag preserves existing entries.

    ```powershell
    $AgentPath = "$env:ProgramFiles\AzureConnectedMachineAgent\azcmagent.exe"
    & $AgentPath config set extensions.blocklist `
        "Microsoft.Azure.AzureDefenderForSQL/AdvancedThreatProtection.Windows" --add
    if ($LASTEXITCODE -ne 0) { throw "Couldn't add the Defender for SQL extension to the block list." }
    ```
2. Check that the block list includes `Microsoft.Azure.AzureDefenderForSQL/AdvancedThreatProtection.Windows`:

    ```powershell
    & $AgentPath config get extensions.blocklist
    ```
3. Return to the resource-level uninstall procedure and remove the extension. The block list doesn't uninstall an existing extension.

If you manage an existing extension allow list instead, remove the Defender for SQL entry while retaining all other required entries. Don't clear the allow list or leave it empty as a way to block this extension: when neither list restricts installation, all extensions are allowed. The block list takes precedence if the extension remains in both lists.

In agent monitor mode, you can't edit the local allow list or block list.

For details, see [Arc extension allow lists and block lists](/en-us/azure/azure-arc/servers/security-extensions#allow-lists-and-block-lists) and [azcmagent configuration commands](/en-us/azure/azure-arc/servers/azcmagent-config#azcmagent-config-set).

### Block installation on an Azure VM

Use Azure PowerShell to create a deny policy and assign it to the individual VM you want to exclude. The policy blocks only the Defender for SQL extension, identified by its publisher and type. It doesn't change restrictions on other extensions.

The policy doesn't change the subscription-level Defender plan setting or turn off automatic provisioning. Installation attempts that match the policy are denied.

1. Sign in and select the subscription that contains the VM:

    ```powershell
    Connect-AzAccount
    Set-AzContext -SubscriptionId "<subscription-id>" -ErrorAction Stop
    ```
2. Create a policy definition that blocks the Defender for SQL extension on Azure VMs. The definition doesn't enforce the restriction until you assign it.

    ```powershell
    $PolicyRule = @'
    {
      "if": {
        "allOf": [
          { "field": "type", "equals": "Microsoft.Compute/virtualMachines/extensions" },
          { "field": "Microsoft.Compute/virtualMachines/extensions/publisher", "equals": "Microsoft.Azure.AzureDefenderForSQL" },
          { "field": "Microsoft.Compute/virtualMachines/extensions/type", "equals": "AdvancedThreatProtection.Windows" }
        ]
      },
      "then": {
        "effect": "deny"
      }
    }
    '@
    
    $Definition = New-AzPolicyDefinition `
        -Name "block-defender-sql-vm-extension" `
        -DisplayName "Block Defender for SQL extension installation on Azure VMs" `
        -Policy $PolicyRule `
        -Mode All `
        -ErrorAction Stop
    ```
3. Get the VM and assign the policy to its resource ID. Using the VM's ID limits the assignment to that VM, rather than its resource group or subscription.

    ```powershell
    $VM = Get-AzVM `
        -ResourceGroupName "<resource-group>" `
        -Name "<vm-name>" `
        -ErrorAction Stop
    
    $Assignment = New-AzPolicyAssignment `
        -Name "block-defender-sql" `
        -Scope $VM.Id `
        -PolicyDefinition $Definition `
        -EnforcementMode Default `
        -ErrorAction Stop
    ```
4. Check that the assignment targets the intended VM and that its enforcement mode is `Default`:

    ```powershell
    $Assignment | Select-Object Name, Scope, EnforcementMode
    ```

    Allow time for the assignment to take effect before uninstalling the extension. A new assignment takes about five minutes to apply to its scope. For details, see [Azure Policy evaluation triggers](/en-us/azure/governance/policy/how-to/get-compliance-data#evaluation-triggers).
5. Return to the resource-level uninstall procedure and remove the extension. Keep the assignment in place to block reinstallation. Remove the assignment before you enable protection again on that VM.

For details, see [New-AzPolicyDefinition](/en-us/powershell/module/az.resources/new-azpolicydefinition), [New-AzPolicyAssignment](/en-us/powershell/module/az.resources/new-azpolicyassignment), and [restricting VM extension installation](/en-us/azure/virtual-machines/extensions/extensions-rmpolicy-howto-ps).