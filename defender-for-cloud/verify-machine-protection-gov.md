---
layout: Conceptual
title: Verify Defender for SQL Servers on Machines Protection in Government Clouds - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/verify-machine-protection-gov
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
description: Verify that SQL VMs are protected with the Defender for SQL Servers on Machines plan as expected, ensuring that all security measures are properly implemented.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: ef232c49-ce46-fb3e-c44b-19ff6095fe58
document_version_independent_id: b3ce3b70-6b99-d876-b99d-c410aebf6506
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/verify-machine-protection-gov.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/verify-machine-protection-gov
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/verify-machine-protection-gov.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cbe4ca68-43ac-4375-aba5-5945a6394c20
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ced846cc-6a3c-4c8f-9dfb-3de0e90e2742
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 713a5978-8f14-07e2-61e2-00ef9682074f
---

# Verify Defender for SQL Servers on Machines Protection in Government Clouds - Microsoft Defender for Cloud | Microsoft Learn

Important

This article applies to government clouds. If you're using commercial clouds, see the [Verify SQL machine protection](verify-machine-protection) article.

After you enable protection for SQL virtual machines (VMs) with the Defender for SQL Servers on Machines plan, verify that your SQL servers are protected. This article shows how to check protection status for multiple Azure VMs, Azure Arc-enabled VMs, and individual SQL server VMs in government cloud environments.

## Verify protection on multiple Azure VMs

Get the Defender for SQL Servers on Machines protection status report for all SQL VMs in a specified Azure subscription by running the [Get-SqlVMProtectionStatusReport.ps1 PowerShell script](https://aka.ms/DfSQLprotectionverificationscale). The script applies to Azure VMs only.

## Verify protection on multiple Azure Arc-enabled VMs

Verify protection status across multiple Azure Arc-enabled VMs. Run the following query in Azure Resource Graph to identify unprotected instances.

1. In the Azure portal, search for and select **Azure Resource Graph**.
2. Copy and run the following query to identify Azure Arc-enabled VMs that aren't in a protected state.

    ```kusto
    resources
    | where type == "microsoft.azurearcdata/sqlserverinstances"
    | extend SQLonArcProtection= tostring(properties.azureDefenderStatus)
    | extend ProtectionStatusLastUpdate = tostring(properties.azureDefenderStatusLastUpdated)
    | project name, SQLonArcProtection, ProtectionStatusLastUpdate, resourceGroup, location, type, tenantId, subscriptionId, properties
    | order by ['name'] asc
    ```
3. Review the results, checking the **SQLonArcProtection** status. Any result that doesn't state `Protected` indicates that the SQL Server VM, or Azure Arc-enabled SQL Server isn't protected.

    [![Screenshot of the results screen once the script runs.](media/verify-machines-protection-gov/script-results.png)](media/verify-machines-protection-gov/script-results.png#lightbox)
4. If the `ProtectionStatusLastUpdate` field doesn't show a date within the last day, the machine might not be protected. To confirm, verify the protection on a single SQL server VM. In the Azure portal, check the **Protection status** under **Security** &gt; **Defender for Cloud**.

    [![Screenshot that shows the last status update for the SQL instance.](media/verify-machines-protection-gov/status-update.png)](media/verify-machines-protection-gov/status-update.png#lightbox)

The script can return the following possible protection statuses:

- **Protected**: Defender for SQL actively protects the instance. Ensure the information isn't outdated by checking the **Last Update** field.
- **Not Protected**: Defender for SQL encountered issues while protecting the instance. This status indicates that some intervention is required to enable successful protection.
- **Inactive**: Defender for SQL runs on the machine, but the SQL instance is either paused or stopped.
- **Empty** or **Unknown**: The protection status couldn't be retrieved or doesn't exist on the machine. In this case, assume that the instance isn't protected by Defender for SQL.

## Verify protection on a single SQL server VM

To verify protection for a single SQL server VM, follow these steps in the Azure portal.

1. Depending on the resources in your environment, search for and select **SQL virtual machines** or **SQL Server - Azure Arc**.
2. Locate and select the relevant resource.
3. Under the **Security** tab, select **Defender for Cloud**.
4. Check the **Protection status**. If the status is **Protected**, the deployment was successful.

    [![Screenshot showing protection status as protected.](media/defender-for-sql-usage-gov/protection-status-protected.png)](media/defender-for-sql-usage-gov/protection-status-protected.png#lightbox)

## Troubleshoot unprotected machines

If databases aren't protected, follow the instructions in [Troubleshoot SQL machine protection issues](troubleshoot-sql-machines-guide-gov).