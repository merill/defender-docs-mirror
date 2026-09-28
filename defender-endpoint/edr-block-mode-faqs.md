---
layout: FAQ
title: Endpoint detection and response (EDR) in block mode frequently asked questions (FAQ) - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/edr-block-mode-faqs
summary: >
  <p><strong>Applies to:</strong></p>

  <ul>

  <li><a href="microsoft-defender-endpoint">Microsoft Defender for Endpoint Plan 2</a></li>

  <li><a href="/defender-xdr">Microsoft Defender XDR</a></li>

  </ul>
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Find answers to frequently asked questions about endpoint detection and response (EDR) in Microsoft Defender for Endpoint.
ms.service: defender-endpoint
ms.subservice: ngp
ms.localizationpriority: medium
audience: ITPro
author: paulinbar
ms.author: painbar
ms.reviewer: sugamar, kausd
ms.custom:
- asr
- partner-contribution
ms.topic: faq
ms.collection: m365-security
ms.date: 2025-05-22T00:00:00.0000000Z
locale: en-us
document_id: 32b89ad7-b326-db75-f38c-9f619072873e
document_version_independent_id: 32b89ad7-b326-db75-f38c-9f619072873e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/edr-block-mode-faqs.yml
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: faq
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: edr-block-mode-faqs
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/edr-block-mode-faqs.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: dd803ad3-e0b3-dd6d-b1d5-da3780912265
---

# Endpoint detection and response (EDR) in block mode frequently asked questions (FAQ) - Microsoft Defender for Endpoint | Microsoft Learn

**Applies to:**

- [Microsoft Defender for Endpoint Plan 2](microsoft-defender-endpoint)
- [Microsoft Defender XDR](/en-us/defender-xdr)

## Can I specify exclusions for EDR in block mode?

If you get a false positive, you can submit the file for analysis at the [Microsoft Security Intelligence submission site](https://www.microsoft.com/en-us/wdsi/filesubmission).

You can also define an exclusion for Microsoft Defender Antivirus. See [Configure and validate exclusions for Microsoft Defender Antivirus scans](microsoft-defender-antivirus-exclusions-configure).

## Do I need to turn EDR in block mode on if I have Microsoft Defender Antivirus running on devices?

No, Microsoft recommends disabling EDR in block mode, when the primary antivirus software on the system is Microsoft Defender Antivirus. The primary purpose of EDR in block mode is to remediate post-breach detections that were missed by a non-Microsoft antivirus product.

## Will EDR in block mode affect a user's antivirus protection?

EDR in block mode doesn't affect non-Microsoft antivirus protection running on users' devices. EDR in block mode works if the primary antivirus solution misses something, or if there's a post-breach detection. EDR in block mode works just like Microsoft Defender Antivirus in passive mode, except that EDR in block mode also blocks and remediates malicious artifacts or behaviors that are detected.

## Why do I need to keep Microsoft Defender Antivirus up to date?

Because Microsoft Defender Antivirus detects and remediates malicious items, it's important to keep it up to date. For EDR in block mode to be effective, it uses the latest device learning models, behavioral detections, and heuristics. The [Defender for Endpoint](microsoft-defender-endpoint) stack of capabilities works in an integrated manner. To get best protection value, you should keep Microsoft Defender Antivirus up to date. See [Manage Microsoft Defender Antivirus updates and apply baselines](microsoft-defender-antivirus-updates).

## Why do we need cloud protection (MAPS) on?

Cloud protection is needed to turn on the feature on the device. Cloud protection allows [Defender for Endpoint](microsoft-defender-endpoint) to deliver the latest and greatest protection based on our breadth and depth of security intelligence, along with behavioral and device learning models.

## What is the difference between active and passive mode?

For endpoints running Windows 10, Windows 11, Windows Server version 1803 or later, Windows Server 2019 and later, or Azure Stack HCI OS, version 23H2 and later, when Microsoft Defender Antivirus is in active mode, it's used as the primary antivirus on the device. When running in passive mode, Microsoft Defender Antivirus isn't the primary antivirus product. In this case, threats aren't remediated by Microsoft Defender Antivirus in real time.

Note

Microsoft Defender Antivirus can run in passive mode only when the device is onboarded to Microsoft Defender for Endpoint.

For more information, see [Microsoft Defender Antivirus compatibility](microsoft-defender-antivirus-compatibility).

## How do I confirm Microsoft Defender Antivirus is in active or passive mode?

To confirm whether Microsoft Defender Antivirus is running in active or passive mode, you can use Command Prompt or PowerShell on a device running Windows.

| Method | Procedure |
| --- | --- |
| PowerShell | 1. Select the Start menu, begin typing `PowerShell`, and then open Windows PowerShell in the results.2. Type `Get-MpComputerStatus`.3. In the list of results, in the **AMRunningMode** row, look for one of the following values:- `Normal`- `Passive Mode`To learn more, see [Get-MpComputerStatus](/en-us/powershell/module/defender/get-mpcomputerstatus). |
| Command Prompt | 1. Select the Start menu, begin typing `Command Prompt`, and then open Windows Command Prompt in the results.<br>2. Type `sc query windefend`.<br>3. In the list of results, in the **STATE** row, confirm that the service is running. |

## How do I confirm that EDR in block mode is turned on with Microsoft Defender Antivirus in passive mode?

You can use PowerShell to confirm that EDR in block mode is turned on with Microsoft Defender Antivirus running in passive mode.

1. Select the Start menu, begin typing `PowerShell`, and then open Windows PowerShell in the results.
2. Type `Get-MPComputerStatus|select AMRunningMode`.
3. Confirm that the result, `EDR Block Mode`, is displayed.

Tip

If Microsoft Defender Antivirus is in active mode, you'll see `Normal` instead of `EDR Block Mode`. To learn more, see [Get-MpComputerStatus](/en-us/powershell/module/defender/get-mpcomputerstatus).

## Is EDR in block mode supported on Windows Server 2016 and Windows Server 2012 R2?

If Microsoft Defender Antivirus is running in active mode or passive mode, EDR in block mode is supported of the following versions of Windows:

- Windows 11
- Windows 10 (all releases)
- Windows Server, version 1803 or newer
- Windows Server 2022
- Windows Server 2019
- Windows Server 2016 and Windows Server 2012 R2 (with the new unified client solution)

With the [new unified client solution](onboard-server#functionality-in-the-modern-unified-solution-for-windows-server-2016-and-windows-server-2012-r2) for Windows Server 2016 and Windows Server 2012 R2, you can run EDR in block mode in either passive mode or active mode.

Note

Windows Server 2016 and Windows Server 2012 R2 must be onboarded using the instructions in [Onboard Windows servers](onboard-server) for this feature to work.

## How much time does it take for EDR in block mode to be disabled?

If you choose to disable EDR in block mode, it can take up to 30 minutes for the system to disable this capability.