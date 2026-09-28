---
layout: FAQ
title: Anti-spam protection FAQ - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/anti-spam-protection-faq
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

  <p>This article provides frequently asked questions and answers about anti-spam protection for Microsoft 365 organizations with cloud mailboxes.</p>

  <p>For questions and answers about the quarantine, see <a href="quarantine-faq">Quarantine FAQ</a>.</p>

  <p>For questions and answers about anti-malware protection, see <a href="anti-malware-protection-faq">Frequently asked questions: Anti-malware protection</a>.</p>

  <p>For questions and answers about anti-spoofing protection, see <a href="anti-phishing-protection-spoofing-faq">Anti-spoofing protection FAQ</a>.</p>
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
ms.date: 2026-07-24T00:00:00.0000000Z
f1.keywords:
- NOCSH
author: chrisda
ms.author: chrisda
audience: ITPro
ms.article: faq
ms.localizationpriority: medium
search.appverid:
- MET150
ms.assetid: c534a35d-b121-45da-9d0a-ce738ce51fce
ms.collection:
- m365-security
- tier2
ms.custom:
- seo-marvel-apr2020
- msecd-doc-authoring-1015
description: Admins can view frequently asked questions and answers about anti-spam protection in Microsoft 365 organizations with cloud mailboxes.
ms.service: defender-office-365
ai-usage: ai-assisted
locale: en-us
document_id: 5fb697a6-bb3b-8ffa-b0ba-ca0b9728ad7b
document_version_independent_id: 5fb697a6-bb3b-8ffa-b0ba-ca0b9728ad7b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/anti-spam-protection-faq.yml
site_name: Docs
depot_name: Learn.defender-office-365
page_type: faq
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: anti-spam-protection-faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/anti-spam-protection-faq.yml
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: b3d6c91e-5f43-907e-68a8-bcdd41ba5b7d
---

# Anti-spam protection FAQ - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

**Applies to**

