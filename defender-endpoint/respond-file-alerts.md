---
layout: Conceptual
title: Take response actions on a file in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/respond-file-alerts
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Take response actions on file-related alerts by stopping and quarantining a file or blocking a file and checking activity details.
ms.service: defender-endpoint
ms.author: chrisda
author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
- mde-edr
ms.topic: how-to
ms.subservice: edr
ms.date: 2026-07-02T00:00:00.0000000Z
ms.custom: sfi-ga-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: ab3aacf2-5672-9b2a-f3ff-2a62a111c900
document_version_independent_id: ab3aacf2-5672-9b2a-f3ff-2a62a111c900
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/respond-file-alerts.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: respond-file-alerts
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/respond-file-alerts.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/e0ffb20c-01c6-407b-a9bd-29111652a1dc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/3904bce4-d817-48cf-85fd-b6146fca83b7
platformId: 7874b5f6-7ddf-3bf8-b29e-e23a288dc87f
---

# Take response actions on a file in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

Quickly respond to detected attacks by stopping and quarantining files or blocking a file. After taking action on files, you can check on activity details in the Action center.

Response actions are available on a file's detailed profile page. Once on this page, you can switch between the new and old page layouts by toggling **new File page**. The following sections describe the newer page layout.

Response actions run along the top of the file page, and include:

- Stop and quarantine file
- Manage indicator
- Download file
- Collect file
- Ask Defender Experts
- Manual actions
- Go hunt
- Deep analysis

Note

If you're using Defender for Endpoint Plan 1, you can take certain response actions manually. For more information, see [Manual response actions](defender-endpoint-plan-1#manual-response-actions).

You can also submit files for deep analysis, to run the file in a secure cloud sandbox. When the analysis is complete, you get a detailed report that provides information about the behavior of the file. You can submit files for deep analysis and read past reports by selecting the **Deep analysis** action.

Some actions require certain permissions. The following table describes what action certain permissions can take on portable executable (PE) and non-PE files:

| Permission | PE files | Non-PE files |
| --- | --- | --- |
| View data | X | X |
| Alerts investigation | ☑ | X |
| Live response basic | X | X |
| Live response advanced | ☑ | ☑ |

For more information on roles, see [Create and manage roles for role-based access control](user-roles).

Important

Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

## Stop and quarantine files in your network

You can contain an attack in your organization by stopping the malicious process and quarantining the file where it was observed.

Important

You can only take the **Stop and Quarantine File** action if:

- The device you're taking the action on is running Windows 10, version 1703 or later, Windows 11, and Windows Server 2012 R2+
- The file does not belong to trusted non-Microsoft publishers or is not signed by Microsoft
- Microsoft Defender Antivirus must at least be running on Passive mode. For more information, see [Microsoft Defender Antivirus compatibility](microsoft-defender-antivirus-compatibility).

The **Stop and Quarantine File** action includes stopping running processes, quarantining the files, and deleting persistent data such as registry keys.

The **Stop and Quarantine File** action takes effect on devices with Windows 10, version 1703 or later, and Windows 11 and Windows Server 2012 R2 or later, where the file was observed in the last 30 days.

Note

You'll be able to restore the file from quarantine at any time.

### Stop and quarantine files

1. Select the file you want to stop and quarantine. You can select a file from any of the following views or use the Search box:

    - **Alerts** - select the corresponding links from the Description or Details in the Alert Story timeline
    - **Search box** - select **File** from the drop-down menu and enter the file name

    Note

    The stop and quarantine file action is limited to a maximum of 1000 devices. To stop a file on a larger number of devices, see Add indicator to block or allow file. The Stop and quarantine action has a maximum timeout period of 3 days. If the targeted device remains offline for longer than this period after the action is initiated, the action will not be delivered to that device. To ensure the file remains blocked beyond the timeout or after the action completes, it's recommended to create an indicator to block the file explicitly.
