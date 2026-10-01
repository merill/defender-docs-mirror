---
layout: Conceptual
title: Onboard Devices to Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-business/mdb-onboard-devices
breadcrumb_path: /defender-business/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: See how to get devices onboarded to Defender for Business to protect your devices from day one. There are several options to onboard your company's devices.
author: chrisda
ms.author: chrisda
ms.topic: overview
ms.service: defender-business
ms.localizationpriority: medium
ms.date: 2026-04-26T00:00:00.0000000Z
ms.reviewer: efratka, nehabha, muktaagarwal
ms.collection:
- SMB
- m365-security
- m365solution-mdb-setup
- highpri
- tier1
locale: en-us
document_id: 4e770c5a-6276-147b-e471-af4fb0bb98d5
document_version_independent_id: 4e770c5a-6276-147b-e471-af4fb0bb98d5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-business/mdb-onboard-devices.md
site_name: Docs
depot_name: Learn.defender-business
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdb-onboard-devices
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-business/mdb-onboard-devices.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://authoring-docs-microsoft.poolparty.biz/devrel/e0ffb20c-01c6-407b-a9bd-29111652a1dc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/3904bce4-d817-48cf-85fd-b6146fca83b7
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: e7ed86ed-d185-3407-4ae0-a7951d186e9a
---

# Onboard Devices to Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn

This article describes how to onboard devices to Defender for Business.

![Visual depicting step 5 - onboarding devices to Defender for Business.](media/mdb-setup-step5.png)

Onboard your business devices to protect them right away. You can choose from several options to onboard your company's devices. This article walks you through your options and describes how onboarding works.

## What to do

1. Select a tab:

    - **Windows 10 and 11**
    - **Mac**
    - **Mobile**: new capabilities are available for iOS and Android devices.
    - **Servers**: Windows Server or Linux Server.
2. View your onboarding options, and follow the guidance on the selected tab.
3. View a list of onboarded devices.
4. Run a phishing test on a device.
5. Proceed to your next steps.

# [Windows 10 and 11](#tab/Windows10and11)
## Windows 10 and 11

Note

Windows devices must run one of the following operating systems:

- Windows 10 or 11 Business
- Windows 10 or 11 Professional
- Windows 10 or 11 Enterprise

For more information, see [Microsoft Defender for Business requirements](mdb-requirements).

Choose one of the following options to onboard Windows client devices to Defender for Business:

- Local script. For onboarding devices manually in the Microsoft Defender portal.
- Group Policy. If you're already using Group Policy in your organization.
- Microsoft Intune. If you're already using Intune.

### Local script for Windows 10 and 11

When you run the onboarding script on a Windows device, it:

- Creates a trust with Microsoft Entra ID, if a trust doesn't already exist.
- Enrolls the device in Microsoft Intune, if it isn't already enrolled.
- Onboards the device to Defender for Business.

If you're not currently using Intune, we recommend using the script to onboard devices to Defender for Business customers.

Tip

We recommend that you onboard up to 10 devices at a time when you use the local script method.

