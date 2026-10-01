---
layout: Conceptual
title: User reported settings in Teams - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/submissions-teams
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
ms.custom:
- msecd-doc-authoring-1016
- sfi-ga-nochange
description: Admins can configure whether users can report malicious messages or calls in Microsoft Teams.
ms.service: defender-office-365
ms.date: 2026-09-28T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 1d442262-3a46-5714-423c-d3a453a7b613
document_version_independent_id: 1d442262-3a46-5714-423c-d3a453a7b613
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/submissions-teams.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: submissions-teams
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/submissions-teams.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 9ce7187e-81c0-8e4d-8bf6-c51859036975
---

# User reported settings in Teams - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

In organizations with Microsoft Defender for Office 365 Plan 1 or Plan 2, or Microsoft Defender XDR, admins can decide whether users can report messages or calls in Microsoft Teams. The following clients support reporting:

- The Microsoft Teams desktop client.
- The Microsoft Teams Web App.
- The Microsoft Teams app for iOS/iPadOS: Version 7.15 or later (messages only).
- The Microsoft Teams app for Android: Version 1416/1.0.0.2025153104 or later (messages only).

Users can report Teams messages from chats, channels, and meeting conversations as malicious or non-malicious. They can also report Teams calls from their call history as scam or not scam. Admins can view the Teams messages and calls that users report.

For more information, watch the following video:

Note

User reporting of calls and messages in Teams is not supported in U.S. Government organizations (Microsoft 365 GCC, GCC High, and DoD).

For information about user reporting of email messages, see [Report suspicious email messages to Microsoft](submissions-report-messages-files-to-microsoft).

## User reporting settings for Teams items

User reporting of messages or calls in Teams consists of two separate settings:

- **In the Teams admin center**: On by default and controls whether users are able to report items from Teams. When this setting is turned off, users can't report items within Teams, so the corresponding setting in the Microsoft Defender portal is irrelevant.
- **In the Microsoft Defender portal**: On by default for new tenants. Existing tenants need to enable it. If user reporting of messages is turned on in the Teams admin center, it also needs to be turned on in the Defender portal for user reported messages to show up correctly on the **User reported** tab on the **Submissions** page.

Important

- When a user reports a Teams message or call to Microsoft, all data directly associated with the item is copied and included in ongoing algorithm reviews. This information includes:

    - Message content.
    - Headers.
    - Attachments.
    - Routing metadata.
    - Call metadata and any other related information.
- The submission might also include contextual data for the reported message. Specifically, up to fifteen messages before and after the reported message might also be shared for analysis.
- Microsoft treats this feedback as your organization's authorization to analyze the submitted information to improve hygiene algorithms. Submitted content is stored in secured, compliance-audited data centers located in the USA and is deleted as soon as it's no longer required.
- Microsoft personnel might read submitted messages, calls, and files, which is typically not permitted for Teams items in Microsoft 365. However, your submission remains confidential between you and Microsoft and isn't shared with any third party during the review process. Microsoft might also use AI to evaluate and generate responses tailored to your submission. Microsoft doesn't use customer data to train any generative AI foundation models, except pursuant to the customer's documented instructions.

### Turn off or turn on user reporting in the Teams admin center

To view or configure user reporting in the Teams admin center, you need to be a member of the **Global Administrator**^\*^ or **Teams Administrator** roles. For more information about permissions in Teams, see [Use Microsoft Teams administrator roles to manage Teams](/en-us/microsoftteams/using-admin-roles).

Important

Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.

1. In the Teams admin center, go to the **Settings & policies** page at https://admin.teams.microsoft.com/one-policy/settings.
2. On the **Settings & policies** page, select either the **Global (Org-wide) default settings** tab for all users or **Custom policies for users & groups** for specific users.
3. On the selected tab (**Global (Org-wide) default settings** or **Custom policies for users & groups**), go to the **Messaging** section and select **Messaging**. If you selected the **Custom policies for users & groups** tab in the previous step, do one of the following steps to edit the specific policy:

    - Click on the policy name in the **Name** column.
    - Click anywhere in the row other than the **Name** column, and then select the ![](media/defender-portal-icon-edit.png)**Edit** action that appears.
