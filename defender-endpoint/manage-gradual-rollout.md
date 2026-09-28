---
layout: Conceptual
title: Manage the gradual rollout process for Microsoft Defender updates - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/manage-gradual-rollout
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how Microsoft Defender engine and platform updates roll out gradually through deployment rings, and how administrators can control update channels for their devices.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.reviewer: yongrhee
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.topic: how-to
ms.subservice: ngp
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: d6193c28-ff74-44a8-9cce-a983333db09b
document_version_independent_id: d6193c28-ff74-44a8-9cce-a983333db09b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/manage-gradual-rollout.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: manage-gradual-rollout
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/manage-gradual-rollout.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: fdb32ba4-3802-f074-b760-ed3f2d0383d5
---

# Manage the gradual rollout process for Microsoft Defender updates - Microsoft Defender for Endpoint | Microsoft Learn

It's important to ensure that client components are up to date to deliver critical protection capabilities and prevent attacks.

Capabilities are provided through several components:

- [Endpoint Detection & Response](overview-endpoint-detection-response)
- [Next-generation protection](microsoft-defender-antivirus-windows) with [cloud-delivered protection](cloud-protection-microsoft-defender-antivirus)
- [Attack Surface Reduction](attack-surface-reduction-overview)

Updates are released monthly using a gradual release process. The gradual release process helps enable early failure detection to identify issues as they occur and address them quickly before a larger rollout.

Note

For more information on how to control daily security intelligence updates, see [Schedule Microsoft Defender Antivirus protection updates](manage-protection-update-schedule-microsoft-defender-antivirus). Updates ensure that next-generation protection can defend against new threats, even if cloud-delivered protection is not available to the endpoint.

## Prerequisites

Make sure your environment meets the following requirements before configuring the gradual rollout process for Microsoft Defender updates.

### Supported operating systems

The following operating systems are supported:

- Windows

## Microsoft gradual rollout model

The following gradual rollout model is followed for monthly Defender updates:

1. The first release goes out to Beta channel subscribers.
2. After validation, feedback, and fixes, we start the gradual rollout process in a throttled way and to Preview channel subscribers first.
3. We then proceed to release the update to the rest of the global population, scaling out from 10-100%.

Our engineers continuously monitor impact and escalate any issues to create a fix as needed.

## How to customize your internal deployment process

If your machines are receiving Defender updates from Windows Update, the gradual rollout process can result in some of your devices receiving Defender updates sooner than others. You can define a strategy for routing automatic updates to specific device groups by using update channel configuration.

Note

When planning for your own gradual release, please make sure to always have a selection of devices subscribed to the preview and staged channels. This will provide your organization as well as Microsoft the opportunity to prevent or find and fix issues specific to your environment.

For machines receiving updates through, for example, Windows Server Update Services (WSUS) or Microsoft Configuration Manager, more options are available to all Windows updates, including options for Microsoft Defender for Endpoint.

