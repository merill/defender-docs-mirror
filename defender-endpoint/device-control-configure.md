---
layout: Conceptual
title: Configure device control in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/device-control-configure
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Configure Microsoft Defender for Endpoint device control by using Microsoft Intune, the Microsoft Defender portal, custom OMA-URI profiles, or Group Policy.
author: limwainstein
ms.author: lwainstein
ms.date: 2026-09-10T00:00:00.0000000Z
ms.topic: how-to
ms.service: defender-endpoint
ms.subservice: asr
ms.collection:
- m365-security
- tier2
- mde-asr
ms.custom:
- partner-contribution
- msecd-doc-authoring-1015
ms.reviewer: joshbregman, tdoucette
ai-usage: ai-assisted
locale: en-us
document_id: 06e044f1-bca7-8409-b1d2-637d1227bbda
document_version_independent_id: 06e044f1-bca7-8409-b1d2-637d1227bbda
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/device-control-configure.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: device-control-configure
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/device-control-configure.md
platformId: 9d161fb4-6b94-f242-1cfb-78bd54ebe94c
---

# Configure device control in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

[Device control](device-control-overview) in Microsoft Defender for Endpoint helps security teams manage access to removable storage, printers, and other peripheral devices on Windows devices. This article describes how to enable and configure device control.

## Configure device control in Microsoft Intune

Microsoft Intune is the recommended tool for configuring and distributing Defender for Endpoint features to devices. However, Intune is a separate product that isn't part of Defender for Endpoint, and it isn't included in all subscriptions. To use Intune, you need a subscription that includes it, or you can buy it separately as a standalone subscription or add-on. If you don't have Intune, you can use any of the other methods in this article. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).

### View device control groups in Intune

In Intune, device control groups appear as reusable settings.

1. On the **Endpoint security | Overview** page in the Microsoft Intune admin center at [https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/~/overview](https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/%7E/overview), go to **Manage** &gt; **Attack surface reduction**.
2. On the **Endpoint security | Attack surface reduction** page, select the **Reusable settings** tab.

### Configure device control in Intune using endpoint security policies

