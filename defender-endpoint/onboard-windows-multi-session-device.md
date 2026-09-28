---
layout: Conceptual
title: Onboard Windows devices in Azure Virtual Desktop - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/onboard-windows-multi-session-device
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn about onboarding Windows devices to Defender for Endpoint in Azure Virtual Desktop
ms.service: defender-endpoint
ms.localizationpriority: medium
ms.topic: install-set-up-deploy
author: paulinbar
ms.author: painbar
ms.custom: nextgen
ms.reviewer: thdoucet
ms.collection:
- m365-security
- tier3
ms.subservice: onboard
ms.date: 2025-11-17T00:00:00.0000000Z
locale: en-us
document_id: 77ccffa6-62b4-2946-f112-1a8cae1f1e4e
document_version_independent_id: 77ccffa6-62b4-2946-f112-1a8cae1f1e4e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/onboard-windows-multi-session-device.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: onboard-windows-multi-session-device
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/onboard-windows-multi-session-device.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7814ca69-56be-4667-8a46-86327796c328
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f15dfcd0-2664-48ba-bb88-f1f86eadbfd1
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: e3f0156a-175f-31de-eb45-84eeef34f0ac
---

# Onboard Windows devices in Azure Virtual Desktop - Microsoft Defender for Endpoint | Microsoft Learn

6 minutes to read

Microsoft Defender for Endpoint supports monitoring both VDI and Azure Virtual Desktop sessions. Depending on your organization's needs, you might need to implement VDI or Azure Virtual Desktop sessions to help your employees access corporate data and apps from an unmanaged device, remote location, or similar scenario. With Microsoft Defender for Endpoint, you can monitor these virtual machines for anomalous activity.

Note

The Defender deployment tool can be used to deploy Defender endpoint security on Windows and Linux devices. The tool is a lightweight, self-updating application that streamlines the deployment process. For more information, see [Deploy Microsoft Defender endpoint security to Windows devices using the Defender deployment tool](/en-us/defender-endpoint/defender-deployment-tool-windows) and [Deploy Microsoft Defender endpoint security to Linux devices using the Defender deployment tool (preview)](/en-us/defender-endpoint/linux-install-with-defender-deployment-tool).

## Before you begin