2. Go to the top bar and select **Stop and Quarantine File**.

    [![The stop and quarantine file action](media/atp-stop-quarantine-file.png)](media/atp-stop-quarantine-file.png#lightbox)
3. Specify a reason, then select **Confirm**.

    [![The stop and quarantine file page](media/atp-stop-quarantine.png)](media/atp-stop-quarantine.png#lightbox)

    The Action center shows the submission information:

    [![The stop and quarantine file action center](media/atp-stopnquarantine-file.png)](media/atp-stopnquarantine-file.png#lightbox)

    - **Submission time** - Shows when the action was submitted.
    - **Success** - Shows the number of devices where the file was stopped and quarantined.
    - **Failed** - Shows the number of devices where the action failed and details about the failure.
    - **Pending** - Shows the number of devices where the file is yet to be stopped and quarantined from. This can take time for cases when the device is offline or not connected to the network.
4. Select any of the status indicators to view more information about the action. For example, select **Failed** to see where the action failed.

#### Notification on device user

When the file is being removed from a device, the following notification is shown:

[![The notification a on device user](media/atp-notification-file.png)](media/atp-notification-file.png#lightbox)

In the device timeline, a new event is added for each device where a file was stopped and quarantined.

A warning is shown before the action is implemented for files widely used throughout an organization. This warning helps validate that the operation is intended.

## Restore file from quarantine

You can roll back and remove a file from quarantine if you've determined that it's clean after an investigation. Run the following command on each device where the file was quarantined.

In an elevated Command Prompt (a Command Prompt window you opened by selecting **Run as administrator**), run the following commands:

Tip

The first command changes the directory to the latest version of &lt;antimalware platform version&gt; in `%ProgramData%\Microsoft\Windows Defender\Platform\<antimalware platform version>`. If that path doesn't exist, it goes to `%ProgramFiles%\Windows Defender`.

```dos
(set "_done=" & if exist "%ProgramData%\Microsoft\Windows Defender\Platform\" (for /f "delims=" %d in ('dir "%ProgramData%\Microsoft\Windows Defender\Platform" /ad /b /o:-n 2^>nul') do if not defined _done (cd /d "%ProgramData%\Microsoft\Windows Defender\Platform\%d" & set _done=1)) else (cd /d "%ProgramFiles%\Windows Defender")) >nul 2>&1

MpCmdRun.exe -Restore -Name EUS:Win32/CustomEnterpriseBlock -All
```

For more information about MpCmdRun, see [Configure and manage Microsoft Defender Antivirus with the MpCmdRun command-line tool](command-line-arguments-microsoft-defender-antivirus).

Note

In some scenarios, the **ThreatName** might appear as: `EUS:Win32/CustomEnterpriseBlock!cl`.

Defender for Endpoint restores all custom blocked files that were quarantined on this device in the last 30 days.

Files quarantined as a potential network threat might not be recoverable. This type of file might not be accessible in quarantine due to lack of network credentials or expired tokens from a temporary sign-in.

## Download or collect file

Selecting **Download file** from the response actions allows you to download a local, password-protected .zip archive containing your file. A flyout appears where you can record a reason for downloading the file, and set a password.

By default, you should be able to download files that are in quarantine.

The **Download file** button can have the following states:

- **Active** - You are able to collect the file.
- **Disabled** - If the button is grayed out or disabled during an active collection attempt, you might not have appropriate RBAC permissions to collect files. The following permissions are required:

    - Microsoft Defender Unified role-based access control (RBAC):
        - Add file collection permission in Microsoft Defender Unified (RBAC)
    - Microsoft Defender for Endpoint role-based access control (RBAC):
        - Portable Executable files (.exe, .sys, .dll, and others):
            - Security Administrator or Advanced live response or Alerts
        - Non-Portable Executable file (.txt, .docx, and others):
            - Security Administrator or Advanced live response
            - Tenants with [role-based access (RBAC) permissions](/en-us/defender-xdr/manage-rbac) enabled

[![The download file action](media/atp-download-file-action.png)](media/atp-download-file-action.png#lightbox)

Important

Starting February 16, 2025, new Microsoft Defender for Endpoint customers will only have access to the Unified Role-Based Access Control (URBAC). Existing customers keep their current roles and permissions. For more information, see [Unified Role-Based Access Control (URBAC) for Microsoft Defender for Endpoint](/en-us/defender-xdr/manage-rbac).

### Download quarantined files

Files that were quarantined by Microsoft Defender Antivirus or your security team are saved in a compliant way according to your [sample submission configurations](cloud-protection-configure). Your security team can download the files directly from the file's detail page via the "Download file" button. **The Download file feature is turned on by default**.

The location depends on your organization's geo settings (either EU, UK, or US). A quarantined file is collected only once per organization. Learn more about Microsoft's data protection from the Service Trust Portal at https://aka.ms/STP.

Having the **Download quarantined files** setting turned on can help security teams examine potentially bad files and investigate incidents quickly and in a less risky way. However, if you need to turn off this setting, go to **Settings** &gt; **Endpoints** &gt; **Advanced features** &gt; **Download quarantined files** to adjust the setting. For more information, see [Advanced features](advanced-features).

#### Backing up quarantined files

Users might be prompted to provide explicit consent before backing up the quarantined file, depending on your [sample submission configuration](cloud-protection-microsoft-antivirus-sample-submission#sample-submission-settings).

The **Download quarantined files** feature doesn't work if sample submission is turned off. If automatic sample submission is set to request permission from the user, only samples that the user agrees to send are collected.

Important

Download quarantined file requirements:

- Your organization uses Microsoft Defender Antivirus in active mode
- Antivirus engine version is 1.1.17300.4 or later. See [Monthly platform and engine versions](microsoft-defender-endpoint-releases#microsoft-defender-antivirus-releases)
- Cloud–based protection is enabled. See [Turn on cloud-delivered protection](cloud-protection-configure)
- Sample submission is turned on
- Client devices must be running Windows 11 or Windows 10, version 1703 or later
- Server devices must be running Windows Server 2016 and later or Azure Stack HCI OS, version 23H2 and later

### Collect files

If a file isn't already stored by Microsoft Defender for Endpoint, you can't download it. Instead, you see a **Collect file** button in the same location.

The **Collect file** button can have the following states:

- **Active** - You are able to collect the file.
- **Disabled** - If the button is grayed out or disabled during an active collection attempt, you might not have appropriate RBAC permissions to collect files.

    The following permissions are required:

    For Portable Executable file (.exe, .sys, .dll, and others)

    - Security Administrator or Advanced live response or Alerts

    Non-Portable Executable file (.txt, .docx, and others)

    - Security Administrator or Advanced live response

If a file hasn't been seen in the organization in the past 30 days, **Collect file** is disabled.

Important

A file that was quarantined as a potential network threat might not be recoverable. If a user attempts to restore the file after quarantine, that file might not be accessible. This can be due to the system no longer having network credentials to access the file. Typically, this is a result of a temporary log on to a system or shared folder and the access tokens expired.

## Add indicator to block or allow a file

Prevent further propagation of an attack in your organization by banning potentially malicious files or suspected malware. If you know a potentially malicious portable executable (PE) file, you can block it. Blocking the file prevents it from being read, written, or executed on devices in your organization.

Important

- The **Block or allow** feature is available if your organization uses Microsoft Defender Antivirus and Cloud-delivered protection is enabled. For more information, see [Manage cloud-delivered protection](deploy-manage-report-microsoft-defender-antivirus).
- The Anti-malware client version must be 4.18.1901.x or later.
- The **Block or allow** feature is designed to prevent suspected malware (or potentially malicious files) from being downloaded from the web. It supports portable executable (PE) files, including *.exe* and *.dll* files. Support for additional file types will be extended over time.
- The **Block or allow** response action is available for devices on Windows 10, version 1703 or later, and Windows 11.
- The allow or block function cannot be done on files if the file's classification exists on the device's cache prior to the allow or block action.

Note

The PE file needs to be in the device timeline for you to be able to take this action.

There may be a couple of minutes of latency between the time the action is taken and the actual file being blocked.

### Enable the block file feature

To start blocking files, you first need to [turn the **Block or allow** feature on](advanced-features) in Settings.

### Allow or block file

When you add an indicator hash for a file, you can choose to raise an alert and block the file whenever a device in your organization attempts to run it.

Files automatically blocked by an indicator don't show up in the file's Action center, but the alerts are still visible in the Alerts queue.

See [Overview of indicators](indicators-overview) for more details on blocking and raising alerts on files.

To stop blocking a file, remove the indicator. You can remove the indicator via the **Edit Indicator** action on the file's profile page. The **Edit Indicator** action is visible in the same position as the **Add Indicator** action, before you added the indicator.

You can also edit indicators from the **Settings** page, under **Rules** &gt; **Indicators**. Indicators are listed on the **Rules** &gt; **Indicators** page by their file's hash.

## Check activity details in Action center

The **Action center** provides information on actions that were taken on a device or file. You can view the following details:

- Investigation package collection
- Antivirus scan
- App restriction
- Device isolation

All other related details are also shown, such as submission date/time, submitting user, and if the action succeeded or failed.

[![The action center with information](media/action-center-details.png)](media/action-center-details.png#lightbox)

## Deep analysis

Cyber security investigations are typically triggered by an alert. Alerts are related to one or more observed files that are often new or unknown. Selecting a file takes you to the file view where you can see the file's metadata. To enrich the data related to the file, you can submit the file for deep analysis.

The Deep analysis feature executes a file in a secure, fully instrumented cloud environment. Deep analysis results show the file's activities, observed behaviors, and associated artifacts, such as dropped files, registry modifications, and communication with IPs. Deep analysis supports extensive analysis of portable executable (PE) files (including *.exe* and *.dll* files).

Deep analysis of a file takes several minutes. Once the file analysis is complete, the Deep Analysis tab updates to display a summary and the date and time of the latest available results.

The deep analysis summary includes a list of observed *behaviors*, some of which can indicate malicious activity, and *observables*, including contacted IPs and files created on the disk. If nothing was found, the Behaviors and Observables sections display a brief message.

Results of deep analysis are matched against threat intelligence and any matches generate appropriate alerts.

Use the deep analysis feature to investigate the details of any file, usually during an investigation of an alert or for any other reason where you suspect malicious behavior. The **Deep analysis** feature is available at the top of the file's page. Select the three dots to access the **Deep analysis** action.

[![Screenshot of the Deep analysis action](/en-us/defender/media/defender-endpoint/deep-analysis.png)](/en-us/defender/media/defender-endpoint/deep-analysis.png#lightbox)

Learn about deep analysis in the following video:

**Submit for deep analysis** is enabled when the file is available in the Defender for Endpoint backend sample collection, or if it was observed on a Windows 10 device that supports submitting to deep analysis.

Note

Only files from Windows 10, Windows 11, and Windows Server 2012 R2+ can be automatically collected.

You can also submit a sample through the [Microsoft Security Intelligence submission portal](https://www.microsoft.com/wdsi/filesubmission) if the file wasn't observed on a Windows 10 device (or Windows 11 or Windows Server 2012 R2+), and wait for **Submit for deep analysis** button to become available.

Note

Due to backend processing flows in the Microsoft Defender portal, there could be up to 10 minutes of latency between file submission and availability of the deep analysis feature in Defender for Endpoint.

### Submit files for deep analysis

To submit a file for deep analysis, use the following steps:

1. Select the file that you want to submit for deep analysis. You can select or search a file from any of the following views:

    - **Alerts** - select the file links from the **Description** or **Details** in the Alert Story timeline
    - **Devices list** - select the file links from the **Description** or **Details** in the **Device in organization** section
    - **Search box** - select **File** from the drop-down menu and enter the file name
2. In the **Deep analysis** tab of the file view, select **Submit**.

    [![The submit PE files button](media/submit-file.png)](media/submit-file.png#lightbox)

    Note

    Only PE files are supported, including *.exe* and *.dll* files. Additionally, Windows App Store Executables are unsupported.

    A progress bar is displayed and provides information on the different stages of the analysis. You can then view the report when the analysis is done.

Note

Depending on device availability, sample collection time can vary. There is a 3-hour timeout for sample collection. The collection will fail and the deep analysis submission will abort if there is no online Windows 10 device (or Windows 11 or Windows Server 2012 R2+) reporting at that time. You can re-submit files for deep analysis to get fresh data on the file.

### View deep analysis reports

View the provided deep analysis report to see more in-depth insights on the file you submitted. The deep analysis report is available in the file view context.

You can view the comprehensive report that provides details on the following sections:

- Behaviors
- Observables

The details provided can help you investigate if there are indications of a potential attack.

1. Select the file you submitted for deep analysis.
2. Select the **Deep analysis** tab. If there are any previous reports, the report summary appears in this tab.

    [![The deep analysis report showing detailed information across a number of categories](media/analysis-results-nothing500.png)](media/analysis-results-nothing500.png#lightbox)

#### Troubleshoot deep analysis

If you come across a problem when trying to submit a file, try each of the following troubleshooting steps.

1. Ensure that the file in question is a PE file. PE files typically have *.exe* or *.dll* extensions (executable programs or applications).
2. Ensure the service has access to the file, that it still exists, and hasn't been corrupted or modified.
3. Wait a short while and try to submit the file again. The queue may be full, or there was a temporary connection or communication error.
4. If the sample collection policy isn't configured, then the default behavior is to allow sample collection. If it's configured, then verify the policy setting allows sample collection before submitting the file again. When sample collection is configured, then check the following registry value:

    ```text
    Path: HKLM\SOFTWARE\Policies\Microsoft\Windows Advanced Threat Protection
    Name: AllowSampleCollection
    Type: DWORD
    Hexadecimal value :
      Value = 0 - block sample collection
      Value = 1 - allow sample collection
    ```
5. Change the organizational unit through the Group Policy. For more information, see [Configure with Group Policy](configure-endpoints-gp).
6. If these steps don't resolve the issue, contact support.