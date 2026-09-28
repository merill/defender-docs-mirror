---
layout: Conceptual
title: Use the Microsoft Defender deployment tool for Windows - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/defender-deployment-tool-windows
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use the Microsoft Defender deployment tool to onboard, update, stage, and offboard supported Windows devices.
ms.service: defender-endpoint
ms.localizationpriority: medium
ms.topic: how-to
author: paulinbar
ms.author: painbar
ms.custom: nextgen, msecd-doc-authoring-1015
ms.reviewer: pahuijbr, sihamilt
ms.collection:
- m365-security
- tier3
ms.subservice: onboard
ms.date: 2026-09-22T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 67364684-294b-f129-1fd8-7580fefde15e
document_version_independent_id: 67364684-294b-f129-1fd8-7580fefde15e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/defender-deployment-tool-windows.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defender-deployment-tool-windows
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/defender-deployment-tool-windows.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 0d8bce2e-138c-0854-de0f-8cf7fa680445
---

# Use the Microsoft Defender deployment tool for Windows - Microsoft Defender for Endpoint | Microsoft Learn

The Microsoft Defender deployment tool is a lightweight, self-updating application that installs prerequisites and onboards [supported Windows devices](minimum-requirements#windows-versions-supported-by-defender-for-endpoint) to Microsoft Defender for Endpoint. Run the tool interactively on individual devices, or automate it with command-line parameters, configuration files, Group Policy, Microsoft Configuration Manager, or another software deployment system.

Use the deployment tool as a separate onboarding method. It doesn't integrate with onboarding through Microsoft Intune, Microsoft Defender for Cloud, or other deployment methods. Before you begin, review the supported operating systems and prerequisites.

The deployment tool provides these features:

- **Prerequisite handling**: Checks for required updates and resolves issues that block deployment.
- **Logging and feedback**: Records operations in a local log and displays error descriptions in interactive mode.
- **Installation and updates**: Avoids reinstalling existing components and downloads current components when needed.
- **Automation**: Supports command-line parameters and reusable configuration files for automated deployments.
- **Staging**: Downloads installation files for target devices that can't download the files directly.
- **Server passive mode**: Configures Microsoft Defender Antivirus to run in passive mode on Windows Server.
- **Nonpersistent virtual desktop infrastructure (VDI)**: Helps devices recreated with the same hostname appear as one device in the Defender portal.
- **Package guardrails**: Requires a portal-generated access key for onboarding and supports package expiration dates from one day to one year. Use the shortest practical validity period.
- **Package management**: Lists deployment packages in the [Microsoft Defender portal](https://security.microsoft.com) and lets you filter them by properties such as status and expiration date.
- **Built-in help**: Displays the available command-line options when you run `DefenderDT.exe -?`.

In interactive mode, the tool prompts for the access key from the Defender portal, installs required updates and Defender components, and connects the device to Defender for Endpoint. If installation requires a restart, sign in after the restart so the tool can resume.

For advanced and large-scale deployments, use command-line parameters or a configuration file.

## Supported operating systems

The Defender deployment tool supports the following operating systems:

- Windows 11
- Windows 10, version 1809 (November 2018) or later
- Windows 7 SP1
- Windows Server 2016 or later
- Windows Server 2012 R2
- Windows Server 2008 R2 SP1

Note

Windows 8.1 Pro and Enterprise are supported by Defender for Endpoint, but not by the Defender deployment tool. Onboard Windows 8.1 devices by using the Microsoft Monitoring Agent (MMA). For more information, see [Onboard previous versions of Windows](onboard-downlevel#install-and-configure-microsoft-monitoring-agent-windows-81-only).

## Prerequisites

Review the general prerequisites and the requirements for Windows 7 SP1 and Windows Server 2008 R2 SP1 before you deploy the tool.

### General prerequisites

- Most operations require administrative privileges.
- Allow access to `definitionupdates.microsoft.com`. The tool downloads updates and installation files from this domain. Because the files are hosted on a content distribution network, the associated IP address ranges aren't static or predictable.
- The tool checks connectivity to your organization before onboarding. Other Defender for Endpoint features also require access to service URLs such as `*.endpoint.security.microsoft.com`. For the complete requirements, see [Configure your network environment to ensure connectivity with the Defender for Endpoint service](configure-environment).

For streamlined connectivity, exclude traffic to `*.endpoint.security.microsoft.com` from SSL/TLS inspection, HTTPS interception, and man-in-the-middle (MITM) proxying. If you enable SSL inspection, Defender for Endpoint sensors might fail to communicate with backend services, resulting in onboarding or connectivity failures.

### Prerequisites for Windows 7 SP1 and Windows Server 2008 R2 SP1

- Devices must run an x64 version of Windows 7 SP1 or Windows Server 2008 R2 SP1. Install the latest available updates to reduce installation time and the likelihood of a restart.
- Install [SHA-2 code-signing support](https://support.microsoft.com/servicing/os/windows/2020/09/2019-sha-2-code-signing-support-requirement-for-windows-and-wsus). The deployment tool requires at least KB4474419.

    - Install the servicing stack update (SSU) [KB4490628](https://support.microsoft.com/topic/servicing-stack-update-for-windows-7-sp1-and-windows-server-2008-r2-sp1-march-12-2019-b4dc0cff-d4f2-a408-0cb1-cb8e918feeba). Windows Update offers the required SSU automatically.
    - Install the SHA-2 update [KB4474419](https://support.microsoft.com/topic/sha-2-code-signing-support-update-for-windows-server-2008-r2-windows-7-and-windows-server-2008-september-23-2019-84a8aad5-d8d9-2d5c-6d78-34f9aa5f8339), released September 10, 2019. Windows Update offers the required update automatically.
- On Windows Server 2008 R2 SP1, install .NET Framework 3.5 or later.

Note

For more information about Defender endpoint security for Windows 7 SP1 and Windows Server 2008 R2 SP1, see [Deploy the Defender endpoint security solution for Windows 7 SP1 and Windows Server 2008 R2 SP1 devices](onboard-downlevel#use-the-defender-deployment-tool-to-deploy-defender-endpoint-security).

## Generate and download a new onboarding package

Generate an onboarding package and access key in the Microsoft Defender portal. You need the access key when you run the tool interactively or with the `-Key` parameter.

1. On the **Onboarding** page in the Microsoft Defender portal at https://security.microsoft.com/securitysettings/endpoints/onboarding, configure the following settings:

    - **Step 1: Select an operating system to start deployment**: Select **Windows**.
    - **Step 2: Choose a deployment option**: Select **Onboard** in **Deploy by downloading and applying packages or files** &gt; **Defender deployment tool**.

    [![Screenshot of the Defender portal option to generate a Defender deployment tool package.](media/defender-deployment-tool-windows/defender-deployment-tool-windows-download-package.png)](media/defender-deployment-tool-windows/defender-deployment-tool-windows-download-package.png#lightbox)
2. On the **Generate Defender deployment tool with an access key** flyout that opens, configure the package:

    - **Name**: Enter a unique, descriptive package name.
    - **Organization**: Verify the displayed organization.
    - **Expires**: Use the shortest practical validity period to reduce the risk of unauthorized package use:
        - **In 7 days** (default)
        - **In 30 days**
        - **Custom** (up to one year)

    Select **Generate**.

    [![Screenshot of the settings for a new Defender deployment tool package.](media/defender-deployment-tool-windows/configure-deployment-package.png)](media/defender-deployment-tool-windows/configure-deployment-package.png#lightbox)
3. When the package is ready, copy and securely store the access key.

    [![Screenshot of the generated deployment package access key and download option.](media/defender-deployment-tool-windows/deployment-package-download-page.png)](media/defender-deployment-tool-windows/deployment-package-download-page.png#lightbox)
4. Select **Download deployment tool**, and save the downloaded executable.

## Deploy Defender endpoint security on devices

Run the Defender deployment tool interactively or non-interactively.

### Interactive use

Use interactive mode for one device or a small number of devices. Double-click the executable to use the default onboarding settings, or run the tool from Command Prompt to specify options.

To onboard a device with the default settings:

1. Double-click the executable to launch it.
2. In the dialog that confirms onboarding will start, select **Continue**.
3. Enter the Defender deployment tool key that you copied from the portal, and then select **Continue**.

    [![Screenshot of the Defender deployment tool access key prompt.](media/defender-deployment-tool-windows/interactive-mode.png)](media/defender-deployment-tool-windows/interactive-mode.png#lightbox)
4. Wait for installation to finish, and then select **OK**. If the tool requires a restart, sign in after the restart so installation can resume.

### Non-interactive use

Use the command-line interface to automate installation and onboarding or to run other operations, such as prerequisite checks.

For the available parameters, see Defender deployment tool command reference. To view the command reference for your downloaded tool version, run `DefenderDT.exe -?`.

### Advanced and large-scale deployments

Run the Defender deployment tool non-interactively from Group Policy, Microsoft Configuration Manager, or another software deployment system. Use command-line parameters to customize onboarding, staging, updates, restarts, proxies, and other operations.

For recurring deployments, use a configuration file instead of repeating command-line parameters. Run the tool with `-MakeConfig` to generate `DefenderDTconfig.txt`. Edit the configuration, and then load it with `-Config:<path>`. If you don't specify a path, the tool looks for `DefenderDTconfig.txt` in the current folder. For an example, see Use a configuration file.

## Defender deployment tool command reference

The following table lists the parameters available in the Defender deployment tool version 1.0.0.6 (September 2026). Run `DefenderDT.exe -?` to verify the parameters available in your downloaded version.

| Category | Parameter | Description |
| --- | --- | --- |
| General | `-?`, `-Help` | Display the available options. |
| General | `-Quiet` | Prevent dialogs from appearing. |
| General | `-Verbose` | Display detailed information and write detailed logs. |
| Configuration | `-AllowReboot` | Allow the device to restart when required. |
| Configuration | `-NoResumeAfterReboot` | Prevent the tool from resuming after a restart. |
| Configuration | `-Proxy:<https://host:port>` | Configure the proxy server for onboarding and Defender for Endpoint. |
| Configuration | `-Precheck` | Check prerequisites and log the results without installing or onboarding. |
| Configuration | `-UpdateOnly` | Install updates without onboarding, even when an onboarding file is present. |
| Onboarding | `-File:<path>` | Specify the absolute path to an `.onboarding` or `.offboarding` file. If you don't specify the parameter, the tool looks for `WindowsDefenderATP.onboarding` in the current folder. |
| Onboarding | `-Source:<path>` | Specify the folder that contains staged installation files. |
| Onboarding | `-Passive` | Configure Microsoft Defender Antivirus to run in passive mode on Windows Server. |
| Onboarding | `-VDI` | Identify the device as a nonpersistent virtual desktop infrastructure (VDI) device. |
| Onboarding | `-DeviceTag:<tag>` | Add a tag to the device. |
| Onboarding | `-Key:<key>` | Specify the onboarding access key generated in the Defender portal. |
| Offboarding | `-Offboard` | Offboard the device. Specify the `.offboarding` file with `-File:<path>`. |
| Offboarding | `-Uninstall` | Offboard the device and uninstall components added during onboarding. Specify the `.offboarding` file with `-File:<path>`. |
| Offboarding | `-Yes` | Proceed with offboarding or uninstalling without prompting for confirmation. |
| Offboarding | `-Offline` | Allow offboarding without connectivity. |
| Configuration | `-RemoveMMA:<workspace-id>` | Remove the specified Microsoft Monitoring Agent (MMA) workspace connection. |
| Advanced deployment | `-MakeConfig` | Generate `DefenderDTconfig.txt` with default values. |
| Advanced deployment | `-Stage:<path>` | Download installation files for all supported Windows versions to the specified absolute path. |
| Advanced deployment | `-Config:<path>` | Load parameters from a configuration file. If you omit the path, the tool looks for `DefenderDTconfig.txt` in the current folder. |

Use an elevated Command Prompt (a Command Prompt window you opened by selecting **Run as administrator**) for onboarding, offboarding, uninstalling, updating, and configuration-file generation. The `-Help`, `-Precheck`, and `-Stage` operations don't require administrative privileges. A configuration file also bypasses the administrator check when it specifies only precheck or staging.

## Usage examples

Replace placeholder paths, keys, and proxy addresses in the following examples with values for your environment. Use an elevated Command Prompt except for the precheck and staging examples.

- Run the default onboarding sequence without displaying dialogs. The tool uses `WindowsDefenderATP.onboarding` from the current folder:

    ```dos
    DefenderDT.exe -Quiet
    ```
- Onboard by using an access key, configure a proxy, allow a required restart, and prevent dialogs:

    ```dos
    DefenderDT.exe -Key:<access-key> -Proxy:https://proxy.contoso.com:8080 -AllowReboot -Quiet
    ```
- Onboard by using an onboarding file in a network location without displaying dialogs:

    ```dos
    DefenderDT.exe -File:\\server.contoso.com\share\WindowsDefenderATP.onboarding -Quiet
    ```
- Offboard the device by using a local offboarding file without prompting for confirmation or displaying dialogs:

    ```dos
    DefenderDT.exe -Offboard -File:C:\Packages\WindowsDefenderATP.offboarding -Yes -Quiet
    ```
- Check prerequisites, display detailed output, and prevent dialogs:

    ```dos
    DefenderDT.exe -PreCheck -Verbose -Quiet
    ```
- Download installation files for all supported Windows versions to an absolute staging path:

    ```dos
    DefenderDT.exe -Stage:C:\DefenderDT\StagedFiles
    ```

### Use a configuration file

Generate a configuration file when you want to reuse the same parameters in multiple deployments.

1. Generate `DefenderDTconfig.txt` in the current folder:

    ```dos
    DefenderDT.exe -MakeConfig
    ```
2. Open `DefenderDTconfig.txt` in a text editor, and configure the parameters for your deployment. Use absolute paths for parameters that accept a path.
3. Run the tool with the configuration file. The following example loads the file from a network location:

    ```dos
    DefenderDT.exe -Config:\\server.contoso.com\share\DefenderDTconfig.txt
    ```

    If `DefenderDTconfig.txt` is in the current folder, run `DefenderDT.exe -Config`.

## Deploy by using Group Policy

Use a Group Policy immediate scheduled task to run the deployment tool as `SYSTEM` with elevated permissions. For the generic steps to create, configure, link, and test the scheduled task, see [Onboard devices by using Group Policy](configure-endpoints-gp#onboard-devices-by-using-group-policy).

Use these Defender deployment tool-specific values:

- Store `DefenderDT.exe`, the `.onboarding` file, and any `DefenderDTconfig.txt` file in a shared, read-only location that the target devices can access.
- For **Program/script**, enter the full Universal Naming Convention (UNC) path to `DefenderDT.exe`. Use the file server's fully qualified domain name (FQDN).
- For **Add arguments**, enter the required command-line parameters. For example, use `-File:\\server\share\WindowsDefenderATP.onboarding -Quiet` when the onboarding file isn't in the tool's working directory.
- Run the task as `NT AUTHORITY\SYSTEM`, regardless of whether a user is signed in, and select **Run with highest privileges**.
- Test the Group Policy object (GPO) with a limited device group before broader deployment.

For more information about the management console, see [Group Policy Management Console](/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-management-console).

## Offboard a device

To offboard a device, download the offboarding package from the Defender portal, transfer it to the target device, and run the deployment tool with the package.

### Step 1: Download the offboarding package

1. On the **Offboarding** page in the Microsoft Defender portal at https://security.microsoft.com/securitysettings/endpoints/offboarding, select **Windows** under **Select operating system**.
2. Under **Defender deployment tool**, select **Download package** to download the `.zip` file that contains the offboarding script.

    [![Screenshot of the Defender portal option to download a deployment tool offboarding package.](media/defender-deployment-tool-windows/defender-deployment-tool-windows-offboard.png)](media/defender-deployment-tool-windows/defender-deployment-tool-windows-offboard.png#lightbox)

### Step 2: Run the offboarding command

Complete these steps on the device that you want to offboard:

1. Copy the `.zip` file to the target device, and extract the `.offboarding` file.
2. Run the deployment tool in an elevated Command Prompt with the absolute path to the extracted `.offboarding` file. For example:

    ```dos
    DefenderDT.exe -Offboard -File:C:\Packages\WindowsDefenderATP.offboarding
    ```
3. Type **Y** in the confirmation dialog to proceed.
4. Wait for the process to finish. After a successful offboarding, the tool displays the following message:

    ```console
    Microsoft Defender deployment tool completed, exit code: 0 [Success]
    ```

## Considerations and limitations

Review the general limitations and the limitations for Windows 7 SP1 and Windows Server 2008 R2 SP1.

### General considerations and limitations

- If the interactive sequence requires a restart, sign in again after the restart so the tool can resume. Otherwise, the device isn't fully onboarded.
- On Windows Server 2016 and later, the **Enabling Feature 'Windows-Defender'** step might fail if the Microsoft Defender Antivirus feature was uninstalled or removed. The user interface and local log show exit code `710` and `EnableFeatureFailed`. The log might also contain error `14081` and `0x3701 The referenced assembly could not be found`. Open a support case for Windows Server if you encounter this issue.

### Known issues and limitations for Windows 7 SP1 and Windows Server 2008 R2 SP1

- You might get alerts about `mpclient.dll`, `mpcommu.dll`, `mpsvc.dll`, `msmplics.dll`, and `sense1ds.dll` loaded by either `MpCmdRun.exe` or `MsSense.exe`. The alerts should resolve over time.
- On Windows 7 SP1 and Windows Server 2008 R2 SP1 with the Desktop Experience pack installed, Action Center might display *Windows did not find antivirus software on this computer*. The notification doesn't indicate a deployment problem.
- Use the preview version of the [client analyzer tool](https://aka.ms/betamdeanalyzer) to collect logs and troubleshoot connectivity on Windows 7 SP1 and Windows Server 2008 R2 SP1. The analyzer requires PowerShell 5.1 or later.
- Microsoft Defender Antivirus doesn't provide a local user interface on these operating systems. To manage Microsoft Defender Antivirus settings locally, install PowerShell 5.1 or later.
- Group Policy configuration requires a Central Store with current Group Policy templates on a domain controller. To use Local Group Policy Editor, manually update `WindowsDefender.admx` and `WindowsDefender.adml` with current Windows 11 templates.
- The Defender endpoint security solution installs in `C:\Program Files\Microsoft Defender for Endpoint`.
- The deployment tool's `-Passive` parameter applies to Windows Server. It isn't supported for Windows 7 SP1.

## Troubleshooting

Review the Defender deployment tool log for problems during installation and onboarding. The log is located at:

`C:\ProgramData\Microsoft\DefenderDeploymentTool\DefenderDeploymentTool-<COMPUTERNAME>.log`

The tool also records events in these Windows event logs:

- **Onboarding**: Windows Logs &gt; Application &gt; Source: WDATPOnboarding
- **Offboarding**: Windows Logs &gt; Application &gt; Source: WDATPOffboarding

To verify that installation succeeded, complete these checks:

1. Verify the services are running with the following commands:

    ```dos
    Sc.exe query sense
    
    Sc.exe query windefend
    ```

    You should see the following output:

    ```console
    SERVICE_NAME: sense
            TYPE               : 10  WIN32_OWN_PROCESS
            STATE              : 4  RUNNING
                                    (STOPPABLE, NOT_PAUSABLE, ACCEPTS_PRESHUTDOWN)
            WIN32_EXIT_CODE    : 0  (0x0)
            SERVICE_EXIT_CODE  : 0  (0x0)
            CHECKPOINT         : 0x0
            WAIT_HINT          : 0x0
    
    SERVICE_NAME: windefend
            TYPE               : 10  WIN32_OWN_PROCESS
            STATE              : 4  RUNNING
                                    (STOPPABLE, NOT_PAUSABLE, ACCEPTS_SHUTDOWN)
            WIN32_EXIT_CODE    : 0  (0x0)
            SERVICE_EXIT_CODE  : 0  (0x0)
            CHECKPOINT         : 0x0
            WAIT_HINT          : 0x0
    ```
2. For Defender Antivirus logs, settings, and other diagnostic information, see [Collect Microsoft Defender Antivirus diagnostic data](collect-diagnostic-data).
3. Use the [client analyzer tool](run-analyzer-windows) to collect logs and troubleshoot connectivity on Windows.

## Exit codes

For large-scale deployments through a software distribution solution, monitor the following exit codes:

| Error code | Meaning |
| --- | --- |
| 0 | Sequence completed successfully |
| 1 | Another instance is already running |
| 2 | Device is already onboarded: no action required |
| 3 | Offboarding is only available for onboarded devices |
| 5 | A new version of this tool is available |
| 6 | Tool updated to the latest version |
| 10 | A reboot is required to continue. The tool resumes automatically unless the `NoResumeAfterReboot` parameter was specified. |
| 11 | Failed to verify signature |
| 12 | Failed to apply process mitigation policy |
| 20 | File not found |
| 30 | Required resource files are missing |
| 40 | Run the tool with administrative permissions |
| 50 | Unsupported operating system |
| 70 | Configuration file error detected |
| 80 | Quality telemetry failed |
| 90 | Prerequisite checks failed |
| 100 | Manifest file is corrupted |
| 200 | Onboarding failed: sensor initialization error |
| 201 | Onboarding file missing or not specified |
| 210 | Failed to reload the Defender Antivirus engine |
| 300 | Offboarding failed |
| 301 | Offboarding file missing or not specified |
| 302 | Invalid offboarding file |
| 400 | Download failed: unable to retrieve required component |
| 500 | Installation failed: unable to install required components |
| 600 | Update failed: unable to apply update package |
| 610 | Unsupported update file |
| 700 | System preparation failed |
| 710 | Failed to enable the Defender Antivirus feature |
| 720 | Failed to uninstall System Center Endpoint Protection (SCEP) |
| 730 | Failed to download and apply the latest manual signature for sovereign cloud |
| 740 | Failed to configure ADL registry settings for sovereign cloud |
| 900 | Failed to uninstall Defender components |
| 920 | Failed to remove the requested Microsoft Monitoring Agent (MMA) workspace |
| 930 | Invalid MMA workspace ID |
| 1000 | An unspecified error occurred |