Familiarize yourself with the [considerations for non-persistent VDI](configure-endpoints-vdi#onboarding-non-persistent-virtual-desktop-infrastructure-vdi-devices). While [Azure Virtual Desktop](/en-us/azure/virtual-desktop/overview) doesn't provide non-persistence options, it does provide ways to use a golden Windows image that can be used to provision new hosts and redeploy machines. This increases volatility in the environment and thus impacts what entries are created and maintained in the Microsoft Defender for Endpoint portal, potentially reducing visibility for your security analysts.

Note

Depending on your choice of onboarding method, devices can appear in Microsoft Defender for Endpoint portal as either:

- Single entry for each virtual desktop
- Multiple entries for each virtual desktop

Microsoft recommends onboarding Azure Virtual Desktop as a single entry per virtual desktop. This ensures that the investigation experience in the Microsoft Defender for Endpoint portal is in the context of one device based on the machine name. Organizations that frequently delete and redeploy AVD hosts should strongly consider using this method as it prevents multiple objects for the same machine from being created in the Microsoft Defender for Endpoint portal. This can lead to confusion when investigating incidents. For test or non-volatile environments, you may opt to choose differently. When using the single entry per virtual desktop method, it is not necessary to offboard the virtual desktops.

Microsoft recommends adding the Microsoft Defender for Endpoint onboarding script to the AVD golden image. This way, you can be sure that this onboarding script runs immediately at first boot. It's executed as a startup script at first boot on all the AVD machines that are provisioned from the AVD golden image. However, if you're using one of the gallery images without modification, place the script in a shared location and call it from either local or domain group policy.

Note

The placement and configuration of the VDI onboarding startup script on the AVD golden image configures it as a startup script that runs when the AVD starts. It's **not** recommended to onboard the actual AVD golden image. Another consideration is the method used to run the script. It should run as early in the startup/provisioning process as possible to reduce the time between the machine being available to receive sessions and the device onboarding to the service. Below scenarios 1 and 2 take this into account.

### Scenarios

There are several ways to onboard an AVD host machine:

- Run the script in the golden image (or from a shared location) during startup.
- Use a management tool to run the script.
- Through [Integration with Microsoft Defender for Cloud](azure-server-integration)

#### *Scenario 1: Using local group policy*

This scenario requires placing the script in a golden image and uses local group policy to run early in the boot process.

Use the instructions in [Onboard the non-persistent virtual desktop infrastructure (VDI) devices](configure-endpoints-vdi).

Follow the instructions for a single entry for each device.

#### *Scenario 2: Using domain group policy*

This scenario uses a centrally located script and runs it using a domain-based group policy. You can also place the script in the golden image and run it in the same way.

##### Download the WindowsDefenderATPOnboardingPackage.zip file from the Microsoft Defender portal

1. Open the VDI configuration package .zip file (WindowsDefenderATPOnboardingPackage.zip)

    1. In the Microsoft Defender portal navigation pane, select **Settings** &gt; **Endpoints** &gt; **Onboarding** (under **Device Management**).
    2. Select Windows 10 or Windows 11 as the operating system.
    3. In the **Deployment method** field, select VDI onboarding scripts for non-persistent endpoints.
    4. Click **Download package** and save the .zip file.
2. Extract the contents of the .zip file to a shared, read-only location that can be accessed by the device. You should have a folder called **OptionalParamsPolicy** and the files **WindowsDefenderATPOnboardingScript.cmd** and **Onboard-NonPersistentMachine.ps1**.

##### Use Group Policy management console to run the script when the virtual machine starts

1. Open the Group Policy Management Console (GPMC), right-click the Group Policy Object (GPO) you want to configure and click **Edit**.
2. In the Group Policy Management Editor, go to **Computer configuration** &gt; **Preferences** &gt; **Control panel settings**.
3. Right-click **Scheduled tasks**, click **New**, and then click **Immediate Task** (At least Windows 7).
4. In the Task window that opens, go to the **General** tab. Under **Security options** click **Change User or Group** and type SYSTEM. Click **Check Names** and then click OK. NT AUTHORITY\SYSTEM appears as the user account the task will run as.
5. Select **Run whether user is logged on or not** and check the **Run with highest privileges** check box.
6. Go to the **Actions** tab and click **New**. Ensure that **Start a program** is selected in the Action field. Enter the following: `Action = "Start a program"`

    `Program/Script = C:\WINDOWS\system32\WindowsPowerShell\v1.0\powershell.exe`

    `Add Arguments (optional) = -ExecutionPolicy Bypass -command "& \\Path\To\Onboard-NonPersistentMachine.ps1"`

    Then select **OK** and close any open GPMC windows.

#### *Scenario 3: Onboarding using management tools*

If you plan to manage your machines using a management tool, you can onboard devices with Microsoft Configuration Manager.

For more information, see [Onboard Windows devices using Configuration Manager](configure-endpoints-sccm).

Note

If you plan to use [Attack surface reduction (ASR) rules](attack-surface-reduction-rules-reference), don't use the [Block process creations originating from PSExec and WMI commands](attack-surface-reduction-rules-reference#block-process-creations-originating-from-psexec-and-wmi-commands) rule. The Configuration Manager client relies heavily on WMI.

After onboarding the device, you can choose to run a detection test to verify that the device is properly onboarded to the service. For more information, see [Run a detection test on a newly onboarded Microsoft Defender for Endpoint device](run-detection-test).

#### Tagging your machines when building your golden image

As part of your onboarding, you may want to consider setting a machine tag to differentiate AVD machines more easily in the Microsoft Security Center. For more information, see [Add device tags by setting a registry key value](machine-tags#create-tags).

#### Other recommended configuration settings

When building your golden image, you may want to configure initial protection settings as well. For more information, see [Other recommended configuration settings](configure-endpoints-gp#other-recommended-configuration-settings).

Also, if you're using FSlogix user profiles, we recommend you follow the guidance described in [FSLogix antivirus exclusions](/en-us/fslogix/overview-prerequisites#configure-antivirus-file-and-folder-exclusions).

#### Licensing requirements

When using Windows Enterprise multi-session, per our security best practices the virtual machine can be licensed through Microsoft Defender for Servers or you can choose to have all Azure Virtual Desktop virtual machine users licensed through one of the following licenses:

- Microsoft Defender for Endpoint Plan 1 or Plan 2 (per user)
- Windows Enterprise E3
- Windows Enterprise E5
- Microsoft 365 E3
- Microsoft Defender Suite
- Microsoft 365 E5

Licensing requirements for Microsoft Defender for Endpoint can be found at: [Licensing requirements](minimum-requirements).

#### Related Links

[Add exclusions for Defender for Endpoint via PowerShell](/en-us/azure/architecture/example-scenario/wvd/windows-virtual-desktop-fslogix#add-exclusions-for-microsoft-defender-for-cloud-by-using-powershell)

[FSLogix anti-malware exclusions](/en-us/fslogix/overview-prerequisites#configure-antivirus-file-and-folder-exclusions)

[Configure Microsoft Defender Antivirus on a remote desktop or virtual desktop infrastructure environment](deployment-vdi-microsoft-defender-antivirus)