---
layout: FAQ
title: Troubleshoot problems with tamper protection - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/tamper-protection-troubleshoot
summary: >
  <p>Resolve common tamper protection problems on Windows and macOS and with the Preview feature on Linux. For an overview of protected settings, see <a href="tamper-protection-overview">Tamper protection overview</a>. For setup instructions, see <a href="tamper-protection-windows-configure">Configure tamper protection on Windows devices</a>, <a href="tamper-protection-macos-configure">Configure tamper protection for Microsoft Defender for Endpoint on macOS</a>, or <a href="tamper-protection-linux-audit-mode">Tamper protection in audit mode for Microsoft Defender for Endpoint on Linux</a>. For general questions, see <a href="tamper-protection-faq">Frequently asked questions about tamper protection</a>.</p>
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Resolve Microsoft Defender for Endpoint tamper protection problems on Windows and macOS and with the Preview feature on Linux.
ms.service: defender-endpoint
ms.localizationpriority: medium
ms.topic: faq
author: limwainstein
ms.author: lwainstein
ms.custom:
- nextgen
- msecd-doc-authoring-1016
ms.reviewer: yongrhee
ms.subservice: ngp
ms.collection:
- m365-security
- tier1
- mde-ngp
search.appverid: met150
ms.date: 2026-09-09T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 7e0aca30-9fd0-647a-1396-f04c9fac1a0a
document_version_independent_id: 7e0aca30-9fd0-647a-1396-f04c9fac1a0a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/tamper-protection-troubleshoot.yml
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: faq
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: tamper-protection-troubleshoot
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/tamper-protection-troubleshoot.yml
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: d5cc8807-3150-d3bc-6408-2f7d4c6b8fc9
---

# Troubleshoot problems with tamper protection - Microsoft Defender for Endpoint | Microsoft Learn

Resolve common tamper protection problems on Windows and macOS and with the Preview feature on Linux. For an overview of protected settings, see [Tamper protection overview](tamper-protection-overview). For setup instructions, see [Configure tamper protection on Windows devices](tamper-protection-windows-configure), [Configure tamper protection for Microsoft Defender for Endpoint on macOS](tamper-protection-macos-configure), or [Tamper protection in audit mode for Microsoft Defender for Endpoint on Linux](tamper-protection-linux-audit-mode). For general questions, see [Frequently asked questions about tamper protection](tamper-protection-faq).

## Tamper protection is blocking a required change on a managed Windows device. What should I do?

Use [troubleshooting mode](troubleshooting-mode-enable) to temporarily change tamper-protected settings on the device. The device must be online when you temporarily disable tamper protection. When troubleshooting mode expires, the temporary changes are discarded, and the settings revert to their previous policy-managed values.

## Changes to Microsoft Defender Antivirus settings using Group Policy are ignored. Why is this happening, and what can we do about it?

