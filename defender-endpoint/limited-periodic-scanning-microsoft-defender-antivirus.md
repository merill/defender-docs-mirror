---
layout: Conceptual
title: Enable the limited periodic Microsoft Defender Antivirus scanning feature - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/limited-periodic-scanning-microsoft-defender-antivirus
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Enable limited periodic scanning on Windows 10 or Windows 11 so Microsoft Defender Antivirus can check for threats alongside another installed antivirus product. Includes important limitations for enterprise use.
ms.service: defender-endpoint
ms.localizationpriority: medium
ms.topic: how-to
author: chrisda
ms.author: chrisda
ms.custom: nextgen, msecd-doc-authoring-1016
ms.date: 2026-07-02T00:00:00.0000000Z
ms.reviewer: yongrhee
ms.subservice: ngp
ms.collection:
- m365-security
- tier3
- mde-ngp
ai-usage: ai-assisted
locale: en-us
document_id: 54159f18-5708-59cb-dfbb-11089d98a33f
document_version_independent_id: 54159f18-5708-59cb-dfbb-11089d98a33f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/limited-periodic-scanning-microsoft-defender-antivirus.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: limited-periodic-scanning-microsoft-defender-antivirus
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/limited-periodic-scanning-microsoft-defender-antivirus.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/e0ffb20c-01c6-407b-a9bd-29111652a1dc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/19ec6774-09b8-473e-a17e-b17b518bbad7
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/3904bce4-d817-48cf-85fd-b6146fca83b7
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ade36b61-c646-4bd8-87ee-f3a843461962
platformId: ba6ee834-abe3-dbe8-5b3b-f840d1b3adb0
---

# Enable the limited periodic Microsoft Defender Antivirus scanning feature - Microsoft Defender for Endpoint | Microsoft Learn

## Overview

Note

**Microsoft does not support this feature in enterprise settings.** This feature uses only a small part of Microsoft Defender Antivirus to find threats. It can't detect most malware or unwanted software. You can't manage this feature or control it through policies. Reporting is also limited. Microsoft recommends that enterprises pick one antivirus product and use it alone.

Limited periodic scanning is a threat detection mode that works when another antivirus product is installed on a Windows 10 or Windows 11 device. You can turn it on only in certain cases. This article covers the prerequisites and steps to enable limited periodic scanning on your device. For more information, see [Microsoft Defender Antivirus compatibility](microsoft-defender-antivirus-compatibility).

## Prerequisites

Before you enable limited periodic scanning, make sure your device meets the following requirements.

### Supported operating systems

Limited periodic scanning is supported on the following operating systems:

- Windows

## How to enable limited periodic scanning

By default, Microsoft Defender Antivirus turns on when no other antivirus product is installed on a Windows 10 or Windows 11 device. It also turns on if the other product is out-of-date, expired, or not working. When Microsoft Defender Antivirus is on, you can configure it as usual on that device:

[![The Windows Security app showing Microsoft Defender Antivirus options, including scan options, settings, and update options](media/vtp-wdav.png)](media/vtp-wdav.png#lightbox)

If another antivirus product is installed and working, Microsoft Defender Antivirus turns itself off. The Windows Security app then shows the status of the other antivirus product in the **Virus & threat protection** section. It also provides a link to that product's settings.

Below the non-Microsoft antivirus product name, select **Microsoft Defender Antivirus options**. Turn on the toggle to enable limited periodic scanning. When you slide the switch to **On**, the standard Microsoft Defender Antivirus options appear below the other product. The limited periodic scanning option is at the bottom of the page.