- [Built-in security features for all cloud mailboxes](eop-about)
- [Microsoft Defender for Office 365 Plan 1 and Plan 2](mdo-about#defender-for-office-365-plan-1-vs-plan-2-cheat-sheet)
- [Microsoft Defender XDR](/en-us/defender-xdr/microsoft-365-defender)

This article provides frequently asked questions and answers about anti-spam protection for Microsoft 365 organizations with cloud mailboxes.

For questions and answers about the quarantine, see [Quarantine FAQ](quarantine-faq).

For questions and answers about anti-malware protection, see [Frequently asked questions: Anti-malware protection](anti-malware-protection-faq).

For questions and answers about anti-spoofing protection, see [Anti-spoofing protection FAQ](anti-phishing-protection-spoofing-faq).

## By default, what happens to a message that's detected as spam?

- **Inbound messages:** Most spam is detected via connection filtering at the edge of the service, which is based on the IP address of the source email server. Anti-spam policies (also known as spam filter policies or content filter policies) inspect and classify messages as bulk, spam, high confidence spam, phishing, or high confidence phishing.

    Anti-spam policies are used in the Standard and Strict preset security policies. You can create custom anti-spam policies that apply to specific groups of users. There's also a default anti-spam policy that applies to all recipients who aren't specified in the Standard and Strict preset security policies or in custom policies.

    By default, messages that are identified as spam are moved to the Junk Email folder by the Standard preset security policy, custom anti-spam policies (configurable), and the default anti-spam policy (configurable). In the Strict preset security policy, spam messages are quarantined.

    For more information, see [Configure anti-spam policies](anti-spam-policies-configure) and [Recommended anti-spam policy settings](recommended-settings-for-eop-and-office365#anti-spam-policy-settings).

    Important

    In environments where the built-in security features for all cloud mailboxes protect on-premises Exchange mailboxes, you need to configure Exchange mail flow rules (also known as transport rules) in your on-premises Exchange organization to recognize the spam filtering verdicts from the cloud. For details, see [Deliver cloud-detected spam to the Junk Email folder in on-premises mailboxes](/en-us/exchange/standalone-eop/configure-eop-spam-protection-hybrid).

    After you manually create the rule in Microsoft 365 to match the rule in on-premises Exchange, the rule replicates in hybrid environments.
- **Outbound messages:** The message is either routed through the [high-risk delivery pool](outbound-spam-high-risk-delivery-pool-about) or is returned to the sender in a non-delivery report (also known as an NDR or bounce message). For more information, see [Outbound spam protection](outbound-spam-protection-about).

## What's a zero-day spam variant and how is it handled by the service?

A zero-day spam variant is a first generation, previously unknown variant of spam that's never been captured or analyzed, so our anti-spam filters can't yet detect it. After a zero-day spam sample is captured and analyzed by our spam analysts, if it meets the spam classification criteria, our anti-spam filters are updated to detect it, and it's no longer considered "zero-day."

Note

If you receive a message that might be a zero-day spam variant, to help us improve the service, submit the message to Microsoft using one of the methods described in [Report messages and files to Microsoft](submissions-report-messages-files-to-microsoft).

## Do I need to configure the service to provide anti-spam protection?

No. The default anti-spam policy protects all current and future cloud recipients in your Microsoft 365 organization after you sign up for the service and add your domain.

As an admin, you can use the following methods to further refine anti-spam protection:

- Add users to the Standard and Strict preset security policies.
- Edit the default spam filtering settings in the default anti-spam policy.
- Create anti-spam policies that apply to specified users, groups, or domains in your organization.

For more information, see the following articles:

- [Recommended anti-spam policy settings](recommended-settings-for-eop-and-office365#anti-spam-policy-settings)
- [Configure anti-spam policies](anti-spam-policies-configure)
- [Preset security policies](preset-security-policies)

## If I change an anti-spam policy, how long does it take for the changes to take effect?

Changes might take up to 1 hour to take effect after you save them.

## If I modify a distribution group that's used to scope an anti-spam policy, how long does it take for the changes to take effect for added or removed group members?

Policy enforcement might be delayed when you add a user to a group that's used to scope an existing policy. This delay isn't caused by policy update latency. Instead, group membership expansion and caching latency cause the delay. Anti-spam and other threat policy rule objects rely on the same rules engine used by Exchange mail flow rules (also known as transport rules), so they inherit the same group membership evaluation behavior. If a policy change needs to take effect quickly for a specific user, scope the policy to the individual rather than a group.

## Is bulk email filtering automatically enabled?

Yes. For more information about bulk email, see [What's the difference between junk email and bulk email?](anti-spam-spam-vs-bulk-about) and [Bulk complaint level (BCL)](anti-spam-bulk-complaint-level-bcl-about).

## Does the service provide URL filtering?

Yes, the service has a URL filter that checks for URLs within messages. If URLs associated with known spam or malicious content are detected, the message is marked as spam.

Customers with Microsoft Defender for Office 365 licenses also get Safe Links protection. For more information, see [Safe Links in Microsoft Defender for Office 365](safe-links-about).

## How can Microsoft 365 customers send false positive (bad) and false negative (good) messages to Microsoft?

See [Report messages and files to Microsoft](submissions-report-messages-files-to-microsoft).

## Can I get spam reports?

Yes. The following reports are available:

- [Spam detections report](reports-email-security#spam-detections-report)
- [Threat protection status report](reports-email-security#threat-protection-status-report)
- [Submissions report (admins)](reports-email-security#submissions-report)
- [User reported messages report](reports-email-security#user-reported-messages-report)

## Someone sent me a message and I can't find it. I suspect that it may have been detected as spam. Is there a tool that I can use to find out?

Yes, the message trace tool enables you to follow email messages as they pass through the service, to find out what happened to them. For more information about how to use the message trace tool to find out why a message was marked as spam, see [Was a message marked as spam?](/en-us/exchange/monitoring/trace-an-email-message/message-trace-faq#was-a-message-marked-as-spam).

## Does the service throttle (rate limit) my mail if users send outbound spam?

If more than half of the email sent by a user within a certain time frame (for example, per hour) is identified as spam, the user is blocked from sending messages. In most cases, outbound spam is routed through the high-risk delivery pool, which reduces the probability of the normal outbound IP pool being added to blocklists.

Notifications are automatically sent when users are blocked due to sending outbound spam or exceeding sending limits. For more information, see [Outbound spam protection](outbound-spam-protection-about).

## Can I use a non-Microsoft anti-spam and anti-malware provider with Microsoft 365?

Yes. Although we recommend that you point your MX record directly to Microsoft, we realize that there are legitimate business reasons to route your email to somewhere other than Microsoft first.

- **Inbound**: Change your MX records to point to the non-Microsoft provider, who then routes the messages to Microsoft 365 for delivery. For more information, see [Enhanced Filtering for connectors in Exchange Online](/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/enhanced-filtering-for-connectors).
- **Outbound**: Configure smart host routing from Microsoft 365 to the destination non-Microsoft provider.

## Does Microsoft have any documentation about how I can protect myself from phishing scams?

Yes. For more information, see [Protect your privacy on the internet](https://support.microsoft.com/windows/ffe36513-e208-7532-6f95-a3b1c8760dfa)

## Are spam and malware messages being investigated as to who sent them, or being transferred to law enforcement entities?

The service focuses on spam and malware detection and removal, though we might occasionally investigate especially dangerous or damaging campaigns and pursue the perpetrators. This pursuit might involve working with our legal and digital crime units to take down a botnet, blocking the spammer from using the service (if they're using it for sending outbound email), and passing the information on to law enforcement for criminal prosecution.

## What are the best practices for outbound mail that help to ensure my mail is delivered?

The guidelines at [External senders - Troubleshoot email sent to Microsoft 365](external-senders-mail-flow-troubleshooting#best-practices-for-bulk-emailing-to-microsoft-365-users) and the following guidelines are best practices for sending outbound email messages:

- **The source email domain should resolve in DNS**: For example, if the sender is user@fabrikam, the domain fabrikam resolves to the IP address 192.168.43.10.

    If a sending domain has no A-record and no MX record in DNS, the service routes the message through its higher risk delivery pool, regardless of the message content. For more information about the high risk delivery pool, see [High-risk delivery pool for outbound messages](outbound-spam-high-risk-delivery-pool-about).
- **The source email server should have a reverse DNS (PTR) entry**: For example, if the email source IP address is 192.168.43.10, the reverse DNS entry would be `43-10.any.icann.org`.
- **The HELO/EHLO and MAIL FROM commands should be consistent, present, and use a domain name rather than an IP address**: The HELO/EHLO command should be configured to match the reverse DNS of the sending IP address. This setting helps ensure that the domain remains the same across the various parts of the message headers.
- **Ensure that proper SPF records are set up in DNS**: SPF records are a mechanism for validating that mail sent from a domain really is coming from that domain and isn't spoofed. For more information about SPF records, see the following links:

    - [Set up SPF to identify valid email sources for your custom cloud domains](email-authentication-spf-configure)
    - [Domains FAQ](/en-us/microsoft-365/admin/setup/domains-faq#how-can-i-validate-spf-records-for-my-domain)
- **Signing email with DKIM, sign with relaxed canonicalization**: If a sender wants to sign their messages using Domain Keys Identified Mail (DKIM) and they want to send outbound mail through the service, they should sign using the relaxed header canonicalization algorithm. Signing with strict header canonicalization may invalidate the signature when it passes through the service.
- **Domain owners should have accurate information in the WHOIS database**: This configuration identifies the owners of the domain and how to contact them by entering the stable parent company, point of contact, and name servers.
- **Format outbound bounce messages**: When messages generate non-delivery reports (also known as NDRs or bounce messages), senders should follow the format of a bounce as specified in [RFC 3464](https://www.ietf.org/rfc/rfc3464.txt).
- **Remove bounced email addresses for non-existent users**: If you receive an NDR indicating that an email address is no longer in use, remove the non-existent email alias from your list. Email addresses change over time, and people sometimes discard them.
- **Use Outlook.com's Smart Network Data Services (SNDS) program**: For more information, see [Smart Network Data Service](https://sendersupport.olc.protection.outlook.com/snds/).

## How do I turn off spam filtering?

If you use a non-Microsoft protection service or device to scan email before it's delivered to Microsoft 365, you can use a mail flow rule (also known as a transport rule) to bypass most spam filtering for incoming messages. For instructions, see [Use mail flow rules to set the spam confidence level (SCL) in messages](/en-us/exchange/security-and-compliance/mail-flow-rules/use-rules-to-set-scl). Scanning for malware and high confidence phishing messages can't be skipped.

If you use a non-Microsoft protection service or device to scan email before it's delivered to Microsoft 365, you should also enable Enhanced Filtering for Connectors (also known as *skip listing*) so detection, reporting, and investigation features in Microsoft 365 are able to correctly identify message sources. For more information, see [Enhanced Filtering for Connectors](/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/enhanced-filtering-for-connectors).

If you need to bypass spam filtering for SecOps mailboxes or phishing simulations, don't use mail flow rules. For more information, see [Configure the delivery of non-Microsoft phishing simulations to users and unfiltered messages to SecOps mailboxes](advanced-delivery-policy-configure).

## Why was my legitimate email flagged as spam?

Legitimate email can be incorrectly flagged as spam (a *false positive*) for several reasons. The following table describes the most common causes and what to do about them:

| Cause | Details | Resolution |
| --- | --- | --- |
| **Email authentication failure** | The message failed SPF, DKIM, or DMARC checks, which caused composite authentication (`compauth`) to fail. Microsoft 365 treats unauthenticated messages with higher suspicion. | Verify that [SPF](email-authentication-spf-configure), [DKIM](email-authentication-dkim-configure), and [DMARC](email-authentication-dmarc-configure) are correctly configured for the sending domain. |
| **Sender reputation** | The sending IP address or domain has a poor reputation due to historical spam complaints, blocklist entries, or low sending volume. | Check whether the sending IP is on any non-Microsoft blocklists. Verify the sender's IP has a valid reverse DNS (PTR) record. If the sender is external, ask them to check their reputation at [Microsoft SNDS](https://sendersupport.olc.protection.outlook.com/snds/). |
| **Message content triggers** | The message body, subject, or attachments contain characteristics associated with spam. For example: <br>- Excessive links<br>- URL shorteners<br>- Form tags<br>- Embedded scripts<br>- Image-only content | Review the message content. Check if any [Advanced Spam Filter (ASF) settings](anti-spam-policies-asf-settings-about) are enabled in the applicable anti-spam policy that could flag the content. For example: <br>- **Empty messages**<br>- **Embed tags in HTML**<br>- **JavaScript or VBScript in HTML** |
| **Bulk complaint level (BCL) threshold** | The message was classified as **bulk** because the sender's BCL met or exceeded the threshold configured in the anti-spam policy. Bulk mail (also known as *gray mail*) includes newsletters, promotions, and marketing email that the user previously opted into. | Bulk mail isn't the same as spam. See How to fix bulk email going to the Junk Email folder? in this article. |
| **User or organization overrides** | An Exchange mail flow rule (transport rule), anti-spam policy, or Outlook Blocked Senders list is configured to treat the sender or domain as spam. | - Review mail flow rules on the **Rules** page in the Exchange admin center at https://admin.exchange.microsoft.com/#/transportrules.<br>- Check the applicable anti-spam policy for blocked senders/domains.<br>- Ask the user to check their **Blocked Senders** list in Outlook. |
| **Non-Microsoft filtering interference** | A non-Microsoft email security service routes messages to Microsoft 365, but the original source IP information is lost. Microsoft 365 evaluates the intermediary's IP address instead of the true source, which can cause SPF and authentication failures. | Configure [Enhanced Filtering for Connectors](/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/enhanced-filtering-for-connectors) (also known as *skip listing*) on the inbound connector to preserve the original source IP. |

### How to investigate a false positive

1. **Examine the message headers**: Look at the `X-Forefront-Antispam-Report` header for the bulk complaint level (BCL) and the filtering verdict. Check the `Authentication-Results` header for SPF, DKIM, and DMARC results.

    For more information about interpreting anti-spam headers, see [Anti-spam message headers](message-headers-eop-mdo).
2. **Use Message trace**: In the [Exchange admin center](https://admin.exchange.microsoft.com), go to **Mail flow** &gt; **Message trace** to track the message and see which filtering rule or policy flagged it.
3. **Check Threat Explorer or Real-time detections** (requires Microsoft Defender for Office 365): Use [Threat Explorer](threat-explorer-real-time-detections-about) to find the message and review the detection technology, delivery action, and override details.
4. **Submit the message to Microsoft**: Report the false positive to Microsoft for analysis. For more information, see [Report messages and files to Microsoft](submissions-report-messages-files-to-microsoft).

### How to prevent future false positives

Caution

Allowlists create a high risk of attackers successfully delivering malicious email that would otherwise be filtered. Use allow entries carefully and only when necessary. Messages identified as malware or high confidence phishing are always filtered, regardless of allow list entries.

Use the following methods (in order of preference) to prevent legitimate email from being flagged:

1. **Fix the root cause**: If the false positive is caused by authentication failures, fix the SPF, DKIM, or DMARC configuration. If it's caused by content, work with the sender to adjust the message content.
2. **Report the false positive**: Use the **Submissions** page in the [Microsoft Defender portal](https://security.microsoft.com) to submit the message to Microsoft. If appropriate, Microsoft creates an allow entry in the [Tenant Allow/Block List](tenant-allow-block-list-about). For more information, see [Report good email to Microsoft](submissions-admin#report-good-email-to-microsoft).
3. **Create a Tenant Allow/Block List entry**: Temporarily allow the sender, domain, or URL while Microsoft reviews the submission. For more information, see [Tenant Allow/Block List](tenant-allow-block-list-about).
4. **Use mail flow rules** (with caution): Create a mail flow rule to bypass spam filtering for messages from the specific sender, but only if you're confident the sender is legitimate. For more information, see [Use mail flow rules to set the SCL in messages](/en-us/exchange/security-and-compliance/mail-flow-rules/use-rules-to-set-scl).

For a complete step-by-step guide, see [How to handle legitimate emails getting blocked (false positives)](step-by-step-guides/how-to-handle-false-positives-in-microsoft-defender-for-office-365).

## What's the difference between spam and high-confidence spam?

Microsoft 365 spam filtering identifies inbound messages as **Spam** or **High confidence spam** based on message categorization and other signals.

### Key differences

| - | Spam | High confidence spam |
| --- | --- | --- |
| **Confidence level** | Moderate probability of being spam. | High probability of being spam. |
| **Default action (default policy)** | Move to Junk Email folder. | Move to Junk Email folder. |
| **Default action (Standard preset policy)** | Move to Junk Email folder. | Quarantine. |
| **Default action (Strict preset policy)** | Quarantine. | Quarantine. |
| **User overrides** | Users can retrieve from Junk Email and add to Safe Senders. | Users can retrieve from Junk Email (default policy) or request release from quarantine (preset policies). |
| **Admin configurable** | Yes. The action is configurable in anti-spam policies. | Yes. The action is configurable in anti-spam policies. |
| **Common triggers** | Promotional content patterns, suspicious links, low sender reputation. | Known spam signatures, phishing-like characteristics, embedded scripts, ASF rule matches (for example, empty messages, form tags, JavaScript in HTML). |

The action for both **Spam** and **High confidence spam** verdicts is configurable in anti-spam policies. For more information, see [Configure anti-spam policies](anti-spam-policies-configure) and [Recommended anti-spam policy settings](recommended-settings-for-eop-and-office365#anti-spam-policy-settings).

## How to fix bulk email going to the Junk Email folder?

Bulk email (also known as *gray mail*) includes newsletters, marketing messages, and promotions that users opted in to receive. Unlike spam, bulk email is typically from legitimate senders, but the volume and content characteristics can resemble spam.

Microsoft 365 assigns a [bulk complaint level (BCL)](anti-spam-bulk-complaint-level-bcl-about) to each inbound message. The BCL value ranges from 0 (unlikely bulk) to 9 (most likely bulk). For the full BCL value breakdown, see [Bulk complaint level (BCL)](anti-spam-bulk-complaint-level-bcl-about).

If the BCL of a message meets or exceeds the **bulk email threshold** set in the applicable anti-spam policy, the message is treated as **Bulk** and the configured action is applied (by default, move to Junk Email folder).

### Step 1: Identify the BCL threshold and message BCL

1. **Find the current BCL threshold**: Check the **Bulk email threshold** value in the applicable anti-spam policy. For the default BCL thresholds in each policy type, see [Bulk complaint level (BCL)](anti-spam-bulk-complaint-level-bcl-about). For instructions on viewing the threshold, see [Open the bulk senders insight in the Microsoft Defender portal](anti-spam-bulk-senders-insight#open-the-bulk-senders-insight-in-the-microsoft-defender-portal).
2. **Find the message's BCL value**: Examine the message headers and look for the `X-Microsoft-Antispam` header. The `BCL:` value indicates the bulk complaint level assigned to the message. For example:

    ```text
    X-Microsoft-Antispam: BCL:5;
    ```

### Step 2: Choose a fix

Based on your situation, use one or more of the following methods:

#### Option A: Adjust the BCL threshold (recommended for organization-wide tuning)

If too many legitimate bulk messages are going to the Junk Email folder, **raise the BCL threshold** in the applicable anti-spam policy. A higher value means fewer messages are classified as bulk. You can also use the [bulk senders insight](anti-spam-bulk-senders-insight) to simulate the effect of threshold changes before you apply them. For more information, see [How to tune bulk email](anti-spam-spam-vs-bulk-about#how-to-tune-bulk-email) and [Configure anti-spam policies](anti-spam-policies-configure).

Note

Settings in the [Standard or Strict preset security policies](preset-security-policies) override custom anti-spam policy settings for recipients included in those policies.

#### Option B: Change the bulk email action

By default, messages that meet the bulk threshold are moved to the Junk Email folder. You can change this action to **No action** if you want bulk email delivered to the Inbox. For more information, see [Configure anti-spam policies](anti-spam-policies-configure).

- **Microsoft Defender portal**: In the anti-spam policy &gt; **Actions** &gt; set the **Bulk complaint level (BCL) met or exceeded** action to **No action** or another preferred action.
- **PowerShell**:

    ```powershell
    Set-HostedContentFilterPolicy -Identity "<Policy Name>" -BulkSpamAction NoAction
    ```

#### Option C: Allow specific bulk senders

If the issue is limited to a specific sender:

1. **Organization-level: Report the message as not junk**: Use the **Submissions** page in the Microsoft Defender portal at https://security.microsoft.com/reportsubmission to report the message as a false positive. During submission, you can also create an allow entry for the sender in the [Tenant Allow/Block List](tenant-allow-block-list-about). For more information, see [Report good email to Microsoft](submissions-admin#report-good-email-to-microsoft).
2. **User-level: Add to Safe Senders**: The user can add the sender to their **Safe Senders** list in Outlook or Outlook on the web. Messages from Safe Senders aren't delivered to the Junk Email folder. For more information, see [Use Junk Email Filters to control which messages you see](https://support.microsoft.com/office/274ae301-5db2-4aad-be21-25413cede077).

    Admins can use PowerShell to add senders to the Safe Senders list in cloud mailboxes. For more information, see [Configure the safelist collection on a mailbox](configure-junk-email-settings-on-exo-mailboxes#use-exchange-online-powershell-to-configure-the-safelist-collection-on-a-mailbox).

Caution

Don't add domains to Safe Senders lists. Attackers could then successfully deliver email from those domains that would otherwise be filtered.

#### Option D: Use the Promotions folder (Preview)

If available in your organization, you can route bulk email that falls *below* the BCL threshold to a dedicated **Promotions** folder instead of the Inbox.

For more information, see [Deliver bulk mail below the BCL threshold to the Promotions folder](anti-spam-bulk-complaint-level-bcl-about#deliver-bulk-mail-below-the-bcl-threshold-to-the-promotions-folder).

#### Option E: Use the Bulk senders insight

Use the **Bulk senders insight** in the Microsoft Defender portal to identify the top bulk senders delivering mail to your organization. This insight helps you identify which senders to allow, block, or tune thresholds for.

For more information, see [Bulk senders insight](anti-spam-bulk-senders-insight).

### Diagnostic workflow

Use the following workflow to diagnose and fix bulk email routing issues:

- **Is the email going to the Junk Email folder?**
    - **Yes**: Check the message headers for the BCL value.
        - **BCL is greater than the BCL threshold**: The message is classified as bulk. To fix it, do one of the following actions:
            - Raise the BCL threshold in the anti-spam policy (Option A).
            - Change the Bulk action to No action (Option B).
            - Allow the specific sender (Option C).
        - **BCL is less than the BCL threshold**: Not a bulk issue. Check the spam filtering verdict:
            - Identified as Spam: See Why was my legitimate email flagged as spam?.
            - Identified as High confidence spam.
    - **No**: The email is delivering correctly.

### Related bulk email resources

- [What's the difference between junk email and bulk email?](anti-spam-spam-vs-bulk-about)
- [Bulk complaint level (BCL) values](anti-spam-bulk-complaint-level-bcl-about)
- [Tune bulk email filtering](anti-spam-spam-vs-bulk-about#how-to-tune-bulk-email)
- [Bulk senders insight](anti-spam-bulk-senders-insight)
- [Configure anti-spam policies](anti-spam-policies-configure)