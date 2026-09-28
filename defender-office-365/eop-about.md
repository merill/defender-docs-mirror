---
layout: Conceptual
title: Built-in security features for all cloud mailboxes - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/eop-about
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.date: 2025-12-10T00:00:00.0000000Z
ms.topic: overview
ms.collection:
- m365-security
- tier2
ms.localizationpriority: medium
ms.assetid: 1270a65f-ddc3-4430-b500-4d3a481efb1e
ms.custom:
- seo-marvel-apr2020
description: Learn how the built-in security features for all cloud mailboxes help protect your organization.
ms.service: defender-office-365
locale: en-us
document_id: 7422e842-9912-922e-5523-5270dbaae984
document_version_independent_id: 7422e842-9912-922e-5523-5270dbaae984
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/eop-about.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: eop-about
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/eop-about.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 24fa72d1-1a23-cb88-041a-ef9db0f1bd95
---

# Built-in security features for all cloud mailboxes - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

The built-in security features for all cloud mailboxes help protect your Microsoft 365 organization from spam, malware, phishing and other email threats. These protections are included in all organizations with cloud mailboxes.

These protections are on by default via the default threat policies for:

- [Anti-malware protection](anti-malware-protection-about)
- [Anti-spam protection](anti-spam-protection-about)
- [Anti-phishing (spoofing) protection](anti-phishing-protection-about#anti-phishing-protection-for-all-cloud-mailboxes)

The default threat policies for these features apply to all recipients. You can't turn them off, but you can override them by turning on and configuring [preset security policies](preset-security-policies) or creating custom threat policies.

You can customize the security settings in the default threat policies, create custom threat policies, or better yet, turn on and add all recipients to the Standard and/or Strict preset security policies. For complete information, see [Configure threat policies](mdo-deployment-guide#step-2-configure-threat-policies).

The rest of this article describes the built-in security features for all cloud mailboxes and how they work.

Tip

The built-in security features for all cloud mailboxes are also available in a standalone subscription to protect on-premises email environments (not just Microsoft Exchange). For more information, see [Built-in security add-on for on-premises mailboxes](/en-us/exchange/standalone-eop/standalone-eop).

## How the built-in security features for all cloud mailboxes work

The following diagram shows how the built-in security features for all cloud mailboxes work.

[![A diagram of email from the internet or Customer feedback entering Microsoft 365 and passing through the built-in security features for all cloud mailboxes.](media/tp_emailprocessingineopt3.png)](media/tp_emailprocessingineopt3.png#lightbox)

1. Incoming messages in Microsoft 365 initially pass through connection filtering, which checks the sender's reputation. Most spam is rejected at this point. For more information, see [Configure connection filtering](connection-filter-policies-configure).
2. If malware is found in the message or a message attachment, the message is delivered to quarantine. By default, only admins can view and interact with malware quarantined messages. But, admins can create and use [quarantine policies](quarantine-policies#anatomy-of-a-quarantine-policy) to specify what users are allowed to do to quarantined messages. To learn more about malware protection, see [Anti-malware protection](anti-malware-protection-about).
3. Policy filtering evaluates the message against any [Exchange mail flow rules (also known as transport rules)](/en-us/exchange/security-and-compliance/mail-flow-rules/mail-flow-rules) configured to act on messages. For example, a rule can notify a manager about messages from a specific sender.

    In on-premises organizations with Exchange Enterprise CAL with Services licenses, [data loss prevention (DLP)](/en-us/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention) checks also happen at this point.
4. The message passes through anti-spam and anti-phishing filtering:

    - Anti-spam policies identify messages as bulk, spam, high confidence spam, phishing, or high confidence phishing.

        High confidence phishing messages are always delivered to quarantine. By default, only admins can view and interact with high confidence phishing messages.
    - Anti-phishing policies identify messages as spoofing.

    You can configure the action to take on the message based on the filtering verdict (for example, quarantine or move to the Junk Email folder), and what users can do to the quarantined messages using [quarantine policies](quarantine-policies#anatomy-of-a-quarantine-policy). For more information, see [Configure anti-spam policies](anti-spam-policies-configure) and [Configure anti-phishing policies for all cloud mailboxes](anti-phishing-policies-eop-configure).

A message that successfully passes all of these protection layers is delivered to the recipients.

For more information, see [Order and precedence of email protection](how-policies-and-protections-are-combined).

### Microsoft 365 datacenters

Microsoft 365 runs on a worldwide network of datacenters that are designed to provide the best availability. For example, if a datacenter becomes unavailable, email messages are automatically routed to another datacenter without any interruption in service. Servers in each datacenter accept messages on your behalf, providing a layer of separation between the servers that host your organization and the internet. Through this highly available network, Microsoft can ensure that email reaches your organization in a timely manner.

Microsoft load balances between datacenters *within the same region only*. If you're provisioned in one region, all of your messages are processed using the mail routing for that region.

### Microsoft 365 communications

The following communication channels are available for issues and new features in Microsoft 365:

- When a Service Level Event affects you, a communication alert (typically accompanied by a bell icon) will appear in the Microsoft 365 admin center at https://admin.microsoft.com. We recommend that you read and act on any items as appropriate.
- The Microsoft 365 Message center at https://admin.microsoft.com/Adminportal/Home?#/MessageCenter also contains information about new and updated features. For more information, see [Track new and changed features in the Microsoft 365 Message center](/en-us/microsoft-365/admin/manage/message-center).
- The [Microsoft 365 roadmap](https://www.microsoft.com/microsoft-365/roadmap?filters=&amp;searchterms=exchange%2Conline%2Cprotection) is a good resource for finding out information about upcoming new features.
- We also post blog articles about new features to the [Microsoft 365 Blogs](https://www.microsoft.com/microsoft-365/blog/) website.

### Security features for cloud mailboxes

This section provides a high-level overview of the main built-in security features for all cloud mailboxes.

For information about requirements, important limits, and feature availability across all subscription plans, see the [Built-in security features for cloud mailboxes service description](/en-us/office365/servicedescriptions/exchange-online-protection-service-description/exchange-online-protection-service-description).

Tip

- Microsoft 365 uses several URL blocklists that help detect known malicious links within messages.
- Microsoft 365 uses a vast list of domains known to send spam.
- Microsoft 365 inspects the active payload in the message body and all message attachments for malware.

| Feature | Comments |
| --- | --- |
| **Protection** |  |
| Preset security policies | [Preset security policies](preset-security-policies)[Configuration analyzer](configuration-analyzer-for-security-policies) |
| Anti-malware | [Anti-malware protection](anti-malware-protection-about)[Frequently asked questions: Anti-malware protection](anti-malware-protection-faq)[Configure anti-malware policies](anti-malware-policies-configure) |
| Inbound anti-spam | [Anti-spam protection](anti-spam-protection-about)[Frequently asked questions: Anti-spam protection](anti-spam-protection-faq)[Configure anti-spam policies](anti-spam-policies-configure) |
| Outbound anti-spam | [Outbound spam protection](outbound-spam-protection-about)[Configure outbound spam filtering](outbound-spam-policies-configure)[Control automatic external email forwarding](outbound-spam-policies-external-email-forwarding) |
| Connection filtering | [Configure connection filtering](connection-filter-policies-configure) |
| Anti-phishing | [Anti-phishing policies](anti-phishing-policies-about)[Configure anti-phishing policies for all cloud mailboxes](anti-phishing-policies-eop-configure) |
| Anti-spoofing protection | [Spoof intelligence insight](anti-spoofing-spoof-intelligence)[Manage the Tenant Allow/Block List](tenant-allow-block-list-about) |
| Zero-hour auto purge (ZAP) for delivered malware, spam, and phishing messages | [ZAP in Exchange Online](zero-hour-auto-purge) |
| Tenant Allow/Block List | [Manage the Tenant Allow/Block List](tenant-allow-block-list-about) |
| Blocklists for message senders | [Create sender blocklists](create-block-sender-lists-in-office-365) |
| Allowlists for message senders | [Create sender allowlists](create-safe-sender-lists-in-office-365) |
| Directory Based Edge Blocking (DBEB) | [Use Directory Based Edge Blocking to reject messages sent to invalid recipients](/en-us/exchange/mail-flow-best-practices/use-directory-based-edge-blocking) |
| **Quarantine and submissions** |  |
| Admin submission | [Use Admin submission to submit suspected spam, phish, URLs, and files to Microsoft](submissions-admin) |
| User reported message settings | [User reported settings](submissions-user-reported-messages-custom-mailbox) |
| Quarantine - admins | [Manage quarantined messages and files as an admin](quarantine-admin-manage-messages-files)[Frequently asked questions: Quarantined messages](quarantine-faq)[Report messages and files to Microsoft](submissions-report-messages-files-to-microsoft)[Anti-spam message headers](message-headers-eop-mdo) You can analyze the message headers of quarantined messages using the [Message Header Analyzer at](https://mha.azurewebsites.net/). |
| Quarantine - end-users | [Find and release quarantined messages as a user](quarantine-end-user)[Use quarantine notifications to release and report quarantined messages](quarantine-quarantine-notifications)[Quarantine policies](quarantine-policies) |
| **Mail flow** |  |
| Mail flow rules | [Mail flow rules (transport rules) in Exchange Online](/en-us/exchange/security-and-compliance/mail-flow-rules/mail-flow-rules)[Mail flow rule conditions and exceptions (predicates) in Exchange Online](/en-us/exchange/security-and-compliance/mail-flow-rules/conditions-and-exceptions)[Mail flow rule actions in Exchange Online](/en-us/exchange/security-and-compliance/mail-flow-rules/mail-flow-rule-actions)[Manage mail flow rules in Exchange Online](/en-us/exchange/security-and-compliance/mail-flow-rules/manage-mail-flow-rules)[Mail flow rule procedures in Exchange Online](/en-us/exchange/security-and-compliance/mail-flow-rules/mail-flow-rule-procedures) |
| Accepted domains | [Manage accepted domains in Exchange Online](/en-us/exchange/mail-flow-best-practices/manage-accepted-domains/manage-accepted-domains) |
| Connectors | [Configure mail flow using connectors in Exchange Online](/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/use-connectors-to-configure-mail-flow) |
| Enhanced Filtering for Connectors | [Enhanced filtering for connectors in Exchange Online](/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/enhanced-filtering-for-connectors) |
| **Monitoring** |  |
| Message trace | [Message trace](message-trace-defender-portal)[Message trace in the Exchange admin center](/en-us/exchange/monitoring/trace-an-email-message/message-trace-modern-eac) |
| Email & collaboration reports | [View email security reports](reports-email-security) |
| Mail flow reports | [Mail flow reports in the Exchange admin center](/en-us/exchange/monitoring/mail-flow-reports/mail-flow-reports) |
| Mail flow insights | [Mail flow insights in the Exchange admin center](/en-us/exchange/monitoring/mail-flow-insights/mail-flow-insights) |
| Auditing reports | [Auditing reports in the Exchange admin center](/en-us/exchange/security-and-compliance/exchange-auditing-reports/exchange-auditing-reports) |
| **Service Level Agreements (SLAs) and support** |  |
| Spam effectiveness SLA | &gt; 99% |
| False positive ratio SLA | &lt; 1:250,000 |
| Virus detection and blocking SLA | 100% of known viruses |
| Monthly uptime SLA | 99.999% |
| Phone and web technical support 24 hours a day, seven days a week | [Get support for Microsoft 365 for business](/en-us/microsoft-365/admin/get-help-support). |
| **Other features** |  |
| A geo-redundant global network of servers | Microsoft 365 runs on a worldwide network of datacenters that are designed to help provide the best availability. For more information, see the Microsoft 365 datacenters section earlier in this article. |
| Message queuing when the on-premises server can't accept mail | Messages in deferral remain in our queues for one day. Message retry attempts are based on the error we get back from the recipient's mail system. On average, messages are retried every 5 minutes. For more information, see the [Mail flow delivery FAQ](mail-flow-about#mail-flow-delivery-faq). |
| Office 365 Message Encryption available as an add-on | For more information, see [Encryption in Office 365](/en-us/purview/encryption). |