---
layout: Conceptual
title: Microsoft Defender for Endpoint SmartScreen app reputation demonstration - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/defender-endpoint-demonstration-app-reputation
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Test how Microsoft Defender for Endpoint SmartScreen helps you identify phishing and malware websites
ms.service: defender-endpoint
ms.subservice: ngp
ms.author: lwainstein
author: limwainstein
ms.reviewer: yongrhee
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
- demo
ms.topic: article
ms.date: 2025-10-20T00:00:00.0000000Z
locale: en-us
document_id: ce95a808-980e-84cb-8d38-5349ada0960f
document_version_independent_id: ce95a808-980e-84cb-8d38-5349ada0960f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/defender-endpoint-demonstration-app-reputation.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defender-endpoint-demonstration-app-reputation
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/defender-endpoint-demonstration-app-reputation.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
platformId: 5577a4f1-61c5-a908-71dc-a69f35b916e6
---

# Microsoft Defender for Endpoint SmartScreen app reputation demonstration - Microsoft Defender for Endpoint | Microsoft Learn

Test how Microsoft Defender for Endpoint SmartScreen helps you identify phishing and malware websites based on App reputation.

## Prerequisites

- Microsoft Edge or Internet Explorer browser required.

### Supported operating systems

- Windows 11
- Windows 10
- Windows Server 2016 and later
- Windows Server 2012 R2
- Windows Server 2008 R2
- Azure Stack HCI OS, version 23H2 and later.

## Scenario Demos

### Known good program

This program has a good reputation; the download should run uninterrupted:

- [Known good program download](https://demo.smartscreen.msft.net/download/known/freevideo.exe)

    Launching this link should render a message similar to the following:

    ![Based on the target file's reputation, SmartScreen allows the download without interference.](media/smartscreen-app-reputation-known-good.png)

### Unknown program

Because the program download doesn't have sufficient reputation to ensure that it's trustworthy, SmartScreen will show a warning before running the program download.

- [Unknown program](https://demo.smartscreen.msft.net/download/unknown/freevideo.exe)

    Launching this link should render a message similar to the following:

    ![SmartScreen doesn't have sufficient reputation information about the download file, and warns the user to stop or proceed with caution.](media/smartscreen-app-reputation-unknown.png)

### Known malware

This download is known malware; SmartScreen should block this program from running.

- [Known malware](https://demo.smartscreen.msft.net/download/known/knownmalicious.exe)

    Launching this link should render a message similar to the following:

    ![Screenshot showing how SmartScreen detects a file download with an unsafe reputation; the download is blocked.](media/smartscreen-app-reputation-known-malware.png)

## Learn more

[Microsoft Defender SmartScreen Documentation](/en-us/windows/security/operating-system-security/virus-and-threat-protection/microsoft-defender-smartscreen/)