---
layout: Conceptual
title: Investigate agent health issues - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/health-status
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn about the values returned when running the mdatp health command
ms.service: defender-endpoint
ms.author: chrisda
author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.topic: reference
ms.subservice: onboard
ms.date: 2024-11-04T00:00:00.0000000Z
locale: en-us
document_id: 6af51064-a3bb-74c3-7331-92b15474b813
document_version_independent_id: 6af51064-a3bb-74c3-7331-92b15474b813
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/health-status.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: health-status
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/health-status.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: c9d4a36e-97e5-ad77-778b-b0169ff598a0
---

# Investigate agent health issues - Microsoft Defender for Endpoint | Microsoft Learn

- [Microsoft Defender for Endpoint Plan 1](microsoft-defender-endpoint)
- [Microsoft Defender for Endpoint Plan 2](microsoft-defender-endpoint)
- [Microsoft Defender XDR](/en-us/defender-xdr)

The following table provides information about the values that are returned when you run the `mdatp health` command and their corresponding descriptions.

| Value | Description |
| --- | --- |
| `app_version` | Displays Microsoft Defender application version. |
| `automatic_definition_update_enabled` | `True` if automatic antivirus definition updates are enabled; otherwise, `false`. |
| `behavior_monitoring` | Feature to detect real time threats and prevention by monitoring the behavior of applications, services, and files.Can have one of the following values: - **disabled** - default - **enabled** |
| `cloud_automatic_sample_submission_consent` | Current sample submission level. Can have one of the following values: - **None**: No suspicious samples are submitted to Microsoft.- **safe**: Only suspicious samples that don't contain personal data are submitted automatically. This value is the default value for this setting.- **All**: All suspicious samples are submitted to Microsoft. |
| `cloud_diagnostic_enabled` | `True` if optional diagnostic data collection is enabled; otherwise, `false`. For more information related to Defender for Endpoint and other products and services like Microsoft Defender Antivirus and Windows, see [Microsoft Privacy Statement](https://go.microsoft.com/fwlink/?linkid=827576). |
| `cloud_enabled` | `True` if cloud-delivered protection is enabled; otherwise, `false`. |
| `conflicting_applications` | List of applications that are possibly conflicting with Microsoft Defender for Endpoint. This list includes, but isn't limited to, other security products and other applications known to cause compatibility issues. |
| `definitions_status` | Status of antivirus definitions. Can have one of the following values: - **up\_to\_date**- **updating**- **unavailable** |
| `definitions_updated` | Date and time of last antivirus definition update. |
| `definitions_updated_minutes_ago` | Number of minutes since last antivirus definition update. |
| `definitions_version` | Antivirus definition version. |
| `edr_client_version` | Version of the EDR client running on the device. |
| `edr_configuration_version` | EDR configuration version. |
| `edr_device_tags` | List of tags associated with the device. |
| `edr_early_preview_enabled` | Setting of edr early preview. Can have one of the following values: - **disabled**- **enabled** |
| `edr_group_ids` | Group ID that the device is associated with. |
| `edr_machine_id` | Device identifier used in the Microsoft Defender portal. |
| `engine_load_status` | Status of antivirus engine to determine whether it's running. Can have one of the following values: - **Engine not loaded** - antivirus engine process is down- **Engine load succeeded** - antivirus engine process is up and running |
| `engine_version` | Version of the antivirus engine. |
| `healthy` | `True` if the product is healthy; otherwise, `false`. |
| `health_issues` | Lists health issues if any. |
| `licensed` | `True` if the device is onboarded to a tenant; otherwise, `false`. |
| `log_level` | Current log level for the product. Can have one of the following values: - **info**- **debug** |
| `machine_guid` | Unique machine identifier used by the antivirus component. |
| `network_protection_enforcement_level` | Mode of network protection. Can have one of the following: - **disabled** - all components associated with network protection are disabled- **block** - network protection prevents connection to malicious websites- **audit** - Check how blocks occur |
| `network_protection_status` | Status of the network protection component (macOS only). Can have one of the following values: - **starting** - Network protection is starting- **failed\_to\_start** - Network protection couldn't be started due to an error- **started** - Network protection is running on the device- **restarting** - Network protection is restarting- **stopping** - Network protection is stopping- **stopped** - Network protection isn't running |
| `org_id` | Organization that the device is onboarded to. If the device isn't yet onboarded to any organization, it shows as `unavailable`. For more information on onboarding, see [Onboard to Microsoft Defender for Endpoint](onboarding). |
| `passive_mode_enabled` | `True` if the antivirus component is set to run in passive mode; otherwise, `false`. |
| `product_expiration` | Date and time when the current product version reaches end of support. |
| `real_time_protection_available` | `True` if the real-time protection component is healthy; otherwise, `false`. |
| `real_time_protection_enabled` | `True` if real-time antivirus protection is enabled; otherwise, `false`. |
| `real_time_protection_subsystem` | Subsystem used to serve real-time protection. If real-time protection isn't operating as expected, it shows as `unavailable`. |
| `release_ring` | Release ring. For more information, see [Deployment rings](onboarding). |
| `supplementary_events_subsystem` | Subsystem that provides supplementary event data. Can have one of the following values: - **ebpf** - Default from app version: `101.2408.0000`- **auditd** |

## Component specific health

You can get more detailed health information for different Defender's features with `mdatp health --details <feature>`. For example:

```bash

mdatp health --details edr

mdatp health --details definitions

mdatp health --details help

```

You can run `mdatp health --help` on recent versions to list all supported features.