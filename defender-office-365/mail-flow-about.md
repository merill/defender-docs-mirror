---
layout: Conceptual
title: Mail flow in Microsoft 365 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/mail-flow-about
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: overview
ms.localizationpriority: medium
ms.assetid: e109077e-cc85-4c19-ae40-d218ac7d0548
ms.custom:
- seo-marvel-apr2020
description: Admin can learn about the options for configuring mail flow and routing in all organizations with cloud mailboxes.
ms.service: defender-office-365
ms.collection:
- m365-security
- tier3
ms.date: 2025-07-09T00:00:00.0000000Z
locale: en-us
document_id: 95ec4cf9-39be-748d-13e4-2b549aa73867
document_version_independent_id: 95ec4cf9-39be-748d-13e4-2b549aa73867
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/mail-flow-about.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-about
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/mail-flow-about.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
platformId: 31e83d14-6cf3-9a6a-21ce-99ae15e944ee
---

# Mail flow in Microsoft 365 - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

In all organizations with cloud mailboxes, all messages sent to your organization pass through [the built-in security features for all cloud mailboxes](eop-about) before users see them. You have options about how to route messages before they're routed to user mailboxes.

## Working with messages and message access options

Microsoft 365 offers flexibility in how your messages are routed. The following articles explain steps in the mail flow process:

- [Directory Based Edge Blocking](/en-us/exchange/mail-flow-best-practices/use-directory-based-edge-blocking) rejects messages to invalid recipients at the service network perimeter by default.
- [View or edit accepted domains in Microsoft 365](/en-us/exchange/mail-flow-best-practices/manage-accepted-domains/manage-accepted-domains) describes how to manage email domains associated with Microsoft 365.
- You can manage subdomains you add to your organization. Learn more about subdomains at [Enable mail flow for subdomains in Exchange Online](/en-us/exchange/mail-flow-best-practices/manage-accepted-domains/enable-mail-flow-for-subdomains).
- [Configure mail flow using connectors](/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/use-connectors-to-configure-mail-flow) introduces connectors and shows how you can use them to customize mail routing. Scenarios include ensuring secure communication with a partner organization and setting up a smart host.
- [Enhanced Filtering for Connectors](/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/enhanced-filtering-for-connectors) describes how to configure connectors if your internet mail is routed to a service or device before delivery to Microsoft 365.
- In environments where the built-in security features for all cloud mailboxes protect on-premises Exchange mailboxes, you need to configure Exchange mail flow rules (also known as transport rules) in your on-premises Exchange organization to recognize the spam filtering verdicts from the cloud. For details, see [Deliver cloud-detected spam to the Junk Email folder in on-premises mailboxes](/en-us/exchange/standalone-eop/configure-eop-spam-protection-hybrid).

    If you don't want to move messages to each user's Junk Email folder, you can choose another action by editing the default anti-spam policy or custom anti-spam policies. For more information, see [Actions in anti-spam policies](anti-spam-protection-about#actions-in-anti-spam-policies).

## Verify mail flow

To verify that Microsoft 365 mail flow is working correctly, use the following tests:

- Send an email message from any web-based email account to a recipient in your Microsoft 365 organization.
- Send an email messages from a user in your organization to a web-based email account.
- If you configured connectors for email communication between an on-premises environment or a partner organization, you can use the built-in connector validation to test mail flow. For more information, see [Validate connectors in Exchange Online](/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/validate-connectors).

## Support for anonymous inbound email over IPv6

Microsoft 365 supports receiving anonymous inbound email over IPv6, but it might not be enabled in your organization. You can tell by the following error:

> 
> 550 5.2.1 Service unavailable, [contoso.com] does not accept email over IPv6.

If you get this error, you can opt in to anonymous inbound email over IPv6 support by [opening a support request](/en-us/microsoft-365/admin/get-help-support).

After you opt in, the source email server must meet both of the following requirements for successful email delivery:

- The source IPv6 address must have a valid reverse DNS lookup (PTR) record that allows the destination to find the domain name from the IPv6 address. If it doesn't, you get the following error:

> 
> 450 4.7.25 Service unavailable, sending IPv6 address [2a01:111:f200:2004::240] must have reverse DNS record.
- The sender's domain must pass either Sender Policy Framework (SPF) or DomainKeys Identified Mail (DKIM) verification. For more information about email authentication records in Microsoft 365, see [Email authentication](email-authentication-about). If it doesn't, you get the following error:

> 
> 450 4.7.26 Service unavailable, message sent over IPv6 [2a01:111:f200:2004::240] must pass either SPF or DKIM validation.

Anonymous email from IPv6 sources goes through [the built-in security features for all cloud mailboxes](eop-about) and Microsoft Defender for Office 365.

## Mail flow delivery FAQ

This FAQ provides information about queued, deferred, and bounced messages in Microsoft 365.

### Why is mail queuing?

Messages are queued or deferred if the service is unable to make a connection to the destination server for delivery. Messages aren't deferred if a 500-series (permanent) error is returned from the destination server.

### How does a message become deferred?

Messages are held when a connection to the destination server can't be made, and the destination server returns temporary errors. For example, connection time out, connection refused, or other 400-series errors. 500-series (permanent) errors result in return of the message in a non-delivery report (also known as an NDR or bounce message).

### How long does a message remain in deferral and what is the retry interval?

Deferred messages remain in our queues for one day. Retry attempts are based on the errors that we receive from the destination email server. The first few deferrals are 15 minutes or less. The interval for subsequent retries increases to a maximum of 60 minutes. The interval duration expansion is dynamic, and considers multiple variables (queue size, internal message priority, etc.).

### After communication to the email server is restored, how are queued messages distributed?

Queued messages are automatically processed in the order in which they were received, and are queued for delivery when the server became unavailable.