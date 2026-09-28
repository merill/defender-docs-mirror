---
layout: Conceptual
title: Set up Microsoft Defender for Endpoint during migration - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/switch-to-mde-phase-2
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Move to Defender for Endpoint. Review the setup process, which includes installing Microsoft Defender Antivirus.
ms.service: defender-endpoint
ms.subservice: onboard
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.date: 2026-09-15T00:00:00.0000000Z
ms.collection:
- m365-security
- m365solution-migratetomdatp
- m365solution-mcafeemigrate
- m365solution-symantecmigrate
- highpri
- tier1
ms.topic: how-to
ms.custom: migrationguides, msecd-doc-authoring-1016
ms.reviewer: jesquive, chventou, jonix, chriggs, owtho, yongrhee
ai-usage: ai-assisted
locale: en-us
document_id: 07366a38-b2b8-8d89-1364-19a6ff902f78
document_version_independent_id: 07366a38-b2b8-8d89-1364-19a6ff902f78
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/switch-to-mde-phase-2.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: switch-to-mde-phase-2
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/switch-to-mde-phase-2.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
platformId: 76b249d7-f914-4c03-3eaf-48aa43b2fa4a
---

# Set up Microsoft Defender for Endpoint during migration - Microsoft Defender for Endpoint | Microsoft Learn

