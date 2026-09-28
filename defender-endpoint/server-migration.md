---
layout: Conceptual
title: Server migration scenarios for the new version of Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/server-migration
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Read this article to get an overview of how to migrate your servers from the previous, MMA-based solution to the current Defender for Endpoint unified solution package.
ms.service: defender-endpoint
author: paulinbar
ms.author: painbar
ms.localizationpriority: medium
ms.date: 2026-07-02T00:00:00.0000000Z
ms.collection:
- m365-security
- tier2
ms.topic: how-to
ms.subservice: onboard
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 9461f113-7839-e0d1-a6cc-a8e9c8b22900
document_version_independent_id: 9461f113-7839-e0d1-a6cc-a8e9c8b22900
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/server-migration.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: server-migration
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/server-migration.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 41d5a1e7-a8e3-8f6e-7080-1ea4c3533d2e
---

# Server migration scenarios for the new version of Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Note

On Windows Server 2016, always ensure the operating system and Microsoft Defender Antivirus are fully updated before proceeding with installation or upgrade. To receive regular product improvements and fixes for the EDR Sensor component, ensure Windows Update [KB5005292 - Microsoft Defender for Endpoint EDR Sensor update](https://go.microsoft.com/fwlink/?linkid=2168277) gets applied or approved after installation. In addition, to keep protection components updated, please reference [Manage Microsoft Defender Antivirus updates and apply baselines](microsoft-defender-antivirus-updates#platform-and-engine-releases).

The migration instructions in this article apply to the new unified solution and installer (MSI) package of Defender for Endpoint for Windows Server 2012 R2 and Windows Server 2016. This article contains high-level instructions for various possible migration scenarios from the previous Microsoft Monitoring Agent (MMA)-based solution to the current Defender for Endpoint unified solution. These high-level steps are intended as guidelines to be adjusted to the deployment and configuration tools available in your environment. Before you begin, review the [prerequisites for Windows Server 2016 and 2012 R2](onboard-server#prerequisites-for-windows-server-2016-and-2012-r2) and ensure your operating system and Microsoft Defender Antivirus are fully updated.

**If you are using Microsoft Defender for Cloud to perform deployment, you can automate installation and upgrade. See [Defender for Servers Plan 2 now integrates with MDE unified solution](https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/defender-for-servers-plan-2-now-integrates-with-mde-unified/ba-p/3527534)**

Note

Operating system upgrades with Defender for Endpoint installed aren't supported. Offboard, uninstall, upgrade the operating system, and then proceed with installation.

## Migrate using the installer script

Note

Make sure the machines you run the script on isn't blocking the execution of the script. The recommended execution policy setting for PowerShell is Allsigned. This requires importing the script's signing certificate into the Local Computer Trusted Publishers store if the script is running as SYSTEM on the endpoint.

To facilitate upgrades when Microsoft Configuration Manager isn't yet available or updated to perform the automated upgrade, you can use this [Defender for Endpoint unified solution upgrade script](https://github.com/microsoft/mdefordownlevelserver/archive/refs/heads/main.zip). Download it by selection the "Code" button and downloading the .zip file, then extracting install.ps1. It can help automate the following required steps:

1. Remove the OMS workspace for Defender for Endpoint (OPTIONAL).
2. Remove System Center Endpoint Protection (SCEP) client if installed.
3. Review the [Prerequisites for Windows Server 2016 and 2012 R2](onboard-server#prerequisites-for-windows-server-2016-and-2012-r2).
4. Enable and update the Microsoft Defender Antivirus feature on Windows Server 2016.
5. Install Defender for Endpoint.
6. Apply the onboarding script **for use with Group Policy** downloaded from the [Microsoft Defender portal](https://security.microsoft.com).

    To use the script, download it to an installation directory where you have also placed the installation and onboarding packages (see [Onboard servers](onboard-server)).

    EXAMPLE: `.\install.ps1 -RemoveMMA <YOUR_WORKSPACE_ID> -OnboardingScript ".\WindowsDefenderATPOnboardingScript.cmd"`

For more information on how to use the script, use the PowerShell command `get-help .\install.ps1`.

## Microsoft Configuration Manager migration scenarios

Note

You need Configuration Manager version 2107 (August 2021) or later to configure Endpoint Protection policies. In [version 2207](/en-us/intune/configmgr/core/plan-design/changes/whats-new-in-version-2207#improved-microsoft-defender-for-endpoint-mde-onboarding-for-windows-server-2012-r2-and-windows-server-2016) (August 2022) or later, you can fully automate deployment and upgrades.

For instructions on how to migrate using Configuration Manager before version 2207, see [Migrating servers from Microsoft Monitoring Agent to the unified solution.](application-deployment-via-mecm)

## If you are running a non-Microsoft antivirus solution

Perform the following steps to migrate machines that currently use a non-Microsoft antivirus solution to the Defender for Endpoint unified solution.

1. Fully update the machine including Microsoft Defender Antivirus (Windows Server 2016) ensuring [Prerequisites for Windows Server 2016 and 2012 R2](onboard-server#prerequisites-for-windows-server-2016-and-2012-r2) are met.
2. Ensure your non-Microsoft antivirus management solution no longer pushes antivirus agents to these machines.
3. Author your policies for the protection capabilities in Defender for Endpoint and target those to the machine in the tool of your choice.
4. Install the Defender for Endpoint package for Windows Server 2012 R2 and Windows Server 2016, and set it to passive mode.
5. Apply the onboarding script **for use with Group Policy** downloaded from the [Microsoft Defender portal](https://security.microsoft.com).
6. Apply updates.
7. Remove your non-Microsoft antivirus software by either using the non-Microsoft antivirus console or by using Configuration Manager as appropriate. Make sure to remove passive mode configuration.

    To move a machine out of passive mode, set the following key:

    Path: `HKLM\SOFTWARE\Policies\Microsoft\Windows Advanced Threat Protection` Name: `ForceDefenderPassiveMode` Type: `REG_DWORD` Value: `0`

Tip

You can use the [installer script for server migration](server-migration#installer-script) as part of your application to automate the non-Microsoft antivirus migration steps in this section. To enable passive mode, apply the -Passive flag. For example, `.\install.ps1 -RemoveMMA <YOUR_WORKSPACE_ID> -OnboardingScript ".\WindowsDefenderATPOnboardingScript.cmd" -Passive`.

In the non-Microsoft antivirus migration procedure, steps 2 and 7 apply only if you intend to replace your non-Microsoft antivirus solution. See [Better together: Microsoft Defender Antivirus and Microsoft Defender for Endpoint](why-use-microsoft-defender-antivirus).

## If you are running System Center Endpoint Protection but aren't managing the machine using Microsoft Configuration Manager

Use the following steps if System Center Endpoint Protection is installed but the machine is not managed by Configuration Manager.

1. Fully update the device, including Microsoft Defender Antivirus (on Windows Server 2016) ensuring [Prerequisites for Windows Server 2016 and 2012 R2](onboard-server#prerequisites-for-windows-server-2016-and-2012-r2) are met.
2. Create and apply policies using Group Policy, PowerShell, or a non-Microsoft management solution.
3. Uninstall System Center Endpoint Protection (Windows Server 2012 R2).
4. Install Microsoft Defender for Endpoint (see [Onboard Windows Server 2012 R2 and Windows Server 2016 to Microsoft Defender for Endpoint](onboard-server))
5. Apply the onboarding script **for use with Group Policy** downloaded from the [Microsoft Defender portal](https://security.microsoft.com).
6. Apply updates.

Tip

You can use the installer script to automate the System Center Endpoint Protection migration steps in this procedure.

## Microsoft Defender for Cloud scenarios

The following scenarios apply when you use Microsoft Defender for Cloud to manage deployment or upgrades.

### You're using Microsoft Defender for Cloud. The Microsoft Monitoring Agent (MMA) and/or Microsoft Antimalware for Azure (SCEP) are installed and you want to upgrade.

If you're using Microsoft Defender for Cloud, you can use the automated upgrade process. See [Protect your endpoints with Defender for Cloud's integrated EDR solution: Microsoft Defender for Endpoint](/en-us/azure/security-center/security-center-wdatp#enable-the-microsoft-defender-for-endpoint-integration).

## Configure Group Policy for server migration

For configuration using Group Policy, ensure you're using the latest ADMX files in your central store to access the correct Defender for Endpoint policy options. For reference, see [How to create and manage the Central Store for Group Policy Administrative Templates in Windows](/en-us/troubleshoot/windows-client/group-policy/create-and-manage-central-store) and download the latest files **for use with Windows 10**.