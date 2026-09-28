---
layout: Conceptual
title: Troubleshoot Microsoft Defender for Endpoint onboarding issues - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-onboarding
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Troubleshoot issues that might arise during the onboarding of devices or to the Microsoft Defender for Endpoint service.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.topic: troubleshooting
ms.subservice: onboard
ms.date: 2025-01-15T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 0c411ca5-dcda-85ae-5913-82349f2a9aff
document_version_independent_id: 0c411ca5-dcda-85ae-5913-82349f2a9aff
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/troubleshoot-onboarding.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: troubleshoot-onboarding
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/troubleshoot-onboarding.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: e3f62f3c-9456-6349-27ed-df7f6280093f
---

# Troubleshoot Microsoft Defender for Endpoint onboarding issues - Microsoft Defender for Endpoint | Microsoft Learn

You might need to troubleshoot the Microsoft Defender for Endpoint onboarding process if you encounter issues. This article provides detailed steps to troubleshoot onboarding issues that might occur when deploying with one of the deployment tools and common errors that might occur on the devices.

Before you start troubleshooting issues with onboarding tools, it's important to check if the minimum requirements are met for onboarding devices to the services. [Learn about the licensing, hardware, and software requirements to onboard devices to the service](minimum-requirements).

Tip

As a companion to this article, see our [Microsoft Defender for Endpoint setup guide](https://go.microsoft.com/fwlink/p/?linkid=2268087) to review best practices and learn about essential tools such as attack surface reduction and next-generation protection. For a customized experience based on your environment, you can access the Defender for [Endpoint automated setup guide](https://go.microsoft.com/fwlink/p/?linkid=2268088) in the Microsoft 365 admin center.

## Prerequisites

### Supported operating systems

- Windows Server 2012 R2 and later

## Troubleshoot issues with onboarding tools

If you've completed the onboarding process and don't see devices in the [Devices list](investigate-machines) after an hour, it might indicate an onboarding or connectivity problem.

### Troubleshoot onboarding when deploying with Group Policy

Deployment with Group Policy is done by running the onboarding script on the devices. The Group Policy console doesn't indicate if the deployment has succeeded or not.

If you've completed the onboarding process and don't see devices in the [Devices list](investigate-machines) after an hour, you can check the output of the script on the devices. For more information, see Troubleshoot onboarding when deploying with a script.

If the script completes successfully, see Troubleshoot onboarding issues on the devices for additional errors that might occur.

### Troubleshoot onboarding issues when deploying with Microsoft Configuration Manager

### Troubleshoot onboarding when deploying with a script

Tip

In Microsoft Configuration Manager version 1606 (July 2016) or later, you're no longer required to onboard devices using a local script. Instead, you can deploy onboarding configuration files via applications or endpoint protection policies. You can still use local scripts for manual device onboarding of a small number of devices.

You can track the deployment in the Configuration Manager Console. If the deployment fails, you can check the output of the script on the devices.

If the onboarding completed successfully but the devices aren't showing up in the **Devices list** after one hour, see Troubleshoot onboarding issues on the device for additional errors that might occur.

**Check the result of the script on the device:**

1. Click **Start**, type **Event Viewer**, and press **Enter**.
2. Go to **Windows Logs** &gt; **Application**.
3. Look for an event from **WDATPOnboarding** event source.

If the script fails and the event is an error, you can check the event ID in the following table to help you troubleshoot the issue.

Note

The following event IDs are specific to the onboarding script only.

| Event ID | Error Type | Resolution steps |
| --- | --- | --- |
| `5` | Offboarding data was found but couldn't be deleted | Check the permissions on the registry, specifically <br>`HKLM\SOFTWARE\Policies\Microsoft\Windows Advanced Threat Protection`. |
| `10` | Onboarding data couldn't be written to registry | Check the permissions on the registry, specifically <br>`HKLM\SOFTWARE\Policies\Microsoft\Windows Advanced Threat Protection`. <br><br> Verify that the script has been run as an administrator. |
| `15` | Failed to start SENSE service | Check the service health (`sc query sense` command). Make sure it's not in an intermediate state (*'Pending\_Stopped'*, *'Pending\_Running'*) and try to run the script again (with administrator rights). <br> If the device is running Windows 10, version 1607 and running the command `sc query sense` returns `START_PENDING`, reboot the device. If rebooting the device doesn't address the issue, upgrade to KB4015217 and try onboarding again. |
| `15` | Failed to start SENSE service | If the message of the error is: System error 577 or error 1058 has occurred, you need to enable the Microsoft Defender Antivirus ELAM driver, see Ensure that Microsoft Defender Antivirus is not disabled by a policy for instructions. |
| `15` | Failed to start SENSE service | The SENSE Feature on Demand (FoD) may not be installed. To determine whether it is installed, enter the following command from an Admin CMD/PowerShell prompt: `DISM.EXE /Online /Get-CapabilityInfo /CapabilityName:Microsoft.Windows.Sense.Client~~~~` If it returns an error or the state is not "Installed," then the SENSE FoD must be installed. See [Available Features on Demand: SENSE Client for Microsoft Defender for Endpoint](/en-us/windows-hardware/manufacture/desktop/features-on-demand-non-language-fod?view=windows-11&amp;preserve-view=true) for installation instructions. |
| `30` | The script failed to wait for the service to start running | The service could have taken more time to start or has encountered errors while trying to start. For more information on events and errors related to SENSE, see [Review events and errors using Event viewer](event-error-codes). |
| `35` | The script failed to find needed onboarding status registry value | When the SENSE service starts for the first time, it writes onboarding status to the registry location <br>`HKLM\SOFTWARE\Microsoft\Windows Advanced Threat Protection\Status`. <br><br> The script failed to find it after several seconds. You can manually test it and check if it's there. For more information on events and errors related to SENSE, see [Review events and errors using Event viewer](event-error-codes). |
| `40` | SENSE service onboarding status isn't set to **1** | The SENSE service has failed to onboard properly. For more information on events and errors related to SENSE, see [Review events and errors using Event viewer](event-error-codes). |
| `65` | Insufficient privileges | Run the script again with administrator privileges. |
| `70` | Offboarding script is for a different organization | Get an offboarding script for the correct organization that the SENSE service is onboarded to. |

### Troubleshoot onboarding issues using Microsoft Intune

You can use Microsoft Intune to check error codes and attempt to troubleshoot the cause of the issue.

If you have configured policies in Intune and they aren't propagated on devices, you might need to configure automatic MDM enrollment.

Use the following tables to understand the possible causes of issues while onboarding:

- Microsoft Intune error codes and OMA-URIs table
- Known issues with non-compliance table
- Mobile Device Management (MDM) event logs table

If none of the event logs and troubleshooting steps work, download the Local script from the **Device management** section of the portal, and run it in an elevated command prompt.

#### Microsoft Intune error codes and OMA-URIs

| Error Code Hex | Error Code Dec | Error Description | OMA-URI | Possible cause and troubleshooting steps |
| --- | --- | --- | --- | --- |
| 0x87D1FDE8 | -2016281112 | Remediation failed | Onboarding <br> Offboarding | **Possible cause:** Onboarding or offboarding failed on a wrong blob: wrong signature or missing PreviousOrgIds fields. <br>**Troubleshooting steps:**<br><br> Check the event IDs in the View agent onboarding errors in the device event log section. <br><br> Check the MDM event logs in the following table or follow the instructions in [Diagnose MDM failures in Windows](/en-us/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10). |
|  |  |  | Onboarding <br> Offboarding <br><br> SampleSharing | **Possible cause:** Microsoft Defender for Endpoint Policy registry key doesn't exist or the OMA DM client doesn't have permissions to write to it. <br>**Troubleshooting steps:** Ensure that the following registry key exists: `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Advanced Threat Protection`<br><br> If it doesn't exist, open an elevated command and add the key. |
|  |  |  | SenseIsRunning <br> OnboardingState <br><br> OrgId | **Possible cause:** An attempt to remediate by read-only property. Onboarding has failed. <br>**Troubleshooting steps:** Check the troubleshooting steps in Troubleshoot onboarding issues on the device. <br><br> Check the MDM event logs in the following table or follow the instructions in [Diagnose MDM failures in Windows](/en-us/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10). |
|  |  |  | All | **Possible cause:** Attempt to deploy Microsoft Defender for Endpoint on non-supported SKU/Platform, particularly Holographic SKU. <br> Currently supported platforms: <br><br> Enterprise, Education, and Professional.<br><br> Server isn't supported. |
| 0x87D101A9 | -2016345687 | SyncML(425): The requested command failed because the sender doesn't have adequate access control permissions (ACL) on the recipient. | All | **Possible cause:** Attempt to deploy Microsoft Defender for Endpoint on non-supported SKU/Platform, particularly Holographic SKU.<br> Currently supported platforms: <br><br> Enterprise, Education, and Professional. |

#### Known issues with non-compliance

The following table provides information on issues with non-compliance and how you can address the issues.

| Case | Symptoms | Possible cause and troubleshooting steps |
| --- | --- | --- |
| `1` | Device is compliant by SenseIsRunning OMA-URI. But is non-compliant by OrgId, Onboarding and OnboardingState OMA-URIs. | **Possible cause:** Check that user passed OOBE after Windows installation or upgrade. During OOBE onboarding couldn't be completed but SENSE is running already. <br>**Troubleshooting steps:** Wait for OOBE to complete. |
| `2` | Device is compliant by OrgId, Onboarding, and OnboardingState OMA-URIs, but is non-compliant by SenseIsRunning OMA-URI. | **Possible cause:** Sense service's startup type is set as "Delayed Start". Sometimes this causes the Microsoft Intune server to report the device as non-compliant by SenseIsRunning when DM session occurs on system start. <br>**Troubleshooting steps:** The issue should automatically be fixed within 24 hours. |
| `3` | Device is non-compliant | **Troubleshooting steps:** Ensure that Onboarding and Offboarding policies aren't deployed on the same device at same time. |

#### Mobile Device Management (MDM) event logs

View the MDM event logs to troubleshoot issues that might arise during onboarding:

Log name: Microsoft\Windows\DeviceManagement-EnterpriseDiagnostics-Provider

Channel name: Admin

| ID | Severity | Event description | Troubleshooting steps |
| --- | --- | --- | --- |
| 1819 | Error | Microsoft Defender for Endpoint CSP: Failed to Set Node's Value. NodeId: (%1), TokenName: (%2), Result: (%3). | Download the [Cumulative Update for Windows 10, 1607](https://go.microsoft.com/fwlink/?linkid=829760). |

## Troubleshoot onboarding issues on the device

If the deployment tools used do not indicate an error in the onboarding process, but devices are still not appearing in the devices list in an hour, go through the following verification topics to check if an error occurred with the Microsoft Defender for Endpoint agent.

- View agent onboarding errors in the device event log
- Ensure the diagnostic data service is enabled
- Ensure the service is set to start
- Ensure the device has an Internet connection
- Ensure that Microsoft Defender Antivirus is not disabled by a policy

### View agent onboarding errors in the device event log

1. Click **Start**, type **Event Viewer**, and press **Enter**.
2. In the **Event Viewer (Local)** pane, expand **Applications and Services Logs** &gt; **Microsoft** &gt; **Windows** &gt; **SENSE**.

    Note

    SENSE is the internal name used to refer to the behavioral sensor that powers Microsoft Defender for Endpoint.
3. Select **Operational** to load the log.
4. In the **Action** pane, click **Filter Current log**.
5. On the **Filter** tab, under **Event level:** select **Critical**, **Warning**, and **Error**, and click **OK**.

    [![The Event Viewer log filter](media/filter-log.png)](media/filter-log.png#lightbox)
6. Events which can indicate issues appear in the **Operational** pane. You can attempt to troubleshoot them based on the solutions in the following table:

    | Event ID | Message | Resolution steps |
    | --- | --- | --- |
    | `5` | Microsoft Defender for Endpoint service failed to connect to the server at *variable* | Ensure the device has Internet access. |
    | `6` | Microsoft Defender for Endpoint service isn't onboarded and no onboarding parameters were found. Failure code: *variable* | [Run the onboarding script again](configure-endpoints-script). |
    | `7` | Microsoft Defender for Endpoint service failed to read the onboarding parameters. Failure code: *variable* | Ensure the device has Internet access, then run the entire onboarding process again. |
    | `9` | Microsoft Defender for Endpoint service failed to change its start type. Failure code: variable | If the event happened during onboarding, reboot and re-attempt running the onboarding script. For more information, see [Run the onboarding script again](configure-endpoints-script). If the event happened during offboarding, contact support. |
    | `10` | Microsoft Defender for Endpoint service failed to persist the onboarding information. Failure code: variable | If the event happened during onboarding, re-attempt running the onboarding script. For more information, see [Run the onboarding script again](configure-endpoints-script). If the problem persists, contact support. |
    | `15` | Microsoft Defender for Endpoint can't start command channel with URL: *variable* | Ensure the device has Internet access. |
    | `17` | Microsoft Defender for Endpoint service failed to change the Connected User Experiences and Telemetry service location. Failure code: variable | [Run the onboarding script again](configure-endpoints-script). If the problem persists, contact support. |
    | `25` | Microsoft Defender for Endpoint service failed to reset health status in the registry. Failure code: *variable* | Contact support. |
    | `27` | Failed to enable Microsoft Defender for Endpoint mode in Windows Defender. Onboarding process failed. Failure code: variable | Contact support. |
    | `29` | Failed to read the offboarding parameters. Error type: %1, Error code: %2, Description: %3 | Ensure the device has Internet access, then run the entire offboarding process again. |
    | `30` | Failed to disable $(build.sense.productDisplayName) mode in Microsoft Defender for Endpoint. Failure code: %1 | Contact support. |
    | `32` | $(build.sense.productDisplayName) service failed to request to stop itself after offboarding process. Failure code: %1 | Verify that the service start type is manual and reboot the device. |
    | `55` | Failed to create the Secure ETW autologger. Failure code: %1 | Reboot the device. |
    | `63` | Updating the start type of external service. Name: %1, actual start type: %2, expected start type: %3, exit code: %4 | Identify what is causing changes in start type of mentioned service. If the exit code isn't 0, fix the start type manually to expected start type. |
    | `64` | Starting stopped external service. Name: %1, exit code: %2 | Contact support if the event keeps re-appearing. |
    | `68` | The start type of the service is unexpected. Service name: %1, actual start type: %2, expected start type: %3 | Identify what is causing changes in start type. Fix mentioned service start type. |
    | `69` | The service is stopped. Service name: %1 | Start the mentioned service. Contact support if the issue persists. |

There are additional components on the device that the Microsoft Defender for Endpoint agent depends on to function properly. If there are no onboarding related errors in the Microsoft Defender for Endpoint agent event log, proceed with the following steps to ensure that the additional components are configured correctly.

### Ensure the diagnostic data service is enabled

Note

In Windows 10 build 1809 and later, the Defender for Endpoint EDR service no longer has a direct dependency on the DiagTrack service. The EDR cyber evidence can still be uploaded if this service is not running.

If the devices aren't reporting correctly, you might need to check that the Windows diagnostic data service is set to automatically start and is running on the device. The service might have been disabled by other programs or user configuration changes.

First, you should check that the service is set to start automatically when Windows starts, then you should check that the service is currently running (and start it if it isn't).

### Ensure the service is set to start

**Use the command line to check the Windows diagnostic data service startup type**:

1. Open an elevated command-line prompt on the device:

    a. Click **Start**, type **cmd**, and press **Enter**.

    b. Right-click **Command prompt** and select **Run as administrator**.
2. Enter the following command, and press **Enter**:

    ```console
    sc qc diagtrack
    ```

    If the service is enabled, then the result should look like the following screenshot:

    [![The result of the sc query command for diagtrack](media/windefatp-sc-qc-diagtrack.png)](media/windefatp-sc-qc-diagtrack.png#lightbox)

    If the `START_TYPE` isn't set to `AUTO_START`, then you need to set the service to automatically start.

**Use the command line to set the Windows diagnostic data service to automatically start:**

1. Open an elevated command-line prompt on the device:

    a. Click **Start**, type **cmd**, and press **Enter**.

    b. Right-click **Command prompt** and select **Run as administrator**.
2. Enter the following command, and press **Enter**:

    ```console
    sc config diagtrack start=auto
    ```
3. A success message is displayed. Verify the change by entering the following command, and press **Enter**:

    ```console
    sc qc diagtrack
    ```
4. Start the service. In the command prompt, type the following command and press **Enter**:

    ```console
    sc start diagtrack
    ```

### Ensure the device has an Internet connection

The Microsoft Defender for Endpoint sensor requires Microsoft Windows HTTP (WinHTTP) to report sensor data and communicate with the Microsoft Defender for Endpoint service.

WinHTTP is independent of the Internet browsing proxy settings and other user context applications and must be able to detect the proxy servers that are available in your particular environment.

To ensure that sensor has service connectivity, follow the steps described in the [Verify client connectivity to Microsoft Defender for Endpoint service URLs](verify-connectivity) topic.

If the verification fails and your environment is using a proxy to connect to the Internet, then follow the steps described in [Configure proxy and Internet connectivity settings](configure-proxy-internet) topic.

### Ensure that Microsoft Defender Antivirus is not disabled by a policy

Important

The following only applies to devices that have **not** yet received the August 2020 (version 4.18.2007.8) update to Microsoft Defender Antivirus.

The update ensures that Microsoft Defender Antivirus cannot be turned off on client devices via system policy.

**Problem**: The Microsoft Defender for Endpoint service doesn't start after onboarding.

**Symptom**: Onboarding successfully completes, but you see error 577 or error 1058 when trying to start the service.

**Solution**: If your devices are running a third-party antimalware client, the Microsoft Defender for Endpoint agent needs the Early Launch Antimalware (ELAM) driver to be enabled. You must ensure that it's not turned off by a system policy.

- Depending on the tool that you use to implement policies, you need to verify that the following Windows Defender policies are cleared:

    - DisableAntiSpyware
    - DisableAntiVirus

    For example, in Group Policy there should be no entries such as the following values:

    - `<Key Path="SOFTWARE\Policies\Microsoft\Windows Defender"><KeyValue Value="0" ValueKind="DWord" Name="DisableAntiSpyware"/></Key>`
    - `<Key Path="SOFTWARE\Policies\Microsoft\Windows Defender"><KeyValue Value="0" ValueKind="DWord" Name="DisableAntiVirus"/></Key>`

Important

The `disableAntiSpyware` setting is discontinued and will be ignored on all Windows 10 devices, as of the August 2020 (version 4.18.2007.8) update to Microsoft Defender Antivirus.

- After clearing the policy, run the onboarding steps again.
- You can also check the previous registry key values to verify that the policy is disabled, by opening the registry key `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Defender`.

    [![The registry key for Microsoft Defender Antivirus](media/atp-disableantispyware-regkey.png)](media/atp-disableantispyware-regkey.png#lightbox)

    Note

    All Windows Defender services (`wdboot`, `wdfilter`, `wdnisdrv`, `wdnissvc`, and `windefend`) should be in their default state. Changing the startup of these services is unsupported and may force you to reimage your system. Example default configurations for `WdBoot` and `WdFilter`:

    - `<Key Path="SYSTEM\CurrentControlSet\Services\WdBoot"><KeyValue Value="0" ValueKind="DWord" Name="Start"/></Key>`
    - `<Key Path="SYSTEM\CurrentControlSet\Services\WdFilter"><KeyValue Value="0" ValueKind="DWord" Name="Start"/></Key>`

    If Microsoft Defender Antivirus is in passive mode, these drivers are set to manual (`0`).

## Troubleshoot onboarding issues on Windows Server 2016 and earlier versions of Windows Server.

If you encounter issues while onboarding a server, go through the following verification steps to address possible issues.

- Ensure Microsoft Monitoring Agent (MMA) is installed and configured to report sensor data to the service
- Ensure that the server proxy and Internet connectivity settings are configured properly
- See [Onboard Windows Server 2016 and Windows Server 2012 R2](onboard-server#onboard-windows-server-2016-and-windows-server-2012-r2)

You might also need to check the following:

- Check that there's a Microsoft Defender for Endpoint Service running in the **Processes** tab in **Task Manager**. For example:

    [![The process view with Microsoft Defender for Endpoint Service running](media/atp-task-manager.png)](media/atp-task-manager.png#lightbox)
- Check **Event Viewer** &gt; **Applications and Services Logs** &gt; **Operation Manager** to see if there are any errors.
- In **Services**, check if the **Microsoft Monitoring Agent** is running on the server. For example,

    [![The services](media/atp-services.png)](media/atp-services.png#lightbox)
- In **Microsoft Monitoring Agent** &gt; **Azure Log Analytics (OMS)**, check the Workspaces and verify that the status is running.

    [![The Microsoft Monitoring Agent Properties](media/atp-mma-properties.png)](media/atp-mma-properties.png#lightbox)
- Check to see that devices are reflected in the **Devices list** in the portal.

## Confirming onboarding of newly built devices

There may be instances when onboarding is deployed on a newly built device but not completed.

The steps in this article provide guidance for the following scenario:

- Onboarding package is deployed to newly built devices
- Sensor doesn't start because the Out-of-box experience (OOBE) or first user logon hasn't been completed
- Device is turned off or restarted before the end user performs a first logon
- In this scenario, the SENSE service won't start automatically even though onboarding package was deployed

Note

User Logon after OOBE is no longer required for SENSE service to start on the following or more recent Windows versions:

- Windows 10 version 1809 or later.
- Windows Server 2019 or later.
- Azure Stack HCI OS version 23H2 and later.

&lt;a name="troubleshoot-onboarding-with-microsoft-endpoint-configuration-manager"

## Troubleshoot onboarding with Microsoft Configuration Manager

Note

The following steps are only relevant when using Microsoft Configuration Manager. For more information about onboarding using Microsoft Configuration Manager, see [Microsoft Defender for Endpoint](/en-us/intune/configmgr/protect/deploy-use/windows-defender-advanced-threat-protection).

1. Create an application in Microsoft Configuration Manager.

    [![The Microsoft Configuration Manager configuration-1](media/mecm-1.png)](media/mecm-1.png#lightbox)
2. Select **Manually specify the application information**.

    [![The Microsoft Configuration Manager configuration-2](media/mecm-2.png)](media/mecm-2.png#lightbox)
3. Specify information about the application, then select **Next**.

    [![The Microsoft Configuration Manager configuration-3](media/mecm-3.png)](media/mecm-3.png#lightbox)
4. Specify information about the software center, then select **Next**.

    [![The Microsoft Configuration Manager configuration-4](media/mecm-4.png)](media/mecm-4.png#lightbox)
5. In **Deployment types** select **Add**.

    [![The Microsoft Configuration Manager configuration-5](media/mecm-5.png)](media/mecm-5.png#lightbox)
6. Select **Manually specify the deployment type information**, then select **Next**.

    [![The Microsoft Configuration Manager configuration-6](media/mecm-6.png)](media/mecm-6.png#lightbox)
7. Specify information about the deployment type, then select **Next**.

    [![The Microsoft Configuration Manager configuration-7](media/mecm-7.png)](media/mecm-7.png#lightbox)
8. In **Content** &gt; **Installation program** specify the command: `net start sense`.

    [![The Microsoft Configuration Manager configuration-8](media/mecm-8.png)](media/mecm-8.png#lightbox)
9. In **Detection method**, select **Configure rules to detect the presence of this deployment type**, then select **Add Clause**.

    [![The Microsoft Configuration Manager configuration-9](media/mecm-9.png)](media/mecm-9.png#lightbox)
10. Specify the following detection rule details, then select **OK**:

    [![The Microsoft Configuration Manager configuration-10](media/mecm-10.png)](media/mecm-10.png#lightbox)
11. In **Detection method** select **Next**.

    [![The Microsoft Configuration Manager configuration-11](media/mecm-11.png)](media/mecm-11.png#lightbox)
12. In **User Experience**, specify the following information, then select **Next**:

    [![The Microsoft Configuration Manager configuration-12](media/mecm-12.png)](media/mecm-12.png#lightbox)
13. In **Requirements**, select **Next**.

    [![The Microsoft Configuration Manager configuration-13](media/mecm-13.png)](media/mecm-13.png#lightbox)
14. In **Dependencies**, select **Next**.

    [![The Microsoft Configuration Manager configuration-14](media/mecm-14.png)](media/mecm-14.png#lightbox)
15. In **Summary**, select **Next**.

    [![The Microsoft Configuration Manager configuration-15](media/mecm-15.png)](media/mecm-15.png#lightbox)
16. In **Completion**, select **Close**.

    [![The Microsoft Configuration Manager configuration-16](media/mecm-16.png)](media/mecm-16.png#lightbox)
17. In **Deployment types**, select **Next**.

    [![The Microsoft Configuration Manager configuration-17](media/mecm-17.png)](media/mecm-17.png#lightbox)
18. In **Summary**, select **Next**.

    [![The Microsoft Configuration Manager configuration-18](media/mecm-18.png)](media/mecm-18.png#lightbox)

    The status is then displayed: [![The Microsoft Configuration Manager configuration-19](media/mecm-19.png)](media/mecm-19.png#lightbox)
19. In **Completion**, select **Close**.

    [![The Microsoft Configuration Manager configuration-20](media/mecm-20.png)](media/mecm-20.png#lightbox)
20. You can now deploy the application by right-clicking the app and selecting **Deploy**.

    [![The Microsoft Configuration Manager configuration-21](media/mecm-21.png)](media/mecm-21.png#lightbox)
21. In **General** select **Automatically distribute content for dependencies** and **Browse**.

    [![The Microsoft Configuration Manager configuration-22](media/mecm-22.png)](media/mecm-22.png#lightbox)
22. In **Content** select **Next**. [![The Microsoft Configuration Manager configuration-23](media/mecm-23.png)](media/mecm-23.png#lightbox)
23. In **Deployment settings**, select **Next**.

    [![The Microsoft Configuration Manager configuration-24](media/mecm-24.png)](media/mecm-24.png#lightbox)
24. In **Scheduling** select **As soon as possible after the available time**, then select **Next**.

    [![The Microsoft Configuration Manager configuration-25](media/mecm-25.png)](media/mecm-25.png#lightbox)
25. In **User experience**, select **Commit changes at deadline or during a maintenance window (requires restarts)**, then select **Next**. [![The Microsoft Configuration Manager configuration-26](media/mecm-26.png)](media/mecm-26.png#lightbox)
26. In **Alerts** select **Next**.

    [![The Microsoft Configuration Manager configuration-27](media/mecm-27.png)](media/mecm-27.png#lightbox)
27. In **Summary**, select **Next**. [![The Microsoft Configuration Manager configuration-28](media/mecm-28.png)](media/mecm-28.png#lightbox)

    The status is then displayed [![The Microsoft Configuration Manager configuration-29](media/mecm-29.png)](media/mecm-29.png#lightbox)
28. In **Completion**, select **Close**.

    [![The Microsoft Configuration Manager configuration-30](media/mecm-30.png)](media/mecm-30.png#lightbox)