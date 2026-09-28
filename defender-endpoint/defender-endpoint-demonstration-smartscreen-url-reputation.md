---
layout: Conceptual
title: Microsoft Defender for Endpoint SmartScreen URL reputation demonstrations - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/defender-endpoint-demonstration-smartscreen-url-reputation
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Demonstrates how Microsoft Defender SmartScreen identifies phishing and malware websites based on URL reputation.
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
ms.date: 2025-03-04T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 60c580f1-1a9b-3681-b341-e1bfe5c85302
document_version_independent_id: 60c580f1-1a9b-3681-b341-e1bfe5c85302
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/defender-endpoint-demonstration-smartscreen-url-reputation.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defender-endpoint-demonstration-smartscreen-url-reputation
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/defender-endpoint-demonstration-smartscreen-url-reputation.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
platformId: 66eb9610-446c-b06e-f6f7-ab8e458dfd91
---

# Microsoft Defender for Endpoint SmartScreen URL reputation demonstrations - Microsoft Defender for Endpoint | Microsoft Learn

Test how Microsoft Defender SmartScreen helps you identify phishing and malware websites based on URL reputation.

## Prerequisites

- Client devices must be running Windows 11 or Windows 10
- Server devices must be running Windows Server 2008 R2 SP1, Windows Server 2012 R2 and later, or Azure Stack HCI OS, version 23H2 and later.
- Microsoft Edge browser required
- For more information, see [Microsoft Defender SmartScreen](/en-us/windows/security/operating-system-security/virus-and-threat-protection/microsoft-defender-smartscreen/)

## SmartScreen for Microsoft Edge URL scenario demonstrations

### Is This Phishing?

Alerts the user to a suspicious page and ask for feedback:

- [Is this Phishing?](https://demo.smartscreen.msft.net/other/areyousure.html)

    Launching this link should render a message similar to the following screenshot:

    ![SmartScreen alerts the user the site is potentially a phishing site and possibly unsafe](media/smartscreen-url-reputation-is-this-phishing.png)

### Phishing Page

A page known for phishing that should be blocked:

- [A known Phishing page](https://demo.smartscreen.msft.net/phishingdemo.html)

    Launching this link should render a message similar to the following example:

    ![SmartScreen reports the site is known for containing phishing threats](media/smartscreen-url-reputation-this-is-phishing.png)

### Malware page

A page that hosts malware and should be blocked:

- [A known malware page](https://demo.smartscreen.msft.net/other/malware.html)

    Launching this link should render a message similar to the following screenshot:

    ![SmartScreen alerts the user that the site is know for containing harmful programs](media/smartscreen-url-reputation-malware-page.png)

### Blocked download

Blocked from downloading because of its URL reputation

- [Download blocked due to URL reputation](https://demo.smartscreen.msft.net/download/malwaredemo/freevideo.exe)

    Launching this link should render a warning that the download was blocked as being unsafe by Microsoft Edge.

### Exploit page

A page that attacks a browser vulnerability

- [Known browser exploit page](https://demo.smartscreen.msft.net/other/exploit.html)

    Launching this link should render a message similar to the Malware page message.

### Malvertising

A benign page hosting a malicious advertisement

- [A page known to contain malicious advertisements](https://demo.smartscreen.msft.net/other/exploit_frame.html)

    Launching this link should render a message similar to the following screenshot:

    ![A demonstration of how SmartScreen responds to a frame on a page that is detected to be malicious. Only the malicious frame is blocked](media/smartscreen-url-reputation-malvertising.png)