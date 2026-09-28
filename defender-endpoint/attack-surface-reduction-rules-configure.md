---
layout: Conceptual
title: Configure ASR rules and exclusions - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/attack-surface-reduction-rules-configure
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Enable attack surface reduction rules to protect your devices from attacks that use macros, scripts, and common injection techniques.
ms.service: defender-endpoint
ms.localizationpriority: medium
author: chrisda
ms.author: chrisda
ms.subservice: asr
ms.topic: how-to
ms.collection:
- m365-security
- tier2
- mde-asr
ms.custom: admindeeplinkDEFENDER, msecd-doc-authoring-1016
ms.date: 2026-09-08T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: e20cedb4-572a-6c65-77e7-27267820699f
document_version_independent_id: e20cedb4-572a-6c65-77e7-27267820699f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/attack-surface-reduction-rules-configure.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: attack-surface-reduction-rules-configure
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/attack-surface-reduction-rules-configure.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bba62c59-6b53-4be4-8b9d-6624f9184c22
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f3a81ffb-ee36-4ec7-b54a-01b6681aff65
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
platformId: 856b11c3-ae6d-5038-2c5b-2ee554bf666b
---

# Configure ASR rules and exclusions - Microsoft Defender for Endpoint | Microsoft Learn

[Attack surface reduction (ASR) rules](attack-surface-reduction-rules-overview) target risky software behavior on Windows devices that attackers commonly exploit through malware (for example, launching scripts that download files, running obfuscated scripts, and injecting code into other processes). This article describes how to enable and configure ASR rules.

For best results, use enterprise-level management solutions like Microsoft Intune or Microsoft Configuration Manager to manage ASR rules. ASR rule settings from Intune or Configuration Manager overwrite conflicting PowerShell settings on startup. To learn how conflicts between MDM and Group Policy settings are resolved, see How policy conflicts are handled.

## Prerequisites

