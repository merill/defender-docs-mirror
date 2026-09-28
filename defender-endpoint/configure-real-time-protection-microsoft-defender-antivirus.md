---
layout: Conceptual
title: Configure Microsoft Defender Antivirus always-on protection - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/configure-real-time-protection-microsoft-defender-antivirus
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Configure Microsoft Defender Antivirus always-on protection with supported management tools to monitor files, programs, and behavior for threats.
ms.service: defender-endpoint
ms.subservice: ngp
ms.localizationpriority: medium
author: chrisda
ms.author: chrisda
ms.reviewer: yongrhee
ms.topic: how-to
ms.date: 2026-09-02T00:00:00.0000000Z
ms.custom: nextgen, msecd-doc-authoring-1015
ms.collection:
- m365-security
- tier2
- mde-ngp
ai-usage: ai-assisted
locale: en-us
document_id: 020b00a8-6660-e16f-c92c-e0615753e9b7
document_version_independent_id: 020b00a8-6660-e16f-c92c-e0615753e9b7
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/configure-real-time-protection-microsoft-defender-antivirus.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-real-time-protection-microsoft-defender-antivirus
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/configure-real-time-protection-microsoft-defender-antivirus.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: dc080164-0e44-cb57-93ca-cd7d5915e422
---

# Configure Microsoft Defender Antivirus always-on protection - Microsoft Defender for Endpoint | Microsoft Learn

Always-on protection in Microsoft Defender Antivirus uses real-time protection, behavior monitoring, and heuristics to detect suspicious and malicious activity. Security administrators can configure these capabilities on Windows devices by using Microsoft Intune, the Microsoft Defender portal, Microsoft Configuration Manager, or Group Policy. You can also use PowerShell or the Windows Security app. Review the supported operating systems before you begin.

Note

