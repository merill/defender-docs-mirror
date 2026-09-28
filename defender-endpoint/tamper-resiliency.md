---
layout: Conceptual
title: Tamper resiliency with Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/tamper-resiliency
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Strengthen Microsoft Defender for Endpoint tamper resiliency with centralized management, device protections, driver controls, and detection.
author: limwainstein
ms.author: lwainstein
ms.reviewer: joshbregman
ms.service: defender-endpoint
ms.subservice: ngp
ms.date: 2026-09-08T00:00:00.0000000Z
ms.topic: overview
ms.custom:
- msecd-doc-authoring-1016
ms.collection:
- tier1
- highpri
- mde-ngp
ai-usage: ai-assisted
locale: en-us
document_id: f69b7502-0190-94f7-3526-96ec713a239d
document_version_independent_id: f69b7502-0190-94f7-3526-96ec713a239d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/tamper-resiliency.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: tamper-resiliency
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/tamper-resiliency.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 01d72471-c1f1-8068-812a-222ec54c42cd
---

# Tamper resiliency with Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Tampering describes attempts by attackers to weaken Microsoft Defender for Endpoint. Attackers might target security controls on individual devices as part of a larger objective, such as deploying ransomware. Tamper resiliency combines device-level protections, centralized management, and detection to help prevent these changes and reduce their impact.

For tamper protection modes, protected settings, requirements, exclusions, and investigation guidance, see [Tamper protection overview](tamper-protection-overview).

Build organization-wide tamper resiliency on a [Zero Trust](/en-us/windows/security/book/security-foundation) model:

- Follow the best practice of least privilege. See [Access control overview for Windows](/en-us/windows/security/identity-protection/access-control/access-control).
- Configure [Conditional Access policies](/en-us/azure/active-directory/conditional-access/overview) to apply access controls based on user and device signals.

Keep devices healthy and centrally managed:

- [Onboard devices to Defender for Endpoint](onboard-configure).
- Make sure [security intelligence and antivirus updates](microsoft-defender-antivirus-updates) are installed.
- Manage devices centrally by using [Microsoft Intune](/en-us/intune/intune-service/protect/advanced-threat-protection-configure), [Microsoft Defender for Endpoint security settings management](/en-us/intune/intune-service/protect/mde-security-integration), or [Configuration Manager](/en-us/intune/configmgr/protect/deploy-use/endpoint-protection-configure).

Note

On Windows devices, you can manage Microsoft Defender Antivirus by using Group Policy, Windows Management Instrumentation (WMI), and PowerShell cmdlets. These methods are more susceptible to tampering than centralized management through Intune, Configuration Manager, or Defender for Endpoint security settings management.

If you're using Group Policy, we recommend [disabling local overrides for Microsoft Defender Antivirus settings](configure-local-policy-overrides-microsoft-defender-antivirus#configure-local-overrides-for-microsoft-defender-antivirus-settings-using-group-policy) and [disabling local list merging](configure-local-policy-overrides-microsoft-defender-antivirus#configure-how-locally-and-globally-defined-threat-remediation-and-exclusions-lists-are-merged).

Use the [device health reports in Microsoft Defender for Endpoint](device-health-reports) to review the health of [Microsoft Defender Antivirus](device-health-microsoft-defender-antivirus-health) and [Defender for Endpoint sensors](device-health-sensor-health-os).

## Prevent tampering on individual devices

Different controls protect against different tampering techniques:

