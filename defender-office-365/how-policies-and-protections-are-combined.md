---
layout: Conceptual
title: Order and precedence of email protection - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/how-policies-and-protections-are-combined
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
keywords: security, malware, Microsoft 365, M365, security center, Microsoft Defender portal, Microsoft Defender for Endpoint, Microsoft Defender for Office 365, Microsoft Defender for Identity
author: chrisda
ms.author: chrisda
ms.topic: reference
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.custom:
- seo-marvel-apr2020
description: Admins can learn how the order of protection settings and the priority order of threat policies affect the application of protection in Microsoft 365.
ms.service: defender-office-365
ms.date: 2025-09-12T00:00:00.0000000Z
locale: en-us
document_id: eaec4805-8c58-1556-d2aa-29307d7bebce
document_version_independent_id: eaec4805-8c58-1556-d2aa-29307d7bebce
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/how-policies-and-protections-are-combined.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: how-policies-and-protections-are-combined
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/how-policies-and-protections-are-combined.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: fb73d04c-d7ce-ecc1-8197-fc8c35475925
---

# Order and precedence of email protection - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

In all organizations with cloud mailboxes, multiple protection features might flag inbound email. For example, anti-spoofing protection that's available to all Microsoft 365 customers, and impersonation protection that's available to Microsoft Defender for Office 365 customers only. Messages also pass through multiple detection scans for malware, spam, phishing, etc. Given all this activity, there might be some confusion as to which policy is applied.

In general, a policy applied to a message is identified in the **X-Forefront-Antispam-Report** header in the **CAT (Category)** property. For more information, see [Anti-spam message headers](message-headers-eop-mdo).

There are two major factors that determine which policy is applied to a message:

- **The order of processing for the email protection type**: This order isn't configurable, and is described in the following table:

    | Order | Email protection | Category | Where to manage |
    | --- | --- | --- | --- |
    | 1 | Malware | `CAT:MALW` | [Configure anti-malware policies](anti-malware-policies-configure) |
    | 2 | High confidence phishing | `CAT:HPHSH` | [Configure anti-spam policies](anti-spam-policies-configure) |
    | 3 | Phishing | `CAT:PHSH` | [Configure anti-spam policies](anti-spam-policies-configure) |
    | 4 | Spoofing – DMARC p=reject (Honor DMARC = On)^\*^ | `CAT:SPOOF` | [Configure anti-phishing policies in Microsoft Defender for Office 365](anti-phishing-policies-mdo-configure) |
    | 5 | Spoofing – DMARC p=quarantine (Honor DMARC = On)^\*^ | `CAT:SPOOF` | [Configure anti-phishing policies in Microsoft Defender for Office 365](anti-phishing-policies-mdo-configure) |
    | 6 | Spoofing^\*^ | `CAT:SPOOF` | [Spoof intelligence insight](anti-spoofing-spoof-intelligence) |
    | 7^\*\*^ | User impersonation (protected users) | `CAT:UIMP` | [Configure anti-phishing policies in Microsoft Defender for Office 365](anti-phishing-policies-mdo-configure) |
    | 8^\*\*^ | Domain impersonation (protected domains) | `CAT:DIMP` | [Configure anti-phishing policies in Microsoft Defender for Office 365](anti-phishing-policies-mdo-configure) |
    | 9^\*\*^ | Mailbox intelligence (contact graph) | `CAT:GIMP` | [Configure anti-phishing policies in Microsoft Defender for Office 365](anti-phishing-policies-mdo-configure) |
    | 10 | High confidence spam | `CAT:HSPM` | [Configure anti-spam policies](anti-spam-policies-configure) |
    | 11 | Spam | `CAT:SPM` | [Configure anti-spam policies](anti-spam-policies-configure) |
    | 12 | Bulk | `CAT:BULK` | [Configure anti-spam policies](anti-spam-policies-configure) |

    ^\*^ Spoofing is a technique commonly used in phishing. Anti-spoofing (including DMARC enforcement) is configured in the anti-phishing policies. When Honor DMARC = Off, rows 4 and 5 collapse into row 6 (SpoofAction applies to both implicit and explicit failures). When Spoof Intelligence = Off, row 6 isn't evaluated.

    ^\*\*^ These features are available only in anti-phishing policies in Microsoft Defender for Office 365.