[Tamper protection](tamper-protection-overview) helps keep always-on protection and other security settings from being changed. As a result, when tamper protection is enabled, any changes made to [tamper-protected settings](tamper-protection-overview#what-happens-when-tamper-protection-is-turned-on) are ignored. To temporarily change tamper-protected settings for testing or diagnostics, use [troubleshooting mode](troubleshooting-mode-enable). After troubleshooting mode ends, the settings return to their configured values. To make permanent changes, update the policy in the management tool that configures the device.

If a file containing a threat is added to an Azure file share, the file isn't remediated immediately. Real-time protection detects the threat when a user opens the file.

## Prerequisites

### Supported operating systems

The following operating systems support always-on protection:

- Windows

To use the Intune procedure, enroll Windows devices in Intune.

Before using Configuration Manager, configure it for Endpoint Protection. For more information, see [Configure Endpoint Protection in Configuration Manager](/en-us/intune/configmgr/protect/deploy-use/endpoint-protection-configure).

## Configure always-on protection settings in Microsoft Intune

Microsoft Intune is the recommended tool for configuring and distributing Defender for Endpoint features to devices. However, Intune is a separate product that isn't part of Defender for Endpoint, and it isn't included in all subscriptions. To use Intune, you need a subscription that includes it, or you can buy it separately as a standalone subscription or add-on. If you don't have Intune, you can use any of the other methods in this article. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).

To configure always-on protection settings in Microsoft Intune, use an endpoint security **Antivirus** policy. For detailed instructions, see [Create endpoint security policies](/en-us/intune/intune-service/protect/endpoint-security-policy#create-endpoint-security-policies) or [Modify existing policies](/en-us/intune/device-configuration/endpoint-security/manage-policies#modify-existing-policies) (links open new tabs in the Intune documentation).

When you create the policy, use these specific settings:

- **Policy type**: Go to **Manage** &gt; **Antivirus** on the **Endpoint security | Overview** page at [https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/~/overview](https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/%7E/overview), and then select ![](media/defender-portal-icon-create.png)**Create policy**.
- **Platform**: Select **Windows**.
- **Profile**: Select **Microsoft Defender Antivirus**.

When you create or modify the policy, use these specific settings on the **Configuration settings** tab:

- In the **Defender**section, configure the following settings:
    - **Allow Real-Time Monitoring**: Select **Allowed**.
    - **Allow On Access Protection**: Select **Allowed**.
    - **Real Time Scan Direction**: Select **Monitor all files (bi-directional)**.
    - **Allow behavior monitoring**: Select **Allowed**.

The Microsoft Defender Antivirus profile doesn't include a separate setting for heuristics. Heuristics are part of real-time protection. For descriptions of all available Windows settings, options, defaults, recommendations, and CSP mappings, see [Configure Microsoft Defender Antivirus using Microsoft Intune](use-intune-config-manager-microsoft-defender-antivirus#policies-and-settings).

## Configure always-on protection settings in the Microsoft Defender portal

If your organization [manages endpoint security policies in the Microsoft Defender portal](endpoint-security-policies-configure), use a Microsoft Defender Antivirus policy to configure always-on protection.

For detailed instructions, see [Create an endpoint security policy](endpoint-security-policies-configure#create-an-endpoint-security-policy) or [Edit an endpoint security policy](endpoint-security-policies-configure#edit-an-endpoint-security-policy) (links open new tabs).

When you create the policy, use these specific settings:

- **Policy type**: On the **Windows policies** tab of the **Endpoint security policies** page in the Microsoft Defender portal at https://security.microsoft.com/policy-inventory, select ![](media/defender-portal-icon-create.png)**Create new policy**.
- **Select platform**: Select **Windows**.
- **Select template**: Select **Microsoft Defender Antivirus**.

When you create or modify the policy, use these specific settings on the **Configuration settings** tab:

- In the **Defender**section, configure the following settings:
    - **Allow Real-Time Monitoring**: Select **Allowed**.
    - **Allow On Access Protection**: Select **Allowed**.
    - **Real Time Scan Direction**: Select **Monitor all files (bi-directional)**.
    - **Allow behavior monitoring**: Select **Allowed**.

The Microsoft Defender Antivirus template doesn't include a separate setting for heuristics. Heuristics are part of real-time protection.

## Configure always-on protection settings in Microsoft Configuration Manager

For instructions to create and deploy an antimalware policy, see [Endpoint Protection antimalware policies in Configuration Manager](/en-us/intune/configmgr/protect/deploy-use/endpoint-antimalware-policies).

In the **Real-time protection** settings of the antimalware policy, configure the following settings:

- **Enable real-time protection**: Select **Yes**.
- **Monitor file and program activity on your computer**: Select **Yes**.
- **Scan system files**: Select **Scan incoming and outgoing files**.
- **Enable behavior monitoring**: Select **Yes**.

## Configure always-on protection settings in Group Policy

You can use Group Policy to manage some Microsoft Defender Antivirus settings. If [tamper protection](tamper-protection-overview) is enabled in your organization, any changes made to [tamper-protected settings](tamper-protection-overview#what-happens-when-tamper-protection-is-turned-on) are ignored. You can't turn off tamper protection by using Group Policy.

To temporarily change tamper-protected settings for testing or diagnostics, use [troubleshooting mode](troubleshooting-mode-enable). After troubleshooting mode ends, the settings return to their configured values. To make permanent changes, use a management tool that supports changes to tamper-protected settings, such as Intune.

The following procedure applies to Windows devices.

1. In Centralized Group Policy, open the [Group Policy Management Console (GPMC)](/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-management-console) on your Group Policy management computer.
2. In the GPMC console tree, expand **Group Policy Objects** in the forest and domain containing the Group Policy Object (GPO) you want to edit.
3. Right-click the GPO, and then select **Edit**.
4. In the **Group Policy Management Editor**, go to **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus**.
5. In the details pane of **Microsoft Defender Antivirus**, the folders used to configure always-on protection are:

    - **Real-time Protection**: Configure real-time protection settings.
    - **Scan**: Turn on heuristics.

    To open and configure a setting, use any of the following methods:

    - Double-click the setting.
    - Right-click the setting, and then select **Edit**.
    - Select the setting, and then select **Action** &gt; **Edit**.

Tip

You can also configure Group Policy locally on individual devices by using the Local Group Policy Editor (`gpedit.msc`). Navigate to the same path: **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus**.

Configure the settings as described in the following subsections.

### Configure real-time protection settings in Group Policy

If a setting described in this article isn't available in Group Policy Management Editor, update the Administrative Templates in your Group Policy Central Store. The Central Store isn't updated automatically. For instructions, see [How to create and manage the Central Store for Group Policy Administrative Templates in Windows](/en-us/troubleshoot/windows-client/group-policy/create-and-manage-central-store).

Configure the following policies to turn on real-time and behavior monitoring:

| Policy | Value |
| --- | --- |
| Turn off real-time protection | Disabled |
| Configure monitoring for incoming and outgoing file and program activity | Enabled, bi-directional (full on-access) |
| Turn on behavior monitoring | Enabled |
| Monitor file and program activity on your computer | Enabled |

1. Go to **Microsoft Defender Antivirus** &gt; **Real-time Protection**.
2. In the details pane of **Real-time Protection**, select a policy setting to view its description and supported options in the help pane. For a list of the settings and links to related guidance, see [Group Policy settings and resources](use-group-policy-microsoft-defender-antivirus#group-policy-settings-and-resources).
3. Open each policy setting in the table, configure the specified value, and then select **OK**.

### Turn on heuristics in Group Policy

Enable the heuristics policy in the **Scan** folder:

1. Go to **Microsoft Defender Antivirus** &gt; **Scan**.
2. In the details pane of **Scan**, open **Turn on heuristics**.
3. Select **Enabled**, and then select **OK**.

### Disable real-time protection in Group Policy

Warning

Disabling real-time protection drastically reduces the protection on your endpoints and isn't recommended. If [tamper protection](tamper-protection-overview) is enabled, you can't turn off real-time protection by using Group Policy. To turn off real-time protection temporarily for testing or diagnostics, use [troubleshooting mode](troubleshooting-mode-enable). After troubleshooting mode ends, real-time protection returns to its configured value.

To disable real-time protection by using Group Policy:

1. Go to **Microsoft Defender Antivirus** &gt; **Real-time Protection**.
2. In the details pane of **Real-time Protection**, open **Turn off real-time protection**.
3. Select **Enabled**, and then select **OK**.

## Configure always-on protection settings using PowerShell

Run the commands in an elevated PowerShell session (a PowerShell window you opened by selecting **Run as administrator**).

The following command turns on real-time monitoring and behavior monitoring, and configures Microsoft Defender Antivirus to scan incoming and outgoing files:

```powershell
Set-MpPreference -DisableRealtimeMonitoring $false -DisableBehaviorMonitoring $false -RealTimeScanDirection Both
```

The following command displays the configured values:

```powershell
Get-MpPreference | Select-Object DisableRealtimeMonitoring, DisableBehaviorMonitoring, RealTimeScanDirection
```

Verify that *DisableRealtimeMonitoring* and *DisableBehaviorMonitoring* are set to `False`, and *RealTimeScanDirection* is set to `0`.

For detailed syntax and parameter information, see [**Set-MpPreference**](/en-us/powershell/module/defender/set-mppreference) and [**Get-MpPreference**](/en-us/powershell/module/defender/get-mppreference).

## Turn on real-time protection in the Windows Security app

You can use the [Windows Security app](https://support.microsoft.com/Windows/Security/Windows-Security/stay-protected-with-the-windows-security-app) to turn on real-time protection on an individual device. It doesn't provide separate controls for all the always-on protection settings described in this article.

To turn on real-time protection in the Windows Security app:

1. In the **Windows security** app on the device, go to **Virus & threat protection**.
2. In the **Virus & threat protection** pane, in the **Virus & threat protection settings** section, select **Manage settings**.
3. In the **Virus & threat protection settings** pane, slide the **Real-time protection** toggle to ![](media/toggle-on.png)**On**.

If your organization manages real-time protection, the **Real-time protection** setting might be unavailable. If you turn off real-time protection, it turns on again automatically after a short delay.

For more information, see [Microsoft Defender Antivirus in the Windows Security app](microsoft-defender-security-center-antivirus).