---
layout: Conceptual
title: Troubleshoot agent health issues with Defender for Endpoint on macOS - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/mac-health-status
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Investigate macOS Defender agent health issues
author: paulinbar
ms.author: painbar
ms.reviewer: lianx; joshbregman
ms.localizationpriority: medium
ms.service: defender-endpoint
ms.subservice: macos
ms.topic: troubleshooting-general
ms.date: 2025-06-06T00:00:00.0000000Z
ms.collection:
- m365-security
- tier3
- mde-macos
locale: en-us
document_id: 430644da-0660-7034-6ce1-846ec7a51dec
document_version_independent_id: 430644da-0660-7034-6ce1-846ec7a51dec
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/mac-health-status.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mac-health-status
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/mac-health-status.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 8fde2cc4-d1bc-680a-b6bd-8c493aed9fac
---

# Troubleshoot agent health issues with Defender for Endpoint on macOS - Microsoft Defender for Endpoint | Microsoft Learn

## Defender for Endpoint health status

The following table provides information about the values that are returned when you run the `mdatp health` command and their corresponding descriptions.

| Value | Description |
| --- | --- |
| `app_version` | Displays Microsoft Defender application version. |
| `automatic_definition_update_enabled` | `True` if automatic antivirus definition updates are enabled; otherwise, `false`. |
| `cloud_automatic_sample_submission_consent` | Current sample submission level. Can have one of the following values: - **None**: No suspicious samples are submitted to Microsoft.- **safe**: Only suspicious samples that don't contain personal data are submitted automatically. This value is the default value for this setting.- **All**: All suspicious samples are submitted to Microsoft. |
| `cloud_diagnostic_enabled` | `True` if optional diagnostic data collection is enabled; otherwise, `false`. For more information related to Defender for Endpoint and other products and services like Microsoft Defender Antivirus and Windows, see [Microsoft Privacy Statement](https://go.microsoft.com/fwlink/?linkid=827576). |
| `cloud_enabled` | `True` if cloud-delivered protection is enabled; otherwise, `false`. |
| `cloud_pin_certificate_thumbs` | pinned cloud certificate's thumbprints. |
| `conflicting_applications` | List of applications that are possibly conflicting with Microsoft Defender for Endpoint. This list includes, but isn't limited to, other security products and other applications known to cause compatibility issues. |
| `data_loss_prevention_status` | Status of data loss prevention. Can have one of the following values: - **unknown**- **unsupported\_os**- **unsupported\_os\_version**- **disabled**- **unhealthy**- **dormant**- **ready**- **active** |
| `definitions_status` | Status of antivirus definitions. Can have one of the following values: - **up\_to\_date**- **updating**- **unavailable** |
| `definitions_updated` | Date and time of last antivirus definition update. |
| `definitions_updated_minutes_ago` | Number of minutes since last antivirus definition update. |
| `definitions_version` | Antivirus definition version. |
| `edr_client_version` | Version of the EDR client running on the device. |
| `device_control_enforcement_level` | Device control activation statue. |
| `edr_configuration_version` | EDR configuration version. |
| `edr_device_tags` | List of tags associated with the device. |
| `edr_early_preview_enabled` | Setting of EDR early preview. Can have one of the following values: - **disabled**- **enabled** |
| `edr_group_ids` | Group ID that the device is associated with. |
| `edr_machine_id` | Device identifier used in the Microsoft Defender portal. |
| `engine_load_status` | Status of antivirus engine to determine whether it's running. Can have one of the following values: - **Engine not loaded** - antivirus engine process is down- **Engine load succeeded** - antivirus engine process is up and running |
| `engine_version` | Version of the antivirus engine. |
| `healthy` | `True` if the product is healthy; otherwise, `false`. |
| `health_issues` | Lists health issues if any. |
| `licensed` | `True` if the device is onboarded to a tenant; otherwise, `false`. |
| `log_level` | Current log level for the product. Can have one of the following values: - **info**- **debug** |
| `machine_guid` | Unique machine identifier used by the antivirus component. |
| `network_protection_enforcement_level` | Mode of network protection. Can have one of the following values: - **disabled** - all components associated with network protection are disabled- **block** - network protection prevents connection to malicious websites- **audit** - Check how blocks occur |
| `network_protection_status` | Status of the network protection component (macOS only). Can have one of the following values: - **starting** - Network protection is starting- **failed\_to\_start** - Network protection couldn't be started due to an error- **started** - Network protection is running on the device- **restarting** - Network protection is restarting- **stopping** - Network protection is stopping- **stopped** - Network protection isn't running |
| `org_id` | Organization that the device is onboarded to. If the device isn't yet onboarded to any organization, it shows as `unavailable`. For more information on onboarding, see [Onboard to Microsoft Defender for Endpoint](onboarding). |
| `passive_mode_enabled` | `True` if the antivirus component is set to run in passive mode; otherwise, `false`. |
| `product_expiration` | Date and time when the current product version reaches end of support. |
| `real_time_protection_available` | `True` if the real-time protection component is healthy; otherwise, `false`. |
| `real_time_protection_enabled` | `True` if real-time antivirus protection is enabled; otherwise, `false`. |
| `real_time_protection_subsystem` | Subsystem used to serve real-time protection. If real-time protection isn't operating as expected, it shows as `unavailable`. |
| `release_ring` | Release ring. For more information, see [Deployment rings](onboarding). |
| `tamper_protection` | Status of tamper protection feature. Can have one of the following values: - **disabled** - tamper protection is off.- **audit** - tamper protection is on but doesn't block any event.- **block** - tamper protection is monitoring events and block them as needed. |
| `troubleshooting_mode` | `True` if Defender for Endpoint is in troubleshooting mode; otherwise, `false`. see [Troubleshooting mode](mac-troubleshoot-mode). |

## Component specific health

You can get more detailed health information for different features in Defender for Endpoint by using the command, `mdatp health --details <feature>`. Here are some examples:

```bash

mdatp health --details permissions

mdatp health --details system_extensions

mdatp health --details edr

mdatp health --details definitions

mdatp health --details features

mdatp health --details help

```

You can run `mdatp health --help` on recent versions to list all supported features.