- **The priority order of policies**: The policy priority order is shown in the following list:

    1. The anti-spam, anti-malware, anti-phishing, Safe Links^\*^, and Safe Attachments^\*^ policies in the [Strict preset security policy](preset-security-policies#profiles-in-preset-security-policies) (when enabled).
    2. The anti-spam, anti-malware, anti-phishing, Safe Links^\*^, and Safe Attachments^\*^ policies in the [Standard preset security policy](preset-security-policies#profiles-in-preset-security-policies) (when enabled).
    3. Anti-phishing, Safe Links, and Safe Attachments in [Defender for Office 365 evaluation policies](try-microsoft-defender-for-office-365#audit-mode-vs-blocking-mode-for-defender-for-office-365) (when enabled).
    4. Custom anti-spam, anti-malware, anti-phishing, Safe Links^\*^, and Safe Attachments^\*^ policies (when created).

        Custom threat policies are assigned a default priority value when you create the policy (newer equals higher), but you can change the priority value at any time. This priority value affects the order of application for that type of threat policy (anti-spam, anti-malware, anti-phishing, etc.). The priority value doesn't affect where custom threat policies are applied in the order of processing as described in the previous table.
    5. Of equal value:

        - The Safe Links and Safe Attachments policies in the [Built-in protection preset security policy](preset-security-policies#profiles-in-preset-security-policies)^\*^.
        - The default policies for anti-malware, anti-spam, and anti-phishing.

        You can configure exceptions to the Built-in protection preset security policy, but you can't configure exceptions to the default threat policies (they apply to all recipients and you can't turn them off).

    ^\*^ Defender for Office 365 only.

    Important

    The priority order matters if the same recipient is intentionally or unintentionally included in multiple policies, because *only* the first policy of that type (anti-spam, anti-malware, anti-phishing, etc.) is applied to that recipient, regardless of how many other policies that the recipient is included in. There's never a merging or combining of the settings in multiple policies for the recipient. The recipient is unaffected by the settings of the remaining policies of that type.

For example, the group named "Contoso Executives" is included in the following policies:

- The Strict preset security policy
- A custom anti-spam policy with the priority value 0 (highest priority)
- A custom anti-spam policy with the priority value 1.

Which anti-spam policy settings are applied to the members of Contoso Executives? The Strict preset security policy. The settings in the custom anti-spam policies are ignored for the members of Contoso Executives, because the Strict preset security policy is always applied first.

As another example, consider the following custom anti-phishing policies in Microsoft Defender for Office 365 that apply to the same recipients, and a message that contains both user impersonation and spoofing:

| Policy name | Priority | User impersonation | Anti-spoofing |
| --- | --- | --- | --- |
| Policy A | 1 | On | Off |
| Policy B | 2 | Off | On |

1. The message is identified as spoofing, because spoofing (5) is evaluated before user impersonation (6) in the order of processing for the email protection type.
2. Policy A is applied first, because it has a higher priority than Policy B.
3. Based on the settings in Policy A, no action is taken on the message because anti-spoofing is turned off.
4. The processing of anti-phishing policies stops for all included recipients, so Policy B is never applied to recipients who are also in Policy A.

To make sure that recipients get the protection settings that you want, use the following guidelines for policy memberships:

- Assign a smaller number of users to higher priority policies, and a larger number of users to lower priority policies. Remember, default threat policies are always applied last.
- Configure higher priority policies to have stricter or more specialized settings than lower priority policies. You have complete control over the settings in custom threat policies and the default threat policies, but no control over most settings in preset security policies.
- Consider using fewer custom policies (only use custom policies for users who require more specialized settings than the Standard or Strict preset security policies, or the default threat policies).

## Appendix

It's important to understand how user allows and blocks, organization allows and blocks, and filtering stack verdicts in [the built-in security features for all cloud mailboxes](eop-about) and in Defender for Office 365 complement or contradict each other.

- For information about filtering stacks and how they're combined, see [Step-by-step threat protection in Microsoft Defender for Office 365](protection-stack-microsoft-defender-for-office365).
- After the filtering stack determines a verdict, only then are organization policies and their configured actions evaluated.
- If the same email address or domain exists in a user's Safe Senders list and Blocked Senders list, the Safe Senders list takes precedence.
- If the same entity (email address, domain, spoofed sending infrastructure, file, or URL) exists in an allow entry and a block entry in the Tenant Allow/Block List, the block entry takes precedence.
- For malware and high confidence phishing verdicts, you can't create allow entries directly in the Tenant Allow/Block List. Instead, use the **Submissions** page at https://security.microsoft.com/reportsubmission to submit the **[email](submissions-admin#report-good-email-to-microsoft)**, **[email attachment](submissions-admin#report-good-email-attachments-to-microsoft)** or **[URL](submissions-admin#report-good-urls-to-microsoft)** to Microsoft. After you select **I've confirmed it's clean**, you can then select **Allow this message**, **Allow this file** or **Allow this URL** to create an allow entry for the domains and email addresses, files or URLs.
- If you use a file type in the [Common attachments filter in anti-malware policies](anti-malware-protection-about#common-attachments-filter-in-anti-malware-policies), allowing the same file in the Tenant Allow/Block list or Exchange mail flow rules (also known as transport rules) doesn't override the verdict.

### User allows and blocks

Entries in a user's *safelist collection* (the Safe Senders list, the Safe Recipients list, and the Blocked Senders list on each mailbox) are able to override some filtering stack verdicts as described in the following table:

| Filtering stack verdict | User's Safe Senders/Recipients list | User's Blocked Senders list |
| --- | --- | --- |
| Malware | **Filter wins**: Email quarantined | **Filter wins**: Email quarantined |
| High confidence phishing | **Filter wins**: Email quarantined | **Filter wins**: Email quarantined |
| Phishing | **User wins**: Email delivered to user's Inbox | **Organization wins**: The applicable anti-spam policy determines the action |
| High confidence spam | **User wins**: Email delivered to user's Inbox | **Organization wins**: The applicable anti-spam policy determines the action |
| Spam | **User wins**: Email delivered to user's Inbox | **Organization wins**: The applicable anti-spam policy determines the action |
| Bulk | **User wins**: Email delivered to user's Inbox | **User wins**: Email delivered to user's Junk Email folder |
| Not spam | **User wins**: Email delivered to user's Inbox | **User wins**: Email delivered to user's Junk Email folder |

- In Exchange Online, the domain allow in the Safe Sender's list might not work if any of the following scenarios quarantined the message:
    - The message is identified as malware or high confidence phishing (malware and high confidence phishing messages are quarantined).
    - [Actions in anti-spam policies](anti-spam-protection-about#actions-in-anti-spam-policies) are configured to quarantine instead of move mail to the Junk Email folder.
    - The email address, URL, or file in the email message is also in a block entry in the [Tenant Allow/Block List](tenant-allow-block-list-about#block-entries-in-the-tenant-allowblock-list).

For more information about the safelist collection and anti-spam settings on user mailboxes, see [Configure junk email settings on cloud mailboxes](configure-junk-email-settings-on-exo-mailboxes).

### Organization allows and blocks

Organization allows and blocks are able to override some filtering stack verdicts as described in the following tables:

- [Advanced delivery policy](advanced-delivery-policy-configure) (skip filtering for designated SecOps mailboxes and phishing simulation URLs):

    | Filtering stack verdict | Advanced delivery policy allow |
    | --- | --- |
    | Malware | **Organization wins**: Email delivered to mailbox |
    | High confidence phishing | **Organization wins**: Email delivered to mailbox |
    | Phishing | **Organization wins**: Email delivered to mailbox |
    | High confidence spam | **Organization wins**: Email delivered to mailbox |
    | Spam | **Organization wins**: Email delivered to mailbox |
    | Bulk | **Organization wins**: Email delivered to mailbox |
    | Not spam | **Organization wins**: Email delivered to mailbox |
- [Exchange mail flow rules](/en-us/exchange/security-and-compliance/mail-flow-rules/mail-flow-rules) (also known as transport rules):

    | Filtering stack verdict | Mail flow rule allows^\*^ | Mail flow rule blocks |
    | --- | --- | --- |
    | Malware | **Filter wins**: Email quarantined | **Filter wins**: Email quarantined |
    | High confidence phishing | **Filter wins**: Email quarantined except in complex routing | **Filter wins**: Email quarantined |
    | Phishing | **Organization wins**: Email delivered to mailbox | **Filter wins**: Phishing action in the applicable anti-spam policy |
    | High confidence spam | **Organization wins**: Email delivered to mailbox | **Filter wins**: Email delivered to user's Junk Email folder |
    | Spam | **Organization wins**: Email delivered to mailbox | **Filter wins**: Email delivered to user's Junk Email folder |
    | Bulk | **Organization wins**: Email delivered to mailbox | **Filter wins**: Email delivered to user's Junk Email folder |
    | Not spam | **Organization wins**: Email delivered to mailbox | **Organization wins**: Email delivered to user's Junk Email folder |

    ^\*^ Organizations that use a non-Microsoft security service or device in front of Microsoft 365 should consider using [Authenticated Received Chain (ARC)](email-authentication-arc-configure) (contact the service for availability) and [Enhanced Filtering for Connectors (also known as skip listing)](/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/enhanced-filtering-for-connectors) instead of [bypass spam filtering mail flow rules](/en-us/exchange/security-and-compliance/mail-flow-rules/use-rules-to-set-scl) (spam confidence level or SCL -1). These improved methods reduce email authentication issues and encourage [defense-in-depth](step-by-step-guides/defense-in-depth-guide) email security.
- IP Allow List and IP Block List in [connection filtering](connection-filter-policies-configure):

    | Filtering stack verdict | IP Allow List | IP Block List |
    | --- | --- | --- |
    | Malware | **Filter wins**: Email quarantined | **Filter wins**: Email quarantined |
    | High confidence phishing | **Filter wins**: Email quarantined | **Filter wins**: Email quarantined |
    | Phishing | **Organization wins**: Email delivered to mailbox | **Organization wins**: Email silently dropped |
    | High confidence spam | **Organization wins**: Email delivered to mailbox | **Organization wins**: Email silently dropped |
    | Spam | **Organization wins**: Email delivered to mailbox | **Organization wins**: Email silently dropped |
    | Bulk | **Organization wins**: Email delivered to mailbox | **Organization wins**: Email silently dropped |
    | Not spam | **Organization wins**: Email delivered to mailbox | **Organization wins**: Email silently dropped |
- Allow and block settings in [anti-spam policies](anti-spam-policies-configure):

    - Allowed sender and domain list.
    - Blocked sender and domain list.
    - Block messages from specific countries/regions or in specific languages.
    - Block messages based on [Advanced Spam Filter (ASF) settings in anti-spam policies](anti-spam-policies-asf-settings-about).

    | Filtering stack verdict | Anti-spam policy allows | Anti-spam policy blocks |
    | --- | --- | --- |
    | Malware | **Filter wins**: Email quarantined | **Filter wins**: Email quarantined |
    | High confidence phishing | **Filter wins**: Email quarantined | **Filter wins**: Email quarantined |
    | Phishing | **Organization wins**: Email delivered to mailbox | **Organization wins**: Phishing action in the applicable anti-spam policy |
    | High confidence spam | **Organization wins**: Email delivered to mailbox | **Organization wins**: Email delivered to user's Junk Email folder |
    | Spam | **Organization wins**: Email delivered to mailbox | **Organization wins**: Email delivered to user's Junk Email folder |
    | Bulk | **Organization wins**: Email delivered to mailbox | **Organization wins**: Email delivered to user's Junk Email folder |
    | Not spam | **Organization wins**: Email delivered to mailbox | **Organization wins**: Email delivered to user's Junk Email folder |
- [Allow entries in the Tenant Allow/Block List](tenant-allow-block-list-about#allow-entries-in-the-tenant-allowblock-list): There are two types of allow entries:

    - **Message level** allow entries act on the entire message, regardless of the entities in the message. Allow entries for email address and domains are message level allow entries. These allow entries override bulk and spam verdicts, and high confidence phishing verdicts from machine learning models.
    - **Entity level** allow entries act on the filtering verdict of entities. Allow entries for URLs, spoofed senders, and files are entity level allow entries. To override malware and high confidence phishing verdicts, you need to use entity level allow entries, which you can create by submission only due to [Secure by default](secure-by-default).

    | Filtering stack verdict | Email address/domain |
    | --- | --- |
    | Malware | **Filter wins**: Email quarantined |
    | High confidence phishing | **Filter wins**: Email quarantined |
    | Phishing | **Organization wins**: Email delivered to mailbox |
    | High confidence spam | **Organization wins**: Email delivered to mailbox |
    | Spam | **Organization wins**: Email delivered to mailbox |
    | Bulk | **Organization wins**: Email delivered to mailbox |
    | Not spam | **Organization wins**: Email delivered to mailbox |
- [Block entries in the Tenant Allow/Block List](tenant-allow-block-list-about#block-entries-in-the-tenant-allowblock-list):

    | Filtering stack verdict | Email address/domain | Spoof | File | URL |
    | --- | --- | --- | --- | --- |
    | Malware | **Filter wins**: Email quarantined | **Filter wins**: Email quarantined | **Organization wins**: Email quarantined | **Filter wins**: Email quarantined |
    | High confidence phishing | **Organization wins**: Email quarantined | **Filter wins**: Email quarantined | **Organization wins**: Email quarantined | **Organization wins**: Email quarantined |
    | Phishing | **Organization wins**: Email quarantined | **Organization wins**: Spoof action in the applicable anti-phishing policy | **Organization wins**: Email quarantined | **Organization wins**: Email quarantined |
    | High confidence spam | **Organization wins**: Email quarantined | **Organization wins**: Spoof action in the applicable anti-phishing policy | **Organization wins**: Email quarantined | **Organization wins**: Email quarantined |
    | Spam | **Organization wins**: Email quarantined | **Organization wins**: Spoof action in the applicable anti-phishing policy | **Organization wins**: Email quarantined | **Organization wins**: Email quarantined |
    | Bulk | **Organization wins**: Email quarantined | **Organization wins**: Spoof action in the applicable anti-phishing policy | **Organization wins**: Email quarantined | **Organization wins**: Email quarantined |
    | Not spam | **Organization wins**: Email quarantined | **Organization wins**: Spoof action in the applicable anti-phishing policy | **Organization wins**: Email quarantined | **Organization wins**: Email quarantined |

### When user and organization settings conflict

The following table describes how conflicts are resolved if both user allow/block settings and organization allow/block settings affect a message:

| Type of organization allow/block | User's Safe Senders/Recipients list | User's Blocked Senders list |
| --- | --- | --- |
| Block entries in the Tenant Allow/Block List for: <br>- Email addresses and domains<br>- Files<br>- URLs | **Organization wins**: Email quarantined | **Organization wins**: Email quarantined |
| Block entries for spoofed senders in the Tenant Allow/Block List | **Organization wins**: Spoof intelligence action in the applicable anti-phishing policy | **Organization wins**: Spoof intelligence action in the applicable anti-phishing policy |
| Advanced delivery policy | **User wins**: Email delivered to mailbox | **Organization wins**: Email delivered to mailbox |
| Block settings in anti-spam policies | **User wins**: Email delivered to mailbox | **User wins**: Email delivered to user's Junk Email folder |
| Honor DMARC policy | **User wins**: Email delivered to mailbox | **User wins**: Email delivered to user's Junk Email folder |
| Blocks by mail flow rules | **User wins**: Email delivered to mailbox | **User wins**: Email delivered to user's Junk Email folder |
| Allows by: <br>- Mail flow rules<br>- IP Allow List (connection filter policy)<br>- Allowed sender and domain list (anti-spam policies)<br>- Tenant Allow/Block List | **User wins**: Email delivered to mailbox | **User wins**: Email delivered to user's Junk Email folder |