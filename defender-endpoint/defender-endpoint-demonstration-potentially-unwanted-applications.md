---
layout: Conceptual
title: Microsoft Defender for Endpoint Potentially unwanted applications (PUA) demonstration - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/defender-endpoint-demonstration-potentially-unwanted-applications
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Demonstration to show how the Potentially Unwanted Applications (PUA) protection feature can identify and block PUAs from downloading and installing on endpoints.
ms.service: defender-endpoint
ms.author: lwainstein
author: limwainstein
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
- demo
ms.topic: article
ms.subservice: asr
ms.date: 2025-10-20T00:00:00.0000000Z
locale: en-us
document_id: cce49e1e-a0ca-74b9-3f9e-ddeddbed7a41
document_version_independent_id: cce49e1e-a0ca-74b9-3f9e-ddeddbed7a41
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/defender-endpoint-demonstration-potentially-unwanted-applications.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defender-endpoint-demonstration-potentially-unwanted-applications
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/defender-endpoint-demonstration-potentially-unwanted-applications.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: e8c36881-9bc3-4192-c146-9c7063b7be58
---

# Microsoft Defender for Endpoint Potentially unwanted applications (PUA) demonstration - Microsoft Defender for Endpoint | Microsoft Learn

The Potentially Unwanted Applications (PUA) protection feature in Microsoft Defender Antivirus can identify and block PUAs from downloading and installing on endpoints in your network. These applications aren't considered viruses, malware, or other types of threats, but might perform actions on endpoints that adversely affect their performance or use.

## Prerequsites

- Enable PUA protection. For more information, see the [Detect and block Potentially Unwanted Applications](detect-block-potentially-unwanted-apps-microsoft-defender-antivirus) article.
- You can also [download and use the PowerShell script](https://www.powershellgallery.com/packages/WindowsDefender_InternalEvaluationSettings/) to enable this setting and others.

### Supported operating systems

- Windows 11 or Windows 10
- Windows Server 2022
- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2008 R2 SP1
- macOS
- Linux

## Scenario

1. Go to http://www.amtso.org/feature-settings-check-potentially-unwanted-applications/
2. Click "Download the Potentially Unwanted Application 'test' file" link
3. After downloading the file, it's automatically blocked and prevented from running.