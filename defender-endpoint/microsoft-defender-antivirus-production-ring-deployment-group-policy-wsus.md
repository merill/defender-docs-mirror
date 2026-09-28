---
layout: Conceptual
title: Production ring deployment using Group Policy and Windows Server Update Services - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/microsoft-defender-antivirus-production-ring-deployment-group-policy-wsus
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Microsoft Defender Antivirus is an enterprise endpoint security platform that helps defend against advanced persistent threats. This article provides information about how to use a ring deployment method to update your Microsoft Defender Antivirus production clients using Group Policy and Windows Server Update Services (WSUS).
ms.service: defender-endpoint
ms.author: chrisda
author: chrisda
ms.reviewer: yongrhee
ms.localizationpriority: high
ms.collection:
- m365-security
- tier1
- mde-ngp
ms.custom: intro-overview
ms.topic: install-set-up-deploy
ms.subservice: ngp
ms.date: 2025-10-20T00:00:00.0000000Z
locale: en-us
document_id: d0bb5854-c033-0a33-fda4-b3738eb919e1
document_version_independent_id: d0bb5854-c033-0a33-fda4-b3738eb919e1
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/microsoft-defender-antivirus-production-ring-deployment-group-policy-wsus.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: microsoft-defender-antivirus-production-ring-deployment-group-policy-wsus
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/microsoft-defender-antivirus-production-ring-deployment-group-policy-wsus.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c6f99e62-1cf6-4b71-af9b-649b05f80cce
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3f56b378-07a9-4fa1-afe8-9889fdc77628
platformId: 15dcd40b-3acc-1146-f269-83ee4f2036fb
---

# Production ring deployment using Group Policy and Windows Server Update Services - Microsoft Defender for Endpoint | Microsoft Learn

Microsoft Defender for Endpoint is an enterprise endpoint security platform designed to help enterprise networks prevent, detect, investigate, and respond to advanced threats.

Tip

Microsoft Defender for Endpoint is available in two plans, Defender for Endpoint Plan 1 and Plan 2. A new Microsoft Defender Vulnerability Management add-on is now available for Plan 2.

## Prerequisites

### Supported operating systems

- Windows
- Windows Server

## Before you begin

This article assumes that you have experience with Windows Server Update Services (WSUS) and/or already have WSUS installed. If you aren't already familiar with WSUS, see the following articles for important configuration details:

- [Configure WSUS](/en-us/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus) - Applies to: Windows Server 2012 and later, and Azure Stack HCI OS, version 23H2 and later.
- [Configure Windows Server Update Services (WSUS) in Analytics Platform System][/sql/analytics-platform-system/configure-windows-server-update-services-wsus.md] - Analytics Platform System

## Setting up the production environment

This section provides information about setting up the production environment using Group Policy and Windows Server Update Services (WSUS).

