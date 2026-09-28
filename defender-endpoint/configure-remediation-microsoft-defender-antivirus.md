---
layout: Conceptual
title: Configure remediation for Microsoft Defender Antivirus detections - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/configure-remediation-microsoft-defender-antivirus
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Configure what Microsoft Defender Antivirus should do when it detects a threat, and how long quarantined files should be retained in the quarantine folder.
ms.service: defender-endpoint
ms.subservice: ngp
ms.localizationpriority: medium
author: chrisda
ms.author: chrisda
ms.topic: how-to
ms.custom: nextgen, msecd-doc-authoring-1015
ms.date: 2026-09-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.reviewer: yongrhee
ms.collection:
- m365-security
- tier2
- mde-ngp
locale: en-us
document_id: 480fd7c4-75aa-0f29-47b4-f3ddb831e9c7
document_version_independent_id: 480fd7c4-75aa-0f29-47b4-f3ddb831e9c7
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/configure-remediation-microsoft-defender-antivirus.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-remediation-microsoft-defender-antivirus
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/configure-remediation-microsoft-defender-antivirus.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: e0167a94-22bc-2827-fe5a-3762340aee83
---

# Configure remediation for Microsoft Defender Antivirus detections - Microsoft Defender for Endpoint | Microsoft Learn

When Microsoft Defender Antivirus runs a scan, it attempts to remediate or remove threats that are detected. Remediation actions can include removing a file, sending it to quarantine, or allowing it to remain. This article includes information and links to resources about specifying what actions should be taken when threats are detected on devices.

Important

Microsoft Defender Antivirus detects and remediates files based on many factors. Sometimes, completing a remediation requires a reboot. Even if the detection is later determined to be a false positive, the reboot must be completed to ensure all additional remediation steps have been completed.

If you are certain Microsoft Defender Antivirus quarantined a file based on a false positive, you can restore the file from quarantine after the device reboots. See [Restore quarantined files in Microsoft Defender Antivirus](restore-quarantined-files-microsoft-defender-antivirus). To avoid false-positive quarantines in the future, you can exclude files from the scans. See [Configure and validate exclusions for Microsoft Defender Antivirus scans](microsoft-defender-antivirus-exclusions-configure).

For scan scheduling and related remediation settings, see [About regular quick and full scans with Microsoft Defender Antivirus](schedule-antivirus-scans).

## Prerequisites

### Supported operating systems

- Windows

## Configure remediation options using Intune

Microsoft Intune is the recommended tool for configuring and distributing Defender for Endpoint features to devices. However, Intune is a separate product that isn't part of Defender for Endpoint, and it isn't included in all subscriptions. To use Intune, you need a subscription that includes it, or you can buy it separately as a standalone subscription or add-on. If you don't have Intune, you can use any of the other methods in this article. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).

