---
layout: Conceptual
title: Spam confidence level - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/anti-spam-spam-confidence-level-scl-about
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: article
ms.localizationpriority: medium
ms.assetid: 34681000-0022-4b92-b38a-e32b3ed96bf6
ms.collection:
- m365-security
- tier2
ms.custom:
- seo-marvel-apr2020
- msecd-doc-authoring-1015
description: The spam confidence level (SCL) is a value that anti-spam filtering stamps on messages in Microsoft 365. Learn what SCL values mean in cloud organizations.
ms.service: defender-office-365
ms.date: 2026-08-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 4cc4ea03-31cf-2489-4143-c5c1a0739f91
document_version_independent_id: 4cc4ea03-31cf-2489-4143-c5c1a0739f91
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/anti-spam-spam-confidence-level-scl-about.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: anti-spam-spam-confidence-level-scl-about
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/anti-spam-spam-confidence-level-scl-about.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 87864dfc-3f26-1a37-1714-f90ccd987b15
---

# Spam confidence level - Microsoft Defender for Office 365 | Microsoft Learn

Historically, the spam confidence level (SCL) helped indicate whether spam filtering considered a message good or bad, or whether filtering was skipped on the message. Spam filtering stamps the SCL value (-1, or 0 to 9) on messages in the `X-Forefront-Antispam-Report` header. An SCL value of 5 or higher generally indicates the message is considered bad.

As the filtering stack evolved, particularly with the expansion into message categorization, the SCL value no longer holds the same meaning in cloud organizations. The value *doesn't* determine whether spam filtering identifies a message as **Spam** or **High confidence spam**, and it *doesn't* determine the action taken on the message. Spam filtering makes those decisions using categorization and other signals, so the same SCL value can appear on messages with different verdicts.

To understand how a message was handled, use other values in the message header. For example, `CAT` (category) identifies what filtered the message, and `DIR` (directionality) indicates whether the message was internal. For more information, see [Anti-spam message headers](message-headers-eop-mdo). For the actions that anti-spam policies take for each verdict, see [Actions in anti-spam policies](anti-spam-protection-about#actions-in-anti-spam-policies).

In the cloud, the primary use of SCL is mail flow rules (also known as transport rules) to [request a bypass from most spam filtering](/en-us/exchange/security-and-compliance/mail-flow-rules/use-rules-to-set-scl) (SCL -1), treat messages as spam (SCL 5 or 6), or treat messages as high confidence spam (SCL 9) based on specific criteria. But even when a rule requests a bypass, the actual SCL value stamped on the message might not be -1 (for example, 0 or 1 to indicate it was evaluated and found not to be spam).

The main purpose of the SCL value is to support *on-premises* Exchange servers, including hybrid environments where cloud-filtered messages are delivered to on-premises mailboxes. In on-premises Exchange, the SCL value is meaningful for the following anti-spam features:

- Delete, reject, and quarantine thresholds in the Content Filter agent on individual servers.
- The Junk Email threshold for the organization.
- The Junk Email threshold on individual mailboxes.
- SCL -1 handling in the Content Filter agent (the message is ignored).

For more information, see [Exchange spam confidence level (SCL) thresholds](/en-us/exchange/antispam-and-antimalware/antispam-protection/scl).

For troubleshooting information about spam filtering overrides, see [Spam verdict override behavior](anti-spam-policies-troubleshooting#spam-verdict-override-behavior). To identify which component filtered a specific message, see [Determine which component filtered the message](anti-spam-policies-troubleshooting#determine-which-component-filtered-the-message).

The bulk complaint level (BCL) identifies bad bulk email (also known as *gray mail*). A higher BCL value indicates the message is more likely to exhibit undesirable spam-like behavior. You configure the BCL threshold in anti-spam policies. For more information, see the following articles:

- [Configure anti-spam policies](anti-spam-policies-configure)
- [Bulk complaint level (BCL)](anti-spam-bulk-complaint-level-bcl-about)
- [What's the difference between junk email and bulk email?](anti-spam-spam-vs-bulk-about)

![The short icon for LinkedIn Learning.](media/eac8a413-9498-4220-8544-1e37d1aaea13.png)**New to Microsoft 365?** Discover free video courses for **Microsoft 365 admins and IT pros**, brought to you by LinkedIn Learning.