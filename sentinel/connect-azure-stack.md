---
layout: Conceptual
title: Onboard your Azure Stack Hub virtual machines to Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/connect-azure-stack
breadcrumb_path: breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
description: This article shows you how to provision the Azure Monitor, Update, and Configuration Management virtual machine extension on Azure Stack Hub virtual machines and start monitoring them with Microsoft Sentinel.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 0f0e0fac-7950-5123-eab6-95a68a6b62a7
document_version_independent_id: a086ba9a-b2b9-889f-9dc5-1cdba680f648
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/connect-azure-stack.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/connect-azure-stack
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/connect-azure-stack.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2ed91286-6cf7-4b83-810d-75d0ee3b09dd
- https://authoring-docs-microsoft.poolparty.biz/devrel/9e3aacba-1f56-4959-b8e6-b8b007efaf00
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6735bd7e-4f7b-457d-b58c-29e6f0198677
- https://authoring-docs-microsoft.poolparty.biz/devrel/df5d72c7-1f77-4f97-b15d-69b6ad842ccc
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: a12215fa-98c9-c5a7-4557-0019108850df
---

# Onboard your Azure Stack Hub virtual machines to Microsoft Sentinel | Microsoft Learn

With Microsoft Sentinel, you can monitor your VMs running on Azure and Azure Stack Hub in one place. To on-board your Azure Stack machines to Microsoft Sentinel, you first need to add the virtual machine extension to your existing Azure Stack Hub virtual machines.

After you connect Azure Stack Hub machines, choose from a gallery of dashboards that surface insights based on data collected from your Azure Stack Hub virtual machines. Microsoft Sentinel dashboards can be easily customized to your needs.

## Add the virtual machine extension

Add the **Azure Monitor, Update, and Configuration Management** virtual machine extension to the virtual machines running on your Azure Stack Hub.

1. In a new browser tab, log into your [Azure Stack Hub portal](/en-us/azure-stack/user/azure-stack-use-portal#access-the-portal).
2. Go to the **Virtual machines** page, select the virtual machine that you want to protect with Microsoft Sentinel. For information on how to create a virtual machine on Azure Stack Hub, see [Create a Windows server VM with the Azure Stack Hub portal](/en-us/azure-stack/user/azure-stack-quick-windows-portal) or [Create a Linux server VM by using the Azure Stack Hub portal](/en-us/azure-stack/user/azure-stack-quick-linux-portal).
3. Select **Extensions**. The list of virtual machine extensions installed on this virtual machine is shown.
4. Select the **Add** tab. The **New Resource** menu blade opens and shows the list of available virtual machine extensions.
5. Select the **Azure Monitor, Update, and Configuration Management** extension and select **Create**. The **Install extension** configuration window opens.

    ![Screenshot of the Azure Stack Hub portal showing the Install extension settings for the Azure Monitor, Update, and Configuration Management extension.](media/connect-azure-stack/azure-monitor-extension-fix.png)

    Note

    If you do not see the **Azure Monitor, Update and Configuration Management** extension listed in your marketplace, reach out to your Azure Stack Hub operator to make it available.
6. On the Microsoft Sentinel menu, select **Workspace settings** followed by **Advanced**, and copy the **Workspace ID** and **Workspace Key (Primary Key)**.
7. In the Azure Stack Hub **Install extension** window, paste the **Workspace ID** and **Workspace Key (Primary Key)** into the indicated fields, and select **OK**.
8. After the extension installation completes, its status shows as **Provisioning Succeeded**. It might take up to one hour for the virtual machine to appear in the Microsoft Sentinel portal.

For more information on installing and configuring the agent for Windows, see [Connect Windows computers](/en-us/azure/azure-monitor/agents/agent-windows#install-the-agent).

For Linux troubleshooting of agent issues, see [Troubleshoot Azure Log Analytics Linux Agent](/en-us/azure/azure-monitor/agents/agent-linux-troubleshoot).

In the Microsoft Sentinel portal on Azure, under **Virtual Machines**, you have an overview of all VMs and computers along with their status.

## Clean up resources

When no longer needed, you can remove the extension from the virtual machine via the Azure Stack Hub portal.

To remove the extension:

1. Open the **Azure Stack Hub Portal**.
2. Go to **Virtual machines** page, select the virtual machine from which you want to remove the extension.
3. Select **Extensions**, select the extension **Microsoft.EnterpriseCloud.Monitoring**.
4. Select **Uninstall**, and confirm your selection.