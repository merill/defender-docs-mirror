---
layout: Conceptual
title: Protect your organization against web threats - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/web-threat-protection
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn about web protection in Microsoft Defender for Endpoint and how it can protect your organization.
ms.service: defender-endpoint
ms.author: lwainstein
author: limwainstein
ms.localizationpriority: medium
ms.date: 2026-07-03T00:00:00.0000000Z
ms.collection:
- m365-security
- tier2
- mde-asr
ms.topic: how-to
ms.subservice: asr
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 63898444-75a3-1cda-106a-69f79d1bff49
document_version_independent_id: 63898444-75a3-1cda-106a-69f79d1bff49
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/web-threat-protection.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: web-threat-protection
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/web-threat-protection.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5287f575-02f0-405f-92b7-800456526b0c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/06e86142-34c2-4b94-ab9c-9477c21f7152
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: a7389c3b-9efd-31ba-4068-a5f667f24ba6
---

# Protect your organization against web threats - Microsoft Defender for Endpoint | Microsoft Learn

Web threat protection is part of [Web protection](web-protection-overview) in Defender for Endpoint. It uses [network protection](network-protection) to secure your devices against web threats. By integrating with Microsoft Edge and popular third-party browsers like Chrome and Firefox, web threat protection stops web threats without a web proxy and can protect devices while they're away or on premises. Web threat protection stops access to phishing sites, malware vectors, exploit sites, untrusted or low-reputation sites, and sites that you've blocked because they're in your [custom indicator list](indicators-overview).

Before you configure web threat protection, review the Prerequisites section, which requires enabling network protection or Microsoft Defender SmartScreen.

Note

It might take up to two hours for devices to receive new custom indicators.

## Prerequisites

Web threat protection uses network protection to provide web browsing security in Edge (excepting Windows devices), non-Microsoft web browsers and nonbrowser processes. On Windows devices, web threat protection in Edge uses Microsoft Defender SmartScreen and network protection isn't required to be enabled.

To turn on Microsoft Defender SmartScreen in Edge: [Configure Microsoft Defender SmartScreen](/en-us/deployedge/microsoft-edge-policies#smartscreenenabled).

To turn on network protection on your devices:

- Edit the Defender for Endpoint security baseline under **Web & Network Protection** to enable network protection before deploying or redeploying it. [Learn about reviewing and assigning the Defender for Endpoint security baseline](configure-machines-security-baseline#review-and-assign-the-microsoft-defender-for-endpoint-security-baseline)
- Turn network protection on using Intune device configuration, SCCM, Group Policy, or your MDM solution. [Read more about enabling network protection](enable-network-protection)

Note

If you set network protection to **Audit only**, blocking is unavailable. Also, you are able to detect and log attempts to access malicious and unwanted websites on Microsoft Edge only.

## Configure web threat protection

The legacy **Web protection** policy in Intune has been deprecated and web threat protection is enabled if [network protection](enable-network-protection) or [Microsoft Defender SmartScreen](/en-us/deployedge/microsoft-edge-policies#smartscreenenabled) is enabled on your devices.