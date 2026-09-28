---
layout: Conceptual
title: Turn on network protection - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/enable-network-protection
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to configure and verify Microsoft Defender Antivirus network protection on Windows devices by using supported management tools.
ms.service: defender-endpoint
ms.localizationpriority: medium
ms.date: 2026-09-02T00:00:00.0000000Z
ms.topic: how-to
author: paulinbar
ms.author: painbar
ms.reviewer: tdoucett
ms.subservice: asr
ms.collection:
- m365-security
- tier2
- mde-asr
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1015
locale: en-us
document_id: 1cb92240-7ac9-b8e2-677c-9f99d0fc95a5
document_version_independent_id: 1cb92240-7ac9-b8e2-677c-9f99d0fc95a5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/enable-network-protection.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: enable-network-protection
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/enable-network-protection.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 68ed54c0-3984-87b9-0036-653fd8df58c9
---

# Turn on network protection - Microsoft Defender for Endpoint | Microsoft Learn

[Network protection](network-protection) helps prevent apps from connecting to dangerous domains that might host phishing scams, exploits, and other malicious content on the internet. Security administrators can configure network protection by using Microsoft Intune, the Microsoft Defender portal, mobile device management (MDM), Microsoft Configuration Manager, Group Policy, or PowerShell.

Before you enable network protection in block mode, use [audit mode](evaluate-network-protection) in a test environment to identify apps that would be blocked.

Before you begin, review the supported operating systems and Microsoft Defender Antivirus requirements in Prerequisites.

## Prerequisites

### Supported operating systems

The procedures in this article apply to the following operating systems:

- Windows 10, version 1709 or later, or Windows 11 (Pro or Enterprise).
- Windows Server 2012 R2, Windows Server 2016, or Windows Server, version 1803 or later.

Network protection is also supported on other platforms. For platform-specific instructions, see [Network protection for Linux](network-protection-linux) and [Network protection for macOS](network-protection-macos).

### Microsoft Defender Antivirus requirements

Network protection requires Microsoft Defender Antivirus in active mode with real-time protection enabled.

- On Windows 10, Windows 11, and Windows Server, version 1803 or later, turn on [real-time protection](configure-real-time-protection-microsoft-defender-antivirus), [behavior monitoring](behavior-monitor), and [cloud-delivered protection](cloud-protection-configure).
- On Windows Server 2012 R2 and Windows Server 2016 with the [modern unified solution](onboard-server#functionality-in-the-modern-unified-solution-for-windows-server-2016-and-windows-server-2012-r2), use Microsoft Defender Antivirus platform update version `4.18.2001.x.x` or later.

### Windows Server requirements

Note

Windows Server supports network protection when you configure it directly by using Microsoft Configuration Manager, Group Policy, or PowerShell. The Microsoft Intune and Microsoft Defender portal procedures in this article can manage supported Windows Server versions through [Defender for Endpoint security settings management](endpoint-security-policies-configure).

To onboard and manage servers through Defender for Endpoint, you need an eligible server license. If your organization accesses Defender for Endpoint only through Defender for Servers, you also need at least one active Defender for Endpoint user subscription license to use security settings management. For more information, see [Server plans](onboard-server#server-plans) and [Licensing and subscriptions for security settings management](/en-us/intune/device-security/microsoft-defender/security-settings-management#licensing-and-subscriptions).

Important

On Windows Server, network protection is an opt-in capability. Before you apply a network protection policy, configure the following settings as described in Configure network protection by using PowerShell:

- On all Windows servers, set *AllowNetworkProtectionOnWinServer* to `$true`.
- On Windows Server 2012 R2 and Windows Server 2016 with the modern unified solution, also set *AllowNetworkProtectionDownLevel* to `$true`.

Without these settings, Microsoft Defender Antivirus ignores the network protection configuration.

## Configure network protection in Microsoft Intune

Microsoft Intune is the recommended tool for configuring and distributing Defender for Endpoint features to devices. However, Intune is a separate product that isn't part of Defender for Endpoint, and it isn't included in all subscriptions. To use Intune, you need a subscription that includes it, or you can buy it separately as a standalone subscription or add-on. If you don't have Intune, you can use any of the other methods in this article. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).

You can enable network protection in Microsoft Intune by using an antivirus policy or a security baseline.

### Configure network protection in Intune using endpoint security policies

To configure network protection by using a Microsoft Intune endpoint security **Antivirus** policy, see [Create endpoint security policies](/en-us/intune/intune-service/protect/endpoint-security-policy#create-endpoint-security-policies) or [Modify existing policies](/en-us/intune/device-configuration/endpoint-security/manage-policies#modify-existing-policies) (links open new tabs in the Intune documentation).

When you create the policy, use these specific settings:

- **Policy type**: Go to **Manage** &gt; **Antivirus** on the **Endpoint security | Overview** page at [https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/~/overview](https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/%7E/overview), and then select ![](media/defender-portal-icon-create.png)**Create policy**.
- **Platform**: Select **Windows**.
- **Profile**: Select **Microsoft Defender Antivirus**.

When you create or modify the policy, use these specific settings on the **Configuration settings** tab:

- **Enable network protection** in the **Defender**section: Select one of the following values:
    - **Enabled (block mode)**: Blocks connections to malicious or suspicious domains.
    - **Enabled (audit mode)**: Records network protection events without blocking connections.
    - **Disabled**: Turns off network protection.
    - **Not configured**: Leaves the setting unmanaged by the policy.

For more information about Microsoft Defender Antivirus profiles in Intune, see [Antivirus policy for endpoint security in Intune](/en-us/intune/intune-service/protect/endpoint-security-antivirus-policy).

### Configure network protection in Intune using a security baseline

Important

Security baselines apply a broad set of Microsoft-recommended settings to your devices. If your devices aren't already managed by a security baseline, don't deploy a baseline only to configure network protection. Use Intune endpoint security policies instead.

To configure network protection as part of a security baseline in Microsoft Intune, see [Create a profile for a security baseline](/en-us/intune/intune-service/protect/security-baselines-configure#create-a-profile-for-a-security-baseline) or [Edit a security baseline](/en-us/intune/device-security/security-baselines/configure-baselines#to-edit-a-baseline) (links open new tabs in the Intune documentation).

When you create the profile, select **Microsoft Defender for Endpoint Security Baseline**.

When you create or modify the profile, use these specific settings on the **Configuration settings** tab:

- **Enable Network Protection** in the **Defender** section: Select **Enabled (block mode)** or **Enabled (audit mode)**.

For more information about security baselines in Microsoft Intune, see [Learn about Intune security baselines for Windows devices](/en-us/intune/intune-service/protect/security-baselines).

## Configure network protection in the Microsoft Defender portal

If your organization [manages endpoint security policies in the Microsoft Defender portal](endpoint-security-policies-configure), use a Microsoft Defender Antivirus policy to configure network protection.

Tip

This method requires the **Security Administrator** role in Microsoft Entra ID.

For detailed instructions, see [Create an endpoint security policy](endpoint-security-policies-configure#create-an-endpoint-security-policy) or [Edit an endpoint security policy](endpoint-security-policies-configure#edit-an-endpoint-security-policy) (links open new tabs).

When you create the policy, use these specific settings:

- **Policy type**: On the **Windows policies** tab of the **Endpoint security policies** page in the Microsoft Defender portal at https://security.microsoft.com/policy-inventory, select ![](media/defender-portal-icon-create.png)**Create new policy**.
- **Select platform**: Select **Windows**.
- **Select template**: Select **Microsoft Defender Antivirus**.

When you create or modify the policy, configure **Enable network protection** in the **Defender** section on the **Configuration settings** tab:

- **Enabled (block mode)**: Blocks connections to malicious or suspicious domains. Block mode is required for IP address and URL indicators and web content filtering.
- **Enabled (audit mode)**: Records network protection events without blocking connections.
- **Disabled (Default)**: Turns off network protection.
- **Not configured**: Leaves the setting unmanaged by the policy.

For Windows Server 2016 and Windows Server 2012 R2, also set **Allow Network Protection Down Level** in the **Threat Severity Default Action** section to **Network protection will be enabled downlevel**.

The policy also contains the following optional network protection settings:

- **Allow Datagram Processing On Win Server**: For server roles that generate high volumes of UDP traffic, select **Datagram processing on Windows Server is disabled (Default)**. Examples include domain controllers, DNS servers, file servers, SQL Server, and Exchange Server.
- **Disable DNS over TCP parsing**: Select whether DNS over TCP parsing is enabled or disabled.
- **Disable HTTP parsing**: Select whether HTTP parsing is enabled or disabled.
- **Disable SSH parsing**: Select whether SSH parsing is enabled or disabled.
- **Disable TLS parsing**: Select whether TLS parsing is enabled or disabled.
- **[Deprecated] Enable DNS Sinkhole**: Select whether DNS sinkhole is enabled or disabled.

## Configure network protection in any MDM solution using the Policy CSP

Tip

Before you configure network protection through MDM, [update the Microsoft Defender Antivirus platform](microsoft-defender-antivirus-updates).

The Policy configuration service provider (CSP) enables organizations to configure policies on Windows devices by using any mobile device management (MDM) solution, not just Microsoft Intune. For more information, see [Policy CSP](/en-us/windows/client-management/mdm/policy-configuration-service-provider).

Configure network protection by using the [EnableNetworkProtection](/en-us/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection) CSP with the following settings:

**OMA-URI path**: `./Device/Vendor/MSFT/Policy/Config/Defender/EnableNetworkProtection`**Data type**: Integer**Value**:

- `0`: Network protection is disabled.
- `1`: Network protection is enabled in block mode.
- `2`: Network protection is enabled in audit mode.

## Configure network protection in Microsoft Configuration Manager

To configure network protection in Microsoft Configuration Manager, use a Windows Defender Exploit Guard policy. For detailed instructions, see [Create and deploy an Exploit Guard policy](/en-us/intune/configmgr/protect/deploy-use/create-deploy-exploit-guard-policy).

When you create or modify the policy, use these specific settings:

- **Exploit Guard components** (new policies only): Select **Network protection**.
- **Configure network protection** (new and existing policies): Select **Block**, **Audit**, or **Disabled**.

### Remove Configuration Manager Exploit Guard settings

When you deploy an Exploit Guard policy by using Configuration Manager, the settings remain on the client if you remove the deployment. The client records `Delete not supported` in the `ExploitGuardHandler.log` file.

To remove the Exploit Guard settings, run the following PowerShell script in the `SYSTEM` context. The script clears the Defender and Exploit Guard MDM policy values, including attack surface reduction rules, controlled folder access, and network protection:

```powershell
$defenderObject = Get-WmiObject -Namespace "root/cimv2/mdm/dmmap" -Class "MDM_Policy_Config01_Defender02" -Filter "InstanceID='Defender' and ParentID='./Vendor/MSFT/Policy/Config'"

$defenderObject.AttackSurfaceReductionRules = $null

$defenderObject.AttackSurfaceReductionOnlyExclusions = $null

$defenderObject.EnableControlledFolderAccess = $null

$defenderObject.ControlledFolderAccessAllowedApplications = $null

$defenderObject.ControlledFolderAccessProtectedFolders = $null

$defenderObject.EnableNetworkProtection = $null

$defenderObject.Put()

$exploitGuardObject = Get-WmiObject -Namespace "root/cimv2/mdm/dmmap" -Class "MDM_Policy_Config01_ExploitGuard02" -Filter "InstanceID='ExploitGuard' and ParentID='./Vendor/MSFT/Policy/Config'"

$exploitGuardObject.ExploitProtectionSettings = $null

$exploitGuardObject.Put()
```

## Configure network protection by using Group Policy

To configure network protection in a domain environment, follow these steps:

1. Open the [Group Policy Management Console (GPMC)](/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-management-console) on your Group Policy management computer.
2. In the GPMC console tree, expand **Group Policy Objects** in the forest and domain that contain the Group Policy object (GPO) you want to edit.
3. Right-click the GPO, and then select **Edit**.
4. In the **Group Policy Management Editor**, go to **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **Microsoft Defender Exploit Guard** &gt; **Network protection**.

    Note

    Group Policy paths on older versions of Windows might use *Windows Defender Antivirus* instead of *Microsoft Defender Antivirus*. Both names refer to the same policy location.
5. In the **Network protection** details pane, open **Prevent users and apps from accessing dangerous websites**.
6. Select **Enabled**, and then select one of the following options:

    - **Block**: Blocks access to malicious IP addresses and domains.
    - **Disable (Default)**: Turns off network protection.
    - **Audit Mode**: Records an event when a user visits a malicious IP address or domain without blocking access.

    Select **OK**.

Tip

You can also configure Group Policy locally on an individual device by using the Local Group Policy Editor (`gpedit.msc`). Go to the same policy path, and then configure **Prevent users and apps from accessing dangerous websites**.

## Configure network protection by using PowerShell

To configure network protection in PowerShell on Windows clients, use the following syntax in an elevated PowerShell session (a PowerShell prompt you opened by selecting **Run as administrator**):

```powershell
Set-MpPreference -EnableNetworkProtection <Disabled | Enabled | AuditMode>
```

- `Disabled`: Turns off network protection.
- `Enabled`: Turns on network protection in block mode, which prevents connections to malicious or suspicious domains.
- `AuditMode`: Turns on network protection in audit mode, which records events for connections to malicious domains without blocking them.

To configure network protection in PowerShell on Windows servers, use the following syntax in an elevated PowerShell session:

- **Windows Server 2019 or later**:

    ```powershell
    Set-MpPreference -AllowNetworkProtectionOnWinServer $true [-AllowDatagramProcessingOnWinServer $false] -EnableNetworkProtection <Disabled | Enabled | AuditMode>
    ```
- **Windows Server 2016** or **Windows Server 2012 R2** with the [modern unified solution for Microsoft Defender for Endpoint](onboard-server#functionality-in-the-modern-unified-solution-for-windows-server-2016-and-windows-server-2012-r2):

    ```powershell
    Set-MpPreference -AllowNetworkProtectionDownLevel $true -AllowNetworkProtectionOnWinServer $true [-AllowDatagramProcessingOnWinServer $false] -EnableNetworkProtection <Disabled | Enabled | AuditMode>
    ```

Important

Set *AllowDatagramProcessingOnWinServer* to `$false` on server roles that generate high volumes of UDP traffic, such as domain controllers, DNS servers, file servers, SQL Server, and Exchange Server. Enabling datagram processing on these servers can reduce network performance and reliability.

For detailed syntax and parameter information, see [**Set-MpPreference**](/en-us/powershell/module/defender/set-mppreference).

## Verify network protection settings on devices

Use one of the following methods to verify the network protection settings on a device:

- **PowerShell**:

    Run the following command in PowerShell:

    ```powershell
    Get-MpPreference | Select-Object EnableNetworkProtection, AllowNetworkProtectionOnWinServer, AllowNetworkProtectionDownLevel, AllowDatagramProcessingOnWinServer
    ```

    - *EnableNetworkProtection*:
        - `0`: Network protection is **off**.
        - `1`: Network protection is on in **Block** mode.
        - `2`: Network protection is on in **Audit** mode.
    - *AllowNetworkProtectionOnWinServer*: On Windows servers, the value should be `True`.
    - *AllowNetworkProtectionDownLevel*: On Windows Server 2016 and Windows Server 2012 R2 with the unified agent, the value should be `True`.
    - *AllowDatagramProcessingOnWinServer*: On server roles that generate high volumes of UDP traffic, the value should be `False`.
- **Registry Editor**:

    1. Open Registry Editor. For example, run `regedit.exe`.
    2. Go to **HKEY\_LOCAL\_MACHINE** &gt; **SOFTWARE** &gt; **Policies** &gt; **Microsoft** &gt; **Windows Defender** &gt; **Policy Manager**.

        If that path doesn't exist, go to **HKEY\_LOCAL\_MACHINE** &gt; **SOFTWARE** &gt; **Microsoft** &gt; **Windows Defender** &gt; **Windows Defender Exploit Guard** &gt; **Network Protection**.
    3. Select **EnableNetworkProtection** to see the current state of network protection on the device:

        - `0`: Network protection is **off**.
        - `1`: Network protection is on in **Block** mode.
        - `2`: Network protection is on in **Audit** mode.

        [![Screenshot of the Network Protection registry key in Registry Editor.](/en-us/defender/media/95341270-b738b280-08d3-11eb-84a0-16abb140c9fd.png)](/en-us/defender/media/95341270-b738b280-08d3-11eb-84a0-16abb140c9fd.png#lightbox)