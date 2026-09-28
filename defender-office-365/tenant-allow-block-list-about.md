---
layout: Conceptual
title: Manage allows and blocks in the Tenant Allow/Block List - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/tenant-allow-block-list-about
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 2026-07-03T00:00:00.0000000Z
ms.collection:
- m365-security
- tier1
ms.custom: msecd-doc-authoring-1016
description: Learn how to manage allow and block entries in the Tenant Allow/Block List to override filtering verdicts for email, Teams, and Office app content in Microsoft Defender for Office 365.
ms.service: defender-office-365
ai-usage: ai-assisted
locale: en-us
document_id: c6337fbb-8613-ac53-439d-5ed89c71c523
document_version_independent_id: c6337fbb-8613-ac53-439d-5ed89c71c523
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/tenant-allow-block-list-about.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: tenant-allow-block-list-about
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/tenant-allow-block-list-about.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 670ff0a5-2ca4-98aa-02c8-0cf4b64da24f
---

# Manage allows and blocks in the Tenant Allow/Block List - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

You might occasionally disagree with the Microsoft filtering verdict for email messages, Microsoft Teams messages, or Office apps. For example, a good message might be marked as bad (a false positive), or a bad message might be allowed through (a false negative), or a URL might be blocked when it shouldn't be.

The Tenant Allow/Block List in the Microsoft Defender portal gives you a way to manually override filtering verdicts. The list is used during mail flow (for email) or time of click (for email, Teams, or Office apps).

The Tenant Allow/Block List is available in the Microsoft Defender portal at https://security.microsoft.com**Email & collaboration** &gt; **Policies & rules** &gt; **Threat policies** &gt; **Rules** section &gt; **Tenant Allow/Block Lists**. Or, to go directly to the **Tenant Allow/Block Lists** page, use https://security.microsoft.com/tenantAllowBlockList.

For usage and configuration instructions, see the following articles:

