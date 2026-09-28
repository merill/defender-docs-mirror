---
layout: Conceptual
title: Protect Microsoft Defender Antivirus exclusions - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/tamper-protection-antivirus-exclusions
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
ms.reviewer: joshbregman, mattcall, pahuijbr, hayhov, oogunrinde
description: Review the requirements for protecting Microsoft Defender Antivirus exclusions with tamper protection, and verify protection on Windows devices.
ms.service: defender-endpoint
ms.localizationpriority: medium
ms.date: 2026-09-08T00:00:00.0000000Z
ms.topic: how-to
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
document_id: 5101f6ac-976f-5fa1-53d3-7db67dfff2a1
document_version_independent_id: 5101f6ac-976f-5fa1-53d3-7db67dfff2a1
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/tamper-protection-antivirus-exclusions.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: tamper-protection-antivirus-exclusions
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/tamper-protection-antivirus-exclusions.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: fd54d6b1-8cac-d28c-1fd9-224952a7ebc2
---

# Protect Microsoft Defender Antivirus exclusions - Microsoft Defender for Endpoint | Microsoft Learn

On Windows devices, tamper protection can prevent unauthorized changes to organization-managed [Microsoft Defender Antivirus exclusions](microsoft-defender-antivirus-exclusions-configure). Review the requirements for protecting exclusions, and use Registry Editor to verify that protection is active. For an overview of how tamper protection exclusions differ between Windows and macOS, see [Tamper protection exclusions](tamper-protection-overview#tamper-protection-exclusions).

## Requirements for protecting antivirus exclusions

Meet the following requirements:

- **Microsoft Defender platform**: Devices run platform version `4.18.2211.5` (November 2022) or later. See [Monthly platform and engine versions](microsoft-defender-antivirus-updates#platform-and-engine-releases).
- **`DisableLocalAdminMerge` setting**: Enable `DisableLocalAdminMerge` to prevent locally configured settings from merging with organization policies. See [DisableLocalAdminMerge](/en-us/windows/client-management/mdm/defender-csp#configurationdisablelocaladminmerge).
- **Device management**: Devices are managed only by Intune or only by Configuration Manager, and the Microsoft Defender for Endpoint sensor (Sense) is enabled.
- **Antivirus exclusions**: Exclusions are managed in Intune or Configuration Manager. See [Microsoft Defender Antivirus policy settings for Windows devices](/en-us/intune/intune-service/protect/antivirus-microsoft-defender-settings-windows). The exclusion protection feature is enabled on devices. See Verify that antivirus exclusions are tamper protected.

Note

If Configuration Manager is the only tool that manages exclusions and all requirements are met, the exclusions are tamper protected. You don't also need to deploy exclusions through Intune.

You don't need to disable tamper protection to apply new exclusion policy settings from Intune or Configuration Manager.

For more information about antivirus exclusions, see [Microsoft Defender for Endpoint and Microsoft Defender Antivirus exclusions](defender-endpoint-exclusions-overview).

## Verify that antivirus exclusions are tamper protected

Use Registry Editor to verify whether Microsoft Defender Antivirus exclusions are tamper protected.

Caution

Don't change the registry values. Use this procedure to view the values only.

1. Open Registry Editor on a Windows device.
2. To verify that only Intune or only Configuration Manager manages the device and that the Defender for Endpoint sensor is enabled, check the following registry values:

    - `ManagedDefenderProductType` in `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Defender` or `HKLM\SOFTWARE\Microsoft\Windows Defender`.
    - `EnrollmentStatus` in `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SenseCM` or `HKLM\SOFTWARE\Microsoft\SenseCM`.

    Use the following table to interpret the values:

    | ManagedDefenderProductType | EnrollmentStatus | Description |
    | --- | --- | --- |
    | `6` | Any value | The device is managed only with Intune and meets the device-management requirement. |
    | `7` | `4` | The device is managed with Configuration Manager and meets the device-management requirement. |
    | `7` | `3` | The device is co-managed with Configuration Manager and Intune. This configuration isn't supported for tamper-protected exclusions. |
    | A value other than `6` or `7` | Any value | The device isn't managed only with Intune or only with Configuration Manager. Exclusions aren't tamper protected. |
3. To confirm that tamper protection is deployed and exclusions are tamper protected, check the `TPExclusions` value in `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Defender\Features` or `HKLM\SOFTWARE\Microsoft\Windows Defender\Features`.

    Use the following table to interpret the value:

    | TPExclusions | Description |
    | --- | --- |
    | `1` | The requirements are met, and exclusions are tamper protected. |
    | `0` | Tamper protection isn't protecting exclusions. If all requirements are met and this state seems incorrect, contact support. |