For more information, see [Requirements for ASR rules](attack-surface-reduction-rules-overview#requirements-for-asr-rules).

## How policy conflicts are handled

When the same ASR rule is configured through more than one method, precedence is resolved as described in the following list:

- **Local device settings (Set-MpPreference)**: These settings have the lowest precedence. Any policy-based method overwrites them on startup.
- **Group Policy**: Overwrites conflicting local device settings on startup. When both Group Policy and a mobile device management (MDM) solution configure the same ASR rule, Group Policy takes precedence by default, unless *MDMWinsOverGP* is enabled (see the next item). To avoid conflicts, don't configure the same ASR rules in both Group Policy and MDM.
- **MDM**: Microsoft Intune or another MDM solution overwrites conflicting local device settings on startup. Whether MDM also overwrites Group Policy depends on the *MDMWinsOverGP* setting in the [ControlPolicyConflict Policy CSP](/en-us/windows/client-management/mdm/policy-csp-controlpolicyconflict):

    - A value of `0` (the default) means the Group Policy setting takes precedence.
    - A value of `1` means the MDM setting applies and the conflicting Group Policy setting is blocked.

    You can configure *MDMWinsOverGP***only** through Policy CSP, for example, by using an Intune custom profile with an OMA-URI or in another MDM solution. There's no Group Policy setting or PowerShell cmdlet for it. In an Intune custom profile, use the following setting:

    **OMA-URI**: `./Device/Vendor/MSFT/Policy/Config/ControlPolicyConflict/MDMWinsOverGP`**Data type**: Integer**Value**: `1`

    Note

    [Controlled configuration](secure-controlled-configuration) enforces settings from Intune or Microsoft Defender for Endpoint security settings management only and ignores conflicting Group Policy, Configuration Manager, and local device settings.
- **Microsoft Configuration Manager**: Applies ASR rules through the Policy CSP in both classic Exploit Guard policy mode and tenant attach mode, so it follows the same MDM precedence and *MDMWinsOverGP* behavior.

## Configure ASR rules in Microsoft Intune

Microsoft Intune is the recommended tool for configuring and distributing Defender for Endpoint features to devices. However, Intune is a separate product that isn't part of Defender for Endpoint, and it isn't included in all subscriptions. To use Intune, you need a subscription that includes it, or you can buy it separately as a standalone subscription or add-on. If you don't have Intune, you can use any of the other methods in this article. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).

In Intune, endpoint security policies are the recommended method to deploy ASR rules, although other methods are also available in Intune (for example, custom profiles with OMA-URIs and CSPs).

### Configure ASR rules and exclusions in Intune using endpoint security policies

To configure ASR rules and exclusions in Microsoft Intune, use an endpoint security **Attack surface reduction** policy. For detailed instructions, see [Create endpoint security policies](/en-us/intune/intune-service/protect/endpoint-security-policy#create-endpoint-security-policies) or [Modify existing policies](/en-us/intune/device-configuration/endpoint-security/manage-policies#modify-existing-policies) (links open new tabs in the Intune documentation).

When you create the policy, use these specific settings:

- **Policy type**: Go to **Manage** &gt; **Attack surface reduction** on the **Endpoint security | Overview** page at [https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/~/overview](https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/%7E/overview), and then select ![](media/defender-portal-icon-create.png)**Create policy**.
- **Platform**: Select **Windows**.
- **Profile**: Select **Attack Surface Reduction Rules**.

Important

Microsoft Defender for Endpoint management supports device objects only. Targeting users isn't supported. Assign the policy to Microsoft Entra device groups, not user groups.

When you create or modify the policy, use these specific settings on the **Configuration settings** tab:

- **Attack surface reduction rules**: Typically, you can enable the [standard protection rules](attack-surface-reduction-rules-overview#asr-rules) in **Block** or **Warn** mode without testing. You should test other ASR rules in **Audit** mode before you switch them to **Block** or **Warn** mode. For more information, see the [ASR rules deployment guide](attack-surface-reduction-rules-deployment).

    After you set the rule mode to **Audit**, **Block**, or **Warn**, an **ASR only per rule exclusions** section appears where you can specify exclusions that apply to that rule only.
- **Attack surface reduction only exclusions**: Use this section to specify exclusions that apply to all ASR rules.

    To specify per-ASR rule exclusions or global ASR rule exclusions, use either of the following methods:

    - Select ![](media/defender-portal-icon-create.png)**Add**. In the box that appears, enter the path or path and filename to exclude. For example:

        - `C:\folder`
        - `%ProgramFiles%\folder\file.exe`
        - `C:\path`
    - Select ![](media/intune-icon-import.png)**Import** to import a CSV file that contains the names of files and folders to exclude. The CSV file uses the following format:

        ```text
        AttackSurfaceReductionOnlyExclusions
        "C:\folder"
        "%ProgramFiles%\folder\file.exe"
        "C:\path"
        ...
        ```

        Tip

        Double quotation marks around the values are optional, and are ignored (aren't used in the values) if you include them. Don't use single quotation marks around the values.

    For more information about exclusions, see [File and folder exclusions for ASR rules](attack-surface-reduction-rules-overview#file-and-folder-exclusions-for-asr-rules).
- **Enable controlled folder access**, **Controlled folder access protected folders**, and **Controlled folder access allowed applications**: For more information, see [Configure CFA in Intune using endpoint security policies](controlled-folder-access-configure#configure-cfa-in-intune-using-endpoint-security-policies).

### Configure ASR rules in Intune using custom profiles with OMA-URIs and CSPs

Although endpoint security policies are recommended, you can also configure ASR rules in Intune using custom profiles that contain Open Mobile Alliance Uniform Resource Identifier (OMA-URI) settings using a Windows [Policy configuration service provider (CSP)](/en-us/windows/client-management/mdm/policy-configuration-service-provider).

For instructions to create and assign a custom profile, see [Use custom device settings in Microsoft Intune](/en-us/intune/device-configuration/templates/configure-custom-settings). For information about the OMA-URI fields in Windows custom profiles, see [Add custom settings for Windows devices in Microsoft Intune](/en-us/intune/device-configuration/templates/configure-custom-settings-windows).

When you create the policy, use these specific settings:

- **Platform**: Select **Windows 10 and later**.
- **Profile type**: Select **Templates**, and then select **Custom**.

When you create or modify the policy, add the following settings on the **Configuration settings** tab:

- **Name**: Enter a unique name for the setting.
- **Description**: Enter an optional, brief description.
- **OMA-URI**: Enter the **Device** value from the [AttackSurfaceReductionRules](/en-us/windows/client-management/mdm/policy-csp-defender#attacksurfacereductionrules) CSP: `./Vendor/MSFT/Policy/Config/Defender/AttackSurfaceReductionRules`
- **Data type**: Select **String**.
- **Value**: Use the following syntax:

    ```text
    <RuleGuid1>=<ModeForRuleGuid1>
    <RuleGuid2>=<ModeForRuleGuid2>
    ...
    <RuleGuidN>=<ModeForRuleGuidN>
    ```

    GUID values for ASR rules are available at [ASR rules](attack-surface-reduction-rules-overview#asr-rules). Use one of the following [rule modes](attack-surface-reduction-rules-overview#modes-for-asr-rules) for each rule:

    - `0`: Off
    - `1`: Block
    - `2`: Audit
    - `5`: Not configured
    - `6`: Warn

    For example:

    ```text
    75668c1f-73b5-4cf0-bb93-3ecf5cb7cc84=2
    3b576869-a4ec-4529-8536-b80a7769e899=1
    d4f940ab-401b-4efc-aadc-ad5f3c50688a=2
    d3e037e1-3eb8-44c8-a917-57927947596d=1
    5beb7efe-fd9a-4556-801d-275e5ffc04cc=0
    be9ba2d9-53ea-4cdc-84e5-9b1eeee46550=1
    ```

Tip

You can add global ASR rule exclusions to the same custom profile instead of creating a separate profile for exclusions. For instructions, see Configure global ASR rule exclusions in Intune using custom profiles with OMA-URIs and CSPs.

#### Configure global ASR rule exclusions in Intune using custom profiles with OMA-URIs and CSPs

You can add global ASR rule exclusions to the custom profile that configures your ASR rules or to a separate Windows custom profile. For instructions to create and assign a custom profile, see [Use custom device settings in Microsoft Intune](/en-us/intune/device-configuration/templates/configure-custom-settings).

On the **Configuration settings** tab, select **Add**. In the **Add row** flyout that opens, configure the following settings:

- **Name**: Enter a unique name for the exclusions setting.
- **Description**: Enter an optional, brief description.
- **OMA-URI**: Enter the **Device** value from the [AttackSurfaceReductionOnlyExclusions](/en-us/windows/client-management/mdm/policy-csp-defender#attacksurfacereductiononlyexclusions) CSP: `./Device/Vendor/MSFT/Policy/Config/Defender/AttackSurfaceReductionOnlyExclusions`
- **Data type**: Select **String**.
- **Value**: Use the following syntax:

    ```text
    <PathOrPathAndFilename1>
    <PathOrPathAndFilename2>
    ...
    <PathOrPathAndFilenameN>
    ```

    For example:

    ```text
    C:\folder
    %ProgramFiles%\folder\file.exe
    C:\path
    ```

## Configure ASR rules and exclusions in the Microsoft Defender portal

If your organization [manages endpoint security policies in the Microsoft Defender portal](endpoint-security-policies-configure), you can configure ASR rules and their exclusions with the same endpoint security policies that Intune uses.

For detailed instructions, see [Create an endpoint security policy](endpoint-security-policies-configure#create-an-endpoint-security-policy) or [Edit an endpoint security policy](endpoint-security-policies-configure#edit-an-endpoint-security-policy) (links open new tabs).

When you create the policy on the **Windows policies** tab of the **Endpoint security policies** page in the Defender portal at https://security.microsoft.com/policy-inventory?osPlatform=Windows, use these specific settings:

- **Select platform**: Select **Windows**.
- **Select template**: Select **Attack surface reduction rules**.

When you create or modify the policy, use the same settings described in Configure ASR rules and exclusions in Intune using endpoint security policies on the **Configuration settings** tab. These settings include global attack surface reduction only exclusions and per-ASR rule exclusions.

When you assign the policy, assignment group limitations apply to devices managed through security settings management. For details, see the [Assignments step](endpoint-security-policies-configure#create-an-endpoint-security-policy).

## Configure ASR rules in any MDM solution using the Policy CSP

The Policy configuration service provider (CSP) enables enterprise organizations to configure policies on Windows devices using any mobile device management (MDM) solution, not just Microsoft Intune. For more information, see [Policy CSP](/en-us/windows/client-management/mdm/policy-configuration-service-provider).

You can configure ASR rules using the [AttackSurfaceReductionRules](/en-us/windows/client-management/mdm/policy-csp-defender#attacksurfacereductionrules) CSP with the following settings:

**OMA-URI path**: `./Vendor/MSFT/Policy/Config/Defender/AttackSurfaceReductionRules`**Value**: `<RuleGuid1>=<ModeForRuleGuid1>|<RuleGuid2>=<ModeForRuleGuid2>|...<RuleGuidN>=<ModeForRuleGuidN>`

- GUID values for ASR rules are available at [ASR rules](attack-surface-reduction-rules-overview#asr-rules)
- The following [rule modes](attack-surface-reduction-rules-overview#modes-for-asr-rules)are available:
    - `0`: Off
    - `1`: Block
    - `2`: Audit
    - `5`: Not configured
    - `6`: Warn

For example:

`75668c1f-73b5-4cf0-bb93-3ecf5cb7cc84=2|3b576869-a4ec-4529-8536-b80a7769e899=1|d4f940ab-401b-4efc-aadc-ad5f3c50688a=2|d3e037e1-3eb8-44c8-a917-57927947596d=1|5beb7efe-fd9a-4556-801d-275e5ffc04cc=0|be9ba2d9-53ea-4cdc-84e5-9b1eeee46550=1`

Note

Be sure to enter OMA-URI values without spaces.

### Configure global ASR rule exclusions in any MDM solution using the Policy CSP

You can use the Policy CSP to configure global ASR rule path and path and filename exclusions using the [AttackSurfaceReductionOnlyExclusions](/en-us/windows/client-management/mdm/policy-csp-defender#attacksurfacereductiononlyexclusions) CSP with the following settings:

**OMA-URI path**: `./Device/Vendor/MSFT/Policy/Config/Defender/AttackSurfaceReductionOnlyExclusions`**Value**: `<PathOrPathAndFilename1>=0|<PathOrPathAndFilename1>=0|...<PathOrPathAndFilenameN>=0`

For example, `C:\folder|%ProgramFiles%\folder\file.exe|C:\path`

## Configure ASR rules and global ASR rule exclusions in Microsoft Configuration Manager

For instructions, see the attack surface reduction information in [Create and deploy an Exploit Guard policy](/en-us/intune/configmgr/protect/deploy-use/create-deploy-exploit-guard-policy).

Warning

There's a known issue with the applicability of attack surface reduction on Server OS versions which is marked as compliant without any actual enforcement. Currently, there's no defined release date for when this will be fixed.

Important

If you're using "Disable admin merge" set to `true` on devices, and you're using any of the following tools/methods, adding ASR rules per-rule exclusions or local ASR rule exclusions don't apply:

- Defender for Endpoint Security Settings Management (Disable Local Admin Merge) **Windows policies** tab of the **Endpoint security policies** page in the Microsoft Defender portal at https://security.microsoft.com/policy-inventory?osPlatform=Windows
- Microsoft Intune (Disable Local Admin Merge)
- The Defender CSP (**[DisableLocalAdminMerge](/en-us/windows/client-management/mdm/defender-csp)**)
- Group Policy (Configure local administrator merge behavior for lists)

To modify this behavior, you need to change "Disable admin merge" to `false`.

## Configure ASR rules and exclusions in Group Policy

Warning

If you manage your computers and devices with Intune, Microsoft Configuration Manager, or other enterprise-level management software, the management software can overwrite conflicting Group Policy settings. To learn how these conflicts are resolved, see How policy conflicts are handled.

1. In Centralized Group Policy, open the [Group Policy Management Console (GPMC)](/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-management-console) on your Group Policy management computer.
2. In the GPMC console tree, expand Group Policy Objects in the forest and domain containing the GPO you want to edit.
3. Right-click on the GPO, and then select **Edit**.
4. In the **Group Policy Management Editor**, go to **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **Microsoft Defender Exploit Guard &gt; Attack Surface Reduction**.
5. In the details pane of **Attack Surface Reduction**, the available settings are:

    - Configure Attack Surface Reduction rules
    - Exclude files and paths from Attack surface reduction rules
    - Apply a list of exclusions to specific attack surface reduction (ASR) rules

    To open and configure an ASR rule setting, use any of the following methods:

    - Double-click on the setting.
    - Right-click on the setting, and then select **Edit**
    - Select the setting, and then select **Action** &gt; **Edit**.

Tip

You can also configure Group Policy locally on individual devices by using the Local Group Policy Editor (`gpedit.msc`). Navigate to the same path: **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **Microsoft Defender Exploit Guard** &gt; **Attack Surface Reduction**.

The available settings are described in Configure ASR rules in Group Policy, Configure global ASR rule exclusions in Group Policy, and Configure per-ASR rule exclusions in Group Policy.

Important

Quotation marks, leading spaces, trailing spaces, and extra characters aren't supported in any of the ASR rule-related values in Group Policy.

Group Policy paths before Windows 10 version 2004 (May 2020) might use *Windows* Defender Antivirus instead of *Microsoft* Defender Antivirus. Both names refer to the same policy location.

### Configure ASR rules in Group Policy

Use the following steps to configure ASR rules and their modes in the Group Policy **Attack Surface Reduction** settings:

1. In the details pane of **Attack Surface Reduction**, open the **Configure Attack Surface Reduction rules** setting.
2. In the setting window that opens, configure the following options:

    1. Select **Enabled**.
    2. **Set the state for each ASR rule**: Select **Show...**.
    3. In the **Set the state for each ASR rule**dialog that opens, configure the following settings:
        - **Value name**: Enter the [GUID value of the ASR rule](attack-surface-reduction-rules-overview#asr-rules).
        - **Value**: Enter one of the following [rule mode](attack-surface-reduction-rules-overview#modes-for-asr-rules)values:
            - `0`: Off
            - `1`: Block
            - `2`: Audit
            - `5`: Not configured
            - `6`: Warn

    [![Screenshot of Configure Attack Surface Reduction rules in Group Policy.](media/asr-rules-gp.png)](media/asr-rules-gp.png#lightbox)

    For more information, see [ASR rule modes](attack-surface-reduction-rules-overview#modes-for-asr-rules).

    Repeat this step as many times as necessary. When you're finished, select **OK**.

### Configure global ASR rule exclusions in Group Policy

The paths or filenames with paths you specify are used as exclusions for all ASR rules.

1. In the details pane of **Attack Surface Reduction**, open the **Exclude files and paths from Attack surface reduction rules** setting.
2. In the setting window that opens, configure the following options:

    1. Select **Enabled**.
    2. **Exclusions from ASR rules**: Select **Show...**.
3. In the **Exclusions from ASR rules** dialog that opens, configure the following settings:

    - **Value name**: Enter the path or path and filename to exclude from all ASR rules.
    - **Value**: Enter `0`.

    The following types of value names are supported:

    - To exclude all files in a folder, enter the full folder path. For example, `C:\Data\Test`.
    - To exclude a specific file in a specific folder (recommended), enter the path and filename. For example, `C:\Data\Test\test.exe`.

    Repeat this step as many times as necessary. When you're finished, select **OK**.

### Configure per-ASR rule exclusions in Group Policy

The paths or filenames with paths you specify are used as exclusions for specific ASR rules.

Note

If the **Apply a list of exclusions to specific attack surface reduction (ASR) rules** setting isn't available in your GPMC, you need version 24H2 or later of the [Administrative Templates files](/en-us/troubleshoot/windows-client/group-policy/create-and-manage-central-store#links-to-download-the-administrative-templates-files-based-on-the-operating-system-version) in your [Central Store](/en-us/troubleshoot/windows-client/group-policy/create-and-manage-central-store#the-central-store).

1. In the details pane of **Attack Surface Reduction**, open the **Apply a list of exclusions to specific attack surface reduction (ASR) rules** setting.
2. In the setting window that opens, configure the following options:

    1. Select **Enabled**.
    2. **Exclusions for each ASR rule**: Select **Show...**.
3. In the **Exclusions for each ASR rule** dialog that opens, configure the following settings:

    - **Value name**: Enter the [GUID value of the ASR rule](attack-surface-reduction-rules-overview#asr-rules).
    - **Value**: Enter one or more exclusions for the ASR rule. Use the syntax `Path1\ProcessName1>Path2\ProcessName2>...PathN\ProcessNameN`. For example, `C:\Windows\Notepad.exe>c:\Windows\regedit.exe>C:\SomeFolder\test.exe`.

    Repeat this step as many times as necessary. When you're finished, select **OK**.

## Configure ASR rules in PowerShell

Warning

If you manage your computers and devices with Intune, Configuration Manager, or another enterprise-level management platform, the management software overwrites any conflicting PowerShell settings on startup.

On the target device, use the following PowerShell command syntax in an elevated PowerShell session (a PowerShell window you opened by selecting **Run as administrator**). This syntax adds, sets, or removes the mode for one or more ASR rules by specifying each rule GUID and its desired action:

```powershell
<Add-MpPreference | Set-MpPreference | Remove-MpPreference> -AttackSurfaceReductionRules_Ids <RuleGuid1>,<RuleGuid2>,...<RuleGuidN> -AttackSurfaceReductionRules_Actions <ModeForRuleGuid1>,<ModeForRuleGuid2>,...<ModeForRuleGuidN>
```

- **Set-MpPreference***overwrites* any existing rules and their corresponding modes with the values you specify. To display the ASR rules currently configured on the device along with their assigned actions, run the following command:

    ```powershell
    $p = Get-MpPreference;0..([math]::Min($p.AttackSurfaceReductionRules_Ids.Count,$p.AttackSurfaceReductionRules_Actions.Count)-1) | % {[pscustomobject]@{Id=$p.AttackSurfaceReductionRules_Ids[$_];Action=$p.AttackSurfaceReductionRules_Actions[$_]}} | Format-Table -AutoSize
    ```

    To add new rules and their corresponding modes without affecting any existing values, use the **Add-MpPreference** cmdlet. To remove the specified rules and their corresponding modes without affecting other existing values, use the **Remove-MpPreference** cmdlet. The command syntax is identical for the three cmdlets.
- GUID values for ASR rules are available at [ASR rules](attack-surface-reduction-rules-overview#asr-rules).
- Valid values for the *AttackSurfaceReductionRules\_Actions* parameter are:

    - `0` or `Disabled`
    - `1` or `Enabled` (**Block** mode)
    - `2` or `AuditMode` or `Audit`
    - `5` or `NotConfigured`
    - `6` or `Warn`

The following example uses `Set-MpPreference` to configure four ASR rules in a single command, setting each rule to a different mode (**Enabled**, **Disabled**, or **AuditMode**):

```powershell
Set-MpPreference -AttackSurfaceReductionRules_Ids 26190899-1602-49e8-8b27-eb1d0a1ce869,3b576869-a4ec-4529-8536-b80a7769e899,e6db77e5-3df2-4cf1-b95a-636979351e5,01443614-cd74-433a-b99e-2ecdc07bfc25 -AttackSurfaceReductionRules_Actions Enabled,Enabled,Disabled,AuditMode
```

### Configure global ASR rule exclusions in PowerShell

On the target device, use the following PowerShell command syntax in an elevated PowerShell session to add, update, or remove path exclusions that apply to all ASR rules:

```powershell
<Add-MpPreference | Set-MpPreference | Remove-MpPreference> -AttackSurfaceReductionOnlyExclusions "<PathOrPathAndFilename1>","<PathOrPathAndFilename2>",..."<PathOrPathAndFilenameN>"
```

- **Set-MpPreference***overwrites* any existing ASR rule exclusions with the values you specify. To display the ASR rule exclusions currently configured on the device, run the following command:

    ```powershell
    (Get-MpPreference).AttackSurfaceReductionOnlyExclusions
    ```

    To add new exceptions without affecting any existing values, use the **Add-MpPreference** cmdlet. To remove the specified exceptions without affecting any other values, use the **Remove-MpPreference** cmdlet. The command syntax is identical for the three cmdlets.

    The following example excludes a folder (`C:\Data\Test`) and a specific executable (`C:\Data\LOBApp\app1.exe`) from all ASR rules on the device:

    ```powershell
    Set-MpPreference -AttackSurfaceReductionOnlyExclusions "C:\Data\Test","C:\Data\LOBApp\app1.exe"
    ```