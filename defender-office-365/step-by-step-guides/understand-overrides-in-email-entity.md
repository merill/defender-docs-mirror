---
layout: Conceptual
title: Understand Overrides Within the Email Entity Page in Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/step-by-step-guides/understand-overrides-in-email-entity
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Shows the different overrides in the email entity page in Microsoft Defender for Office 365 to help admins troubleshoot configurations.
author: MSFTBen
ms.author: benharri
ms.service: defender-office-365
ms.topic: how-to
audience: ITPro
ms.collection:
- m365-guidance-templates
- m365-security
- tier3
ms.date: 2026-07-24T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 5936c2b3-6d48-2e02-d9ec-7865db02693a
document_version_independent_id: 5936c2b3-6d48-2e02-d9ec-7865db02693a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/step-by-step-guides/understand-overrides-in-email-entity.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: step-by-step-guides/understand-overrides-in-email-entity
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/step-by-step-guides/understand-overrides-in-email-entity.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 2705c16e-8142-90c0-5c1d-5ab65e3f586b
---

# Understand Overrides Within the Email Entity Page in Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn

Within the Microsoft Defender for Office 365 *[email entity page](../mdo-email-entity-page)*, there's a wealth of useful information about an email, including if applicable the **overrides** which affected that message, and potentially the location that the message was delivered or moved to post delivery.

This article is all about helping you **understand the different overrides**, how they're triggered, and helpful information for diagnosing when the effect of an override was unexpected, such as an email being blocked when no threats were found.

## Understand the overrides details table

The following table lists all overrides, a description of what that override means and some starting points for troubleshooting. Not all overrides are honored, depending on the circumstance. For example an email that contains malware is automatically blocked regardless if an end user set the sender as a "safe sender". To learn more about how overrides are applied, see [How policies and protections are combined](../how-policies-and-protections-are-combined).