| Control | Platform | Tampering techniques |
| --- | --- | --- |
| [Tamper protection](tamper-protection-overview) | Windows | Terminate or suspend processes, stop services, modify registry settings or exclusions, hijack DLLs, modify the file system, or impair agent integrity. |
| [Tamper protection](tamper-protection-macos-configure) | macOS | Terminate or suspend processes, modify Defender for Endpoint files, or impair agent integrity. |
| [Attack surface reduction (ASR) rules](attack-surface-reduction-rules-overview) | Windows | Prevent apps from writing exploited vulnerable signed drivers to disk. See [Block abuse of exploited vulnerable signed drivers (Device)](attack-surface-reduction-rules-reference#block-abuse-of-exploited-vulnerable-signed-drivers-device). |
| [App Control for Business](/en-us/windows/security/application-security/application-control/app-control-for-business/operations/appcontrol-operational-guide), formerly Windows Defender Application Control (WDAC) | Windows | Prevent vulnerable kernel drivers from loading. See [Microsoft vulnerable driver block list](/en-us/windows/security/application-security/application-control/app-control-for-business/design/microsoft-recommended-driver-block-rules). |

## Protect against driver-based tampering on Windows

Attackers can exploit vulnerabilities in signed drivers to gain kernel access and disable or bypass security controls. Use the Microsoft vulnerable driver blocklist, an ASR rule, and App Control for Business policies to reduce this risk.

### Use the Microsoft vulnerable driver blocklist

Since the Windows 11 2022 Update, the vulnerable driver blocklist is enabled by default. Except on Windows Server 2016, the blocklist is also enforced when memory integrity, also known as hypervisor-protected code integrity (HVCI), Smart App Control, or S mode is active. The blocklist is updated quarterly, and updates are delivered through monthly Windows updates.

See [Microsoft vulnerable driver block list](/en-us/windows/security/application-security/application-control/app-control-for-business/design/microsoft-recommended-driver-block-rules#microsoft-vulnerable-driver-blocklist).

To deploy the latest recommended blocklist through an App Control for Business policy, see [Vulnerable driver blocklist XML](/en-us/windows/security/application-security/application-control/app-control-for-business/design/microsoft-recommended-driver-block-rules#microsoft-vulnerable-driver-blocklist).

### Use the vulnerable signed drivers ASR rule

The **Block abuse of exploited vulnerable signed drivers** ASR rule prevents apps from saving vulnerable signed drivers on a device. It doesn't prevent an existing driver from loading. Run the rule in **Audit** mode to evaluate its effect before you use **Block** mode. For more information, see [Block abuse of exploited vulnerable signed drivers (Device)](attack-surface-reduction-rules-reference#block-abuse-of-exploited-vulnerable-signed-drivers).

### Use App Control for Business to block drivers

[App Control for Business operational guidance](/en-us/windows/security/application-security/application-control/app-control-for-business/operations/appcontrol-operational-guide) explains how to create policies that control which drivers can run. Use audit mode to evaluate compatibility before you enforce an App Control policy.

## Protect Microsoft Defender Antivirus exclusions on Windows

Attackers might add or modify Microsoft Defender Antivirus exclusions to avoid scanning. Tamper protection can protect organization-managed exclusion lists when devices meet the platform, management, sensor, and policy requirements. For the complete requirements and verification steps, see [Protect Microsoft Defender Antivirus exclusions with tamper protection](tamper-protection-antivirus-exclusions).

The `DisableLocalAdminMerge` setting is one of the exclusion-protection requirements. For configuration information, see [Disable local list merging](configure-local-policy-overrides-microsoft-defender-antivirus#use-microsoft-intune-to-disable-local-list-merging).

As a separate protection, enable [HideExclusionsFromLocalAdmin](/en-us/windows/client-management/mdm/defender-csp#configurationhideexclusionsfromlocaladmins) to prevent local administrators from viewing existing exclusions through Registry Editor or the **Get-MpPreference** PowerShell cmdlet. This setting doesn't remove the exclusions.

## Detecting potential tampering activity in the Microsoft Defender portal

Some potential tampering activity generates an alert in the Microsoft Defender portal. To reduce unnecessary alert noise, activity that isn't correlated with suspicious behavior might not generate a standalone alert. The activity remains available in the device timeline and advanced hunting. For investigation guidance, see [View information about tampering attempts](tamper-protection-overview#view-information-about-tampering-attempts).

Tampering alert titles can include:

- Attempt to bypass Microsoft Defender for Endpoint client protection
- Attempt to stop Microsoft Defender for Endpoint sensor
- Attempt to tamper with Microsoft Defender on multiple devices
- Attempt to turn off Microsoft Defender Antivirus protection
- Defender detection bypass
- Driver-based tampering attempt blocked
- Image file execution options set for tampering purposes
- Microsoft Defender Antivirus protection turned off
- Microsoft Defender Antivirus tampering
- Modification attempt in Microsoft Defender Antivirus exclusion list
- Pending file operations mechanism abused for tampering purposes
- Possible anti-malware Scan Interface (AMSI) tampering
- Possible remote tampering
- Possible sensor tampering in memory
- Potential attempt to tamper with MDE via drivers
- Security software tampering
- Suspicious Microsoft Defender Antivirus exclusion
- Tamper protection bypass
- Tampering activity typical to ransomware attacks
- Tampering with Microsoft Defender for Endpoint sensor communication
- Tampering with Microsoft Defender for Endpoint sensor settings
- Tampering with the Microsoft Defender for Endpoint sensor

If the [Block abuse of exploited vulnerable signed drivers (Device)](attack-surface-reduction-rules-reference#block-abuse-of-exploited-vulnerable-signed-drivers) ASR rule is triggered, view the event in the [attack surface reduction rules report](attack-surface-reduction-rules-report) or [advanced hunting](attack-surface-reduction-rules-monitor#asr-rule-events-in-advanced-hunting).

If [App Control for Business](/en-us/windows/security/application-security/application-control/app-control-for-business/deployment/appcontrol-deployment-guide) is enabled, you can view [block and audit activity in advanced hunting](/en-us/windows/security/application-security/application-control/app-control-for-business/operations/querying-application-control-events-centrally-using-advanced-hunting).