| [![Diagram of migration phase 1: prepare your environment for migration to Defender for Endpoint.](media/phase-diagrams/prepare.png#lightbox)](switch-to-mde-phase-1)[Phase 1: Prepare your environment](switch-to-mde-phase-1) | ![Diagram of migration phase 2: set up your Defender for Endpoint environment.](media/phase-diagrams/setup.png#lightbox)Phase 2: Set up | [![Diagram of migration phase 3: onboard devices to Microsoft Defender for Endpoint.](media/phase-diagrams/onboard.png#lightbox)](switch-to-mde-phase-3)[Phase 3: Onboard devices to Defender for Endpoint](switch-to-mde-phase-3) |
| --- | --- | --- |
|  | *You're here!* |  |

**Welcome to the Setup phase of [migrating to Defender for Endpoint](switch-to-mde-overview#the-migration-process)**. This phase includes the following steps:

1. Reinstall/enable Microsoft Defender Antivirus on your endpoints.
2. Add Defender for Endpoint to the exclusion list for your existing solution.
3. Configure Defender for Endpoint Plan 1 or Plan 2.
4. Set up your device groups, device collections, and organizational units.

Important

If you want to run multiple security solutions side by side, see [Considerations for performance, configuration, and support](/en-us/defender-endpoint/mde-side-by-side).

You might have already configured mutual security exclusions for devices onboarded to Microsoft Defender for Endpoint. If you still need to set mutual exclusions to avoid conflicts, see [Add Microsoft Defender for Endpoint to the exclusion list for your existing solution](/en-us/defender-endpoint/switch-to-mde-phase-2#step-2-add-microsoft-defender-for-endpoint-to-the-exclusion-list-for-your-existing-solution).

## Step 1: Reinstall/enable Microsoft Defender Antivirus on your endpoints

On certain versions of Windows, Microsoft Defender Antivirus was likely uninstalled or disabled when your non-Microsoft antivirus/antimalware solution was installed. When endpoints running Windows are onboarded to Defender for Endpoint, Microsoft Defender Antivirus can run in passive mode alongside a non-Microsoft antivirus solution. To learn more, see [Antivirus protection with Defender for Endpoint](microsoft-defender-antivirus-compatibility#antivirus-protection-without-defender-for-endpoint).

As you're making the switch to Defender for Endpoint, you might need to take certain steps to reinstall or enable Microsoft Defender Antivirus. The following table describes what to do on your Windows clients and servers.

| Endpoint type | What to do |
| --- | --- |
| Windows clients (such as endpoints running Windows 10 and Windows 11) | In general, you don't need to take any action for Windows clients as the Microsoft Defender Antivirus feature cannot be removed. If you are running a non-Microsoft antimalware solution, Microsoft Defender Antivirus is most likely in the automatic disabled state at this point of the migration process. When client endpoints are onboarded to Defender for Endpoint, if those endpoints are still running a non-Microsoft antivirus solution, Microsoft Defender Antivirus goes into passive mode instead of the disabled state.If the non-Microsoft antivirus solution is then uninstalled, Microsoft Defender Antivirus goes into active mode automatically. |
| Windows servers | On Windows Server, you may need to reinstall the Microsoft Defender Antivirus feature and set it to passive mode manually. On Windows servers, when a non-Microsoft antivirus/antimalware is installed, Microsoft Defender Antivirus can't run alongside the non-Microsoft antivirus solution. In those cases, Microsoft Defender Antivirus is disabled or uninstalled manually.  To reinstall or enable Microsoft Defender Antivirus on Windows Server, perform the following tasks: - [Re-enable Defender Antivirus on Windows Server if it was disabled](enable-update-mdav-to-latest-ws#re-enable-microsoft-defender-antivirus-on-windows-server-if-it-was-disabled)- [Re-enable Defender Antivirus on Windows Server if it was uninstalled](enable-update-mdav-to-latest-ws#re-enable-microsoft-defender-antivirus-on-windows-server-if-it-was-uninstalled)- Set Microsoft Defender Antivirus to passive mode on Windows ServerIf you run into issues reinstalling or re-enabling Microsoft Defender Antivirus on Windows Server, see [Troubleshooting: Microsoft Defender Antivirus is getting uninstalled on Windows Server](switch-to-mde-troubleshooting#microsoft-defender-antivirus-is-getting-uninstalled-on-windows-server). If Microsoft Defender Antivirus features and installation files were previously removed from Windows Server operating systems, follow the guidance in [Configure a Windows Repair Source](/en-us/windows-hardware/manufacture/desktop/configure-a-windows-repair-source) to restore the feature installation files. |

Tip

To learn more about Microsoft Defender Antivirus states with non-Microsoft antivirus protection, see [Microsoft Defender Antivirus compatibility](microsoft-defender-antivirus-compatibility).

### Manually set Microsoft Defender Antivirus to passive mode on Windows Server

To set Microsoft Defender Antivirus to passive mode on Windows Server, complete the following steps.

Tip

You can now run Microsoft Defender Antivirus in passive mode on Windows Server 2012 R2 and 2016. For more information, see [Onboard Windows Server 2012 R2 and Windows Server 2016 to Microsoft Defender for Endpoint](onboard-server).

1. Open Registry Editor, and then navigate to `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Advanced Threat Protection`.
2. Edit (or create) a DWORD entry called **ForceDefenderPassiveMode**, and specify the following settings:

    - Set the DWORD's value to **1**.
    - Under **Base**, select **Hexadecimal**.

Note

To validate that passive mode was set as expected, search for **Event 5007** in the **Microsoft-Windows-Windows Defender Operational** log (located at `C:\Windows\System32\winevt\Logs`) and confirm that either the **ForceDefenderPassiveMode** or **PassiveMode** registry keys were set to **0x1**.

## Step 2: Add Microsoft Defender for Endpoint to the exclusion list for your existing solution

In the exclusion-list step, you add Defender for Endpoint to the exclusion list for your existing endpoint protection solution and any other security products your organization is using. Make sure to refer to your solution provider's documentation to add exclusions.

Select the tab for information about exclusions for that operating system.

The processes in this section are exclusively for Microsoft Defender for Endpoint for Windows platforms, including down-level OS. This list doesn't account for any other Windows communications requirements.

# [Windows](#tab/Windows)
The specific exclusions to configure depend on which version of Windows your endpoints or devices are running, and are listed in the following table.

| OS | Exclusions |
| --- | --- |
| Windows 11Windows 10, version 1803 or later (See Windows 10 release information)Windows 10, version 1703 or 1709 with KB4493441 installedWindows Server 2025  Azure Stack HCI OS, version 23H2 and later Windows Server 2022Windows Server 2019Windows Server, version 1803Windows Server 2016 running the modern unified solutionWindows Server 2012 R2 running the modern unified solution | **EDR exclusions**: `C:\Program Files\Windows Defender Advanced Threat Protection\MsSense.exe``C:\Program Files\Windows Defender Advanced Threat Protection\SenseCncProxy.exe``C:\Program Files\Windows Defender Advanced Threat Protection\SenseSampleUploader.exe``C:\Program Files\Windows Defender Advanced Threat Protection\SenseIR.exe``C:\Program Files\Windows Defender Advanced Threat Protection\SenseCM.exe``C:\Program Files\Windows Defender Advanced Threat Protection\SenseNdr.exe``C:\Program Files\Windows Defender Advanced Threat Protection\Classification\SenseCE.exe``C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\DataCollection``C:\Program Files\Windows Defender Advanced Threat Protection\SenseTVM.exe``C:\Program Files\Windows Defender Advanced Threat Protection\SenseTracer.exe``C:\Program Files\Windows Defender Advanced Threat Protection\SenseDlpProcessor.exe`**Registry path**:`HKLM\SOFTWARE\Microsoft\Windows Advanced Threat Protection\*`**Antivirus exclusions**:`C:\Program Files\Windows Defender\MsMpEng.exe``C:\Program Files\Windows Defender\NisSrv.exe``C:\Program Files\Windows Defender\ConfigSecurityPolicy.exe``C:\Program Files\Windows Defender\MpCmdRun.exe``C:\Program Files\Windows Defender\MpDefenderCoreService.exe``C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.*\MsMpEng.exe``C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.*\NisSrv.exe``C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.*\ConfigSecurityPolicy.exe``C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.*\MpCopyAccelerator.exe``C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.*\MpCmdRun.exe``C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.*\MpDefenderCoreService.exe``C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.*\mpextms.exe`**Endpoint Data Loss Prevention (Endpoint DLP) exclusions**:`C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.*\MpDlpService.exe``C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.*\MpDlpCmd.exe``C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.*\MipDlp.exe``C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.*\DlpUserAgent.exe` |
| Windows Server 2016 or Windows Server 2012 R2 running the [modern unified solution](/en-us/editor/MicrosoftDocs/defender-docs-pr/defender-endpoint%2Fswitch-to-mde-phase-2.md/main/76b249d7-f914-4c03-3eaf-48aa43b2fa4a/onboard-server.md) | The following **additional** exclusions are required after updating the Sense EDR component using [KB5005292](https://support.microsoft.com/servicing/Management-Tools/microsoft-defender/update/microsoft-defender-for-endpoint-update-for-edr-sensor): `C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Platform\*\MsSense.exe``C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Platform\*\SenseCnCProxy.exe``C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Platform\*\SenseIR.exe``C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Platform\*\SenseCE.exe``C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Platform\*\SenseSampleUploader.exe``C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Platform\*\SenseCM.exe``C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\DataCollection``C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Platform\*\SenseTVM.exe` |
| [Windows 8.1](/en-us/windows/release-health/status-windows-8.1-and-windows-server-2012-r2)[Windows 7](/en-us/windows/release-health/status-windows-7-and-windows-server-2008-r2-sp1)[Windows Server 2008 R2 SP1](/en-us/windows/release-health/status-windows-7-and-windows-server-2008-r2-sp1) | `C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Monitoring Host Temporary Files 6\45\MsSenseS.exe`( Monitoring Host Temporary Files 6\45 can be different numbered subfolders.) `C:\Program Files\Microsoft Monitoring Agent\Agent\AgentControlPanel.exe``C:\Program Files\Microsoft Monitoring Agent\Agent\HealthService.exe``C:\Program Files\Microsoft Monitoring Agent\Agent\HSLockdown.exe``C:\Program Files\Microsoft Monitoring Agent\Agent\MOMPerfSnapshotHelper.exe``C:\Program Files\Microsoft Monitoring Agent\Agent\MonitoringHost.exe``C:\Program Files\Microsoft Monitoring Agent\Agent\TestCloudConnection.exe` |

# [macOS](#tab/macOS)
For macOS devices, the following table lists processes to exclude in your non-Microsoft antivirus/antimalware solution:

| Process | Location |
| --- | --- |
| `wdavdaemon_enterprise`EDR engine | `/Library/Application Support/Microsoft/Defender/` |
| `wdavdaemon_unprivileged`Antivirus engine | `/Library/Application Support/Microsoft/Defender/` |
| `telemetryd_v1`Telemetry daemon for EDR | `/Library/Application Support/Microsoft/Defender/` |
| `Netext`Network extension | `/Library/SystemExtensions/*/com.microsoft.wdav.netext.systemextension/Contents/MacOS/` |
| `Epsext`Endpoint security extension | `/Library/SystemExtensions/*/com.microsoft.wdav.epsext.systemextension/Contents/MacOS/` |
| `msupdate`Microsoft AutoUpdate update tool | `/Library/Application\ Support/Microsoft/MAU2.0/Microsoft\ AutoUpdate.app/Contents/MacOS` |

# [Linux](#tab/Linux)
For Linux servers, the following table lists processes to exclude in your non-Microsoft antivirus/antimalware solution:

| Process | Location |
| --- | --- |
| `wdavdaemon`Core daemon (service). Uses FANotify for both antimalware and EDR purposes (TALPA on older RHEL). | `/opt/microsoft/mdatp/sbin/` |
| `wdavdaemon enterprise`EDR engine. Used for enrichment. | `/opt/microsoft/mdatp/sbin/` |
| `wdavdaemon unprivileged` Antivirus engine | `/opt/microsoft/mdatp/sbin/` |
| `crashpad_handler`Collects crash dumps | `/opt/microsoft/mdatp/sbin/` |
| `mdatp`Command line utility | `/opt/microsoft/mdatp/sbin/Wdavdaemonclient` |
| `mde_netfilter`Packet filter for Network protection, also used for response capabilities | `/opt/microsoft/mde_netfilter/sbin` |

---

Important

As a best practice, keep your organization's devices and endpoints up to date. Make sure to get the **[latest updates for Microsoft Defender for Endpoint and Microsoft Defender Antivirus](microsoft-defender-antivirus-updates)**, and keep your organization's operating systems and productivity apps up to date.

## Step 3: Configure Defender for Endpoint onboarding and protection settings

Configure your Defender for Endpoint capabilities before devices are onboarded.

> 
> Microsoft Intune is the recommended tool for configuring and distributing Defender for Endpoint features to devices. However, Intune is a separate product that isn't part of Defender for Endpoint, and it isn't included in all subscriptions. To use Intune, you need a subscription that includes it, or you can buy it separately as a standalone subscription or add-on. If you don't have Intune, you can use any of the other methods in this article. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).

- If you have Defender for Endpoint Plan 1, complete steps 1-5 in the following procedure.
- If you have Defender for Endpoint Plan 2, complete steps 1-7 in the following procedure.

1. Make sure Defender for Endpoint is provisioned. As a Security Administrator, go to the [Microsoft Defender portal](https://security.microsoft.com) and sign in. Then, in the navigation pane, select **Assets** &gt; **Devices**.

    The following table shows what your screen might look like and what it means.

    | Screen | What it means |
    | --- | --- |
    | [![Screenshot showing message that says hang on because MDE isn't provisioned yet.](media/mde-hangon-provisioning.png)](media/mde-hangon-provisioning.png#lightbox) | Defender for Endpoint isn't finished provisioning yet. You might have to wait a little while for the process to finish. |
    | [![Screenshot showing device inventory page with no device onboarded yet.](media/device-inventory-empty.png)](media/device-inventory-empty.png#lightbox) | Defender for Endpoint is provisioned. In this case, proceed to step 2, Turn on tamper protection. |
2. Turn on [tamper protection](tamper-protection-overview). We recommend turning tamper protection on for your whole organization. You can do this task in the [Microsoft Defender portal](https://security.microsoft.com).

    1. In the Microsoft Defender portal, choose **Settings** &gt; **Endpoints**.
    2. Go to **General** &gt; **Advanced features**, and then set the toggle for tamper protection to **On**.
    3. Select **Save**.

    For more information, see [Tamper protection](tamper-protection-overview).
3. If you're using either [Microsoft Intune](/en-us/intune/intune-service/fundamentals/what-is-intune) or [Microsoft Configuration Manager](/en-us/intune/configmgr/core/understand/introduction) to onboard devices and configure device policies, set up integration with Defender for Endpoint by following these steps: 

    1. In the [Microsoft Intune admin center](https://intune.microsoft.com), go to **Endpoint security**.
    2. Under **Setup**, choose **Microsoft Defender for Endpoint**.
    3. Under **Endpoint Security Profile Settings**, set the toggle for **Allow Microsoft Defender for Endpoint to enforce Endpoint Security Configurations** to **On**.
    4. Near the top of the screen, select **Save**.
    5. In the [Microsoft Defender portal](https://security.microsoft.com), choose **Settings** &gt; **Endpoints**.
    6. Scroll down to **Configuration management**, and select **Enforcement scope**.
    7. Set the toggle for **Use MDE to enforce security configuration settings from MEM** to **On**, and then select the options for both Windows client and Windows Server devices.
    8. If you're planning to use Configuration Manager, set the toggle for **Manage Security settings using Configuration Manager** to **On**. (If you need help with this step, see [Coexistence with Microsoft Configuration Manager](/en-us/intune/intune-service/protect/mde-security-integration#co-existence-with-microsoft-endpoint-configuration-manager).)
    9. Scroll down and select **Save**.
4. Configure your initial [attack surface reduction capabilities](attack-surface-reduction-overview). At a minimum, enable the [standard protection attack surface reduction (ASR) rules](attack-surface-reduction-rules-overview#asr-rules) that are listed in the following table right away:

    | Standard protection rules | Configuration methods |
    | --- | --- |
    | [Block credential stealing from the Windows local security authority subsystem](attack-surface-reduction-rules-reference#block-credential-stealing-from-the-windows-local-security-authority-subsystem)[Block abuse of exploited vulnerable signed drivers (Device)](attack-surface-reduction-rules-reference#block-abuse-of-exploited-vulnerable-signed-drivers)[Block persistence through WMI event subscription](attack-surface-reduction-rules-reference#block-persistence-through-wmi-event-subscription) | [Intune](attack-surface-reduction-rules-configure#configure-asr-rules-in-microsoft-intune) (Device configuration profiles or Endpoint Security policies) [Mobile Device Management (MDM)](attack-surface-reduction-rules-configure#configure-asr-rules-in-any-mdm-solution-using-the-policy-csp) (Use the [Defender/AttackSurfaceReductionRules policy CSP](/en-us/windows/client-management/mdm/policy-csp-defender#defender-attacksurfacereductionrules) configuration service provider (CSP) to individually enable and set the mode for each rule.)[Group Policy](attack-surface-reduction-rules-configure#configure-asr-rules-and-exclusions-in-group-policy) or [PowerShell](attack-surface-reduction-rules-configure#configure-asr-rules-in-powershell) (only if you're not using Intune, Configuration Manager, or another enterprise-level management platform) |

    For more information, see [Attack surface reduction capabilities](attack-surface-reduction-overview).
5. Configure your [next-generation protection capabilities](next-generation-protection).

    | Capability | Configuration methods |
    | --- | --- |
    | [Intune](/en-us/intune/intune-service/fundamentals/tutorial-walkthrough-endpoint-manager) | 1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** &gt; **Configuration profiles**, and then select the profile type you want to configure. If you haven't yet created a **Device restrictions** profile type, or if you want to create a new one, see [Configure device restriction settings in Microsoft Intune](/en-us/intune/intune-service/configuration/device-restrictions-configure).2. Select **Properties**, and then select **Configuration settings: Edit**3. Expand **Microsoft Defender Antivirus**.4. Enable **Cloud-delivered protection**.5. In the **Prompt users before sample submission** dropdown, select **Send all samples automatically**.6. In the **Detect potentially unwanted applications** dropdown, select **Enable** or **Audit**.7. Select **Review + save**, and then choose **Save**. **TIP**: For more information about Intune device profiles, including how to create and configure their settings, see [What are Microsoft Intune device profiles?](/en-us/intune/intune-service/configuration/device-profiles). |
    | [Configuration Manager](/en-us/intune/configmgr) | See [Create and deploy antimalware policies for Endpoint Protection in Configuration Manager](/en-us/intune/configmgr/protect/deploy-use/endpoint-antimalware-policies).  When you create and configure your antimalware policies, make sure to review the [real-time protection settings](/en-us/intune/configmgr/protect/deploy-use/endpoint-antimalware-policies#real-time-protection-settings) and [enable block at first sight](configure-block-at-first-sight-microsoft-defender-antivirus). |
    | [Advanced Group Policy Management](/en-us/microsoft-desktop-optimization-pack/agpm/) or [Group Policy Management Console](use-group-policy-microsoft-defender-antivirus) | 1. Go to **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus**.2. Look for a policy called **Turn off Microsoft Defender Antivirus**.3. Choose **Edit policy setting**, and make sure that policy is disabled. Disabling that policy enables Microsoft Defender Antivirus. (You might see *Windows Defender Antivirus* instead of *Microsoft Defender Antivirus* in some versions of Windows.) |
    | Control Panel in Windows | Follow the guidance here: [Company Portal device setting requirements for Windows](/en-us/intune/intune-service/user-help/update-device-settings-windows). (You might see *Windows Defender Antivirus* instead of *Microsoft Defender Antivirus* in some versions of Windows.) |

    *If you have Defender for Endpoint Plan 1, your initial setup and configuration is complete. If you have Defender for Endpoint Plan 2, continue through steps 6-7.*
6. Configure your endpoint detection and response (EDR) policies in the [Intune admin center](https://intune.microsoft.com). To get help with this task, see [Create EDR policies](/en-us/intune/intune-service/protect/endpoint-security-edr-policy#create-edr-policies).
7. Configure your automated investigation and remediation capabilities in the [Microsoft Defender portal](https://security.microsoft.com). To get help with this task, see [Configure automated investigation and remediation capabilities in Microsoft Defender for Endpoint](configure-automated-investigations-remediation).

    *At this point, initial setup and configuration of Defender for Endpoint Plan 2 is complete.*

## Step 4: Add your existing solution to the exclusion list for Microsoft Defender Antivirus

When configuring Microsoft Defender Antivirus exclusions, you add your existing solution to the list of exclusions for Microsoft Defender Antivirus. You can choose from several methods to add your exclusions to Microsoft Defender Antivirus, as listed in the following table:

| Method | What to do |
| --- | --- |
| [Intune](/en-us/intune/intune-service/fundamentals/tutorial-walkthrough-endpoint-manager) | 1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and sign in.2. Select **Devices** &gt; **Configuration profiles**, and then select the profile that you want to configure.3. Under **Manage**, select **Properties**.4. Select **Configuration settings: Edit**.5. Expand **Microsoft Defender Antivirus**, and then expand **Microsoft Defender Antivirus Exclusions**.6. Specify the files, folders, and processes to exclude from Microsoft Defender Antivirus scans. For reference, see [Microsoft Defender Antivirus exclusions](/en-us/intune/intune-service/configuration/device-restrictions-windows-10#microsoft-defender-antivirus-exclusions).7. Choose **Review + save**, and then choose **Save**. |
| [Microsoft Configuration Manager](/en-us/intune/configmgr/) | 1. Using the [Configuration Manager console](/en-us/intune/configmgr/core/servers/manage/admin-console), go to **Assets and Compliance** &gt; **Endpoint Protection** &gt; **Antimalware Policies**, and then select the policy that you want to modify.2. Specify exclusion settings for files, folders, and processes to exclude from Microsoft Defender Antivirus scans. |
| [Group Policy Object](/en-us/previous-versions/windows/desktop/Policy/group-policy-objects) | 1. On your Group Policy management computer, open the [Group Policy Management Console (GPMC)](/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-management-console). Right-click the Group Policy Object you want to configure and then select **Edit**.2. In the **Group Policy Management Editor**, go to **Computer configuration** and select **Administrative templates**.3. Expand the tree to **Windows components &gt; Microsoft Defender Antivirus &gt; Exclusions**. (You might see *Windows Defender Antivirus* instead of *Microsoft Defender Antivirus* in some versions of Windows.)4. Double-click the **Path Exclusions** setting and add the exclusions.5. Set the option to **Enabled**.6. Under the **Options** section, select **Show...**.7. Specify each folder on its own line under the **Value name** column. If you specify a file, make sure to enter a fully qualified path to the file, including the drive letter, folder path, filename, and extension. Enter **0** in the **Value** column.8. Select **OK**.9. Double-click the **Extension Exclusions** setting and add the exclusions.10. Set the option to **Enabled**.11. Under the **Options** section, select **Show...**.12. Enter each file extension on its own line under the **Value name** column. Enter **0** in the **Value** column.13. Select **OK**. |
| Local group policy object | 1. On the endpoint or device, open the Local Group Policy Editor.2. Go to **Computer Configuration** &gt; **Administrative Templates** &gt; **Windows Components** &gt; **Microsoft Defender Antivirus** &gt; **Exclusions**. (You might see *Windows Defender Antivirus* instead of *Microsoft Defender Antivirus* in some versions of Windows.)3. Specify your path and process exclusions. |
| Registry key | 1. Export the following registry key: `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Defender\exclusions`.2. Import the registry key. Here are two examples:- Local path: `regedit.exe /s c:\temp\MDAV_Exclusion.reg`- Network share: `regedit.exe /s \\FileServer\ShareName\MDAV_Exclusion.reg` |

[Learn more about exclusions for Microsoft Defender for Endpoint and Microsoft Defender Antivirus](defender-endpoint-exclusions-overview).

### Important considerations for Microsoft Defender Antivirus exclusions

When you add [exclusions to Microsoft Defender Antivirus scans](/en-us/defender-endpoint/microsoft-defender-antivirus-exclusions-configure), you should add path and process exclusions.

- *Path exclusions* exclude specific files and whatever those files access.
- *Process exclusions* exclude whatever a process touches, but doesn't exclude the process itself.
- List your process exclusions using their full path and not by their name only. (The name-only method is less secure.)
- If you list each executable (.exe) as both a path exclusion and a process exclusion, the process and whatever it touches are excluded.

## Step 5: Set up your device groups, device collections, and organizational units

Device groups, device collections, and organizational units enable your security team to manage and assign security policies efficiently and effectively. The following table describes each of these groups and how to configure them. Your organization might not use all three collection types.

Note

Device group creation is supported in Defender for Endpoint Plan 1 and Plan 2.

| Collection type | What to do |
| --- | --- |
| [Device groups](machine-groups) (formerly called *machine groups*) enable your security operations team to configure security capabilities, such as automated investigation and remediation.  Device groups are also useful for assigning access to those devices so that your security operations team can take remediation actions if needed.  Device groups are created while the attack was detected and stopped, alerts, such as an "initial access alert," were triggered and appeared in the [Microsoft Defender portal](/en-us/defender-xdr/microsoft-365-defender). | 1. Go to the [Microsoft Defender portal](https://security.microsoft.com).2. In the navigation pane on the left, choose **Settings** &gt; **Endpoints** &gt; **Permissions** &gt; **Device groups**.3. Choose **+ Add device group**.4. Specify a name and description for the device group.5. In the **Automation level** list, select an option. (We recommend **Full - remediate threats automatically**.) To learn more about the various automation levels, see [How threats are remediated](automated-investigations#how-threats-are-remediated).6. Specify conditions for a matching rule to determine which devices belong to the device group. For example, you can choose a domain, OS versions, or even use [device tags](machine-tags).7. On the **User access** tab, specify roles that should have access to the devices that are included in the device group.8. Choose **Done**. |
| [Device collections](/en-us/intune/configmgr/core/clients/manage/collections/introduction-to-collections) enable your security operations team to manage applications, deploy compliance settings, or install software updates on the devices in your organization.  Device collections are created by using [Configuration Manager](/en-us/intune/configmgr/). | Follow the steps in [Create a collection](/en-us/intune/configmgr/core/clients/manage/collections/create-collections#bkmk_create). |
| [Organizational units](/en-us/azure/active-directory-domain-services/create-ou) enable you to logically group objects such as user accounts, service accounts, or computer accounts.  You can then assign administrators to specific organizational units, and apply group policy to enforce targeted configuration settings.  Organizational units are defined in [Microsoft Entra Domain Services](/en-us/azure/active-directory-domain-services). | Follow the steps in [Create an Organizational Unit in a Microsoft Entra Domain Services managed domain](/en-us/azure/active-directory-domain-services/create-ou). |