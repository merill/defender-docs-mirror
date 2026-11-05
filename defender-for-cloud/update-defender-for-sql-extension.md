---
layout: Conceptual
title: Update the Defender for SQL extension manually - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/update-defender-for-sql-extension
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
description: Update the Defender for SQL extension on Azure Arc-enabled servers and Azure virtual machines by using the Azure portal, scripts, or REST APIs.
ms.topic: how-to
ms.date: 2026-11-05T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1030
ai-usage: ai-generated
locale: en-us
document_id: 05bb7234-973b-5b8f-e47b-993d604f3749
document_version_independent_id: e6ea93ff-1826-c16e-34ad-f95d992f92f4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/update-defender-for-sql-extension.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/update-defender-for-sql-extension
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/update-defender-for-sql-extension.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cbe4ca68-43ac-4375-aba5-5945a6394c20
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ced846cc-6a3c-4c8f-9dfb-3de0e90e2742
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 29ff9101-48d0-4939-300f-682abb0c5f92
---

# Update the Defender for SQL extension manually - Microsoft Defender for Cloud | Microsoft Learn

Update the Defender for SQL extension on an Azure Arc-enabled server or Azure virtual machine (VM) to the latest version available in the machine's Azure region. Choose the Azure portal procedure or the scripted procedure for your machine type, then verify the installed version and SQL Server protection status.

These procedures target the extension with publisher `Microsoft.Azure.AzureDefenderForSQL` and type `AdvancedThreatProtection.Windows`. They don't update the SQL IaaS extension or the Azure Connected Machine agent.

## Update by using the Azure portal

Use the portal to inspect the installed extension and update to the latest offered version where an update action is available.

### Update an Arc-enabled server

1. In the Azure portal, open **Machines - Azure Arc**, and select the server that hosts SQL Server.
2. Under **Settings**, select **Extensions**.
3. Find the Defender for SQL extension by its publisher and type.
4. Check **Update available** for the latest offered version.
5. If an update is available, select the extension, and then select **Update**.
6. Refresh the extension details and verify the resulting version and status.

