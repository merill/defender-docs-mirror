---
layout: Conceptual
title: Controlled configuration in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/secure-controlled-configuration
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Controlled configuration makes cloud policy the single source of truth for Defender Antivirus settings, overriding Group Policy, scripts, and local changes to eliminate configuration drift.
ms.service: defender-endpoint
ms.localizationpriority: medium
ms.date: 2026-09-15T00:00:00.0000000Z
ms.topic: concept-article
author: chrisda
ms.author: chrisda
ms.reviewer: jcedola
ms.subservice: ngp
ms.collection:
- m365-security
- tier2
- mde-ngp
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1015
locale: en-us
document_id: 1805aa13-88c7-8bb9-ccd4-95e8c6ae99e4
document_version_independent_id: 1805aa13-88c7-8bb9-ccd4-95e8c6ae99e4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/secure-controlled-configuration.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: secure-controlled-configuration
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/secure-controlled-configuration.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
platformId: 02ac8a65-0519-a445-a2dc-8ef8f2717d3c
---

# Controlled configuration in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Important

The features described in this article are currently in Preview, aren't available in all organizations, and are subject to change.

Controlled configuration is a configuration enforcement model that makes cloud-managed policy the single source of truth for Microsoft Defender Antivirus settings. When controlled configuration is enabled, Intune and Microsoft Defender for Endpoint policies take precedence. The device ignores settings from Group Policy, scripts, Microsoft Configuration Manager, and local admin changes.

Controlled configuration eliminates configuration drift and policy conflicts by extending tamper-protection-style enforcement to the entire Defender Antivirus configuration surface.

[Tamper protection](tamper-protection-overview) and controlled configuration are complementary but distinct capabilities:

| Feature | Tamper protection | Controlled configuration |
| --- | --- | --- |
| **Scope** | Small fixed set of security settings (~10-13 settings) | Entire Defender Antivirus configuration surface |
| **Configuration source** | Microsoft-defined defaults only | Organization-defined cloud policy (Intune/Defender for Endpoint) |
| **Customization** | No customization | Full policy-driven control |
| **Enforcement** | Prevents disabling critical protections | Overrides all non-cloud configuration channels |

Controlled configuration is a superset of tamper protection that provides policy-driven control over the full Microsoft Defender Antivirus configuration.

Note

Although tamper protection and controlled configuration can technically be turned on at the same time, we recommend that your organization selects one or the other.

## Prerequisites

- Devices must be onboarded to Microsoft Defender for Endpoint.
- Devices must be managed through Microsoft Intune or Defender for Endpoint security settings management.
- Devices must run Windows 10, Windows 11, or Windows Server 2019.
- Devices must run Microsoft Defender for Endpoint EDR Sensor version later than 10.8804 (September 2025).
- Devices must run Microsoft Defender Antivirus platform version 4.18.26060.3004 or later (June 2026).

Controlled configuration doesn't currently support:

- Co-management (Configuration Manager + Intune) environments.
- GCC High environments.

## What controlled configuration covers

Currently, controlled configuration provides protection and enforcement for Microsoft Defender Antivirus settings, including:

- Antivirus configuration (scan settings, exclusions, updates)
- Attack surface reduction (ASR) policies
- Defender Configuration Service Provider (CSP) and Policy CSP surface (broad set of antivirus-related controls)
- Local admin merge behavior

Currently, controlled configuration doesn't cover:

- Microsoft Defender Device Control
- Endpoint detection and response (EDR) settings
- Windows operating system settings (such as Firewall)

## How controlled configuration enforcement works

Controlled configuration enforces cloud-managed policy through three mechanisms:

- **Single-source enforcement**: When controlled configuration is enabled, the following enforcement rules apply:

    - Only Intune and Defender for Endpoint policies are honored for Defender Antivirus settings.
    - Group Policy Object (GPO), scripts, Configuration Manager, and local admin changes are ignored.
    - Microsoft Defender Antivirus doesn't honor local exclusions. Organizations can still choose to allow local administrator-defined exclusions by enabling the local administrator merge setting through policy. When local administrator merge is enabled, locally defined exclusions can be merged with centrally managed exclusions.
- **Secure defaults**: If a setting isn't explicitly configured in a policy, controlled configuration applies Microsoft-defined defaults. This behavior ensures that devices maintain a strong security posture even when administrators haven't configured every available setting.
- **Conflict resolution**: Controlled configuration uses a value-based precedence model rather than a last-write-wins model:

    - **On** takes precedence over **Off**. If one policy sets controlled configuration to On and another sets it to Off, the feature stays enabled on the device.
    - If multiple policies assign different values, a conflict is reported, but the On value is still enforced.
    - If multiple policies assign the same value, the result is success with no conflict.

    Important

    **Not configured** doesn't mean **Off**. To disable the feature, explicitly deploy a policy that sets controlled configuration to **Off**.

## Enable controlled configuration

You can enable controlled configuration through either Microsoft Intune or [Microsoft Defender for Endpoint security settings management](manage-security-policies).

> 
> Microsoft Intune is the recommended tool for configuring and distributing Defender for Endpoint features to devices. However, Intune is a separate product that isn't part of Defender for Endpoint, and it isn't included in all subscriptions. To use Intune, you need a subscription that includes it, or you can buy it separately as a standalone subscription or add-on. If you don't have Intune, you can use any of the other methods in this article. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).