4. In the policy details page that opens, find the **Report a security concern** toggle, and verify the value is ![](media/scc-toggle-on.png)**On**.

    If the value is ![](media/scc-toggle-off.png)**Off**, move the toggle to ![](media/scc-toggle-on.png)**On**, and then select **Save**.

    [![Screenshot of the Report a security concern toggle in the policy details page in the Teams admin center.](media/submissions-teams-turn-on-off-tac-security-risk.png)](media/submissions-teams-turn-on-off-tac-security-risk.png#lightbox)
5. In the Teams admin center, go to the **Messaging settings** page at https://admin.teams.microsoft.com/one-policy/settings/messaging.
6. On the **Messaging settings** page, go to the **Messaging safety** section, find the **Report incorrect security detections** toggle, and verify the value is ![](media/scc-toggle-on.png)**On**.

    If the value is ![](media/scc-toggle-off.png)**Off**, move the toggle to ![](media/scc-toggle-on.png)**On**, and then select **Save**.

    [![Screenshot of the Report incorrect security detections toggle on the Messaging settings page in the Microsoft Teams admin center.](media/submissions-teams-turn-on-off-tac-not-security-risk.png)](media/submissions-teams-turn-on-off-tac-not-security-risk.png#lightbox)
7. In the Teams admin center, go to the **Calling settings** page at https://admin.teams.microsoft.com/one-policy/settings/calling.
8. On the **Calling settings** page, go to the **General** section, find the **Report a call** toggle, and verify the value is ![](media/scc-toggle-on.png)**On**.

    If the value is ![](media/scc-toggle-off.png)**Off**, move the toggle to ![](media/scc-toggle-on.png)**On**, and then select **Save**.

    [![Screenshot of the Report a call toggle on the Calling settings page in the Microsoft Teams admin center.](media/submissions-teams-turn-on-off-tac-security-risk-call.png)](media/submissions-teams-turn-on-off-tac-security-risk-call.png#lightbox)

For more information about messaging policies in Teams, see [Manage messaging policies in Teams](/en-us/microsoftteams/messaging-policies-in-teams). For more information about calling policies in Teams, see [Manage calling policies in Teams](/en-us/microsoftteams/teams-calling-policy).

### Turn off or turn on user reporting in the Defender portal

To modify the **Monitor reported items in Microsoft Teams** setting in the Defender portal, you need to be a member of the **Organization Management** or **Security Administrator** role groups. For more information about permissions in the Defender portal, see [Permissions in the Microsoft Defender portal](mdo-portal-permissions).

The **Monitor reported items in Microsoft Teams** setting is meaningful only if Teams message or call reporting is turned on in the Teams admin center.

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Settings** &gt; **Email & collaboration** &gt; **Teams user reported settings** tab. To go directly to the **Teams user reported settings** page, use https://security.microsoft.com/securitysettings/teamsUserSubmission.
2. On the **Teams user reported settings** page, go to the **Microsoft Teams** section for the **Monitor reported items in Microsoft Teams** setting.

    The **Monitor reported items in Microsoft Teams** setting is turned on by default for new tenants; existing tenants need to enable it. Typically, you leave it turned on if message or call reporting is also turned on in Teams admin center. For more information, see [Report suspicious email messages to Microsoft](submissions-report-messages-files-to-microsoft#report-suspicious-email-messages-to-microsoft).

    [![Screenshot of the 'Monitor reported items in Microsoft Teams' setting in the Microsoft Defender portal.](media/submissions-teams-turn-on-off-defender-portal.png)](media/submissions-teams-turn-on-off-defender-portal.png#lightbox)

For more information about email user reported item settings in the Defender portal, see [Email user reported settings](submissions-user-reported-messages-custom-mailbox).

### Use Exchange Online PowerShell to configure user reporting in Teams

To view or configure user reporting in Teams by using PowerShell, connect to [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

To view the current Teams user reporting configuration, run the following command:

```powershell
Get-ReportSubmissionPolicy -Identity DefaultReportSubmissionPolicy |
    Format-List ReportChatMessageEnabled,ReportChatMessageToCustomizedAddressEnabled,ReportChatMessageAddresses
```

For detailed syntax and parameter information, see [Set-ReportSubmissionPolicy](/en-us/powershell/module/exchangepowershell/set-reportsubmissionpolicy).

#### Send reported Teams items to Microsoft only

Tip

The value `-ReportChatMessageEnabled $true` is required to achieve **Send reported items to** &gt; **Microsoft only**. The values `-EnableUserEmailNotification $true` and `-ReportChatMessageToCustomizedAddressEnabled $false` are also required.

```powershell
Set-ReportSubmissionPolicy -Identity DefaultReportSubmissionPolicy `
    -ReportChatMessageEnabled $true `
    -ReportChatMessageToCustomizedAddressEnabled $false `
    -EnableUserEmailNotification $true
```

#### Send reported Teams items to the reporting mailbox only

Tip

The value `-ReportChatMessageEnabled $false` is required to achieve **Send reported items to** &gt; **My reporting mailbox only**. The value `-ReportChatMessageToCustomizedAddressEnabled $true` is also required.

```powershell
Set-ReportSubmissionPolicy -Identity DefaultReportSubmissionPolicy `
    -ReportChatMessageEnabled $false `
    -ReportChatMessageToCustomizedAddressEnabled $true `
    -ReportChatMessageAddresses "securityadmin@contoso.com"
```

#### Send reported Teams items to Microsoft and the reporting mailbox

```powershell
Set-ReportSubmissionPolicy -Identity DefaultReportSubmissionPolicy `
    -ReportChatMessageEnabled $true `
    -ReportChatMessageToCustomizedAddressEnabled $true `
    -ReportChatMessageAddresses "securityadmin@contoso.com"
```

To change the reporting mailbox without changing the reported item destination, run the following command:

```powershell
Set-ReportSubmissionPolicy -Identity DefaultReportSubmissionPolicy `
    -ReportChatMessageAddresses "securityadmin@contoso.com"
```

## How users report items in Teams

Tip

- Reported items remain visible to users.
- Users can report the same items multiple times.
- Message senders aren't notified their messages were reported.
- The caller isn't notified that their calls were reported.

### Report malicious messages in Teams

Follow these steps to report a malicious message in Teams:

1. In the Microsoft Teams client, hover over the malicious message without selecting it, then select ![](media/defender-portal-icon-more-actions.png)**More options** &gt; **Report this message**.

    [![Screenshot of the select path to report a message in the Microsoft Teams client.](media/submissions-user-report-message-in-teams-client-click-path.png)](media/submissions-user-report-message-in-teams-client-click-path.png#lightbox)
2. In the **report this message** dialog that opens, verify **Security risk - Spam, phishing, malicious content** is selected, and then select **Report**.

    [![Screenshot of the final dialog to report a message in the Microsoft Teams client.](media/submissions-user-report-message-in-teams-client-click-report.png)](media/submissions-user-report-message-in-teams-client-click-report.png#lightbox)

    Note

    If [reporting for Microsoft Purview Communication Compliance is turned off](/en-us/purview/communication-compliance-policies#user-reported-messages-policy), users might not have the dropdown list to select **Security risk - Spam, phishing, malicious content**. Instead, they're shown a confirmation pop-up.
3. In the confirmation dialog that opens, select **Close**.

### Report non-malicious messages in Teams

Follow these steps to report a non-malicious message in Teams:

1. In the Teams chat or channel, hover over the message without selecting it, then select ![](media/defender-portal-icon-more-actions.png)**More options** &gt; **Report this message**.
2. In the **Report this message** dialog that opens, select **Not a security concern**, then select **Report**.

### Report calls in Teams

All completed or missed one-to-one and group calls are supported.

1. In the Microsoft Teams client, go to the call history view and select ![](media/defender-portal-icon-more-actions.png)**More options** &gt; **Report call**.

    [![Screenshot of the select path to report a call in the Microsoft Teams client.](media/submissions-user-report-calls-in-teams-client-click-path.png)](media/submissions-user-report-calls-in-teams-client-click-path.png#lightbox)
2. In the **Report call** dialog that opens, verify **Security concern - Spam, phishing, malicious call** is selected, and then select **Report**.

    [![Screenshot of the final dialog to report a call in the Microsoft Teams client.](media/submissions-user-report-call-in-teams-client-click-report.png)](media/submissions-user-report-call-in-teams-client-click-report.png#lightbox)
3. In the confirmation dialog that opens, select **Close**.

## What happens after a user reports items from Teams?

What happens to a user reported Teams item depends on the settings in the **Reported items destinations** section on the **User reported settings** page at https://security.microsoft.com/securitysettings/userSubmission:

User reporting in Teams is supported only for users with an online Teams mailbox. The reporting mailbox configured in **User reported settings** must also be an Exchange Online mailbox. On-premises mailboxes aren't supported in either scenario.

- **Send the reported items to** &gt; **Microsoft and my reporting mailbox**: The default user reporting mailbox is the Exchange Online mailbox of the global admin. The value for older Microsoft 365 organizations is unchanged.
- **Send the reported items to** &gt; **Microsoft only**
- **Send the reported items to** &gt; **My reporting mailbox only**

For more information, see [User reported settings](submissions-user-reported-messages-custom-mailbox).

**Notes**:

- For shared channel user reports, the report goes to the organization that owns/created the channel.
- If you select **Send the reported items to** &gt; **My reporting mailbox only**, reported items don't go to Microsoft for analysis unless an admin manually submits the item from the **User reported** tab on the **Submissions** page at https://security.microsoft.com/reportsubmission?viewid=user. Reporting items to Microsoft is an important part of training the service to help improve the accuracy of filtering (reduce false positives and false negatives). That's why we use **Send the reported items to** &gt; **Microsoft and my reporting mailbox** as the default.
- Regardless of the **Send the reported items to** setting, the following actions occur when a user reports a Teams item:

    - Metadata from the reported Teams items (for example, senders/callers, recipients, reported by, and item details) is available on the **User reported** tab on the **Submissions** page.
    - The alert policies named **Teams message reported by user as a security risk**, **Teams message reported by user as a not security risk**, **Teams call reported by user as a security risk**, and **Teams call reported by user as a not security risk** generate alerts by default. For more information, see [Manage alerts](/en-us/defender-xdr/alert-policies#manage-alerts).

    To view the corresponding alert for a user reported item in Teams, go to the **User reported** tab on the **Submissions** page, and then double-click the item to open the submission flyout. Select ![](media/defender-portal-icon-more-actions.png)**More options** and then select **View alert**.

## View and triage user reported items in Teams

Information about user reported items in Teams is available on the **User reported** tab on the **Submissions** page at https://security.microsoft.com/reportsubmission?viewid=user. For more information, see [View user reported items to Microsoft](submissions-admin#view-user-reported-messages-to-microsoft).