The [Arc portal upgrade procedure](/en-us/azure/azure-arc/servers/manage-vm-extensions-portal#upgrade-extensions) documents this update action. An Arc extension upgrade preserves its configuration.

### Inspect and update an Azure VM

1. In the Azure portal, open **Virtual machines**, and select the VM that hosts SQL Server.
2. Under **Settings**, select **Extensions + applications**.
3. Select the Defender for SQL extension and review its version and status.
4. If an extension update action is available, use it to start the update. Otherwise, use the Azure VM CLI example.
5. Refresh the extension details and verify the resulting version and status.

The [Defender for SQL troubleshooting guidance](/en-us/azure/defender-for-cloud/troubleshoot-sql-machines-guide#step-3-identify-and-resolve-protection-misconfigurations-at-the-sql-server-instance-level) directs customers to update outdated extensions from the machine's extensions page.

## Update programmatically

Use Azure CLI to update the extension on an Arc-enabled server or Azure VM.

### Prerequisites

- An Azure Arc-enabled Windows server or Azure Windows VM with the Defender for SQL extension already installed. For initial setup, see [Enable Defender for SQL Servers on Machines](/en-us/azure/defender-for-cloud/defender-for-sql-usage).
- Permission to read the machine and its extensions and perform the relevant update operation. For Arc-enabled servers, **Azure Connected Machine Resource Administrator** includes the extension upgrade permission. For Azure VMs, **Virtual Machine Contributor** includes extension management permissions. Scope permissions to the resources you manage, or use a custom role with the necessary actions. See the [Arc role definition](/en-us/azure/role-based-access-control/built-in-roles/management-and-governance#azure-connected-machine-resource-administrator) and [VM role definition](/en-us/azure/role-based-access-control/built-in-roles/compute#virtual-machine-contributor).
- The network and extension deployment requirements in [Defender for SQL prerequisites](/en-us/azure/defender-for-cloud/defender-for-sql-usage#prerequisites).
- For the scripted procedures, PowerShell 7 and the [Azure CLI](/en-us/cli/azure/install-azure-cli).
- For the Arc procedure, Azure CLI version 2.75.0 or later and the `connectedmachine` CLI extension.
- Before either CLI procedure, sign in with `az login` and select the subscription with `az account set --subscription "<subscription-id>"`.

### Update an Arc-enabled server by using Azure CLI

Run these commands in PowerShell for the Arc-enabled machine that hosts SQL Server. Replace the placeholders with your resource details. The update and verification examples use the extension resource name `MicrosoftDefenderForSQL`. If your installed extension has a different resource name, use that name instead.

1. Update to the latest available version. This command enables minor-version selection at deployment and leaves future automatic upgrades enabled. The output includes the extension's status.

    ```powershell
    az connectedmachine extension update `
      --resource-group "<resource-group>" `
      --machine-name "<arc-machine-name>" `
      --name "MicrosoftDefenderForSQL" `
      --publisher "Microsoft.Azure.AzureDefenderForSQL" `
      --type "AdvancedThreatProtection.Windows" `
      --auto-upgrade-minor-version true `
      --enable-auto-upgrade true
    ```
2. Verify the version and status if needed, or run this command later to check again. Confirm that the provisioning state is `Succeeded` and review the installed runtime version.

    ```powershell
    az connectedmachine extension show `
        --resource-group "<resource-group>" `
        --machine-name "<arc-machine-name>" `
        --name "MicrosoftDefenderForSQL" `
        --output json
    ```

For command details, see [Update an Arc machine extension](/en-us/cli/azure/connectedmachine/extension#az-connectedmachine-extension-update) and [Show an Arc machine extension](/en-us/cli/azure/connectedmachine/extension#az-connectedmachine-extension-show). For future automatic updates, see [Automatic extension upgrade for Azure Arc-enabled servers](/en-us/azure/azure-arc/servers/manage-automatic-vm-extension-upgrade).

### Update an Azure VM by using Azure CLI

Run these commands in PowerShell to update the existing Defender for SQL extension. Replace the placeholders with your resource details.

Important

The Azure VM command requests the `2.0` handler series, not a specific four-part build. Azure delivers the latest available patch/hotfix in that series.

For the Arc proxy scenario, the required installed Defender for SQL build is `2.0.3585.403` or later. Requesting a handler series alone doesn't prove that the installed build meets this requirement.

1. Update to the latest available version in the handler series. The command leaves future automatic upgrades enabled and returns the extension's status. `--force-update` requests an update even if the configuration hasn't changed.

    ```powershell
    az vm extension set `
        --resource-group "<resource-group>" `
        --vm-name "<vm-name>" `
        --publisher "Microsoft.Azure.AzureDefenderForSQL" `
        --name "AdvancedThreatProtection.Windows" `
        --version "2.0" `
        --enable-auto-upgrade true `
        --force-update
    ```
2. Verify the version and status if needed, or run this command later to check again. Retrieve the extension's instance view, confirm that provisioning succeeded, and review the installed runtime version and any failure details.

    ```powershell
    az vm extension show `
        --resource-group "<resource-group>" `
        --vm-name "<vm-name>" `
        --name "AdvancedThreatProtection.Windows" `
        --instance-view `
        --output json
    ```

For command details, see [Set a VM extension](/en-us/cli/azure/vm/extension#az-vm-extension-set) and [Show a VM extension](/en-us/cli/azure/vm/extension#az-vm-extension-show).

## Verify the update and SQL Server protection

Check the installed runtime version, not only the requested handler version.

For Arc, inspect `properties.instanceView.typeHandlerVersion` in the REST representation, or the equivalent field returned by your CLI. For an Azure VM, inspect the instance view requested in the scripted procedure. Compare the reported installed build with the feature's required build. For the Arc proxy scenario, verify `2.0.3585.403` or later. A major/minor value alone doesn't establish the four-part installed build.

To confirm SQL Server protection, open the relevant **SQL virtual machines** or **SQL Server - Azure Arc** resource in the portal. Under **Security**, select **Defender for Cloud**, and confirm that **Protection status** is **Protected**. If the update fails or protection isn't healthy, use [Troubleshoot Defender for SQL on machines configuration](/en-us/azure/defender-for-cloud/troubleshoot-sql-machines-guide).

For the resource-level protection check, see [Verify SQL machine protection](/en-us/azure/defender-for-cloud/verify-machine-protection#verify-protection-on-a-single-sql-server-vm). The subscription recommendation refreshes every 12 hours, so don't use an immediate recommendation change as the only verification.

## REST API reference

For REST API integration, use these references.

- [Arc machine extension Update API](/en-us/rest/api/hybridcompute/machine-extensions/update)
- [Azure VM extension Update API](/en-us/rest/api/compute/virtual-machine-extensions/update)
- [Azure VM extension Get API](/en-us/rest/api/compute/virtual-machine-extensions/get)