---
layout: Conceptual
title: Secure by default in Office 365 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/secure-by-default
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.date: 2026-02-13T00:00:00.0000000Z
ms.topic: concept-article
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
- essentials-security
description: Learn more about the secure by default configuration in all organizations with cloud mailboxes.
ms.service: defender-office-365
locale: en-us
document_id: 4008b532-e5f4-8df8-cc06-6a96dfa30adc
document_version_independent_id: 4008b532-e5f4-8df8-cc06-6a96dfa30adc
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/secure-by-default.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: secure-by-default
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/secure-by-default.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: adeeb299-5dc0-6a0a-d0d9-fd0a3bafaae8
---

# Secure by default in Office 365 - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

"Secure by default" is a term used to define the default settings that are most secure as possible.

However, security needs to be balanced with productivity. This balance includes:

- **Usability**: Settings shouldn't get in the way of user productivity.
- **Risk**: Security might block important activities.
- **Legacy settings**: Some configurations for older products and features might need to be maintained for business reasons, even if new, modern settings are improved.

All organizations with cloud mailboxes automatically receive email protection. This protection includes:

- Email with suspected malware is automatically quarantined. The quarantine policy used by the anti-malware policy controls whether recipients are notified. For more information, see [Configure anti-malware policies](anti-malware-policies-configure).
- Email identified as high confidence phishing is quarantined by default.

For more information, see [Built-in security features for all cloud mailboxes](eop-about).

Because Microsoft wants to keep our customers secure by default, some organization overrides aren't applied for malware or high confidence phishing. These overrides include:

- Allowed sender lists or allowed domain lists in anti-spam policies.
- Outlook Safe Senders.
- The IP Allow List in the default connection filter policy.
- Exchange mail flow rules (also known as transport rules).

Use [admin submissions](submissions-admin#report-good-email-to-microsoft) to temporarily allow specific messages blocked by Microsoft 365.

More information on these overrides can be found in [Create sender allowlists](create-safe-sender-lists-in-office-365).

Note

Anti-spam policies that use the **Move message to Junk Email folder** action for high confidence phishing messages are converted to the **Quarantine message** action. The **Redirect message to email address** action for high confidence phishing messages is unaffected.

Secure by default isn't a setting that you can turn on or off. It's how our filtering keeps potentially dangerous or unwanted messages out of your mailboxes. Malware and high confidence phishing messages should be quarantined. By default, only admins can manage messages quarantined as malware or high confidence phishing, and they can also report false positives to Microsoft from quarantine. For more information, see [Manage quarantined messages and files as an admin](quarantine-admin-manage-messages-files).

## More information

Secure by default means we take the same action on messages you would take if you knew the message was malicious, even if you configured exceptions that would otherwise allow delivery of the message. We always used this approach on malware, and now we're extending this approach to high confidence phishing messages.

Our data indicates a user is 30 times more likely to click a malicious link in messages in the Junk Email folder versus Quarantine. Our data also indicates the false positive rate (good messages marked as bad) for high confidence phishing messages is low. Admins can resolve any false positives with admin submissions.

We also determined the allowed sender and allowed domain lists in anti-spam policies and Safe Senders in Outlook were too broad and were causing more harm than good.

To put it another way: as a security service, we're acting on your behalf to prevent users from being compromised.

## Exceptions

You should only consider using overrides in the following scenarios:

- Phishing simulations: Simulated attacks can help you identify vulnerable users before a real attack impacts your organization. To prevent phishing simulation messages from being filtered, see [Configure non-Microsoft phishing simulations in the advanced delivery policy](advanced-delivery-policy-configure#use-the-microsoft-defender-portal-to-configure-non-microsoft-phishing-simulations-in-the-advanced-delivery-policy).
- Security/SecOps mailboxes: Dedicated mailboxes used by security teams to get unfiltered messages (both good and bad). Teams can then review to see if they contain malicious content. For more information, see [Configure SecOps mailboxes in the advanced delivery policy](advanced-delivery-policy-configure#use-the-microsoft-defender-portal-to-configure-secops-mailboxes-in-the-advanced-delivery-policy).
- Non-Microsoft filters: Secure by default applies only when the MX record for your domain points to Microsoft 365 (for example, contoso.mail.protection.outlook.com). If the MX record for your domain points to a non-Microsoft service or device, policies including but not limited to the following scenarios can result in the delivery of messages detected as high confidence phishing by anti-spam policies:
    - [Exchange mail flow rules to bypass spam filtering](/en-us/exchange/security-and-compliance/mail-flow-rules/use-rules-to-set-scl).
    - Senders identified in the [Safe Senders list](configure-junk-email-settings-on-exo-mailboxes) in user mailboxes.
    - [Allow entries in the Tenant Allow/Block List](tenant-allow-block-list-about#allow-entries-in-the-tenant-allowblock-list).
    - Senders identified in the [allowed senders list and allowed domains list in anti-spam policies](anti-spam-protection-about#allow-and-block-lists-in-anti-spam-policies).
    - Source IP addresses allowed by the [connection filter policy](connection-filter-policies-configure).
- False positives: To temporarily allow certain messages that Microsoft 365 blocked, use [admin submissions](submissions-admin#report-good-email-to-microsoft). By default, allow entries for domains and email addresses, files, and URLs exist for 30 days. During those 30 days, Microsoft learns from the allow entries and removes them or automatically extends them. By default, allow entries for spoofed senders never expire.