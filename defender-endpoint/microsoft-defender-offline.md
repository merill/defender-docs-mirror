---
layout: Conceptual
title: Microsoft Defender Offline scan in Windows - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/microsoft-defender-offline
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: You can use Microsoft Defender Offline Scan straight from the Microsoft Defender Antivirus app. You can also manage how it's deployed in your network.
ms.service: defender-endpoint
ms.localizationpriority: medium
ms.date: 2026-07-03T00:00:00.0000000Z
author: limwainstein
ms.author: lwainstein
ms.custom: nextgen, msecd-doc-authoring-1016
ms.reviewer: yongrhee
ms.subservice: ngp
ms.topic: how-to
ms.collection:
- m365-security
- tier2
- mde-ngp
ai-usage: ai-assisted
locale: en-us
document_id: dedb98ad-6659-a92e-e34d-d1a1cf613046
document_version_independent_id: dedb98ad-6659-a92e-e34d-d1a1cf613046
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/microsoft-defender-offline.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: microsoft-defender-offline
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/microsoft-defender-offline.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: a158645e-cda2-4716-5b63-05f0518e48bd
---

# Microsoft Defender Offline scan in Windows - Microsoft Defender for Endpoint | Microsoft Learn

| Applies to | Type |
| --- | --- |
| **Platform** | Windows |
| **Protection type** | Hardware |
| **Firmware/ Rootkit** | Operating system  Driver  Memory (Heap)  Application  Identity  Cloud |

Note

The protection for Microsoft Defender Offline Scan focuses on firmware and rootkits.

Microsoft Defender Offline is an anti-malware scanning tool that lets you boot and run a scan from a trusted environment. The scan runs from outside the normal Windows kernel so it can target malware that attempts to bypass the Windows shell, such as viruses and rootkits that infect or overwrite the master boot record (MBR).

You can use Microsoft Defender Offline Scan if you suspect a malware infection, or you want to confirm a thorough clean of the endpoint after a malware outbreak.

## Prerequisites and requirements

The following are the hardware requirements for Microsoft Defender Offline Scan in Windows:

- x64 Windows 11
- x64/x86 Windows 10
- x64/x86 Windows 8.1
- x64/x86 Windows 7 Service Pack 1

Caution

Microsoft Defender Offline Scan does not apply to:

