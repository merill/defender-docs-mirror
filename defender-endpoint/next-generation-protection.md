---
layout: Conceptual
title: Overview of next-generation protection in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/next-generation-protection
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Get an overview of next-generation protection in Microsoft Defender for Endpoint. Reinforce the security perimeter of your network by using next-generation protection designed to catch all types of emerging threats.
ms.service: defender-endpoint
ms.localizationpriority: high
ms.topic: concept-article
author: paulinbar
ms.author: painbar
ms.reviewer: yongrhee
ms.custom: nextgen
ms.subservice: ngp
ms.collection:
- m365-security
- tier1
- mde-ngp
ms.date: 2025-03-26T00:00:00.0000000Z
locale: en-us
document_id: 9fb4b609-74f7-7205-7ee7-396066192df4
document_version_independent_id: 9fb4b609-74f7-7205-7ee7-396066192df4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/next-generation-protection.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: next-generation-protection
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/next-generation-protection.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 23fe0d01-8e60-8697-7edd-ea1e8c072e0c
---

# Overview of next-generation protection in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Microsoft Defender for Endpoint includes next-generation protection to catch and block all types of emerging threats. The majority of modern malware is polymorphic, meaning it constantly mutates to evade detection. As soon as one variant is identified, another takes its place. This rapid evolution underscores the need for agile and innovative security solutions.

Next-generation protections, such as [Microsoft Defender Antivirus](microsoft-defender-antivirus-windows) blocks malware using local and cloud-based machine learning models, behavior analysis, and heuristics. Microsoft Defender Antivirus uses predictive technologies, machine learning, applied science, and artificial intelligence to detect and block malware at the first sign of abnormal behavior.

In addition to Microsoft Defender Antivirus, your next-generation protection services include the following capabilities:

- [Behavior-based, heuristic, and real-time antivirus protection](configure-protection-features-microsoft-defender-antivirus), which includes always-on scanning using file and process behavior monitoring and other heuristics (also known as *real-time protection*). It also includes detecting and blocking apps that are deemed unsafe, but might not be detected as malware.
- [Cloud-delivered protection](cloud-protection-microsoft-defender-antivirus), which includes near-instant detection and blocking of new and emerging threats.
- [AI agent runtime protection](ai-agent-runtime-protection-overview), which monitors activity in the agentic loop and blocks attacks targeting local AI agents running on your devices.
- [Dedicated protection and product updates](microsoft-defender-antivirus-updates), which includes updates related to keeping Microsoft Defender Antivirus up to date.

Next-generation protection is included in both [Defender for Endpoint Plan 1 and Plan 2](microsoft-defender-endpoint). Next-generation protection is also included in [Microsoft Defender for Business](/en-us/defender-business/mdb-overview) and [Microsoft 365 Business Premium](/en-us/microsoft-365/business-premium/m365bp-overview).

To configure next-generation protection services, see [Configure Microsoft Defender Antivirus features](configure-microsoft-defender-antivirus-features).

If you're looking for Microsoft Defender Antivirus-related information for other platforms, see one of the following articles:

- [Set preferences for Microsoft Defender for Endpoint on macOS](mac-preferences)
- [Microsoft Defender for Endpoint on Mac](microsoft-defender-endpoint-mac)
- [macOS Antivirus policy settings for Microsoft Defender Antivirus for Intune](/en-us/intune/intune-service/protect/antivirus-microsoft-defender-settings-macos)
- [Set preferences for Microsoft Defender for Endpoint on Linux](linux-preferences)
- [Microsoft Defender for Endpoint on Linux](microsoft-defender-endpoint-linux)
- [Configure Defender for Endpoint on Android features](android-configure)
- [Configure Microsoft Defender for Endpoint on iOS features](ios-configure-features)

Tip

**Performance tip** Due to a variety of factors (examples listed below) Microsoft Defender Antivirus, like other antivirus software, can cause performance issues on endpoint devices. In some cases, you might need to tune the performance of Microsoft Defender Antivirus to alleviate those performance issues. Microsoft's **Performance analyzer** is a PowerShell command-line tool that helps determine which files, file paths, processes, and file extensions might be causing performance issues; some examples are:

- Top paths that impact scan time
- Top files that impact scan time
- Top processes that impact scan time
- Top file extensions that impact scan time
- Combinations – for example:
    - top files per extension
    - top paths per extension
    - top processes per path
    - top scans per file
    - top scans per file per process

You can use the information gathered using Performance analyzer to better assess performance issues and apply remediation actions. See [Performance analyzer for Microsoft Defender Antivirus](tune-performance-defender-antivirus).