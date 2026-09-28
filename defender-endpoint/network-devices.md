---
layout: Conceptual
title: Set up authenticated network scans in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/network-devices
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Set up authenticated network scans to discover network devices in Microsoft Defender for Endpoint.
ms.service: defender-endpoint
ms.subservice: onboard
ms.author: lwainstein
author: limwainstein
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.custom: admindeeplinkDEFENDER, msecd-doc-authoring-1016
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 81bb402d-9828-f322-e8c6-ffa2b16d572b
document_version_independent_id: 81bb402d-9828-f322-e8c6-ffa2b16d572b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/network-devices.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: network-devices
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/network-devices.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
platformId: b96b1302-cb51-d27a-06ea-8bb3aaad95c5
---

# Set up authenticated network scans in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

## Overview

Authenticated network scans provide an agentless way to discover and assess network infrastructure devices, such as switches, routers, WLAN controllers, firewalls, and VPN gateways. This article walks you through the prerequisites, scanner installation and registration, and configuration steps needed to set up authenticated network scans and view discovered devices in the device inventory.

For more information, see [Authenticated network scans](device-discovery#authenticated-network-scans).

Note

The Windows authenticated scan is deprecated from December 18,2025. For more information, see [Windows authenticated scan deprecation FAQs](/en-us/defender-vulnerability-management/defender-vulnerability-management-faq#windows-authenticated-scan-deprecation-faqs).

## Prerequisites

To configure scan jobs, you need the **Manage security settings in Defender** permission. For more information, see [Create and manage roles for role-based access control](user-roles).

### Supported devices

Any network device that responds to SNMPv2 or SNMPv3 queries can be discovered by authenticated network scans. We recommend that you configure all your network devices for scanning, regardless of vendor or operating system.

### Supported Windows versions for the scanner

The scanner is supported on Windows 10, version 1903 and Windows Server, version 1903 and later. For more information, see [Windows 10, version 1903 and Windows Server, version 1903](https://support.microsoft.com/servicing/os/windows-10/2020/11/windows-10-update-history-4)

Note

You can install up to 40 scanners per tenant.

## Select scanner device

To select a device that performs the authenticated network scans:

- Decide on a Defender for Endpoint onboarded device (client or server) that has a network connection to the management port for the network devices you plan on scanning.
- Allow SNMP traffic between the Defender for Endpoint scanning device and the targeted network devices (for example, by the firewall).
- Decide which network devices are assessed for vulnerabilities (for example, a Cisco switch or a Palo Alto Networks firewall).
- Make sure SNMP read-only is enabled on all configured network devices to allow the Defender for Endpoint scanning device to query the configured network devices. `SNMP write` isn't needed for the proper functionality of this feature.
- Obtain the IP addresses of the network devices to be scanned (or the subnets where these devices are deployed).
- Obtain the SNMP credentials of the network devices (for example, Community String, noAuthNoPriv, authNoPriv, authPriv). You need to provide the credentials when configuring a new scan job.
- Proxy client configuration: No extra configuration is required other than the Defender for Endpoint device proxy requirements.
- To allow the scanner to be authenticated and work properly, add the following domains/URLs:

    - `*.security.microsoft.com`
    - `*.mdiot.microsoft.com`
    - `login.microsoftonline.com`
    - `*.blob.core.windows.net/networkscannerstable/*`

    Note

    Not all URLs are specified in the Defender for Endpoint documented list of allowed data collection.

## Install the scanner

To install the scanner on the designated device:

1. In the Microsoft Defender Portal, select **Settings** &gt; **Device discovery** &gt; **Authenticated scans**.
2. Download the scanner and install it on the designated Defender for Endpoint scanning device.

    [![Screenshot of the add new authenticated scan screen.](/en-us/defender/media/defender-endpoint/network-authenticated-scan-new.png)](/en-us/defender/media/defender-endpoint/network-authenticated-scan-new.png#lightbox)

## Register the scanner

You can complete the registration on the designated scanning device or any other device (for example, your personal client device).

The account the user signs in with and the device used to complete the sign in process, must be in the same tenant where the device is onboarded to Microsoft Defender for Endpoint.

To complete the scanner registration process:

1. Copy and follow the URL that appears on the command line and use the provided installation code to complete the registration process. You might need to change command prompt settings to copy the URL.
2. Type the code and sign in using a Microsoft account that has the **Manage security settings in Defender** permission.

When finished, you should see a message confirming you've signed in.

Note

A scheduled task that searches for updates runs regularly. When the task runs, it compares the version of the scanner on the client device to the version of the agent on the update location. The update location is where Windows looks for updates, such as on a network share or from the internet.

If there's a difference between the two versions, the update process determines which files are different and need to be updated on the local computer. Once the required updates are determined, the scheduled task starts downloading the updates.

## Configure a new authenticated network scan

To configure a new authenticated network scan, complete the following steps:

1. In the Microsoft Defender Portal, select **Settings** &gt; **Device discovery** &gt; **Authenticated scans**.
2. Select **Add new scan** and choose **Network device authenticated scan** and select **Next**.

    [![Screenshot of the add new network device authenticated scan screen.](/en-us/defender/media/defender-endpoint/network-authenticated-scan.png)](/en-us/defender/media/defender-endpoint/network-authenticated-scan.png#lightbox)
3. Select whether to **Activate scan**.
4. Type a **Scan name**.
5. Select the **Scanning device:** The onboarded device you use to scan the network devices.
6. Type the **Target (range):** The IP address ranges or hostnames you want to scan. You can either enter the addresses or import a CSV file. Importing a file overrides any manually added addresses.
7. Select the **Scan interval:** By default, the scan runs every four hours. You can change the scan interval or have it only run once, by selecting **Don't repeat**.
8. Select your **Authentication method**.

    You can select to **Use azure KeyVault for providing credentials:** If you manage your credentials in Azure KeyVault, you can type the Azure KeyVault URL and Azure KeyVault secret name to be accessed by the scanning device to provide credentials. The secret value depends on the authentication method you select, as shown in the following table:

    | Authentication Method | Azure KeyVault secret value |
    | --- | --- |
    | `AuthPriv` | Username;AuthPassword;PrivPassword |
    | `AuthNoPriv` | Username;AuthPassword |
    | `CommunityString` | CommunityString |
9. Select **Next** to run or skip the test scan.
10. Select **Next** to review the settings and then select **Submit** to create your new network device authenticated scan.

Note

To prevent device duplication in the network device inventory, make sure each IP address is configured only once across multiple scanning devices.

### Scan and add network devices

During the setup process, you can perform a one time test scan to verify that:

- There's connectivity between the Defender for Endpoint scanning device and the configured target network devices.
- The configured SNMP credentials are correct.

Each scanning device can support up to 1,500 successful IP addresses scan. For example, if you scan 10 different subnets where only 100 IP addresses return successful results, you can scan 1,400 IP more addresses from other subnets on the same scanning device.

If there are multiple IP address ranges/subnets to scan, the test scan results take several minutes to show up. A test scan is available for up to 1,024 addresses.

When the test scan results are displayed, you can choose which devices to include in the periodic scan. If you skip viewing the scan results, all configured IP addresses are added to the network device authenticated scan (regardless of the device's response). The scan results can also be exported.

## View network devices in the device inventory

Newly discovered devices are displayed under the device inventory in the new **Network devices** tab. It might take up to two hours after adding a scanning job until the devices are updated.

[![Screenshot of the network device tab in the device inventory.](/en-us/defender/media/defender-endpoint/network-devices-inventory.png)](/en-us/defender/media/defender-endpoint/network-devices-inventory.png#lightbox)