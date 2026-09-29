---
layout: Conceptual
title: Enable Microsoft Defender for SQL Servers on Machines - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-sql-usage
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
description: Learn how to protect your Microsoft SQL Servers on Azure VMs, on-premises, and in hybrid and multicloud environments with Microsoft Defender for Cloud.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 67e8dbbb-7cd3-afb7-a115-4d1fb56337f8
document_version_independent_id: 0418b176-3f1e-4ee8-e9e4-50abb72ad928
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-sql-usage.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-sql-usage
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-sql-usage.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cbe4ca68-43ac-4375-aba5-5945a6394c20
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ced846cc-6a3c-4c8f-9dfb-3de0e90e2742
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 45b417aa-12f9-034f-8d88-f2eb243385c6
---

# Enable Microsoft Defender for SQL Servers on Machines - Microsoft Defender for Cloud | Microsoft Learn

Important

This article applies to Azure commercial cloud and Azure Government cloud.

The Defender for SQL Servers on Machines plan is one of the Defender for Databases plans in Microsoft Defender for Cloud. Use Defender for SQL Servers on Machines to protect SQL virtual machines (VM) and Azure Arc SQL Server instances.

Important

The Defender for SQL Servers on Machines plan is undergoing a transition to the new agent architecture. For more information, see [Defender for SQL Servers on Machines plan transition](release-notes-archive#update-to-defender-for-sql-servers-on-machines-plan).

## Prerequisites

Before you enable the plan, make sure the following prerequisites are met:

- **Subscription permissions**: To deploy the plan on a subscription, including Azure Policy, you need **Subscription Owner** permissions.
- **SQL Server instance permissions**: SQL Server service accounts must be a member of the **sysadmin** fixed server role on each SQL Server instance, which is the default setting. Learn more about the [SQL Server service account requirement](/en-us/sql/sql-server/azure-arc/configure-least-privilege).
- **Supported Resources**:

    - [SQL virtual machines](/en-us/azure/azure-sql/virtual-machines/windows/sql-server-on-azure-vm-iaas-what-is-overview), and [Azure Arc SQL Server instances](/en-us/sql/sql-server/azure-arc/overview) are supported.
    - On-premises machines must be [onboarded to Arc and registered as Azure Arc SQL Server instances](/en-us/azure/azure-arc/servers/learn/quick-enable-hybrid-vm).

**Communication**: Allow outbound HTTPS traffic on Transmission Control Protocol (TCP) port 443 using Transport Layer Security (TLS) to `*.<region>.arcdataservices.com` URL. Learn more about [URL requirements](/en-us/azure/azure-arc/servers/network-requirements#urls?tabs=azure-cloud).

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
- **Supported SQL Server versions** - SQL Server 2012 (11.x) and later versions.
- **Supported operating systems**- Windows Server 2012 R2 and later versions.

Note

Azure Arc SQL Server instances with the Arc proxy feature enabled are **not** currently supported. Arc proxy is an optional connectivity feature for Azure Arc-enabled servers.

## Enable the plan

### Enable the plan on an Azure subscription

To enable the Defender for SQL servers on machines plan, you need to enable the Defender for Databases plan on your subscription. The Defender for SQL servers on machines plan is included in the Defender for Databases plan.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Navigate to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select the relevant subscription.
4. On the Defender plans page, locate the Databases plan and select **Select types**.

    [![Screenshot that shows you where to select types on the Defender plans page.](media/tutorial-enabledatabases-plan/select-types.png)](media/tutorial-enabledatabases-plan/select-types.png#lightbox)
5. In the Resource types selection window, toggle the **SQL Servers on Machines** plan to **On**.

    [![Screenshot that shows where to toggle the Defender for SQL servers on machines, to on.](media/defender-for-sql-usage/sql-toggle-on.png)](media/defender-for-sql-usage/sql-toggle-on.png#lightbox)
6. Select **Continue** &gt; **Save**.

### Enable the plan on an Amazon Web Services (AWS) or Google Cloud Platform (GCP) subscription

To enable the Defender for SQL servers on machines plan, you need to enable the Defender for Databases plan on your subscription. The Defender for SQL servers on machines plan is included in the Defender for Databases plan.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Search for and select **Microsoft Defender for Cloud**.
3. Select **Environment settings**.
4. Select the relevant AWS or GCP subscription.
5. On the Defender plans page, locate the Databases plan and select **Settings**.
6. In the SQL Servers on machines section, toggle the SQL Servers on machines plan to **On**.

    [![Screenshot that shows where to locate the on button for Defender for SQL Servers on machines is located.](media/defender-for-sql-usage/enable-on-aws.png)](media/defender-for-sql-usage/enable-on-aws.png#lightbox)
7. Select **Save**.

## Enable the plan at the SQL Server resource level

We recommend enabling the plan on your entire Azure subscription. However, you might need to enable Defender for SQL on machines on specific machines.

To enable the plan on specific machines, you need to [disable the plan on the subscription](disable-sql-on-machines) and apply the following instructions to the relevant machines at the resource level.

1. In the Azure portal, search for and select:

    - **Azure Arc** &gt; **Data services** &gt; **SQL Server instances**.  or
    - **SQL virtual machines**.
2. Select the relevant SQL Server instance.
3. Locate the security menu and select **Microsoft Defender for Cloud**.

    [![Screenshot that shows where to locate Defender for Cloud under the security section.](media/defender-for-sql-usage/select-defender-for-cloud.png)](media/defender-for-sql-usage/select-defender-for-cloud.png#lightbox)
4. Select **Enable Microsoft Defender for SQL servers on Machines**.

    [![Screenshot that shows where to enable Defender for SQL servers on machines.](media/defender-for-sql-usage/enable-resource-level.png)](media/defender-for-sql-usage/enable-resource-level.png#lightbox)

## Verify that your machines are protected

Important

Don't skip verifying that all machines are protected, as it's important to confirm your deployment is secure.

Depending on your environment, it can take a few hours to discover and protect SQL instances. As a final step, you should [verify that all machines are protected](verify-machine-protection).