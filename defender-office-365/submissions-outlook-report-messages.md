---
layout: Conceptual
title: Report phishing and suspicious emails in Outlook for admins - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/submissions-outlook-report-messages
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
- tier1
description: Learn how users report phishing and suspicious emails in supported Outlook clients using the built-in Report button, and how admins configure where those reports are sent and review them in Microsoft 365.
ms.service: defender-office-365
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: b42e4760-166e-7bff-bc05-7185eb24cdd7
document_version_independent_id: b42e4760-166e-7bff-bc05-7185eb24cdd7
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/submissions-outlook-report-messages.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: submissions-outlook-report-messages
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/submissions-outlook-report-messages.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
platformId: 518913ea-e14e-518f-46d1-0631bde367f7
---

# Report phishing and suspicious emails in Outlook for admins - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

In Microsoft 365 organizations with mailboxes in Exchange Online, users can report phishing and suspicious email in Outlook. Users can report false positives (good email that was blocked or sent to their Junk Email folder) and false negatives (unwanted email or phishing that was delivered to their Inbox) from Outlook on all platforms using free tools from Microsoft.

Microsoft provides the built-in **Report** button in [supported versions of Outlook](submissions-outlook-report-messages#use-the-built-in-report-button-in-outlook) on virtually all Outlook platforms for users to report good and bad messages.

For more information about reporting messages to Microsoft, see [Report messages and files to Microsoft](submissions-report-messages-files-to-microsoft).

Admins configure user reported messages to go to a specified reporting mailbox, to Microsoft, or both. These reported messages are available on the **User reported** tab on the **Submissions** page in the Microsoft Defender portal. For more information, see [User reported settings](submissions-user-reported-messages-custom-mailbox).

Tip

As a companion to this article, see our [Microsoft Defender for Office 365 setup guide](https://setup.cloud.microsoft/defender/office-365-setup-guide) to review best practices and to protect against email, link, and collaboration threats. Features include Safe Links, Safe Attachments, and more. For a customized experience based on your environment, you can access the [Microsoft Defender for Office 365 automated setup guide](https://admin.microsoft.com/Adminportal/Home?Q=ADG#/modernonboarding/office365advancedthreatprotectionadvisor) in the Microsoft 365 admin center.

## Use the built-in Report button in Outlook

The built-in **Report** button is available in the following versions of Outlook:

- Outlook for Microsoft 365:
    - **Current channel**: Version 16.0.17827.15010 or later
    - **Monthly Enterprise Channel**: Version 16.0.18025.20000 or later
    - **Semi-Annual Channel (Preview)**: Release 2502, build 16.0.18526.20024 or later
    - **Semi-Annual Channel**: Release 2502, build 16.0.18526.20024 or later
- Outlook for Mac version 16.89 (24090815) or later^\*^
- Outlook for iOS version 4.2511 or later^\*^
- Outlook for Android version 4.2446 or later^\*^
- The new Outlook for Windows^\*^
- Outlook on the web^\*^

^\*^ In this version of Outlook, the built-in **Report** button also supports reporting messages from shared mailboxes or other mailboxes by a delegate. The delegate user needs [Send As permissions](/en-us/microsoft-365/admin/add-users/give-mailbox-permissions-to-another-user) to report messages from the shared mailbox. Without Send As permission, the reported message is **not** sent to the reporting mailbox. Instead, the reported message is removed from the folder only.

The **Report** button is available in supported versions of Outlook if both of the following conditions are true:

- User reporting is turned on.
- The built-in **Report** button is configured in the [user reported settings](submissions-user-reported-messages-custom-mailbox) at https://security.microsoft.com/securitysettings/userSubmission.

If user reporting is turned off and a non-Microsoft add-in button is selected, the **Report** button isn't available in supported versions of Outlook.

### Use the built-in Report button in Outlook to report junk and phishing messages

Users can use the built-in **Report** button to report junk or phishing messages in supported versions of Outlook:

- Users can report a message as junk from the Inbox or any email folder other than Junk Email folder.
- Users can report a message as phishing from any email folder.

In a supported version of Outlook, select one or more messages, select **Report**, and then select **Report phishing** or **Report junk** in the dropdown list. For example:

- **Outlook for Microsoft 365**:

[![Screenshot of selecting the Report button after selecting a message in Outlook](media/outlook-report-junk-phishing.png)](media/outlook-report-junk-phishing.png#lightbox)
- **Outlook on the web**:

[![Screenshot of selecting the Report button after selecting multiple messages in Outlook on the web.](media/owa-report-junk-phishing.png)](media/owa-report-junk-phishing.png#lightbox)

Based on the [User reported settings](submissions-user-reported-messages-custom-mailbox) in your organization, messages reported as junk or phishing are sent to the reporting mailbox, to Microsoft, or both. The following actions are also taken on messages that users report with the **Report** button:

- **Reported as junk**: The messages are moved to the Junk Email folder, and the sender is automatically added to the user's Blocked Senders list.
- **Reported as phishing**: The messages are deleted.

### Use the built-in Report button in Outlook to report messages that aren't junk

In a supported version of Outlook, select one or more messages in the Junk Email folder, select **Report**, and then select **Not junk** in the dropdown list. For example:

- **Outlook for Microsoft 365**:

[![Screenshot of the Not junk selection from the Report button after selecting a message in the Junk Email folder in Outlook on the web.](media/outlook-report-as-not-junk.png)](media/outlook-report-as-not-junk.png#lightbox)
- **Outlook on the web**:

[![Screenshot of the Not junk selection from the Report button after selecting multiple messages in the Junk Email folder in Outlook on the web.](media/owa-report-as-not-junk.png)](media/owa-report-as-not-junk.png#lightbox)

Based on the [User reported settings](submissions-user-reported-messages-custom-mailbox) in your organization, messages reported as Not junk are sent to the reporting mailbox, to Microsoft, or both. Messages reported as Not junk are also moved out of Junk Email to the Inbox.

## Review reported messages

To review messages that users reported to Microsoft, admins can use the **User reported** tab on the **Submissions** page in the Microsoft Defender portal at https://security.microsoft.com/reportsubmission. For more information, see [View user reported messages to Microsoft](submissions-admin#view-user-reported-messages-to-microsoft).

Note

If the [User reported settings](submissions-user-reported-messages-custom-mailbox) in the organization send user reported messages (email and [Microsoft Teams](submissions-teams)) to Microsoft (exclusively or in addition to the reporting mailbox), we do the same checks as when admins submit messages to Microsoft for analysis from the **Submissions** page. So, submitting or resubmitting messages to Microsoft is useful to admins only for messages that were never submitted to Microsoft, or when admins disagree with the original verdict.