- Learn more about how to use solutions such as WSUS and ConfigMgr to manage the distribution and application of updates at [Manage Microsoft Defender Antivirus updates and apply baselines - Windows security](microsoft-defender-antivirus-updates#product-updates).

## Update channels for monthly updates

You can assign a machine to an update channel to define the cadence in which a machine receives monthly engine and platform updates.

For more information on how to configure Defender update channels and the gradual rollout process, see [Create a custom gradual rollout process for Microsoft Defender updates](configure-updates).

The following update channels are available:

| Channel name | Description | Application |
| --- | --- | --- |
| Beta Channel - Prerelease | Test updates before others | Devices set to this channel are the first to receive new monthly updates. Select Beta Channel to participate in identifying and reporting issues to Microsoft. Devices in the Windows Insider Program are subscribed to this channel by default. For use in test environments only. |
| Current Channel (Preview) | Get Current Channel updates **earlier** during gradual release | Devices set to this channel are offered updates earliest during the gradual release cycle. Suggested for pre-production/validation environments. |
| Current Channel (Staged) | Get Current Channel updates later during gradual release | Devices are offered updates later during the gradual release cycle. Suggested to apply to a small, representative part of your device population (~10%). |
| Current Channel (Broad) | Get updates at the end of gradual release | Devices will be offered updates only after the gradual release cycle completes. Suggested to apply to a broad set of devices in your production population (~10-100%). |
| Critical: Time Delay | Delay Defender updates | Devices are offered updates with a 48-hour delay. Best for datacenter machines that only receive limited updates. Suggested for critical environments only. |
| (default) |  | If you disable or don't configure this policy, the device remains in Current Channel (Default): Stay up to date automatically during the gradual release cycle. This means Microsoft assigns a channel to the device. The channel selected by Microsoft might be one that receives updates early during the gradual release cycle, which isn't suitable for devices in a production or critical environment. |

### Update channels for security intelligence updates

You can also assign a machine to a channel to define the cadence in which it receives security intelligence updates, formerly referred to as signature, definition, or daily updates. Unlike the monthly process, this gradual release cycle occurs multiple times a day.

| Channel name | Description | Application |
| --- | --- | --- |
| Current Channel (Staged) | Get Current Channel updates earlier during gradual release | Devices are offered updates during the gradual release cycle. Suggested to apply to a small, representative part of your device population (~10%). |
| Current Channel (Broad) | Get updates at the end of gradual release | Devices will be offered updates after the gradual release cycle. Suggested to apply to a broad set of devices in all populations, including production. Note: this setting applies to all Defender updates. |
| (default) |  | If you disable or don't configure this policy, Microsoft will either assign the device to Current Channel (Broad) or a beta channel early in the gradual release cycle. The channel selected by Microsoft might be one that receives updates early during the gradual release cycle, which may not be suitable for devices in a production or critical environment. |

Note

If you want to force an update to the newest signature instead of leveraging the time delay, you must remove the security intelligence update channel policy first.

## Update guidance

In most cases, the recommended configuration when using Windows Update is to allow endpoints to receive and apply monthly Defender updates as they arrive. This option provides the best balance between protection and possible impact associated with the changes they can introduce.

For environments where there's a need for a more controlled gradual rollout of automatic Defender updates, consider an approach with deployment groups:

1. Participate in the Windows Insider program or assign a group of devices to the Beta Channel.
2. Designate a pilot group that opts in to Preview Channel, typically validation environments, to receive new updates early.
3. Designate a group of machines that receive updates later during the gradual rollout from Staged channel. Typically, this group would be a representative ~10% of the population.
4. Designate a group of machines that receive updates after the gradual release cycle completes. These are typically important production systems. For the remainder of devices, the default setting is to receive new updates as they arrive during the Microsoft gradual rollout process and no further configuration is required.

Adopting this deployment-group rollout model:

- Allows you to test early releases before they reach a production environment
- Ensure the production environment still receives regular updates and ensure protection against critical threats.

## Management tools

To create your own custom gradual rollout process for monthly updates, you can use the following tools:

- Group policy
- Microsoft Intune
- PowerShell

For details on how to use Group Policy, Microsoft Intune, and PowerShell, see [Create a custom gradual rollout process for Microsoft Defender updates](configure-updates).

Tip

If you're looking for Antivirus related information for other platforms, see:

- [Set preferences for Microsoft Defender for Endpoint on macOS](mac-preferences)
- [Microsoft Defender for Endpoint on Mac](microsoft-defender-endpoint-mac)
- [macOS Antivirus policy settings for Microsoft Defender Antivirus for Intune](/en-us/intune/intune-service/protect/antivirus-microsoft-defender-settings-macos)
- [Set preferences for Microsoft Defender for Endpoint on Linux](linux-preferences)
- [Microsoft Defender for Endpoint on Linux](microsoft-defender-endpoint-linux)
- [Configure Defender for Endpoint on Android features](android-configure)
- [Configure Microsoft Defender for Endpoint on iOS features](ios-configure-features)