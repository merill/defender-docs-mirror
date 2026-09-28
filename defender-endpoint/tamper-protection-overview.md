---
layout: Conceptual
title: Tamper protection overview - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/tamper-protection-overview
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
ms.reviewer: joshbregman, mattcall, pahuijbr, hayhov, gberecz, ksarens
description: Learn how tamper protection prevents unauthorized changes on Windows and macOS devices and detects tampering on Linux devices in Preview.
ms.service: defender-endpoint
ms.localizationpriority: medium
ms.date: 2026-09-09T00:00:00.0000000Z
ms.topic: overview
author: limwainstein
ms.author: lwainstein
ms.custom:
- msecd-doc-authoring-1016
- nextgen
- admindeeplinkDEFENDER
ms.subservice: ngp
ms.collection:
- m365-security
- tier2
- mde-ngp
ai-usage: ai-assisted
locale: en-us
document_id: 7655a2b2-841b-5be4-1c56-c222c6472f77
document_version_independent_id: 7655a2b2-841b-5be4-1c56-c222c6472f77
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/tamper-protection-overview.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: tamper-protection-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/tamper-protection-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 8f3f8cc2-cd7f-e002-1e0a-e1b5d24bb49a
---

# Tamper protection overview - Microsoft Defender for Endpoint | Microsoft Learn

Tamper protection in Microsoft Defender for Endpoint helps protect important security settings from being disabled or changed. During cyberattacks, attackers often try to disable security features on devices to access data, install malware, and exploit data, identities, and devices.

Your security team can manage tamper protection for devices in your organization.

For answers to common questions, see [Frequently asked questions about tamper protection](tamper-protection-faq). For help with blocked settings and exclusion protection, see [Troubleshoot problems with tamper protection](tamper-protection-troubleshoot).

Note

[Controlled configuration](secure-controlled-configuration) builds on tamper protection. The existing tamper protection setting in management experiences is renamed to controlled configuration. The renamed setting doesn't automatically enable controlled configuration protections. Deploy a controlled configuration policy through Microsoft Intune or Microsoft Defender for Endpoint security settings management to enable them.

## Tamper protection modes

Tamper protection modes and protected settings differ among Windows, macOS, and Linux devices.

### Tamper protection modes on Windows devices

Tamper protection doesn't prevent you from *viewing* security settings or affect how non-Microsoft antivirus apps register with the Windows Security app. It continues to protect the Microsoft Defender Antivirus service and its features when Defender Antivirus runs in passive mode. For more information about active and passive modes, see [Microsoft Defender Antivirus compatibility with other security products](microsoft-defender-antivirus-compatibility).

On Windows devices, tamper protection has the following modes:

- **Disabled**: Tamper protection is turned off.
- **Enabled**: Tamper protection is turned on, and the following tamper-protected settings can't be changed:
    - Virus and threat protection remains enabled.
    - Real-time protection remains turned on.
    - Behavior monitoring remains turned on.
    - Antivirus protection, including IOfficeAntivirus (IOAV), remains enabled.
    - Cloud protection remains enabled.
    - Security intelligence updates occur.
    - Automatic actions are taken on detected threats.
    - Notifications are visible in the Windows Security app.
    - Archived files are scanned.
    - Exclusions can't be modified or added. See [Protect Microsoft Defender Antivirus exclusions with tamper protection](tamper-protection-antivirus-exclusions).
    - Attempts to modify Microsoft Defender Antivirus settings through the registry are blocked.

Note

When tamper protection is turned on, changes made through a management tool, including Group Policy, might appear to succeed, but tamper protection blocks the changes. Use [troubleshooting mode](troubleshooting-mode-enable) to temporarily disable tamper protection when you need to change a protected setting.

Starting with security intelligence update `1.383.1159.0` (March 2023), tamper protection no longer locks **Allow Scanning Network Files** to its default value. In managed environments, the default value is `enabled`.

To help ensure that tamper protection doesn't interfere with non-Microsoft security products or enterprise installation scripts that modify Microsoft Defender Antivirus settings, use security intelligence version `1.287.60.0` (February 2019) or later. See [Latest security intelligence updates for Microsoft Defender Antivirus and other Microsoft antimalware](https://www.microsoft.com/wdsi/defenderupdates).

For configuration methods and precedence information, see [Configure tamper protection on Windows devices](tamper-protection-windows-configure).

