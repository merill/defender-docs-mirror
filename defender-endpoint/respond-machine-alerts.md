---
layout: Conceptual
title: Take response actions on a device in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/respond-machine-alerts
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Respond to attacks on a device in Microsoft Defender for Endpoint by isolating it, collecting an investigation package, running a scan, or restricting apps.
ms.service: defender-endpoint
ms.author: lwainstein
author: limwainstein
ms.localizationpriority: medium
ms.date: 2026-07-23T00:00:00.0000000Z
ms.collection:
- m365-security
- tier2
- mde-edr
ms.topic: how-to
ms.subservice: edr
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: b1f34a64-3009-5ec1-6d42-6067776b4136
document_version_independent_id: b1f34a64-3009-5ec1-6d42-6067776b4136
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/respond-machine-alerts.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: respond-machine-alerts
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/respond-machine-alerts.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/e0ffb20c-01c6-407b-a9bd-29111652a1dc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/3904bce4-d817-48cf-85fd-b6146fca83b7
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 1bbcd1d3-21f7-241e-b156-58e4a4516e02
---

# Take response actions on a device in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

Quickly respond to detected attacks by isolating devices or collecting an investigation package. After taking action on devices, you can check activity details on the Action center.

Response actions run along the top of a specific device page and include:

- Manage tags
- Initiate automated investigation
- Initiate live response session
- Collect investigation package
- Run antivirus scan
- Restrict app execution
- Isolate device
- Contain device
- Consult a threat expert
- Action center

