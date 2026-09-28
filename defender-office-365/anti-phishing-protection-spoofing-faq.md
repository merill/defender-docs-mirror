---
layout: FAQ
title: Anti-spoofing protection FAQ - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/anti-phishing-protection-spoofing-faq
summary: >
  <div class="TIP">

  <p>Tip</p>

  <p><em>Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?</em> Use the 90-day Defender for Office 365 trial at the <a href="https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef">Microsoft Defender portal trials hub</a>. Learn about who can sign up and trial terms on <a href="/defender-office-365/try-microsoft-defender-for-office-365">Try Microsoft Defender for Office 365</a>.</p>

  </div>

  <p><strong>Applies to</strong></p>

  <ul>

  <li><a href="eop-about">Built-in security features for all cloud mailboxes</a></li>

  <li><a href="mdo-about#defender-for-office-365-plan-1-vs-plan-2-cheat-sheet">Microsoft Defender for Office 365 Plan 1 and Plan 2</a></li>

  <li><a href="/defender-xdr/microsoft-365-defender">Microsoft Defender XDR</a></li>

  </ul>

  <p>This article provides frequently asked questions and answers about anti-spoofing protection for all organizations with cloud mailboxes.</p>

  <p>For questions and answers about anti-spam protection, see <a href="anti-spam-protection-faq">Frequently asked questions: Anti-spam protection</a>.</p>

  <p>For questions and answers about anti-malware protection, see <a href="anti-malware-protection-faq">Frequently asked questions: Anti-malware protection</a></p>
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
f1.keywords:
- NOCSH
author: chrisda
ms.author: chrisda
ms.date: 2023-06-20T00:00:00.0000000Z
audience: ITPro
ms.topic: faq
ms.localizationpriority: medium
search.appverid:
- MET150
ms.collection:
- m365-security
- tier2
description: Admins can view frequently asked questions and answers about anti-spoofing protection in Microsoft 365.
ms.service: defender-office-365
locale: en-us
document_id: 6db24b2a-4880-c80d-8d29-0a82ddba8360
document_version_independent_id: 6db24b2a-4880-c80d-8d29-0a82ddba8360
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/anti-phishing-protection-spoofing-faq.yml
site_name: Docs
depot_name: Learn.defender-office-365
page_type: faq
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: anti-phishing-protection-spoofing-faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/anti-phishing-protection-spoofing-faq.yml
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: d690920d-e549-e25f-f3b6-88f8099ba35f
---

# Anti-spoofing protection FAQ - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

**Applies to**

- [Built-in security features for all cloud mailboxes](eop-about)
- [Microsoft Defender for Office 365 Plan 1 and Plan 2](mdo-about#defender-for-office-365-plan-1-vs-plan-2-cheat-sheet)
- [Microsoft Defender XDR](/en-us/defender-xdr/microsoft-365-defender)

This article provides frequently asked questions and answers about anti-spoofing protection for all organizations with cloud mailboxes.

For questions and answers about anti-spam protection, see [Frequently asked questions: Anti-spam protection](anti-spam-protection-faq).

For questions and answers about anti-malware protection, see [Frequently asked questions: Anti-malware protection](anti-malware-protection-faq)

## Why did Microsoft choose to junk unauthenticated inbound email?

Microsoft believes that the risk of continuing to allow unauthenticated inbound email is higher than the risk of losing legitimate inbound email.

## Does junking unauthenticated inbound email cause legitimate email to be marked as spam?

When Microsoft enabled this feature in 2018, some false positives happened (good messages were marked as bad). Over time, senders adjusted to the requirements. The number of messages that were misidentified as spoofed became negligible for most email paths.

Microsoft itself first adopted the new email authentication requirements several weeks before deploying it to customers. While there was disruption at first, it gradually declined.

## Is spoof intelligence available to Microsoft 365 customers without Defender for Office 365?

Yes. As of October 2018, spoof intelligence is available to all organizations with cloud mailboxes.

## How can I report spam or non-spam messages back to Microsoft?

See [Report messages and files to Microsoft](submissions-report-messages-files-to-microsoft).

## What happens if I disable anti-spoofing protection for my organization?

We don't recommend disabling anti-spoofing protection. Disabling the protection allows more delivered phishing and spam messages in your organization. Not all phishing is spoofing, and not all spoofed messages will be missed. However, your risk is higher.

Now that [Enhanced Filtering for Connectors](/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/enhanced-filtering-for-connectors) is available, we no longer recommended turning off anti-spoofing protection when your email is routed through a non-Microsoft service before arriving at Microsoft 365.

## Does anti-spoofing protection mean I'm protected from all phishing?

Unfortunately, no. Attackers constantly adapt to use other techniques (for example, compromised accounts or accounts in free email services). However, anti-phishing protection works better to detect these other types of phishing methods. The protection layers in Microsoft 365 are designed work together and build on top of each other.

## Do other large email services block unauthenticated inbound email?

Nearly all large email services implement traditional SPF, DKIM, and DMARC checks. Some services have other, more strict checks, but few go as far as Microsoft 365 to block unauthenticated email and treat them as spoofed messages. However, the industry is becoming more aware about issues with unauthenticated email, particularly because of the problem of phishing.

## Do I still need to enable the Advanced Spam Filter setting "SPF record: hard fail" ('MarkAsSpamSpfRecordHardFail') if I enable anti-spoofing?

No. This ASF setting is no longer required. Anti-spoofing protection considers both SPF hard fails and a wider set of criteria. If you have anti-spoofing enabled and the **SPF record: hard fail** (*MarkAsSpamSpfRecordHardFail*) turned on, you'll probably get more false positives.

We recommend that you disable this feature as it provides almost no additional benefit for detecting spam or phishing messages, and would instead generate mostly false positives. For more information, see [Advanced Spam Filter (ASF) settings in anti-spam policies](anti-spam-policies-asf-settings-about).

## Does Sender Rewriting Scheme help fix forwarded email?

SRS only partially fixes the problem of forwarded email. By rewriting the SMTP **MAIL FROM** value, SRS can ensure that the forwarded message passes SPF at the next destination. However, because anti-spoofing is based on the **From** address in combination with the **MAIL FROM** or DKIM-signing domain (or other signals), it's not enough to prevent SRS forwarded email from being marked as spoofed.