[![Screenshot that shows an example ring deployment schedule for Group Policy with WSUS environments.](media/microsoft-defender-antivirus-deploy-ring-group-policy-wsus.png)](media/microsoft-defender-antivirus-deploy-ring-group-policy-wsus.png#lightbox)

Note

Security intelligence update (SIU) is equivalent to signature updates, which is the same as definition updates.

1. On the left pane of **Server Manager**, select **Dashboard** &gt; **Tools** &gt; **Windows Server Update Services**.

    Note

    If the **Complete WSUS Installation** dialog box appears, select **Run**. In the **Complete WSUS Installation** dialog box, select **Close when the installation successfully finishes**.
2. The **WSUS Configuration Wizard** opens. On the **Before you Begin** page, review the information, and then select **Next**.
3. Read the instructions on the **Join the Microsoft Update Improvement Program** page. Keep the default selection if you want to participate in the program, or clear the checkbox if you don't. Then select **Next**.
4. On the **Choose Upstream Server** page, select **Synchronize from another Windows Server Update Services server**.

    - In **Server name**, enter the server name. For example, type *YR2K19*.
    - In **Port number** enter the port on which this server communicates with the upstream server. For example, type *8530*.

    This is shown in the following figure.

    [![Screenshot that shows a screen capture of the Update Services snap-in console, Choose Upstream Server page.](media/microsoft-defender-antivirus-deploy-ring-group-policy-wsus-production-update-service-upstream.png)](media/microsoft-defender-antivirus-deploy-ring-group-policy-wsus-production-update-service-upstream.png#lightbox)
5. Select **Next**.

    An autonomous downstream server, like a replica server, also uses another WSUS server as its master repository, but allows for individual approvals for updates different from approvals of the master. The autonomous server:

    - Allows flexibility in creating computer groups
    - Doesn't have to be in the same Active Directory forest as the master
6. (Optional, depending on configuration) On the **Specify Proxy Server** page, select the **Use a proxy server when synchronizing** checkbox. Then enter the proxy server name and port number (port 80 by default) in the corresponding boxes.

    Important

    You must complete this step if you identified that WSUS needs a proxy server to have internet access.

    - If you want to connect to the proxy server by using specific user credentials, select the **Use user credentials to connect to the proxy server** checkbox. Then enter the user name, domain, and password of the user in the corresponding boxes.
    - If you want to enable basic authentication for the user who is connecting to the proxy server, select the **Allow basic authentication (password is sent in cleartext)** checkbox.

    Select **Next**.
7. On the **Connect to Upstream Server** page, select **start Connecting**. When WSUS connects to the server, select **Next**.
8. On the **Choose Languages** page, you can select the languages from which WSUS receives updates: **all languages** or a **subset of languages**. Selecting a subset of languages saves disk space, but it's important to choose all the languages that all the clients need on this WSUS server.

    If you choose to get updates only for specific languages, select **Download updates only in these languages**, and then select the languages for which you want updates. Otherwise, leave the default selection.

    Warning

    If you select the option **Download updates only in these languages**, and the server has a downstream WSUS server connected to it, selecting this option will force the downstream server to also use only the selected languages.

    After you select the language options for your deployment, select **Next**.
9. The **Set Sync Schedule** page opens. (The **Choose Products** and **Choose Classifications** pages are grayed out and can't be configured).

    - Select **Synchronize automatically**, the WSUS server synchronizes at set intervals.
    - In **First synchronization** specify a time for the first synchronization. For example, select *5:00:00 PM.*
    - In **Synchronizations per day**, specify the number of times you want synchronizations to occur. For example, select *1*, and then select **Next**.
10. On the **Finished** page, select **Next**.
11. On the **What's next** page, select **Next** to finish.

#### Define the order of sources for downloading security intelligence updates

1. On your Group Policy management computer, open the **Group Policy Management Console**, right-click the *Group Policy Object* you want to configure and select **Edit**.
2. In the **Group Policy Management Editor** go to **Computer configuration**, select **Policies**, then select **Administrative templates**.
3. Expand the tree to **Windows components** &gt; **Windows Defender** &gt; **Signature updates**.

    - Double-click the **Define the order of sources for downloading security intelligence updates** setting and set the option to **Enabled**.
    - In **Options**, type *InternalDefinitionUpdateServer*, and then select **OK**. The configured **Define the order of sources for downloading security intelligence updates** page is shown in the following figure.

        [![Screenshot that shows a screen capture of the results from a Microsoft Update Catalog search for KB4052623.](media/microsoft-defender-antivirus-deploy-ring-group-policy-wsus-gp-download-order.png)](media/microsoft-defender-antivirus-deploy-ring-group-policy-wsus-gp-download-order.png#lightbox)
4. In **Define the order of sources for downloading security intelligence updates**, select **Enabled**. In **Options**, enter the order of sources for downloading security intelligence updates. For example, type *InternalDefinitionUpdateServer*.

## If you encounter problems

If you encounter problems with your deployment, create or append your Microsoft Defender Antivirus policy:

1. In [Group Policy Management Console](/en-us/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn265969%28v=ws.11%29) (GPMC, GPMC.msc), create or append to your Microsoft Defender Antivirus policy using the following setting:

    Go to **Computer Configuration** &gt; **Policies** &gt; **Administrative Templates** &gt; **Windows Components** &gt; **Microsoft Defender Antivirus** &gt; (administrator-defined) *PolicySettingName*. For example, *MDAV\_Settings\_Production*, right-click, and then select **Edit**. **Edit** for **MDAV\_Settings\_Production** is shown in the following figure:

    [![Screenshot that shows a screen capture of the administrator-defined Microsoft Defender Antivirus policy Edit option.](media/microsoft-defender-antivirus-deploy-ring-group-policy-wsus-gp-policy-edit.png)](media/microsoft-defender-antivirus-deploy-ring-group-policy-wsus-gp-policy-edit.png#lightbox)
2. Select **Define the order of sources for downloading security intelligence updates**.
3. Select the radio button named **Enabled**.
4. Under **Options**, change the entry to *FileShares*, select **Apply**, and then select **OK**. This change is shown in the following figure:

    [![Screenshot that shows a screen capture of the Define the order of sources for downloading security intelligence updates page.](media/microsoft-defender-antivirus-deploy-ring-group-policy-wsus-gp-policy-define-order.png)](media/microsoft-defender-antivirus-deploy-ring-group-policy-wsus-gp-policy-define-order.png#lightbox)
5. Select **Define the order of sources for downloading security intelligence updates**.
6. Select the radio button named **Disabled**, select **Apply**, and then select **OK**. The disabled option is shown in the following figure:

    [![Screenshot that shows a screen capture of the Define the order of sources for downloading security intelligence updates page with Security Intelligence updates disabled.](media/microsoft-defender-antivirus-deploy-ring-group-policy-wsus-gp-policy-disabled.png)](media/microsoft-defender-antivirus-deploy-ring-group-policy-wsus-gp-policy-disabled.png#lightbox)
7. The change is active when Group Policy updates. There are two methods to refresh Group Policy:

    - From the command line, run the Group Policy update command. For example, run `gpupdate / force`. For more information, see [gpupdate](/en-us/windows-server/administration/windows-commands/gpupdate)
    - Wait for Group Policy to automatically refresh. Group Policy refreshes every 90 minutes +/- 30 minutes.

    If you have multiple forests/domains, force replication or wait 10-15 minutes. Then force a Group Policy Update from the Group Policy Management Console.

    - Right-click on an organizational unit (OU) that contains the machines (for example, Desktops), select **Group Policy Update**. This UI command is the equivalent of doing a gpupdate.exe /force on every machine in that OU. The feature to force Group Policy to refresh is shown in the following figure:

        [![Screenshot that shows a screen capture of the Group Policy Management console, initiating a forced update.](media/microsoft-defender-antivirus-deploy-ring-group-policy-wsus-gp-management-console.png)](media/microsoft-defender-antivirus-deploy-ring-group-policy-wsus-gp-management-console.png#lightbox)
8. After the issue is resolved, set the **Signature Update Fallback Order** back to the original setting. `InternalDefinitionUpdateServer|MicrosoftUpdateServer|MMPC|FileShare`.