---
layout: FAQ
title: Software developer FAQ - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/developer-faq
summary: >
  <p>This page provides answers to common questions we receive from software developers. For general guidance about submitting malware or incorrectly detected files, read the submission guide.</p>
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
ms.date: 2022-03-18T00:00:00.0000000Z
description: This page provides answers to common questions we receive from software developers.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
audience: ITPro
ms.collection: m365-security
ms.topic: faq
locale: en-us
document_id: 10a7d99b-9658-2c8d-1bd0-72e77c0145ab
document_version_independent_id: 10a7d99b-9658-2c8d-1bd0-72e77c0145ab
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/developer-faq.yml
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: faq
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: developer-faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/developer-faq.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 98b20a41-cf53-4839-9dca-080ffa3dc61a
---

# Software developer FAQ - Microsoft Defender XDR | Microsoft Learn

This page provides answers to common questions we receive from software developers. For general guidance about submitting malware or incorrectly detected files, read the submission guide.

## Does Microsoft accept files for a known list or false-positive prevention program?

No. We don't accept these requests from software developers. Developers who signing their program's files in a consistent manner, with a digital certificate issued by a trusted root authority, helps our research team quickly identify the source of a program and apply previously gained knowledge. In some cases, this might result in your program being quickly added to the known list. Far less frequently, it adds your digital certificate to a list of trusted publishers.

## How do I dispute the detection of my program?

Submit the file in question as a software developer. Wait until your submission has a final determination.

If you're not satisfied with our determination of the submission, use the developer contact form provided with the submission results to reach Microsoft. We use the information you provide to investigate further if necessary.

We encourage all software vendors and developers to read about [how Microsoft identifies malware and Potentially Unwanted Applications (PUA)](/en-us/defender-xdr/criteria).

## Why is Microsoft asking for a copy of my program?

Providing copies can help us with our analysis. Participants of the [Microsoft Active Protection Service (MAPS)](https://www.microsoft.com/msrc/mapp) might occasionally receive these requests. The requests stop after our systems have received and processed the file.

## Why does Microsoft classify my installer as a software bundler?

It contains instructions to offer a program classified as unwanted software. You can review the [criteria](/en-us/defender-xdr/criteria) we use to check applications for behaviors that are considered unwanted.

## Why is the Windows Firewall blocking my program?

Firewall blocks aren't related to Microsoft Defender Antivirus and other Microsoft antimalware. [Learn about Windows Firewall](/en-us/windows/security/threat-protection/windows-firewall/windows-firewall-with-advanced-security).

## Why does the Microsoft Defender SmartScreen say my program isn't commonly downloaded?

Microsoft Defender SmartScreen isn't related to Microsoft Defender Antivirus and other Microsoft antimalware. [Learn about Microsoft Defender SmartScreen](/en-us/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview)