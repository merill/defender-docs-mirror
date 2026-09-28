---
layout: Conceptual
title: Quarantined email messages in Microsoft 365 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/quarantine-about
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
ms.assetid: 4c234874-015e-4768-8495-98fcccfc639b
ms.collection:
- m365-security
- tier1
ms.custom:
- seo-marvel-apr2020
- msecd-doc-authoring-1015
description: Learn about email quarantine in Microsoft 365, including which detections quarantine messages, how retention works, and how admins and users manage quarantined items.
ms.service: defender-office-365
ms.date: 2026-07-17T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 7c3c4140-f617-8f92-e2e9-6c250492e0d2
document_version_independent_id: 7c3c4140-f617-8f92-e2e9-6c250492e0d2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/quarantine-about.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: quarantine-about
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/quarantine-about.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: bf1e86fb-ee72-9d97-2621-41be0c8f7a3e
---

# Quarantined email messages in Microsoft 365 - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

In all organizations with cloud mailboxes, quarantine is available to hold potentially dangerous or unwanted messages.

Note

In Microsoft 365 operated by 21Vianet in China, quarantine isn't currently available in the Microsoft Defender portal. Quarantine is available only in the classic Exchange admin center (classic EAC).

You can't completely turn off quarantine in Microsoft 365. Malware and high-confidence phishing messages are always quarantined to protect the service. Admins can reduce quarantined messages by changing actions to deliver messages to the Junk Email folder instead of quarantine in anti-spam policies and anti-phishing policies.

Whether a detected message is quarantined by default depends on the following factors:

- The protection feature that detected the message. For example, the following detections are always quarantined:
    - Malware detections by [anti-malware policies](anti-malware-policies-configure)^\*^.
    - Malware or phishing detections by [Safe Attachments policies](safe-attachments-policies-configure), including [Built-in protection](preset-security-policies) for Safe Attachments^\*^.
    - High confidence phishing detections by [anti-spam policies](anti-spam-policies-configure).
- Whether you're using the Standard or Strict [preset security policies](preset-security-policies). The Strict profile quarantines more types of detections than the Standard profile.

^\*^ Malware filtering is skipped on SecOps mailboxes that are identified in the advanced delivery policy. For more information, see [Configure the advanced delivery policy for non-Microsoft phishing simulations and email delivery to SecOps mailboxes](advanced-delivery-policy-configure).

The default actions for email protection features in Microsoft 365, including preset security policies, are described in the feature tables in [Recommended email and collaboration threat policy settings for cloud organizations](recommended-settings-for-eop-and-office365).

For anti-spam and anti-phishing protection, admins can also modify the default threat policy or create custom threat policies to quarantine messages instead of delivering them to the Junk Email folder. For instructions, see the following articles:

- [Configure anti-spam policies](anti-spam-policies-configure)
- [Configure anti-phishing policies if you don't have Microsoft Defender for Office 365](anti-phishing-policies-eop-configure)
- [Configure anti-phishing policies in Microsoft Defender for Office 365](anti-phishing-policies-mdo-configure)

Threat policies for [supported features](quarantine-policies#step-2-assign-a-quarantine-policy-to-supported-features) have one or more *quarantine policies* assigned to them (each action within the threat policy has an associated quarantine policy assignment).

Tip

All actions taken by admins or users on quarantined messages are audited. For more information about audited quarantine events, see [Quarantine schema in the Office 365 Management API](/en-us/office/office-365-management-api/office-365-management-activity-api-schema#quarantine-schema).

## Quarantine policies

*Quarantine policies* define what users can or can't do to quarantined messages, and whether users receive quarantine notifications for those messages. For more information, see [Anatomy of a quarantine policy](quarantine-policies#anatomy-of-a-quarantine-policy).

Tip

You can create customized [quarantine notifications for different languages](quarantine-policies#customize-quarantine-notifications-for-different-languages). You can also [use a custom logo in quarantine notifications](quarantine-policies#customize-all-quarantine-notifications).

The default quarantine policies assigned to protection feature verdicts enforce the historical capabilities that users get for their quarantined messages (messages where they're a recipient). For more information, see the table in [Find and release quarantined messages as a user](quarantine-end-user).

For example, only admins can work with messages that were quarantined as malware or high confidence phishing. By default, users can work with their messages that were quarantined as spam, bulk, phishing, spoof, user impersonation, domain impersonation, or mailbox intelligence.

Admins can create and apply custom quarantine policies that define less restrictive or more restrictive capabilities for users, and also turn on quarantine notifications. For more information, see [Create quarantine policies](quarantine-policies#step-1-create-quarantine-policies-in-the-microsoft-defender-portal).

Both users and admins can work with quarantined messages:

- Admins can work with all types of quarantined messages for all users, including messages that were quarantined as malware, high confidence phishing, or as a result of mail flow rules (also known as transport rules). For more information, see [Manage quarantined messages and files as an admin](quarantine-admin-manage-messages-files).

    Tip

    For the permissions required to download and release all messages from quarantine, see [What do you need to know before you begin?](quarantine-admin-manage-messages-files#what-do-you-need-to-know-before-you-begin) in Manage quarantined messages and files as an admin.
- Users can work with their quarantined messages based on the protection feature that quarantined the message, and the setting in corresponding quarantine policy. For more information, see [Find and release quarantined messages as a user](quarantine-end-user).

    Note

    Recipients can't release quarantined messages in the following scenarios, regardless of how the quarantine policy is configured:

    - Messages quarantined as malware by anti-malware policies.
    - Messages quarantined as malware or phishing by Safe Attachments policies.
    - Messages quarantined as high confidence phishing by anti-spam policies.

    If the quarantine policy allows recipients to release messages, they can only *request* the release of these quarantined messages.
- Admins can report false positives to Microsoft from quarantine. For more information, see [Take action on quarantined email](quarantine-admin-manage-messages-files#take-action-on-quarantined-email) and [Take action on quarantined files](quarantine-admin-manage-messages-files#take-action-on-quarantined-files).
- Users can also report false positives to Microsoft from quarantine, based on the **Reporting from quarantine** setting in [user reported settings](submissions-user-reported-messages-custom-mailbox).

### Quarantine retention

How long quarantined messages or files are held in quarantine before they expire depends on why the message or file was quarantined. Features and their corresponding retention periods are described in the following table:

| Quarantine reason | Default retention period | Customizable? | Comments |
| --- | --- | --- | --- |
| Messages quarantined by anti-spam policies as spam, high confidence spam, phishing, high confidence phishing, or bulk. | 15 days <br>- The default anti-spam policy.<br>- Anti-spam policies you create in PowerShell or the Microsoft Defender portal.<br><br> 30 days <br>- Standard and Strict [preset security policies](preset-security-policies#appendix) | Yes^\*^ | You can configure the value from 1 to 30 days in the default anti-spam policy and in custom anti-spam policies. For more information, see the **Retain spam in quarantine for this many days** (*QuarantineRetentionPeriod*) setting in [Configure anti-spam policies](anti-spam-policies-configure). ^\*^You can't change the value in the Standard or Strict preset security policies. |
| Messages quarantined by anti-phishing policies: <br>- **Anti-phishing policies for all cloud mailboxes**: Spoof intelligence.<br>- **Anti-phishing policies in Defender for Office 365**: User impersonation protection, domain impersonation protection, and mailbox intelligence protection. | 15 days or 30 days | Yes^\*^ | This retention period is also controlled by the **Retain spam in quarantine for this many days** (*QuarantineRetentionPeriod*) setting in **anti-spam** policies. The retention period is the value from the first matching **anti-spam** policy that the recipient is defined in. |
| Messages quarantined by anti-malware policies (malware messages). | 30 days | No | If you turn on the *common attachments filter* in anti-malware policies (in the default policy or in custom policies), file attachments in email messages to the affected recipients are treated as malware based solely on the file extension using true type matching. A predefined list of mostly executable file types is used by default, but you can customize the list. For more information, see [Common attachments filter in anti-malware policies](anti-malware-protection-about#common-attachments-filter-in-anti-malware-policies). |
| Messages quarantined by mail flow rules where the action is **Deliver the message to the hosted quarantine** (*Quarantine*). | 30 days | No |  |
| Messages quarantined by Safe Attachments policies in Defender for Office 365 (malware or phishing messages). | 30 days | No |  |
| Messages quarantined by Safe Attachments policies in Defender for Office 365 that contain encrypted (password-protected) attachments that can't be scanned. | 30 days | No | Admins can release these messages without a password. Users can supply the attachment password to have their own messages rescanned and possibly released, if the quarantine policy allows it. For more information, see [Encrypted (password-protected) attachments in Safe Attachments policies](safe-attachments-about#encrypted-password-protected-attachments-in-safe-attachments-policies). |
| Files quarantined by Safe Attachments for SharePoint, OneDrive, and Microsoft Teams (malware files). | 30 days | No | Files quarantined in SharePoint or OneDrive are removed from quarantine after 30 days, but the blocked files remain in SharePoint or OneDrive in the blocked state. |
| Messages in chats and channels quarantined by zero-hour auto protection (ZAP) for Microsoft Teams in Defender for Office 365 | 30 days | No |  |

When messages expire from quarantine after the retention period, the messages are permanently deleted and can't be recovered.

For more information about quarantine, see [Quarantine FAQ](quarantine-faq).