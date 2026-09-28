---
layout: Conceptual
title: Configure cloud protection in Microsoft Defender Antivirus - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/cloud-protection-configure
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Configure Microsoft Defender Antivirus cloud protection, automatic sample submission, and cloud blocking levels by using supported management tools.
ms.service: defender-endpoint
ms.localizationpriority: medium
ms.topic: how-to
author: chrisda
ms.author: chrisda
ms.date: 2026-09-10T00:00:00.0000000Z
ms.reviewer: pahuijbr
ms.custom: nextgen, msecd-doc-authoring-1015
ms.subservice: ngp
ms.collection:
- m365-security
- tier2
- mde-ngp
ai-usage: ai-assisted
locale: en-us
document_id: 553354c3-28b8-81ce-0672-2d2b92e99446
document_version_independent_id: 553354c3-28b8-81ce-0672-2d2b92e99446
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/cloud-protection-configure.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: cloud-protection-configure
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/cloud-protection-configure.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 0f3c7d77-c1b8-530d-f87f-c3422fa6af63
---

# Configure cloud protection in Microsoft Defender Antivirus - Microsoft Defender for Endpoint | Microsoft Learn

[Cloud protection in Microsoft Defender Antivirus](cloud-protection-microsoft-defender-antivirus) delivers accurate, real-time, and intelligent protection. Use this article to turn on cloud protection and configure how aggressively Microsoft Defender Antivirus blocks suspicious files. Cloud protection is enabled by default, and we recommend keeping it turned on.

Note

