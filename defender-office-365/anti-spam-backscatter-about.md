---
layout: Conceptual
title: Backscatter in Microsoft 365 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/anti-spam-backscatter-about
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: concept-article
ms.localizationpriority: medium
ms.assetid: 6f64f2de-d626-48ed-8084-03cc72301aa4
ms.collection:
- m365-security
- tier2
ms.custom:
- seo-marvel-apr2020
description: In this article, admins can about backscatter and how Microsoft 365 tries to prevent it.
ms.service: defender-office-365
ms.date: 2025-07-02T00:00:00.0000000Z
locale: en-us
document_id: 10fd1abb-2ae2-5644-0986-d941a6e2b92c
document_version_independent_id: 10fd1abb-2ae2-5644-0986-d941a6e2b92c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/anti-spam-backscatter-about.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: anti-spam-backscatter-about
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/anti-spam-backscatter-about.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 47ff6d2d-080f-80c9-84d3-0a0eb2ff9c47
---

# Backscatter in Microsoft 365 - Microsoft Defender for Office 365 | Microsoft Learn

*Backscatter* is non-delivery reports (also known as NDRs or bounce messages) that you receive for messages you didn't send. Spammers often use real email addresses as the From address to lend credibility to their messages. When a nonexistent recipient receives spam, the destination email server unwittingly sends the NDR to the forged sender in the From address (also known as the `5322.From` address or P2 sender).

Microsoft 365 makes every effort to identify and silently drop messages from dubious sources without generating an NDR. But, it's almost impossible for Microsoft 365 to send absolutely no backscatter, based on the sheer volume email flowing through the service.

Backscatterer.org maintains a blocklist (also known as a DNS blocklist or DNSBL) of email servers that are responsible for sending backscatter. Their blocklist isn't a list of spammers, and Microsoft 365 servers might appear on their list.

Tip

The Backscatterer.org website (http://www.backscatterer.org/?target=usage) recommends using their service in Safe mode as large email services almost always send some backscatter.

The Advanced Spam Filter (ASF) in anti-spam policies has a setting to mark backscatter as spam, but this setting isn't required in most environments. For more information, see [ASF 'mark as spam' settings](anti-spam-policies-asf-settings-about#mark-as-spam-settings).