- **Domains and email addresses** and **spoofed senders**: [Allow or block emails using the Tenant Allow/Block List](tenant-allow-block-list-email-spoof-configure)
    - Entries apply to the From address (also known as the `5322.From` address or P2 sender), not the MAIL FROM address (also known as the `5321.MailFrom` address, P1 sender, or envelope sender). For more information about these addresses, see [Why internet email needs authentication](email-authentication-about#why-internet-email-needs-authentication).
    - Entries apply to messages from both internal and external senders. Special handling applies to internal spoofing scenarios.
    - Block entries for **Domains and email addresses** also prevent users in the organization from *sending* email to those blocked domains and addresses.
- **Files**: [Allow or block files using the Tenant Allow/Block List](tenant-allow-block-list-files-configure)
- **URLs**: [Allow or block URLs using the Tenant Allow/Block List](tenant-allow-block-list-urls-configure).
    - To allow phishing URLs from non-Microsoft attack simulation training, don't use URL allow entries in the Tenant Allow/Block List. Use the [advanced delivery policy](advanced-delivery-policy-configure) to specify the URLs.
- **IP addresses**: [Allow or block IPv6 addresses using the Tenant Allow/Block List](tenant-allow-block-list-ip-addresses-configure).
- **Teams domains and email addresses**: [Block domains and addresses in Microsoft Teams using the Tenant Allow/Block List](tenant-allow-block-list-teams-domains-configure).

The Tenant Allow/Block List configuration articles linked in this section contain procedures in the Microsoft Defender portal and in PowerShell.

## Block entries in the Tenant Allow/Block List

Important

In the Tenant Allow/Block List, block entries take precedence over allow entries.

Block entries directly control message delivery. If an email message contains a URL or domain that's blocked in the Tenant Allow/Block List, the message can be classified as *high confidence phishing* and moved to quarantine, even if the sender is legitimate. If legitimate messages are quarantined as high confidence phishing, review your Tenant Allow/Block List block entries for URLs or domains that are included in the affected messages.

Use the **Submissions** page (also known as *admin submission*) at https://security.microsoft.com/reportsubmission to create block entries for the following types of items as you submit them as false negatives to Microsoft:

- **[Domains and email addresses](submissions-admin#report-questionable-email-to-microsoft)**:

    - Email messages from blocked domains and email addresses are marked as *high confidence phishing* and then moved to quarantine.
    - Users in the organization can't send email to these blocked domains and addresses. They receive the following non-delivery report (also known as an NDR or bounce message): `550 5.7.703 Your message can't be delivered because messages to XXX, YYY are blocked by your organization using Tenant Allow Block List.` The entire message is blocked for all internal and external recipients of the message, even if only one recipient email address or domain is defined in a block entry.

    Tip

    Blocking a specific sender or domain in the Tenant Allow/Block List treats those messages as high confidence phishing. To treat those messages as spam, add the sender to the blocked senders list or blocked domains list in [anti-spam policies](anti-spam-policies-configure).
- **[Files](submissions-admin#report-questionable-email-attachments-to-microsoft)**: Email messages that contain file block entries are blocked as *malware*. Messages containing blocked file entries are quarantined.
- **[URLs](submissions-admin#report-questionable-urls-to-microsoft)**: Email messages that contain URL block entries are blocked as *high confidence phishing*. Messages containing URL block entries are quarantined.

In the Tenant Allow/Block List, you can also directly create block entries for the following types of items:

- **[Domains and email addresses](tenant-allow-block-list-email-spoof-configure#create-block-entries-for-domains-and-email-addresses)**, **[Files](tenant-allow-block-list-files-configure#create-block-entries-for-files)**, and **[URLs](tenant-allow-block-list-urls-configure#create-block-entries-for-urls)**.
- **[Spoofed senders](tenant-allow-block-list-email-spoof-configure#create-block-entries-for-spoofed-senders)**: If you manually override an existing allow verdict from [spoof intelligence](anti-spoofing-spoof-intelligence), the blocked spoofed sender becomes a manual block entry that appears only on the **Spoofed senders** tab in the Tenant Allow/Block List.
- **[IP addresses](tenant-allow-block-list-ip-addresses-configure#create-block-entries-for-ipv6-addresses)**: If you manually create a block entry, all incoming email messages from that IP address are dropped at the edge of the service.
- **[Teams domains and addresses](tenant-allow-block-list-teams-domains-configure)**: If you manually create a block entry, all incoming Teams communication from that domain and email address is blocked, and existing communication is deleted.

By default, the following types of block entries expire after 30 days, but you can set them to expire up to 90 days or to never expire:

- [Domains and email addresses](tenant-allow-block-list-email-spoof-configure#create-block-entries-for-domains-and-email-addresses)
- [Files](tenant-allow-block-list-files-configure#create-block-entries-for-files)
- [URLs](tenant-allow-block-list-urls-configure#create-block-entries-for-urls).

The following types of block entries never expire:

- [Spoofed senders](tenant-allow-block-list-email-spoof-configure#create-block-entries-for-spoofed-senders)
- [IP addresses](tenant-allow-block-list-ip-addresses-configure#create-block-entries-for-ipv6-addresses)
- [Teams domains and addresses](tenant-allow-block-list-teams-domains-configure).

## Allow entries in the Tenant Allow/Block List

Unnecessary allow entries expose your organization to malicious email that the system would otherwise filter, so there are limitations for creating allow entries directly in the Tenant Allow/Block List:

- **Domains and email addresses** and **URLs**: You can create allow entries directly in the Tenant Allow/Block List to override the following verdicts:

    - Bulk
    - Spam
    - High confidence spam
    - Phishing (not high confidence phishing)

    For malware and high confidence phishing verdicts, you can't create allow entries directly in the Tenant Allow/Block List. Instead, use the **Submissions** page at https://security.microsoft.com/reportsubmission to submit the **[email](submissions-admin#report-good-email-to-microsoft)** or **[URL](submissions-admin#report-good-urls-to-microsoft)** to Microsoft. After you select **I've confirmed it's clean**, you can then select **Allow this message** or **Allow this URL** to create an allow entry for the domains and email addresses or URLs.
- **Files**: You can't create allow entries directly in the Tenant Allow/Block List. Instead, use the **Submissions** page at https://security.microsoft.com/reportsubmission to submit the **[email attachment](submissions-admin#report-good-email-attachments-to-microsoft)** to Microsoft. After you select **I've confirmed it's clean**, you can then select **Allow this file** to create an allow entry for the files.
- **Spoofed senders**:

    - If spoof intelligence already blocked the message as spoofing, use the **Submissions** page at https://security.microsoft.com/reportsubmission to [report the email to Microsoft](submissions-admin#report-good-email-to-microsoft) as **I've confirmed it's clean**, and then select **Allow this message**.
    - You can proactively create [an allow entry for a spoofed sender](tenant-allow-block-list-email-spoof-configure#create-allow-entries-for-spoofed-senders) on the **Spoofed sender** tab in the Tenant Allow/Block List before [spoof intelligence](anti-spoofing-spoof-intelligence) identifies and blocks the message as spoofing.
- **IP addresses**: You can proactively create [an allow entry for an IP address](tenant-allow-block-list-ip-addresses-configure#create-block-entries-for-ipv6-addresses) on the **IP addresses** tab in the Tenant Allow/Block List to override the IP filters for incoming messages.

    - An IP address allow entry bypasses IP-based filtering checks (for example, connection filtering or IP reputation checks).
    - An IP address allow entry doesn't change message throttling behavior.
    - An IP address block entry rejects messages at the service edge.

The following list describes what happens in the Tenant Allow/Block List when you submit something to Microsoft as a false positive on the **Submissions** page:

- **Email attachments** and **URLs**: An allow entry is created and the entry appears on the **Files** or **URLs** tab in the Tenant Allow/Block List, respectively.

    For URLs reported as false positives, subsequent messages that contain variations of the original URL are allowed. For example, you use the **Submissions** page to report the incorrectly blocked URL `www.contoso.com/abc`. If your organization later receives a message that contains the URL (for example but not limited to: `www.contoso.com/abc`, `www.contoso.com/abc?id=1`, `www.contoso.com/abc/def/gty/uyt?id=5`, or `www.contoso.com/abc/whatever`), the message isn't blocked based on the URL. In other words, you don't need to report multiple variations of the same URL as good to Microsoft.
- **Email**: If Microsoft 365 blocked a message, an allow entry might be created in the Tenant Allow/Block List:

    - If the message was blocked by [spoof intelligence](anti-spoofing-spoof-intelligence), an allow entry for the sender is created, and the entry appears on the **Spoofed senders** tab in the Tenant Allow/Block List.
    - If [user or mailbox intelligence impersonation protection in Defender for Office 365](anti-phishing-policies-about#impersonation-settings-in-anti-phishing-policies-in-microsoft-defender-for-office-365) blocked a message, an allow entry isn't created in the Tenant Allow/Block List. Instead, the domain or sender is added to the **Trusted senders and domains section** in the [anti-phishing policy](anti-phishing-policies-mdo-configure#use-the-microsoft-defender-portal-to-modify-anti-phishing-policies) that detected the message.
    - If the message was blocked due to file-based filters, an allow entry for the file is created, and the entry appears on the **Files** tab in the Tenant Allow/Block List.
    - If the message was blocked due to URL-based filters, an allow entry for the URL is created, and the entry appears on the **URL** tab in the Tenant Allow/Block List.
    - If the message was blocked for any other reason, an allow entry for the sender email address or domain is created, and the entry appears on the **Domains & addresses** tab in the Tenant Allow/Block List.
    - If the message wasn't blocked due to filtering, no allow entries are created anywhere.

Tip

Allow entries from submissions are added during mail flow based on the filters that determined the message was malicious. For example, if the sender email address and a URL in the message are determined to be malicious, an allow entry is created for the sender (email address or domain) and the URL.

During mail flow or time of click, if messages containing the entities in the allow entries pass other checks in the filtering stack, the messages are delivered (all filters associated with the allowed entities are skipped). For example, if a message passes [email authentication checks](email-authentication-about), URL filtering, and file filtering, a message from an allowed sender email address is delivered if it's also from an allowed sender.

By default, allow entries for [domains and email addresses](submissions-admin#report-good-email-to-microsoft), [files](submissions-admin#report-good-email-attachments-to-microsoft), and [URLs](submissions-admin#report-good-urls-to-microsoft) are kept for 45 days after the filtering system determines that the entity is clean, and then the allow entry is removed. Or you can set allow entries to expire up to 30 days after you create them. Allow entries for [spoofed senders](tenant-allow-block-list-email-spoof-configure#create-allow-entries-for-spoofed-senders) never expire.

## What to expect after you add an allow or block entry

After you add an allow entry on the **Submissions** page or a block entry in the Tenant Allow/Block List, the entry starts working within 5 minutes.

If Microsoft determines that a Tenant Allow/Block List allow entry is no longer needed, the entry is automatically removed and the built-in [threat management alert policy](/en-us/defender-xdr/alert-policies#threat-management-alert-policies) named **Removed an entry in Tenant Allow/Block List** creates an alert.