[Tamper protection](tamper-protection-overview) helps prevent unauthorized changes to cloud protection and other security settings. When tamper protection is turned on, changes to [tamper-protected settings](tamper-protection-overview#what-happens-when-tamper-protection-is-turned-on) are ignored. If tamper protection blocks a required change on a device, use [troubleshooting mode](troubleshooting-mode-enable) to temporarily disable tamper protection. After troubleshooting mode ends, changes to tamper-protected settings revert to their configured state.

## Prerequisites

### Supported operating systems

The following operating systems support cloud protection:

- Windows

For information about the network-connectivity requirements for the cloud protection service, see [Configure and validate network connections](configure-network-connections-microsoft-defender-antivirus).

## Why cloud protection should be turned on

Microsoft Defender Antivirus cloud protection helps protect against malware on your endpoints and throughout your network. We recommend keeping cloud protection turned on because certain security features and capabilities in Microsoft Defender for Endpoint only work when cloud protection is enabled.

[![Diagram of Defender for Endpoint features that depend on cloud protection, such as tamper protection, block at first sight, and ASR rules.](media/mde-cloud-protection.png)](media/mde-cloud-protection.png#lightbox)

The following table summarizes the features and capabilities that depend on cloud protection:

| Feature or capability | Subscription requirement |
| --- | --- |
| **Checking against metadata in the cloud**. The Microsoft Defender Antivirus cloud service uses machine learning models as an extra layer of defense. These machine learning models include metadata, so when a suspicious or malicious file is detected, its metadata is checked. To learn more, see [Blog: Get to know the advanced technologies at the core of Microsoft Defender for Endpoint next-generation protection](https://www.microsoft.com/security/blog/2019/06/24/inside-out-get-to-know-the-advanced-technologies-at-the-core-of-microsoft-defender-atp-next-generation-protection/) | Microsoft Defender for Endpoint Plan 1 or Plan 2 (Standalone or included in a plan like Microsoft 365 E3 or E5) |
| **[Cloud protection and sample submission](cloud-protection-microsoft-antivirus-sample-submission)**. Files and executables can be sent to the Microsoft Defender Antivirus cloud service for detonation and analysis. Automatic sample submission relies on cloud protection, although it can also be configured as a standalone setting.To learn more, see [Cloud protection and sample submission in Microsoft Defender Antivirus](cloud-protection-microsoft-antivirus-sample-submission). | Microsoft Defender for Endpoint Plan 1 or Plan 2 (Standalone or included in a plan like Microsoft 365 E3 or E5) |
| **[Tamper protection](tamper-protection-overview)**. Tamper protection helps protect against unwanted changes to your organization's security settings. To learn more, see [Tamper protection overview](tamper-protection-overview). | Microsoft Defender for Endpoint Plan 2 (Standalone or included in a plan like Microsoft 365 E5) |
| **[Block at first sight](configure-block-at-first-sight-microsoft-defender-antivirus)**Block at first sight detects new malware and blocks it within seconds. When a suspicious or malicious file is detected, block at first sight capabilities queries the cloud protection backend and applies heuristics, machine learning, and automated analysis of the file to determine whether it's a threat.To learn more, see [What is "block at first sight"?](configure-block-at-first-sight-microsoft-defender-antivirus) | Microsoft Defender for Endpoint Plan 1 or Plan 2 (Standalone or included in a plan like Microsoft 365 E3 or E5) |
| **[Emergency signature updates](microsoft-defender-antivirus-updates#security-intelligence-updates)**. When malicious content is detected, emergency signature updates and fixes are deployed. Rather than wait for the next regular update, you can receive these fixes and updates within minutes. To learn more about updates, see [Microsoft Defender Antivirus security intelligence and product updates](microsoft-defender-antivirus-updates). | Microsoft Defender for Endpoint Plan 2 (Standalone or included in a plan like Microsoft 365 E5) |
| **[Endpoint detection and response (EDR) in block mode](edr-in-block-mode)**. EDR in block mode provides extra protection when Microsoft Defender Antivirus isn't the primary antivirus product on a device. EDR in block mode remediates artifacts found during EDR-generated scans that the non-Microsoft, primary antivirus solution might have missed. When enabled for devices with Microsoft Defender Antivirus as the primary antivirus solution, EDR in block mode provides the added benefit of automatically remediating artifacts identified during EDR-generated scans. To learn more, see [EDR in block mode](edr-in-block-mode). | Microsoft Defender for Endpoint Plan 2 (Standalone or included in a plan like Microsoft 365 E5) |
| **[Attack surface reduction (ASR) rules](attack-surface-reduction-rules-overview)**. ASR rules block risky behavior from apps. Some ASR rules require cloud protection. For more information, see [Requirements for ASR rules](attack-surface-reduction-rules-overview#requirements-for-asr-rules). | Microsoft Defender for Endpoint Plan 1 or Plan 2 (Standalone or included in a plan like Microsoft 365 E3 or E5) |
| **[Indicators of compromise (IoCs)](indicators-overview)**. In Defender for Endpoint, IoCs can be configured to define the detection, prevention, and exclusion of entities. For example, "Allow" indicators can define exceptions to antivirus scans and remediation actions. "Alert and block" indicators can prevent files or processes from running. To learn more, see [Create indicators](indicators-overview). | Microsoft Defender for Endpoint Plan 2 (Standalone or included in a plan like Microsoft 365 E5) |

Note

In Windows 10 and Windows 11, there is no difference between the **Basic** and **Advanced** reporting options described in this article. The distinction between the Basic and Advanced reporting options is legacy, and choosing either setting results in the same level of cloud protection. There is no difference in the type or amount of information that is shared. For more information on what we collect, see the [Microsoft Privacy Statement](https://go.microsoft.com/fwlink/?linkid=521839).

## Specify the cloud protection level

Turning on cloud protection enables Microsoft Defender Antivirus to use the cloud protection service. The cloud protection level controls how aggressively Microsoft Defender Antivirus blocks and scans suspicious files. Turn on cloud protection before you configure the cloud protection level.

## Use Microsoft Intune to turn on cloud protection

Microsoft Intune is the recommended tool for configuring and distributing Defender for Endpoint features to devices. However, Intune is a separate product that isn't part of Defender for Endpoint, and it isn't included in all subscriptions. To use Intune, you need a subscription that includes it, or you can buy it separately as a standalone subscription or add-on. If you don't have Intune, you can use any of the other methods in this article. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).

To configure cloud protection in Microsoft Intune, use an endpoint security **Antivirus** policy. For detailed instructions, see [Create endpoint security policies](/en-us/intune/device-configuration/endpoint-security/manage-policies#create-endpoint-security-policies) or [Modify existing policies](/en-us/intune/device-configuration/endpoint-security/manage-policies#modify-existing-policies) (links open new tabs in the Intune documentation).

When you create the policy, use these specific settings:

- **Policy type**: On the **Endpoint security | Overview** page in the Microsoft Intune admin center at [https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/~/overview](https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/%7E/overview), under **Manage**, select **Antivirus**, and then select **Create Policy**.
- **Platform**: Select **Windows**.
- **Profile**: Select **Microsoft Defender Antivirus**.

When you create or modify the policy, configure the following settings on the **Configuration settings** tab:

- **Allow cloud protection**: Select **Allowed. Turns on Cloud Protection (Default)**.
- **Submit samples consent**: Select one of the following values:
    - **Send safe samples automatically. (Default)**
    - **Send all samples automatically**
- **Cloud block level**: Select one of the following values:
    - **Not configured**: Uses the default blocking level.
    - **High**: Aggressively blocks unknown files while optimizing client performance. This option increases the chance of false positives.
    - **High plus**: Aggressively blocks unknown files and applies more protection measures. This option might affect client performance.
    - **Zero tolerance**: Blocks all unknown executable files.

For more information about the available settings, see [Windows Antivirus policy settings for Microsoft Defender Antivirus](/en-us/intune/device-configuration/endpoint-security/ref-antivirus-defender-settings-windows).

## Use the Microsoft Defender portal to turn on cloud protection

If your organization [manages endpoint security policies in the Microsoft Defender portal](endpoint-security-policies-configure), use a Microsoft Defender Antivirus policy to configure cloud protection.

For detailed instructions, see [Create an endpoint security policy](endpoint-security-policies-configure#create-an-endpoint-security-policy) or [Edit an endpoint security policy](endpoint-security-policies-configure#edit-an-endpoint-security-policy) (links open new tabs).

When you create the policy on the **Windows policies** tab of the **Endpoint security policies** page in the Defender portal at https://security.microsoft.com/policy-inventory?osPlatform=Windows, use these specific settings:

- **Select platform**: Select **Windows**.
- **Select template**: Select **Microsoft Defender Antivirus**.

When you create or modify the policy, configure the following settings on the **Configuration settings** tab:

- **Allow cloud protection**: Select **Allowed. Turns on Cloud Protection (Default)**.
- **Submit samples consent**: Select one of the following values:
    - **Send safe samples automatically. (Default)**
    - **Send all samples automatically**
- **Cloud block level**: Select one of the following values:
    - **Not configured**: Uses the default blocking level.
    - **High**: Aggressively blocks unknown files while optimizing client performance. This option increases the chance of false positives.
    - **High plus**: Aggressively blocks unknown files and applies more protection measures. This option might affect client performance.
    - **Zero tolerance**: Blocks all unknown executable files.

## Use Microsoft Configuration Manager to turn on cloud protection

Use a Configuration Manager antimalware policy to configure cloud protection. For instructions to create and deploy an antimalware policy, see [Endpoint Protection antimalware policies in Configuration Manager](/en-us/intune/configmgr/protect/deploy-use/endpoint-antimalware-policies).

To turn on cloud protection, configure the following settings in the antimalware policy:

- **Advanced Settings**:
    - **Enable auto sample file submission to help Microsoft determine whether certain detected items are Malicious**: Select **Yes**.
- **Cloud Protection Service**:
    - **Cloud Protection Service membership**: Select **Advanced**.
    - **Level for blocking suspicious files**: Select one of the following values:
        - **Normal**: Uses the default Microsoft Defender Antivirus blocking level.
        - **High**: Aggressively blocks unknown files while optimizing client performance. This option increases the chance of false positives.
        - **High with extra protection**: Aggressively blocks unknown files and applies more protection measures. This option might affect device performance.
        - **Block unknown programs**: Blocks all unknown programs.

## Use Group Policy to turn on cloud protection

Note

MAPS settings configure cloud-delivered protection.

To turn on cloud protection by using Group Policy:

1. Open the [Group Policy Management Console (GPMC)](/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-management-console) on your Group Policy management device.
2. In the GPMC console tree, expand Group Policy Objects in the forest and domain containing the GPO you want to edit.
3. Right-click the GPO, and then select **Edit**.
4. In the **Group Policy Management Editor**, go to **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **MAPS**.

    Note

    Group Policy paths before Windows 10, version 2004 (May 2020) might use *Windows* Defender Antivirus instead of *Microsoft* Defender Antivirus. Both names refer to the same policy location.
5. In the details pane of **MAPS**, the available settings are:

    - Join Microsoft MAPS
    - Send file samples when further analysis is required

    To open and configure a cloud protection setting, use any of the following methods:

    - Double-click the setting.
    - Right-click the setting, and then select **Edit**.
    - Select the setting, and then select **Action** &gt; **Edit**.

Tip

You can also configure Group Policy locally on individual devices by using the Local Group Policy Editor (`gpedit.msc`). Navigate to the same path: **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **MAPS**.

### Enable and configure Join Microsoft MAPS

1. In the details pane of **MAPS**, open the **Join Microsoft MAPS** setting.
2. In the setting window that opens, configure the following options:

    1. Select **Enabled**.
    2. **Join Microsoft MAPS** in the **Options**section: Select one of the following values:
        - **Basic MAPS**: Basic membership sends basic information to Microsoft about malware and potentially unwanted software that has been detected on your device. Information includes where the software came from (like URLs and partial paths), the actions taken to resolve the threat, and whether the actions were successful.
        - **Advanced MAPS**: In addition to basic information, advanced membership sends detailed information about malware and potentially unwanted software, including the full path to the software, and detailed information about how the software has affected your device.

    When you're finished, select **OK**.

### Enable and configure Send file samples when further analysis is required

1. In the details pane of **MAPS**, open the **Send file samples when further analysis is required** setting.
2. In the setting window that opens, configure the following options:

    1. Select **Enabled**.
    2. **Send file samples when further analysis is required** in the **Options**section: Select one of the following values:
        - **Send safe samples**: Most samples are sent automatically. Files that are likely to contain personal information prompt the user for more confirmation.
        - **Send all samples**

    When you're finished, select **OK**.

Note

- **Always Prompt** lowers the protection state of the device.
- **Never send** lowers the protection state of the device and disables [Block at First Sight](configure-block-at-first-sight-microsoft-defender-antivirus).

### Specify the cloud protection level with Group Policy

1. In the **Group Policy Management Editor**, go to **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **MpEngine**.
2. In the details pane of **MpEngine**, open the **Select cloud protection level** setting. To open the setting, use any of the following methods:

    - Double-click the setting.
    - Right-click the setting, and then select **Edit**.
    - Select the setting, and then select **Action** &gt; **Edit**.
3. In the setting window that opens, configure the following options:

    1. Select **Enabled**.
    2. Under **Select cloud blocking level**, select one of the following protection levels:
        - **Default blocking level**: Provides strong detection without increasing the risk of detecting legitimate files.

Caution

If you're using [Resultant Set of Policy with Group Policy](/en-us/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn789183%28v=ws.11%29) (RSOP), selecting **Default blocking level** can produce misleading results because RSOP reads a setting with a `0` value as disabled. Instead, confirm that the registry key is present in `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Defender\MpEngine`, or use [GPresult](/en-us/windows-server/administration/windows-commands/gpresult).
        - **Moderate blocking level**: Provides moderate protection only for high-confidence detections.
        - **High blocking level**: Aggressively blocks unknown files while optimizing client performance. This option increases the chance of false positives.
        - **High + blocking level**: Applies more protection measures. This option might affect client performance and increase the chance of false positives.
        - **Zero tolerance blocking level**: Blocks all unknown executable files.

    When you're finished, select **OK**.

Tip

Are you using Group Policy Objects on premises? See how they translate in the cloud. [Analyze your on-premises group policy objects using Group Policy analytics in Microsoft Intune](/en-us/intune/intune-service/configuration/group-policy-analytics).

## Use PowerShell to turn on cloud protection

Run the commands in an elevated PowerShell session (a PowerShell window you opened by selecting **Run as administrator**).

### Turn on cloud protection with PowerShell

The following command turns on cloud protection:

```powershell
Set-MpPreference -MAPSReporting Advanced
```

### Configure automatic sample submission with PowerShell

The following command configures automatic safe sample submission:

```powershell
Set-MpPreference -SubmitSamplesConsent SendSafeSamples
```

To submit all samples automatically instead of only safe samples, use `SendAllSamples` for the *SubmitSamplesConsent* value.

### Specify the cloud protection level with PowerShell

The following command sets the cloud protection level to High:

```powershell
Set-MpPreference -CloudBlockLevel High
```

*CloudBlockLevel* supports the following values:

- `Default`
- `High`
- `HighPlus`
- `ZeroTolerance`

### Verify the configuration

The following command displays the current cloud protection, sample submission, and cloud block level settings:

```powershell
Get-MpPreference | Select-Object MAPSReporting, SubmitSamplesConsent, CloudBlockLevel
```

To verify cloud protection is turned on, confirm that *MAPSReporting* is `2` (Advanced). If you configured automatic sample submission, *SubmitSamplesConsent* is `1` (Send safe samples automatically) or `3` (Send all samples automatically). *CloudBlockLevel* shows the configured cloud protection level.

### Turn off cloud protection with PowerShell

The following command turns off cloud protection:

```powershell
Set-MpPreference -MAPSReporting Disabled
```

For detailed syntax and parameter information, see [**Set-MpPreference**](/en-us/powershell/module/defender/set-mppreference) and [**Get-MpPreference**](/en-us/powershell/module/defender/get-mppreference).

## Use the Windows Security app to turn on cloud protection

On an unmanaged device, you can turn on cloud protection in the [Windows Security app](https://support.microsoft.com/Windows/Security/Windows-Security/stay-protected-with-the-windows-security-app).

Note

If Group Policy manages these settings, they appear dimmed in the Windows Security app and can't be changed locally.

Group Policy changes must reach the device before the settings are updated in the Windows Security app.

1. In the **Windows Security** app on the device, go to **Virus & threat protection**.
2. In the **Virus & threat protection** pane, in the **Virus & threat protection settings** section, select **Manage settings**.

    [![Screenshot of the Virus and threat protection settings in the Windows Security app.](/en-us/defender/media/wdav-protection-settings-wdsc.png)](/en-us/defender/media/wdav-protection-settings-wdsc.png#lightbox)
3. Turn on **Cloud-delivered protection** and **Automatic sample submission**.

The Windows Security app doesn't provide a setting to configure the cloud protection level.

## Use Windows Management Instrumentation (WMI) to turn on cloud protection

Use the [**Set** method of the **MSFT\_MpPreference**](/en-us/previous-versions/windows/desktop/defender/set-msft-mppreference) class to configure the properties for cloud-delivered protection (MAPS reporting), sample submission behavior, and cloud blocking level:

```WMI
MAPSReporting
SubmitSamplesConsent
CloudBlockLevel
```

For more information about the API, see [Windows Defender WMIv2 APIs](/en-us/previous-versions/windows/desktop/defender/windows-defender-wmiv2-apis-portal).