To configure remediation actions in Microsoft Intune, use an endpoint security **Antivirus** policy. For detailed instructions, see [Create endpoint security policies](/en-us/intune/intune-service/protect/endpoint-security-policy#create-endpoint-security-policies) or [Modify existing policies](/en-us/intune/device-configuration/endpoint-security/manage-policies#modify-existing-policies) (links open new tabs in the Intune documentation).

When you create the policy, use these specific settings:

- **Policy type**: Go to **Manage** &gt; **Antivirus** on the **Endpoint security | Overview** page at [https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/~/overview](https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/%7E/overview), and then select ![](media/defender-portal-icon-create.png)**Create policy**.
- **Platform**: Select **Windows**.
- **Profile**: Select **Microsoft Defender Antivirus**.

When you create or modify the policy, use these specific settings on the **Configuration settings** tab:

- In the **Threat security default action** section, configure the available settings:

    - **Remediation action for High severity threats**
    - **Remediation action for Severe threats**
    - **Remediation action for Low severity threats**
    - **Remediation action for Moderate severity threats**

    with an available action value:

    - **Not configured** (default)
    - **Clean**
    - **Quarantine**
    - **Remove**
    - **Allow**
    - **User defined**
    - **Block**

    Warning

    **Allow** doesn't remediate detected threats and suppresses ongoing detection events. Don't configure this action when [tamper protection is enabled](tamper-protection-overview). Use **Allow** only in specialized environments (for example, industrial control systems or critical infrastructure) where:

    - Automatic remediation isn't practical for operations.
    - Other procedures exist to respond to detected threats.
    - Compensating security controls are deployed.

    Use standard remediation actions (**Clean**, **Quarantine**, **Remove**, or **Block**) in all other environments.

For more information about antivirus policies in Intune, see [Antivirus policy for endpoint security in Intune](/en-us/intune/intune-service/protect/endpoint-security-antivirus-policy).

## Configure remediation options in the Microsoft Defender portal

If your organization [manages endpoint security policies in the Microsoft Defender portal](endpoint-security-policies-configure), use a Microsoft Defender Antivirus policy to configure remediation actions.

For detailed instructions, see [Create an endpoint security policy](endpoint-security-policies-configure#create-an-endpoint-security-policy) or [Edit an endpoint security policy](endpoint-security-policies-configure#edit-an-endpoint-security-policy) (links open new tabs).

When you create the policy on the **Windows policies** tab of the **Endpoint security policies** page in the Defender portal at https://security.microsoft.com/policy-inventory?osPlatform=Windows, use these specific settings:

- **Select platform**: Select **Windows**.
- **Select template**: Select **Microsoft Defender Antivirus**.

When you create or modify the policy, use the same remediation action settings described in Configure remediation options using Intune on the **Configuration settings** tab.

## Configure remediation options using Configuration Manager

For instructions to create and deploy an antimalware policy, see [Endpoint Protection antimalware policies in Configuration Manager](/en-us/intune/configmgr/protect/deploy-use/endpoint-antimalware-policies).

Configure the following settings in the antimalware policy:

- **Default Actions Settings**: For each threat severity level, select one of the following remediation actions:
    - **Recommended**: Use the action recommended in the malware definition file.
    - **Quarantine**: Quarantine the detected malware without removing it.
    - **Remove**: Remove the detected malware.
    - **Allow**: Don't remove or quarantine the detected malware.
- **Threat Overrides Settings**: For **Threat name and override action**, select **Set** to configure the remediation action for a specific threat ID.

Warning

**Allow** doesn't remediate detected threats. Use **Allow** only in specialized environments where automatic remediation isn't practical, other threat-response procedures exist, and compensating security controls are deployed.

## Configure remediation options using Group Policy

Use the following steps to configure remediation options in Group Policy:

1. In Centralized Group Policy, open the [Group Policy Management Console (GPMC)](/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-management-console) on your Group Policy management computer.
2. In the GPMC console tree, expand Group Policy Objects in the forest and domain containing the GPO you want to edit.
3. Right-click the GPO, and then select **Edit**.
4. In the **Group Policy Management Editor**, go to **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus**.

    Note

    Group Policy paths before Windows 10, version 2004 (May 2020) might use *Windows* Defender Antivirus instead of *Microsoft* Defender Antivirus. Both names refer to the same policy location.
5. In the details pane of **Microsoft Defender Antivirus**, use the following table to select the location and setting you want to configure.

    | Subfolder | Setting | Description | Default setting (if not configured) |
    | --- | --- | --- | --- |
    | n/a | Turn off routine remediation. | Specify whether Microsoft Defender Antivirus automatically remediates threats, or whether to prompt the user. | Disabled. Threats are remediated automatically. |
    | Quarantine | Configure removal of items from Quarantine folder. | Specify how many days items should be kept in quarantine before being removed. | 90 days |
    | Scan | Create a system restore point. | A system restore point is created each day before cleaning or scanning is attempted. | Disabled |
    | Scan | Turn on removal of items from scan history folder. | Specify how many days items should be kept in the scan history. | 30 days |
    | Threats | Specify threat alert levels at which default action shouldn't be taken when detected. | Every threat that is detected by Microsoft Defender Antivirus is assigned a threat level:<br>    - `1`: Low<br>    - `2`: Medium<br>    - `4`: High<br>    - `5`: Severe<br><br>Use this setting to specify how threats for each level are remediated. Valid values are:<br>    - `2`: Quarantine<br>    - `3`: Remove<br>    - `6`: Ignore<br>    - `11`: None<br><br>**Warning**: The actions Ignore (`6`) and None (`11`) don't remediate detected threats. Ignore (`6`) suppresses ongoing detection events, while None (`11`) continues to generate alerts and Protection History entries. Don't configure either action when [tamper protection is enabled](tamper-protection-overview). Use these actions only in specialized environments (for example, industrial control systems or critical infrastructure) where Automatic remediation isn't practical for operations, other procedures exist to respond to detected threats, or compensating security controls are deployed. Use standard remediation actions (Quarantine (`2`) or Remove (`3`)) in all other environments. | n/a |
    | Threats | Specify threats upon which default action shouldn't be taken when detected. | Specify how specific threats (using their threat ID) should be remediated. You can specify whether the specific threat should be quarantined, removed, or ignored. | n/a |
6. In the details pane of the selected location, open the setting. To open and configure a setting, use any of the following methods:

    - Double-click the setting.
    - Right-click the setting, and then select **Edit**.
    - Select the setting, and then select **Action** &gt; **Edit**.
7. In the setting window that opens, configure the setting, and then select **OK**.

    Repeat this step as many times as necessary.

Tip

You can also configure Group Policy locally on individual devices by using the Local Group Policy Editor (`gpedit.msc`). Navigate to the same path: **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus**.

## Configure remediation options using PowerShell

Run the commands in an elevated PowerShell session (a PowerShell window you opened by selecting **Run as administrator**).

### Configure default actions by threat severity

The following example quarantines low and moderate severity threats and removes high and severe threats:

```powershell
Set-MpPreference -LowThreatDefaultAction Quarantine -ModerateThreatDefaultAction Quarantine -HighThreatDefaultAction Remove -SevereThreatDefaultAction Remove
```

### Configure the default action for a specific threat

Replace `<threat-ID>` with the numeric threat ID. The following command quarantines the specified threat:

```powershell
Set-MpPreference -ThreatIDDefaultAction_Ids <threat-ID> -ThreatIDDefaultAction_Actions Quarantine
```

To configure multiple threats, specify comma-separated lists of threat IDs and corresponding actions. Each action applies to the threat ID in the same position in the other list.

### Configure quarantine and scan history retention

The following example keeps items in quarantine for 90 days and items in scan history for 30 days:

```powershell
Set-MpPreference -QuarantinePurgeItemsAfterDelay 90 -ScanPurgeItemsAfterDelay 30
```

Specify `0` to keep items indefinitely.

### Turn on system restore point creation

The following command allows Microsoft Defender Antivirus to create a system restore point before cleaning or scanning:

```powershell
Set-MpPreference -DisableRestorePoint $false
```

For detailed syntax, available remediation actions, and parameter information, see [**Set-MpPreference**](/en-us/powershell/module/defender/set-mppreference).