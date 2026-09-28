---
layout: Conceptual
title: Overview for how to troubleshoot performance issues for Microsoft Defender for Endpoint on macOS - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/mac-support-perf-overview
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Troubleshoot performance issues overview for Microsoft Defender for Endpoint on macOS.
author: paulinbar
ms.author: painbar
ms.reviewer: joshbregman
ms.service: defender-endpoint
ms.topic: overview
ms.localizationpriority: medium
ms.date: 2025-04-16T00:00:00.0000000Z
ms.subservice: macos
ms.custom: partner-contribution
locale: en-us
document_id: 6febc790-8b28-c1d8-7e57-1fbc47a081f7
document_version_independent_id: 6febc790-8b28-c1d8-7e57-1fbc47a081f7
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/mac-support-perf-overview.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mac-support-perf-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/mac-support-perf-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 3980f435-fbc5-1171-1243-2bd6a2317de4
---

# Overview for how to troubleshoot performance issues for Microsoft Defender for Endpoint on macOS - Microsoft Defender for Endpoint | Microsoft Learn

This article provides general guidelines to identify performance issues related to Microsoft Defender for Endpoint on macOS. See [Troubleshoot performance issues for Microsoft Defender for Endpoint on macOS](mac-support-perf) for more specific guidance.

Depending on the applications that you're running and your device characteristics, you might experience suboptimal performance when running Microsoft Defender for Endpoint on macOS. In particular, applications or system processes that access many resources over a short timespan can lead to performance issues in Microsoft Defender for Endpoint on macOS.

Tip

As a general best practice, it's recommended to [update the Microsoft Defender for Endpoint agent to latest available version](mac-whatsnew) and confirming that the issue still persists before investigating further.

Caution

Running other non-Microsoft endpoint protection products alongside Microsoft Defender for Endpoint on macOS is likely to lead to performance problems and unpredictable side effects. If non-Microsoft endpoint protection is an absolute requirement in your environment, you can configure Microsoft Defender Antivirus to run in **[Passive mode](mac-preferences)**. After you configure Passive mode, you can use Defender for Endpoint on macOS EDR functionality.

Warning

Before starting, make sure that other security products aren't currently running on the device. Multiple security products might conflict and affect system performance.

Tip

If you're running other non-Microsoft security products, make sure that the Microsoft Defender for Endpoint on macOS processes and paths are excluded from that non-Microsoft security product and that security product is excluded from Microsoft Defender for Endpoint on macOS. And vice-versa. When troubleshooting performance issues for Microsoft Defender for Endpoint on macOS, you should review the **Activity Monitor** or run **top** to see which of the three (3) processes is leading the high cpu utilization

| Daemon name | Component | Troubleshooting guide |
| --- | --- | --- |
| wdavdaemon | Core (privileged) | Open a [Microsoft support case](contact-support). |
| wdavdaemon\_unprivileged | Anti-malware (AV, EPP) | Review [Troubleshoot performance issues for Microsoft Defender for Endpoint on macOS](mac-support-perf). |
| wdavdaemon\_enterprise | Endpoint Detection and Response (EDR) | Open a [Microsoft support case](contact-support). |

Additionally, gather [Defender for Endpoint Client Analyzer](overview-client-analyzer) files while the issue occurs. This is used by the support team to investigate the issue.