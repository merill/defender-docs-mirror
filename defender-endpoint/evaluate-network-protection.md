---
layout: Conceptual
title: Evaluate network protection - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/evaluate-network-protection
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: See how network protection works by testing common scenarios that it protects against.
ms.service: defender-endpoint
ms.localizationpriority: medium
ms.topic: how-to
author: limwainstein
ms.author: lwainstein
ms.reviewer: yongrhee
ms.subservice: asr
ms.collection:
- m365-security
- tier2
- mde-asr
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 912db662-838c-15ac-610b-df9cb0737149
document_version_independent_id: 912db662-838c-15ac-610b-df9cb0737149
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/evaluate-network-protection.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: evaluate-network-protection
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/evaluate-network-protection.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 071d50be-a5b3-aba6-13cf-5c47fbb57111
---

# Evaluate network protection - Microsoft Defender for Endpoint | Microsoft Learn

## Overview

[Network protection](network-protection) helps prevent employees from using any application to access dangerous domains that might host phishing scams, exploits, and other malicious content on the Internet.

Use the following steps to evaluate network protection by enabling the feature and visiting a testing site. The sites referenced in this evaluation aren't malicious. They're specially created websites that pretend to be malicious. Each test site replicates the behavior that would happen if a user visited a malicious site or domain.

## Enable network protection in audit mode

Enable network protection in audit mode to see which IP addresses and domains might be blocked. You can make sure it doesn't affect line-of-business apps, or get an idea of how often blocks occur.

1. Type **powershell** in the Start menu, right-click **Windows PowerShell** and select **Run as administrator**.
2. Run the following cmdlet:

    ```PowerShell
    Set-MpPreference -EnableNetworkProtection AuditMode
    ```

### Visit a (fake) malicious domain

To verify audit mode behavior, visit a simulated malicious site and confirm that the connection is allowed with a test message.

1. Open Internet Explorer, Google Chrome, or any other browser of your choice.
2. Go to the [SmartScreen test ratings site](https://smartscreentestratings2.net).

    The network connection is allowed and a test message displays.

    [![The connection blockage notification](media/np-notif.png)](media/np-notif.png#lightbox)

Note

Network connections can be successful even though a site is blocked by network protection. To learn more, see [Network protection and the TCP three-way handshake](network-protection#network-protection-and-the-tcp-three-way-handshake).

## Review network protection events in Windows Event Viewer

To review blocked apps, open Event Viewer. Filter for Event ID 1125 in the Microsoft-Windows-Windows Defender/Operational log. The following table lists all network protection events.

| Event ID | Provide/Source | Description |
| --- | --- | --- |
| 5007 | Windows Defender (Operational) | Event when settings are changed |
| 1125 | Windows Defender (Operational) | Event when a network connection is audited |
| 1126 | Windows Defender (Operational) | Event when a network connection is blocked |

### Troubleshooting Network Protection

If network protection fails to detect malicious sites, make sure that the following prerequisites are enabled:

1. Microsoft Defender Antivirus is the primary antivirus app (active mode)
2. [Behavior Monitoring is enabled](behavior-monitor)
3. [Cloud Protection is enabled](cloud-protection-configure)
4. [Cloud Protection network connectivity is functional](configure-network-connections-microsoft-defender-antivirus)