---
layout: Conceptual
title: Create allowlists - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/create-safe-sender-lists-in-office-365
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: how-to
ms.collection:
- m365-security
- tier2
ms.localizationpriority: medium
ms.assetid: 9721b46d-cbea-4121-be51-542395e6fd21
ms.custom:
- msecd-doc-authoring-1016
- seo-marvel-apr2020
description: Admins can learn about the available and preferred options to allow inbound messages to Microsoft 365.
ms.service: defender-office-365
ms.date: 2026-07-24T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 813fea63-0d52-0bdb-7336-37a3bf9cee21
document_version_independent_id: 813fea63-0d52-0bdb-7336-37a3bf9cee21
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/create-safe-sender-lists-in-office-365.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: create-safe-sender-lists-in-office-365
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/create-safe-sender-lists-in-office-365.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
platformId: 4365e4a6-5713-a21b-0179-6915d4c7a099
---

# Create allowlists - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

All organizations with cloud mailboxes offer multiple ways of allowing inbound email from trusted senders. Collectively, you can think of these options as *allowlists*.

The following list contains the available methods to allow senders from most recommended to least recommended:

1. Allow entries for domains and email addresses (including spoofed senders) in the Tenant Allow/Block List.
2. Exchange mail flow rules (also known as transport rules).
3. Outlook Safe Senders (the Safe Senders list in each mailbox that affects only that mailbox).
4. IP Allow List in the default connection filter policy.
5. Allowed sender lists or allowed domain lists in anti-spam policies.

The following sections describe each allowlist method in detail, including the Tenant Allow/Block List, mail flow rules, Outlook Safe Senders, the IP Allow List, and allowed sender or domain lists in anti-spam policies.

Important

Messages that are identified as malware^\*^ or high confidence phishing are always quarantined, regardless of the allowlist option you use. For more information, see [Secure by default in Office 365](secure-by-default).

^\*^ Malware filtering is skipped on SecOps mailboxes that are identified in the advanced delivery policy. For more information, see [Configure the advanced delivery policy for non-Microsoft phishing simulations and email delivery to SecOps mailboxes](advanced-delivery-policy-configure).

Be careful to closely monitor *any* exceptions to spam filtering using allowed sender or allowed domain lists.