Controlled configuration is configured through the same policy surface as tamper protection. In the Windows Security Experience profile, Intune renames the tamper protection setting to **Controlled Configuration (Device)** when controlled configuration is available. You can't enable controlled configuration through the Settings Catalog or the Device Control v1 (DCv1) template.

Because controlled configuration and tamper protection use the same policy setting, setting **Controlled Configuration (On)** supersedes the tamper protection value on that device. You don't deploy separate tamper protection and controlled configuration policies for the same setting. To migrate existing tamper protection (DCv1) policies to controlled configuration, create a Windows Security Experience policy with **Controlled Configuration (On)**, then remove the tamper protection setting from your DCv1 policies to avoid conflicts.

1. On the **Endpoint security** page in the Microsoft Intune admin center at https://intune.microsoft.com, create a new Windows Security Experience profile or edit an existing one.
2. Locate the **Controlled Configuration (Device)** setting (formerly **Tamper Protection**).
3. Set the value to **Controlled Configuration (On)** to enable controlled configuration.
4. Assign the policy to the appropriate device groups.

## Minimum client version and rollback

Before you assign **Controlled Configuration (On)**, update devices to Microsoft Defender Antivirus platform version 4.18.26060.3004 or later, and validate the deployment with a pilot group.

On devices with earlier platform versions, Intune might send **Controlled Configuration (On)** and **Tamper Protection (Off)**, but the device might apply only the tamper protection setting. This behavior leaves both controlled configuration and tamper protection turned off.

To roll back, change the Windows Security Experience policy from **Controlled Configuration (On)** to **Tamper Protection (On)**, redeploy the policy, sync the affected devices, and verify that tamper protection is enabled. Normal policy delivery latency applies.

## Reporting and monitoring

Controlled configuration status is visible in both the Intune admin center and the Microsoft Defender portal, depending on how devices are managed.

- **Intune**: For devices enrolled directly through Intune by using Mobile Device Management (MDM), you can view:

    - Policy status (Success, Conflict, or Error)
    - Device-level controlled configuration status
- **Microsoft Defender portal**: For devices managed through Defender for Endpoint security settings management, check the Microsoft Defender portal for effective configuration state.

    Note

    These devices aren't visible in Intune reports. Use the Microsoft Defender portal to verify the effective controlled configuration state.

## Verify controlled configuration on a device

To confirm the controlled configuration state directly on a device, run the following PowerShell cmdlet:

```powershell
Get-MpComputerStatus
```

Review the following properties in the output:

- **ControlledConfigurationState**: The current controlled configuration enforcement state on the device.
- **IsTamperProtected**: Indicates whether tamper protection (the foundation of controlled configuration) is active.
- **TamperProtectionSource**: The source that enforces the current state.

You can also use `Get-MpComputerStatus` to confirm that the Microsoft Defender Antivirus platform version meets the prerequisites, and to validate the configuration state after a policy change or a controlled configuration reset.

## Lifecycle behaviors

Controlled configuration behavior varies depending on device lifecycle changes:

- **Policy unassignment**: Controlled configuration is removed from the device unless another controlled configuration policy still applies.
- **Defender for Endpoint unenrollment**: Controlled configuration remains **On** (not cleaned up automatically).
- **Device offboarding**: Controlled configuration is removed and reset to **Off**.

## Reset controlled configuration on a device

To clear the controlled configuration state on a device, run the following commands in an elevated Command Prompt (a Command Prompt window you opened by selecting **Run as administrator**):

Tip

The device must have tamper protection turned on and be in troubleshooting mode.

The first command changes the directory to the latest version of &lt;antimalware platform version&gt; in `%ProgramData%\Microsoft\Windows Defender\Platform\<antimalware platform version>`. If that path doesn't exist, it goes to `%ProgramFiles%\Windows Defender`.

```dos
(set "_done=" & if exist "%ProgramData%\Microsoft\Windows Defender\Platform\" (for /f "delims=" %d in ('dir "%ProgramData%\Microsoft\Windows Defender\Platform" /ad /b /o:-n 2^>nul') do if not defined _done (cd /d "%ProgramData%\Microsoft\Windows Defender\Platform\%d" & set _done=1)) else (cd /d "%ProgramFiles%\Windows Defender")) >nul 2>&1

MpCmdRun.exe -Config -ResetControlledConfiguration
```

For more information, see [Enable and use troubleshooting mode in Microsoft Defender for Endpoint](troubleshooting-mode-enable).

## Known limitations

Currently, the following limitations apply to controlled configuration:

- You might see false conflicts in Intune when both tamper protection and controlled configuration policies target the same device.
- You might see reporting inconsistencies between the Intune admin center and the Microsoft Defender portal.
- Coverage is limited to Microsoft Defender Antivirus settings (device control, EDR, and firewall aren't yet covered).
- When you turn on controlled configuration through Microsoft Defender for Endpoint security settings management or Intune, tamper protection is turned off, unless another tamper protection policy explicitly sets tamper protection to on. When controlled configuration is on and tamper protection is off, the tamper protection secure score is lower. We're working to address this gap.