On Windows devices, tamper protection is part of anti-tampering capabilities that include [standard protection attack surface reduction (ASR) rules](attack-surface-reduction-rules-overview#asr-rules). Tamper protection is also an important part of [built-in protection](built-in-protection). For more information, see:

- [Built-in protection helps guard against ransomware](built-in-protection) (article)
- [Tamper protection is turned on for all enterprise customers](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/tamper-protection-will-be-turned-on-for-all-enterprise-customers/ba-p/3616478) (Tech Community blog post)

### Tamper protection modes on macOS devices

On macOS devices, tamper protection has the following modes:

- **Disabled**: Tamper protection is turned off.
- **Audit**: Tamper protection logs attempts to uninstall the Defender for Endpoint agent or create, delete, rename, or modify Defender for Endpoint files. It doesn't block the attempts. Audit mode is the default after installation of Defender for Endpoint.
- **Block**: Tamper protection blocks attempts to uninstall the Defender for Endpoint agent or create, delete, rename, or modify Defender for Endpoint files. Commands that try to stop the `wdavdaemon` process also fail.

For configuration methods and precedence information, see [Configure tamper protection for Microsoft Defender for Endpoint on macOS](tamper-protection-macos-configure).

### Tamper protection mode on Linux devices

Important

Tamper protection on Linux devices is currently in Preview.

On Linux devices, tamper protection is currently available only in **Audit** mode. Audit mode detects and reports unauthorized changes to Defender for Endpoint assets, even when the root user makes the changes. It doesn't block the activity.

Audit mode detects the following tampering attempts:

- Modifying Defender for Endpoint configuration files.
- Deleting, renaming, or moving Defender for Endpoint configuration files, state files, and binaries.
- Stopping Defender for Endpoint processes or restarting Defender for Endpoint services.

For supported Linux distributions, prerequisites, verification, and testing, see [Tamper protection in audit mode for Microsoft Defender for Endpoint on Linux](tamper-protection-linux-audit-mode).

## Requirements for tamper protection

### Supported operating systems

Tamper protection is available for devices that are running one of the following operating systems:

- [Supported Linux distributions and kernel versions](tamper-protection-linux-audit-mode#prerequisites), where tamper protection in audit mode is currently in Preview.
- [macOS devices](tamper-protection-macos-configure), where tamper protection uses platform-specific modes and behavior.
- Windows 10 or later, including Enterprise multi-session.
- Windows Server 2016 and later.
- Windows Server, version 1803 or later.
- Windows Server 2012 R2 using the [modern unified solution](onboard-server#functionality-in-the-modern-unified-solution-for-windows-server-2016-and-windows-server-2012-r2).
- Azure Stack HCI OS, version 23H2 and later.

On the following versions of Windows, the Windows Security app doesn't show whether tamper protection is enabled:

- Windows Server 2012 R2 using the modern unified solution
- Windows Server 2016
- Windows 10:
    - Version 1809 (November 2018)
    - Version 1803 (April 2018)
    - Version 1709 (October 2017)
- Windows Server 2019

Important

On Windows Server 2016, the Windows Security app might also show an inaccurate *real-time protection* status when tamper protection is enabled. To check both settings, see [Determine the status of tamper protection and real-time protection using PowerShell](tamper-protection-windows-configure#determine-the-status-of-tamper-protection-and-real-time-protection-using-powershell).

### Required permissions

Required permissions depend on how you configure tamper protection:

- **Microsoft Intune**: Your account has RBAC permissions equivalent to the built-in Intune **Endpoint Security Manager** role. See [Endpoint Security Manager](/en-us/intune/fundamentals/role-based-access-control/ref-built-in-roles#endpoint-security-manager).
- **Microsoft Defender portal**: Your account has the **Authorization and settings/Security settings/Core security settings (manage)** permission in [Microsoft Defender XDR unified role-based access control (RBAC)](/en-us/defender-xdr/manage-rbac). The **Global Administrator**^\*^, **Security Administrator**, and **Security Operator** Microsoft Entra roles are granted this permission. See [Permissions in Microsoft Defender unified RBAC](/en-us/defender-xdr/custom-permissions-details#authorization-and-settings).
- **Windows Security app**: You have administrator permissions on the Windows device.

Important

^\*^ Follow the principle of least privilege by assigning accounts only the permissions they need. The Global Administrator role is highly privileged. Limit its use to emergencies or situations where you can't use a less-privileged role.

### Device onboarding requirement

Devices must be [onboarded to Defender for Endpoint](onboarding) before you configure tamper protection by using Intune or the Microsoft Defender portal. If a device isn't onboarded, tamper protection appears as **Not applicable** until onboarding is complete.

### Requirements for Windows management methods

Other requirements vary based on how you configure tamper protection:

- **Microsoft Intune**:

    - You have an Intune license. Intune is a separate product that isn't included with all Defender for Endpoint subscriptions. See [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).
    - Your organization uses [Intune to manage devices](/en-us/intune/intune-service/fundamentals/manage-devices). Co-managed devices aren't supported for this feature.
    - **Windows 10 requirements**: Version 1709 (October 2017) or later.
    - **Microsoft Defender Antivirus requirements**:
        - **Platform update**: `4.18.1906.3` (June 2019) or later.
        - **Engine update**: `1.1.15500.X` (March 2019) or later.
    - Intune and Defender for Endpoint use the same Microsoft Entra infrastructure.
    - Set [DisableLocalAdminMerge](/en-us/windows/client-management/mdm/defender-csp#configurationdisablelocaladminmerge) to `true` on devices.
- **Microsoft Defender portal**:

    - **Microsoft Defender Antivirus requirements**:

        - **Platform update**: `4.18.2010.7` (October 2020) or later.
        - **Engine update**: `1.1.17600.5` (October 2020) or later.
    - [Cloud-delivered protection](cloud-protection-configure) is turned on so the enabled state can be controlled.

        Starting with platform update `4.18.2111.5` (November 2021), turning on tamper protection automatically turns on cloud-delivered protection if it isn't already enabled on the device.
- **Microsoft Configuration Manager**: [Set up tenant attach](/en-us/intune/configmgr/tenant-attach/endpoint-security-get-started). Tenant attach synchronizes on-premises Configuration Manager devices with the Microsoft Intune admin center so you can deploy endpoint security policies to device collections.
- **Windows Security app**: The Windows device isn't managed by a security team.

Note

Tamper protection might block changes to certain security settings. If Event ID 5013 appears, see [Review event logs and error codes to troubleshoot issues with Microsoft Defender Antivirus](troubleshoot-microsoft-defender-antivirus).

## Tamper protection exclusions

Tamper protection exclusions have different purposes on Windows and macOS devices.

### Windows devices

On Windows devices, tamper protection can protect organization-managed Microsoft Defender Antivirus exclusion lists from unauthorized changes under certain conditions. These exclusions define files, folders, file types, and processes that Microsoft Defender Antivirus doesn't scan. For requirements and verification steps, see [Protect Microsoft Defender Antivirus exclusions with tamper protection](tamper-protection-antivirus-exclusions).

### macOS devices

On macOS devices, tamper protection exclusions allow trusted processes to perform operations that tamper protection would otherwise block. Defender for Endpoint includes built-in exclusions for Jamf and Intune management processes. You can use an MDM profile to add exclusions for other trusted management processes based on their path, team ID, signing ID, process arguments, or a combination of these attributes. For more information, see [Configure tamper protection exclusions on macOS](tamper-protection-macos-configure#configure-tamper-protection-exclusions).

## View information about tampering attempts

Tampering attempts might indicate a larger cyberattack. Attackers try to change security settings to persist on devices and avoid detection.

On Windows devices, Defender for Endpoint detects potential attempts to turn off Microsoft Defender Antivirus protection or change antivirus exclusions. Tampering activity can also include attempts to stop or modify the Defender for Endpoint sensor or bypass tamper protection. For examples of alert titles, see [Detecting potential tampering activity in the Microsoft Defender portal](tamper-resiliency#detecting-potential-tampering-activity-in-the-microsoft-365-defender-portal).

On Linux devices, tamper protection in audit mode is currently in Preview. Tampering alerts are available in the device timeline and in **Incidents and alerts** in the Microsoft Defender portal.

Some potential tampering activity generates an alert on the **Alerts** page in the Defender portal at https://security.microsoft.com/alerts. Open the alert to review the affected assets and entities, the reason the alert was triggered, and related events that occurred before and after the activity. The alert process tree and timeline can help you identify the process, file, user, or device associated with the attempt. For more information, see [Investigate alerts in Microsoft Defender for Endpoint](investigate-alerts).

To reduce unnecessary alert noise, tampering activity that isn't correlated with suspicious activity might not generate an alert. The activity is still available in the device timeline and advanced hunting.

Your security operations team can use [endpoint detection and response](overview-endpoint-detection-response) to investigate the affected device and take response actions. They can also use advanced hunting to find related events and alerts.

### Query tampering attempts with advanced hunting

Tampering events from supported operating systems are available in the `DeviceEvents` table. For information about queries, supported tables, and required permissions, see [Proactively hunt threats with advanced hunting](/en-us/defender-xdr/advanced-hunting-overview).

On the **Advanced hunting** page in the Defender portal at https://security.microsoft.com/v2/advanced-hunting, run the following query:

```kusto
DeviceEvents
| where Timestamp > ago(10d)
| where ActionType == "TamperingAttempt"
```

To limit the results to a specific device, add the following line and replace `<DeviceId>` with the device ID from the **Device inventory** page in the Defender portal at https://security.microsoft.com/machines:

```kusto
| where DeviceId == "<DeviceId>"
```

Tamper protection alert titles vary by detected activity and operating system. The following query returns two known tamper protection alert titles:

```kusto
AlertInfo
| where Timestamp > ago(10d)
| where DetectionSource == "EDR"
| where Title in ("Tamper Protection bypass", "Tampering with the Microsoft Defender for Endpoint sensor")
```

Adjust the `Timestamp` value in either query as needed.

### Tune alerts for legitimate tampering activity

To reduce alert noise from known and approved activity, create alert tuning rules in the Microsoft Defender portal. For more information, see [Tune an alert](/en-us/defender-xdr/investigate-alerts#tune-an-alert).

## Review your security recommendations

Tamper protection integrates with [Microsoft Defender Vulnerability Management](/en-us/defender-vulnerability-management/defender-vulnerability-management). [Security recommendations](/en-us/defender-vulnerability-management/tvm-security-recommendation) identify devices where tamper protection isn't turned on. In the [Vulnerability Management dashboard](/en-us/defender-vulnerability-management/tvm-dashboard-insights#vulnerability-management-dashboard), search for *tamper*, and then select **Turn on Tamper Protection** in the results. For more information, see [Defender Vulnerability Management dashboard insights](/en-us/defender-vulnerability-management/tvm-dashboard-insights#dashboard-insights---threat-and-vulnerability-management).