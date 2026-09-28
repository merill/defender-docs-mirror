---
layout: Conceptual
title: Submit messages, URLs, and attachments for analysis in the Microsoft Defender portal - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/submissions-admin
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
- seo-marvel-apr2020
- sfi-image-nochange
description: 'Admins can learn how to use the Submissions page in the Microsoft Defender portal to submit messages, URLs, and email attachments to Microsoft for analysis. Reasons for submission include: legitimate messages that were blocked, suspicious messages that were allowed, suspected phishing email, spam, malware, and other potentially harmful messages.'
ms.service: defender-office-365
ms.date: 2026-07-30T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 316e988c-f8f1-0687-d41c-fdf6ed808f8b
document_version_independent_id: 316e988c-f8f1-0687-d41c-fdf6ed808f8b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/submissions-admin.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: submissions-admin
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/submissions-admin.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 80e38bb0-f287-72bb-525a-80cdaa78776f
---

# Submit messages, URLs, and attachments for analysis in the Microsoft Defender portal - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

For more information about how Microsoft stores and handles your submissions, see [Report suspicious email messages to Microsoft](submissions-report-messages-files-to-microsoft#report-suspicious-email-messages-to-microsoft).

In Microsoft 365 organizations with Exchange Online mailboxes, admins can use the **Submissions** page in the Microsoft Defender portal to submit messages, URLs, and attachments to Microsoft for analysis. There are two basic types of admin submissions:

- **Admin-originated submissions**: Admins identify and report messages, attachments, or URLs (entities) by selecting ![](media/defender-portal-icon-create.png)**Submit to Microsoft for analysis** from the tabs on the **Submissions** page as described in the Admin-originated submissions section.

    After the admin reports the entity, an entry appears on the corresponding tab on the **Submissions** page (anywhere except the **User reported** tab).
- **Admin submission of user reported messages**: The built-in [user reporting experience](submissions-user-reported-messages-custom-mailbox) is turned on and configured. User reported messages appear on the **User reported** tab on the **Submissions** page, and admins submit or resubmit the messages to Microsoft from the **User reported** tab.

    After an admin submits the message from the **User reported** tab, an entry is also created on the corresponding tab on the **Submissions** page (for example, the **Emails** tab). From the **User reported** tab, admins can review, submit (or resubmit) these messages to Microsoft for analysis, mark them with a verdict, and notify the reporting user. For the full set of admin actions, see Admin options for user reported messages.

When admins or users submit messages to Microsoft for analysis, we do the following checks:

- **Email authentication check** (email messages only): Whether email authentication passed or failed when it was delivered.
- **Policy hits**: Information about any policies or overrides that might have allowed or blocked the incoming email into the organization, thus overriding our filtering verdicts.
- **Payload reputation/detonation**: Up-to-date examination of any URLs and attachments in the message.
- **Grader analysis**: Review done by human graders to confirm whether or not messages are malicious.

Important

In U.S. Government organizations (Microsoft 365 GCC, GCC High, and DoD), admins can submit email messages to Microsoft for analysis, but the messages are analyzed for email authentication and policy hits only. Payload reputation, detonation, and grader analysis aren't done for compliance reasons (data isn't allowed to leave the organization boundary).

Watch this short video to learn how to use admin submissions in Microsoft Defender for Office 365 to submit messages to Microsoft for evaluation.

For more information about how **users** can submit messages and files to Microsoft, see [Report messages and files to Microsoft](submissions-report-messages-files-to-microsoft).

