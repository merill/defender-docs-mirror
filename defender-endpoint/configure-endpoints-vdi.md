---
layout: Conceptual
title: Onboard non-persistent VDI devices to Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/configure-endpoints-vdi
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to onboard non-persistent virtual desktop infrastructure devices to Microsoft Defender for Endpoint and maintain VDI images.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.reviewer: pahuijbr; yonghree
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.custom: admindeeplinkDEFENDER, msecd-doc-authoring-1015
ms.topic: install-set-up-deploy
ms.date: 2026-09-21T00:00:00.0000000Z
ms.subservice: onboard
ai-usage: ai-assisted
locale: en-us
document_id: 73867a0a-d15e-74a0-d78a-7bb2e5830ccd
document_version_independent_id: 73867a0a-d15e-74a0-d78a-7bb2e5830ccd
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/configure-endpoints-vdi.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-endpoints-vdi
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/configure-endpoints-vdi.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://authoring-docs-microsoft.poolparty.biz/devrel/7814ca69-56be-4667-8a46-86327796c328
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/f15dfcd0-2664-48ba-bb88-f1f86eadbfd1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 98e6573c-d886-45c4-49ff-767d0a35f41c
---

# Onboard non-persistent VDI devices to Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

You can use the virtual desktop infrastructure (VDI) onboarding package to onboard non-persistent Windows virtual desktops to Microsoft Defender for Endpoint as the desktops are provisioned. Before you begin, review the prerequisites and choose a device-entry model. Then, add the onboarding scripts to a primary image, verify onboarding, and prepare an onboarded image for reuse.

Note

Onboard a persistent VDI device in the same way as a physical Windows device. For supported deployment methods, see [Onboard Windows client devices](onboard-client).

Note

The Defender deployment tool can be used to deploy Defender endpoint security on Windows and Linux devices. The tool is a lightweight, self-updating application that streamlines the deployment process. For more information, see [Deploy Microsoft Defender endpoint security to Windows devices using the Defender deployment tool](/en-us/defender-endpoint/defender-deployment-tool-windows) and [Deploy Microsoft Defender endpoint security to Linux devices using the Defender deployment tool (preview)](/en-us/defender-endpoint/linux-install-with-defender-deployment-tool).

## Prerequisites