[![Screenshot that shows response actions across the top of a device page in the Microsoft Defender portal.](media/response-actions.png)](media/response-actions.png#lightbox)

Note

[Defender for Endpoint Plan 1](defender-endpoint-plan-1) includes only the following manual response actions:

- Run antivirus scan
- Isolate device
- Stop and quarantine a file
- Add an indicator to block or allow a file

[Microsoft Defender for Business](/en-us/defender-business/mdb-overview) doesn't include the "Stop and quarantine a file" action at this time.

Your subscription must include Defender for Endpoint Plan 2 to have all of the response actions described in this article.

You can find device pages from any of the following views:

- **Alerts queue**: Select the device name beside the device icon from the alerts queue.
- **Devices list**: Select the heading of the device name from the devices list.
- **Search box**: Select **Device** from the drop-down menu and enter the device name.

Important

For information on availability and support for each response action, see the supported minimum operating system requirements listed in [Minimum requirements for Microsoft Defender for Endpoint](minimum-requirements).

Some high-impact response actions can be restricted on high-value assets to prevent potential business disruption. For more information, see [Restrict response actions on high-value assets](restrict-response-actions-high-value-assets).

## Manage tags

Add or manage tags to create a logical group affiliation. Device tags support proper mapping of the network, enabling you to attach different tags to capture context and to enable dynamic list creation as part of an incident.

For more information on device tagging, see [Create and manage device tags](machine-tags).

## Initiate automated investigation

You can start a new automated investigation on the device if needed. While an investigation runs, any other alert from the device is added to that investigation until it completes. If the same threat appears on other devices, those devices are also added.

For more information on automated investigations, see [Overview of Automated investigations](automated-investigations).

## Initiate live response session

Live response gives you instant access to a device through a remote shell connection. Live response lets you do deep investigative work and take quick action to contain threats in real time.

Live response helps you collect forensic data, run scripts, send suspicious entities for analysis, fix threats, and hunt for emerging threats.

For more information on live response, see [Investigate entities on devices using live response](live-response).

Note

Live response can be restricted on devices onboarded as [high-value assets](restrict-response-actions-high-value-assets), based on the selective response actions defined when the device was onboarded. If live response isn't available for a device, review the device's selective response actions configuration.

## Collect investigation package from devices

As part of the investigation or response process, you can collect an investigation package from a device. By collecting the investigation package, you can identify the current state of the device and further understand the tools and techniques used by the attacker.

To download the package (zipped folder) and investigate the events that occurred on a device, follow these steps:

1. Select **Collect investigation package** from the row of response actions at the top of the device page.
2. Specify in the text box why you want to perform this action. Select **Confirm**.
3. The zip file downloads.

Or, use this alternate procedure:

1. Select **Collect Investigation Package** from the response actions section of the device page.

    [![Screenshot of the device page option to collect an investigation package.](media/collect-investigation-package.png)](media/collect-investigation-package.png#lightbox)
2. Add comments and then select **Confirm**.

    [![Screenshot of the confirmation dialog for adding a comment to the action.](media/comments-confirm.png)](media/comments-confirm.png#lightbox)
3. Select **Action center** from the response actions section of the device page.

    [![Screenshot of the Action center selected in the response actions section of the device page.](media/action-center-selected.png)](media/action-center-selected.png#lightbox)
4. Select **Package collection package available** to download the collection package.

    [![Screenshot of the option to download the collected investigation package from the Action center.](media/download-package.png)](media/download-package.png#lightbox)

    Note

    Collection of the investigation package might fail if the target device has a low battery level or is on a metered connection.

### Investigation package contents for Windows devices

For Windows devices, the package contains the folders described in the following table:

| Folder | Description |
| --- | --- |
| Autoruns | Contains a set of files that each represent the content of the registry of a known auto start entry point (ASEP) to help identify attacker's persistency on the device. If the registry key isn't found, the file contains the following message: "ERROR: The system was unable to find the specified registry key or value." |
| Installed programs | This .CSV file contains the list of installed programs that can help identify what is currently installed on the device. For more information, see [Win32_Product class](https://go.microsoft.com/fwlink/?linkid=841509). |
| Network connections | This folder contains a set of data points related to the connectivity information that can help in identifying connectivity to suspicious URLs, attacker's command and control (C&C) infrastructure, any lateral movement, or remote connections. - `ActiveNetConnections.txt`: Displays protocol statistics and current TCP/IP network connections. Enables you to look for suspicious connectivity made by a process.- `Arp.txt`: Displays the current address resolution protocol (ARP) cache tables for all interfaces. ARP cache can reveal other hosts on a network that were compromised or suspicious systems on the network that might be used to run an internal attack.- `DnsCache.txt`: Displays the contents of the DNS client resolver cache, which includes both entries preloaded from the local Hosts file and any recently obtained resource records for name queries resolved by the computer. Reviewing the DNS cache can help identify suspicious connections.- `IpConfig.txt`: Displays the full TCP/IP configuration for all adapters. Adapters can represent physical interfaces, such as installed network adapters, or logical interfaces, such as dial-up connections.- `FirewallExecutionLog.txt` and `pfirewall.log`The `pfirewall.log` file must exist in `%windir%\system32\logfiles\firewall\pfirewall.log`. It's included in the investigation package. For more information on creating the firewall log file, see [Configure the Windows Firewall with Advanced Security Log](/en-us/windows/security/operating-system-security/network-security/windows-firewall/configure-logging). |
| Prefetch files | Windows Prefetch files are designed to speed up the application startup process. It can be used to track all the files recently used in the system and find traces for applications that might be deleted but can still be found in the prefetch file list. - `Prefetch folder`: Contains a copy of the prefetch files from `%SystemRoot%\Prefetch`. We recommend downloading a prefetch file viewer to view the prefetch files.- `PrefetchFilesList.txt`: Contains the list of all the copied files that can be used to track if there were any copy failures to the prefetch folder. |
| Processes | Contains a .CSV file listing the processes currently running on the device. This process list can be useful when identifying a suspicious process and its state. |
| Scheduled tasks | Contains a .CSV file listing the scheduled tasks, which can be used to identify routines performed automatically on a chosen device to look for suspicious code that was set to run automatically. |
| Security event log | Contains the security event log, which contains records of sign-in or sign out activity, or other security-related events specified by the system's audit policy. Open the event log file using Event viewer. |
| Services | Contains a .CSV file that lists services and their states. |
| Windows Server Message Block (SMB) sessions | Lists shared access to files, printers, and serial ports and miscellaneous communications between nodes on a network. Reviewing SMB session data can help identify data exfiltration or lateral movement.Contains files for `SMBInboundSessions` and `SMBOutboundSession`. If there are no sessions (inbound or outbound), you get a text file that tells you that there are no SMB sessions found. |
| System Information | Contains a `SystemInformation.txt` file that lists system information such as OS version and network cards. |
| Temp Directories | Contains a set of text files that lists the files located in `%Temp%` for every user in the system. This can help to track suspicious files that an attacker might have dropped on the system. If the file contains the following message: "The system can't find the path specified," it means that there's no temp directory for this user, and might be because the user didn't sign in to the system. |
| Users and Groups | Provides a list of files that each represent a group and its members. |
| WdSupportLogs | Provides the `MpCmdRunLog.txt` and `MPSupportFiles.cab`. This folder is only created on Windows 10, version 1709 or later with February 2020 update rollup or more recent versions installed: - Win10 1709 (RS3) Build 16299.1717: [KB4537816](https://support.microsoft.com/servicing/os/windows-10/2020/02/february-25-2020-kb4537816-os-build-16299-1717)- Win10 1803 (RS4) Build 17134.1345: [KB4537795](https://support.microsoft.com/topic/february-25-2020-kb4537795-os-build-17134-1345-36b35e62-d897-2dc3-289c-44a1327c2d8e)- Win10 1809 (RS5) Build 17763.1075: [KB4537818](https://support.microsoft.com/servicing/os/windows-10/2020/02/february-25-2020-kb4537818-os-build-17763-1075)- Win10 1903/1909 (19h1/19h2) Builds 18362.693 and 18363.693: [KB4535996](https://support.microsoft.com/topic/february-27-2020-kb4535996-os-builds-18362-693-and-18363-693-7974b3c8-f463-2980-1ec6-72363d291bd2) |
| CollectionSummaryReport.xls | The CollectionSummaryReport.xls file is a summary of the investigation package collection. It contains the list of data points, the command used to extract the data, the execution status, and the error code if there's failure. You can use this report to track if the package includes all the expected data and identify if there were any errors. |

### Investigation package contents for Mac and Linux devices

The following table lists the contents of the collection packages for Mac and Linux devices:

| Object | macOS | Linux |
| --- | --- | --- |
| Applications | A list of all installed applications | Not applicable |
| Disk volume | - Amount of free space- List of all mounted disk volumes- List of all partitions | - Amount of free space- List of all mounted disk volumes- List of all partitions |
| File | A list of all open files with the corresponding processes using these files | A list of all open files with the corresponding processes using these files |
| History | Shell history | Not applicable |
| Kernel modules | All loaded modules | Not applicable |
| Network connections | - Active connections- Active listening connections- ARP table- Firewall rules- Interface configuration- Proxy settings- VPN settings | - Active connections- Active listening connections- ARP table- Firewall rules- IP list- Proxy settings |
| Processes | A list of all running processes | A list of all running processes |
| Services and scheduled tasks | - Certificates- Configuration profiles- Hardware information | - CPU details- Hardware information- Operating system information |
| System security information | - Extensible Firmware Interface (EFI) integrity information- Firewall status- Malware Removal Tool (MRT) information- System Integrity Protection (SIP) status | Not applicable |
| Users and groups | - Sign-in history- Sudoers | - Sign-in history- Sudoers |

## Run Microsoft Defender Antivirus scan on devices

As part of the investigation or response process, you can remotely initiate an antivirus scan to help identify and remediate malware that might be present on a compromised device.

Important

- The remote antivirus scan action is supported for macOS and Linux for client version 101.98.84 and above. You can also use live response to run the action. For more information on live response, see [Investigate entities on devices using live response](live-response)
- A Microsoft Defender Antivirus scan can run alongside other antivirus solutions, whether Microsoft Defender Antivirus is the active antivirus solution or not. Microsoft Defender Antivirus can be in Passive mode. For more information, see [Microsoft Defender Antivirus compatibility](microsoft-defender-antivirus-compatibility).

Once you have selected **Run antivirus scan**, select the scan type that you'd like to run (quick or full) and add a comment before confirming the scan.

[![Screenshot of the notification to select a quick or full scan and add a comment.](media/run-antivirus.png)](media/run-antivirus.png#lightbox)

The Action center shows the antivirus scan details. The device timeline includes a new event that shows a scan action was submitted on the device. Microsoft Defender Antivirus alerts show any threats found during the scan.

Note

When triggering a scan using Defender for Endpoint response action, Microsoft Defender Antivirus `ScanAvgCPULoadFactor` value applies and limits the CPU impact of the scan. If `ScanAvgCPULoadFactor` isn't configured, the default value is a limit of 50% maximum CPU load during a scan. For more information, see [Configure advanced scan types for Microsoft Defender Antivirus](configure-advanced-scan-types-microsoft-defender-antivirus).

## Restrict app execution

In addition to containing an attack by stopping malicious processes, you can also lock down a device and prevent subsequent attempts of potentially malicious programs from running.

Important

- Restrict app execution is available for devices on Windows 10, version 1709 or later, Windows 11, and Windows Server 2019 or later.
- Restrict app execution is available if your organization uses Microsoft Defender Antivirus.
- Restrict app execution needs to meet the Windows Defender Application Control code integrity policy formats and signing requirements. For more information, see [Code integrity policy formats and signing](/en-us/windows/security/application-security/application-control/app-control-for-business/deployment/use-code-signing-for-better-control-and-protection).

To restrict an app from running, a code integrity policy is applied. This policy only allows files to run if they're signed by a Microsoft-issued certificate. Allowing only Microsoft-signed files helps stop attackers from controlling compromised devices.

Note

You are able to reverse the restriction of applications from running at any time. The button on the device page changes to say **Remove app restrictions**, and then you select **Remove app restrictions**, type a comment, and select **Confirm**.

Once you have selected **Restrict app execution** on the device page, type a comment and select **Confirm**. The Action center shows the app restriction details, and the device timeline includes a new event.

[![Screenshot of the app restriction confirmation notification.](media/restrict-app-execution.png)](media/restrict-app-execution.png#lightbox)

### Device user notification for app restriction

When an app is restricted, the following notification is displayed to inform the user that an app is being restricted from running:

[![Screenshot of the app restriction message shown to the device user.](media/atp-app-restriction.png)](media/atp-app-restriction.png#lightbox)

Note

The notification isn't available on Windows Server 2016 and Windows Server 2012 R2.

## Isolate devices from the network

Depending on the severity of the attack and the sensitivity of the device, you might want to isolate the device from the network. Device isolation can help prevent the attacker from controlling the compromised device and performing further activities such as data exfiltration and lateral movement.

**Important points to keep in mind**:

- In environments that use web proxies (including Proxy Auto Configuration (PAC), WPAD, or static/direct proxy configurations), devices might not be able to recover from network isolation. Use selective isolation in such cases. When using selective isolation, exclusion settings aren't required to avoid this scenario.
- Isolating devices from the network is supported for macOS for client version 101.98.84 and above. You can also use live response to run the action. For more information on live response, see [Investigate entities on devices using live response](live-response)
- Full isolation is available for devices running Windows 11, Windows 10, version 1703 or later, Windows Server 2012 R2 and later, and Azure Stack HCI OS, version 23H2 and later.
- Isolating devices from the network is supported when Defender is running in passive mode on all supported Windows operating systems, macOS and Linux supported versions.
- You can use the device isolation capability on all supported Microsoft Defender for Endpoint on Linux listed in [System requirements](mde-linux-prerequisites). Ensure that the following prerequisites are enabled:

    - `iptables`
    - `ip6tables`
    - Linux kernel with `CONFIG_NETFILTER`, `CONFIG_IP_NF_IPTABLES`, and `CONFIG_IP_NF_MATCH_OWNER` for kernel version lower than 5.x and `CONFIG_NETFILTER_XT_MATCH_OWNER` from 5.x kernel.
- Selective isolation is available for devices running on Windows 11, Windows 10 version 1703 or later, Windows Server 2012 R2 and later, Azure Stack HCI OS, version 23H2 and later, and macOS. For more information about selective isolation, see [Isolation exclusions](network-isolation-exclusions).
- When isolating a device, only certain processes and destinations are allowed. Therefore, devices that are behind a full VPN tunnel won't be able to reach the Microsoft Defender for Endpoint cloud service after the device is isolated. We recommend using a split-tunneling VPN for Microsoft Defender for Endpoint and Microsoft Defender Antivirus cloud-based protection-related traffic.
- The feature supports VPN connection.
- You must have at least the `Active remediation actions` role assigned. For more information, see [Create and manage roles](user-roles).
- You must have access to the device based on the device group settings. For more information, see [Create and manage device groups](machine-groups).
- Exclusions, such as e-mail, messaging application, and other applications for both macOS and Linux isolation aren't supported.
- An isolated device is removed from isolation when an administrator modifies or adds a new `iptable` rule to the isolated device.
- Isolating a server running on Microsoft Hyper-V blocks network traffic to all child virtual machines of the server.
- Device isolation is automatically lifted after seven days.

The device isolation feature disconnects the compromised device from the network while retaining connectivity to the Defender for Endpoint service, which continues to monitor the device. On Windows 10, version 1709 or later, you can use selective isolation for more control over the network isolation level. You can also choose to enable Outlook and Microsoft Teams connectivity.

Note

You can reconnect the device back to the network at any time. The button on the device page changes to say **Release from isolation**. At this stage, you can take the same steps as isolating the device.

If a device is inactive or offline when an isolation action is submitted, Microsoft Defender for Endpoint retries enforcing the isolation for up to three days. If the device doesn't reconnect in that time, the isolation won't be retried, and administrators should reissue the isolation action after the device becomes active.

Once you have selected **Isolate device** on the device page, type a comment and select **Confirm**. The Action center shows the scan information and the device timeline includes a new event.

[![An isolated device details page](media/isolate-device.png)](media/isolate-device.png#lightbox)

Note

The notification isn't available on non-Windows platforms.

## Isolate device - automatic attack disruption (Preview)

When a device in your organization might be compromised, Microsoft Defender for Endpoint can automatically isolate it as part of [automatic attack disruption](/en-us/defender-xdr/automatic-attack-disruption). Automatic isolation helps reduce further impact on the organization and limit attacker lateral movement. It also helps prevent data exfiltration and ransomware spread. When a device is isolated automatically:

- The compromised device is disconnected from the network, reducing the risk of further impact on the organization.
- The device retains connectivity to the Microsoft Defender for Endpoint service, which continues to monitor the device.

Note

Automatic device isolation works only on end-user workstations that are onboarded and managed by Microsoft Defender for Endpoint.

To manually isolate a device, see Isolate devices from the network.

### View automatic device isolation actions

After automatic isolation is applied, you can review the action and its status in the Defender portal:

- Open the relevant incident and review the **Activities** tab.

    [![Screenshot showing how to view automatic device isolation in the Activities tab.](/en-us/defender/media/defender-endpoint/view-automatic-device-isolation-activities.png)](/en-us/defender/media/defender-endpoint/view-automatic-device-isolation-activities.png#lightbox)
- Open the affected device page and confirm the device isolation status.
- Open **Action center** to review action history and current state.

    [![Screenshot showing how to view automatic device isolation in the Action center.](/en-us/defender/media/defender-endpoint/view-automatic-device-isolation-action.png)](/en-us/defender/media/defender-endpoint/view-automatic-device-isolation-action.png#lightbox)

### Safeguards and business impact

Before deploying or responding to automatic device isolation, consider the following:

- **Scoped action**: Isolation targets specific devices involved in the incident rather than broadly throughout the environment.
- **Time-limited isolation**: Isolation is automatically undone after a defined time window. You can also release isolation earlier after completing investigation and remediation.
- **Customer control**: Security operators can review the incident context and take follow-up actions, including releasing isolation when it's safe to do so.

### Isolation exclusions and automatic attack disruption exclusions

There are two types of exclusions relevant to automatic device isolation:

- [Selective isolation exclusions](network-isolation-exclusions): Define which processes and network destinations remain accessible on an isolated device. Use these to preserve critical communications (for example, management tools or business applications) while the device is isolated. Selective isolation exclusions are available for devices running on Windows 11, Windows 10 version 1703 or later, Windows Server 2012 R2 and later, Azure Stack HCI OS, version 23H2 and later, and macOS.
- [Automatic attack disruption exclusions](/en-us/defender-xdr/automatic-attack-disruption-exclusions): Define which devices or entities are excluded from automatic disruption actions entirely. Use these to prevent business-critical devices from being isolated in the first place.

Note

When an isolation exclusion rule is defined, automatic attack disruption uses selective isolation by default and isolates the device according to the configured isolation exclusion rules.

If an automatically isolated device is business-critical, prioritize rapid validation and stakeholder coordination. Release isolation only after you confirm appropriate containment and remediation steps are in place. Consider using [automatic attack disruption exclusions](/en-us/defender-xdr/automatic-attack-disruption-exclusions) to reduce the likelihood of isolating devices that can't tolerate interruption.

### Confirm automatic device isolation

To confirm that automatic device isolation was applied, follow these steps:

1. Open the relevant incident generated by automatic attack disruption in the [Microsoft Defender portal](https://security.microsoft.com).
2. Review the **Activity** tab or **Action center** to see which automated response actions were applied.
3. Open the affected device page and confirm that the device status shows that it's isolated.
    - If the isolation action shows as failed or pending, confirm that the device is online and can report to Defender for Endpoint. You can retry from the device action panel if available.
    - If a device appears isolated but you can't collect investigation data, verify that your investigation method (for example, live response) is supported for that device and scenario. Also confirm required service endpoints are reachable in your network configuration. For more information, see [Investigate entities on devices using live response](live-response) and [Configure device connectivity and proxy settings in Microsoft Defender for Endpoint](configure-device-connectivity).

### Release a device from automatic isolation

You can release the device from containment at any time after you mitigate the risk and complete investigation:

1. Select the device from the **Device inventory** or open the device page.
2. Select **Release from isolation** from the action menu.

For more information about releasing devices, see Isolate devices from the network.

Note

If isolation is removed unexpectedly, check whether a time-limited undo window applies in your environment and review the action history for the release event.

### Exclude devices from automatic device isolation

You can exclude specific devices from automatic device isolation by using policy applications and exclusions. Create a new device tag or use an existing tag, assign the tag to the devices you want to exclude, and configure the policy application to exclude the **Isolate device** action for that tag.

For detailed instructions, see [Policy applications and exclusions (Preview)](/en-us/defender-xdr/automatic-attack-disruption-exclusions#policy-applications-and-exclusions-preview).

[![Screenshot of the Configure exclusions step with the Isolate device action excluded.](media/policy-application-isolate-device-exclusion.png)](media/policy-application-isolate-device-exclusion.png#lightbox)

When automatic attack disruption identifies an excluded device as compromised, the **Isolate device** action isn't performed. The action appears with a **Skipped** status in the Action center, and the device continues to operate normally.

[![Screenshot of a skipped Isolate device action in the Action center.](media/isolate-device-action-skipped.png)](media/isolate-device-action-skipped.png#lightbox)

Important

If you're running a breach and attack simulation (BAS) or another security validation exercise, you might want to temporarily exclude the **Isolate device** action. This exclusion allows the simulated attack to proceed without automatically isolating the affected devices.

### Forcibly release device from isolation

The device isolation feature is an invaluable tool for safeguarding devices against external threats. However, there are instances when isolated devices become unresponsive.

There's a downloadable script for cases where isolated devices become unresponsive that you can run to forcibly release them from isolation. The script is available through a link on the device page in the Microsoft Defender portal.

Note

- Admins and manage security settings in Security Center permissions can forcibly release devices from isolation.
- The script is valid for the specific device only.
- The script expires in three days.

To forcibly release device from isolation:

1. On the device page, select **Download script to force-release a device from isolation** from the action menu.
2. In the pane on the right, select **Download script**.

#### Minimum requirements for forcible device release

To forcibly release a device from isolation, the device must be running Windows. The following versions are supported:

- Windows 10 21H2 and 22H2 with KB5023773.
- Windows 11 version 21H2, all editions with KB5023774.
- Windows 11 version 22H2, all editions with KB5023778.

### Device user notification for isolation

When a device is being isolated, the following notification is displayed to inform the user that the device is being isolated from the network:

[![Screenshot of the no network connection message shown to the device user.](media/atp-notification-isolate.png)](media/atp-notification-isolate.png#lightbox)

Note

The notification isn't available on non-Windows platforms.

## Contain critical assets

When a critical asset is compromised and used to spread threats, stopping the spread can be hard. These assets must keep running to avoid productivity loss. Defender for Endpoint contains the critical asset at a granular level. It stops the attack from spreading while keeping the asset running.

Through automatic attack disruption, Defender for Endpoint flags a malicious device and identifies its role. It then applies a matching policy to contain the critical asset. This containment blocks only specific ports and communication directions.

You can identify critical assets by the **critical asset** tag on the device or IP page. Device containment supports critical asset types like domain controllers, DNS servers, and DHCP servers.

## Contain devices from the network

When you find an unmanaged device that is compromised or might be compromised, you can contain it from the network. This prevents the attack from moving laterally. When you contain a device, all Defender for Endpoint onboarded devices block incoming and outgoing communication with that device. Containment helps protect nearby devices while the security analyst finds and fixes the threat.

Note

Blocking incoming and outgoing communication with a 'contained' device is supported on onboarded Microsoft Defender for Endpoint Windows 10 and Windows Server 2019+ devices.

Once devices are contained, we recommend investigating and remediating the threat on the contained devices as soon as possible. After remediation, you should remove the devices from containment.

### How to contain a device

To contain a device from the Device inventory page, follow these steps:

1. Go to the **Device inventory** page and select the device to contain.
2. Select **Contain device** from the actions menu in the device flyout.

    [![Screenshot of the contain device popup message.](/en-us/defender/media/defender-endpoint/contain_device.png)](/en-us/defender/media/defender-endpoint/contain_device.png#lightbox)
3. On the contain device popup, type a comment, and select **Confirm**.

    [![Screenshot of the contain device menu item.](/en-us/defender/media/defender-endpoint/contain_device_popup.png)](/en-us/defender/media/defender-endpoint/contain_device_popup.png#lightbox)

Important

Containing a large number of devices might cause performance issues on Defender for Endpoint-onboarded devices. To prevent any issues, Microsoft recommends containing up to 100 devices at any given time.

### Contain a device from the device page

A device can also be contained from the device page by selecting **Contain device** from the action bar:

[![Screenshot of the contain device menu item on the device page.](/en-us/defender/media/defender-endpoint/contain_device_page.png)](/en-us/defender/media/defender-endpoint/contain_device_page.png#lightbox)

Note

It can take up to 5 minutes for the details about a newly contained device to reach Microsoft Defender for Endpoint onboarded devices.

Important

- If a contained device changes its IP address, all Microsoft Defender for Endpoint onboarded devices recognize this and start blocking communications with the new IP address. The original IP address is no longer blocked (It might take up to 5 minutes to see these changes).
- In cases where the contained device's IP is used by another device on the network, a warning while containing the device with a link to advanced hunting (with a pre-populated query) is displayed. This provides visibility to other devices using the same IP to help you make a conscious decision if you'd like to continue containing the device.
- In cases where the contained device is a network device, a warning appears with a message that containment can cause network connectivity issues (for example, containing a router that's acting as a default gateway). At this point, you're able to choose whether to contain the device or not.

After you contain a device, if the behavior isn't as expected, verify the Base Filtering Engine (BFE) service is enabled on the Defender for Endpoint onboarded devices.

### Stop containing a device

You can stop containing a device at any time.

1. Select the device from the **Device inventory** or open the device page.
2. Select **Release from containment** from the action menu. Releasing from containment restores the device's connection to the network.

## Contain IP addresses of undiscovered devices

Important

Some information in this article relates to prereleased product, which might be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

Defender for Endpoint can also contain IP addresses linked to devices that are undiscovered or not onboarded. Containing an IP address stops attackers from spreading attacks to other devices. When an IP address is contained, all onboarded devices block incoming and outgoing traffic with devices that use that IP address.

Note

Blocking incoming and outgoing communication with a 'contained' device is supported on onboarded Defender for Endpoint Windows 10, Windows 11, Windows Server 2012 R2, and Windows Server 2016 devices.

Containing an IP address associated with undiscovered devices or devices not onboarded to Defender for Endpoint is done automatically through [automatic attack disruption](/en-us/defender-xdr/automatic-attack-disruption). The Contain IP policy automatically blocks a malicious IP address when Defender for Endpoint detects the IP address to be associated with an undiscovered device or a device not onboarded.

A message indicating that the action is applied appears on the applicable incident, device, or IP page. Here’s an example.

[![Screenshot that highlights a contained IP address in the incident graph.](/en-us/defender/media/defender-endpoint/contain-ip-attack-disrupt-small.png)](/en-us/defender/media/defender-endpoint/contain-ip-attack-disrupt.png#lightbox)

After an IP address is contained, you can view the action in the History view of the Action center. You can see when the action occurred and identify the IP addresses that were contained.

[![Screenshot of the contained IP address in the Action center.](/en-us/defender/media/defender-endpoint/contain-ip-action-center-small.png)](/en-us/defender/media/defender-endpoint/contain-ip-action-center.png#lightbox)

If a contained IP address is part of an incident, an indicator is present on the [incident graph](/en-us/defender-xdr/investigate-incidents#attack-story) and on the incident's [evidence and response](/en-us/defender-xdr/investigate-incidents#evidence-and-response) tab. Here’s an example.

[![Screenshot that highlights a contained IP address in the Evidence and response tab of an incident.](/en-us/defender/media/defender-endpoint/contain-ip-evidence-small.png)](/en-us/defender/media/defender-endpoint/contain-ip-evidence.png#lightbox)

You can stop an IP address' containment at any time. To stop containment, select the **Contain IP** action in the **Action center**. In the flyout, select **Undo**. This action restores the IP address’ connection to the network.

## Contain a user from the network

When an identity in your network might be compromised, you must prevent that identity from accessing the network and different endpoints. Defender for Endpoint can contain an identity, blocking it from access, and helping prevent attacks, specifically, ransomware. When an identity is contained, all supported Defender for Endpoint onboarded devices block incoming traffic in attack-related protocols (network logons, RPC, SMB, RDP). The devices also end ongoing remote sessions and log off existing RDP connections, including all related processes. Legitimate traffic continues to flow normally. Containing an identity can significantly help to reduce the impact of an attack. When an identity is contained, security operations analysts have extra time to locate, identify, and remediate the threat to the compromised identity. Once contained by automatic attack disruption, a user is automatically removed from containment in the next five days.

### Contain user important notes

- Defender for Endpoint enforces user containment at the endpoint layer and doesn't disable the account in the identity provider. Defender for Endpoint blocks attacker use of compromised identities on protected devices and limits authentication-based access, file system access, and network communication paths. This action applies controls at a granular level, so Microsoft can target attack-related activity and preserve normal business communication where possible.
- When the contain user action is triggered by [predictive shielding](/en-us/defender-xdr/shield-predict-threats) (Preview), the contain user action applies restrictions more selectively, with a focus on users identified as high risk through prediction logic. The contain user action in predictive shielding prevents new sessions rather than terminating existing ones.
- While the predictive shielding feature as a whole is in Preview, this action is generally available, both when triggered by attack disruption and predictive shielding.
- Blocking incoming communication with a "contained" user is supported on onboarded Microsoft Defender for Endpoint Windows 10 and 11 devices (Sense version 8740 and higher), Windows Server 2019+ devices, and Windows Servers 2012R2 and 2016 with the modern agent.
- **Important**: Once a **Contain user** action is enforced on a domain controller, it starts a GPO update on the Default Domain Controller policy. A change of a GPO starts a sync across the domain controllers in your environment. This is expected behavior, and if you monitor your environment for AD GPO changes, you might be notified of such changes. Undoing the **Contain user** action reverts the GPO changes to their previous state, which will then start another AD GPO synchronization in your environment. Learn more about [merging of security policies on domain controllers](/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj966251%28v=ws.11%29#merging-of-security-policies-on-domain-controllers).

### How to contain a user

Currently, containing users is only available automatically by using automatic attack disruption. When Microsoft detects a user as being compromised a "Contain User" policy is automatically set.

### View the contain user actions

After a user is contained, you can view the action in the History view of the Action Center. In the Action Center History view, you can see when the action occurred and which users in your organization were contained:

[![Screenshot of the user contain action in the Action center.](/en-us/defender/media/defender-endpoint/user-contain-action-center.png)](/en-us/defender/media/defender-endpoint/user-contain-action-center.png#lightbox)

Furthermore, after an identity is considered "contained", that user will be blocked by Defender for Endpoint and can't perform any malicious lateral movement or remote encryption on or to any supported Defender for Endpoint onboarded device. These blocks show up as alerts to help you quickly see the devices the compromised user attempted access and potential attack techniques:

[![Screenshot of a user contain lateral movement block event.](/en-us/defender/media/defender-endpoint/user-contain-lateral-move-block.png)](/en-us/defender/media/defender-endpoint/user-contain-lateral-move-block.png#lightbox)

To view the current status of the contain user action and other actions, see [Track the action status in the Activities tab (Preview)](/en-us/defender-xdr/autoad-results#track-the-action-status-in-the-activities-tab-preview).

### Undo contain user actions

Tip

Undoing contain user actions requires membership in the **Global Administrator**^\*^ role in [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal).

^\*^ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.

You can release the blocks and containment on a user at any time:

1. Select the **Contain User** action in the **Action center**. In the side pane, select **Undo**.
2. Select the user from either the user inventory, Incident page side pane, or alert side pane and select **Undo**.

This action restores the user's connection to the network.

[![Screenshot of the user contain undo option in the Action center.](/en-us/defender/media/defender-endpoint/undo-user-contain-action.png)](/en-us/defender/media/defender-endpoint/undo-user-contain-action.png#lightbox)

### Investigation capabilities with Contain User

After a user is contained, you can investigate the potential threat by viewing the blocked actions by the compromised user. In the device timeline view, you can see information about specific events, including protocol and interface granularity, and the relevant MITRE Technique associated it.

[![Screenshot of blocked event details for a contained user.](/en-us/defender/media/defender-endpoint/event-blocked-by-contained-user.png)](/en-us/defender/media/defender-endpoint/event-blocked-by-contained-user.png#lightbox)

In addition, you can expand the investigation by using advanced hunting. Look for any action type starting with *contain* in the `DeviceEvents` table. Then, you can view all the different singular blocking events in relation to Contain User in your organization, dive deeper into the context of each block, and extract the different entities and techniques associated with those events.

[![Screenshot of advanced hunting for user contain events.](/en-us/defender/media/defender-endpoint/user-contain-advanced-hunting.png)](/en-us/defender/media/defender-endpoint/user-contain-advanced-hunting.png#lightbox)

## GPO hardening - predictive shielding (Preview)

The [predictive shielding](/en-us/defender-xdr/shield-predict-threats) (Preview) feature lets Defender for Endpoint apply the GPO hardening action. GPO hardening temporarily blocks new Group Policy Object policies on high-risk devices. This helps prevent compromise by limiting changes to key settings.

To get better results from predictive shielding, use the Microsoft Defender for Identity sensor. For more information, see [Enrich predictive shielding with Microsoft Defender for Identity](/en-us/defender-xdr/shield-predict-threats-manage#enrich-predictive-shielding-data).

After the action is applied, you can view its impact in the incident graph, track it in the Action center, and investigate with advanced hunting. For more information, see [Manage predictive shielding actions](/en-us/defender-xdr/shield-predict-threats-manage).

## Safeboot hardening - predictive shielding (Preview)

As part of the [predictive shielding](/en-us/defender-xdr/shield-predict-threats) (Preview) feature, Defender for Endpoint automatically applies the Safeboot hardening action. Safeboot hardening helps protect devices from being compromised by enforcing stricter boot settings on devices that are predicted to be at high risk of compromise.

To enrich predictive shielding actions, we recommend you use the Microsoft Defender for Identity sensor in your environment. For more information, see [Enrich predictive shielding with Microsoft Defender for Identity](/en-us/defender-xdr/shield-predict-threats-manage#enrich-predictive-shielding-data).

After the action is applied, you can view the action impact in the incident graph, track the actions in the Action center, and investigate further using advanced hunting. For more information, see [Manage predictive shielding actions](/en-us/defender-xdr/shield-predict-threats-manage).

To view the current status of the Safeboot hardening action and other actions, see [Track the action status in the Activities tab (Preview)](/en-us/defender-xdr/autoad-results#track-the-action-status-in-the-activities-tab-preview).

## Consult a threat expert

You can consult a Microsoft threat expert for more insights about a compromised or potentially compromised device. Microsoft Threat Experts work with you directly from the Defender portal for a timely and accurate response. Experts help you understand complex threats, targeted attack alerts, and threat intelligence shown on your portal dashboard.

See [Configure and manage Endpoint Attack Notifications](configure-microsoft-threat-experts) for details.

## Check activity details and status

The Action center (https://security.microsoft.com/action-center) provides information on actions that were taken on a device or file. You can view the following details:

- Investigation package collection
- Antivirus scan
- App restriction
- Device isolation

All other related details are also shown, for example, submission date/time, submitting user, and if the action succeeded or failed.

[![Screenshot of the Action center with action details.](media/action-center-details.png)](media/action-center-details.png#lightbox)

The **Activities** tab in the **Incident** page shows the details and status of actions that were taken as part of the incident response. For more information, see [Track the action status in the Activities tab (Preview)](/en-us/defender-xdr/autoad-results#track-the-action-status-in-the-activities-tab-preview).