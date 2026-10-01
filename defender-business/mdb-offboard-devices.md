---
layout: Conceptual
title: Offboard a Device from Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-business/mdb-offboard-devices
breadcrumb_path: /defender-business/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn about how to remove or offboard devices from Microsoft Defender for Business, as devices are replace or your business needs change.
author: chrisda
ms.author: chrisda
ms.topic: overview
ms.service: defender-business
ms.localizationpriority: medium
ms.date: 2026-04-25T00:00:00.0000000Z
ms.reviewer: nehabha
ms.collection:
- SMB
- m365-security
- m365-initiative-defender-business
- tier1
locale: en-us
document_id: 3c168950-b161-39db-3cf7-5e90b489a7ef
document_version_independent_id: 3c168950-b161-39db-3cf7-5e90b489a7ef
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-business/mdb-offboard-devices.md
site_name: Docs
depot_name: Learn.defender-business
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdb-offboard-devices
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-business/mdb-offboard-devices.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b11ae577-8d18-47ab-998c-ea182a941e71
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/e0ffb20c-01c6-407b-a9bd-29111652a1dc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/87b1d24d-826d-4337-90a0-b6c35e4561f2
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/3904bce4-d817-48cf-85fd-b6146fca83b7
platformId: e4057644-0565-0a31-a935-ff4df0839bf0
---

# Offboard a Device from Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn

As you replace or retire devices, or as your business needs change, you can offboard devices from Defender for Business. When you offboard a device, it stops sending data to Defender for Business. Its status changes to `Inactive` within seven days. You don't need to offboard devices that are already listed as `Inactive`.

Data from a device, such as alerts, vulnerabilities, and detected threats, remains visible in the Microsoft Defender portal until the [configured retention period](/en-us/defender-endpoint/data-storage-privacy#how-long-will-microsoft-store-my-data-what-is-microsofts-data-retention-policy) expires, usually 180 days.

Devices that weren't active within the last 30 days don't affect your organization's [exposure score](mdb-view-tvm-dashboard).

Important

The procedures in this article describe how to remove a device from monitoring by Defender for Business. If you're using Microsoft Intune to manage devices, and you prefer to remove the device from Intune, see [Remove devices by using wipe, retire, or manually unenrolling the device](/en-us/intune/intune-service/remote-actions/devices-wipe).

## What to do

1. Select one of the following tabs:

    - **Windows 10 or 11**
    - **Mac**
    - **Servers**: Windows Server or Linux Server
    - **Mobile**: for iOS/iPadOS or Android devices
2. Follow the guidance on the selected tab.
3. Proceed to your next steps.

# [Windows 10 or 11](#tab/Windows1011)
## Windows 10 or 11

1. Go to the [Microsoft Defender portal](https://security.microsoft.com) and sign in.
2. In the navigation pane, choose **Settings**, and then choose **Endpoints**.
3. Under **Device management**, choose **Offboarding**.
4. Select an operating system, such as **Windows 10 and 11**, and then, under **Offboard a device**, in the **Deployment method** section, choose **Local script**.
5. In the confirmation screen, review the information, and then choose **Download** to proceed.
6. Select **Download offboarding package**. We recommend saving the offboarding package to a removable drive.
7. Run the script on each device that you want to offboard.

# [Mac](#tab/mac)
## Mac

1. Go to the [Microsoft Defender portal](https://security.microsoft.com) and sign in.
2. In the navigation pane, choose **Settings**, and then choose **Endpoints**.
3. Under **Device management**, choose **Offboarding**.
4. In the **Select operating system to start the offboarding process** list, select **macOS**.
5. In the **Deployment method** section, select either **Local Script** or **Mobile Device Management / Microsoft Intune**, depending on your preferred method.
6. Select **Download package**. We recommend saving the offboarding package to a removable drive.
7. Run the script on each Mac computer that you want to offboard.

# [Servers](#tab/Servers)
## Servers

Choose the operating system for your server:

- Windows Server
- Linux Server

### Windows Server

1. Go to the [Microsoft Defender portal](https://security.microsoft.com) and sign in.
2. In the navigation pane, choose **Settings** &gt; **Endpoints**, and then under **Device management**, choose **Offboarding**.
3. Select an operating system, such as **Windows Server 1803, 2019, and 2022**, and then in the **Deployment method** section, choose **Local script**.
4. Select **Download package**. We recommend that you save the offboarding package to a removable drive. The zipped folder is named `WindowsDefenderATPOffboardingPackage_valid_until_YYYY-MM-DD.zip`, where `YYYY-MM-DD` is the expiry date of the package.
5. On your Windows Server device, extract the contents of the zipped folder to a location such as the Desktop folder.
6. Open a Command Prompt window as an administrator.
7. Type the location of the script file. For example, if you copied the file to the Desktop folder, type `%userprofile%\Desktop\WindowsDefenderATPOffboardingScript_valid_until_2022-11-11.cmd`, where `YYYY-MM-DD` is the expiry date of the package. Then press **Enter** or select **OK**.

### Linux Server

1. Go to the [Microsoft Defender portal](https://security.microsoft.com) and sign in.
2. In the navigation pane, choose **Settings** &gt; **Endpoints**, and then under **Device management**, choose **Offboarding**.
3. Select **Linux Server** for the operating system, and then in the **Deployment method** section, choose **Local script**.
4. Select **Download package**. We recommend that you save the offboarding package to a removable drive. The zipped folder is named `WindowsDefenderATPOffboardingPackage_valid_until_YYYY-MM-DD.zip`, where `YYYY-MM-DD` is the expiry date of the package.
5. On your Linux Server device, extract the contents of the zipped folder to a location such as the Desktop folder.
6. Open a terminal, and navigate to the directory where the `MicrosoftDefenderATPOffboardingLinuxServer_valid_until_YYYY-MM-DD` file, where `YYYY-MM-DD` is the expiry date of the file, is located.
7. Type `python MicrosoftDefenderATPOffboardingLinuxServer_valid_until_YYYY-MM-DD.py` in the terminal.

Note

This procedure offboards the server, meaning that the server stops sending security data to Defender for Business. It doesn't remove the Defender for Business software from the device. For information about how to completely remove the software from the device, see [Offboard or uninstall Microsoft Defender for Endpoint on Linux](/en-us/defender-endpoint/linux-off-board-endpoints).

# [Mobile devices](#tab/mobiles)
## Mobile devices

You can use Microsoft Intune to manage mobile devices, such as iOS, iPadOS, and Android devices.

See [Microsoft Intune device management](/en-us/intune/intune-service/remote-actions/device-management).

---