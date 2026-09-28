---
layout: Conceptual
title: Client behavioral blocking - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/client-behavioral-blocking
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Client behavioral blocking is part of behavioral blocking and containment capabilities at Microsoft Defender for Endpoint
author: limwainstein
ms.author: lwainstein
ms.reviewer: shwetaj
ms.topic: concept-article
ms.service: defender-endpoint
ms.subservice: ngp
ms.localizationpriority: medium
ms.custom:
- next-gen
- mde-ngp
ms.collection:
- m365-security
- tier2
ms.date: 2025-04-25T00:00:00.0000000Z
locale: en-us
document_id: 918d6c47-5a98-8fcb-2a88-b8db35ee7dfb
document_version_independent_id: 918d6c47-5a98-8fcb-2a88-b8db35ee7dfb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/client-behavioral-blocking.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: client-behavioral-blocking
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/client-behavioral-blocking.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: f3b9e1c0-8540-9aec-9b80-4e32cb28b917
---

# Client behavioral blocking - Microsoft Defender for Endpoint | Microsoft Learn

**Platform**

- Windows

## Overview

Client behavioral blocking is a component of [behavioral blocking and containment capabilities](behavioral-blocking-containment) in Defender for Endpoint. As suspicious behaviors are detected on devices (also referred to as clients or endpoints), artifacts (such as files or applications) are blocked, checked, and remediated automatically.

[![Cloud and client protection](media/pre-execution-and-post-execution-detection-engines.png)](media/pre-execution-and-post-execution-detection-engines.png#lightbox)

Antivirus protection works best when paired with cloud protection.

## How client behavioral blocking works

[Microsoft Defender Antivirus](microsoft-defender-antivirus-windows) can detect suspicious behavior, malicious code, fileless and in-memory attacks, and more on a device. When suspicious behaviors are detected, Microsoft Defender Antivirus monitors and sends those suspicious behaviors and their process trees to the cloud protection service. Machine learning differentiates between malicious applications and good behaviors within milliseconds, and classifies each artifact. In almost real time, as soon as an artifact is found to be malicious, it's blocked on the device.

Whenever a suspicious behavior is detected, an [alert](alerts-queue) is generated and is visible while the attack was detected and stopped; alerts, such as an "initial access alert," are triggered and appear in the [Microsoft Defender portal](/en-us/defender-xdr/microsoft-365-defender).

Client behavioral blocking is effective because it not only helps prevent an attack from starting, it can help stop an attack that has begun executing. And, with [feedback-loop blocking](feedback-loop-blocking) (another capability of behavioral blocking and containment), attacks are prevented on other devices in your organization.

## Behavior-based detections

Behavior-based detections are named according to the [MITRE ATT&CK Matrix for Enterprise](https://attack.mitre.org/matrices/enterprise). The naming convention helps identify the attack stage where the malicious behavior was observed:

| Tactic | Detection threat name |
| --- | --- |
| Initial Access | `Behavior:Win32/InitialAccess.*!ml` |
| Execution | `Behavior:Win32/Execution.*!ml` |
| Persistence | `Behavior:Win32/Persistence.*!ml` |
| Privilege Escalation | `Behavior:Win32/PrivilegeEscalation.*!ml` |
| Defense Evasion | `Behavior:Win32/DefenseEvasion.*!ml` |
| Credential Access | `Behavior:Win32/CredentialAccess.*!ml` |
| Discovery | `Behavior:Win32/Discovery.*!ml` |
| Lateral Movement | `Behavior:Win32/LateralMovement.*!ml` |
| Collection | `Behavior:Win32/Collection.*!ml` |
| Command and Control | `Behavior:Win32/CommandAndControl.*!ml` |
| Exfiltration | `Behavior:Win32/Exfiltration.*!ml` |
| Impact | `Behavior:Win32/Impact.*!ml` |
| Uncategorized | `Behavior:Win32/Generic.*!ml` |

Tip

To learn more about specific threats, see **[recent global threat activity](https://www.microsoft.com/wdsi/threats)**.

## Configuring client behavioral blocking

If your organization is using Defender for Endpoint, client behavioral blocking is enabled by default. However, to benefit from all Defender for Endpoint capabilities, including [behavioral blocking and containment](behavioral-blocking-containment), make sure the following features and capabilities of Defender for Endpoint are enabled and configured:

- [Defender for Endpoint baselines](configure-machines-security-baseline)
- [Devices onboarded to Defender for Endpoint](onboard-configure)
- [EDR in block mode](edr-in-block-mode)
- [Attack surface reduction](attack-surface-reduction-rules-overview)
- [Next-generation protection](configure-microsoft-defender-antivirus-features) (antivirus, antimalware, and other threat protection capabilities)

Tip

If you're looking for Antivirus related information for other platforms, see:

- [Set preferences for Microsoft Defender for Endpoint on macOS](mac-preferences)
- [Microsoft Defender for Endpoint on Mac](microsoft-defender-endpoint-mac)
- [macOS Antivirus policy settings for Microsoft Defender Antivirus for Intune](/en-us/intune/intune-service/protect/antivirus-microsoft-defender-settings-macos)
- [Set preferences for Microsoft Defender for Endpoint on Linux](linux-preferences)
- [Microsoft Defender for Endpoint on Linux](microsoft-defender-endpoint-linux)
- [Configure Defender for Endpoint on Android features](android-configure)
- [Configure Microsoft Defender for Endpoint on iOS features](ios-configure-features)