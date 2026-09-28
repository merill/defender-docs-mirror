---
layout: Conceptual
title: Microsoft Safety Scanner Download - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/safety-scanner-download
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Download Microsoft Safety Scanner to run a manual malware scan on Windows and reverse changes made by identified threats. See requirements and how to scan.
ms.reviewer: 
keywords: security, malware
ms.service: defender-endpoint
ms.subservice: reference
ms.mktglfcycl: secure
ms.sitesec: library
ms.localizationpriority: medium
ms.author: painbar
author: paulinbar
ms.collection:
- m365-security
- tier2
ms.topic: get-started
ms.date: 2025-04-04T00:00:00.0000000Z
locale: en-us
document_id: 514fb844-fe42-bdee-21ee-02255ad3c303
document_version_independent_id: 514fb844-fe42-bdee-21ee-02255ad3c303
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/safety-scanner-download.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: safety-scanner-download
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/safety-scanner-download.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
platformId: 3373db39-3958-b544-6943-c6c28529c950
---

# Microsoft Safety Scanner Download - Microsoft Defender for Endpoint | Microsoft Learn

Microsoft Safety Scanner is a scan tool designed to find and remove malware from Windows computers. Download it and run a scan to find malware and try to reverse changes made by identified threats.

- **[Download Microsoft Safety Scanner (32-bit)](https://go.microsoft.com/fwlink/?LinkId=212733)**
- **[Download Microsoft Safety Scanner (64-bit)](https://go.microsoft.com/fwlink/?LinkId=212732)**

Note

Safety Scanner is exclusively SHA-2 signed. Your devices must be updated to support SHA-2 in order to run Safety Scanner. To learn more, see [2019 SHA-2 Code Signing Support requirement for Windows and WSUS](https://support.microsoft.com/servicing/os/windows/2020/09/2019-sha-2-code-signing-support-requirement-for-windows-and-wsus).

## Important information

- The security intelligence update version of the Microsoft Safety Scanner matches the version described [in this web page](https://www.microsoft.com/wdsi/defenderupdates).
- Microsoft Safety Scanner only scans when manually triggered. Safety Scanner expires 10 days after being downloaded. To rerun a scan with the latest anti-malware definitions, download and run Safety Scanner again. We recommend that you always download the latest version of this tool before each scan.
- Safety Scanner is a portable executable and doesn't appear in the Windows Start menu or as an icon on the desktop. Note where you saved this download.
- This tool doesn't replace your anti-malware product. For real-time protection with automatic updates, use [Microsoft Defender Antivirus on Windows 11, Windows 10, and Windows 8](https://www.microsoft.com/windows/comprehensive-security). These anti-malware products also provide powerful malware removal capabilities. If you're having difficulties removing malware with these products, you can refer to our help on [removing difficult threats](https://www.microsoft.com/wdsi/help/troubleshooting-infection).

## System requirements

Safety Scanner helps remove malicious software from computers running Windows 11, Windows 10, Windows 10 Tech Preview, Windows 8.1, Windows 8, Windows 7, Windows Server 2019, Windows Server 2016, Windows Server Tech Preview, Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2. For details, refer to the [Microsoft Lifecycle Policy](/en-us/lifecycle/).

## How to run a scan

1. Download this tool and open it.
2. Select the type of scan that you want to run and start the scan.
3. Review the scan results displayed on screen. For detailed detection results, view the log at **%SYSTEMROOT%\debug\msert.log**.

To remove this tool, delete the executable file (msert.exe by default).

For more information about the Safety Scanner, see the support article on [how to troubleshoot problems using Safety Scanner](https://support.microsoft.com/Office/how-to-troubleshoot-an-error-when-you-run-the-microsoft-safety-scanner).

## Related resources

- [Troubleshooting Safety Scanner](https://support.microsoft.com/Office/how-to-troubleshoot-an-error-when-you-run-the-microsoft-safety-scanner)
- [Microsoft Defender Antivirus](https://www.microsoft.com/windows/comprehensive-security)
- [Removing difficult threats](https://support.microsoft.com/defender/troubleshoot-problems-with-detecting-and-removing-malware)
- [Submit file for malware analysis](https://www.microsoft.com/wdsi/filesubmission)
- [Microsoft anti-malware and threat protection solutions](microsoft-defender-endpoint)