1. Go to the [Microsoft Defender portal](https://security.microsoft.com), and sign in.
2. In the navigation pane, choose **Settings** &gt; **Endpoints**, and then under **Device management**, choose **Onboarding**.
3. Select **Windows 10 and 11**.
4. Under **Connectivity type**, select **Streamlined**.
5. In the **Deployment method** section, choose **Local script**, and then select **Download onboarding package**. We recommend that you save the onboarding package to a removable drive.
6. On a Windows device, extract the contents of the configuration package to a location, such as the Desktop folder. You should have a file named `WindowsDefenderATPLocalOnboardingScript.cmd`.
7. Open a command prompt as an administrator.
8. Type the location of the script file. For example, if you copied the file to the Desktop folder, type `%userprofile%\Desktop\WindowsDefenderATPLocalOnboardingScript.cmd`, and then press the **Enter** key or select **OK**.
9. After the script runs, Run a detection test.

### Group Policy for Windows 10 and 11

If you prefer to use Group Policy to onboard Windows clients, follow the guidance in [Onboard Windows devices using Group Policy](/en-us/defender-endpoint/configure-endpoints-gp). This article describes the steps for onboarding to Microsoft Defender for Endpoint. The steps for onboarding to Defender for Business are similar.

### Intune for Windows 10 and 11

You can onboard Windows clients and other devices in Intune by using the [Intune admin center](https://intune.microsoft.com). There are several methods available for enrolling devices in Intune. We recommend using one of the following methods:

- Enable Windows automatic enrollment for company-owned or company-managed devices
- Ask users to enroll their own Windows 10/11 devices in Intune

#### Enable automatic enrollment for Windows 10 and 11

When you set up automatic enrollment, users add their work account to the device. In the background, the device registers and joins Microsoft Entra ID and is enrolled in Intune.

1. Go to the [Azure portal](https://portal.azure.com/) and sign in.
2. Select **Microsoft Entra ID** &gt; **Mobility (MDM and MAM)** &gt; **Microsoft Intune**.
3. Configure the **MDM User scope** and the **MAM user scope**.

    ![Screenshot of setting MDM user scope and MAM user scope in Intune.](media/mem-mam-scope-azure-ad.png)

    - For MDM User scope, we recommend that you select **All** so that all users can automatically enroll their Windows devices.
    - In the MAM user scope section, we recommend the following default values for the URLs:

        - **MDM Terms of use URL**
        - **MDM Discovery URL**
        - **MDM Compliance URL**
4. Select **Save**.
5. After a device is enrolled in Intune, you can add it to a device group in Defender for Business. [Learn more about device groups in Defender for Business](mdb-create-edit-device-groups).

Tip

To learn more, see [Enable Windows automatic enrollment](/en-us/intune/intune-service/enrollment/windows-enroll).

#### Ask users to enroll their Windows 10 and 11 devices

1. Watch the following video to see how enrollment works:
2. Share this article with users in your organization: [Enroll Windows 10/11 devices in Intune](/en-us/intune/intune-service/user-help/enroll-windows-10-device).
3. After a device is enrolled in Intune, you can add it to a device group in Defender for Business. [Learn more about device groups in Defender for Business](mdb-create-edit-device-groups).

### Run a detection test on a Windows 10 or 11 device

After you onboard Windows devices to Defender for Business, run a detection test on the device to ensure that everything is working correctly.

1. On the Windows device, create a folder: `C:\test-MDATP-test`.
2. Open a Command Prompt window as an administrator, and then run the following command:

    ```powershell
    powershell.exe -NoExit -ExecutionPolicy Bypass -WindowStyle Hidden $ErrorActionPreference = 'silentlycontinue';(New-Object System.Net.WebClient).DownloadFile('http://127.0.0.1/1.exe', 'C:\\test-MDATP-test\\invoice.exe');Start-Process 'C:\\test-MDATP-test\\invoice.exe'
    ```

When the command runs, the Command Prompt window closes automatically. If successful, the detection test is marked as completed, and a new alert appears in the [Microsoft Defender portal](https://security.microsoft.com) for the newly onboarded device within about 10 minutes.

# [Mac](#tab/mac)
## Mac

Note

We recommend using the local script to onboard Macs. Although you can [set up enrollment for Mac using Intune](/en-us/intune/intune-service/enrollment/macos-enroll), the local script is the simplest method for onboarding Macs to Defender for Business.

To onboard Mac devices, choose one of the following options:

- Local script for Mac (*recommended*)
- Intune for Mac (if you're already using Intune)

### Local script for Mac

When you run the local script on a Mac, it:

- Creates a trust with Microsoft Entra ID, if a trust doesn't already exist.
- Enrolls the Mac in Microsoft Intune, if it isn't already enrolled.
- Onboards the Mac to Defender for Business.

We recommend onboarding no more than 10 Macs at a time using this method.

1. Go to the [Microsoft Defender portal](https://security.microsoft.com), and sign in.
2. In the navigation pane, choose **Settings** &gt; **Endpoints**, and then under **Device management**, choose **Onboarding**.
3. Select **macOS**.
4. Under **Connectivity type**, select **Streamlined**.
5. In the **Deployment method** section, choose **Local script**, and then select **Download onboarding package**. Save the package to a removable drive. Also select **Download installation package**, and save it to your removable device.
6. On your Mac, save the installation package as `wdav.pkg` to a local directory.
7. Save the onboarding package as `WindowsDefenderATPOnboardingPackage.zip` to the same directory you used for the installation package.
8. Use Finder to navigate to `wdav.pkg` you saved, and then open it.
9. Select **Continue**, agree to the license terms, and then enter your password when prompted.
10. You're prompted to allow installation of a driver from Microsoft, *System Extension Blocked* or *Installation is on hold*, or both. You must allow the driver installation. Select **Open Security Preferences** or **Open System Preferences** &gt; **Security & Privacy**, and then select **Allow**.
11. Use the following Bash command to run the onboarding package:

    ```bash
    /usr/bin/unzip WindowsDefenderATPOnboardingPackage.zip \
    && /bin/chmod +x MicrosoftDefenderATPOnboardingMacOs.sh \
    && Sudo bash -x MicrosoftDefenderATPOnboardingMacOs.sh
    ```

After the Mac is enrolled in Intune, you can add it to a device group. [Learn more about device groups in Defender for Business](mdb-create-edit-device-groups).

### Intune for Mac

If you already have Intune, you can enroll Mac computers by using the [Intune admin center](https://intune.microsoft.com). There are several methods available for enrolling Mac in Intune. We recommend one of the following methods:

- Choose an option for company-owned Mac
- Ask users to enroll their own Mac in Intune

#### Options for company-owned Mac

Choose one of the following options to enroll company-managed Mac devices in Intune:

| Option | Description |
| --- | --- |
| Apple Automated Device Enrollment | Use this method to automate enrollment on devices purchased through Apple Business Manager or Apple School Manager. Automated device enrollment deploys the enrollment profile *over the air*, so you don't need to have physical access to devices.  For more information, see [Automatically enroll Mac with the Apple Business Manager or Apple School Manager](/en-us/intune/intune-service/enrollment/device-enrollment-program-enroll-macos). |
| Device enrollment manager (DEM) | Use this method for large-scale deployments and when there are multiple people in your organization who can help with enrollment setup. Someone with device enrollment manager (DEM) permissions can enroll up to 1,000 devices with a single Microsoft Entra account. This method uses the Company Portal app or Microsoft Intune app to enroll devices. You can't use a DEM account to enroll devices by using Automated Device Enrollment.  For more information, see [Enroll devices in Intune by using a device enrollment manager account](/en-us/intune/intune-service/enrollment/device-enrollment-manager-enroll). |
| Direct enrollment | Direct enrollment enrolls devices with no user affinity, so this method is best for devices that aren't associated with a single user. This method requires you to have physical access to the Macs you're enrolling.  For more information, see [Use Direct Enrollment for Mac](/en-us/intune/intune-service/enrollment/device-enrollment-direct-enroll-macos). |

#### Ask users to enroll their own Mac in Intune

If your business prefers to have users enroll devices in Intune, direct them to follow these steps:

1. Go to the [Company Portal website](https://portal.manage.microsoft.com/) and sign in.
2. Follow the instructions on the Company Portal website to add the device.
3. Install the [Company Portal app](https://aka.ms/EnrollMyMac), and follow the instructions in the app.

### Confirm that a Mac is onboarded

1. To confirm that the device is associated with your company, use the following Python command in Bash:

    `mdatp health --field org_id`.
2. If you're using macOS 10.15 (Catalina) or later, grant Defender for Business consent to protect your device. Go to **System Preferences** &gt; **Security & Privacy** &gt; **Privacy** &gt; **Full Disk Access**. Select the lock icon at the bottom of the dialog to make changes, and then select **Microsoft Defender for Business**, or **Defender for Endpoint**, if that's what you see.
3. To verify that the device is onboarded, use the following command in Bash:

    `mdatp health --field real_time_protection_enabled`

After you enroll a device in Intune, you can add it to a device group. [Learn more about device groups in Defender for Business](mdb-create-edit-device-groups).

# [Mobile devices](#tab/mobiles)
## Mobile devices

Use the following methods to onboard mobile devices, such as Android and iOS devices:

- Use the Microsoft Defender app
- Use Microsoft Intune

### Use the Microsoft Defender app

[Mobile threat defense capabilities](mdb-mtd) are available in Defender for Business. With these capabilities, you can now onboard mobile devices, such as Android and iOS, by using the Microsoft Defender app. With this method, users download the app from Google Play or the Apple App Store, sign in, and complete onboarding steps.

Important

Ensure that Defender for Business finishes provisioning: In the [Microsoft Defender portal](https://security.microsoft.com), go to **Assets** &gt; **Devices**.

- If you see the message, *Hang on! We're preparing new spaces for your data and connecting them*, Defender for Business isn't finished provisioning. This process is happening now, and it can take up to 24 hours to complete.
- If you see a list of devices, or you're prompted to onboard devices, it means Defender for Business provisioning is complete.

Users can use the following procedures to onboard mobile devices using the Microsoft Defender app:

- Android:

    1. If you didn't sign in and register your device in the Microsoft Authenticator app, follow these steps on the device:

        1. Install the [Microsoft Authenticator app](https://apps.apple.com/app/microsoft-authenticator/id983156458) from the Google Play store.
        2. In the Microsoft Authenticator app, sign in and register your device using your Microsoft 365 work or school account.
    2. Install the [Microsoft Defender: Antivirus app](https://play.google.com/store/apps/details?id=com.microsoft.scmx) from the Google Play store on your device.
    3. Open the Microsoft Defender app, sign in, and complete the onboarding process.
- iOS/iPadOS:

    1. If you didn't sign in and register your device in the Microsoft Authenticator app, follow these steps on the device:

        1. Install the [Microsoft Authenticator app](https://play.google.com/store/apps/details?id=com.azure.authenticator) from the Apple App Store.
        2. In the Microsoft Authenticator app, sign in and register your device using your Microsoft 365 work or school account.
    2. Install the [Microsoft Defender: Security app](https://apps.apple.com/app/microsoft-defender-security/id1526737990) from the Apple App Store on your device.
    3. Allow the Microsoft Defender app to set up a VPN connection and add VPN configurations.
    4. Choose whether to allow notifications, such as alerts.

Tip

After you onboard a mobile device using the Microsoft Defender app, go to the Run a phishing test on a device section later in this article.

### Use Microsoft Intune

If your subscription includes Microsoft Intune, you can use it to onboard mobile devices, such as Android and iOS or iPadOS devices. See the following resources to get help enrolling these devices into Intune:

- [Enroll Android devices](/en-us/intune/intune-service/fundamentals/deployment-guide-enrollment-android)
- [Enroll iOS or iPadOS devices](/en-us/intune/intune-service/fundamentals/deployment-guide-enrollment-ios-ipados)

After you enroll a device in Intune, you can add it to a device group. [Learn more about device groups in Defender for Business](mdb-create-edit-device-groups).

# [Servers](#tab/Servers)
## Servers

Note

To onboard an instance of Windows Server or Linux Server, you need an extra license, such as [Microsoft Defender for Business servers](get-defender-business#how-to-get-microsoft-defender-for-business-servers).

Choose the operating system for your server:

- Windows Server
- Linux Server

## Windows Server

Important

Before you onboard a Windows Server endpoint, ensure you meet the following requirements:

- You have a Microsoft Defender for Business servers license. For more information, see [How to get Microsoft Defender for Business servers](get-defender-business#how-to-get-microsoft-defender-for-business-servers).
- The enforcement scope for Windows Server is turned on. Go to **Settings** &gt; **Endpoints** &gt; **Configuration management** &gt; **Enforcement scope**. Select **Use MDE to enforce security configuration settings from MEM**, select **Windows Server**, and then select **Save**.

You can onboard an instance of Windows Server to Defender for Business by using a local script.

### Local script for Windows Server

1. Go to the [Microsoft Defender portal](https://security.microsoft.com), and sign in.
2. In the navigation pane, choose **Settings** &gt; **Endpoints**, and then under **Device management**, choose **Onboarding**.
3. Select an operating system, such as **Windows Server 1803, 2019, and 2022**, and then in the **Deployment method** section, choose **Local script**.

    If you select **Windows Server 2012 R2 and 2016**, you have two packages to download and run: an installation package and an onboarding package. The installation package contains an MSI file that installs the Defender for Business agent. The onboarding package contains the script to onboard your Windows Server endpoint to Defender for Business.
4. Select **Download onboarding package**. We recommend that you save the onboarding package to a removable drive.

    If you select **Windows Server 2012 R2 and 2016**, also select **Download installation package**, and save the package to a removable drive.
5. On your Windows Server endpoint, extract the contents of the installation and onboarding packages to a location such as the Desktop folder. You should have a file named `WindowsDefenderATPLocalOnboardingScript.cmd`.

    If you're onboarding Windows Server 2012 R2 or Windows Server 2016, extract the installation package first.
6. Open a command prompt as an administrator and complete the following steps:

    - **Windows Server 2012 R2 or Windows Server 2016**: Run the following commands:

        ```cmd
        Msiexec.exe /i md4ws.msi /quiet
        ```

        Run the `WindowsDefenderATPLocalOnboardingScript.cmd`. For example, if you copied the file to the Desktop folder, run the following command:

        ```cmd
        %userprofile%\Desktop\WindowsDefenderATPLocalOnboardingScript.cmd
        ```
    - **Windows Server 1803, 2019, or 2022**: Run the `WindowsDefenderATPLocalOnboardingScript.cmd`. For example, if you copied the file to the Desktop folder, run the following command:

        ```cmd
        %userprofile%\Desktop\WindowsDefenderATPLocalOnboardingScript.cmd
        ```
7. Go to the Run a detection test on Windows Server section.

### Run a detection test on Windows Server

After you onboard your Windows Server endpoint to Defender for Business, run a detection test to ensure that everything is working correctly:

1. On the Windows Server device, create a folder: `C:\test-MDATP-test`.
2. Open Command Prompt as an administrator, and run the following commands:

    ```cmd
    powershell.exe -NoExit -ExecutionPolicy Bypass -WindowStyle Hidden $ErrorActionPreference = 'silentlycontinue';(New-Object System.Net.WebClient).DownloadFile('http://127.0.0.1/1.exe', 'C:\\test-MDATP-test\\invoice.exe');Start-Process 'C:\\test-MDATP-test\\invoice.exe'
    ```

When the command runs, the Command Prompt window closes automatically. If successful, the detection test is marked as completed, and a new alert appears in the [Microsoft Defender portal](https://security.microsoft.com) for the newly onboarded device within about 10 minutes.

## Linux Server

Important

Ensure that you meet the following requirements before you onboard a Linux Server endpoint:

- You have a Microsoft Defender for Business servers license. For more information, see [How to get Microsoft Defender for Business servers](get-defender-business#how-to-get-microsoft-defender-for-business-servers).
- You meet the [prerequisites for Microsoft Defender for Endpoint on Linux](/en-us/defender-endpoint/mde-linux-prerequisites).

### Onboard Linux Server endpoints

Use the following methods to onboard a Linux Server instance to Defender for Business:

- **Defender deployment tool**: [Deploy Microsoft Defender for Endpoint on Linux with Defender deployment tool](/en-us/defender-endpoint/linux-install-with-defender-deployment-tool).
- **Local script**: [Deploy Microsoft Defender for Endpoint on Linux manually](/en-us/defender-endpoint/linux-install-manually).
- **Ansible**: [Deploy Microsoft Defender for Endpoint on Linux with Ansible](/en-us/defender-endpoint/linux-install-with-ansible).
- **Chef**: [Deploy Defender for Endpoint on Linux with Chef](/en-us/defender-endpoint/linux-deploy-defender-for-endpoint-with-chef).
- **Puppet**: [Deploy Microsoft Defender for Endpoint on Linux with Puppet](/en-us/defender-endpoint/linux-install-with-puppet).

Note

Onboarding an instance of Linux Server to Defender for Business is the same as onboarding to [Microsoft Defender for Endpoint on Linux](/en-us/defender-endpoint/microsoft-defender-endpoint-linux).

---

## View a list of onboarded devices

1. Go to the [Microsoft Defender portal](https://security.microsoft.com), and sign in.
2. In the navigation pane, go to **Assets** &gt; **Devices**. The **Device inventory** view opens.

## Run a phishing test on a device

After you onboard a device, run a quick phishing test to ensure the device is connected and generates alerts as expected.

1. On a device, go to https://smartscreentestratings2.net. Defender for Business should block that URL on the user's device.
2. As a member of your organization's security team, go to the [Microsoft Defender portal](https://security.microsoft.com) and sign in.
3. In the navigation pane, go to **Incidents**. You should see an informational alert that indicates a device tried to access a phishing site.