To configure device control in Microsoft Intune, use an endpoint security **Attack surface reduction** policy. For detailed instructions, see [Create endpoint security policies](/en-us/intune/intune-service/protect/endpoint-security-policy#create-endpoint-security-policies) or [Modify existing policies](/en-us/intune/device-configuration/endpoint-security/manage-policies#modify-existing-policies) (links open new tabs in the Intune documentation).

When you create the policy, use these specific settings:

- **Policy type**: Go to **Manage** &gt; **Attack surface reduction** on the **Endpoint security | Overview** page at [https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/~/overview](https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/%7E/overview), and then select ![](media/defender-portal-icon-create.png)**Create policy**.
- **Platform**: Select **Windows**. Currently, the **Device Control** profile isn't supported for Windows Server devices managed through Defender for Endpoint security settings management, even though **This policy applies to** shows Windows Server.
- **Profile**: Select **Device Control**.

When you create or modify the policy, use these specific settings on the **Configuration settings** tab:

- **Defender** section: See [Allow Full Scan Removable Drive Scanning](/en-us/windows/client-management/mdm/policy-csp-defender#allowfullscanremovabledrivescanning) settings.
- **Device Control** section: Configure custom policies with reusable settings. Each row in this section represents a device control policy. The policy name appears in user notifications, advanced hunting, and reports.

    Select ![](media/defender-portal-icon-create.png)**Add** to add a policy. Configure the following settings:

    - **Name**: Enter a unique name.
    - **Included ID**: Select the reusable settings that the policy applies to.
    - **Excluded ID**: Select the reusable settings that the policy excludes.
    - **Type**, **Options**, and **Access mask**: Configure the action, user notification and event behavior, and allowed permissions.

    [![Screenshot of the Intune Device Control profile configuration settings.](media/device-control-profile.png)](media/device-control-profile.png#lightbox)

    For information about adding reusable groups of settings to a policy, see [Add reusable groups to a Device Control profile](/en-us/intune/device-security/reusable-settings-groups#add-reusable-groups-to-a-device-control-profile). For information about device control rules, see [Device control overview: Rules](device-control-policies#rules).

    Add an **Allow** or **Deny** policy when you add an audit policy to avoid unexpected results.

    Important

    If you configure only audit policies, permissions are inherited from the default enforcement setting.

    Intune doesn't preserve the order of policies shown in the user interface for policy enforcement. Use non-intersecting **Allow** and **Deny** policies by explicitly adding devices to be excluded. You can't change the default enforcement setting in the Intune graphical interface. If you change the default enforcement to `Deny` by using another method and create an `Allow` policy for specific devices, all other devices are blocked.
- **Device Installation Restrictions**: See [Device Installation](/en-us/windows/client-management/mdm/policy-csp-deviceinstallation?WT.mc_id=Portal-fx) settings.
- **Removable Storage Access**: See [Removable Storage Access](/en-us/windows/client-management/mdm/policy-csp-admx-removablestorage) settings.
- **Data Protection**: See [Allow Direct Memory Access](/en-us/windows/client-management/mdm/policy-csp-dataprotection) settings.
- **Dma Guard**: See [Device Enumeration Policy](/en-us/windows/client-management/mdm/policy-csp-dmaguard?WT.mc_id=Portal-fx) settings.
- **Storage**: See [Removable Disk Deny Write Access](/en-us/windows/client-management/mdm/policy-csp-Storage#removablediskdenywriteaccess) settings.
- **Connectivity**: See [Allow USB Connection](/en-us/windows/client-management/mdm/policy-csp-Connectivity#allowusbconnection) and [Allow Bluetooth](/en-us/windows/client-management/mdm/policy-csp-Connectivity#allowbluetooth) settings.
- **Bluetooth**: Configure settings related to Bluetooth connections and services. See [Policy CSP - Bluetooth](/en-us/windows/client-management/mdm/policy-csp-Bluetooth?WT.mc_id=Portal-fx).
- **System**: See [Allow Storage Card](/en-us/windows/client-management/mdm/policy-csp-System#allowstoragecard) settings.

Tip

You don't need to configure all available settings at once. Consider starting with the **Device Control** settings.

### Configure device control in Intune using custom profiles with OMA-URIs and CSPs

Although endpoint security policies are recommended, you can also configure device control in Intune by using custom profiles that contain Open Mobile Alliance Uniform Resource Identifier (OMA-URI) settings from the [Defender configuration service provider (CSP)](/en-us/windows/client-management/mdm/defender-csp).

For instructions to create and assign a custom profile, see [Use custom device settings in Microsoft Intune](/en-us/intune/device-configuration/templates/configure-custom-settings). For information about the OMA-URI fields in Windows custom profiles, see [Add custom settings for Windows devices in Microsoft Intune](/en-us/intune/device-configuration/templates/configure-custom-settings-windows).

Important

Using Intune OMA-URI settings to configure device control requires Intune to manage the *Device Configuration* workload if the device is co-managed with Configuration Manager. For more information, see [How to switch Configuration Manager workloads to Intune](/en-us/intune/configmgr/comanage/how-to-switch-workloads).

When you create the policy, use these specific settings:

- **Platform**: Select **Windows 10 and later**.
- **Profile type**: Select **Templates**, and then select **Custom**.

When you create or modify the policy, add a row for each setting on the **Configuration settings** tab. Use the following OMA-URI values for device control settings:

- **Device control default enforcement**: Establishes what decisions are made during device control access checks when none of the policy rules match.
    - **OMA-URI**: `./Vendor/MSFT/Defender/Configuration/DefaultEnforcement`
    - **Data type**: Integer
    - **Values**:
        - `DefaultEnforcementAllow` = `1`
        - `DefaultEnforcementDeny` = `2`
- **Device types**: Specifies the device types, identified by their primary IDs, that have device control protection turned on. Separate multiple product family IDs with a pipe, without spaces.
    - **OMA-URI**: `./Vendor/MSFT/Defender/Configuration/SecuredDevicesConfiguration`
    - **Data type**: String
    - **Values**:
        - `RemovableMediaDevices`
        - `CdRomDevices`
        - `WpdDevices`
        - `PrinterDevices`
- **Enable device control**: Enables or disables device control on the device.
    - **OMA-URI**: `./Vendor/MSFT/Defender/Configuration/DeviceControlEnabled`
    - **Data type**: Integer
    - **Values**:
        - Disable = `0`
        - Enable = `1`

#### Create policies with OMA-URI

[![Screenshot of the Intune settings used to create a device control policy with OMA-URI.](media/create-policy-with-oma-uri.png)](media/create-policy-with-oma-uri.png#lightbox)

When you create policies with OMA-URI in Intune, create one XML file for each policy. As a best practice, use the **Device Control** profile to author custom policies.

In the **Add Row** pane, specify the following settings:

- In the **Name** field, type `Allow Read Activity`.
- In the **OMA-URI** field, type `./Vendor/MSFT/Defender/Configuration/DeviceControl/PolicyRules/%7b[PolicyRule Id]%7d/RuleData`. Use the PowerShell command `New-Guid` to generate the GUID that replaces `[PolicyRule Id]`. Use the same GUID for the `PolicyRule Id` value in the policy XML file.
- In the **Data Type** field, select **String (XML file)**, and use **Custom XML**.

You can use parameters to set conditions for specific entries. For an example, see the [Allow Read policy XML file for removable storage](https://github.com/microsoft/mdatp-devicecontrol/blob/main/windows/device/Intune%20OMA-URI/Allow%20Read.xml).

Note

Comments using XML comment notation `<!-- COMMENT -->` can be used in the Rule and Group XML files, but they must be inside the first XML tag, not the first line of the XML file.

#### Create groups with OMA-URI

[![Screenshot of the Intune settings used to create a device control group with OMA-URI.](media/create-group-with-oma-uri.png)](media/create-group-with-oma-uri.png#lightbox)

When you create groups with OMA-URI in Intune, create one XML file for each group. As a best practice, use reusable settings to define groups.

In the **Add Row** pane, specify the following settings:

- In the **Name** field, type `Any Removable Storage Group`.
- In the **OMA-URI** field, type `./Vendor/MSFT/Defender/Configuration/DeviceControl/PolicyGroups/%7b[GroupId]%7d/GroupData`. Use the PowerShell command `New-Guid` to generate the GUID that replaces `[GroupId]`. Use the same GUID for the group `Id` value in the group XML file.
- In the **Data Type** field, select **String (XML file)**, and use **Custom XML**.

Note

Comments using XML comment notation `<!-- COMMENT -->` can be used in the Rule and Group XML files, but they must be inside the first XML tag, not the first line of the XML file.

## Configure device control in the Microsoft Defender portal

If your organization [manages endpoint security policies in the Microsoft Defender portal](endpoint-security-policies-configure), you can configure device control with the same endpoint security policies that Intune uses.

Important

Device control policies created in the Defender portal apply only to devices enrolled in Intune. They don't apply to devices managed through Defender for Endpoint security settings management that aren't enrolled in Intune.

For detailed instructions, see [Create an endpoint security policy](endpoint-security-policies-configure#create-an-endpoint-security-policy) or [Edit an endpoint security policy](endpoint-security-policies-configure#edit-an-endpoint-security-policy) (links open new tabs).

When you create the policy on the **Windows policies** tab of the **Endpoint security policies** page in the Defender portal at https://security.microsoft.com/policy-inventory?osPlatform=Windows, use these specific settings:

- **Select platform**: Select **Windows**.
- **Select template**: Select **Device control**.

When you create or modify the policy, use the same settings described in Configure device control in Intune using endpoint security policies on the **Configuration settings** tab.

## Configure device control in Group Policy

Warning

If you manage device control with Intune or another mobile device management service, remove conflicting Group Policy settings. The [ControlPolicyConflict setting](/en-us/windows/client-management/mdm/policy-csp-controlpolicyconflict) isn't applicable to the Defender CSP.

To configure device control settings in Group Policy, follow these steps:

1. In Centralized Group Policy, open the [Group Policy Management Console (GPMC)](/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-management-console) on your Group Policy management computer.
2. In the GPMC console tree, expand **Group Policy Objects** in the forest and domain that contain the Group Policy Object (GPO) you want to edit.
3. Right-click the GPO, and then select **Edit**.
4. In the **Group Policy Management Editor**, go to **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus**.
5. The device control settings are available in the following locations:

    - **Features**:
        - Device Control
    - **Device Control**:
        - Select Device Control Default Enforcement Policy
        - Turn on device control for specific device types
        - Define device control policy groups
        - Define device control policy rules

    To open and configure a setting, use any of the following methods:

    - Double-click the setting.
    - Right-click the setting, and then select **Edit**.
    - Select the setting, and then select **Action** &gt; **Edit**.

Tip

You can also configure Group Policy locally on individual devices by using the Local Group Policy Editor (`gpedit.msc`). Go to the same base path: **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus**, and then select **Features** or **Device Control**, depending on the setting.

Note

If you don't see the device control Group Policy settings, add the Group Policy Administrative Templates (ADMX). You can download [WindowsDefender.adml](https://github.com/microsoft/mdatp-devicecontrol/blob/main/windows/WindowsDefender.adml) and [WindowsDefender.admx](https://github.com/microsoft/mdatp-devicecontrol/blob/main/windows/WindowsDefender.admx) from the [Microsoft Defender for Endpoint device control samples](https://github.com/microsoft/mdatp-devicecontrol/tree/main/windows) on GitHub.

### Enable device control in Group Policy

To enable removable storage access control, follow these steps:

1. In the **Microsoft Defender Antivirus** policy tree, select **Features**.
2. In the details pane of **Features**, open the **Device Control** setting.
3. In the **Device Control** window, select **Enabled**.

[![Screenshot of the Group Policy setting used to enable or disable removable storage access control.](media/deploy-dc-gpo/enable-disable-rsac.png)](media/deploy-dc-gpo/enable-disable-rsac.png#lightbox)

### Configure default enforcement in Group Policy

You can set the default access to `Deny` or `Allow` for all device control features, including `RemovableMediaDevices`, `CdRomDevices`, `WpdDevices`, and `PrinterDevices`.

[![Screenshot of the Group Policy setting used to select the default device control enforcement.](media/set-default-enforcement-deny-gp.png)](media/set-default-enforcement-deny-gp.png#lightbox)

For example, you can have a `Deny` or `Allow` policy for `RemovableMediaDevices`, but not for `CdRomDevices` or `WpdDevices`. If you set the default enforcement to `Deny`, read, write, and execute access to `CdRomDevices` and `WpdDevices` is blocked. If you want to manage only storage, create an `Allow` policy for printers. Otherwise, default enforcement also denies access to printers.

To set the default enforcement to deny, follow these steps:

1. In the **Microsoft Defender Antivirus** policy tree, select **Device Control**.
2. In the details pane of **Device Control**, open the **Select Device Control Default Enforcement Policy** setting.
3. In the **Select Device Control Default Enforcement Policy** window, configure the following options:

    1. Select **Enabled**.
    2. Under **Options**, select **Default Deny**.

### Configure device types in Group Policy

To configure the device types that a device control policy applies to, follow these steps:

1. In the **Microsoft Defender Antivirus** policy tree, select **Device Control**.
2. In the details pane of **Device Control**, open the **Turn on device control for specific device types** setting.
3. In the **Turn on device control for specific device types** window, configure the following options:

    1. Select **Enabled**.
    2. Under **Options**, in the **Turn on device control for specific device types** box, specify the product family IDs, separated by a pipe (`|`). Enter the value as a single string without spaces. Otherwise, the device control engine might parse the value incorrectly. Product family IDs include `RemovableMediaDevices`, `CdRomDevices`, `WpdDevices`, and `PrinterDevices`.

[![Screenshot of the Group Policy setting used to configure protected device types.](media/deploy-dc-gpo/configure-device.png)](media/deploy-dc-gpo/configure-device.png#lightbox)

### Define device control groups in Group Policy

Create and deploy one XML file for each removable storage group:

1. Use the properties in your removable storage group to create an XML file. Make sure the root node is `PolicyGroups`. For example:

    ```xml
     <PolicyGroups>
         <Group Id="{d8819053-24f4-444a-a0fb-9ce5a9e97862}" Type="Device">
    
         </Group>
     </PolicyGroups>
    ```
2. Save the XML file to your network share.
3. In the **Microsoft Defender Antivirus** policy tree, select **Device Control**.
4. In the details pane of **Device Control**, open the **Define device control policy groups** setting.
5. In the **Define device control policy groups** window, configure the following options:

    1. Select **Enabled**.
    2. Under **Options**, in the **Define the policy groups here** box, specify the network share file path that contains the XML groups data.

For an example that defines any removable storage, CD-ROM, Windows portable devices, and approved USBs groups, see the [removable storage group XML file](https://github.com/microsoft/mdatp-devicecontrol/blob/main/windows/device/Group%20Policy/Scenario%202%20GPO%20Removable%20Storage%20Group.xml).

Note

You can use XML comments in the format `<!--COMMENT-->` in rule and group XML files. Place comments inside the first XML tag, not on the first line of the XML file.

### Define device control policies in Group Policy

Create and deploy one XML file for each removable storage access policy rule:

1. Use the properties in the removable storage access policy rule to create an XML file. Make sure the root node is `PolicyRules`. For example:

    ```xml
    <PolicyRules>
      <PolicyRule Id="{d8819053-24f4-444a-a0fb-9ce5a9e97862}">
          ...
       </PolicyRule>
    </PolicyRules>
    ```
2. Save the XML file to a network share.
3. In the **Microsoft Defender Antivirus** policy tree, select **Device Control**.
4. In the details pane of **Device Control**, open the **Define device control policy rules** setting.
5. In the **Define device control policy rules** window, configure the following options:

    1. Select **Enabled**.
    2. Under **Options**, in the **Define the policy rules here** box, specify the network share file path that contains the XML rules data.

### Validate device control XML files with MpCmdRun

The MpCmdRun command-line utility can validate XML files used for Group Policy deployments. Validation detects syntax errors that the device control engine might encounter when it parses the settings.

To validate the XML files, follow these steps:

1. In an elevated Command Prompt (a Command Prompt window you opened by selecting **Run as administrator**), run the following commands. Replace the example XML file paths with the paths to your rules and groups XML files.

    Tip

    The first command changes the directory to the latest version of &lt;antimalware platform version&gt; in `%ProgramData%\Microsoft\Windows Defender\Platform\<antimalware platform version>`. If that path doesn't exist, it goes to `%ProgramFiles%\Windows Defender`.

    ```dos
    (set "_done=" & if exist "%ProgramData%\Microsoft\Windows Defender\Platform\" (for /f "delims=" %d in ('dir "%ProgramData%\Microsoft\Windows Defender\Platform" /ad /b /o:-n 2^>nul') do if not defined _done (cd /d "%ProgramData%\Microsoft\Windows Defender\Platform\%d" & set _done=1)) else (cd /d "%ProgramFiles%\Windows Defender")) >nul 2>&1
    
    MpCmdRun.exe -DeviceControl -TestPolicyXml "C:\Policies\PolicyRules.xml" -Rules
    
    MpCmdRun.exe -DeviceControl -TestPolicyXml "C:\Policies\Groups.xml" -Groups
    ```

If there are no errors, the following output is shown:

```console
DC policy rules parsing succeeded
Verifying absolute rules data against the original data
Rules verified with success
DC policy groups parsing succeeded
Verifying absolute groups data against the original data
Groups verified with success
Has Group Dependency Loop: no
```

Note

To capture evidence of files that are copied or printed, use [Endpoint DLP](/en-us/purview/dlp-copy-matched-items-get-started?tabs=purview-portal%2Cpurview).

You can use XML comments in the format `<!-- COMMENT -->` in rule and group XML files. Place comments inside the first XML tag, not on the first line of the XML file.