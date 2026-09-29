---
layout: Conceptual
title: Verify SQL Machine Protection - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/verify-machine-protection
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
description: Verify SQL Server protection on Azure VMs, Azure Arc machines, and multicloud resources with Defender for SQL Servers on Machines.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 2e872836-342f-1cf4-77c1-ba624896f08f
document_version_independent_id: 0e17419c-c89a-2786-110c-db68b60bd69f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/verify-machine-protection.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/verify-machine-protection
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/verify-machine-protection.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cbe4ca68-43ac-4375-aba5-5945a6394c20
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ced846cc-6a3c-4c8f-9dfb-3de0e90e2742
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 93703f65-4623-5081-0d19-9d8347290c35
---

# Verify SQL Machine Protection - Microsoft Defender for Cloud | Microsoft Learn

Important

This article applies to Azure commercial cloud and Azure Government cloud.

After you enable Defender for SQL Servers on Machines, use the following verification procedures to confirm coverage for SQL Servers on Azure VMs, on-premises machines, and multiple cloud resources. You can check the protection status for an entire Azure subscription or verify a single SQL server virtual machine (VM) or Azure Arc SQL Server instance.

## Verify protection on an entire Azure subscription

Defender for Cloud presents the **The status of Microsoft SQL Servers on Machines should be protected** recommendation, which allows you to review the protection status of Defender for SQL Servers on Machines. This recommendation identifies all SQL VMs and Azure Arc SQL Server instances within a specified Azure subscription. It presents the protection status of each SQL Server instance. See [The status of Microsoft SQL Servers on Machines should be protected](https://aka.ms/NewStatusRecommendation).

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Navigate to **Microsoft Defender for Cloud** &gt; **Recommendations**.
3. Search for and select [The status of Microsoft SQL Servers on Machines should be protected](https://aka.ms/NewStatusRecommendation).
4. Select **View recommendation for all resources**.

    [![Screenshot that shows where to locate the View recommendation for all resources button.](media/verify-machines-protection/view-recommendation.png)](media/verify-machines-protection/view-recommendation.png#lightbox)
5. Review the unhealthy reason.

    [![Screenshot that shows where to locate the protection status and the reason for that status.](media/verify-machines-protection/protection-status-reason.png)](media/verify-machines-protection/protection-status-reason.png#lightbox)
6. Select the unhealthy resource.
7. Follow the steps in the Troubleshoot SQL machines protection guide, starting at [Step 3: Identify and resolve protection misconfigurations at the SQL Server instance Level](troubleshoot-sql-machines-guide#step-3-identify-and-resolve-protection-misconfigurations-at-the-sql-server-instance-level).

Defender for Cloud updates the **The status of Microsoft SQL Servers on Machines should be protected** recommendation every 12 hours. Follow the [Troubleshoot SQL machines protection](troubleshoot-sql-machines-guide) guide to fix each unprotected SQL server instance.

## Verify protection on a single SQL server VM

You can also verify the protection status of a single SQL server VM or Azure Arc SQL Server instance.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Depending on the resources in your environment, search for and select either:

    - **SQL virtual machines**
    - **SQL Server - Azure Arc**
3. Locate and select the relevant resource.
4. Under the **Security** tab, select **Defender for Cloud**.
5. Check the **Protection status**. If the status is **Protected**, the deployment was successful.

    [![Screenshot showing protection status as protected.](media/verify-machines-protection/protection-status-protected.png)](media/verify-machines-protection/protection-status-protected.png#lightbox)
6. (Optional) Resolve the unprotected server instance status with the [troubleshooting SQL Server on Machines guide](troubleshoot-sql-machines-guide).

Defender for Cloud updates the **The status of Microsoft SQL Servers on Machines should be protected** recommendation every 12 hours. Follow the [Troubleshoot SQL machines protection](troubleshoot-sql-machines-guide) guide to fix each unprotected SQL server instance.