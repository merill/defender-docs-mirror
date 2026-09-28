---
layout: Conceptual
title: Report spam, non-spam, phishing, suspicious emails, Teams messages, and files to Microsoft - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/submissions-report-messages-files-to-microsoft
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.date: 2026-07-22T00:00:00.0000000Z
ms.topic: overview
ms.localizationpriority: medium
ms.assetid: c31406ea-2979-4fac-9288-f835269b9d2f
ms.collection:
- m365-security
- tier1
description: How do I report a suspicious email, Teams message, or file to Microsoft? Report messages, Teams messages, URLs, email attachments, and files to Microsoft for analysis. Learn to report spam email and phishing emails.
ms.service: defender-office-365
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1015
locale: en-us
document_id: 35ce9704-2cc2-852b-e286-715d40f66be6
document_version_independent_id: 35ce9704-2cc2-852b-e286-715d40f66be6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/submissions-report-messages-files-to-microsoft.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: submissions-report-messages-files-to-microsoft
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/submissions-report-messages-files-to-microsoft.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: df70dbf5-7829-01b7-71e1-3615c782e213
---

# Report spam, non-spam, phishing, suspicious emails, Teams messages, and files to Microsoft - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

Wondering what to do with suspicious email messages, Teams messages, URLs, email attachments, or files? In all organizations with cloud mailboxes, *users* and *admins* have different ways to report suspicious email messages, URLs, and email attachments to Microsoft. In organizations with Microsoft Defender for Office 365 Plan 1 or Plan 2, or Microsoft Defender XDR, users can also report suspicious Teams messages and calls.

Admins in Microsoft 365 organizations with Microsoft Defender for Endpoint also have several methods for reporting files.

Watch this video for more information about the unified submissions experience.

Watch this video to learn how users report suspicious email messages, email attachments, and Teams messages to Microsoft.

## Report suspicious email messages to Microsoft

Important

When you make a submission to Microsoft, everything associated with the submission is copied and included in the continual algorithm reviews. This copy includes all data associated with the submission, including message content, headers, any attachments, related data about routing, and all other data directly associated with the submission.

Microsoft treats your submission as your organization's permission to analyze all the information to fine-tune the submission hygiene algorithms. Your submission is held in secured and audited data centers in the USA. The submission is deleted as soon as it's no longer required. Microsoft personnel might read your submitted messages and attachments, which is normally not permitted for customer data in Microsoft 365. However, your submission is still treated as confidential between you and Microsoft, and your data isn't shared with any other party as part of the review process. Microsoft might also use AI to evaluate and create responses tailored to your submissions.

For information about reporting messages and calls in Microsoft Teams in Defender for Office 365 Plan 1 or Plan 2, see [User reported settings in Microsoft Teams](submissions-teams).

| Method | Submission type | Comments |
| --- | --- | --- |
| [The built-in Report button in supported versions of Outlook](submissions-outlook-report-messages#use-the-built-in-report-button-in-outlook) | User |  |
| [The Submissions page in the Microsoft Defender portal](submissions-admin) | Admin | Admins can report good (false positives) and bad (false negatives) messages, email attachments, and URLs (entities) from the available tabs on the **Submissions** page.  Admins can also submit user reported messages from the **User reported** tab on the **Submissions** page to Microsoft for analysis. The **Submissions** page is available only in organizations with cloud mailboxes. |
| Report messages from quarantine | Admin and User | Admins can [submit quarantined messages to Microsoft for analysis](quarantine-admin-manage-messages-files#submit-email-to-microsoft-for-review-from-quarantine) (false positives and false negatives).  If users are allowed to [release their own messages from quarantine](quarantine-end-user#release-quarantined-email), and [user reported settings](submissions-user-reported-messages-custom-mailbox) is configured to allow users to report quarantined messages, users can select **Report message as having no threats** (false positive) when they release a quarantined message. |
| [Report messages and calls in Microsoft Teams](submissions-teams#how-users-report-items-in-teams) | User | In organizations with Defender for Office 365 Plan 1 or Plan 2, or Microsoft Defender XDR, users can report malicious messages and calls in Microsoft Teams. |

Note

If your organization doesn't have Microsoft Defender for Office 365, users and admins can still report suspicious emails by submitting them directly through the Microsoft submission portals (for example, the Microsoft malware or phishing submission sites). Forwarding suspicious emails isn't a replacement for Defender-based reporting and might not include full message metadata required for analysis.

## Related reporting settings for admins

[User reported settings](submissions-user-reported-messages-custom-mailbox) allow admins to configure whether user reported messages go to a specified reporting mailbox, to Microsoft, or both. After this feature is configured, user reported messages appear on the **User reported** tab on the **Submissions** page in the Defender portal.

User reported messages are also available to admins in the following locations in the Microsoft Defender portal:

- [User-reported messages report](reports-email-security#user-reported-messages-report)
- [Automated investigation and response (AIR) results](air-view-investigation-results) (Defender for Office 365 Plan 2)
- [Threat Explorer](threat-explorer-real-time-detections-about) (Defender for Office 365 Plan 2)

In Defender for Office 365, admins can also submit messages from the [Email entity page](mdo-email-entity-page#actions-on-the-email-entity-page) and from [Alerts](/en-us/defender-xdr/investigate-alerts) in the Defender portal.

Admins can use the sample submission portal at https://www.microsoft.com/wdsi/filesubmission to submit other suspected files to Microsoft for analysis. For more information, see [Submit files for analysis](/en-us/defender-xdr/submission-guide).

To report suspected phishing or fraud, you can also go directly to the [Submissions page](https://security.microsoft.com/reportsubmission) in the Defender portal.

If you encounter a tech support scam, report it at [Report a scam](https://www.microsoft.com/concern/scam).

Tip

In U.S. Government organizations (Microsoft 365 GCC, GCC High, and DoD), admins can submit messages to Microsoft for analysis. The messages are analyzed for email authentication and policy checks only. Payload reputation, detonation, and grader analysis aren't done for compliance reasons (data isn't allowed to leave the organization boundary). If you report a message, URL, or email attachment to Microsoft from one of these organizations, you get the following message in the result details:

**Further investigation needed**. Your tenant doesn't allow data to leave the environment, so nothing was found during the initial scan. You'll need to contact Microsoft support to have this item reviewed.