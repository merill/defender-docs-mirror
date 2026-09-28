---
layout: Conceptual
title: Run and customize scheduled and on-demand scans - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/customize-run-review-remediate-scans-microsoft-defender-antivirus
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Customize and initiate Microsoft Defender Antivirus scans on endpoints across your network
ms.service: defender-endpoint
ms.localizationpriority: medium
author: chrisda
ms.author: chrisda
ms.custom: nextgen
ms.date: 2025-03-26T00:00:00.0000000Z
ms.reviewer: yongrhee
ms.subservice: ngp
ms.topic: article
ms.collection:
- m365-security
- tier2
- mde-ngp
locale: en-us
document_id: 8eb11f2f-e00e-12e2-4931-9fccee751f89
document_version_independent_id: 8eb11f2f-e00e-12e2-4931-9fccee751f89
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/customize-run-review-remediate-scans-microsoft-defender-antivirus.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: customize-run-review-remediate-scans-microsoft-defender-antivirus
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/customize-run-review-remediate-scans-microsoft-defender-antivirus.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 1e554137-8d66-f573-17c9-d48815f55c3e
---

# Run and customize scheduled and on-demand scans - Microsoft Defender for Endpoint | Microsoft Learn

You can use Group Policy, PowerShell, and Windows Management Instrumentation (WMI) to configure Microsoft Defender Antivirus scans.

| Article | Description |
| --- | --- |
| [Configure and validate file, folder, and process-opened file exclusions in Microsoft Defender Antivirus scans](microsoft-defender-antivirus-exclusions-configure) | You can exclude files (including files modified by specified processes) and folders from on-demand scans, scheduled scans, and always-on real-time protection monitoring and scanning |
| [Configure Microsoft Defender Antivirus scanning options](configure-advanced-scan-types-microsoft-defender-antivirus) | You can configure Microsoft Defender Antivirus to include certain types of email storage files, back-up or reparse points, and archived files (such as .zip files) in scans. You can also enable network file scanning |
| [Configure remediation for scans](configure-remediation-microsoft-defender-antivirus) | Configure what Microsoft Defender Antivirus should do when it detects a threat, and how long quarantined files should be retained in the quarantine folder |
| [About scheduled scans](schedule-antivirus-scans) | Learn about recurring (scheduled) scans, including when they should run and whether they run as full or quick scans |
| [Configure and run scans](run-scan-microsoft-defender-antivirus) | Run and configure on-demand scans using PowerShell, Windows Management Instrumentation, or individually on endpoints with the Windows Security app |
| [Review scan results](review-scan-results-microsoft-defender-antivirus) | Review the results of scans using Microsoft Configuration Manager, Microsoft Intune, or the Windows Security app |