Always submit messages in your allowlists to Microsoft for analysis. For instructions, see [Report good email to Microsoft](submissions-admin#report-good-email-to-microsoft). If the messages or message sources are determined to be benign, Microsoft can automatically stop blocking the messages, and you don't need to manually maintain entries in your own allowlists.

Instead of allowing email, you also have several options to block email from specific sources using *blocked sender lists*. For more information, see [Create sender blocklists](create-block-sender-lists-in-office-365).

## Use allow entries in the Tenant Allow/Block List

Our number one recommended option for allowing mail from senders or domains is the Tenant Allow/Block List. For instructions, see [Create allow entries for domains and email addresses](tenant-allow-block-list-email-spoof-configure#create-allow-entries-for-domains-and-email-addresses) and [Create allow entries for spoofed senders](tenant-allow-block-list-email-spoof-configure#create-allow-entries-for-spoofed-senders).

Only consider other allow methods (mail flow rules, Outlook Safe Senders, IP Allow List, or allowed sender/domain lists in anti-spam policies) if you can't use allow entries in the Tenant Allow/Block List for some reason.

## Use mail flow rules

Note

You can't use message headers and mail flow rules to designate an internal sender as a safe sender. The procedures in this section work for external senders only.

Mail flow rules in Exchange Online use conditions and exceptions to identify messages, and actions to specify what should be done to those messages. For more information, see [Mail flow rules (transport rules) in Exchange Online](/en-us/Exchange/security-and-compliance/mail-flow-rules/mail-flow-rules).

To create a mail flow rule that bypasses spam filtering, follow the steps in [Use mail flow rules to set the spam confidence level (SCL) in messages](/en-us/exchange/security-and-compliance/mail-flow-rules/use-rules-to-set-scl). To safely allow senders, use the conditions and actions described in this section.

The following example assumes you need email from contoso.com to skip spam filtering. Configure the following settings:

1. **Apply this rule if** (condition): **The sender** &gt; **domain is** &gt; contoso.com.
2. Configure either of the following settings:

    - **Apply this rule if** (extra condition): **The message headers** &gt; **includes any of these words**:

        - **Enter text** (header name): `Authentication-Results`
        - **Enter words** (header value): `dmarc=pass` or `dmarc=bestguesspass` (add both values).

        This condition checks the email authentication status of the sending email domain to ensure that the sending domain isn't being spoofed. For more information about email authentication, see [Email authentication](email-authentication-about).
    - **IP Allow List**: Specify the source IP address or address range in the default connection filter policy. For instructions, see [Configure connection filtering](connection-filter-policies-configure).

        Use this setting if the sending domain doesn't use email authentication. Be as restrictive as possible when it comes to the source IP addresses in the IP Allow List. We recommend an IP address range of /24 or less (less is better). Don't use IP address ranges that belong to consumer services (for example, outlook.com) or shared infrastructures.

    Important

    - Never configure mail flow rules with *only* the sender domain as the condition to skip spam filtering. Doing so *significantly* increases the likelihood that attackers can:

        - Spoof the sending domain (or impersonate the full email address).
        - Skip all spam filtering.
        - Skip sender authentication checks so the message arrives in the recipient's Inbox.
    - Don't use domains you own (also known as accepted domains) or popular domains (for example, microsoft.com) as conditions in mail flow rules. Doing so creates opportunities for attackers to send email that would otherwise be filtered.
    - If you allow an IP address behind a network address translation (NAT) gateway, you need to know all servers involved in the NAT pool. IP addresses and NAT participants can change. Periodically check your IP Allow List entries as part of your standard maintenance procedures.
3. **Optional conditions**:

    - **The sender** &gt; **is internal/external** &gt; **Outside the organization**: This condition is implicit, but it's OK to use it to account for on-premises email servers that might not be correctly configured.
    - **The subject or body** &gt; **subject or body includes any of these words** &gt; &lt;keywords&gt;: If you can further restrict the messages by keywords or phrases in the subject line or message body, you can use those words as a condition.
4. **Do the following** (actions): Configure both of the following actions in the rule:

    1. **Modify the message properties** &gt; **set the spam confidence level (SCL)** &gt; **Bypass spam filtering**.
    2. **Modify the message properties** &gt; **set a message header**:

        - **Enter text** (header name): For example, `X-ETR`.
        - **Enter words** (header value): For example, `Bypass spam filtering for authenticated sender 'contoso.com'`.

        For a mail flow rule that includes more than one domain, you can customize the header text as appropriate.

When a message skips spam filtering due to a mail flow rule, the value `SFV:SKN` value is stamped in the **X-Forefront-Antispam-Report** header. If the message is from a source that's on the IP Allow List, the value `IPV:CAL` is also added. These values can help you with troubleshooting.

[![Example mail flow rule settings in the new EAC to bypassing spam filtering.](media/1-allowlist-skipfilteringfromcontoso.png)](media/1-allowlist-skipfilteringfromcontoso.png#lightbox)

## Use Outlook Safe Senders

Caution

This method creates a high risk of attackers successfully delivering email that would otherwise be filtered. Messages determined to be malware or high confidence phishing are filtered. For more information, see [When user and organization settings conflict](how-policies-and-protections-are-combined#when-user-and-organization-settings-conflict).

Instead of an organizational setting, users or admins can add the sender email addresses to the Safe Senders list in the mailbox. Safe Senders list entries in the mailbox affect that mailbox only. For user instructions, see [Add recipients of my email messages to the Safe Senders List](https://support.microsoft.com/office/be1baea0-beab-4a30-b968-9004332336ce). For admin instructions, see [Configure junk email settings on cloud mailboxes](configure-junk-email-settings-on-exo-mailboxes).

This method isn't desirable in most situations since senders bypass parts of the filtering stack. Although you trust the sender, the sender can still be compromised and send malicious content. You should let our filters check every message and then [report the false positive/negative to Microsoft](submissions-report-messages-files-to-microsoft) if we got it wrong. Bypassing the filtering stack also interferes with [zero-hour auto purge (ZAP)](zero-hour-auto-purge). If allow list entries aren't working as expected, see [Troubleshoot common anti-spam policy issues](anti-spam-policies-troubleshooting#problem-allow-list-entries-arent-working).

When messages skip spam filtering due to entries in a user's Safe Senders list, the **X-Forefront-Antispam-Report** header field contains the value `SFV:SFE`, which indicates that filtering for spam, spoof, and phishing (not high confidence phishing) was bypassed.

- In Exchange Online, whether entries in the Safe Senders list work or don't work depends on the verdict and action in the policy that identified the message:
    - **Move messages to Junk Email folder**: Domain entries and sender email address entries are honored. Messages from those senders aren't moved to the Junk Email folder.
    - **Quarantine**: Domain entries aren't honored (messages from those senders are quarantined). Email address entries are honored (messages from those senders aren't quarantined) if either of the following statements is true:
        - The message isn't identified as malware or high confidence phishing (malware and high confidence phishing messages are quarantined).
        - The email address, URL, or file in the email message isn't also in a block entry in the [Tenant Allow/Block List](tenant-allow-block-list-about#block-entries-in-the-tenant-allowblock-list).
- Entries for blocked senders and blocked domains are honored (messages from those senders are moved to the Junk Email folder). Safe mailing list settings are ignored.

## Use the IP Allow List in the default connection filter policy

Caution

Without other verification (for example, using mail flow rules), email from sources in the IP Allow List skips spam filtering and sender email authentication (SPF, DKIM, and DMARC). This method creates a high risk of attackers successfully delivering email that would otherwise be filtered. Messages determined to be malware or high confidence phishing are filtered. For more information, see [When user and organization settings conflict](how-policies-and-protections-are-combined#when-user-and-organization-settings-conflict).

You can also add the source email servers to the IP Allow List in the default connection filter policy. For details, see [Configure connection filtering](connection-filter-policies-configure).

- It's important that you keep the number of allowed IP addresses to a minimum, so avoid using entire IP address ranges whenever possible.
- Don't use IP address ranges that belong to consumer services (for example, outlook.com) or shared infrastructures.
- Regularly review the entries in the IP Allow List and remove the entries that you no longer need.

## Use allowed sender lists or allowed domain lists in anti-spam policies

Caution

This method creates a high risk of attackers successfully delivering email that would otherwise be filtered. Messages determined to be malware or high confidence phishing are filtered. For more information, see [When user and organization settings conflict](how-policies-and-protections-are-combined#when-user-and-organization-settings-conflict).

Don't use popular domains (for example, microsoft.com) in allowed domain lists.

You should generally avoid using allowed sender lists or allowed domain lists in custom anti-spam policies or in the default anti-spam policy. You should avoid this option *if at all possible* because senders bypass all spam, spoof, phishing protection (except high confidence phishing), and sender authentication (SPF, DKIM, DMARC). This method is best used for temporary testing only. For detailed steps to configure allowed sender lists or allowed domain lists, see [Configure anti-spam policies](anti-spam-policies-configure).

The maximum limit for these lists is approximately 1,000 entries, but you can enter a maximum of 30 entries in the Microsoft Defender portal. Use PowerShell to add more than 30 entries.

Note

As of September 2022, allowed senders, domains, or subdomains in your organization's [accepted domains](/en-us/exchange/mail-flow-best-practices/manage-accepted-domains/manage-accepted-domains) must pass email authentication checks to skip spam filtering.

## Considerations for bulk email

A standard SMTP email message can contain different sender email addresses as described in [Why internet email needs authentication](email-authentication-about#why-internet-email-needs-authentication). When email is sent on behalf of someone else, the addresses can be different. This condition happens often for bulk email messages.

For example, suppose that Blue Yonder Airlines hired Margie's Travel to send advertising email messages. The message you receive in your Inbox has the following properties:

- The MAIL FROM address (also known as the `5321.MailFrom` address, P1 sender, or envelope sender) is `blueyonder.airlines@margiestravel.com`.
- The From address (also known as the `5322.From` address or P2 sender) is `blueyonder@news.blueyonderairlines.com`, which is what you see in Outlook.

Safe sender lists and safe domain lists in anti-spam policies inspect only the From addresses. This behavior is similar to Outlook Safe Senders that use the From address.

To prevent this message from being filtered, you can take the following steps:

- Add `blueyonder@news.blueyonderairlines.com` (the From address) as an Outlook Safe Sender.
- Use a mail flow rule with a condition that looks for messages from `blueyonder@news.blueyonderairlines.com` (the From address), `blueyonder.airlines@margiestravel.com` (the MAIL FROM address), or both.