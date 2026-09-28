---
layout: Conceptual
title: Block potentially unwanted applications with Microsoft Defender Antivirus - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/detect-block-potentially-unwanted-apps-microsoft-defender-antivirus
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Enable the potentially unwanted application (PUA) antivirus feature to block unwanted software such as adware.
ms.service: defender-endpoint
ms.localizationpriority: high
author: chrisda
ms.author: chrisda
ms.custom: nextgen, msecd-doc-authoring-1015
ms.reviewer: yongrhee, mimilone, julih
ms.subservice: ngp
ms.topic: how-to
ms.collection:
- m365-security
- tier2
- mde-ngp
ms.date: 2026-09-15T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: ced9c93b-f023-b2f5-dcaa-7b6fea426b3d
document_version_independent_id: ced9c93b-f023-b2f5-dcaa-7b6fea426b3d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/detect-block-potentially-unwanted-apps-microsoft-defender-antivirus.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: detect-block-potentially-unwanted-apps-microsoft-defender-antivirus
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/detect-block-potentially-unwanted-apps-microsoft-defender-antivirus.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5287f575-02f0-405f-92b7-800456526b0c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/06e86142-34c2-4b94-ab9c-9477c21f7152
platformId: a766f1dd-dfd4-e10f-43d5-86bdffad8a44
---

# Block potentially unwanted applications with Microsoft Defender Antivirus - Microsoft Defender for Endpoint | Microsoft Learn

Learn how to detect and block potentially unwanted applications (PUA) using Microsoft Defender Antivirus and Microsoft Edge. This article covers how to enable PUA protection, configure it across management tools, and review PUA detection events.

## About potentially unwanted applications (PUA)

Potentially unwanted applications (PUA) are a category of software that can cause your machine to run slowly, display unexpected ads, or at worst, install other software that might be unexpected or unwanted. PUA isn't considered a virus, malware, or other type of threat, but it might perform actions on endpoints that adversely affect endpoint performance or use. The term *PUA* can also refer to an application that has a poor reputation, as assessed by Microsoft Defender for Endpoint, due to certain kinds of undesirable behavior.

Here are some examples:

- **Advertising software** that displays advertisements or promotions, including software that inserts advertisements to webpages.
- **Bundling software** that offers to install other software that isn't digitally signed by the same entity. Also, software that offers to install other software that qualifies as PUA.
- **Evasion software** that actively tries to evade detection by security products, including software that behaves differently in the presence of security products.

Tip

For more examples and a discussion of the criteria we use to label applications for special attention from security features, see [How Microsoft identifies malware and potentially unwanted applications](/en-us/defender-xdr/criteria).

Potentially unwanted applications can increase the risk of your network being infected with actual malware, make malware infections harder to identify, or cost your IT and security teams time and effort to clean them up. If your organization's subscription includes [Microsoft Defender for Endpoint](microsoft-defender-endpoint), you can also set Microsoft Defender Antivirus PUA to block, in order to block apps that are considered to be PUA on Windows devices.