| Override | Description | Notes |
| --- | --- | --- |
| Third Party Filter | We detected your MX record points to a non-Microsoft service and you have a [mail flow rule that bypasses most Microsoft 365 filtering](/en-us/exchange/security-and-compliance/mail-flow-rules/use-rules-to-set-scl) (SCL -1) and [secure by default](../secure-by-default). |  |
| Admin initiated time travel | Admin triggered investigation, which leads to zero-hour auto purge (ZAP) modifying the delivery location of messages. | [Zero-hour auto purge (ZAP)](../zero-hour-auto-purge) |
| Antimalware policy block by file type | The file extension for an attachment within the message matched a banned file type listed in the anti-malware policy for the recipient | You may wish to tweak the file extensions listed in the Common attachments filter section of the anti-malware policy. [Configure anti-malware policies](../anti-malware-policies-configure). |
| Antispam policy settings | The message matched a custom option in the anti-spam policy for the recipient. For example: "SPF record: hard fail" or "Empty messages". | Check the "Mark as spam" options in the anti-spam policy for the affected recipient. [Configure anti-spam policies](../anti-spam-policies-configure). |
| Connection policy | The message originated from an allowed / blocked IP within your connection filter policy. | Check the "Connection filter policy" within the anti-spam policies section of the security portal. [Configure connection filter policies](../connection-filter-policies-configure). |
| Exchange transport rule | The message matched a custom transport rule that affected the final delivery location. | You can use the email entity page, or Exchange message trace to highlight which transport rule was triggered. [Mail flow rules in Exchange Online](/en-us/exchange/security-and-compliance/mail-flow-rules/mail-flow-rules). |
| Exclusive mode (User override) | The recipient has chosen to mark all messages as spam unless they're received from a sender in their trusted contact list. | The recipient has likely configured: "Don't trust email unless it comes from someone in my Safe Senders and Recipients list" within the Junk email settings in Outlook or OWA. [Learn more](/en-us/powershell/module/exchangepowershell/set-mailboxjunkemailconfiguration). |
| Filtering skipped due to on-premises organization | The message was marked as nonspam by your Exchange on-premises environment before being delivered to Exchange Online | You should review your on-premises environment to locate the source of the override. |
| IP region filter from policy | The message was detected as coming from a country/region that an admin has selected to block in the anti-spam policy for the recipient. | Modify the "From these countries/regions" option within the anti-spam policy applied to the affected recipient. [Configure anti-spam policies](../anti-spam-policies-configure). |
| Language filter from policy | The message was detected as containing a language that an admin has selected to block in the anti-spam policy for the recipient. | Modify the "Contains specific languages" option within the anti-spam policy to the affected recipient. [Configure anti-spam policies](../anti-spam-policies-configure). |
| Phishing simulation | The message met the criteria defined by an administrator to be considered a phishing simulation message. | Criteria are within the "Phishing simulation" tab within Advanced delivery in the security portal. [Configure Advanced delivery policy](../advanced-delivery-policy-configure). |
| Quarantine release | The recipient or an administrator released this message from quarantine. | [Release messages from quarantine](../quarantine-end-user). |
| SecOps Mailbox | The message was sent to the specific security operations mailbox defined by an administrator. | Mailboxes are defined within the "SecOps mailbox" tab within Advanced delivery in the security portal. [Configure Advanced delivery policy](../advanced-delivery-policy-configure). |
| Sender address list (Admin Override) | The message matched an entry in the allowed/blocked senders within the anti-spam policy for the recipient. | Check the "Allowed and blocked senders and domains" section of the relevant anti-spam policy. (allows with this method aren't recommended). [Create safe sender lists in Office 365](../create-safe-sender-lists-in-office-365). |
| Sender address list (User override) | The recipient has manually set this sender address to be delivered to the inbox (allowed) or junk email folder (blocked). | The recipient has likely configured "Safe senders and domains" or "Blocked senders and domains" within the Junk email settings in Outlook or OWA. [Set-MailboxJunkEmailConfiguration cmdlet](/en-us/powershell/module/exchangepowershell/set-mailboxjunkemailconfiguration). |
| Sender domain list (Admin Override) | The message matched an entry in the allowed/blocked domains within the anti-spam policy for the recipient. | Check the "Allowed and blocked senders and domains" section of the relevant anti-spam policy. (allows with this method aren't recommended). [Create safe sender lists in Office 365](../create-safe-sender-lists-in-office-365). |
| Sender domain list (User override) | The recipient has manually set the sending domain to be delivered to the inbox (allowed) or junk email folder (blocked). | The recipient has likely configured "Safe senders and domains" or "Blocked senders and domains" within the Junk email settings in Outlook or OWA. [Set-MailboxJunkEmailConfiguration cmdlet](/en-us/powershell/module/exchangepowershell/set-mailboxjunkemailconfiguration). |
| Tenant Allow/Block List file | An entry was matched for a file hash listed in the Tenant allow/block list. | Review the entires within the "Tenant Allow/Block Lists" page within the security portal. [About the Tenant Allow/Block List](../tenant-allow-block-list-about). |
| Tenant Allow/Block List sender email address | An entry was matched for a sender address listed in the Tenant allow/block list. | Review the entires within the "Tenant Allow/Block Lists" page within the security portal. [About the Tenant Allow/Block List](../tenant-allow-block-list-about). |
| Tenant Allow/Block List spoof | An entry was matched for spoof detection in the Tenant allow/block list. | Review the entires within the "Tenant Allow/Block Lists" page within the security portal. [About the Tenant Allow/Block List](../tenant-allow-block-list-about). |
| Tenant Allow/Block List URL | An entry was matched for a URL listed in the Tenant allow/block list. | Review the entires within the "Tenant Allow/Block Lists" page within the security portal. [About the Tenant Allow/Block List](../tenant-allow-block-list-about). |
| Trusted contact list (User override) | The recipient has chosen to mark contacts in their contacts folder as trusted senders automatically. | The recipient has likely configured: "Trust email from my contacts" within the Junk email settings in Outlook or OWA. [Set-MailboxJunkEmailConfiguration cmdlet](/en-us/powershell/module/exchangepowershell/set-mailboxjunkemailconfiguration). |
| Trusted domain (User override) | The recipient has added this domain to their safe recipients list within Outlook, emails sent to this domain aren't treated as junk email. | The recipient has likely configured "Safe Recipients" within Outlook's Junk email options. [Block or allow junk email settings in Outlook](https://support.microsoft.com/office/block-or-allow-junk-email-settings-48c9f6f7-2309-4f95-9a4d-de987e880e46). |
| Trusted recipient (User override) | The recipient has added this sender to their safe recipients list within Outlook, emails sent to this sender aren't treated as junk email. | The recipient has likely configured "Safe Recipients" within Outlook's Junk email options. [Block or allow junk email settings in Outlook](https://support.microsoft.com/office/block-or-allow-junk-email-settings-48c9f6f7-2309-4f95-9a4d-de987e880e46). |
| Trusted senders only (User override) | This override marks all messages as spam unless they're received from a sender in the recipient's trusted contact list, primarily used in outlook.com. This behavior is the same as Exclusive mode (User override). | The recipient has likely configured: "Don't trust email unless it comes from someone in my Safe Senders and Recipients list" within the Junk email settings. [Set-MailboxJunkEmailConfiguration cmdlet](/en-us/powershell/module/exchangepowershell/set-mailboxjunkemailconfiguration). |