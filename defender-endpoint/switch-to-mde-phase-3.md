---
layout: Conceptual
title: Migrate to Microsoft Defender for Endpoint - Onboard - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/switch-to-mde-phase-3
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Onboard devices to Microsoft Defender for Endpoint, run a detection test, confirm Microsoft Defender Antivirus passive mode, get antivirus updates, and uninstall your non-Microsoft solution.
ms.service: defender-endpoint
ms.subservice: onboard
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- m365solution-migratetomdatp
- highpri
- tier1
ms.custom:
- msecd-doc-authoring-1016
- migrationguides
- admindeeplinkDEFENDER
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.reviewer: jesquive, chventou, jonix, chriggs, owtho, yongrhee
ai-usage: ai-assisted
locale: en-us
document_id: 17a961eb-5201-8eb4-6bd9-d4fc48f0fa82
document_version_independent_id: 17a961eb-5201-8eb4-6bd9-d4fc48f0fa82
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/switch-to-mde-phase-3.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: switch-to-mde-phase-3
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/switch-to-mde-phase-3.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
platformId: fb923cd8-9315-f805-3a9c-79a04e4a842d
---

# Migrate to Microsoft Defender for Endpoint - Onboard - Microsoft Defender for Endpoint | Microsoft Learn

| [![Diagram of the migration phases with Phase 1 Prepare highlighted.](media/phase-diagrams/prepare.png#lightbox)](switch-to-mde-phase-1)[Phase 1: Prepare](switch-to-mde-phase-1) | [![Diagram of the migration phases with Phase 2 Set up highlighted.](media/phase-diagrams/setup.png#lightbox)](switch-to-mde-phase-2)[Phase 2: Set up](switch-to-mde-phase-2) | ![Diagram of the migration phases with Phase 3 Onboard highlighted as the current step.](media/phase-diagrams/onboard.png#lightbox)Phase 3: Onboard |
| --- | --- | --- |
|  |  | *You're here!* |

**Welcome to Phase 3 of [migrating to Defender for Endpoint](switch-to-mde-overview#the-migration-process)**. Before you begin, make sure you've completed [Phase 1: Prepare](switch-to-mde-phase-1) and [Phase 2: Set up](switch-to-mde-phase-2). This migration phase includes the following steps:

1. Onboard devices to Defender for Endpoint.
2. Run a detection test.
3. Confirm that Microsoft Defender Antivirus is in passive mode on your endpoints.
4. Get updates for Microsoft Defender Antivirus.
5. Uninstall your non-Microsoft solution.
6. Make sure Defender for Endpoint is working correctly.

Important

If you want to run multiple security solutions side by side, see [Considerations for performance, configuration, and support](/en-us/defender-endpoint/mde-side-by-side).

You might have already configured mutual security exclusions for devices onboarded to Microsoft Defender for Endpoint. If you still need to set mutual exclusions to avoid conflicts, see [Add Microsoft Defender for Endpoint to the exclusion list for your existing solution](/en-us/defender-endpoint/switch-to-mde-phase-2#step-2-add-microsoft-defender-for-endpoint-to-the-exclusion-list-for-your-existing-solution).

## Step 1: Onboard devices to Microsoft Defender for Endpoint

Follow these steps to start onboarding devices to Microsoft Defender for Endpoint.

1. Go to the [Microsoft Defender portal](https://security.microsoft.com) and sign in.
2. Choose **Settings** &gt; **Endpoints** &gt; **Onboarding** (under **Device management**).
3. In the **Select operating system to start onboarding process** list, select an operating system.
4. Under **Deployment method**, select an option. Follow the links and prompts to onboard your organization's devices. Need help? See Onboarding methods (in this article).

Note

If something goes wrong while onboarding, see [Troubleshoot Microsoft Defender for Endpoint onboarding issues](troubleshoot-onboarding). That article describes how to resolve onboarding issues and common errors on endpoints.

### Onboarding methods

Deployment methods vary, depending on operating system and preferred methods. The following table lists resources to help you onboard to Defender for Endpoint:

| Operating systems | Methods |
| --- | --- |
| Windows 10 or laterWindows Server 2016 or laterWindows Server, version 1803 or laterWindows Server 2012 R2 | [Microsoft Intune or Mobile Device Management](configure-endpoints-mdm)[Microsoft Configuration Manager](configure-endpoints-sccm)[Group Policy](configure-endpoints-gp)[VDI scripts](configure-endpoints-vdi)[Local script (up to 10 devices)](configure-endpoints-script) The local script method is suitable for a proof of concept but shouldn't be used for production deployment. For a production deployment, we recommend using Group Policy, Microsoft Configuration Manager, or Intune. |
| Windows Server 2008 R2 SP1 | [Microsoft Monitoring Agent (MMA)](onboard-downlevel#install-and-configure-microsoft-monitoring-agent-windows-81-only) or [Microsoft Defender for Cloud](/en-us/azure/security-center/security-center-wdatp) The Microsoft Monitoring Agent is now Azure Log Analytics agent. To learn more, see [Log Analytics agent overview](/en-us/azure/azure-monitor/platform/log-analytics-agent). |
| Windows 8.1 EnterpriseWindows 8.1 ProWindows 7 SP1 ProWindows 7 SP1 | [Microsoft Monitoring Agent (MMA)](onboard-downlevel)The Microsoft Monitoring Agent is now Azure Log Analytics agent. To learn more, see [Log Analytics agent overview](/en-us/azure/azure-monitor/platform/log-analytics-agent). |
| **Windows serversLinux servers** | [Integration with Microsoft Defender for Cloud](azure-server-integration) |
| macOS | [Local script](mac-install-manually)[Microsoft Intune](mac-install-with-intune)[JAMF Pro](mac-install-with-jamf)[Mobile Device Management](mac-install-with-other-mdm) |
| Linux | [Local script](linux-install-manually)[Puppet](linux-install-with-puppet)[Ansible](linux-install-with-ansible)[Chef](linux-deploy-defender-for-endpoint-with-chef) |
| Android | [Microsoft Intune](/en-us/intune/intune-service/protect/microsoft-defender-deploy-android) |
| iOS | [Microsoft Intune](ios-install)[Mobile Application Manager](ios-install-unmanaged) |

Note

If you're using Windows Server 2016 or Windows Server 2012 R2, see [Onboard Windows Server 2012 R2 and Windows Server 2016 to Microsoft Defender for Endpoint](onboard-server).

Important

The standalone versions of Defender for Endpoint Plan 1 and Plan 2 do not include server licenses. To onboard servers, you'll need an additional license, such as [Microsoft Defender for Servers Plan 1 or Plan 2](/en-us/azure/defender-for-cloud/plan-defender-for-servers-select-plan). To learn more, see [Server plans](onboard-server#server-plans).

## Step 2: Run a detection test

To verify that your onboarded devices are properly connected to Defender for Endpoint, you can run a detection test. Before running a detection test on macOS or Linux, make sure the device meets the system requirements for [macOS](microsoft-defender-endpoint-mac) or [Linux](mde-linux-prerequisites).

| Operating system | Guidance |
| --- | --- |
| Windows 10 or laterWindows Server 2012 R2 and later Windows Server, version 1803, or later | See [Run a detection test](run-detection-test). |
| macOS (see [System requirements](microsoft-defender-endpoint-mac)) | Download and use the [DIY detection test app for macOS](https://aka.ms/mdatpmacosdiy). Also see [Run the connectivity test](troubleshoot-cloud-connect-mdemac#run-the-connectivity-test). |
| Linux (see [System requirements](mde-linux-prerequisites)) | 1. Run the following command, and look for a result of **1**: `mdatp health --field real_time_protection_enabled`.2. Open a Terminal window, and run the following command: `curl -o ~/Downloads/eicar.com.txt https://www.eicar.org/download/eicar.com.txt`.3. Run the following command to list any detected threats: `mdatp threat list`.For more information, see [Defender for Endpoint on Linux](microsoft-defender-endpoint-linux). |

## Step 3: Confirm that Microsoft Defender Antivirus is in passive mode on your endpoints

Now that your endpoints have been onboarded to Defender for Endpoint, your next step is to make sure Microsoft Defender Antivirus is running in passive mode by using PowerShell.

1. On a Windows device, open Windows PowerShell as an administrator.
2. Run the following PowerShell cmdlet: `Get-MpComputerStatus|select AMRunningMode`.
3. Review the results. You should see **Passive mode**.

Note

To learn more about passive mode and active mode, see [More details about Microsoft Defender Antivirus states](microsoft-defender-antivirus-compatibility#more-details-about-microsoft-defender-antivirus-states).

### Set Microsoft Defender Antivirus on Windows Server to passive mode manually

The **ForceDefenderPassiveMode** registry value controls whether Microsoft Defender Antivirus stays in passive mode on supported Windows Server versions. To set this value on Windows Server 2019 and later, Windows Server, version 1803 or later and Azure Stack HCI OS, version 23H2 and later, follow these steps:

1. Open Registry Editor, and then navigate to `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Advanced Threat Protection`.
2. Edit (or create) a DWORD entry called **ForceDefenderPassiveMode**, and specify the following settings:

    - Set the DWORD's value to **1**.
    - Under **Base**, select **Hexadecimal**.

Note

You can use other methods to set the registry key, such as the following:

- [Group Policy Preference](/en-us/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn581922%28v=ws.11%29)
- [Local Group Policy Object tool](/en-us/windows/security/operating-system-security/device-management/windows-security-configuration-framework/security-compliance-toolkit-10#what-is-the-local-group-policy-object-lgpo-tool)
- [A package in Configuration Manager](/en-us/intune/configmgr/apps/deploy-use/packages-and-programs)

### Start Microsoft Defender Antivirus on Windows Server 2016

If you're using Windows Server 2016, you might need to start Microsoft Defender Antivirus manually by doing the following steps:

1. In an elevated Command Prompt (a Command Prompt window you opened by selecting **Run as administrator**), run the following commands:

    Tip

    The first command changes the directory to the latest version of &lt;antimalware platform version&gt; in `%ProgramData%\Microsoft\Windows Defender\Platform\<antimalware platform version>`. If that path doesn't exist, it goes to `%ProgramFiles%\Microsoft Defender`.

    Run the following batch commands to switch to the latest Windows Defender platform folder and then enable Windows Defender:

    ```dos
    (set "_done=" & if exist "%ProgramData%\Microsoft\Windows Defender\Platform\" (for /f "delims=" %d in ('dir "%ProgramData%\Microsoft\Windows Defender\Platform" /ad /b /o:-n 2^>nul') do if not defined _done (cd /d "%ProgramData%\Microsoft\Windows Defender\Platform\%d" & set _done=1)) else (cd /d "%ProgramFiles%\Windows Defender")) >nul 2>&1
    
    MpCmdRun.exe -WdEnable
    ```
2. Restart the device.

## Step 4: Get updates for Microsoft Defender Antivirus

Keep Microsoft Defender Antivirus up to date so your devices can protect against new malware and attack methods. Updates are important even when Microsoft Defender Antivirus runs in passive mode. For more information, see [Microsoft Defender Antivirus compatibility](microsoft-defender-antivirus-compatibility).

There are two types of updates related to keeping Microsoft Defender Antivirus up to date:

- Security intelligence updates
- Product updates

To get your updates, follow the guidance in [Manage Microsoft Defender Antivirus updates and apply baselines](microsoft-defender-antivirus-updates).

## Step 5: Uninstall your non-Microsoft solution

Important

If, for some reason, Microsoft Defender Antivirus does not go into active mode after you uninstall your non-Microsoft antivirus/antimalware solution, see [Microsoft Defender Antivirus seems to be stuck in passive mode](switch-to-mde-troubleshooting#microsoft-defender-antivirus-seems-to-be-stuck-in-passive-mode).

If, at this point you have onboarded your organization's devices to Defender for Endpoint, and Microsoft Defender Antivirus is installed and enabled, then your next step is to uninstall your non-Microsoft antivirus, antimalware, and endpoint protection solution. When you uninstall your non-Microsoft solution, Microsoft Defender Antivirus changes from passive mode to active mode. In most cases, this happens automatically.

You can monitor the state of Microsoft Defender Antivirus at scale from the Defender XDR Portal using the [Device Health Report](https://security.microsoft.com/devicehealth?viewid=oldavhealthreport). This report highlights the state of Microsoft Defender Antivirus on devices onboarded to Defender for Endpoint, helping you to track current antivirus mode, engine version and various other details.

Important

If, for some reason, Microsoft Defender Antivirus does not go into active mode after you have uninstalled your non-Microsoft antivirus/antimalware solution, see [Microsoft Defender Antivirus seems to be stuck in passive mode](switch-to-mde-troubleshooting#microsoft-defender-antivirus-seems-to-be-stuck-in-passive-mode).

To get help with uninstalling your non-Microsoft solution, contact their technical support team.

## Step 6: Make sure Defender for Endpoint is working correctly

Now that you have onboarded to Defender for Endpoint, and you have uninstalled your former non-Microsoft solution, your next step is to make sure that Defender for Endpoint working correctly.

1. Go to the [Microsoft Defender portal](https://security.microsoft.com) and sign in.
2. In the navigation pane, choose **Endpoints** &gt; **Device inventory**. There, you're able to see protection status for devices.

To learn more, see [Device inventory](machines-view-overview).