[Learn more about Windows Enterprise subscriptions](https://www.microsoft.com/microsoft-365/windows/windows-11-enterprise).

Tip

As a companion to this article, see our [Microsoft Defender for Endpoint setup guide](https://go.microsoft.com/fwlink/p/?linkid=2268087) to review best practices and learn about essential tools such as attack surface reduction and next-generation protection. For a customized experience based on your environment, you can access the Defender for [Endpoint automated setup guide](https://go.microsoft.com/fwlink/p/?linkid=2268088) in the Microsoft 365 admin center.

## Prerequisites

### Supported operating systems

**Windows client:**

- Windows 11
- Windows 10
- Windows 8.1

**Windows Server:**

- Windows Server 2016 and later
- Windows Server, version 1803 or later
- Windows Server 2012 R2 (Requires Microsoft Defender for Endpoint)

**Other platforms:**

- Azure Stack HCI OS, version 23H2 and later
- For macOS, see [Detect and block potentially unwanted applications with Defender for Endpoint on macOS](mac-pua).
- For Linux, see [Detect and block potentially unwanted applications with Defender for Endpoint on Linux](linux-pua).

## Configure PUA protection in Microsoft Edge

The [new Microsoft Edge](https://support.microsoft.com/edge/get-to-know-microsoft-edge), which is Chromium-based, blocks potentially unwanted application downloads and associated resource URLs. This feature is provided via [Microsoft Defender SmartScreen](/en-us/windows/security/operating-system-security/virus-and-threat-protection/microsoft-defender-smartscreen/).

### Enable PUA protection in Chromium-based Microsoft Edge

Although potentially unwanted application protection in Microsoft Edge (Chromium-based, version 80.0.361.50) is turned off by default, it can easily be turned on from within the browser.

1. In your Microsoft Edge browser, select the ellipses, and then choose **Settings**.
2. Select **Privacy, search, and services**.
3. Under the **Security** section, turn on **Block potentially unwanted apps**.

Tip

If you're running Microsoft Edge (Chromium-based), you can safely explore the URL-blocking feature of PUA protection by testing it out on one of our [Microsoft Defender SmartScreen demo pages](https://demo.smartscreen.msft.net/).

### Block URLs with Microsoft Defender SmartScreen

In Chromium-based Microsoft Edge with PUA protection turned on, Microsoft Defender SmartScreen protects you from PUA-associated URLs.

Security administrators can [configure Microsoft Edge](/en-us/DeployEdge/configure-microsoft-edge) to control how Microsoft Edge and Microsoft Defender SmartScreen work together to protect groups of users from PUA-associated URLs. There are several [Microsoft Defender SmartScreen group policy settings](/en-us/DeployEdge/microsoft-edge-policies#smartscreen-settings) available, including [the SmartScreenPuaEnabled policy](/en-us/DeployEdge/microsoft-edge-policies#smartscreenpuaenabled). In addition, admins can [configure Microsoft Defender SmartScreen](/en-us/microsoft-edge/deploy/available-policies?source=docs#configure-windows-defender-smartscreen) as a whole, using group policy settings to turn Microsoft Defender SmartScreen on or off.

Although Microsoft Defender for Endpoint has its own blocklist based upon a data set managed by Microsoft, you can customize this list based on your own threat intelligence. If you [create and manage indicators in the Microsoft Defender for Endpoint portal](indicators-overview), Microsoft Defender SmartScreen respects the new settings.

## Microsoft Defender Antivirus and PUA protection

The potentially unwanted application (PUA) protection feature in Microsoft Defender Antivirus can detect and block PUA on endpoints in your network.

Microsoft Defender Antivirus blocks detected PUA files and any attempts to download, move, run, or install them. Blocked PUA files are then moved to quarantine. When a PUA file is detected on an endpoint, Microsoft Defender Antivirus sends a notification to the user ([unless notifications are disabled](configure-notifications-microsoft-defender-antivirus)) in the same format as other threat detections. The notification is prefaced with `PUA:` to indicate its content.

The notification appears in the usual [quarantine list within the Windows Security app](microsoft-defender-security-center-antivirus).

## Configure PUA protection in Microsoft Defender Antivirus

You can enable PUA protection with Microsoft Defender for Endpoint Security Settings Management, [Microsoft Intune](/en-us/intune/intune-service/protect/device-protect), [Microsoft Configuration Manager](/en-us/intune/configmgr/protect/deploy-use/endpoint-protection), [Group Policy](/en-us/azure/active-directory-domain-services/manage-group-policy), or via [Microsoft Defender Antivirus PowerShell cmdlets](/en-us/powershell/module/defender/?preserve-view=true&amp;view=win10-ps).

At first, try using PUA protection in audit mode. It detects potentially unwanted applications without actually blocking them. Detections are captured in the Windows Event log. PUA protection in audit mode is useful if your company is conducting an internal software security compliance check and it's important to avoid false positives.

Scenarios and default settings for PUA protection depend on whether devices are onboarded to Defender for Endpoint or Microsoft Defender for Business.

### Microsoft Defender Antivirus without devices onboarded to Defender for Endpoint

The following table shows the default PUA protection settings for devices that aren't onboarded to Defender for Endpoint:

| Scenarios | Security intelligence update version | PUA protection default setting |
| --- | --- | --- |
| Windows 10 or laterWindows Server 2016 or later | older than 1.329.495.0 | Disabled (0) |
| Windows 10 or laterWindows Server 2016 or later | 1.329.495.0 or later | Audit mode (2) |

### Microsoft Defender Antivirus with devices onboarded to Defender for Endpoint Plan 1/Plan 2 or Defender for Business

The following table shows the default PUA protection settings for devices onboarded to Defender for Endpoint Plan 1, Plan 2, or Defender for Business:

| Scenarios | Security intelligence update version | Smart App Control | PUA protection default setting |
| --- | --- | --- | --- |
| Windows 10, version 2004 or laterWindows Server 2012 R2 and Windows Server 2016 with the [modern unified solution for Windows Server 2016 and 2012 R2](onboard-server#functionality-in-the-modern-unified-solution-for-windows-server-2016-and-windows-server-2012-r2)Windows Server 2019 or later | Older than 1.329.495.0 | Feature not available | Audit mode (2) |
| Windows 11, version 22H2 or later | 1.329.495.0 or later | Available | Audit mode (2) |
| Windows 10, version 2004 or laterWindows Server 2012 R2 and Windows Server 2016 with the [modern unified solution for Windows Server 2016 and 2012 R2](onboard-server#functionality-in-the-modern-unified-solution-for-windows-server-2016-and-windows-server-2012-r2)Windows Server 2019 or later | 1.329.495.0 or later | Feature not available | Block mode (1) |

Tip

To enforce PUA protection in block mode, use any of the following management methods:

- Defender for Endpoint Security Settings Management
- Intune
- Configuration Manager
- Group Policy
- PowerShell

### Use Microsoft Defender for Endpoint Security Settings Management to configure PUA protection

For more information about using Defender for Endpoint Security Settings Management to configure PUA protection, see [Use Microsoft Defender for Endpoint Security Settings Management to manage Microsoft Defender Antivirus](/en-us/intune/intune-service/protect/mde-security-integration)

### Use Intune to configure PUA protection

Microsoft Intune is the recommended tool for configuring and distributing Defender for Endpoint features to devices. However, Intune is a separate product that isn't part of Defender for Endpoint, and it isn't included in all subscriptions. To use Intune, you need a subscription that includes it, or you can buy it separately as a standalone subscription or add-on. If you don't have Intune, you can use any of the other methods in this article. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).

For information about configuring PUA protection through Intune device restriction settings, see the following articles:

- [Configure device restriction settings in Microsoft Intune](/en-us/intune/intune-service/configuration/device-restrictions-configure)
- [Microsoft Defender Antivirus device restriction settings for Windows 10 in Intune](/en-us/intune/intune-service/configuration/device-restrictions-windows-10#microsoft-defender-antivirus)

### Use Configuration Manager to configure PUA protection

PUA protection is enabled by default in the Microsoft Configuration Manager (Current Branch).

See [How to create and deploy anti-malware policies: Scheduled scans settings](/en-us/intune/configmgr/protect/deploy-use/endpoint-antimalware-policies#real-time-protection-settings) for details on configuring Microsoft Configuration Manager (Current Branch).

For System Center 2012 Configuration Manager, see [How to Deploy Potentially Unwanted Application Protection Policy for Endpoint Protection in Configuration Manager](/en-us/previous-versions/system-center/system-center-2012-R2/hh508770%28v=technet.10%29#BKMK_PUA).

Note

PUA events blocked by Microsoft Defender Antivirus are reported in the Windows Event Viewer and not in Microsoft Configuration Manager.

### Use Group Policy to configure PUA protection

Perform the following steps to configure PUA protection by using Group Policy:

Note

If the **Configure detection for potentially unwanted applications** setting isn't available in your GPMC, update the Administrative Templates files in your Central Store. The setting is included in the Windows 10, version 1809 Administrative Templates and later. For download links and instructions, see [Create and manage the Central Store for Group Policy Administrative Templates in Windows](/en-us/troubleshoot/windows-client/group-policy/create-and-manage-central-store).

1. In Centralized Group Policy, open the [Group Policy Management Console (GPMC)](/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-management-console) on your Group Policy management computer.
2. In the GPMC console tree, expand Group Policy Objects in the forest and domain containing the GPO you want to edit.
3. Right-click the GPO, and then select **Edit**.
4. In the **Group Policy Management Editor**, go to **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus**.

    Note

    Group Policy paths before Windows 10, version 2004 (May 2020) might use *Windows* Defender Antivirus instead of *Microsoft* Defender Antivirus. Both names refer to the same policy location.
5. In the details pane of **Microsoft Defender Antivirus**, open the **Configure detection for potentially unwanted applications** setting. To open the setting, use any of the following methods:

    - Double-click the setting.
    - Right-click the setting, and then select **Edit**.
    - Select the setting, and then select **Action** &gt; **Edit**.
6. In the setting window that opens, configure the following options:

    1. Select **Enabled**.
    2. **Options**section: Select one of the following values:
        - **Block**: Block potentially unwanted applications.
        - **Audit Mode**: Test how the setting works in your environment.

    When you're finished, select **OK**.

Tip

You can also configure Group Policy locally on individual devices by using the Local Group Policy Editor (`gpedit.msc`). Navigate to the same path: **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus**.

### Use PowerShell cmdlets to configure PUA protection

Use the following PowerShell cmdlets to enable, audit, disable, or query PUA protection in Microsoft Defender Antivirus.

#### To enable PUA protection

Enable PUA protection in Microsoft Defender Antivirus to block potentially unwanted applications on the device:

```PowerShell
Set-MpPreference -PUAProtection Enabled
```

Setting the value for this cmdlet to `Enabled` turns on PUA protection in Microsoft Defender Antivirus if it's disabled.

#### To set PUA protection to audit mode

Use audit mode to log PUA detections without blocking apps, so you can evaluate the impact before enforcement:

```PowerShell
Set-MpPreference -PUAProtection AuditMode
```

Setting `AuditMode` detects PUAs without blocking them.

#### To disable PUA protection

We recommend keeping PUA protection turned on. However, you can disable PUA protection in Microsoft Defender Antivirus for troubleshooting or policy rollback by using the following cmdlet:

```PowerShell
Set-MpPreference -PUAProtection Disabled
```

Setting the value for this cmdlet to `Disabled` turns off PUA protection in Microsoft Defender Antivirus if it has been enabled.

#### To query the PUA status

To confirm the current PUA protection setting on the device, query the Microsoft Defender Antivirus preferences:

```powershell
Get-MpPreference | Format-Table PUAProtection
```

| Value | Description |
| --- | --- |
| `0` | PUA Protection off (Default). Microsoft Defender Antivirus won't protect against potentially unwanted applications. |
| `1` | PUA Protection on. Detected items are blocked. They'll show in history along with other threats. |
| `2` | Audit mode. Microsoft Defender Antivirus detects potentially unwanted applications but takes no action. You can review information about the applications Microsoft Defender Antivirus would've taken action against by searching for events created by Microsoft Defender Antivirus in the Event Viewer, but not in the [Microsoft Defender portal](https://security.microsoft.com). |

For more information about managing Microsoft Defender Antivirus with PowerShell, see [Use PowerShell cmdlets to configure and run Microsoft Defender Antivirus](use-powershell-cmdlets-microsoft-defender-antivirus) and [Defender Antivirus cmdlets](/en-us/powershell/module/defender/index).

## Test and make sure that PUA blocking works

Once you have PUA enabled in block mode, you can test to make sure that it's working properly. For more information, see [Potentially unwanted applications (PUA) demonstration](defender-endpoint-demonstration-potentially-unwanted-applications).

## View PUA events using PowerShell

PUA events are reported in the Windows Event Viewer, but not in Microsoft Configuration Manager or in Intune. You can also use the `Get-MpThreat` cmdlet to view threats that Microsoft Defender Antivirus handled. The following sample output shows the details returned for a detected PUA item, including its execution status, severity, and threat name:

```console
CategoryID       : 27
DidThreatExecute : False
IsActive         : False
Resources        : {webfile:_q:\Builds\Dalton_Download_Manager_3223905758.exe|http://d18yzm5yb8map8.cloudfront.net/
                    fo4yue@kxqdw/Dalton_Download_Manager.exe|pid:14196,ProcessStart:132378130057195714}
RollupStatus     : 33
SchemaVersion    : 1.0.0.0
SeverityID       : 1
ThreatID         : 213927
ThreatName       : PUA:Win32/InstallCore
TypeID           : 0
PSComputerName   :
```

## Get email notifications about PUA detections

You can turn on email notifications to receive mail about PUA detections. For more information about Microsoft Defender Antivirus events, see [Troubleshoot event IDs](troubleshoot-microsoft-defender-antivirus). PUA events are recorded under event ID **1160**.

## View PUA events using advanced hunting

If you're using [Microsoft Defender for Endpoint](microsoft-defender-endpoint), you can use an advanced hunting query to view PUA events. The following query searches the `DeviceEvents` table for `AntivirusDetection` actions and filters results to PUA-related detections, showing details such as the device name, file path, and remediation status:

```console
DeviceEvents
| where ActionType == "AntivirusDetection"
| extend x = parse_json(AdditionalFields)
| project Timestamp, DeviceName, FolderPath, FileName, SHA256, ThreatName = tostring(x.ThreatName), WasExecutingWhileDetected = tostring(x.WasExecutingWhileDetected), WasRemediated = tostring(x.WasRemediated)
| where ThreatName startswith_cs 'PUA:'
```

To learn more about advanced hunting, see [Proactively hunt for threats with advanced hunting](/en-us/defender-xdr/advanced-hunting-overview).

## Exclude files from PUA protection

Sometimes a file is erroneously blocked by PUA protection, or a feature of a PUA is required to complete a task. In these cases, a file can be added to an exclusion list.

For more information, see [Configure and validate exclusions based on file extension and folder location](microsoft-defender-antivirus-exclusions-configure).