- ARM Windows 11
- ARM Windows 10
- Windows Server Stock Keeping Units (SKU's)

For more information about Windows 10 and Windows 11 requirements, see [Minimum hardware requirements](/en-us/windows-hardware/design/minimum/minimum-hardware-requirements-overview) and [Hardware component guidelines](/en-us/windows-hardware/design/component-guidelines/components).

Important

If BitLocker is enabled on the system drive, suspend BitLocker protection before running Microsoft Defender Offline. Otherwise, you may be prompted to enter the BitLocker recovery key when the system restarts into the offline environment. For instructions, see [Suspend BitLocker protection](/en-us/troubleshoot/windows-client/windows-security/suspend-bitlocker-protection-non-microsoft-updates).

## Microsoft Defender Offline updates

To receive Microsoft Defender Offline Scan updates:

- Microsoft Defender Antivirus must be your primary antivirus software (not in passive mode).
- Update Microsoft Defender Antivirus how you normally deploy updates to endpoints. Use a supported version of the:

    - [Platform Update](https://www.microsoft.com/wdsi/defenderupdates)
    - [Engine Update](microsoft-defender-antivirus-updates)
    - Security Intelligence Updates

        - You can manually download and install the latest protection updates from the [Microsoft Malware Protection Center](https://www.microsoft.com/wdsi/defenderupdates)
        - See the [Manage Microsoft Defender Antivirus Security intelligence updates](manage-protection-updates-microsoft-defender-antivirus) article for more information.
- Users must be signed in with local administrator privileges.
- Windows Recovery Environment (WinRE) needs to be enabled.

Note

If WinRE is disabled, the Windows Defender Offline scan doesn't run and no error messages are displayed. Nothing happens even if the machine is restarted manually. To resolve this issue, enable WinRE.

- To check the WinRE status, you can execute this command-line: `reagentc /info`.
- If the status is Disabled, you can enable it by executing this command-line: `reagentc /enable`.

## Usage scenarios

The need to run Microsoft Defender Offline Scan:

If Microsoft Defender Antivirus determines that you need to run Microsoft Defender Offline, it prompts the user on the device. The prompt can occur via a notification, similar to the following:

[![Notification to run Microsoft Defender Offline](/en-us/defender/media/notification.png)](/en-us/defender/media/notification.png#lightbox)

The user is also notified within the Microsoft Defender Antivirus client. If you're using Intune to manage devices, you can see the notification in Intune.

- You can manually force an offline scan that is built-in Windows 10, version 1607 or newer, and Windows 11. Or, for older operating systems such as Windows 7 SP1 and Windows 8.1, you can create bootable media to run an offline scan (see the In Windows 7 Service Pack 1 and Windows 8.1 section).

In Configuration Manager, you can identify the status of endpoints by navigating to **Monitoring &gt; Overview &gt; Security &gt; Endpoint Protection Status &gt; System Center Endpoint Protection Status**.

Microsoft Defender Offline scans are indicated under **Malware remediation status** as **Offline scan required**.

[![The indicator for a scan for Microsoft Defender Offline](/en-us/defender/media/sccm-wdo.png)](/en-us/defender/media/sccm-wdo.png#lightbox)

## Configure notifications

Microsoft Defender Offline notifications are configured in the same policy setting as other Microsoft Defender Antivirus notifications.

For more information about notifications in Windows Defender, see [Configure the notifications that appear on endpoints](configure-notifications-microsoft-defender-antivirus).

## Run a scan

Important

Before you use Microsoft Defender Offline Scan, **make sure you save any files** and shut down running programs. The Microsoft Defender Offline scan takes about 15 minutes to run. It will restart the endpoint when the scan is complete. The scan is performed outside of the usual Windows operating environment. The user interface will appear different to a normal scan performed by Windows Defender. After the scan is completed, the endpoint will be restarted and Windows will load normally.

You can run a Microsoft Defender Offline scan with the following methods:

- The Windows Security app
- PowerShell
- Windows Management Instrumentation (WMI)

### Use the Windows Defender Security app to run an offline scan

Starting with Windows 10, version 1607 or newer, and Windows 11, Microsoft Defender Offline Scan can be run with one click directly from the [Windows Security app](microsoft-defender-security-center-antivirus). In previous versions of Windows, a user had to install Microsoft Defender Offline Scan to bootable media, restart the endpoint, and load the bootable media.

Note

In Windows 10, version 1607, the offline scan can be run from **Windows Settings &gt; Update & security &gt; Windows Defender** or from the Windows Defender client.

1. On your Windows device, open the **Windows Security** app. Select **Virus & threat protection**, and then choose **Scan options**.
2. Select the radio button **Microsoft Defender Offline scan** and select **Scan now**.

    The offline scan process starts from `C:\ProgramData\Microsoft\Windows Defender\Offline Scanner`.
3. You get a prompt to save your work before continuing, similar to the following image:

    ![Screenshot of screen prompt to save all work before continuing.](/en-us/defender/media/defender-offline-save-work.png)

    After you saved your work, select **Scan**.
4. After you select **Scan**, you get another prompt requesting your permission to make changes to your device, similar to the following image:

    ![Screenshot of a screen prompt requesting permission to apply.](/en-us/defender/media/defender-offline-apply-change.png)

    Select **Yes**.
5. Another prompt appears and informs you that you'll be signed out and Windows will shut down in less than a minute, similar to the following image:

    ![Screenshot of a screen prompt informing about the sign out.](/en-us/defender/media/defender-offline-sign-out-notification.png)
6. You see that the Microsoft Defender Antivirus scan (offline scan) is in progress.

    ![Screenshot of the Microsoft Defender Antivirus scan.](/en-us/defender/media/defender-offline-antivirus-run.png)

    You'll see the following image:

    ![Screenshot of a dialogue when the run is ongoing.](/en-us/defender/media/defender-offline-scan-run-2.png)

### Use PowerShell cmdlets to run an offline scan

Run the following cmdlet to initiate a Microsoft Defender Offline scan, which reboots the device into an isolated environment to detect persistent malware:

```PowerShell
Start-MpWDOScan
```

See [Use PowerShell cmdlets to configure and run Microsoft Defender Antivirus](use-powershell-cmdlets-microsoft-defender-antivirus) and [Defender Antivirus cmdlets](/en-us/powershell/module/defender/) for more information on how to use PowerShell with Microsoft Defender Antivirus.

### Use Windows Management Instrumentation (WMI) to run an offline scan

Use the [**MSFT\_MpWDOScan**](/en-us/previous-versions/windows/desktop/legacy/dn455323%28v=vs.85%29) class to run an offline scan.

Important

Running this command immediately restarts the endpoint to begin the offline scan. Save all files and close applications before continuing.

The following WMI command triggers a Microsoft Defender Offline scan, which restarts the endpoint, performs the offline scan, and then boots back into Windows.

```console
wmic /namespace:\\root\Microsoft\Windows\Defender path MSFT_MpWDOScan call Start
```

For more information about Windows Defender WMI APIs, see [Windows Defender WMIv2 APIs](/en-us/previous-versions/windows/desktop/defender/windows-defender-wmiv2-apis-portal).

#### In Windows 7 Service Pack 1 and Windows 8.1:

To run Microsoft Defender Offline on Windows 7 SP1 or Windows 8.1, create bootable media and then use it to scan the endpoint:

1. Download Windows Defender Offline and install it to a CD, DVD, or USB flash drive using the following links:

    - [Download the 64-bit version (msstool64.exe)](https://go.microsoft.com/fwlink/?LinkID=234124)
    - [Download the 32-bit version (msstool32.exe)](https://go.microsoft.com/fwlink/?LinkID=234123)

    If you're not sure which version to download, see [Is my PC running the 32-bit or 64-bit version of Windows?](https://support.microsoft.com/Windows/Experience/Compatibility/32-bit-and-64-bit-windows-frequently-asked-questions).
2. To get started, find a blank CD, DVD, or USB flash drive with at least 250 MB of free space, and then run the tool. You are guided through the steps to create the removable media.

    Tip

    We recommend you to do the following when downloading Windows Defender Offline:

    - Download Windows Defender Offline and create the CD, DVD, or USB flash drive on a PC that isn't infected with malware as the malware can interfere with the media creation.
    - If you use a USB drive, the drive will be reformatted and any data on it will be erased. Ensure to back up any important data from the drive first.

    ![Screenshot of a dialogue for scan in PC.](/en-us/defender/media/defender-offline-scan-pc-for-virus.png)
3. Scan your PC for viruses and other malware.

    1. Once you've created the USB drive, CD, or DVD, remove it from your current computer and take it to the computer you want to scan. Insert the USB drive or disc into the other computer and restart the computer.
    2. Boot from the USB drive, CD, or DVD to run the scan. Depending on the computer's settings, it may automatically boot from the media after you restart it, or you may have to press a key to enter a "boot devices" menu or modify the boot order in the computer's UEFI firmware or BIOS.
    3. After you boot the device, you see a Microsoft Defender tool that will automatically scan your computer and remove malware.
    4. After the scan is complete and you're done with the tool, you can reboot your computer and remove the Microsoft Defender Offline media to boot back into Windows.
4. Remove any malware that's found from your PC.

    If you experience a Stop error on a blue screen when you run the offline scan, restart your device and try running a Microsoft Defender Offline scan again. If the blue-screen error happens again, contact [Microsoft Support](https://support.microsoft.com/).

### Where can I find the scan results?

To see the Microsoft Defender Offline scan results in Windows 10 and Windows 11:

1. Select **Start**, and then select **Settings** &gt; **Update & Security** &gt; **Windows Security** &gt; **Virus & threat protection**.
2. On the **Virus & threat protection** screen, under **Current threats**, select **Scan options**, and then select **Protection history**. For more information, see [Review threat detection history in the Windows Security app](microsoft-defender-security-center-antivirus).

### How can I find out if Microsoft Defender Offline scan was kicked off?

In the **Event Viewer**, go to **Applications and Services Logs &gt; Microsoft &gt; Windows &gt; Windows Defender &gt; Operational**. You'll see:

- Log Name: Microsoft-Windows-Windows Defender/Operational
- Source: Microsoft-Windows-Windows Defender
- Event ID: 2030
- Level: Information
- Description: Microsoft Defender Antivirus downloaded and configured Microsoft Defender Antivirus (offline scan) to run on the next reboot.

On older versions than Windows 10, 2004, you'll see:

Windows Defender Antivirus downloaded and configured Windows Defender Offline to run on the next reboot.

- Log Name: `Microsoft-Windows-Windows Defender/Operational`
- Source: `Microsoft-Windows-Windows Defender`
- Event ID: `5007`
- Level: `Information`
- Description: `Microsoft Defender Antivirus Configuration has changed. If this is an unexpected event, you should review the settings as this may be the result of malware.`
- Old value: `N/A\Scan\OfflineScanRun =`
- New value: `HKLM\SOFTWARE\Microsoft\Windows Defender\Scan\OfflineScanRun = 0x0`