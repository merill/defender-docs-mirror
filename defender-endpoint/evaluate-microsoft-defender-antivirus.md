---
layout: Conceptual
title: Evaluate Microsoft Defender Antivirus - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/evaluate-microsoft-defender-antivirus
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Businesses of all sizes can use this guide to evaluate and test the protection offered by Microsoft Defender Antivirus in Windows.
ms.service: defender-endpoint
ms.localizationpriority: medium
ms.topic: article
author: chrisda
ms.author: chrisda
ms.reviewer: yongrhee
ms.custom: nextgen
ms.date: 2025-10-20T00:00:00.0000000Z
ms.subservice: ngp
ms.collection:
- m365-security
- tier2
- mde-ngp
locale: en-us
document_id: 3adfff8b-0841-2920-893e-920c5f10695e
document_version_independent_id: 3adfff8b-0841-2920-893e-920c5f10695e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/evaluate-microsoft-defender-antivirus.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: evaluate-microsoft-defender-antivirus
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/evaluate-microsoft-defender-antivirus.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: c5f7cd60-d26f-3fb7-1f3d-f128209af154
---

# Evaluate Microsoft Defender Antivirus - Microsoft Defender for Endpoint | Microsoft Learn

Use this guide to determine how well Microsoft Defender Antivirus protects you from viruses, malware, and potentially unwanted applications. It explains the important next-generation protection features of Microsoft Defender Antivirus available for both small and large enterprises, and how they increase malware detection and protection across your network.

## Prerequisites

### Supported operating systems

- Windows

You can choose to configure and evaluate each setting independently, or all at once. We have grouped similar settings based upon typical evaluation scenarios, and include instructions for using PowerShell to enable the settings.

The guide is available:

- [Evaluate Microsoft Defender Antivirus using PowerShell](microsoft-defender-antivirus-using-powershell).

You can also download a PowerShell script that enables all the settings described in the guide automatically:

- [Download the PowerShell script to automatically configure the settings](https://aka.ms/wdeppscript).

Important

The guide is currently intended for single-machine evaluation of Microsoft Defender Antivirus. Enabling all of the settings in this guide may not be suitable for real-world deployment.

For the latest recommendations for real-world deployment and monitoring of Microsoft Defender Antivirus across a network, see [Deploy Microsoft Defender Antivirus](deploy-manage-report-microsoft-defender-antivirus).

Tip

If you're looking for Antivirus related information for other platforms, see:

> 
> - [Set preferences for Microsoft Defender for Endpoint on macOS](mac-preferences)
> - [Microsoft Defender for Endpoint on Mac](microsoft-defender-endpoint-mac)
> - [macOS Antivirus policy settings for Microsoft Defender Antivirus for Intune](/en-us/intune/intune-service/protect/antivirus-microsoft-defender-settings-macos)
> - [Set preferences for Microsoft Defender for Endpoint on Linux](linux-preferences)
> - [Microsoft Defender for Endpoint on Linux](microsoft-defender-endpoint-linux)
> - [Configure Defender for Endpoint on Android features](android-configure)
> - [Configure Microsoft Defender for Endpoint on iOS features](ios-configure-features)
>