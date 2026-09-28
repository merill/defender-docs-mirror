---
layout: Conceptual
title: Outbound delivery pools - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/outbound-spam-high-risk-delivery-pool-about
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
ms.assetid: ac11edd9-2da3-462d-8ea3-bbf9dbc6f948
ms.collection:
- m365-security
- tier2
description: Learn how the delivery pools are used to protect the reputation of email servers in the Microsoft 365 datacenters.
ms.service: defender-office-365
ms.date: 2026-06-25T00:00:00.0000000Z
ms.custom: sfi-ga-nochange
locale: en-us
document_id: fae8aa8c-8243-0516-d124-47fd855a0407
document_version_independent_id: fae8aa8c-8243-0516-d124-47fd855a0407
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/outbound-spam-high-risk-delivery-pool-about.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: outbound-spam-high-risk-delivery-pool-about
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/outbound-spam-high-risk-delivery-pool-about.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
platformId: d40cd5bf-43cc-dc68-79ca-d2308a88982c
---

# Outbound delivery pools - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

Email servers in the Microsoft 365 datacenters might be temporarily guilty of sending spam. For example, a malware or malicious spam attack in an on-premises email organization that sends outbound mail through Microsoft 365, or compromised Microsoft 365 accounts. Attackers also try to avoid detection by relaying messages through Microsoft 365 forwarding.

These scenarios can result in the IP address of the affected Microsoft 365 datacenter servers appearing on non-Microsoft blocklists. Destination email organizations that use these blocklists will reject email from those Microsoft 365 messages sources.

## High-risk delivery pool

To prevent our IP addresses from being blocked, all outbound messages from Microsoft 365 datacenter servers that are determined to be spam are sent through the *high-risk delivery pool*.

The high risk delivery pool is a separate IP address pool for outbound email that's only used to send "low quality" messages (for example, spam and [backscatter](anti-spam-backscatter-about). Using the high risk delivery pool helps prevent the normal IP address pool for outbound email from sending spam. The normal IP address pool for outbound email maintains the reputation sending "high quality" messages, which reduces the likelihood that these IP addresses appear on IP blocklists.

The possibility that IP addresses in the high-risk delivery pool are placed on IP blocklists remains, but this behavior is by design. Delivery to the intended recipients isn't guaranteed, because many email organizations don't accept messages from the high risk delivery pool.

For more information, see [Control outbound spam](outbound-spam-protection-about) and [Troubleshoot outbound sending limits in Exchange Online](outbound-spam-sending-limits-troubleshoot).

Note

Messages where the source email domain has no A record and no MX record defined in public DNS are always routed through the high-risk delivery pool, regardless of their spam or sending limit disposition.

Messages that exceed the following limits are blocked, so they aren't sent through the high-risk delivery pool:

- The [sending limits of the service](/en-us/office365/servicedescriptions/exchange-online-service-description/exchange-online-limits#sending-limits-across-office-365-options).
- [Outbound spam policies](outbound-spam-policies-configure) where the senders are restricted from sending mail.

### Bounce messages

The outbound high-risk delivery pool manages the delivery of all non-delivery reports (also known as NDRs or bounce messages). Possible causes for a surge in NDRs include:

- A spoofing campaign that affects one of the customers using the service.
- A directory harvest attack.
- A spam attack.
- A rogue email server.

Any of these issues can result in a sudden increase in the number of NDRs being processed by the service. These NDRs often appear to be spam to other email servers and services (also known as *[backscatter](anti-spam-backscatter-about)*).

### Relay pool

In certain scenarios, messages that are forwarded or relayed via Microsoft 365 are sent using a special relay pool, because the destination shouldn't consider Microsoft 365 as the actual sender. It's important for us to isolate this email traffic, because there are legitimate and invalid scenarios for auto forwarding or relaying email out of Microsoft 365. Similar to the high-risk delivery pool, a separate IP address pool is used for relayed mail. This address pool isn't published because it can change often, and it's not part of published SPF record for Microsoft 365.

Microsoft 365 needs to verify that the original sender is legitimate so we can confidently deliver the forwarded message.

To avoid using the relay pool, a forwarded or relayed message must meet at least one of the following criteria when it arrives at Microsoft 365:

- The outbound sender is in an [accepted domain](/en-us/exchange/mail-flow-best-practices/manage-accepted-domains/manage-accepted-domains) of the organization.
- SPF passes for the sending domain when the message arrives at Microsoft 365.

In cases where we can authenticate the sender, we use Sender Rewriting Scheme (SRS) to help the recipient email system know that the forwarded message is from a trusted source. You can read more about how that works and what you can do to help make sure the sending domain passes authentication in [Sender Rewriting Scheme (SRS) in Office 365](/en-us/office365/troubleshoot/antispam/sender-rewriting-scheme).

To improve authentication of forwarded mail, make sure DKIM is enabled for the sending domain. For example, if fabrikam.com is part of contoso.com and is defined in the accepted domains of the organization, and the sender is `sender@fabrikam.com`, enable DKIM for fabrikam.com. This improvement helps authentication, but by itself it doesn't prevent routing through the relay pool, as described in the criteria above. To enable DKIM, see [Set up DKIM to sign mail from your cloud domain](email-authentication-dkim-configure).

To add a custom domain, follow the steps in [Add a domain to Microsoft 365](/en-us/microsoft-365/admin/setup/add-domain).

If the MX record for your domain points to a non-Microsoft service or an on-premises email server, you should use [Enhanced Filtering for Connectors](/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/enhanced-filtering-for-connectors). Enhanced Filtering ensures SPF validation is correct for inbound mail and avoids sending email through the relay pool.

### Find out which outbound pool was used

As an Exchange Service Administrator or Global Administrator^\*^, you might want to find out which outbound pool was used to send a message from Microsoft 365 to an external recipient.

Important

^\*^ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.

To do so, you can [use Message trace](/en-us/exchange/monitoring/trace-an-email-message/message-trace-modern-eac) and look for the `OutboundIpPoolName` property in the output. This property contains a friendly name value for the outbound pool that was used.