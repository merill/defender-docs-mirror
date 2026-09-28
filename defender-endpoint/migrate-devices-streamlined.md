---
layout: Conceptual
title: Migrate devices to use the streamlined connectivity method - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/migrate-devices-streamlined
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to migrate devices to Defender for Endpoint using the streamlined connectivity method.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.topic: how-to
ms.subservice: onboard
ms.date: 2026-09-18T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 49f96e51-7edd-546d-4bb2-d3d061a6a9a1
document_version_independent_id: 49f96e51-7edd-546d-4bb2-d3d061a6a9a1
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/migrate-devices-streamlined.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: migrate-devices-streamlined
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/migrate-devices-streamlined.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
platformId: 63267a12-d429-9bf1-00d6-48edb2543fd9
---

# Migrate devices to use the streamlined connectivity method - Microsoft Defender for Endpoint | Microsoft Learn

Use this article to reonboard existing Microsoft Defender for Endpoint devices with the streamlined connectivity package. Streamlined connectivity consolidates core Defender for Endpoint service traffic under a smaller set of network destinations. Before you migrate devices, configure the required network destinations and confirm that the devices meet the [streamlined connectivity prerequisites](configure-device-connectivity#prerequisites).

In most cases, you don't need to offboard devices before reonboarding them. Apply the streamlined onboarding package, and then reboot Windows devices or restart the Defender for Endpoint service on macOS and Linux devices.

Important

Review the following limitations before you migrate devices:

- Offboarding isn't required to switch to streamlined connectivity. After you apply the updated onboarding package, reboot Windows devices or restart the Defender for Endpoint service on macOS and Linux devices.
- Windows 10 versions 1607, 1703, 1709, and 1803 don't support reonboarding. Offboard first and then onboard using the updated package. These versions also require a longer URL list.
- Devices that run the Microsoft Monitoring Agent (MMA) don't support streamlined connectivity and must continue to use standard connectivity.

> 
> Note
> 
> The Defender deployment tool can be used to deploy Defender endpoint security on Windows and Linux devices. The tool is a lightweight, self-updating application that streamlines the deployment process. For more information, see [Deploy Microsoft Defender endpoint security to Windows devices using the Defender deployment tool](/en-us/defender-endpoint/defender-deployment-tool-windows) and [Deploy Microsoft Defender endpoint security to Linux devices using the Defender deployment tool (preview)](/en-us/defender-endpoint/linux-install-with-defender-deployment-tool).

## Migrate devices to streamlined connectivity

Use the platform-specific procedures in this section to migrate existing devices from standard connectivity to streamlined connectivity.

### Plan the migration

Before you migrate devices:

- **Plan a gradual rollout**: Begin with a small set of devices. Expand the rollout after you verify that the test devices use streamlined connectivity.
- **Use supported management tools**: For managed devices, use deployment methods such as Intune, Configuration Manager, Group Policy, Jamf Pro, or another supported management tool.
- **Test cloud connectivity**: Confirm that devices can communicate with Defender for Endpoint services. For more information, see [Verify client connectivity to Microsoft Defender for Endpoint service URLs](verify-connectivity).
- **Prepare a rollback plan**: Keep the standard connectivity destinations available during the migration. If problems occur, reapply the standard connectivity onboarding package.
- **Validate migration success**: Verify that devices use streamlined connectivity before you remove the standard core service destinations from your firewall or proxy configuration. Continue to allow supporting service destinations required for the operating system, updates, certificate validation, and your deployment and security features. For more information, see [Onboarding devices using streamlined connectivity](configure-device-connectivity).

### Restart devices or services after reonboarding

After you apply the streamlined onboarding package, complete the action for the device operating system:

- **Windows**: Reboot the device.
- **macOS**: Reboot the device, or restart the Defender for Endpoint service:

    ```bash
    sudo launchctl unload /Library/LaunchDaemons/com.microsoft.fresno.plist
    sudo launchctl load /Library/LaunchDaemons/com.microsoft.fresno.plist
    ```
- **Linux**: Reboot the device, or restart the Defender for Endpoint service:

    ```bash
    sudo systemctl restart mdatp
    ```

# [Windows 10 and 11](#tab/windows10and11)
Use the following options to migrate Windows 10 and Windows 11 devices to the streamlined connectivity method.

### Migrate Windows 10 and Windows 11 devices

Important

Windows 10 versions 1607, 1703, 1709, and 1803 don't support reonboarding. To migrate existing devices, you need to fully offboard and onboard using the streamlined onboarding package.

For general information, see [Onboard Windows client devices](onboard-client).

Confirm that the devices meet the [streamlined connectivity prerequisites](configure-device-connectivity#prerequisites).

### Migrate devices using a local script

Follow the guidance in [Onboard Windows devices using a local script](configure-endpoints-script) with the streamlined onboarding package. After you apply the package, reboot the device.

### Migrate devices using Group Policy

Follow the guidance in [Onboard Windows devices using Group Policy](configure-endpoints-gp) with the streamlined onboarding package. After you apply the policy, reboot the device.

### Migrate devices using Microsoft Intune

> 
> Microsoft Intune is the recommended tool for configuring and distributing Defender for Endpoint features to devices. However, Intune is a separate product that isn't part of Defender for Endpoint, and it isn't included in all subscriptions. To use Intune, you need a subscription that includes it, or you can buy it separately as a standalone subscription or add-on. If you don't have Intune, you can use any of the other methods in this article. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).

Follow the guidance in [Update the onboarding state for a Windows device](/en-us/intune/intune-service/protect/endpoint-security-edr-policy#updating-the-onboarding-state-for-a-device) with the streamlined onboarding package. The **Auto from connector** option doesn't automatically reapply the onboarding package to existing devices. Create a new onboarding policy, assign it to a test group, and confirm that the devices receive the policy. After you apply the policy, reboot the devices.

### Migrate devices using Microsoft Configuration Manager

Follow the guidance in [Update onboarding information for existing devices](/en-us/intune/configmgr/protect/deploy-use/defender-advanced-threat-protection#bkmk_updateatp) to deploy the streamlined onboarding package.

### Migrate VDI devices using the streamlined method

Follow the guidance in [Onboard nonpersistent virtual desktop infrastructure (VDI) devices](configure-endpoints-vdi) with the streamlined onboarding package. After you apply the package, reboot the device.

# [Windows Server](#tab/Windowsserver)
Use the following options to migrate Windows Server devices to the streamlined connectivity method.

### Migrate Windows Server devices

For general information on onboarding Windows server devices, see [Onboard Windows servers to the Microsoft Defender for Endpoint service](onboard-server).

Confirm that the devices meet the [streamlined connectivity prerequisites](configure-device-connectivity#prerequisites).

### Migrate devices with Microsoft Defender for Cloud

Devices already onboarded through Microsoft Defender for Cloud don't reonboard automatically. To migrate existing servers, deploy the streamlined onboarding package by using a supported method for the server operating system. For more information, see [Onboard Windows servers to the Microsoft Defender for Endpoint service](onboard-server).

### Migrate Windows Server devices using Microsoft Configuration Manager

Follow the guidance in [Update onboarding information for existing devices](/en-us/intune/configmgr/protect/deploy-use/defender-advanced-threat-protection#bkmk_updateatp) to deploy a policy that contains the streamlined onboarding package.

### Migrate Windows Server devices using Group Policy

Follow the guidance in [Onboard Windows devices using Group Policy](configure-endpoints-gp) with the streamlined onboarding package. After you apply the policy, reboot the server.

### Migrate Windows Server VDI devices

Follow the guidance in [Onboard nonpersistent virtual desktop infrastructure (VDI) devices](configure-endpoints-vdi) with the streamlined onboarding package. After you apply the package, reboot the server.

# [macOS](#tab/macOS)
Use the following options to migrate macOS devices to the streamlined connectivity method.

### Migrate macOS devices

For general information on onboarding macOS devices, see [Microsoft Defender for Endpoint on macOS](microsoft-defender-endpoint-mac).

Confirm that the devices meet the [streamlined connectivity prerequisites](configure-device-connectivity#prerequisites).

### Migrate macOS devices manually

Download the manual streamlined onboarding package, `WindowsDefenderATPOnboardingPackage.zip`. Extract `WindowsDefenderATPOnboarding.mobileconfig`, and follow the onboarding steps in [Deploy Microsoft Defender for Endpoint on macOS manually](mac-install-manually).

After you install the updated configuration profile, reboot the device or restart the Defender for Endpoint service.

### Migrate macOS devices using Microsoft Intune

To migrate macOS devices with Intune:

1. Download `GatewayWindowsDefenderATPOnboardingPackage.zip`, and extract `intune/WindowsDefenderATPOnboarding.xml`.
2. Create a new [custom configuration profile](mac-install-with-intune#step-14-deploy-the-microsoft-defender-for-endpoint-onboarding-package-for-macos), and upload `WindowsDefenderATPOnboarding.xml`. Don't assign the profile yet.
3. Exclude the test devices from the assignment for the existing standard connectivity onboarding profile. For more information, see [Exclude groups from a policy assignment](/en-us/intune/intune-service/configuration/device-profile-assign#exclude-groups-from-a-policy-assignment).
4. Assign the new streamlined connectivity onboarding profile to the test devices, and confirm that Intune reports a successful deployment.
5. Reboot the devices or restart the Defender for Endpoint service.

### Migrate macOS devices with Jamf Pro

> 
> Jamf Pro is a separate third-party product that isn't part of Defender for Endpoint and isn't included with Defender for Endpoint subscriptions. To use Jamf Pro, your organization needs a separate Jamf Pro subscription. For product and subscription information, see [Jamf Pro](https://www.jamf.com/products/jamf-pro/). If your organization doesn't use Jamf Pro, use another configuration method in this article, if available.

To migrate macOS devices with Jamf Pro:

1. Download `GatewayWindowsDefenderATPOnboardingPackage.zip`, and extract `jamf/WindowsDefenderATPOnboarding.plist`.
2. [Create a configuration profile in Jamf Pro](mac-jamfpro-policies#step-2-create-a-configuration-profile-in-jamf-pro-using-the-onboarding-package), and upload `WindowsDefenderATPOnboarding.plist` to the `com.microsoft.wdav.atp` preference domain. Don't assign the profile yet.
3. Exclude the test devices from the scope of the existing standard connectivity onboarding profile.
4. Add the test devices to the scope of the new streamlined connectivity onboarding profile, and confirm that Jamf Pro reports a successful deployment.
5. Reboot the devices or restart the Defender for Endpoint service.

For more Jamf Pro guidance, see [Deploy Microsoft Defender for Endpoint on macOS with Jamf Pro](mac-install-with-jamf).

# [Linux](#tab/linux)
### Migrate Linux devices

For general information on onboarding Linux devices, see [Microsoft Defender for Endpoint on Linux](microsoft-defender-endpoint-linux).

Confirm that the devices meet the [streamlined connectivity prerequisites](configure-device-connectivity#prerequisites).

### Migrate Linux devices using a local script

Follow the guidance in [Deploy Microsoft Defender for Endpoint on Linux manually](linux-install-manually) with the streamlined onboarding package. After you apply the package, reboot the device or restart the Defender for Endpoint service.

### Third-party Linux deployment tools (Puppet, Ansible, Chef)

Replace the onboarding package in your existing Puppet, Ansible, or Chef deployment configuration with the streamlined onboarding package. After you deploy the package, reboot the device or restart the Defender for Endpoint service.

---

## Verify migrated device connectivity

Use the following methods to confirm that migrated devices use streamlined connectivity.

### Use the Client Analyzer on Windows

Run the Microsoft Defender for Endpoint Client Analyzer on a migrated Windows device to confirm that the device connects to the streamlined destinations. The analyzer automatically uses the onboarding package configured on the device. For instructions, see [Run the client analyzer on Windows](run-analyzer-windows) and [Verify client connectivity to Microsoft Defender for Endpoint service URLs](verify-connectivity).

### Track connectivity type with advanced hunting

Use advanced hunting in the Microsoft Defender portal to view the connectivity type that devices report in the `DeviceInfo` table:

- **Column name**: `ConnectivityType`.
- **Possible values**: Blank, `Streamlined`, or `Standard`.
- **Data type**: String.
- **Description**: The type of connectivity from the device to the Defender for Endpoint cloud service.

After a migrated device establishes communication with the EDR command-and-control channel, the value is `Streamlined`. If you reapply a standard onboarding package, the value changes to `Standard`. The value remains blank for devices that haven't attempted to reonboard.

Use the advanced hunting queries later in this article to review individual devices and deployment totals. For the schema, see [DeviceInfo table](/en-us/defender-xdr/advanced-hunting-deviceinfo-table).

### Track connectivity locally in Windows Event Viewer

Use the SENSE operational log in Windows Event Viewer to confirm that a Windows device connects to a streamlined destination.

1. Select **Start**, type `Event Viewer`, and press **Enter**.
2. Under **Log Summary**, double-click **Microsoft-Windows-SENSE/Operational**.

    ![Screenshot of the SENSE operational log in Event Viewer.](media/log-summary-event-viewer.png)

    You can also expand **Applications and Services Logs** &gt; **Microsoft** &gt; **Windows** &gt; **SENSE**, and then select **Operational**.
3. Find event ID 4, which records a successful connection to a Defender for Endpoint processing server. Confirm that the contacted server uses the `endpoint.security.microsoft.com` domain. For example:

    ```xml
    Contacted server 6 times, all succeeded, URI: <region>.<geo>.endpoint.security.microsoft.com.
    <EventData>
     <Data Name="UInt1">6</Data>
     <Data Name="Message1">https://<region>.<geo>.endpoint.security.microsoft.com>
    </EventData>
    ```
4. Review event ID 5 for connection errors.

Note

SENSE is the internal name of the behavioral sensor that powers Defender for Endpoint. For more information about the events that the service records, see [Review events and errors using Event Viewer](event-error-codes).

### Run optional Windows feature tests

After migration, confirm that the device continues to appear in Device Inventory with the same device ID. Review the device timeline to confirm that events continue to arrive.

#### Test Live Response connectivity

Start a [live response session](respond-machine-alerts#initiate-live-response-session) on a test device, and run a basic command to confirm that the session is responsive. For more information, see [Investigate entities on devices using live response](live-response).

#### Test automated investigation and response connectivity

Confirm that the device meets the requirements for automated investigation and response. For more information, see [Configure automated investigation and response capabilities](/en-us/defender-xdr/m365d-configure-auto-investigation-response).

#### Test cloud-delivered protection connectivity

Verify cloud-delivered protection connectivity on a Windows test device.

In an elevated Command Prompt (a Command Prompt window you opened by selecting **Run as administrator**), run the following commands:

Tip

The first command changes the directory to the latest version of &lt;antimalware platform version&gt; in `%ProgramData%\Microsoft\Windows Defender\Platform\<antimalware platform version>`. If that path doesn't exist, it goes to `%ProgramFiles%\Windows Defender`.

```dos
(set "_done=" & if exist "%ProgramData%\Microsoft\Windows Defender\Platform\" (for /f "delims=" %d in ('dir "%ProgramData%\Microsoft\Windows Defender\Platform" /ad /b /o:-n 2^>nul') do if not defined _done (cd /d "%ProgramData%\Microsoft\Windows Defender\Platform\%d" & set _done=1)) else (cd /d "%ProgramFiles%\Windows Defender")) >nul 2>&1

MpCmdRun.exe -ValidateMapsConnection
```

For more information about MpCmdRun, see [Configure and manage Microsoft Defender Antivirus with the MpCmdRun command-line tool](command-line-arguments-microsoft-defender-antivirus).

#### Test block at first sight

Follow the block at first sight (BAFS) demonstration instructions in [Defender for Endpoint demonstrations](defender-endpoint-demonstrations).

#### Test SmartScreen

Follow the SmartScreen demonstration instructions on the [Microsoft Defender SmartScreen Demo (msft.net)](https://demo.smartscreen.msft.net/) page.

### PowerShell detection test

1. On the Windows device, create a folder: `C:\test-MDATP-test`.
2. Open Command Prompt as an administrator.
3. In the Command Prompt window, run the following PowerShell command:

    ```powershell
    powershell.exe -NoExit -ExecutionPolicy Bypass -WindowStyle Hidden $ErrorActionPreference = 'silentlycontinue';(New-Object System.Net.WebClient).DownloadFile('http://127.0.0.1/1.exe', 'C:\\test-MDATP-test\\invoice.exe');Start-Process 'C:\\test-MDATP-test\\invoice.exe'
    ```

If the command runs successfully and the test file executes, the Windows EDR detection test is complete and a new alert appears in the Microsoft Defender portal within a few minutes. For more information, see [Run an EDR detection test](edr-detection).

### Test connectivity on macOS and Linux

Run the following command to confirm that `edr_partner_geo_location` is available. The value should use the format `GW_<geo>`, where `<geo>` is the geographic location of your organization:

```bash
mdatp health --details edr
```

Run the connectivity test, and confirm that the results include the `endpoint.security.microsoft.com` domain:

```bash
mdatp connectivity test
```

Expect two results for `/storage`, and one result each for `/mdav`, `/xplat`, and `/packages`. For example: `https://mdav.us.endpoint.security.microsoft.com/storage`.

### Query connectivity type for migrated devices

Run the following query to list onboarded devices and show the most recent connectivity type reported for each device:

```kusto
DeviceInfo
| where OnboardingStatus == "Onboarded"
| summarize arg_max(Timestamp, ConnectivityType) by DeviceName
```

Run the following query to count onboarded devices by operating system and connectivity type:

```kusto
DeviceInfo
| where OnboardingStatus == "Onboarded"
| summarize arg_max(Timestamp, ConnectivityType, OSPlatform) by DeviceName
| summarize count() by OSPlatform, ConnectivityType
| render columnchart
```

### Use the Client Analyzer on macOS and Linux

Run the XMDE Client Analyzer to collect connectivity and health diagnostics. Use the procedure for the device operating system:

- [Run the client analyzer on macOS](run-analyzer-macos).
- [Run the client analyzer on Linux](run-analyzer-linux).