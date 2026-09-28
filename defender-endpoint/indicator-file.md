---
layout: Conceptual
title: Create indicators for files - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/indicator-file
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
ms.reviewer: yongrhee
description: Create indicators for a file hash that define the detection, prevention, and exclusion of entities.
ms.service: defender-endpoint
ms.author: lwainstein
author: limwainstein
ms.localizationpriority: medium
ms.date: 2026-07-03T00:00:00.0000000Z
ms.collection:
- m365-security
- tier2
- mde-asr
ms.topic: how-to
ms.subservice: asr
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: e82a1df8-8d06-742d-10db-432f4b45721a
document_version_independent_id: e82a1df8-8d06-742d-10db-432f4b45721a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/indicator-file.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: indicator-file
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/indicator-file.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 69cd24d8-04ae-400e-985f-fec9d83a0b44
---

# Create indicators for files - Microsoft Defender for Endpoint | Microsoft Learn

Important

In Defender for Endpoint Plan 1 and Defender for Business, you can create an indicator to block or allow a file. In Defender for Business, your indicator is applied across your environment and cannot be scoped to specific devices.

Note

For file indicators to work on Windows Server 2016 and Windows Server 2012 R2, those devices must be onboarded using the [modern unified solution for Windows Server 2016 and Windows Server 2012 R2](onboard-server#functionality-in-the-modern-unified-solution-for-windows-server-2016-and-windows-server-2012-r2). Custom file indicators with the Allow, Block and Remediate actions are now also available in the [enhanced anti-malware engine capabilities for macOS and Linux](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/enhanced-antimalware-engine-capabilities-for-linux-and-macos/ba-p/3292003).

File indicators prevent further propagation of an attack in your organization by banning potentially malicious files or suspected malware. If you know a potentially malicious portable executable (PE) file, you can block it. Blocking the file prevents it from being read, written, or executed on devices in your organization. Before you begin, review the prerequisites for supported operating systems and platform-specific requirements.

There are three ways you can create indicators for files:

- By creating an indicator through the settings page
- By creating a contextual indicator using the add indicator button from the file details page
- By creating an indicator programmatically through the [Indicator API](api/ti-indicator)

## Prerequisites

Understand the following prerequisites before you create indicators for files:

- [Enable behavior monitoring](behavior-monitor)
- [Turn on cloud-based protection](cloud-protection-configure).
- [Configure cloud protection network connectivity](configure-network-connections-microsoft-defender-antivirus)

### Supported operating systems

The following operating systems support file indicators:

- Windows 10, version 1703 or later
- Windows 11
- Windows Server 2012 R2
- Windows Server 2016 or later
- Azure Stack HCI OS, version 23H2 and later.

### Windows prerequisites

Before creating file indicators on Windows, make sure the following requirements are met:

- This feature is available if your organization uses [Microsoft Defender Antivirus](microsoft-defender-antivirus-windows) (in active mode)
- The anti-malware client version must be `4.18.1901.x` or later. See [Monthly platform and engine versions](microsoft-defender-endpoint-releases#microsoft-defender-antivirus-releases)
- File hash computation is enabled by setting `Computer Configuration\Administrative Templates\Windows Components\Microsoft Defender Antivirus\MpEngine\Enable File Hash Computation` to **Enabled**. Or, you can run the following PowerShell command: `Set-MpPreference -EnableFileHashComputation $true`

Note

File indicators support portable executable (PE) files, including `.exe` and `.dll` files only.

### macOS prerequisites

Before creating file indicators on macOS, verify the following prerequisites:

- Real-time protection (RTP) needs to be active.
- [Configure file hash computation on macOS](mac-resources#configuring-from-the-command-line). Run the following command: `mdatp config enable-file-hash-computation --value enabled`

Note

On macOS, file indicators support three types of files: Mach-O executables, POSIX shell scripts (e.g., those run by sh or bash), and AppleScript files (.scpt). (Mach-O is macOS's native executable format, comparable to .exe and .dll on Windows.)

### Linux prerequisites

Before creating file indicators on Linux, ensure the following prerequisites are in place:

- Available in Defender for Endpoint version `101.85.27` or later.
- [Configure file hash computation on Linux](linux-preferences#configure-file-hash-computation-feature) in the Microsoft Defender portal or in the managed JSON
- Behavior monitoring enabled is preferred, but file indicators work with any other scan (RTP or Custom).

Note

On Linux, file indicators support script files (.sh files) and ELF files.

## Create an indicator for files from the settings page

To create a file indicator from the settings page, perform the following steps:

1. In the navigation pane, select **System** &gt; **Settings** &gt; **Endpoints** &gt; **Indicators** (under **Rules**).
2. Select the **File hashes** tab.
3. Select **Add item**.
4. Specify the following details:

    - Indicator: Specify the entity details and define the expiration of the indicator.
    - Action: Specify the action to be taken and provide a description.
    - Scope: Define the scope of the device group (scoping isn't available in [Defender for Business](/en-us/defender-business/mdb-overview)).
5. Review the details in the Summary tab, then select **Save**.

## Create a contextual indicator from the file details page

One of the options when taking [response actions on a file](respond-file-alerts) is adding an indicator for the file. When you add an indicator hash for a file, you can choose to raise an alert and block the file whenever a device in your organization attempts to run it.

Files automatically blocked by an indicator won't show up in the file's Action center, but the alerts will still be visible in the Alerts queue.

## Block files

To block files by using indicators, complete the following step:

1. To start blocking files, [turn on the "block or allow" feature](advanced-features) in Settings (in the [Microsoft Defender portal](https://security.microsoft.com), go to **Settings** &gt; **Endpoints** &gt; **General** &gt; **Advanced features** &gt; **Allow or block file**).

## Alerting on file blocking actions (preview)

Important

This information relates to the **Automated investigation and remediation engine** public preview, which is a prerelease product that might be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

The current supported actions for file IOC are allow, audit and block, and remediate. After choosing to block a file, you can choose whether triggering an alert is needed. By choosing whether to generate an alert for the block event, you can control the number of alerts sent to your security operations teams and ensure that only necessary alerts are raised.

1. In the [Microsoft Defender portal](https://security.microsoft.com), go to **Settings** &gt; **Endpoints** &gt; **Indicators** &gt; **Add New File Hash**.
2. Choose to block and remediate the file.
3. Specify whether to generate an alert on the file block event and define the alerts settings:

    - The alert title
    - The alert severity
    - Category
    - Description
    - Recommended actions

    [![The Alert settings for file indicators](media/indicators-generate-alert.png)](media/indicators-generate-alert.png#lightbox)

    Important

    - Typically, file blocks are enforced and removed within 15 minutes, average 30 minutes but can take upwards of 2 hours.
    - If there are conflicting file IoC policies with the same enforcement type and target, the policy of the more secure hash will be applied. An SHA-256 file hash IoC policy will win over an SHA-1 file hash IoC policy, which will win over an MD5 file hash IoC policy if the hash types define the same file. This is always true regardless of the device group.
    - In all other cases, if conflicting file IoC policies with the same enforcement target are applied to all devices and to the device's group, then for a device, the policy in the device group will win.
    - If the EnableFileHashComputation group policy is disabled, the blocking accuracy of the file IoC is reduced. However, enabling `EnableFileHashComputation` may impact device performance. For example, copying large files from a network share onto your local device, especially over a VPN connection, might have an effect on device performance. For more information about the EnableFileHashComputation group policy, see [Defender CSP](/en-us/windows/client-management/mdm/defender-csp). For more information on configuring this feature on Defender for Endpoint on Linux and macOS, see [Configure file hash computation feature on Linux](linux-preferences#configure-file-hash-computation-feature) and [Configure file hash computation feature on macOS](mac-preferences#configure-file-hash-computation-feature).

## Advanced hunting capabilities for file indicators (preview)

Important

The following advanced hunting capabilities information relates to the **Automated investigation and remediation engine** public preview, which is a prerelease product that might be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

Currently in preview, you can query the response action activity in advanced hunting. The following sample advanced hunting query shows how to query response action activity:

```console
search in (DeviceFileEvents, DeviceProcessEvents, DeviceEvents, DeviceRegistryEvents, DeviceNetworkEvents, DeviceImageLoadEvents, DeviceLogonEvents)
Timestamp > ago(30d)
| where AdditionalFields contains "EUS:Win32/CustomEnterpriseBlock!cl"
```

For more information about advanced hunting, see [Proactively hunt for threats with advanced hunting](/en-us/defender-xdr/advanced-hunting-overview).

Here are other threat names that can be used in the sample query:

Files:

- `EUS:Win32/CustomEnterpriseBlock!cl`
- `EUS:Win32/CustomEnterpriseNoAlertBlock!cl`

Certificates:

- `EUS:Win32/CustomCertEnterpriseBlock!cl`

The response action activity can also be viewable in the device timeline.

## Policy conflict handling for file indicators

Cert and File IoC policy handling conflicts follow this order:

1. If the file isn't allowed by Windows Defender Application Control and AppLocker enforce mode policies, then **Block**.
2. Else, if the file is allowed by the Microsoft Defender Antivirus exclusions, then **Allow**.
3. Else, if the file is blocked or warned by a block or warn file IoCs, then **Block/Warn**.
4. Else, if the file is blocked by SmartScreen, then **Block**.
5. Else, if the file is allowed by an allow file IoC policy, then **Allow**.
6. Else, if the file is blocked by attack surface reduction rules, controlled folder access, or antivirus protection, then **Block**.
7. Else, **Allow** (passes Windows Defender Application Control & AppLocker policy, no IoC rules apply to it).

Note

In situations when Microsoft Defender Antivirus is set to **Block**, but Defender for Endpoint indicators for file hash or certificates are set to **Allow**, the policy defaults to **Allow**.

Note

In situations where a certificate-based indicator is configured to **Block**, but a file hash indicator for one of its signed files is configured to **Allow**, this configuration is **not supported by design**. Certificate-based indicators have higher precedence in the Defender evaluation pipeline and will always override file hash allow indicators. A configuration that simultaneously:

- blocks a certificate, and
- attempts to allow one of its signed files via file hash

is **not supported**. Certificate-based indicators take precedence, and therefore the file will continue to be blocked.

If there are conflicting file IoC policies with the same enforcement type and target, the policy of the more secure (meaning longer) hash is applied. For example, an SHA-256 file hash IoC policy takes precedence over an MD5 file hash IoC policy if both hash types define the same file.

Warning

Policy conflict handling for files and certs differ from policy conflict handling for domains/URLs/IP addresses.

Microsoft Defender Vulnerability Management's block vulnerable application features uses the file IoCs for enforcement and follows the Policy conflict handling order.

### Examples

The following examples show how component enforcement interacts with file indicator actions:

| Component | Component enforcement | File indicator Action | Result |
| --- | --- | --- | --- |
| Antivirus protection | Block | Allow | Allow |
| Attack surface reduction file path exclusion | Allow | Block | Block |
| Attack surface reduction rule | Block | Allow | Allow |
| Windows Defender Application Control | Allow | Block | Allow |
| Windows Defender Application Control | Block | Allow | Block |
| Microsoft Defender Antivirus exclusion | Allow | Block | Allow |