- Review the [minimum requirements for Microsoft Defender for Endpoint](minimum-requirements) and [configure device connectivity](configure-device-connectivity).
- To download the onboarding package, you need full access to Defender for Endpoint. The Microsoft Entra [Security Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator) role grants this access. For more information, see [Assign basic permissions](basic-permissions).
- Use an account with local administrator permissions to configure and maintain the primary VDI image.
- For Windows Server 2012 R2 and Windows Server 2016, install the current unified Defender for Endpoint solution before you add the VDI onboarding scripts. For prerequisites and installation guidance, see [Onboard Windows Server 2012 R2 and Windows Server 2016](onboard-server#onboard-windows-server-2016-and-windows-server-2012-r2).

## Plan non-persistent VDI onboarding

Non-persistent desktops are short-lived, and their device names are often reused. Choose one of the following device-entry models before you configure the image:

- **Single entry for each device**: Recreated desktops that use the same final device name use one device entry in the Defender portal. This model uses `Onboard-NonPersistentMachine.ps1` and `WindowsDefenderATPOnboardingScript.cmd`.
- **Multiple entries for each device**: Each provisioned VDI instance creates a separate device entry. This model uses `WindowsDefenderATPOnboardingScript.cmd`.

The first time a VDI device onboards, client reporting can be delayed by approximately three to four hours.

Important

Don't onboard the primary image, internal template virtual machines (VMs), or replica VMs. Cloning an onboarded image can duplicate its `senseGuid`, which can prevent the provisioned VMs from appearing as new device entries in the Defender portal.

Warning

On VDI devices with limited resources, the boot process can delay Defender for Endpoint sensor onboarding.

## Onboard non-persistent VDI devices

Download the VDI onboarding package, add the applicable scripts to the primary image, and configure the scripts to run when each provisioned device starts.

Note

Before you configure VDI onboarding for Windows Server 2012 R2 or Windows Server 2016, install the current unified Defender for Endpoint solution as described in [Onboard Windows Server 2012 R2 and Windows Server 2016](onboard-server).

1. On the **Onboarding** page in the Microsoft Defender portal at https://security.microsoft.com/securitysettings/endpoints/onboarding, configure the package. If the direct link doesn't open, sign in to the [Microsoft Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2077139), and then open the **Onboarding** page.

    1. **Step 1: Select an operating system to start deployment**: Select the operating-system version group for the VDI devices. Don't select **Windows**, which starts the separate [Defender deployment tool workflow](defender-deployment-tool-windows).
    2. If **Connectivity type** is available, select **Standard** or **Streamlined** for your environment. For streamlined-connectivity requirements, see [Onboard devices using streamlined connectivity](configure-device-connectivity).
    3. For **Deployment method**, select **VDI onboarding scripts for non-persistent endpoints**.
    4. Select **Download onboarding package** to download `WindowsDefenderATPOnboardingPackage.zip`.
2. Extract the package. Copy the applicable files from the extracted `WindowsDefenderATPOnboardingPackage` folder to `C:\Windows\System32\GroupPolicy\Machine\Scripts\Startup` in the primary image:

    - For a single entry for each device, copy `Onboard-NonPersistentMachine.ps1` and `WindowsDefenderATPOnboardingScript.cmd`.
    - For multiple entries for each device, copy `WindowsDefenderATPOnboardingScript.cmd`.

    Note

    If the `C:\Windows\System32\GroupPolicy\Machine\Scripts\Startup` folder is hidden, turn on **Hidden items** in File Explorer.
3. Open the Local Group Policy Editor, and go to **Computer Configuration** &gt; **Windows Settings** &gt; **Scripts (Startup/Shutdown)** &gt; **Startup**.

    Note

    You can also use domain Group Policy to run the onboarding scripts.
4. Configure the startup script for the device-entry model:

    - **Single entry for each device**: On the **PowerShell Scripts** tab, select **Add**, and select `Onboard-NonPersistentMachine.ps1`. The PowerShell script runs `WindowsDefenderATPOnboardingScript.cmd`; don't add the `.cmd` file separately.
    - **Multiple entries for each device**: On the **Scripts** tab, select **Add**, and select `WindowsDefenderATPOnboardingScript.cmd`.

    Note

    For the single-entry model, run `Onboard-NonPersistentMachine.ps1` only after the VM has its final device name and completes its final provisioning restart. Running the script earlier can create duplicate device entries or inconsistent onboarding. The script isn't signed. If your organization restricts PowerShell script execution, use an organization-approved method to run the script.
5. Provision a test pool that contains one device. Sign in to the device, sign out, and then sign in with another account.
6. On the **Device inventory** page in the Microsoft Defender portal at https://security.microsoft.com/machines?category=all-devices, search for the device name.

    - For the single-entry model, verify that only one device entry appears.
    - For the multiple-entry model, verify that the expected separate device entries appear for the provisioned VDI instances.

## Configure legacy MMA-based VDI devices

Note

Windows Server 2008 R2 SP1 now uses the [Defender deployment tool](defender-deployment-tool-windows). If Windows Server 2008 R2 SP1, Windows Server 2012 R2, or Windows Server 2016 devices still use the legacy Microsoft Monitoring Agent (MMA), Microsoft recommends upgrading to the current Defender for Endpoint agent. For upgrade guidance, see [Update MMA on Windows devices](update-agent-mma-windows) and [Server migration scenarios in Microsoft Defender for Endpoint](server-migration).

For an existing legacy MMA-based VDI deployment that uses the single-entry model, configure the VDI device tag:

1. Create the registry value by importing the following registry data:

    ```console
    [HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Advanced Threat Protection\DeviceTagging]
     "VDI"="NonPersistent"
    ```

    Alternatively, create the same registry value from Command Prompt:

    ```dos
    reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Advanced Threat Protection\DeviceTagging" /v VDI /t REG_SZ /d "NonPersistent" /f
    ```
2. For Windows Server 2012 R2 and later, follow the [server onboarding process](onboard-server).

## Update VDI images

Apply operating-system, app, Defender platform, engine, and security intelligence updates to VDI images through your normal image-maintenance process. If the primary image was onboarded and the SENSE service is running, offboard the image and clear its local Defender for Endpoint registration data before you use the image to provision devices.

Note

To update virtual desktop infrastructure (VDI) images, you need local administrator permissions and the [PsExec](/en-us/sysinternals/downloads/psexec) tool.

To remove Defender for Endpoint registration data from an onboarded image:

1. [Offboard the machine](offboard-machines), and confirm that the offboarding process finishes.
2. Make sure `PsExec.exe` is available in the command prompt path. PsExec starts a command shell under the SYSTEM account so that you can remove the registration data.
3. Open Command Prompt as an administrator.
4. Check the SENSE service state to confirm that the sensor isn't running:

    ```dos
    sc query sense
    ```
5. Start a SYSTEM-level command shell and remove the local Defender for Endpoint registration data:

    ```console
    PsExec.exe -s cmd.exe
    
    del "C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Cyber\*.*" /f /s /q
    
    REG DELETE "HKLM\SOFTWARE\Microsoft\Windows Advanced Threat Protection" /v senseGuid /f
    
    REG DELETE "HKLM\SOFTWARE\Microsoft\Windows Advanced Threat Protection" /v senseId /f
    
    REG DELETE "HKLM\SOFTWARE\Microsoft\Windows Advanced Threat Protection" /v 2567E824-34AB-4A74-90E9-BC0F8BDFAA4A /f
    
    REG DELETE "HKLM\SOFTWARE\Microsoft\Windows Advanced Threat Protection" /v 7DC0B629-D7F6-4DB3-9BF7-64D5AAF50F1A /f
    
    REG DELETE "HKLM\SOFTWARE\Microsoft\Windows Advanced Threat Protection" /v C9D38BBB-E9DD-4B27-8E6F-7DE97E68DAB9 /f
    
    REG DELETE "HKLM\SOFTWARE\Microsoft\Windows Advanced Threat Protection\48A68F11-7A16-4180-B32C-7F974C7BD783" /f
    
    exit
    ```

Note

A registry deletion command can return **The system was unable to find the specified registry key or value** when the registry path doesn't exist. You can ignore this expected message.

### Prepare images for third-party VDI platforms

For VMware instant cloning and similar technologies, make sure that the primary image, internal template VMs, and replica VMs aren't onboarded to Defender for Endpoint. With the single-entry model, clones provisioned from an onboarded VM can inherit the same `senseGuid`. The duplicate identifier can prevent new non-persistent VDI devices from appearing in the [Microsoft Defender portal](https://security.microsoft.com).

For platform-specific image preparation, contact the VDI platform vendor.

## Other recommended configuration settings

Onboarding connects VDI devices to Defender for Endpoint, but it doesn't configure Microsoft Defender Antivirus protection and performance settings.

### Configure Microsoft Defender Antivirus

For recommended protection, update, scan, and performance settings, see [Configure Microsoft Defender Antivirus on a remote desktop or virtual desktop infrastructure environment](deployment-vdi-microsoft-defender-antivirus).