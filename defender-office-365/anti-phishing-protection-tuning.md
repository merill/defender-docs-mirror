---
layout: Conceptual
title: Tune anti-phishing protection - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/anti-phishing-protection-tuning
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
ms.collection:
- m365-security
- tier2
description: Identify why a phishing message was delivered in Microsoft 365 and learn how to adjust anti-phishing settings to help prevent similar messages in the future.
ms.service: defender-office-365
ms.date: 2026-07-24T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 7b241a93-f563-23de-8211-ce73e3ee81b7
document_version_independent_id: 7b241a93-f563-23de-8211-ce73e3ee81b7
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/anti-phishing-protection-tuning.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: anti-phishing-protection-tuning
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/anti-phishing-protection-tuning.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: eb889a4e-e166-705d-3a95-5b39d1493d24
---

# Tune anti-phishing protection - Microsoft Defender for Office 365 | Microsoft Learn

Although Microsoft 365 includes many anti-phishing features, some phishing messages can still be delivered to mailboxes in your organization. This article describes how to discover why a phishing message was delivered, and how to adjust anti-phishing settings *without accidentally making things worse*.

## First things first: deal with any compromised accounts and make sure you block any more phishing messages from getting through

If a recipient's account was compromised as a result of the phishing message, follow the steps in [Responding to a compromised cloud email account](responding-to-a-compromised-email-account).

If you have Microsoft Defender for Office 365 (included or in an add-on subscription), you can use [Office 365 Threat Intelligence](office-365-ti) to identify other users who also received the phishing message. Defender for Office 365 includes more ways to block phishing messages:

- [Safe Links in Microsoft Defender for Office 365](safe-links-policies-configure)
- [Safe Attachments in Microsoft Defender for Office 365](safe-attachments-policies-configure)
- [Configure anti-phishing policies in Microsoft Defender for Office 365](anti-phishing-policies-mdo-configure). You can temporarily increase the **Phishing email threshold** in the policy from **Standard** to **Aggressive**, **More aggressive**, or **Most aggressive**.

Verify that Safe Links, Safe Attachments, and anti-phishing policies are working. Safe Links and Safe Attachments protection is turned on by default via Built-in protection in [preset security policies](preset-security-policies). Anti-phishing has a default policy that applies to all recipients where anti-spoofing protection is turned on by default. Impersonation protection isn't turned on in the default anti-phishing policy, and therefore needs to be configured. For instructions, see [Configure anti-phishing policies in Microsoft Defender for Office 365](anti-phishing-policies-mdo-configure).

## Report the phishing message to Microsoft

Reporting phishing messages is helpful in tuning the filters that are used to protect all customers in Microsoft 365. For instructions, see [Use the Submissions page to submit suspected spam, phish, URLs, legitimate email getting blocked, and email attachments to Microsoft](submissions-admin).

## Inspect the message headers

You can examine the headers of the phishing message to see whether any of your organization's settings allowed similar phishing messages to be delivered. In other words, examining the message headers can help you identify settings in your organization that allowed this phishing message or similar phishing messages to be delivered.

Specifically, check the Spam Filtering Verdict (SFV) value in the **X-Forefront-Antispam-Report** header field. The SFV value indicates whether spam or phishing filtering was skipped. For example, messages that used a mail flow rule (transport rule) to skip spam filtering have the value `SFV:SKN`. For more information on how to get message headers and the complete list of all available anti-spam and anti-phishing message headers, see [Anti-spam message headers](message-headers-eop-mdo).

Tip