When tamper protection is on, Group Policy changes to tamper-protected settings might appear to succeed, but tamper protection blocks the changes. For more information, see [Tamper protection overview](tamper-protection-overview#what-happens-when-tamper-protection-is-turned-on).

To make a temporary change on a device, use [troubleshooting mode](troubleshooting-mode-enable). To make permanent changes, adjust the tamper protection policy or exclude the affected devices from tamper protection through Intune or Configuration Manager. For policy configuration details, see [Configure tamper protection on Windows devices](tamper-protection-windows-configure).

## Why does tamper protection appear as Not applicable?

Devices must be onboarded to Microsoft Defender for Endpoint before you configure tamper protection through Intune or the Microsoft Defender portal. If a device isn't onboarded, tamper protection appears as **Not applicable** until onboarding is complete. See [Device onboarding requirement](tamper-protection-overview#device-onboarding-requirement).

## Why did Microsoft Defender Antivirus generate Event ID 5013?

Event ID 5013 means tamper protection blocked a change to a Microsoft Defender Antivirus setting. The event identifies the setting that the attempted action tried to change. See [Review event logs and error codes to troubleshoot issues with Microsoft Defender Antivirus](troubleshoot-microsoft-defender-antivirus).

## Why aren't Microsoft Defender Antivirus exclusions tamper protected?

Exclusion protection requires a supported Microsoft Defender platform version, the `DisableLocalAdminMerge` setting, a supported device-management state, and centrally managed exclusions. Verify the requirements and the `TPExclusions` registry value in [Protect Microsoft Defender Antivirus exclusions with tamper protection](tamper-protection-antivirus-exclusions).

## How do I protect exclusions for Microsoft Defender Antivirus?

See [Protect Microsoft Defender Antivirus exclusions with tamper protection](tamper-protection-antivirus-exclusions) for requirements and verification steps.

## Tamper protection is reported as disabled on a macOS device. How do I troubleshoot it?

If `mdatp health` reports that tamper protection is disabled more than an hour after you enabled tamper protection and onboarded the device, retrieve detailed status information. The following command reports the effective mode, configuration source, and managed exclusions:

```bash
mdatp health --details tamper_protection
```

The following sample output shows the current tamper protection mode, configuration source, and any managed exclusions delivered by policy. Verify that `tamper_protection` and `configuration_source` match your intended configuration:

```console
tamper_protection                           : "audit"
exclusions                                  : [{"path":"/usr/bin/ruby","team_id":"","signing_id":"com.apple.ruby","args":["/usr/local/bin/global_mdatp_restarted.rb"]}] [managed]
feature_enabled_protection                  : true
feature_enabled_portal                      : true
configuration_source                        : "local"
configuration_local                         : "audit"
configuration_portal                        : "block"
configuration_default                       : "audit"
configuration_is_managed                    : false
```

- `tamper_protection` is the *effective* mode. If the value matches the intended mode, tamper protection is configured correctly.
- `configuration_source` identifies the source that sets the effective enforcement level. The value should match the method you used to configure tamper protection. If you used a managed profile but the value isn't `mdm`, check the profile configuration.
    - `mdm`: A managed profile configures the mode. Only a Security Administrator can change the mode by updating the profile.
    - `local`: The `mdatp config` command configures the mode.
    - `portal`: The Microsoft Defender portal configures the default enforcement level.
    - `defaults`: No source configures the mode, so Defender for Endpoint uses the default mode.
- If `feature_enabled_protection` is `false`, tamper protection isn't enabled for the organization. This value can occur if Defender for Endpoint doesn't report the device as licensed.
- If `feature_enabled_portal` is `false`, configuring the default mode in the Microsoft Defender portal isn't enabled for the organization.
- `configuration_local`, `configuration_portal`, and `configuration_default` show the modes that each configuration source would apply. For example, an MDM profile can set block mode while `configuration_default` reports audit mode. If you remove the MDM profile and no local or portal setting applies, Defender for Endpoint uses the reported default mode.

Note

Before version `101.98.71` (May 2023), inspect the Defender for Endpoint logs to get the same information. Run the following command to confirm the most recent tamper protection feature-state entry in the Defender core log:

```bash
sudo grep -F '[{tamperProtection}]: Feature state:' /Library/Logs/Microsoft/mdatp/microsoft_defender_core.log | tail -n 1
```

## Tamper protection audit mode is reported as disabled on a Linux device. How do I troubleshoot it?

Important

Tamper protection for Linux is currently in Preview.

During Preview, audit mode is enabled by default on eligible devices in the Insiders-Slow ring. The feature rolls out gradually over two weeks. Verify that the device meets the [Linux tamper protection prerequisites](tamper-protection-linux-audit-mode#prerequisites), including the Defender for Endpoint version, distribution, and kernel requirements.

Run the following command to check the tamper protection status and errors:

```bash
mdatp health --details tamper_protection
```

The following output shows that tamper protection is enabled in audit mode without errors:

```bash
tamper_protection_enforcement_level : "audit"
tamper_protection_errors            : []
```

If `tamper_protection_enforcement_level` is `disabled`, use `tamper_protection_errors` to identify the cause:

| Error | Description |
| --- | --- |
| `tamper_protection_unsupported_kernel_version` | The device kernel version doesn't support tamper protection. |
| `not_supported_in_the_current_configuration` | Tamper protection can't be enabled because a required internal configuration isn't available. |

If the device meets the prerequisites but audit mode remains disabled, run the following command to check the cloud configuration:

```bash
mdatp health --details cloud
```

Locate `ecs_configuration_version` in the output. The following value indicates that the cloud configuration isn't available:

```text
ecs_configuration_version : unavailable
```

If the value is `unavailable`, allow access to `https://config.edge.skype.com/config/v1`. For more information, see [Microsoft Defender for Endpoint streamlined connectivity URLs](streamlined-device-connectivity-urls-commercial#urls-used-for-core-functionality).