---
layout: Conceptual
title: Feedback-loop blocking - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/feedback-loop-blocking
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Feedback-loop blocking, also called rapid protection, is part of behavioral blocking and containment capabilities in Microsoft Defender for Endpoint
keywords: behavioral blocking, rapid protection, feedback blocking, Microsoft Defender for Endpoint
author: chrisda
ms.author: chrisda
ms.reviewer: shwetaj
ms.topic: concept-article
ms.service: defender-endpoint
ms.localizationpriority: medium
ms.custom:
- next-gen
- mde-edr
ms.subservice: edr
ms.collection:
- m365-security
- tier2
ms.date: 2025-10-20T00:00:00.0000000Z
locale: en-us
document_id: dbecdc49-5fa0-1125-853b-8e47ff805ef5
document_version_independent_id: dbecdc49-5fa0-1125-853b-8e47ff805ef5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/feedback-loop-blocking.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: feedback-loop-blocking
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/feedback-loop-blocking.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/0850fefd-e402-4507-ae98-46cfdfc2e16c
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6ecf98a5-97c7-4249-b209-a9d9e42633a0
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: abd5f508-d339-76f2-c22f-d7b64f75f643
---

# Feedback-loop blocking - Microsoft Defender for Endpoint | Microsoft Learn

## Overview

Feedback-loop blocking, also referred to as rapid protection, is a component of [behavioral blocking and containment capabilities](behavioral-blocking-containment) in [Microsoft Defender for Endpoint](microsoft-defender-endpoint). With feedback-loop blocking, devices across your organization are better protected from attacks.

## Prerequisites

### Supported operating systems

- Windows

## How feedback-loop blocking works

When a suspicious behavior or file is detected, such as by [Microsoft Defender Antivirus in Windows](microsoft-defender-antivirus-windows), information about that artifact is sent to multiple classifiers. The rapid protection loop engine inspects and correlates the information with other signals to arrive at a decision as to whether to block a file. Checking and classifying artifacts happens quickly. It results in rapid blocking of confirmed malware, and drives protection across the entire ecosystem.

With rapid protection in place, an attack can be stopped on a device, other devices in the organization, and devices in other organizations, as an attack attempts to broaden its foothold.

## Configuring feedback-loop blocking

If your organization is using Defender for Endpoint, feedback-loop blocking is enabled by default. However, rapid protection occurs through a combination of Defender for Endpoint capabilities, machine learning protection features, and signal-sharing across Microsoft security services. Make sure the following features and capabilities of Defender for Endpoint are enabled and configured:

- [Microsoft Defender for Endpoint baselines](configure-machines-security-baseline)
- [Devices onboarded to Microsoft Defender for Endpoint](onboard-configure)
- [EDR in block mode](edr-in-block-mode)
- [Attack surface reduction](attack-surface-reduction-rules-overview)
- [Next-generation protection](configure-microsoft-defender-antivirus-features) (antivirus)

Tip

If you're looking for Antivirus related information for other platforms, see:

- [Set preferences for Microsoft Defender for Endpoint on macOS](mac-preferences)
- [Microsoft Defender for Endpoint on Mac](microsoft-defender-endpoint-mac)
- [macOS Antivirus policy settings for Microsoft Defender Antivirus for Intune](/en-us/intune/intune-service/protect/antivirus-microsoft-defender-settings-macos)
- [Set preferences for Microsoft Defender for Endpoint on Linux](linux-preferences)
- [Microsoft Defender for Endpoint on Linux](microsoft-defender-endpoint-linux)
- [Configure Defender for Endpoint on Android features](android-configure)
- [Configure Microsoft Defender for Endpoint on iOS features](ios-configure-features)