For other ways that **admins** can report messages to Microsoft in the Defender portal, see [Related reporting settings for admins](submissions-report-messages-files-to-microsoft#related-reporting-settings-for-admins).

## Prerequisites

Before you use the **Submissions** page, review the following requirements and considerations:

- You open the Microsoft Defender portal at https://security.microsoft.com/. To go directly to the **Submissions** page, use https://security.microsoft.com/reportsubmission.
- You need to be assigned permissions before you can do the procedures in this article. You have the following options:

    - [Microsoft Defender XDR Unified role based access control (RBAC)](/en-us/defender-xdr/manage-rbac) (If **Email & collaboration** &gt; **Defender for Office 365** permissions is ![](media/scc-toggle-on.png)**Active**. Affects the Defender portal only, not PowerShell): **Security operations/Security data/Response (manage)** or **Security operations/Security data/Security data basics (read)**.
    - [Email & collaboration permissions in the Microsoft Defender portal](mdo-portal-permissions): Membership in the **Security Administrator** or **Security Reader** role groups.
    - [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): Membership in the **Security Administrator** or **Security Reader** roles gives users the required permissions *and* permissions for other features in Microsoft 365.
- Admins can submit email messages as old as 30 days if they're still available in the mailbox and haven't been purged by the user or an admin.
- Admin submissions are throttled at the following rates:

    - Maximum submissions in any 15-minute period: 150 submissions
    - Same submissions in a 24 hour period: Three submissions
    - Same submissions in a 15-minute period: One submission
- If the [User reported settings](submissions-user-reported-messages-custom-mailbox) in the organization send user reported messages (email and [Microsoft Teams](submissions-teams)) to Microsoft (exclusively or in addition to the reporting mailbox), we do the same checks as when admins submit messages to Microsoft for analysis from the **Submissions** page, so submitting or resubmitting messages to Microsoft is useful to admins only for messages that have never been submitted to Microsoft, or when you disagree with the original verdict.
- A **Files** tab is available on the **Submissions** page only in organizations with Microsoft Defender or Microsoft Defender for Endpoint Plan 2. For information and instructions to submit files from the **Files** tab, see [Submit files in Microsoft Defender for Endpoint](/en-us/defender-endpoint/admin-submissions-mde).

## Admin-originated submissions

Tip

The tab where you select select ![](media/defender-portal-icon-create.png)**Submit to Microsoft for analysis** doesn't particularly matter, as long as you set **Select the submission type** to the correct value.

### Report questionable email to Microsoft

To report a questionable email message to Microsoft for analysis, perform the following steps:

1. In the Defender portal at https://security.microsoft.com, go to **Actions & submissions** &gt; **Submissions**. Or, to go directly to the **Submissions** page, use https://security.microsoft.com/reportsubmission.
2. On the **Submissions** page, verify that the **Emails** tab is selected.
3. On the **Emails** tab, select ![](media/defender-portal-icon-create.png)**Submit to Microsoft for analysis**.
4. On the first page of the **Submit to Microsoft for analysis** flyout that opens, enter the following information:

    - **Select the submission type**: Verify the value **Email** is selected.
    - **Add the network message ID or upload the email file**: Select one of the following options:

        - **Add the email network message ID**: The GUID value is available in the **X-MS-Exchange-Organization-Network-Message-Id** header or in the **X-MS-Office365-Filtering-Correlation-Id** header in messages.
        - **Upload the email file (.msg or .eml)**: Select **Browse files**. In the dialog that opens, find and select the .eml or .msg file, and then select **Open**.
    - **Choose at least one recipient who had an issue**: Specify the recipients to run a policy check against. The policy check determines if the email bypassed scanning due to user or organization policies or override.
    - **Why are you submitting this message to Microsoft?**: You can select either:

        - **It appears suspicious**: Select this value only when you don't know or you're unsure of the message verdict and you would like to get a verdict from Microsoft. Select **Submit**, and then go to Step 6.
        - **I've confirmed it's a threat**: In all other cases, select this value after you've already determined the message verdict as malicious. Select one of the following values in the **Choose a category** section that appears:

            - **Phish**
            - **Malware**
            - **Spam**

            Select **Next**.

            [![Submit a false negative (bad) email to Microsoft for analysis on the Submissions page in the Defender portal.](media/admin-submission-email-block.png)](media/admin-submission-email-block.png#lightbox)
5. On the second page of the **Submit to Microsoft for analysis** flyout that opens, you can either:

    - Select **Submit**.
    - Select **Block all emails from this sender or domain**: This option creates a block entry for the sender domain or email address in the Tenant Allow/Block List. For more information about the Tenant Allow/Block List, see [Manage allows and blocks in the Tenant Allow/Block List](tenant-allow-block-list-about).

        After you select this option, the following settings are available:

        - By default, **Sender** is selected but you can select **Domain** instead.
        - **Remove block entry after**: The default value is **30 days**, but you can select from the following values:
            - **1 day**
            - **7 days**
            - **30 days**
            - **Never expire**
            - **Specific date**: The maximum value is 30 days from today.
        - **Block entry note (optional)**: Enter optional information about why you're blocking this item.

        When you're finished on the second page of the **Submit to Microsoft for analysis** flyout, select **Submit**.

        [![Choose whether to create a corresponding block entry for the sender domain or email address in the Tenant Allow/Block List.](media/admin-submission-email-block-page-2.png)](media/admin-submission-email-block-page-2.png#lightbox)
6. Select **Done**.

After a few moments, the block entry is available on the **Domains & addresses** tab on the **Tenant Allow/Block Lists** page at https://security.microsoft.com/tenantAllowBlockList?viewid=Sender.

Note

Admin submissions for on-premises mailboxes are supported only for messages less than 7 days old.

Currently, admin submissions by uploading files from on-premises mailboxes isn't supported.

### Report questionable email attachments to Microsoft

To submit a questionable email attachment to Microsoft for analysis, perform the following steps:

1. In the Defender portal at https://security.microsoft.com, go to **Actions & submissions** &gt; **Submissions**. Or, to go directly to the **Submissions** page, use https://security.microsoft.com/reportsubmission.
2. On the **Submissions** page, select the **Email attachments** tab.
3. On the **Email attachments** tab, select ![](media/defender-portal-icon-create.png)**Submit to Microsoft for analysis**.
4. On the first page of the **Submit to Microsoft for analysis** flyout that opens, enter the following information:

    - **Select the submission type**: Verify the value **Email attachment** is selected.
    - **File**: Select ![](media/defender-portal-icon-import.png)**Browse files** to find and select the file to submit.
    - **Why are you submitting this email attachment to Microsoft?**: Select one of the following values:

        - **It appears suspicious**: Select this value if you're unsure and you want a verdict from Microsoft, select **Submit**, and then go to Step 6.
        - **I've confirmed it's a threat**: Select this value if you're sure that the item is malicious, and then select one of the following values in the **Choose a category** section that appears:

            - **Phish**
            - **Malware**

            Select **Next**.

            [![Submit a false negative (bad) email attachment to Microsoft for analysis on the Submissions page in the Defender portal.](media/admin-submission-file-block.png)](media/admin-submission-file-block.png#lightbox)
5. On the second page of the **Submit to Microsoft for analysis** flyout that opens, you can choose one of the following:

    - Select **Submit**.
    - Select **Block this file**: This option creates a block entry for the file in the Tenant Allow/Block List. For more information about the Tenant Allow/Block List, see [Manage allows and blocks in the Tenant Allow/Block List](tenant-allow-block-list-about).

        After you select this option, the following settings are available:

        - **Remove block entry after**: The default value is **30 days**, but you can select from the following values:
            - **1 day**
            - **7 days**
            - **30 days**
            - **Never expire**
            - **Specific date**: The maximum value is 30 days from today.
        - **Block entry note (optional)**: Enter optional information about why you're blocking this item.

        When you're finished in the **Submit to Microsoft for analysis** flyout, select **Submit**.

    [![Choose whether to create a corresponding block entry for the file in the Tenant Allow/Block List.](media/admin-submission-file-block-page-2.png)](media/admin-submission-file-block-page-2.png#lightbox)
6. Select **Done**.

After a few moments, the block entry is available on the **Files** tab on the **Tenant Allow/Block Lists** page at https://security.microsoft.com/tenantAllowBlockList?viewid=FileHash.

### Report questionable URLs to Microsoft

To report a questionable URL to Microsoft for analysis, perform the following steps:

1. In the Defender portal at https://security.microsoft.com, go to **Actions & submissions** &gt; **Submissions**. Or, to go directly to the **Submissions** page, use https://security.microsoft.com/reportsubmission.
2. On the **Submissions** page, select the **URLs** tab.
3. On the **URLs** tab, select ![](media/defender-portal-icon-create.png)**Submit to Microsoft for analysis**.
4. In the **Submit to Microsoft for analysis** flyout that opens, enter the following information:

    - **Select the submission type**: Verify the value **URL** is selected.
    - **URL**: Enter the full URL (for example, `https://www.fabrikam.com/marketing.html`), and then select it in the box that appears. You can enter up to 50 URLs at once.
    - **Why are you submitting this URL to Microsoft?**: Select one of the following values:

        - **It appears suspicious**: Select this value if you're unsure and you want a verdict from Microsoft, select **Submit**, and then go to Step 6.
        - **I've confirmed it's a threat**: Select this value if you're sure that the item is malicious, and then select one of the following values in the **Choose a category** section that appears:

            - **Phish**
            - **Malware**

            Select **Next**.

            [![Submit a false negative (bad) URL to Microsoft for analysis on the Submissions page in the Defender portal.](media/admin-submission-url-block.png)](media/admin-submission-url-block.png#lightbox)
5. On the second page of the **Submit to Microsoft for analysis** flyout that opens, select one of the following options:

    - Select **Submit**.
    - Select **Block this URL**: This option creates a block entry for the URL in the Tenant Allow/Block List. For more information about the Tenant Allow/Block List, see [Manage allows and blocks in the Tenant Allow/Block List](tenant-allow-block-list-about).

        After you select this option, the following settings are available:

        - **Remove block entry after**: The default value is **30 days**, but you can select from the following values:
            - **1 day**
            - **7 days**
            - **30 days**
            - **Never expire**
            - **Specific date**: The maximum value is 30 days from today.
        - **Block entry note (optional)**: Enter optional information about why you're blocking this item.

        When you're finished in the **Submit to Microsoft for analysis** flyout, select **Submit**.

    [![Choose whether to create a corresponding block entry for the URL in the Tenant Allow/Block List.](media/admin-submission-url-block-page-2.png)](media/admin-submission-url-block-page-2.png#lightbox)
6. Select **Done**.

After a few moments, the block entry is available on the **URL** tab on the **Tenant Allow/Block Lists** page at https://security.microsoft.com/tenantAllowBlockList?viewid=Url.

### Report good email to Microsoft

Note

Submitting a message as "should not have been blocked" doesn't automatically override impersonation protections in your tenant. For recurring legitimate senders flagged by [domain or user impersonation protection](anti-phishing-policies-about#impersonation-settings-in-anti-phishing-policies-in-microsoft-defender-for-office-365), update the **Trusted senders and domains** section in the [anti-phishing policy](anti-phishing-policies-mdo-configure#use-the-microsoft-defender-portal-to-modify-anti-phishing-policies) that detected the message, or create an allow entry in the [Tenant Allow/Block List](tenant-allow-block-list-about).

1. In the Defender portal at https://security.microsoft.com, go to **Actions & submissions** &gt; **Submissions**. Or, to go directly to the **Submissions** page, use https://security.microsoft.com/reportsubmission.
2. On the **Submissions** page, verify that the **Emails** tab is selected.
3. On the **Emails** tab, select ![](media/defender-portal-icon-create.png)**Submit to Microsoft for analysis**.
4. In the first page of the **Submit to Microsoft for analysis** flyout that opens, enter the following information:

    - **Select the submission type**: Verify the value **Email** is selected.
    - **Add the network message ID or upload the email file**: Select one of the following options:

        - **Add the email network message ID**: The GUID value is available in the **X-MS-Exchange-Organization-Network-Message-Id** header in the message or in the **X-MS-Office365-Filtering-Correlation-Id** header in quarantined messages.
        - **Upload the email file (.msg or .eml)**: Select **Browse files**. In the dialog that opens, find and select the .eml or .msg file, and then select **Open**.
    - **Choose at least one recipient who had an issue**: Specify the recipients to run a policy check against. The policy check determines if the email was blocked due to user or organization policies or overrides.
    - **Why are you submitting this message to Microsoft?**: Select one of the following values:

        - **It appears clean**: Select this value only when you don't know or you're unsure of the message verdict and you would like to get a verdict from Microsoft. Select **Submit**, and then go to Step 6.
        - **I've confirmed it's clean**: In all other cases, select this value after you've already determined the message verdict as clean. Select **Next**.

    [![Submit a false positive (good) email to Microsoft for analysis on the Submissions page in the Defender portal.](media/admin-submission-email-allow.png)](media/admin-submission-email-allow.png#lightbox)
5. On the second page of the **Submit to Microsoft for analysis** flyout that opens, select one of the following options:

    - Select **Submit**.
    - Select **Allow this message**: This option creates an allow entry for the elements of the message in the Tenant Allow/Block List. For more information about the Tenant Allow/Block List, see [Manage allows and blocks in the Tenant Allow/Block List](tenant-allow-block-list-about).

        After you select this option, the following settings are available:

        - **Remove allow entry after**: The default value is **45 days after last used date**, but you can select from the following values:

            - **1 day**
            - **7 days**
            - **30 days**
            - **Specific date**: The maximum value is 30 days from today.

            For spoofed senders, this value is meaningless, because entries for spoofed senders never expire.

            When **45 days after last used date** is selected, the last used date of the allow entry is updated when the malicious email message is encountered during mail flow. The allow entry is kept for 45 days after the filtering system determines that the email message is clean. For all other values, the allow entry expires on the defined date (**1 day**, **7 days**, **30 days**, or the **Specific date**).
        - **Allow entry note (optional)**: Enter optional information about why you're allowing this item. For spoofed senders, any value you enter here isn't shown in the allow entry on the **Spoofed senders** tab on the **Tenant Allow/Block Lists** page.

        When you're finished on the second page of the **Submit to Microsoft for analysis** flyout, select **Submit**.

        [![Choose whether to create a corresponding allow entry for the elements of the message in the Tenant Allow/Block List.](media/admin-submission-email-allow-page-2.png)](media/admin-submission-email-block-page-2.png#lightbox)
6. Select **Done**.

After a few moments, the associated allow entries appear on the **Domains & addresses**, **Spoofed senders**, **URLs**, or **Files** tabs on the **Tenant Allow/Block Lists** page at https://security.microsoft.com/tenantAllowBlockList.

Important

- Allow entries are added during mail flow based on the filters that determined the message was malicious. For example, if the sender email address and a URL in the message were determined to be bad, an allow entry is created for the sender (email address or domain) and the URL.
- If the sender email address is not found to be malicious by our filtering system, submitting the email message to Microsoft won't create an allow entry in the Tenant Allow/Block List.
- When an allowed domain or email address, spoofed sender, URL, or file (*entity*) is encountered again, all filters that are associated with the entity are skipped. For email messages, all other entities are still evaluated by the filtering system before making a decision.
- During mail flow, if messages from the allowed domain or email address pass other checks in the filtering stack, the messages are delivered. For example, if a message passes [email authentication checks](email-authentication-about), a message from an allowed sender email address are delivered.
- By default, allow entries for domains and email addresses are kept for 45 days after the filtering system determines that the entity is clean, and then the allow entry is removed. For all other values like 1 day, 7 days, 30 days, specific date the allow entry expire at the defined date. By default, allow entries for spoofed senders never expire.
- For messages that were incorrectly blocked by [domain or user impersonation protection](anti-phishing-policies-about#impersonation-settings-in-anti-phishing-policies-in-microsoft-defender-for-office-365), the allow entry for the domain or sender is not created in the Tenant Allow/Block List. Instead, the domain or sender is added to the **Trusted senders and domains** section in the [anti-phishing policy](anti-phishing-policies-mdo-configure#use-the-microsoft-defender-portal-to-modify-anti-phishing-policies) that detected the message.
- When you override the verdict in the spoof intelligence insight, the spoofed sender becomes a manual allow or block entry that only appears on the **Spoofed senders** on the **Tenant Allow/Block Lists** page at https://security.microsoft.com/tenantAllowBlockList?viewid=SpoofItem.
- If you allow at least 7 email addresses in the same domain in the Tenant Allow/Block List, submissions automatically roll up the email addresses into a domain allow entry. This action happens when submission is trying to add an email address allow for that domain.

### Report good email attachments to Microsoft

To report a good email attachment to Microsoft for analysis, perform the following steps:

1. In the Defender portal at https://security.microsoft.com, go to **Actions & submissions** &gt; **Submissions**. Or, to go directly to the **Submissions** page, use https://security.microsoft.com/reportsubmission.
2. On the **Submissions** page, select the **Email attachments** tab.
3. On the **Email attachments** tab, select ![](media/defender-portal-icon-create.png)**Submit to Microsoft for analysis**.
4. On the **Submit to Microsoft for analysis** flyout that opens, enter the following information:

    - **Select the submission type**: Verify the value **Email attachment** is selected.
    - **File**: Select **Browse files** to find and select the file to submit.
    - **Why are you submitting the message to Microsoft?**: Select one of the following options:

        - **It appears clean**: Select this value if you're unsure and you want a verdict from Microsoft, select **Submit**, and then go to Step 6.
        - **I've confirmed it's clean**: Select this value if you're sure that the item is clean, and then select **Next**.

    [![Submit a false positive (good) email attachment to Microsoft for analysis on the Submissions page in the Defender portal.](media/admin-submission-file-allow.png)](media/admin-submission-file-allow.png#lightbox)
5. On the second page of the **Submit to Microsoft for analysis** flyout that opens, select one of the following options:

    - Select **Submit**.
    - Select **Allow this file**: This option creates a allow entry for the file in the Tenant Allow/Block List. For more information about the Tenant Allow/Block List, see [Manage allows and blocks in the Tenant Allow/Block List](tenant-allow-block-list-about).

        After you select this option, the following settings are available:

        - **Remove allow entry after**: The default value is **45 days after last used date**, but you can select from the following values:

            - **1 day**
            - **7 days**
            - **30 days**
            - **Specific date**: The maximum value is 30 days from today.

            When **45 days after last used date** is selected, the last used date of the allow entry is updated when the malicious email attachment is encountered during mail flow. The allow entry is kept for 45 days after the filtering system determines that the email attachment is clean. For all other values like 1 day, 7 days, 30 days, specific date the allow entry expire at the defined date.
        - **Allow entry note (optional)**: Enter optional information about why you're allowing this item.

        When you're finished on the second page of the **Submit to Microsoft for analysis** flyout, select **Submit**.

    [![Choose whether to create a corresponding allow entry for the file in the Tenant Allow/Block List.](media/admin-submission-file-allow-page-2.png)](media/admin-submission-file-allow-page-2.png#lightbox)
6. Select **Done**.

After a few moments, the allow entry is available on the **Files** tab on the **Tenant Allow/Block List** page. For more information about the Tenant Allow/Block List, see [Manage allows and blocks in the Tenant Allow/Block List](tenant-allow-block-list-about).

Important

- By default, allow entries for files are kept for 45 days after the filtering system determines that the entity is clean, and then the allow entry is removed. For all other values like 1 day, 7 days, 30 days, specific date the allow entry expire at the defined date.
- When the file is encountered again during mail flow, [Safe Attachments](safe-attachments-about) detonation or file reputation checks and all other file-based filters are overridden. If the filtering system determines that all other entities in the email message are clean, the message are delivered.
- During selection, all file-based filters, including [Safe Attachments](safe-attachments-about) detonation or file reputation checks are overridden, allowing user access to the file.

### Report good URLs to Microsoft

For URLs reported as false positives, we allow subsequent messages that contain variations of the original URL. For example, you use the **Submissions** page to report the incorrectly blocked URL `www.contoso.com/abc`. If your organization later receives a message that contains the URL (for example, but not limited to: `www.contoso.com/abc`, `www.contoso.com/abc?id=1`, `www.contoso.com/abc/def/gty/uyt?id=5`, or `www.contoso.com/abc/whatever`), the message won't be blocked based on the URL. In other words, you don't need to report multiple variations of the same URL as good to Microsoft.

1. In the Defender portal at https://security.microsoft.com, go to **Actions & submissions** &gt; **Submissions**. Or, to go directly to the **Submissions** page, use https://security.microsoft.com/reportsubmission.
2. On the **Submissions** page, select the **URLs** tab
3. On the **URLs** tab, select ![](media/defender-portal-icon-create.png)**Submit to Microsoft for analysis**.
4. In the **Submit to Microsoft for analysis** flyout that opens, enter the following information:

    - **Select the submission type**: Verify the value **URL** is selected.
    - **URL**: Enter the full URL (for example, `https://www.fabrikam.com/marketing.html`), and then select it in the box that appears. You can also provide a top level domain (for example, `https://www.fabrikam.com/*`), and then select it in the box that appears. You can enter up to 50 URL at once.
    - **Why are you submitting this URL to Microsoft?**: Select one of the following options:

        - **It appears clean**: Select this value if you're unsure and you want a verdict from Microsoft, select **Submit**, and then go to Step 6.
        - **I've confirmed it's clean**: Select this value if you're sure that the item is clean, and then select **Next**.

            [![Submit a false positive (good) URL to Microsoft for analysis on the Submissions page in the Defender portal.](media/admin-submission-url-allow.png)](media/admin-submission-url-allow.png#lightbox)
5. On the second page of the **Submit to Microsoft for analysis** flyout that opens, select one of the following options:

    - Select **Submit**.
    - Select **Allow this URL**: This option creates an allow entry for the URL in the Tenant Allow/Block List. For more information about the Tenant Allow/Block List, see [Manage allows and blocks in the Tenant Allow/Block List](tenant-allow-block-list-about).

        After you select this option, the following settings are available:

        - **Remove allow entry after**: The default value is **45 days after last used date**, but you can select from the following values:

            - **1 day**
            - **7 days**
            - **30 days**
            - **Specific date**: The maximum value is 30 days from today.

            When **45 days after last used date** is selected, the last used date of the allow entry is updated when the malicious URL is encountered during mail flow. The allow entry is kept for 45 days after the filtering system determines that the URL is clean. For all other values like 1 day, 7 days, 30 days, specific date the allow entry expire at the defined date.
        - **Allow entry note (optional)**: Enter optional information about why you're allowing this item.

        When you're finished on the second page of the **Submit to Microsoft for analysis** flyout, select **Submit**.

    [![Choose whether to create a corresponding allow entry for the URL in the Tenant Allow/Block List.](media/admin-submission-url-allow-page-2.png)](media/admin-submission-url-allow-page-2.png#lightbox)
6. Select **Done**.

After a few moments, the allow entry is available on the **URL** tab on the **Tenant Allow/Block Lists** page at https://security.microsoft.com/tenantAllowBlockList?viewid=Url.

Note

- By default, allow entries for URLs are kept for 45 days after the filtering system determines that the entity is clean, and then the allow entry is removed. For all other values like 1 day, 7 days, 30 days, specific date the allow entry expire at the defined date.
- When the URL is encountered again during mail flow, [Safe Links](safe-links-about) detonation or URL reputation checks and all other URL-based filters are overridden. If the filtering system determines that all other entities in the email message are clean, the message are delivered.
- During selection, all URL-based filters, including [Safe Links](safe-links-about) detonation or URL reputation checks are overridden, allowing user access to content at the URL.

### Report Teams messages to Microsoft in Defender for Office 365 Plan 2

Tip

[Submission of Teams message to Microsoft](submissions-teams) is currently in Preview, isn't available in all organizations, and is subject to change.

In Microsoft 365 organizations that have Microsoft Defender for Office 365 Plan 2 (add-on licenses or included in subscriptions like Microsoft 365 E5), You can't submit Teams messages from the **Teams messages** tab on the **Submissions** page. The only way to submit a Teams message to Microsoft for analysis is to submit a user reported Teams message from the **User reported** tab as described in Submit user reported messages to Microsoft for analysis.

The entries on the **Teams messages** tab are the result of submitting user reported Teams message to Microsoft. For more information, see View converted admin submissions.

### View email admin submissions to Microsoft

In the Defender portal at https://security.microsoft.com, go to **Actions & submissions** &gt; **Submissions**. Or, to go directly to the **Submissions** page, use https://security.microsoft.com/reportsubmission.

On the **Submissions** page, verify that the **Emails** tab is selected.

On the **Emails** tab, you can quickly filter the view by selecting one of the available quick filters:

- **Pending**
- **Completed**

[![The quick filters available for admin submissions on the Emails tab of the Submissions page.](media/submissions-quick-filters.png)](media/submissions-quick-filters.png#lightbox)

You can sort the entries by clicking on an available column header. Select ![](media/defender-portal-icon-customize.png)**Customize columns** to change the columns that are shown. The default values are marked with an asterisk (^\*^):

- **Submission name**^\*^
- **Sender**^\*^
- **Recipient**
- **Submitted by**^\*^
- **Date submitted**^\*^
- **Reason for submitting**^\*^
- **Status**^\*^
- **Result**^\*^
- **Delivery/Block reason**
- **Submission ID**
- **Network Message ID**
- **Direction**
- **Sender IP**
- **Bulk compliant level (BCL)**
- **Destination**
- **Policy action**
- **Phish simulation**
- **Is dispute**: For more information, see Dispute the result for submissions to Microsoft.
- **Tags**^\*^: For more information about user tags, see [User tags](user-tags-about).
- **Action**

To group the entries, select ![](media/defender-portal-icon-group.png)**Group** and then select one of the following values:

- **Reason**
- **Status**
- **Result**
- **Dispute status**
- **Tags**

To ungroup the entries, select **None**.

To filter the entries, select ![](media/defender-portal-icon-filter.png)**Filter**. The following filters are available in the **Filter** flyout that opens:

- **Date submitted**: **Start date** and **End date** values.
- **Submission ID**: A GUID value that's assigned to every submission.
- **Network Message ID**
- **Sender**
- **Recipient**
- **Submission name**
- **Submitted by**
- **Reason for submitting**: Any of the following values:
    - **Not junk**
    - **Appears clean**
    - **Appears suspicious**
    - **Phish**
    - **Malware**
    - **Spam**.
- **Status**: **Pending** and **Completed**.
- **Tags**: **All** or select [user tags](user-tags-about) from the dropdown list.

When you're finished on the **Filter** flyout, select **Apply**. To clear the filters, select ![](media/defender-portal-icon-clear-filters.png)**Clear filters**.

Use ![](media/defender-portal-icon-download.png)**Export** to export the list of entries to a CSV file.

#### View email admin submission details

If you select an entry on the **Emails** tab of the **Submissions** page by clicking anywhere in the row other than the check box next to the first column, a details flyout opens.

At the top of the details flyout, the following message information is available:

- The title of the flyout is the message Subject value.
- Any user tags that are assigned to the recipients of the message (including the Priority account tag). For more information, see [User tags in Microsoft Defender for Office 365](user-tags-about)
- In Defender for Office 365, the actions that are available at the top of the flyout are described in the Actions for admin submissions in Defender for Office 365 section.

Tip

To see details about other submissions without leaving the details flyout, use ![](media/updownarrows.png)**Previous item** and **Next item** at the top of the flyout.

The next sections in the details flyout are related to email message submissions:

- **Result details** section:

    - **Result**: Contains the **Result** value for the submission. For example:

        - **Should not have been blocked**
        - **Allowed due to user overrides**
        - **Allowed due to a rule**
    - **Recommended steps for email submissions**: Contains links to related actions. For example:

        - **View Exchange mail flow rules (transport rules)**
        - **View this message in Explorer** (Threat Explorer or Real-time detections in Defender for Office 365 only)
        - **Search for similar messages in Explorer** (Threat Explorer or Real-time detections in Defender for Office 365 only)
    - If you disputed the verdict on the message, a box shows information about the dispute results:

        - The date and email address of the admin who disputed the message.
        - **View dispute details**: A read only copy of the **Dispute details** flyout that the admin filled out when they disputed the message.
        - **View original submission**: The original details flyout of the email message submission.

        [![Screenshot of the disputed results box for email messages.](media/submissions-dispute-info-in-details-flyout.png)](media/submissions-dispute-info-in-details-flyout.png#lightbox)
- **Submission details** section:

    - **Date submitted**
    - **Submission name**
    - **Submission type**: The value is **Email**.
    - **Reason for submitting**
    - **Submission ID**
    - **Submitted by**
    - **Submission status**
- **Allow details** section: Available only for email submissions where the **Result** value is **Allowed due to user overrides** or **Allowed to a rule**: Contains the **Name** (email address) and **Type** (**Sender**) values.

The rest of the details flyout contains the **Delivery details**, **Email details**, **URLs**, and **Attachments** sections that are part of the *Email summary panel*. For more information, see [The Email summary panel](mdo-email-entity-page#the-email-summary-panel).

When you're finished in the details flyout, select **Close**.

### View Teams admin submissions to Microsoft in Defender for Office 365 Plan 2

In the Defender portal at https://security.microsoft.com, go to the **Submissions** page at **Actions & submissions** &gt; **Submissions**. Or, to go directly to the **Submissions** page, use https://security.microsoft.com/reportsubmission.

On the **Submissions** page, select the **Teams messages** tab.

You can sort the entries by clicking on an available column header. Select ![](media/defender-portal-icon-customize.png)**Customize columns** to change the columns that are shown. The default values are marked with an asterisk (^\*^):

- **Submission name**^\*^
- **Sender**^\*^
- **Date submitted**^\*^
- **Reason for submitting**^\*^
- **Submitted by**
- **Status**^\*^
- **Result**^\*^
- **Recipient**
- **Submission ID**
- **Teams message ID**
- **Destination**
- **Phish simulation**
- **Tags**^\*^: For more information about user tags, see [User tags](user-tags-about).

To group the entries, select ![](media/defender-portal-icon-group.png)**Group** and then select one of the following values:

- **Reason**
- **Status**
- **Result**
- **Tags**

To ungroup the entries, select **None**.

To filter the entries, select ![](media/defender-portal-icon-filter.png)**Filter**. The following filters are available in the **Filter** flyout that opens:

- **Date submitted**: **Start date** and **End date**.
- **Submission ID**: A GUID value that's assigned to every submission.
- **Teams message ID**
- **Sender**
- **Recipient**
- **Teams message**
- **Submitted by**
- **Reason for submitting**: Any of the following values:
    - **Not junk**
    - **Appears clean**
    - **Appears suspicious**
    - **Phish**
    - **Malware**
- **Status**: **Pending** and **Completed**.
- **Tags**: **All** or select [user tags](user-tags-about) from the dropdown list.

When you're finished on the **Filter** flyout, select **Apply**. To clear the filters, select ![](media/defender-portal-icon-clear-filters.png)**Clear filters**.

Use ![](media/defender-portal-icon-download.png)**Export** to export the list of entries to a CSV file.

#### View Teams admin submission details

If you select an entry on the **Teams messages** tab of the **Submissions** page by clicking anywhere in the row other than the check box next to the first column, a details flyout opens.

At the top of the details flyout, the following message information is available:

- The title of the flyout is the subject or the first 100 characters of the Teams message.
- The current message verdict.
- The number of links in the message.
- ![](media/defender-portal-icon-view-alert.png)**View alert**. An alert is triggered when an admin submission is created or updated. Selecting this action takes you to the details of the alert.

Tip

To see details about other submissions without leaving the details flyout, use ![](media/updownarrows.png)**Previous item** and **Next item** at the top of the flyout.

The next sections in the details flyout are related to Teams submissions:

- **Submission results** section:

    - **Result**: Contains the **Result**value for the submission. For example:
        - **Should have been blocked**
        - **We did not receive the submission, please fix the problem and resubmit**
    - **Recommended steps for email submissions**: Contains links to related actions. For example:
        - **View Exchange mail flow rules (transport rules)**
- **Submission details** section:

    - **Date submitted**
    - **Submission name**
    - **Submission type**: The value is **Teams**
    - **Reason for submitting**
    - **Submission ID**
    - **Submitted by**
    - **Submission status**

The rest of the details flyout contains the **Message details**, **Sender**, **Participants**, **Channel details**, and **URLs** sections that are part of the *Teams message entity panel*. For more information, see [The Teams message entity panel in Microsoft Defender for Office 365](teams-message-entity-panel).

Tip

To remove users from Teams chats, see [Remove users from Teams chats in the Teams message entity panel](teams-message-entity-panel#remove-users-from-teams-chats-in-the-teams-message-entity-panel).

When you're finished in the details flyout, select **Close**.

### View email attachment admin submissions to Microsoft

In the Defender portal at https://security.microsoft.com, go to the **Submissions** page at **Actions & submissions** &gt; **Submissions**. Or, to go directly to the **Submissions** page, use https://security.microsoft.com/reportsubmission.

On the **Submissions** page, select the **Email attachments** tab.

On the **Email attachments** tab, you can quickly filter the view by selecting one of the available quick filters:

- **Pending**
- **Completed**

[![The quick filters available for admin submissions on the Email attachments tab of the Submissions page.](media/submissions-quick-filters.png)](media/submissions-quick-filters.png#lightbox)

You can sort the entries by clicking on an available column header. Select ![](media/defender-portal-icon-customize.png)**Customize columns** to change the columns that are shown. The default values are marked with an asterisk (^\*^):

- **Attachment filename**^\*^
- **Date submitted**^\*^
- **Reason for submitting**^\*^
- **Status**^\*^
- **Result**^\*^
- **Filter verdict**
- **Delivery/Block reason**
- **Submission ID**
- **Object ID**
- **Policy action**
- **Submitted by**
- **Tags**^\*^: For more information about user tags, see [User tags](user-tags-about).
- **Action**

To group the entries, select ![](media/defender-portal-icon-group.png)**Group** and then select one of the following values:

- **Reason**
- **Status**
- **Result**
- **Tags**

To ungroup the entries, select **None**.

To filter the entries, select ![](media/defender-portal-icon-filter.png)**Filter**. The following filters are available in the **Filter** flyout that opens:

- **Date submitted**: **Start date** and **End date**.
- **Submission ID**: A GUID value that's assigned to every submission.
- **Attachment filename**
- **Submitted by**
- **Reason for submitting**: Any of the following values:
    - **Not junk**
    - **Appears clean**
    - **Appears suspicious**
    - **Phish**
    - **Malware**
- **Status**: **Pending** and **Completed**.
- **Tags**: **All** or select [user tags](user-tags-about) from the dropdown list.

When you're finished on the **Filter** flyout, select **Apply**. To clear the filters, select ![](media/defender-portal-icon-clear-filters.png)**Clear filters**.

Use ![](media/defender-portal-icon-download.png)**Export** to export the list of entries to a CSV file.

#### View email attachment admin submission details

If you select an entry on the **Email attachments** tab of the **Submissions** page by clicking anywhere in the row other than the check box next to the first column, a details flyout opens.

At the top of the details flyout, the following message information is available:

- The title of the flyout is the filename of the attachment.
- The **Status** and **Result** values of the submission.
- ![](media/defender-portal-icon-view-alert.png)**View alert**. In Defender for Office 365, an alert is triggered when an admin submission is created or updated. Selecting this action takes you to the details of the alert.

Tip

To see details about other submissions without leaving the details flyout, use ![](media/updownarrows.png)**Previous item** and **Next item** at the top of the flyout.

The next sections in the details flyout are related to email attachment submissions:

- **Result details** section:

    - **Result**: Contains the **Result**value for the submission. For example:
        - **Should have been blocked**
        - **Should not have been blocked**
    - **Recommended steps for email submissions**: Contains links to related actions. For example:
        - **Block URL/file in Tenant Allow/Block List**
- **Submission details** section:

    - **Date submitted**
    - **Submission name**
    - **Submission type**: The value is **File**.
    - **Reason for submitting**
    - **Submission ID**
    - **Submitted by**
    - **Submission status**

When you're finished in the details flyout, select **Close**.

### View URL admin submissions to Microsoft

In the Defender portal at https://security.microsoft.com, go to the **Submissions** page at **Actions & submissions** &gt; **Submissions**. Or, to go directly to the **Submissions** page, use https://security.microsoft.com/reportsubmission.

On the **Submissions** page, select the **URLs** tab.

On the **URLs** tab, you can quickly filter the view by selecting one of the available quick filters:

- **Pending**
- **Completed**

[![The quick filters available for admin submissions on the URLs tab of the Submissions page.](media/submissions-quick-filters.png)](media/submissions-quick-filters.png#lightbox)

You can sort the entries by clicking on an available column header. Select ![](media/defender-portal-icon-customize.png)**Customize columns** to change the columns that are shown. The default values are marked with an asterisk (^\*^):

- **URL**^\*^
- **Date submitted**^\*^
- **Reason for submitting**^\*^
- **Status**^\*^
- **Result**^\*^
- **Filter verdict**
- **Delivery/Block reason**
- **Submission ID**
- **Object ID**
- **Policy action**
- **Submitted by**
- **Is dispute**: For more information, see Dispute the result for submissions to Microsoft.
- **Tags**^\*^: For more information about user tags, see [User tags](user-tags-about).
- **Action**

To group the entries, select ![](media/defender-portal-icon-group.png)**Group** and then select one of the following values:

- **Reason**
- **Status**
- **Result**
- **Dispute status**
- **Tags**

To ungroup the entries, select **None**.

To filter the entries, select ![](media/defender-portal-icon-filter.png)**Filter**. The following filters are available in the **Filter** flyout that opens:

- **Date submitted**: **Start date** and **End date**.
- **Submission ID**: A GUID value that's assigned to every submission.
- **URL**
- **Submitted by**
- **Reason for submitting**: Any of the following values:
    - **Not junk**
    - **Appears clean**
    - **Appears suspicious**
    - **Phish**
    - **Malware**
- **Status**: **Pending** and **Completed**.
- **Tags**: **All** or select [user tags](user-tags-about) from the dropdown list.

When you're finished on the **Filter** flyout, select **Apply**. To clear the filters, select ![](media/defender-portal-icon-clear-filters.png)**Clear filters**.

Use ![](media/defender-portal-icon-download.png)**Export** to export the list of entries to a CSV file.

#### View URL admin submission details

If you select an entry on the **URLs** tab of the **Submissions** page by clicking anywhere in the row other than the check box next to the first column, a details flyout opens.

At the top of the details flyout, the following message information is available:

- The title of the flyout is the domain of the URL.
- The **Status** and **Result** values of the submission.
- ![](media/defender-portal-icon-view-alert.png)**View alert**. In Defender for Office 365, an alert is triggered when an admin submission is created or updated. Selecting this action takes you to the details of the alert.

Tip

To see details about other submissions without leaving the details flyout, use ![](media/updownarrows.png)**Previous item** and **Next item** at the top of the flyout.

The remaining sections in the details flyout are related to URL submissions:

- **Result details** section:

    - **Result**: Contains the **Result** value for the submission. For example:

        - **Should have been blocked**
        - **Should not have been blocked**
    - **Recommended steps for email submissions**: Contains links to related actions. For example:

        - **Block URL/file in Tenant Allow/Block List**
    - If you disputed the verdict on the URL, a box shows information about the dispute results:

        - The date and email address of the admin who disputed the message.
        - **View dispute details**: A read only copy of the **Dispute details** flyout that the admin filled out when they disputed the message.
        - **View original submission**: The original details flyout of the URL submission.

        [![Screenshot of the disputed results box for URLs.](media/submissions-dispute-info-in-details-flyout.png)](media/submissions-dispute-info-in-details-flyout.png#lightbox)
- **Submission details** section:

    - **Date submitted**
    - **URL**
    - **Submission type**: The value is **URL**.
    - **Reason for submitting**
    - **Submission ID**
    - **Submitted by**
    - **Submission status**
- **Allows details** or **Block details** sections: Available only for URL submissions where the URL was blocked or allowed: Contains the **Name** (URL domain) and **Type** (**URL**) values.

When you're finished in the details flyout, select **Close**.

### Results from Microsoft

The analysis results of the reported item are shown in the details flyout that opens when you select an entry on the **Emails**, **Teams messages**, **Email attachments**, or **URLs** tab of the **Submissions** page:

- If there was a failure in the sender's email authentication at the time of delivery.
- Information about any policies or overrides that could have affected or overridden the message verdict from filtering system.
- Current detonation results to see if the URLs or files in the message were malicious or not.
- Feedback from graders.

For more information about how Microsoft processes submissions, see [How submissions are processed behind the scenes](https://techcommunity.microsoft.com/blog/microsoftdefenderforoffice365blog/how-your-submissions-to-defender-for-office-365-are-processed-behind-the-scenes/4231551).

If an override or policy configuration was found, the result should be available in several minutes. If there wasn't a problem in email authentication or delivery wasn't affected by an override or policy, the detonation and feedback from graders could take up to a day.

Note

In Defender for Office 365 Plan 2, agentic AI grading is available for admin and user reported phishing messages. The agentic grading system has multiple layers: a machine learning grader model, agentic grading, and human graders. If machine learning returns a verdict with high confidence, this verdict is shown for the submission result. If not, the message goes to agentic grading for additional analysis/response. After that, the message goes to a human grader for final review if required.

AI-powered Submissions Response provides generative AI explanations for admin and user reported email submissions to Microsoft. For more information, see [Submission result definitions](submissions-result-definitions).

### Dispute the result for submissions to Microsoft

When you disagree with the verdict of an email or URL you submitted to Microsoft, you can dispute the verdict for eligible items. *Disputing* the item is different from *resubmitting* the item:

- **Dispute**: Select ![](media/defender-portal-icon-create.png)**Dispute submission result**to dispute eligible items.
    - The original verdict and history are retained.
    - You can dispute an item only once.
- **Resubmit**: Select ![](media/defender-portal-icon-create.png)**Submit to Microsoft for analysis**to resubmit eligible items.
    - The analysis starts over with no previous verdict or history.
    - You can resubmit an item multiple times.

You can use the procedures in this section to dispute admin submitted items that meet **all** of the following criteria:

- The item was submitted from the **Emails** or **URLs** tabs of the **Submissions** page.
- The **Status** property value is **Completed**.
- The **Result** property is one of the following values:

    - **Threats found**
    - **No threats found**
    - **Spam**
    - **Bulk**
- The item wasn't previously disputed (filter by **Is dispute** &gt; **No**).

    Tip

    To dispute items on the **User submitted** tab, you first need to convert the user submission to an admin submission.

1. On the **Submissions** page in the Defender portal, go to the **Emails**, or **URLs** tabs:

    - **Emails** tab: https://security.microsoft.com/reportsubmission?viewid=email
    - **URLs** tab: https://security.microsoft.com/reportsubmission?viewid=url
2. On the tab, do one of the following steps:

    - Select one or more eligible items by selecting the check box next to the first column, and then select the ![](media/defender-portal-icon-create.png)**Dispute submission result** action that appears.

        [![Screenshot of an entry select on the URLs tab of the Submissions page with Dispute submission result emphasized.](media/submissions-dispute-from-main-tab.png)](media/submissions-dispute-from-main-tab.png#lightbox)
    - Select an eligible item by clicking anywhere in the row other than the check box next to the first column. In th details flyout that opens, select **Dispute submission result**.

        [![Screenshot of the details flyout of an admin submissions entry where you can select Dispute submission result.](media/submissions-dispute-from-details.png)](media/submissions-dispute-from-details.png#lightbox)
3. In the **Dispute details** flyout that opens, configure the following settings:

    - **Tell us what did not go well**: Select one or more of the following values:
        - **Result**
        - **Reason**
        - **Recommended steps**
    - **Additional information (optional)**: Enter an explanation that you think might be helpful.
    - **Upload as screenshot**: Select this option to upload a JPG or PNG image less than one MB.

    Important

    If you don't select **Result**, the item isn't sent to Microsoft for reevaluation. Instead, an entry is created on the **Emails** or **URLs** tab without resubmitting the item. Values other than **Result** are taken as feedback.

    When you're finished on the **Dispute details** flyout, select **Submit dispute**.

    [![Screenshot of the Dispute details flyout.](media/submissions-dispute-options-flyout.png)](media/submissions-dispute-options-flyout.png#lightbox)
4. On the **Dispute submitted** flyout, select **Done**.

    [![Screenshot of the Dispute submitted flyout.](media/submissions-dispute-submitted.png)](media/submissions-dispute-submitted.png#lightbox)

#### View disputed items

On the **Emails** or **URLs** tabs of the **Submissions** page, the following controls are available for disputed items:

- ![](media/defender-portal-icon-group.png)**Group** &gt; **Dispute status** groups entries on the page into the following categories:

    - **Not disputed**
    - **Dispute submission**
    - **Disputed**
- ![](media/defender-portal-icon-customize.png)**Customize columns** &gt; **Is dispute** adds the **Is dispute** column to the entries on the page.
- ![](media/defender-portal-icon-filter.png)**Filter** &gt; **Is dispute** &gt; **Yes** or **No** filters filters the entries on the page by whether the item was disputed.

The details flyout for the email message or URL submission contains information and links about the disputed item.

### Actions for admin submissions in Defender for Office 365

In organizations with Microsoft Defender for Office 365 (add-on licenses or included in subscriptions like Microsoft 365 E5 or Microsoft 365 Business Premium), the following actions are available for admin submissions in the details flyout that opens after you select an entry from the list by clicking anywhere in the row other than the check box:

- ![](media/defender-portal-icon-open.png)**Open email entity**: Available in the details flyout of entries on the **Emails** tab only. For more information, see [What's on the Email entity page](mdo-email-entity-page#whats-on-the-email-entity-page).
- ![](media/defender-portal-icon-take-actions.png)**Take actions**: Available in the details flyout of entries on the **Emails** tab only. This action starts the same Action wizard that's available on the Email entity page. For more information, see [Actions on the Email entity page](mdo-email-entity-page#actions-on-the-email-entity-page).
- ![](media/defender-portal-icon-view-alert.png)**View alert**. An alert is triggered when an admin submission is created or updated. Selecting this action takes you to the details of the alert.
- In the **Result details** section, the following links for [Threat Explorer](threat-explorer-real-time-detections-about) might also be available, depending on the status and result of the reported item:

    - **View this message in Explorer**: **Emails** tab only.
    - **Search for similar messages in Explorer**: **Emails** tab only.
    - **Search for URL or file**: **Email attachments** or **URL** tabs only.

## Admin options for user reported messages

For email messages, admins can see what users are reporting on the **User reported** tab on the **Submissions** page if the following statements are true:

- The [user reported settings](submissions-user-reported-messages-custom-mailbox) are turned on.
- **Email messages**: You're using supported methods for users to report messages:
    - The [built-in Report button in Outlook](submissions-outlook-report-messages#use-the-built-in-report-button-in-outlook).
    - [Supported non-Microsoft reporting tools](submissions-user-reported-messages-custom-mailbox#options-for-non-microsoft-reporting-tools)
- **Teams messages**: [User reporting settings for Teams messages](submissions-teams#user-reporting-settings-for-teams-messages) is turned on.

Note

- User-reported messages that are sent to Microsoft only or to Microsoft and the [reporting mailbox](submissions-user-reported-messages-custom-mailbox) appear on the **User reported** tab.
- User-reported messages that are sent only to the reporting mailbox appear on the **User reported** tab with the **Result** value **Not Submitted to Microsoft**. Admins should report these messages to Microsoft for analysis.

In organizations with Microsoft Defender for Office 365 Plan 1 or Plan 2 (add-on licenses or included in subscriptions like Microsoft 365 E5), admins can also see [user reported messages in Microsoft Teams](submissions-teams).

In the Microsoft Defender portal at https://security.microsoft.com, go to **Actions & submissions** &gt; **Submissions**. Or, to go directly to the **Submissions** page, use https://security.microsoft.com/reportsubmission.

On the **Submissions** page, select the **User reported** tab.

The **User reported** tab provides information and actions including viewing user reported messages, viewing user reported email message details, and admin actions for user reported messages.

### View user reported messages to Microsoft

On the **User reported** tab, you can quickly filter the view by selecting one of the available quick filters:

- **Threats**
- **Spam**
- **No threats**
- **Simulations**

[![Quick filters on the User reported tab on the Submissions page.](media/submissions-user-reported-quick-filters.png)](media/submissions-user-reported-quick-filters.png#lightbox)

You can sort the entries by clicking on an available column header. Select ![](media/defender-portal-icon-customize.png)**Customize columns** to change the columns that are shown. The default values are marked with an asterisk (^\*^):

- **Name and type**^\*^
- **Reported by**^\*^
- **Date reported**^\*^
- **Sender**^\*^
- **Reported reason**^\*^
- **Result**^\*^: Contains the following information for reported messages based on the [user reported settings](submissions-user-reported-messages-custom-mailbox):
    - **Send reported items to** &gt; **Microsoft and my reporting mailbox** or **Microsoft only**: Values derived from the following analysis:
        - **Policy hits**: Information about any policies or overrides that may have allowed or blocked the incoming messages, including overrides to our filtering verdicts. The result should be available within several minutes. Otherwise, detonation and feedback from graders could take up to one day.
        - **Payload reputation/detonation**: Up-to-date examination of any URLs and files in the message.
        - **Grader analysis**: Review done by human graders in order to confirm whether or not messages are malicious.
    - **Send reported items to** &gt; **My reporting mailbox only**: The value is always **Not submitted to Microsoft**, because the messages weren't analyzed by Microsoft.
- **Message reported ID**
- **Network Message ID**
- **Teams message ID**
- **Sender IP**
- **Reported from**
- **Phish simulation**
- **Converted to admin submission**
- **Marked as**^\*^
- **Marked by**^\*^
- **Date marked**
- **Tags**^\*^: For more information about user tags, see [User tags](user-tags-about).

To group the entries, select ![](media/defender-portal-icon-group.png)**Group** and then select one of the following values:

- **Sender**
- **Reported by**
- **Result**
- **Reported from**
- **Converted to admin submission**
- **Tags**

To ungroup the entries, select **None**.

To filter the entries, select ![](media/defender-portal-icon-filter.png)**Filter**. The following filters are available in the **Filter** flyout that opens:

- **Date reported**: **Start date** and **End date**.
- **Reported by**
- **Name**
- **Message reported ID**
- **Network message ID**
- **Teams message ID**
- **Sender**
- **Reported reason**: The values **No threats**, **Phish**, and **Spam**.
- **Reported from**: The values **Microsoft** and **Third party**.
- **Phish simulation**: The values **Yes** and **No**.
- **Converted to admin submission**: The values **Yes** and **No**.
- **Submission type**: The available values are:
    - **Email**
    - **Teams message** (Defender for Office 365 Plan 2 only; currently in Preview).
- **Tags**: **All** or select one or more user tags (including Priority account) that are assigned to users. For more information about user tags, see [User tags in Microsoft Defender for Office 365](user-tags-about).

When you're finished on the **Filter** flyout, select **Apply**. To clear the filters, select ![](media/defender-portal-icon-clear-filters.png)**Clear filters**.

Use ![](media/defender-portal-icon-download.png)**Export** to export the list of entries to a CSV file.

For more information about the actions that are available for messages on the **User reported** tab, see Admin actions for user reported messages.

### View user reported email message details

If you select an email-related entry on the **User reported** tab of the **Submissions** page by clicking anywhere in the row other than the check box next to the first column, a details flyout opens.

At the top of the details flyout, the following message information is available:

- The title of the flyout is the message Subject value.
- Any user tags that are assigned to the recipients of the message (including the Priority account tag). For more information, see [User tags in Microsoft Defender for Office 365](user-tags-about)
- The actions that are available at the top of the flyout are described in the Admin actions for user reported messages section.

Tip

To see details about other submissions without leaving the details flyout, use ![](media/updownarrows.png)**Previous item** and **Next item** at the top of the flyout.

The next sections in the details flyout are related to user reported submissions:

- **Result details** section:

    - **Result**: Contains the **Result**value for the submission. For example:
        - **Should not have been blocked**
        - **Allowed due to user overrides**
        - **Allowed due to a rule**
    - **Recommended steps for email submissions**: Contains links to related actions. For example:
        - **View Exchange mail flow rules (transport rules)**
        - **View this message in Explorer** (Threat Explorer or Real-time detections in Defender for Office 365 only)
        - **Search for similar messages in Explorer** (Threat Explorer or Real-time detections in Defender for Office 365 only)
- **Reported message details** section:

    - **Date submitted**
    - **Submission name**
    - **Reported reason**.
    - **Message reported ID**
    - **Reported by**
    - **Phish simulation**: The value is **Yes** or **No**.
    - **Converted to admin submission**: The value is **Yes** or **No**. For more information, see View converted admin submissions.

The rest of the details flyout contains the **Delivery details**, **Email details**, **URLs**, and **Attachments** sections that are part of the *Email summary panel*. For more information, see [The Email summary panel](mdo-email-entity-page#the-email-summary-panel).

Tip

If the **Result** value is **Phish simulation**, the details flyout might contain the following information only:

- **Result details** section
- **Reported message details** section
- **Email details**section with the following values:
    - **Network Message ID**
    - **Sender**
    - **Sent date**

When you're finished in the details flyout, select **Close**.

### View user reported Teams message details in Defender for Office 365 Plan 2

In Microsoft 365 organizations that have Microsoft Defender for Office 365 Plan 2 (add-on licenses or included in subscriptions like Microsoft 365 E5), user reported Teams messages are available on the **User reported** tab of the **Submissions** page. It's easy to find them if you filter the results by the **Message type** value **Teams message**.

If you select a Teams message entry on the **User reported** tab by clicking anywhere in the row other than the check box next to the first column, a details flyout opens.

At the top of the details flyout, the following message information is available:

- The title of the flyout is the subject or the first 100 characters of the Teams message.
- The current message verdict.
- The number of links in the message.
- The available actions are described in the Admin actions for user reported messages section.

Tip

To see details about other submissions without leaving the details flyout, use ![](media/updownarrows.png)**Previous item** and **Next item** at the top of the flyout.

The next sections in the details flyout are related to user reported Teams submissions:

- **Submission results** section:

    - **Result**: Contains the **Result**value for the submission. For example:
        - **Should not have been blocked**
        - **Not submitted to Microsoft**
    - **Recommended steps for email submissions**: Contains links to related actions. For example:
        - **View Exchange mail flow rules (transport rules)**
- **Reported message details** section:

    - **Date reported**
    - **Submission name**
    - **Reported reason**.
    - **Message reported ID**
    - **Reported by**
    - **Phish simulation**: The value is **Yes** or **No**.
    - **Converted to admin submission**: The value is **Yes** or **No**. For more information, see View converted admin submissions.

The rest of the details flyout contains the **Message details**, **Sender**, **Participants**, **Channel details**, and **URLs** sections that are part of the *Teams message entity panel*. For more information, see [The Teams message entity panel in Microsoft Defender for Office 365](teams-message-entity-panel).

Tip

To remove users from Teams chats, see [Remove users from Teams chats in the Teams message entity panel](teams-message-entity-panel#remove-users-from-teams-chats-in-the-teams-message-entity-panel).

If the **Result** value is **Phish simulation**, the details flyout might contain the following information only:

- **Result details** section
- **Reported message details** section
- **Email details**section with the following values:
    - **Network Message ID**
    - **Sender**
    - **Sent date**

When you're finished in the details flyout, select **Close**.

### Admin actions for user reported messages

On the **User reported** tab, actions for user reported messages are available on the tab itself or in the details flyout of a selected entry:

- Select the message from the list by selecting the check box next to the first column. The following actions are available on the **User reported** tab:

    - ![](media/defender-portal-icon-submit-user-reported-message.png)**Submit to Microsoft for analysis**
    - ![](media/defender-portal-icon-mark-and-notify.png)**Mark as and notify**
    - **Trigger investigation** (Defender for Office 365 Plan 2 only)
- Select the message from the list by clicking anywhere in the row other than the check box. The following actions are available in the details flyout that opens^\*^:

    - ![](media/defender-portal-icon-submit-user-reported-message.png)**Submit to Microsoft for analysis**
    - ![](media/defender-portal-icon-mark-and-notify.png)**Mark as and notify**
    - ![](media/defender-portal-icon-view-submission.png)**View the converted admin submission**
    - Actions in Microsoft Defender for Office 365 only:
        - ![](media/defender-portal-icon-open.png)**Open email entity**
        - ![](media/defender-portal-icon-take-actions.png)**Take actions**
        - ![](media/defender-portal-icon-view-alert.png)**View alert**

    Tip

    To see details or take action on other user reported messages without leaving the details flyout, use ![](media/updownarrows.png)**Previous item** and **Next item** at the top of the flyout.

^\*^ Depending on the nature and status of the message, some actions might not be available, are available directly at the top of the flyout, or are available under ![](media/defender-portal-icon-more-actions.png)**More actions** at the top of the flyout.

These actions are described in the following subsections.

Note

After a user reports a suspicious message, the user or admins can't undo the reporting of the message, regardless of where the reported message goes (to the reporting mailbox, to Microsoft, or both). The user can recover the reported message from their Deleted Items or Junk Email folders.

#### Submit user reported messages to Microsoft for analysis

After you select the message on the **User reported** tab, use either of the following methods to submit the message to Microsoft:

- **On the User reported tab**: Select ![](media/defender-portal-icon-create.png)**Submit to Microsoft for analysis**.
- **In the details flyout of the selected message**: Select **Submit to Microsoft for analysis** or ![](media/defender-portal-icon-more-actions.png)**More options** &gt; **Submit to Microsoft for analysis** at the top of the flyout.

In the **Submit to Microsoft for analysis** flyout that opens, do the following steps based on whether the message an email message or a Teams message:

- **Email messages**:

    - **Why are you submitting this message to Microsoft?**: Select one of the following values:
        - **It appears clean** or **It appears suspicious**: Select one of these values if you're unsure and you want a verdict from Microsoft.

            Select **Submit**, and then select **Done**.
        - **I've confirmed it's clean**: Select this value if you're sure that the item is clean, and then select **Next**.

            On the next page of the flyout, select one of the following options:

            - Select **Submit**, and then select **Done**.
            - Select **Allow this message**: This option creates an allow entry for the elements of the message in the Tenant Allow/Block List. For more information about the Tenant Allow/Block List, see [Manage allows and blocks in the Tenant Allow/Block List](tenant-allow-block-list-about).

            After you select this option, the following settings are available:

            - **Remove allow entry after**: The default value is **45 days after last used date**, but you can select from the following values:
                - **1 day**
                - **7 days**
                - **30 days**
                - **Specific date**: The maximum value is 30 days from today.

            When **45 days after last used date** is selected, the last used date of the allow entry is updated when the malicious email message is encountered during mail flow. The allow entry is kept for 45 days after the filtering system determines that the email message is clean. For all other values like 1 day, 7 days, 30 days, specific date the allow entry expire at the defined date.

            - **Allow entry note (optional)**: Enter optional information about why you're allowing this item. For spoofed senders, any value you enter here isn't shown in the allow entry on the **Spoofed senders** tab on the **Tenant Allow/Block Lists** page.

            When you're finished in the flyout, select **Submit**, and then select **Done**.
        - **I've confirmed it's a threat**: Select this value if you're sure that the item is malicious, and then select one of the following values in the **Choose a category** section that appears:

            - **Phish**
            - **Malware**
            - **Spam**

            Select **Next**.

            On the next page of the flyout, select one of the following options:

            - Select **Submit**, and then select **Done**.
            - Select **Block all emails from this sender or domain**: This option creates a block entry for the sender domain or email address in the Tenant Allow/Block List. For more information about the Tenant Allow/Block List, see [Manage allows and blocks in the Tenant Allow/Block List](tenant-allow-block-list-about).

            After you select this option, the following settings are available:

            - By default, **Sender** is selected but you can select **Domain** instead.
            - **Remove block entry after**: The default value is **30 days**, but you can select from the following values:
                - **1 day**
                - **7 days**
                - **30 days**
                - **Never expire**
                - **Specific date**: The maximum value is 30 days from today.
            - **Block entry note (optional)**: Enter optional information about why you're blocking this item.

            When you're finished in the flyout, select **Submit**, and then select **Done**.

    [![The available actions in the Submit to Microsoft for analysis dropdown list.](media/admin-submission-user-reported-submit-button-options.png)](media/admin-submission-user-reported-submit-button-options.png#lightbox)
- **Teams messages**: Select one of the following values:

    - **I've confirmed its clean**
    - **It appears clean**
    - **It appears suspicious**

    After you select one of these values, select **Submit**, and then select **Done**.

    - **I've confirmed it's a threat**: Select this value if you're sure that the item is malicious, and then select one of the following values in the **Choose a category** section that appears:
    - **Phish**
    - **Malware**

        Select **Submit**, and then select **Done**.

After you submit a user reported message to Microsoft from the **User reported** tab, the value of **Converted to admin submission** turns from **No** to **Yes**, and a corresponding admin submission entry is created on the appropriate tab on the **Submissions** page (for example, the **Emails** tab).

#### Trigger an investigation in Defender for Office 365 Plan 2

To trigger an automated investigation for a user reported message, use the following action:

- **On the User reported tab**, select **Trigger investigation** in the dropdown list on ![](media/defender-portal-icon-create.png)**Submit to Microsoft for analysis**.

[![The Trigger investigation action in the Submit to Microsoft for analysis dropdown list.](media/admin-submission-user-reported-submit-button-options.png)](media/admin-submission-user-reported-submit-button-options.png#lightbox)

For more information, see [A security administrator triggers an investigation from Threat Explorer](air-examples#example-a-security-administrator-triggers-an-investigation-from-threat-explorer).

#### Notify users about admin submitted messages to Microsoft

After an admin submits a user reported message to Microsoft from the **User reported** tab, admins can use the ![](media/defender-portal-icon-mark-and-notify.png)**Mark as and notify** action to mark the message with a verdict and send a templated notification message to the user who reported the message.

When automatic notifications use the default notification template, users receive the notification in their preferred language based on their Outlook language settings. Custom notification templates configured by admins aren't affected.

- Available verdicts for email messages:

    - **No threats found**
    - **Phishing**
    - **Spam**
- Available verdicts for Teams messages:

    - **No threats found**
    - **Phishing**

For more information, see [Notify users from within the portal](submissions-admin-review-user-reported-messages#notify-users-from-within-the-portal).

#### View converted admin submissions

After an admin submits a user reported message to Microsoft from the **User reported** tab, the value of **Converted to admin submission** is **Yes**.

If you select one of these messages by clicking anywhere in the row other than the check box next to the name, the details flyout contains ![](media/defender-portal-icon-more-actions.png)**More actions** &gt; ![](media/defender-portal-icon-view-submission.png)**View the converted admin submission**.

This action takes you to the corresponding admin submission entry on the appropriate tab (for example, the **Emails** tab).

#### Actions for user reported messages in Defender for Office 365

In organizations with Microsoft Defender for Office 365 (add-on licenses or included in subscriptions like Microsoft 365 E5 or Microsoft 365 Business Premium), the following actions might also be available in the details flyout of a user reported message on the **User reported** tab:

- ![](media/defender-portal-icon-open.png)**Open email entity** (email messages only): For more information, see [What's on the Email entity page](mdo-email-entity-page#whats-on-the-email-entity-page).
- ![](media/defender-portal-icon-take-actions.png)**Take actions** (email messages only): This action starts the same Action wizard that's available on the Email entity page. For more information, see [Actions on the Email entity page](mdo-email-entity-page#actions-on-the-email-entity-page).
- ![](media/defender-portal-icon-view-alert.png)**View alert**. An alert is triggered when an admin submission is created or updated. Selecting this action takes you to the details of the alert.