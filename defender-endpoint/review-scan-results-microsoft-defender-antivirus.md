---
layout: Conceptual
title: Review the results of Microsoft Defender Antivirus scans - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/review-scan-results-microsoft-defender-antivirus
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Review Microsoft Defender Antivirus scan results and detected threats using the Microsoft Defender portal, Intune, Configuration Manager, PowerShell, WMI, or the Windows Security app.
ms.service: defender-endpoint
ms.localizationpriority: medium
author: chrisda
ms.author: chrisda
ms.reviewer: yongrhee
ms.custom: nextgen, msecd-doc-authoring-1016
ms.date: 2026-09-15T00:00:00.0000000Z
ms.subservice: ngp
ms.topic: how-to
ms.collection:
- m365-security
- tier2
- mde-ngp
ai-usage: ai-assisted
locale: en-us
document_id: a9b67e3f-7bc9-f00f-6bd4-2fe8b9fc3966
document_version_independent_id: a9b67e3f-7bc9-f00f-6bd4-2fe8b9fc3966
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/review-scan-results-microsoft-defender-antivirus.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: review-scan-results-microsoft-defender-antivirus
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/review-scan-results-microsoft-defender-antivirus.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/a72e95ff-4b4f-4cc1-90c6-7dcba67ff05f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/24dc3ccd-591a-4415-a1fe-8759afafcb12
platformId: c74111b4-88e2-bf85-6609-b81551c3fce1
---

# Review the results of Microsoft Defender Antivirus scans - Microsoft Defender for Endpoint | Microsoft Learn

After a Microsoft Defender Antivirus scan completes, whether it's an [on-demand scan](run-scan-microsoft-defender-antivirus) or [scheduled antivirus scan](schedule-antivirus-scans), the results are recorded and you can view the results. This article explains how to review scan results, including detected threats and their details, using the Microsoft Defender portal, Microsoft Intune, Configuration Manager, PowerShell, or Windows Management Instrumentation (WMI).

## Prerequisites

### Supported operating systems

The following operating systems are supported:

- Windows

## Use Microsoft Defender to review scan results

To view the scan results using the Defender portal, follow these steps.

1. Sign in to [Microsoft Defender portal](https://security.microsoft.com)
2. Go to **Incidents & alerts** &gt; **Alerts**.

    You can view the scanned results under **Alerts**.

## Use Microsoft Intune to review scan results

Microsoft Intune is the recommended tool for configuring and distributing Defender for Endpoint features to devices. However, Intune is a separate product that isn't part of Defender for Endpoint, and it isn't included in all subscriptions. To use Intune, you need a subscription that includes it, or you can buy it separately as a standalone subscription or add-on. If you don't have Intune, you can use any of the other methods in this article. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).

To view the scan results using Microsoft Intune admin center, see [Antivirus agent status report](/en-us/intune/device-management/reports/overview#antivirus-agent-status-report-organizational) (opens in a new tab in the Intune documentation).

## Use Configuration Manager to review scan results

To view scan results in Configuration Manager, see [How to monitor Endpoint Protection status](/en-us/intune/configmgr/protect/deploy-use/monitor-endpoint-protection).

## Use PowerShell cmdlets to review scan results

To review recent threat detections recorded by Microsoft Defender Antivirus, run the following cmdlet. It returns each detection on the endpoint. If there are multiple detections of the same threat, each detection is listed separately, based on the time of each detection:

```PowerShell
Get-MpThreatDetection
```

[![The PowerShell cmdlets and outputs](/en-us/defender/media/wdav-get-mpthreatdetection.png)](/en-us/defender/media/wdav-get-mpthreatdetection.png#lightbox)

You can specify `-ThreatID` to limit the output to only show the detections for a specific threat.

To list threats currently known to Microsoft Defender Antivirus on the device, with multiple detections of the same threat combined into a single item, use the following cmdlet:

```PowerShell
Get-MpThreat
```

[![The PowerShell code](/en-us/defender/media/wdav-get-mpthreat.png)](/en-us/defender/media/wdav-get-mpthreat.png#lightbox)

See [Use PowerShell cmdlets to configure and run Microsoft Defender Antivirus](use-powershell-cmdlets-microsoft-defender-antivirus) and [Defender Antivirus cmdlets](/en-us/powershell/module/defender/) for more information on how to use PowerShell with Microsoft Defender Antivirus.

## Use Windows Management Instrumentation (WMI) to review scan results

Use the [**Get** method of the **MSFT\_MpThreat** and **MSFT\_MpThreatDetection**](/en-us/previous-versions/windows/desktop/defender/windows-defender-wmiv2-apis-portal) classes.

Tip

If you're looking for Antivirus related information for other platforms, see:

- [Set preferences for Microsoft Defender for Endpoint on macOS](mac-preferences)
- [Microsoft Defender for Endpoint on Mac](microsoft-defender-endpoint-mac)
- [macOS Antivirus policy settings for Microsoft Defender Antivirus for Intune](/en-us/intune/intune-service/protect/antivirus-microsoft-defender-settings-macos)
- [Set preferences for Microsoft Defender for Endpoint on Linux](linux-preferences)
- [Microsoft Defender for Endpoint on Linux](microsoft-defender-endpoint-linux)
- [Configure Defender for Endpoint on Android features](android-configure)
- [Configure Microsoft Defender for Endpoint on iOS features](ios-configure-features)