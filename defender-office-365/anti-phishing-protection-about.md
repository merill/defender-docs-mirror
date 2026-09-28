---
layout: Conceptual
title: Anti-phishing protection - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/anti-phishing-protection-about
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
ms.assetid: 75af74b2-c7ea-4556-a912-8c48e07271d3
ms.collection:
- m365-security
- tier2
ms.custom:
- TopSMBIssues
description: Admins can learn about the anti-phishing protection features in the default protections in Microsoft 365 and in Microsoft Defender for Office 365.
ms.service: defender-office-365
ms.date: 2025-07-01T00:00:00.0000000Z
locale: en-us
document_id: e9def5ec-772d-7cb2-6367-5dcd607a6179
document_version_independent_id: e9def5ec-772d-7cb2-6367-5dcd607a6179
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/anti-phishing-protection-about.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: anti-phishing-protection-about
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/anti-phishing-protection-about.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 2c9bb934-d508-3bdb-5c8c-59a8eab9d677
---

# Anti-phishing protection - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

*Phishing* is an email attack that tries to steal sensitive information in messages that appear to be from legitimate or trusted senders. There are specific categories of phishing. For example:

- **Spear phishing** uses focused, customized content that's specifically tailored to the targeted recipients (typically, after reconnaissance on the recipients by the attacker).
- **Whaling** is directed at executives or other high value targets within an organization for maximum effect.
- **Business email compromise (BEC)** uses forged trusted senders (financial officers, customers, trusted partners, etc.) to trick recipients into approving payments, transferring funds, or revealing customer data. Learn more by watching [this video](https://www.youtube.com/watch?v=8Kn31h9HwIQ&amp;list=PL3ZTgFEc7LystRja2GnDeUFqk44k7-KXf&amp;index=2).
- **Ransomware** that encrypts your data and demands payment to decrypt it almost always starts in phishing messages. Anti-phishing protection can't help you decrypt encrypted files, but it can help detect the initial phishing messages that are associated with the ransomware campaign. For more information about recovering from a ransomware attack, see [Ransomware incident response playbooks](/en-us/security/ransomware/).

With the growing complexity of attacks, it's even difficult for trained users to identify sophisticated phishing messages. Fortunately, [the built-in security features for all cloud mailboxes](eop-about) and [the additional features in Microsoft Defender for Office 365](/en-us/defender-office-365/mdo-about#defender-for-office-365-plan-1-vs-plan-2-cheat-sheet) can help.

## Anti-phishing protection for all cloud mailboxes

All organizations with cloud mailboxes contain the following features that help protect your organization from phishing threats:

- **Spoof intelligence**: Use the spoof intelligence insight to review detected spoofed senders in messages from external and internal domains, and manually allow or block those detected senders. For more information, see [Spoof intelligence insight](anti-spoofing-spoof-intelligence).
- **Anti-phishing policies for all cloud mailboxes**: Turn spoof intelligence on or off, turn unauthenticated sender indicators in Outlook on or off, and specify the action for blocked spoofed senders. For more information, see [Configure anti-phishing policies for all cloud mailboxes](anti-phishing-policies-eop-configure).

    **Honor the sender's DMARC policy when the message is detected as spoof**: Control what happens to messages where the sender fails explicit [DMARC](email-authentication-dmarc-configure) checks and the DMARC policy is set to `p=quarantine` or `p=reject`. For more information, see [Spoof protection and sender DMARC policies](anti-phishing-policies-about#spoof-protection-and-sender-dmarc-policies).
- **Allow or block spoofed senders in the Tenant Allow/Block List**: When you override the verdict in the spoof intelligence insight, the spoofed sender becomes a manual allow or block entry that only appears on the **Spoofed senders** tab on the **Tenant Allow/Block Lists** page at https://security.microsoft.com/tenantAllowBlockList?viewid=SpoofItem. You can also manually create allow or block entries for spoofed senders before spoof intelligence detects them. For more information, see [Spoofed senders in the Tenant Allow/Block List](tenant-allow-block-list-email-spoof-configure#spoofed-senders-in-the-tenant-allowblock-list).
- **Implicit email authentication**: Microsoft 365 enhances standard email authentication checks for inbound email ([SPF](email-authentication-spf-configure), [DKIM](email-authentication-dkim-configure), and [DMARC](email-authentication-dmarc-configure) with sender reputation, sender history, recipient history, behavioral analysis, and other advanced techniques to help identify forged senders. For more information, see [Email authentication](email-authentication-about).

## Additional anti-phishing protection in Microsoft Defender for Office 365

Microsoft Defender for Office 365 contains additional and more advanced anti-phishing features:

- **Anti-phishing policies in Microsoft Defender for Office 365**:
    - Configure impersonation protection settings for specific message senders and sender domains, mailbox intelligence settings, and adjustable phishing email thresholds. For more information, see [Configure anti-phishing policies in Microsoft Defender for Office 365](anti-phishing-policies-mdo-configure).
    - Details about detected impersonation attempts are available in the impersonation insight. For more information, see [Impersonation insight in Defender for Office 365](anti-phishing-mdo-impersonation-insight).
    - For more information about the differences between anti-phishing policies for all cloud mailboxes vs. anti-phishing policies in Defender for Office 365, see [Anti-phishing policies](anti-phishing-policies-about).
- **Campaign Views**: Machine learning and other heuristics identify and analyze messages that are involved in coordinated phishing attacks against the entire service and your organization. For more information, see [Campaign Views in Microsoft Defender for Office 365](campaigns).
- **Attack simulation training**: Admins can create fake phishing messages and send them to internal users as an education tool. For more information, see [Get started using Attack simulation training](attack-simulation-training-get-started).

## Other anti-phishing resources

- For end users: [Protect yourself from phishing schemes and other forms of online fraud](https://support.microsoft.com/office/be0de46a-29cd-4c59-aaaf-136cf177d593).
- [How Microsoft 365 validates the From address to prevent phishing](anti-phishing-from-email-address-validation).