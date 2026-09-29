---
layout: Conceptual
title: Troubleshoot Defender for SQL on Machines Configuration - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/troubleshoot-sql-machines-guide
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
description: Troubleshoot Defender for SQL on Machines configuration issues in commercial clouds after enabling protection at the subscription or SQL resource level.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: references_regions, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: ec4e44b5-4478-7b84-3fe8-2379ab197f6a
document_version_independent_id: 6956cd7a-ca0b-7244-08c3-808e44ac03c9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/troubleshoot-sql-machines-guide.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/troubleshoot-sql-machines-guide
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/troubleshoot-sql-machines-guide.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cbe4ca68-43ac-4375-aba5-5945a6394c20
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ced846cc-6a3c-4c8f-9dfb-3de0e90e2742
platformId: 9df45406-fc16-8c10-af6a-70d2113da64b
---

# Troubleshoot Defender for SQL on Machines Configuration - Microsoft Defender for Cloud | Microsoft Learn

This article helps you identify and resolve configuration and protection issues with Microsoft Defender for SQL on Machines in commercial cloud environments.

Important

This article applies to Azure commercial cloud and Azure Government cloud.

Before you start the troubleshooting steps, [enable Defender for SQL Server on Machines](defender-for-sql-usage) at the [Azure subscription level](defender-for-sql-usage#enable-the-plan-on-an-azure-subscription) or [SQL Server resource level](defender-for-sql-usage#enable-the-plan-at-the-sql-server-resource-level).

## Step 1: Required resources and enablement process

Defender for SQL Server on Machines automatically creates the following resources on your machines:

| Resource Type | Level Created |
| --- | --- |
| System Managed Identity. Created only if a user-defined managed identity doesn't exist. | Virtual machine/Arc-enabled server hosting the SQL server instance |
| Defender for SQL extension | The extension is installed on each virtual machine/Arc-enabled server hosting the SQL server instance |

When you enable Defender for SQL Server on a subscription or specified SQL Server, it performs the following actions to protect each SQL Server instance:

- Creates a system-managed identity if there's no user-managed identity in the subscription.
- Installs the Defender for SQL extension on the virtual machine/Arc-enabled server hosting the SQL Server.
- Impersonates the Windows user running the SQL Server service (default sysadmin role) to access the SQL Server instance.

## Step 2: Ensure that you fulfilled the prerequisites

Before you troubleshoot, ensure the following prerequisites are met:

- **Subscription permissions**: To deploy the plan on a subscription, including Azure Policy, you need **Subscription Owner** permissions.
- **SQL Server instance permissions**: SQL Server service accounts must have the **sysadmin** fixed server role on each SQL Server instance, which is the default setting. For more information, see [SQL Server service account requirement](/en-us/sql/sql-server/azure-arc/configure-least-privilege).
- **Supported Resources**:

    - [SQL virtual machines](/en-us/azure/azure-sql/virtual-machines/windows/sql-server-on-azure-vm-iaas-what-is-overview), and [Azure Arc SQL Server instances](/en-us/sql/sql-server/azure-arc/overview) are supported.
    - On-premises machines must be [onboarded to Arc and registered as Azure Arc SQL Server instances](/en-us/azure/azure-arc/servers/learn/quick-enable-hybrid-vm).
- **Communication**: Allow outbound HTTPS traffic over Transmission Control Protocol (TCP) port 443 using Transport Layer Security (TLS) to `*.<region>.arcdataservices.com` URL. For more information, see [URL requirements](/en-us/azure/azure-arc/servers/network-requirements#urls?tabs=azure-cloud).
- **Extensions**: Ensure these extensions aren't blocked in your environment. Learn more about [restricting extensions installation on Windows VMs](/en-us/azure/virtual-machines/extensions/extensions-rmpolicy-howto-ps).

    - **Defender for SQL (IaaS and Arc)**

        - Publisher: Microsoft.Azure.AzureDefenderForSQL
        - Type: AdvancedThreatProtection.Windows
    - **SQL IaaS Extension (IaaS)**

        - Publisher: Microsoft.SqlServer.Management
        - Type: SqlIaaSAgent
    - **SQL IaaS Extension (Arc)**

        - Publisher: Microsoft.AzureData
        - Type: WindowsAgent.SqlServer
- **Supported SQL Server versions**: SQL Server 2012 R2 (11.x) and later versions.
- **Supported operating systems**: SQL Server 2012 R2 and later versions.

## Step 3: Identify and resolve protection misconfigurations at the SQL Server instance Level

Follow the [verification process](verify-machine-protection) to identify protection misconfigurations on SQL Server instances.

The recommendation `The status of Microsoft SQL Servers on Machines should be protected` can be used to verify the protection status of SQL Servers, but the recommendation should be remediated at the resource level. Any SQL server that is unprotected is identified in the unhealthy resource section of the recommendation with a protection status listed and a reason.

Important

The recommendation is only updated every 12 hours. To check the real-time status of your machine, you must [verify the protection status of each SQL server](verify-machine-protection#verify-protection-on-a-single-sql-server-vm) and perform any troubleshooting if necessary.

Use the corresponding unhealthy reason and recommended actions to resolve the misconfiguration:

| Unhealthy reason | Recommended action |
| --- | --- |
| **Missing identity** | Assign user-defined/system-defined managed identity to the virtual machine/Arc-enabled server hosting the SQL Server instance. No Role-based access control permissions are required. |
| **Defender for SQL extension does not exist** | Ensure that the Defender for SQL extension isn't blocked by [Azure deny policies](/en-us/azure/virtual-machines/extensions/extensions-rmpolicy-howto-ps):  - Publisher: Microsoft.Azure.AzureDefenderForSQL  - Type: AdvancedThreatProtection.Windows  Manually install the Defender for SQL extension on the virtual machine by hosting the SQL Server instance by using the provided script. Ensure you have version 2.X or above.  1. Run this script `Set-AzVMExtension -Publisher 'Microsoft.Azure.AzureDefenderForSQL' -ExtensionType  'AdvancedThreatProtection.Windows' -ResourceGroupName 'resourceGroupeName' -VMName <Vm name> -Name 'Microsoft.Azure.AzureDefenderForSQL.AdvancedThreatProtection.Windows' -TypeHandlerVersion '2.0' -Location 'vmLocation' -EnableAutomaticUpgrade $true` 2. Run this script to set the context of the right subscription: `connect-AzAccount -Subscription SubscriptionId -UseDeviceAuthentication` |
| **Defender for SQL extension should be up-to-date** | Update the extension in the Extensions page in the virtual machine/Arc-enabled server resource. |
| **Error during the installation of the Defender for SQL extension** | Check the Defender for SQL extension status in the portal for additional information to troubleshoot the issue. |
| **SQL Server instance is inactive** | Defender for SQL server on Machines can only protect active (running) SQL server instances. |
| **Lack of permissions** | Ensure that the SQL Server service account is a member of the sysadmin fixed server role on each SQL Server instance (default setting). Learn more about [SQL Server service permissions](/en-us/sql/sql-server/azure-arc/configure-least-privilege). |
| **Lack of communication** | Ensure outbound HTTPS traffic on TCP port 443 using Transport Layer Security (TLS) is allowed from the virtual machine/Arc-enabled server to the `*.<region>.arcdataservices.com` URL. Learn more about [URL requirements](/en-us/azure/azure-arc/servers/network-requirements#urls?tabs=azure-cloud) |
| **SQL server restart is needed** | Restart the SQL Server instance so that the Defender for SQL Server installation takes effect. |
| **Internal error** | Please contact support. |

### Multiple SQL Server instances on the same virtual machine

If you have multiple SQL Server instances installed on the same virtual machine, the recommendation `The status of Microsoft SQL Servers on Machines should be protected` can't differentiate between instances. To correlate the error message with the corresponding SQL Server instance, check the error message under the Defender for SQL extension. The Defender for SQL extension can display the following reasons for each instance:

- Restart the SQL Server
- Check permissions
- Ensure the SQL Server instance is active

1. In the Azure portal, search for and select **SQL virtual machine**.
2. Select the relevant virtual machine.
3. Go to **Settings** &gt; **Extensions + applications**.

    [![Screenshot that shows where to locate the Extensions and applications section.](media/troubleshoot-sql-machines-guide/extensions.png)](media/troubleshoot-sql-machines-guide/extensions.png#lightbox)
4. Select the relevant extension to view its protection status.

    [![Screenshot that shows the information screen for the selected extension.](media/troubleshoot-sql-machines-guide/extension-status.png)](media/troubleshoot-sql-machines-guide/extension-status.png#lightbox)

Based on the unhealthy reason listed, take the appropriate action described in Step 3: Identify and resolve protection misconfigurations to remediate the misconfiguration for that SQL Server instance.

## Step 4: Reverify protection status

After completing the remediation of all errors for each SQL Server instance, [reverify the protection status of each SQL Server instance](verify-machine-protection).