You can copy and paste the contents of a message header into the [Message Header Analyzer](https://mha.azurewebsites.net/) tool. This tool helps parse headers and presents them in a human readable format.

You can also use the [configuration analyzer](configuration-analyzer-for-security-policies) to compare your threat policies to the Standard and Strict recommendations.

## Best practices to stay protected

Use the following best practices to reduce future phishing risk and validate your protection settings.

- On a monthly basis, run [Microsoft Secure Score](/en-us/defender-xdr/microsoft-secure-score), a security assessment tool that measures your organization's security posture, to assess your organization's security settings.
- Use [Threat Explorer and real-time detections](threat-explorer-real-time-detections-about) to search for good messages quarantined by mistake (false positives) or delivered bad messages (false negatives). You can search by sender, recipient, or message ID. For a quarantined message, use the **Detection technology** value to find an appropriate method to override. For an allowed message, view which policy allowed the message.
- Email from spoofed senders (the From address doesn't match the source of the message) is classified as *phishing* in Defender for Office 365. Some spoofing is benign, and some users might want blocked messages from specific spoofed senders.

    Periodically review the following features to identify benign or desired messages identified as spoofing:

    - [Spoof intelligence insight](anti-spoofing-spoof-intelligence)
    - [Entries for spoofed senders in the Tenant Allow/Block List](tenant-allow-block-list-email-spoof-configure#use-the-microsoft-defender-portal-to-view-entries-for-spoofed-senders-in-the-tenant-allowblock-list)
    - [Spoof detections report](reports-email-security#spoof-detections-report)

    After you configure any necessary overrides, you can confidently [configure spoof intelligence in anti-phishing policies](anti-phishing-policies-about#spoof-settings) to **Quarantine** suspicious messages instead of delivering them to the user's Junk Email folder.
- In Defender for Office 365, you can also use the **Impersonation insight** page at https://security.microsoft.com/impersonationinsight to track user impersonation or domain impersonation detections. For more information, see [Impersonation insight in Defender for Office 365](anti-phishing-mdo-impersonation-insight).
- Periodically review the [Threat Protection Status report](reports-defender-for-office-365#threat-protection-status-report) for phishing detections.
- Don't include your Microsoft 365 domains in the allowed senders list or the allowed domains list in anti-spam policies. Although adding your Microsoft 365 domains to the allowed senders list or allowed domains list prevents blocking some legitimate messages, it also results in the delivery of malicious messages normally blocked by the spam and/or phishing filters. Instead of allowing the domain, correct the underlying email delivery problem.

    If Microsoft 365 blocks legitimate messages from senders in your Microsoft 365 domain, completely configure the SPF, DKIM, and DMARC records in DNS for *all* of your Microsoft 365 domains:

    - Verify your SPF record identifies *all* sources of email for your domain (don't forget non-Microsoft services!).
    - To ensure destination email systems can reject messages from unauthorized sources for your domain, use hard fail (`-all`) in the SPF record. You can use the [spoof intelligence insight](anti-spoofing-spoof-intelligence) to help identify senders using your domain so you can include all authorized non-Microsoft senders in your SPF record.

    For configuration instructions, see:

    - [Set up SPF to identify valid email sources for your custom cloud domains](email-authentication-spf-configure)
    - [Set up DKIM to sign mail from your cloud domain](email-authentication-dkim-configure)
    - [Set up DMARC to validate the From address domain for cloud senders](email-authentication-dmarc-configure)
- We recommend that mail for your Microsoft 365 domain is delivered directly to Microsoft 365 (point the MX record of your Microsoft 365 domain to Microsoft 365). If you must use a non-Microsoft service in front of Microsoft 365, use Enhanced Filtering for Connectors. For instructions, see [Enhanced Filtering for Connectors in Exchange Online](/en-us/Exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/enhanced-filtering-for-connectors).
- Have users use the [built-in Report button in Outlook](submissions-outlook-report-messages#use-the-built-in-report-button-in-outlook). Configure the [user reported settings](submissions-user-reported-messages-custom-mailbox) to send user reported messages to a reporting mailbox, to Microsoft, or both. User reported messages are then available to admins on the **User reported** tab on the **Submissions** page at https://security.microsoft.com/reportsubmission?viewid=user. Admin can report user reported messages or any messages to Microsoft as described in [Use the Submissions page to submit suspected spam, phish, URLs, legitimate email getting blocked, and email attachments to Microsoft](submissions-admin). User or admin reporting of false positives or false negatives to Microsoft is important, because it helps train our detection systems.
- Multifactor authentication (MFA) is a good way to prevent compromised accounts. You should strongly consider enabling MFA for all of your users. For a phased approach, start by enabling MFA for your most sensitive users (admins, executives, etc.) before you enable MFA for everyone. For instructions, see [Set up multifactor authentication](/en-us/microsoft-365/admin/security-and-compliance/set-up-multi-factor-authentication).
- Forwarding rules to external recipients are often used by attackers to extract data. Use the **Review mailbox forwarding rules** information in [Microsoft Secure Score](/en-us/defender-xdr/microsoft-secure-score) to find and even prevent forwarding rules to external recipients. For more information, see [Mitigating Client External Forwarding Rules with Secure Score](/en-us/archive/blogs/office365security/mitigating-client-external-forwarding-rules-with-secure-score).

    Use the [Autoforwarded messages report](/en-us/exchange/monitoring/mail-flow-reports/mfr-auto-forwarded-messages-report) to view specific details about forwarded email.