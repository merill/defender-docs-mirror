---
layout: Conceptual
title: Manage quarantined messages and files as an admin - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/quarantine-admin-manage-messages-files
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
ms.assetid: 065cc2cf-2f3a-47fd-a434-2a20b8f51d0c
ms.collection:
- m365-security
- tier1
ms.custom:
- msecd-doc-authoring-1016
- seo-marvel-apr2020
- sfi-ga-nochange
- sfi-image-nochange
description: Admins can learn how to view and manage quarantined messages for all users in Microsoft 365 organizations with cloud mailboxes. Admins in organizations with Microsoft Defender for Office 365 can also manage quarantined files in SharePoint, OneDrive, and Microsoft Teams.
ms.service: defender-office-365
ms.date: 2026-08-31T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 63f8cdbb-7429-da44-41cb-c85bb9f27e99
document_version_independent_id: 63f8cdbb-7429-da44-41cb-c85bb9f27e99
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/quarantine-admin-manage-messages-files.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: quarantine-admin-manage-messages-files
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/quarantine-admin-manage-messages-files.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
platformId: 85cbf2a3-474a-771b-1f87-d273d68c2782
---

# Manage quarantined messages and files as an admin - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

In all organizations with cloud mailboxes, quarantine holds potentially dangerous or unwanted messages detected by [the built-in security features for all cloud mailboxes](eop-about). Admins can view, release, and delete all types of quarantined messages and files for all users.

Admins in Microsoft 365 organizations with Defender for Office 365 (included or in an add-on subscription) can also manage files quarantined by [Safe Attachments for SharePoint, OneDrive, and Microsoft Teams](safe-attachments-for-spo-odfb-teams-about) and Microsoft Teams messages [quarantined by zero-hour auto purge (ZAP)](zero-hour-auto-purge#zero-hour-auto-purge-zap-in-microsoft-teams).

Users can manage most quarantined email messages based on the *quarantine policy* for [supported email protection features](quarantine-policies#step-2-assign-a-quarantine-policy-to-supported-features). In particular, admins can use quarantine policies to configure:

- Whether recipients are notified about quarantined messages.
- The actions that recipients can take on their quarantined messages.

For more information about quarantine policies, see [Anatomy of a quarantine policy](quarantine-policies#anatomy-of-a-quarantine-policy).

Admins and users (depending on the [user reported settings](submissions-user-reported-messages-custom-mailbox) for the organization) can report false positives to Microsoft from quarantine.

You view and manage quarantined messages in the Microsoft Defender portal or in [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

Watch this short video to learn how to manage quarantined messages as an admin.

Tip

As a companion to this article, see our [Microsoft Defender for Office 365 setup guide](https://setup.cloud.microsoft/defender/office-365-setup-guide) to review best practices and to protect against email, link, and collaboration threats. Features include Safe Links, Safe Attachments, and more. For a customized experience based on your environment, you can access the [Microsoft Defender for Office 365 automated setup guide](https://admin.microsoft.com/Adminportal/Home?Q=ADG#/modernonboarding/office365advancedthreatprotectionadvisor) in the Microsoft 365 admin center.

## What do you need to know before you begin?

Before you begin, review the following portal access, permissions, and retention information:

- To open the Microsoft Defender portal, go to https://security.microsoft.com. To go directly to the **Quarantine** page, use https://security.microsoft.com/quarantine.
- To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- You need to be assigned permissions before you can do the procedures in this article. You have the following options:

    - [Microsoft Defender XDR Unified role based access control (RBAC)](/en-us/defender-xdr/manage-rbac) (If **Email & collaboration** &gt; **Defender for Office 365** permissions is ![](media/scc-toggle-on.png)**Active**. Affects the Defender portal only, not PowerShell):
        - *Take action on quarantined messages for all users*: **Security operations / Security data / Email & collaboration quarantine (manage)**.
        - *Read-only access to quarantined messages for all users*: **Security operations / Security data / Security data basics (read)**.
        - *Preview and download quarantined messages for all users*: **Security operations/Raw data (email & collaboration)/Email and Collaboration content: Quarantine Emails (read)**.
    - [Email & collaboration permissions in the Microsoft Defender portal](mdo-portal-permissions):
        - *Take action on quarantined messages for all users*: Membership in the **Quarantine Administrator**, **Security Administrator**, or **Organization Management**role groups.
            - *Submit messages from quarantine to Microsoft*: Membership in the **Security Administrator** role groups.
            - *Use **Block sender** to add senders to your own Blocked Senders list*: Admins see **Block sender** only if they filter the quarantine results by **Recipient** &gt; **Only me** instead of the default value **All users**. Assigning any permission that gives admin access to quarantine (for example, **Security Reader** or **Global Reader**) gives access to **Block sender** in quarantine if the user filters the quarantine results by **Recipient** &gt; **Only me**.
        - *Read-only access to quarantined messages for all users*: Membership in the **Global Reader**, **Security Reader**, or **Security Operator** role groups.
        - *Preview and download quarantined messages for all users*: Membership in the **Global Reader**, **Security Reader**, or **Security Operator** role groups.
    - [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): Membership in these roles gives users the required permissions *and*permissions for other features in Microsoft 365:
        - *Take action on quarantined messages for all users*: Membership in the **Security Administrator** or **Global Administrator**^\*^ roles.

            Important

            ^\*^ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.

            - *Submit messages from quarantine to Microsoft*: Membership in the **Security Administrator** role.
            - *Use **Block sender** to add senders to your own Blocked Senders list*: Admins see **Block sender** only if they filter the quarantine results by **Recipient** &gt; **Only me** instead of the default value **All users**. Assigning any permission that gives admin access to quarantine (for example, **Security Reader** or **Global Reader**) gives access to **Block sender** in quarantine if the user filters the quarantine results by **Recipient** &gt; **Only me**.
        - *Read-only access to quarantined messages for all users*: Membership in the **Global Reader**, **Security Reader**, or **Security Operator** roles.
        - *Preview and download quarantined messages for all users*: Membership in the **Global Reader**, **Security Reader**, or **Security Operator** roles.

    Note

    Currently, roles assigned through Azure Privileged Identity Management aren't supported in quarantine. For more information about PIM, see [Privileged Identity Management (PIM) and why to use it with Microsoft Defender for Office 365](/en-us/defender-office-365/pim-in-mdo-configure).

    The ability to manage quarantined messages using [Exchange Online permissions](/en-us/exchange/permissions-exo/permissions-exo) ended in February 2023 per MC447339.

    Guest admins from other organizations can't manage quarantined messages. The admin needs to be in the same organization as the recipients.
- Quarantined messages and files are retained for a default period of time based on why they were quarantined. After the retention period expires, the messages are automatically deleted and aren't recoverable. For more information, see [Quarantine retention](quarantine-about#quarantine-retention).
- For information about the order of precedence for user allows and blocks and organization allows and blocks, see [When user and organization settings conflict](how-policies-and-protections-are-combined#when-user-and-organization-settings-conflict).
- All actions taken by admins or users on quarantined messages are audited. For more information about audited quarantine events, see [Quarantine schema in the Office 365 Management API](/en-us/office/office-365-management-api/office-365-management-activity-api-schema#quarantine-schema).

## Use the Microsoft Defender portal to manage quarantined email messages

### View quarantined email

In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Review** &gt; **Quarantine** &gt; **Email** tab. Or, to go directly to the **Email** tab on the **Quarantine** page, use https://security.microsoft.com/quarantine?viewid=Email.

By default, only the first 100 entries are shown until you scroll down to the bottom of the list, which loads more results.

Tip

For answers to frequently asked questions about quarantined messages, select ![](media/defender-portal-icon-refresh.png)**Resolution to common issues** at the top of the page. Or, see the following articles:

- [Quarantine](quarantine-about)
- [Quarantine policies](quarantine-policies)
- [Use quarantine notifications to release and report quarantined messages](quarantine-quarantine-notifications)

On the **Email** tab, you can decrease the vertical spacing in the list by clicking ![](media/defender-portal-icon-standard.png)**Change list spacing to compact or normal** and then selecting ![](media/defender-portal-icon-compact.png)**Compact list**.

You can sort the entries by clicking on an available column header. Select ![](media/defender-portal-icon-customize.png)**Customize columns** to change the columns that are shown. The default values are marked with an asterisk (^\*^):

- **Time received**^\*^
- **Subject**^\*^
- **Sender**^\*^
- **Quarantine reason**^\*^ (see the possible values in the ![](media/defender-portal-icon-filter.png)**Filter** description.)
- **Release status**^\*^ (see the possible values in the ![](media/defender-portal-icon-filter.png)**Filter** description.)
- **Policy type**^\*^ (see the possible values in the ![](media/defender-portal-icon-filter.png)**Filter** description.)
- **Expires**^\*^
- **Recipient**: The recipient email address always resolves to the primary email address, even if the message was sent to a [proxy address](/en-us/exchange/recipients-in-exchange-online/manage-user-mailboxes/add-or-remove-email-addresses).
- **Sender address override reason**^\*^: One of the following values:

    - **None**
    - **Message sender is blocked by recipient settings**
    - **Message sender is blocked by administrator settings**

    Tip

    If a sender is blocked and **Don't show blocked senders** is selected (default), messages from those senders are shown on the **Quarantine** page and are included in quarantine notifications when the **Sender address override reason** value is **None**. This behavior occurs because the messages were blocked due to reasons other than sender address overrides. For more information, see [Limits for junk email settings](configure-junk-email-settings-on-exo-mailboxes#limits-for-junk-email-settings).
- **Released by**^\*^
- **Message ID**
- **Policy name**
- **Message size**
- **Mail direction**
- **Recipient tag**

To filter the entries, select ![](media/defender-portal-icon-filter.png)**Filter**. The following filters are available in the **Filters** flyout that opens:

- **Message ID**: The globally unique identifier of the message.

    For example, you used [message trace](message-trace-defender-portal) to look for a message, and you determine that the message was quarantined instead of delivered. Be sure to include the full message ID value, which might include angle brackets (&lt;&gt;). For example: `<79239079-d95a-483a-aacf-e954f592a0f6@XYZPR00BM0200.contoso.com>`.
- **Sender address**
- **Recipient address**
- **Subject**
- **Time received**: Select one of the following values:

    - **Last 24 hours**
    - **Last 7 days** (default)
    - **Last 14 days**
    - **Last 30 days**
    - **Custom**: Enter a **Start time** and **End time** (date).
- **Expires**: Filter messages by when they expire from quarantine. Select one of the following values:

    - **Today**
    - **Next 2 days**
    - **Next 7 days**
    - **Custom**: Enter a **Start time** and **End time** (date).
- **Recipient tag**: Currently, the only selectable [user tag](user-tags-about) is Priority account.
- **Quarantine reason**: Select one or more of the following values:

    - **Transport rule** (mail flow rule)
    - **Bulk**
    - **Spam**
    - **Data loss prevention**
    - **Malware**: Anti-malware policies for email in Microsoft 365 or Safe Attachments policies in Defender for Office 365. The **Policy Type** value indicates which feature was used.
    - **Admin action - File type block**: Messages blocked as malware by the common attachments filter in anti-malware policies. For more information, see [Anti-malware policies](anti-malware-protection-about#anti-malware-policies).
    - **Phishing**: The spam filter verdict was **Phishing** or anti-phishing protection quarantined the message ([spoof settings](anti-phishing-policies-about#spoof-settings) or [impersonation protection](anti-phishing-policies-about#impersonation-settings-in-anti-phishing-policies-in-microsoft-defender-for-office-365)).
    - **High confidence phishing**
    - **Password protected item**: Safe Attachments quarantined the message because it contains an encrypted (password-protected) attachment that can't be scanned. For more information, see [Encrypted (password-protected) attachments in Safe Attachments policies](safe-attachments-about#encrypted-password-protected-attachments-in-safe-attachments-policies).
- **Recipient**: Select one of the following values:

    - **All users** (the default value, even if it doesn't appear selected)
    - **Only me**: Show messages sent to the currently signed in recipient only. This value is required for admins to see the Allow sender and Block sender actions.
- **Blocked sender**: One of the following values:

    - **Don't show blocked senders** (default)
    - **Show all senders**

    Tip

    If a sender is blocked and **Don't show blocked senders** is selected, messages from those senders are shown on the **Quarantine** page and are included in quarantine notifications when the **Sender address override reason** value is **None**. This behavior occurs because the messages were blocked due to reasons other than sender address overrides.
- **Release status**: Select one or more of the following values

    - **Needs review**
    - **Denied**
    - **Release requested**
    - **Released**
- **Policy type**: Filter messages by what type of threat policy quarantined the message. Select one or more of the following values:

    - **Anti-malware policy**
    - **Safe Attachments policy**
    - **Anti-phishing policy**
    - **Anti-spam policy**
    - **Transport rule** (mail flow rule)
    - **Data loss prevention rule**

    The **Policy type** and **Quarantine reason** values are interrelated. For example, **Bulk** is always associated with an **Anti-spam policy**, never with an **Anti-malware policy**.

When you're finished on the **Filters** flyout, select **Apply**. To clear the filters, select ![](media/defender-portal-icon-clear-filters.png)**Clear filters**.

Tip

Filters are cached. The filters from the last sessions are selected by default the next time you open the **Quarantine** page. This behavior helps with triage operations.

Use the ![](media/defender-portal-icon-search.png)**Search** box and a corresponding value to find specific messages. Wildcards aren't supported. You can search by the following values:

- Sender email address
- Subject. Use the entire subject of the message. The search isn't case-sensitive.

After you enter the search criteria, press Enter to filter the results.

Note

The **Search** box searches for quarantined items in the current view (which is limited to 100 items), not all quarantined items. To search all quarantined items, use ![](media/defender-portal-icon-filter.png)**Filter** and the resulting **Filters** flyout.

After you find a specific quarantined message, select the message to view details about it and to take action on it (for example, view, release, download, or delete the message).

Tip

On mobile devices, the previously described controls are available under ![](media/defender-portal-icon-more-actions.png)**More**.

[![Screenshot of selecting a quarantined message and then selecting More on a mobile device.](media/quarantine-message-main-page-mobile-actions.png)](media/quarantine-message-main-page-mobile-actions.png#lightbox)

### View quarantined email details

Use the following steps to open the details flyout for a quarantined email message.

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Review** &gt; **Quarantine** &gt; **Email** tab. Or, to go directly to the **Email** tab on the **Quarantine** page, use https://security.microsoft.com/quarantine?viewid=Email.
2. On the **Email** tab, select the quarantined message by clicking anywhere in the row other than the check box.

In the details flyout that opens, the following information is available:

Tip

The actions that are available at the top of the flyout are described in Take action on quarantined email.

To see details about other quarantined messages without leaving the details flyout, use ![](media/updownarrows.png)**Previous item** and **Next item** at the top of the flyout.

- **Quarantine details**section:
    - **Received**: The date/time when the message was received.
    - **Expires**: The date/time when the message is automatically and permanently deleted from quarantine.
    - **Subject**
    - **Quarantine reason**: Shows if a message was identified as **Spam**, **Bulk**, **Phish**, matched a mail flow rule (**Transport rule**), or was identified as containing **Malware**.
    - **Policy type**
    - **Policy name**
    - **Recipient**
        - Recipient email addresses always resolve to the primary email address, even if the message was sent to a [proxy address](/en-us/exchange/recipients-in-exchange-online/manage-user-mailboxes/add-or-remove-email-addresses).
        - If the original message was sent to multiple recipients, select ![](media/defender-portal-icon-more-actions.png)**More options** &gt; ![](media/defender-portal-icon-preview-message.png)**Preview message** or ![](media/defender-portal-icon-more-actions.png)**More options** &gt; ![](media/defender-portal-icon-view-message-headers.png)**View message headers** to see the complete list of recipients.
    - **Not yet released to**, **Released to**, and/or **Released by**: Depending on the state of the message, one or more of the following values might be available:
        - **Not yet released to**: Email addresses of recipients who didn't receive the released message.
        - **Released to**: Email addresses of recipients the message was released to.
        - **Released by**:
            - Admin released: `<email address of admin who released the message> released for <recipient>`. For example, `admin@contoso.com released to laura@contoso.com`.
            - User released: The user's SMTP address.
            - System released: "System released."
            - Other: The default behavior is admin released.
    - **Sender address override reason**

The rest of the details flyout contains the **Delivery details**, **Email details**, **Authentication**, **URLs**, and **Attachments** sections that are part of the *Email summary panel*. For more information, see [The Email summary panel](mdo-email-entity-page#the-email-summary-panel).

[![Screenshot of the details flyout that opens after you select a quarantined email message from the Email tab of the Quarantine page.](media/quarantine-message-details-flyout-with-actions.png)](media/quarantine-message-details-flyout-with-actions.png#lightbox)

To take action on the message, see Take action on quarantined email.

Tip

To see details about other quarantined messages without leaving the details flyout, use ![](media/updownarrows.png)**Previous item** and **Next item** at the top of the flyout.

### Take action on quarantined email

Use the following steps to select a quarantined email message and access its available actions.

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Review** &gt; **Quarantine** &gt; **Email** tab. Or, to go directly to the **Email** tab on the **Quarantine** page, use https://security.microsoft.com/quarantine?viewid=Email.
2. On the **Email** tab, select the quarantined email message by using either of the following methods:

    - Select the message from the list by selecting the check box next to the first column. The available actions are no longer grayed out.

        [![Screenshot of the available actions after you select the check box of a quarantined message on the Email tab on the Quarantine page.](media/quarantine-message-selected-message-actions-remove-blocked.png)](media/quarantine-message-selected-message-actions-remove-blocked.png#lightbox)
    - Select the message from the list by clicking anywhere in the row other than the check box. The available actions are in the details flyout that opens.

        [![Screenshot of the available actions in the details flyout that opens after you select a quarantined message on the Email tab of the Quarantine page.](media/quarantine-message-details-flyout-actions.png)](media/quarantine-message-details-flyout-actions.png#lightbox)

    Using either method to select the message, many actions are available under ![](media/defender-portal-icon-more-actions.png)**More** or **More options**.

After you select the quarantined message, the available actions are described in the following subsections.

Tip

On mobile devices, the action experience is slightly different:

- When you select the message by selecting the check box, all actions are under ![](media/defender-portal-icon-more-actions.png)**More**:

    [![Screenshot of selecting a quarantined message and selecting More on a mobile device.](media/quarantine-message-main-page-mobile-actions.png)](media/quarantine-message-main-page-mobile-actions.png#lightbox)
- When you select the message by clicking anywhere in the row other than the check box, description text isn't available on some action icons in the details flyout. But, the actions and their order are the same as on a PC:

    [![Screenshot of the details of a quarantined message with available actions highlighted.](media/quarantine-message-details-flyout-mobile-actions.png)](media/quarantine-message-details-flyout-mobile-actions.png#lightbox)

#### Release quarantined email

The **Release** action isn't available for email messages already released (the **Release status** value is **Released**).

Messages are automatically deleted from quarantine after the date shown in the **Expires** column if you don't release or manually remove the messages.

- You can't release a message to the same recipient more than once.
- You can't choose to release messages only to recipients who didn't receive the released message.
- Members of the **Security Administrators** role group can see and use the **Submit the message to Microsoft to improve detection** and **Allow email with similar attributes** options.
- Users can report false positives to Microsoft from quarantine, depending on the value of the **Reporting from quarantine** setting in [user reported settings](submissions-user-reported-messages-custom-mailbox).
- For messages quarantined by Safe Attachments because they contain an encrypted (password-protected) attachment that couldn't be scanned, you release the message with full authority without providing the attachment password. Only end users are prompted for the password when they release these messages themselves. For more information, see [Encrypted (password-protected) attachments in Safe Attachments policies](safe-attachments-about#encrypted-password-protected-attachments-in-safe-attachments-policies).

Tip

- Non-Microsoft anti-virus solutions, security services, and [outbound connectors](/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/use-connectors-to-configure-mail-flow) can cause the following issues for messages that are released from quarantine:

    - The message is quarantined after being released.
    - Content is removed from the released message before it reaches the recipient's Inbox.
    - The released message never arrives in the recipient's Inbox.
    - Actions in [quarantine notifications](quarantine-quarantine-notifications) might be randomly selected.

    Verify that you aren't using non-Microsoft filtering before you open a support ticket about these issues.
- Inbox rules (created by users in Outlook or by admins by using the **\*-InboxRule** cmdlets in Exchange Online PowerShell) can move or delete messages from the Inbox.
- Admins can use [message trace](message-trace-defender-portal) to determine if a released message was delivered to the recipient's Inbox.
- Selecting **Move or delete** &gt; **Inbox** on quarantined messages in ![](media/defender-portal-icon-take-actions.png)**Take action** from other Defender for Office 365 features (for example, Explorer (Threat Explorer) or the Email entity page) also allows you to release messages from quarantine. For more information, see [Threat hunting: The Take action wizard](threat-explorer-threat-hunting#the-take-action-wizard).

After you select the message, use either of the following methods to release it:

- **On the Email tab**: Select ![](media/defender-portal-icon-check-mark.png)**Release**.
- **In the details flyout of the selected message**: Select ![](media/defender-portal-icon-check-mark.png)**Release email**.

In the **Release email to recipient inboxes** flyout that opens, configure the following options:

- **Send a copy of this message to other recipients**: If you select this option, select one or more recipients by clicking in the **Recipients** box that appears. Select ![](media/defender-portal-icon-remove-selection.png) to remove an entry.
- **Submit the message to Microsoft to improve detection (false positive)**: If you select this option, the erroneously quarantined message is reported to Microsoft as a false positive. Depending on the results of their analysis, the service-wide spam filter rules might be adjusted to allow the message through.

    Selecting this option also reveals the following options:

    - **Allow this message**: If you select this option, allow entries are added to the [Tenant Allow/Block List](tenant-allow-block-list-about)for the sender and any related URLs or attachments in the message. The following options also appear:
        - **Remove entry after**: The default value is **45 days after last used date**, but you can also select **1 day**, **7 days**, **30 days**, or a **Specific date** that's less than 30 days.
        - **Allow entry note (optional)**: Enter an optional note that contains additional information.

When you're finished on the **Release email to recipient inboxes** flyout, select **Release message**.

Back on the **Email** tab, the **Release status** value of the message is **Released**.

Note

Releasing a message from quarantine re-delivers it to the recipient's mailbox rather than restoring it in place. As a result, the message appears in Outlook with the re-delivery time as the delivery timestamp instead of the original delivery time. The original send date is preserved in the message headers.

#### Approve or deny release requests from users for quarantined email

Users can request the release of email messages if the quarantine policy used **Allow recipients to request a message to be released from quarantine** (`PermissionToRequestRelease` permission) instead of **Allow recipients to release a message from quarantine** (`PermissionToRelease` permission) when the message was quarantined. For more information, see [Create quarantine policies in the Microsoft Defender portal](quarantine-policies#step-1-create-quarantine-policies-in-the-microsoft-defender-portal).

After a recipient requests the release of the email message, the **Release status** value changes to **Release requested**, and an admin can approve or deny the request.

Tip

One alert to release the message might be created for multiple release requests for that message. Use the **quarantine** link in the **Details** section of the alert message to take action on the release request from users in the organization for the past 7 days.

Messages are automatically deleted from quarantine after the date shown in the **Expires** column if you don't release or manually remove the messages.

After you select the message, use either of the following methods to approve or deny the release request:

- **On the Email tab**: Select ![](media/defender-portal-icon-check-mark.png)**Release** or ![](media/defender-portal-icon-deny.png)**Deny**.
- **In the details flyout of the selected message**: Select ![](media/defender-portal-icon-check-mark.png)**Release email** or ![](media/defender-portal-icon-more-actions.png)**More** &gt; ![](media/defender-portal-icon-deny.png)**Deny release**.

If you select **Release** or **Release email**, a **Release email to recipient inboxes** flyout opens. The options are the same as described in Release quarantined email.

After you release the message, the **Release status** value of the message changes to **Released** on the **Email** tab.

If you select **Deny** or **Deny release**, a **Deny release** flyout opens where you can review information about the message. When you select **Deny release**, a **Release denied** flyout opens where you can select the link to learn more about releasing messages. Select **Done** when you're finished on the **Release denied** flyout.

Back on the **Email** tab, the **Release status** value of the message changes to **Denied**.

Tip

You can deny release for all recipients only. You can't deny release for specific recipients.

#### Delete email from quarantine

When you delete an email message from quarantine, the message is removed and isn't sent to the original recipients.

Messages are automatically deleted from quarantine after the date shown in the **Expires** column if you don't release or manually remove the messages.

After you select the message, use either of the following methods to remove it:

- **On the Email tab**: Select ![](media/defender-portal-icon-delete.png)**Delete from quarantine**.
- **In the details flyout of the selected message**: Select ![](media/defender-portal-icon-more-actions.png)**More options** &gt; ![](media/defender-portal-icon-delete.png)**Delete from quarantine**.

Warning

Deleting the message from quarantine is permanent and the message isn't recoverable.

In the **Delete (n) messages from quarantine** flyout that opens, select **Permanently delete the message from quarantine** and then select **Delete**.

Back on the **Email** tab, the deleted message is no longer listed.

#### Preview email from quarantine

After you select the message, use either of the following methods to preview it:

- **On the Email tab**: Select ![](media/defender-portal-icon-preview-message.png)**Preview message**.
- **In the details flyout of the selected message**: Select ![](media/defender-portal-icon-more-actions.png)**More options** &gt; ![](media/defender-portal-icon-preview-message.png)**Preview message**.

In the flyout that opens, choose one of the following tabs:

- **Source**: Shows the HTML version of the message body with all links disabled.
- **Plain text**: Shows the message body in plain text.

#### View email message headers

After you select the message, use either of the following methods to view the message headers:

- **On the Email tab**: Select ![](media/defender-portal-icon-more-actions.png)**More** &gt; ![](media/defender-portal-icon-view-message-headers.png)**View message headers**.
- **In the details flyout of the selected message**: Select ![](media/defender-portal-icon-more-actions.png)**More options** &gt; ![](media/defender-portal-icon-view-message-headers.png)**View message headers**.

In the **Message header** flyout that opens, the message header (all header fields) is shown.

Use ![](media/defender-portal-icon-copy.png)**Copy message header** to copy the message header to the clipboard.

Select the **Microsoft Message Header Analyzer** link to analyze the header fields and values in depth. Paste the message header into the **Insert the message header you would like to analyze** section (CTRL+V or right-click and choose **Paste**), and then select **Analyze headers**.

#### Submit email to Microsoft for review from quarantine

After you select the message, use either of the following methods to submit the message to Microsoft for analysis:

- **On the Email tab**: Select ![](media/defender-portal-icon-more-actions.png)**More** &gt; ![](media/defender-portal-icon-create.png)**Submit for review**.
- **In the details flyout of the selected message**: Select ![](media/defender-portal-icon-more-actions.png)**More options** &gt; ![](media/defender-portal-icon-create.png)**Submit for review**.

In the **Submit to Microsoft for analysis** flyout that opens, configure the following options:

- **Add the network message ID or upload the email file**: Select one of the following options:

    - **Add the email network message ID**: This value is selected by default, with the corresponding value in the box.
    - **Upload the email file (.msg or eml)**: After you select this option, select the ![](media/defender-portal-icon-import.png)**Browse files** button that appears to find and select the .msg or .eml message file to submit.
- **Choose a recipient who had an issue**: Select one (preferred) or more original recipients of the message to analyze the policies that were applied to them.
- **Select a reason for submitting to Microsoft**: Choose one of the following options:

    - **I've confirmed it's clean** (default): Select this option if you're sure that the message is clean, and then select **Next**. Then the following settings are available:

        - **Allow this email**: If you select this option, allow entries are added to the [Tenant Allow/Block List](tenant-allow-block-list-about) for the sender and any related URLs or attachments in the message. The following options also appear:
        - **Remove entry after**: The default value is **45 days after last used date**, but you can also select **1 day**, **7 days**, **30 days**, or a **Specific date** that's less than 30 days.
        - **Allow entry note**: Enter an optional note that contains additional information.
    - **It appears clean**: Select this option if you're unsure and you want a verdict from Microsoft.

When you're finished on the **Submit to Microsoft for analysis** flyout, select **Submit**.

Tip

Users can report false positives to Microsoft from quarantine, depending on the value of the **Reporting from quarantine** setting in [user reported settings](submissions-user-reported-messages-custom-mailbox).

#### Allow email senders from quarantine

Tip

The **Allow sender** action is available to admins only if they filter the quarantine results by **Recipient** &gt; **Only me** instead of the default value **All users**.

If the sender is already in the recipient's [safelist collection](configure-junk-email-settings-on-exo-mailboxes), **Allow sender** isn't available.

The **Allow sender** action adds the sender of the selected email message to the Safe Senders list **in the mailbox of whomever is signed in**. Typically, this action is for end-users if it's available to them by [quarantine policies](quarantine-policies#anatomy-of-a-quarantine-policy). For more information about users allowing senders, see [Add recipients of my email messages to the Safe Senders List](https://support.microsoft.com/office/be1baea0-beab-4a30-b968-9004332336ce).

After you select the message, use either of the following methods to add the message sender to the Safe Senders list in **your own** mailbox:

- **On the Email tab**: Select ![](media/defender-portal-icon-allow-sender.png)**More** &gt; ![](media/defender-portal-icon-block-sender.png)**Allow sender**.
- **In the details flyout of the selected message**: Select ![](media/defender-portal-icon-allow-sender.png)**More options** &gt; ![](media/defender-portal-icon-block-sender.png)**Allow sender**.

The flyout that opens indicates when the sender was successfully added to your Safe Senders list. Select **Done**.

#### Block email senders from quarantine

Tip

The **Block sender** action is available to admins only if they filter the quarantine results by **Recipient** &gt; **Only me** instead of the default value **All users**.

If the sender is already in the recipient's [safelist collection](configure-junk-email-settings-on-exo-mailboxes), **Block sender** isn't available. **Remove sender from user block list** is available instead.

The **Block sender** action adds the sender of the selected email message to the Blocked Senders list **in the mailbox of whomever is signed in**. Typically, this action is for end-users if it's available to them by [quarantine policies](quarantine-policies#anatomy-of-a-quarantine-policy). For more information about users blocking senders, see [Block a mail sender](https://support.microsoft.com/office/b29fd867-cac9-40d8-aed1-659e06a706e4)

After you select the message, use either of the following methods to add the message sender to the Blocked Senders list in **your own** mailbox:

- **On the Email tab**: Select ![](media/defender-portal-icon-more-actions.png)**More** &gt; ![](media/defender-portal-icon-block-sender.png)**Block sender**.
- **In the details flyout of the selected message**: Select ![](media/defender-portal-icon-more-actions.png)**More options** &gt; ![](media/defender-portal-icon-block-sender.png)**Block sender**.

In the **Block sender** flyout that opens, review the information about the sender, and then select **Block**.

Tip

The organization can still receive mail from the blocked sender. The policy precedence as described in [User allows and blocks](how-policies-and-protections-are-combined#user-allows-and-blocks) determines whether messages from the sender are delivered to the Junk Email folder or to quarantine. To delete messages from the blocked sender upon arrival, use [mail flow rules](/en-us/exchange/security-and-compliance/mail-flow-rules/mail-flow-rules) (also known as transport rules) to **Block the message**.

#### Remove senders from user Blocked Senders lists from quarantine

The **Remove sender from user block list** is available only if the sender of the quarantined message is already in the recipient's [Block Senders list](configure-junk-email-settings-on-exo-mailboxes).

Admins can remove senders from the Block Senders list of their own mailboxes (if quarantine is filtered by **Recipient** &gt; **Only me**) or from the mailboxes of other users (if quarantine is filtered by **Recipient** &gt; **All users**).

After you select the message, use either of the following methods to remove the sender from the user's Block Senders list:

- **On the Email tab**: Select ![](media/defender-portal-icon-more-actions.png)**More** &gt; ![](media/defender-portal-icon-remove-sender.png)**Remove sender from user block list**.
- **In the details flyout of the selected message**: Select ![](media/defender-portal-icon-more-actions.png)**More options** &gt; ![](media/defender-portal-icon-remove-sender.png)**Remove sender from user block list**.

The flyout that opens indicates when the sender was successfully removed from the recipient's Blocked Senders list. Select **Done**.

#### Share email from quarantine

You can send a copy of the quarantined email message, including potentially harmful content, to the specified recipients.

After you select the message, use either of the following methods to send a copy of it to others:

- **On the Email tab**: Select ![](media/defender-portal-icon-more-actions.png)**More** &gt; ![](media/defender-portal-icon-share-email.png)**Share email**.
- **In the details flyout of the selected message**: Select ![](media/defender-portal-icon-more-actions.png)**More options** &gt; ![](media/defender-portal-icon-share-email.png)**Share email**.

In the **Share email with other users** flyout that opens, select one or more recipients to receive a copy of the message. When you're finished, select **Share**.

#### Download email from quarantine

After you select the email message, use either of the following methods to download it:

- **On the Email tab**: Select ![](media/defender-portal-icon-more-actions.png)**More** &gt; ![](media/defender-portal-icon-download.png)**Download messages**.
- **In the details flyout of the selected message**: Select ![](media/defender-portal-icon-more-actions.png)**More options** &gt; ![](media/defender-portal-icon-download.png)**Download message**.

In the **Download file** flyout that opens, enter the following information:

- **Reason for downloading file**: Enter descriptive text.
- **Create password** and **Confirm password**: Enter the password required to open the downloaded message file.

When you're finished on the **Download file** flyout, select **Download**.

When the download is ready, a **Save As** dialog opens for you to view or change the downloaded filename and location. By default, The .eml message file is saved in a compressed file named Quarantined Messages.zip in your **Downloads** folder. If the .zip file already exists, a number is appended to the filename (for example, Quarantined Messages(1).zip).

Accept or change the downloaded file details, and then select **Save**.

Back on the **Download file** flyout, select **Done**.

#### Actions for quarantined email messages in Defender for Office 365

In organizations with Microsoft Defender for Office 365 (add-on licenses or included in subscriptions like Microsoft 365 E5 or Microsoft 365 Business Premium), the following actions are also available in the details flyout of a selected message:

- ![](media/defender-portal-icon-open.png)**Open email entity**: For more information, see [What's on the Email entity page](mdo-email-entity-page#whats-on-the-email-entity-page).
- ![](media/defender-portal-icon-take-actions.png)**Take actions**: This action starts the same Action wizard that's available on the Email entity page. For more information, see [Actions on the Email entity page](mdo-email-entity-page#actions-on-the-email-entity-page).

#### Take action on multiple quarantined email messages

When you select up to 100 quarantined messages on the **Email** tab by selecting the check boxes next to the first column, the following bulk actions are available on the **Email** tab (depending on the **Release status** values of the messages that you selected):

- Release quarantined email messages:

    - Not available for messages with the **Release status** value **Released**.
    - Approve user release requests if the **Release status** value of the messages is **Released requested**.

    The only available options to select for bulk actions are **Send a copy of this message to other recipients** and **Send the message to Microsoft to improve detection (false positive)**.
- Approve or deny release requests from users for quarantined email
- Delete email from quarantine
- Submit email messages to Microsoft for review

    The only available options to select for bulk actions are **Allow emails with similar attributes** and the related **Remove allow entry after** and **Allow entry note** options.
- Download email messages from quarantine

[![Screenshot of the available actions on the Email tab of the Quarantine page after you select the check box of multiple quarantined messages.](media/quarantine-message-bulk-actions.png)](media/quarantine-message-bulk-actions.png#lightbox)

### Find who deleted a quarantined message

By default, many threat policy verdicts allow users to delete their quarantined messages (messages where they're a recipient). For more information, see the table at [Manage quarantined messages and files as a user](quarantine-end-user).

Admins can search the audit log to find events for messages that were deleted from quarantine by using the following procedures:

1. In the Defender portal at https://security.microsoft.com, go to **Audit**. Or, to go directly to the **Audit** page, use https://security.microsoft.com/auditlogsearch.

    Tip

    You can also get to the **Audit** page in the Microsoft Purview portal at https://purview.microsoft.com/auditlogsearch
2. On the **Audit** page, verify that the **New Search** tab is selected, and then configure the following settings:

    - **Date and time range (UTC)**
    - **Activities - friendly names**: Click in the box, start typing "quarantine" in the ![](media/defender-portal-icon-search.png)**Search** box that appears, and then select **Deleted Quarantine message** from the results.
    - **Users**: If you know who deleted the message from quarantine, you can further filter the results by user.
3. When you're finished entering the search criteria, select **Search** to generate the search.

For complete instructions for audit log searches, see [Audit New Search](/en-us/purview/audit-new-search).

## Use the Microsoft Defender portal to manage quarantined files in Defender for Office 365

Note

The procedures for quarantined files in this section are available only to Microsoft Defender for Office 365 Plan 1 or Plan 2 subscribers.

Files quarantined in SharePoint or OneDrive are removed from quarantine after 30 days, but the blocked files remain in SharePoint or OneDrive in the blocked state.

In organizations with Defender for Office 365, admins can manage files quarantined by Safe Attachments for SharePoint, OneDrive, and Microsoft Teams. To enable protection for these files, see [Turn on Safe Attachments for SharePoint, OneDrive, and Microsoft Teams](safe-attachments-for-spo-odfb-teams-configure).

### View quarantined files

In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Review** &gt; **Quarantine** &gt; **Files** tab. Or, to go directly to the **Files** tab on the **Quarantine** page, use https://security.microsoft.com/quarantine?viewid=Files.

On the **Files** tab, you can decrease the vertical spacing in the list by clicking ![](media/defender-portal-icon-standard.png)**Change list spacing to compact or normal** and then selecting ![](media/defender-portal-icon-compact.png)**Compact list**.

You can sort the entries by clicking on an available column header. Select ![](media/defender-portal-icon-customize.png)**Customize columns** to change the columns that are shown. The default values are marked with an asterisk (^\*^):

- **User**^\*^
- **Location**^\*^: The value is **SharePoint** or **OneDrive**.
- **Attachment filename**^\*^
- **File URL**^\*^
- **File Size**
- **Release status**^\*^
- **Expires**^\*^
- **Detected by**
- **Modified by time**

To filter the entries, select ![](media/defender-portal-icon-filter.png)**Filter**. The following filters are available in the **Filters** flyout that opens:

- **Time received**:
    - **Last 24 hours**
    - **Last 7 days**
    - **Last 14 days**
    - **Last 30 days** (default)
    - **Custom**: Enter a **Start time** and **End time** (date).
- **Expires**:
    - **Custom** (default): Enter a **Start time** and **End time** (date).
    - **Today**
    - **Next 2 days**
    - **Next 7 days**
- **Quarantine reason**: The only available value is **Malware**.
- **Policy type**: The only available value is **Unknown**.

When you're finished in the **Filters** flyout, select **Apply**. To clear the filters, select ![](media/defender-portal-icon-clear-filters.png)**Clear filters**.

Use the ![](media/defender-portal-icon-search.png)**Search** box and a corresponding value to find specific files by filename. Wildcards aren't supported.

After you enter the search criteria, press Enter to filter the results.

After you find a specific quarantined file, select the file to view details about it and to take action on it (for example, view, release, download, or delete the file).

### View quarantined file details

Use the following steps to open the details flyout for a quarantined file.

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Review** &gt; **Quarantine** &gt; **Files** tab. Or, to go directly to the **Files** tab on the **Quarantine** page, use https://security.microsoft.com/quarantine?viewid=Files.
2. On the **Files** tab, select the quarantined file by clicking anywhere in the row other than the check box.

In the details flyout that opens, the following information is available:

[![Screenshot of the details flyout that opens after you select a quarantined file from the Files tab of the Quarantine page.](media/quarantine-file-details-flyout.png)](media/quarantine-file-details-flyout.png#lightbox)

- **File details**section:
    - **File Name**
    - **File URL**: URL that defines the location of the file (for example, in SharePoint).
    - **Malicious content detected on** The date/time the file was quarantined.
    - **Expires**: The date when the file is automatically deleted from quarantine.
    - **Detected by**
    - **Released?**
    - **Malware Name**
    - **Document ID**: A unique identifier for the document.
    - **File Size**
    - **Organization** Your organization's unique ID.
    - **Last modified**
    - **Last modified By**: The user who last modified the file.
    - **Secure Hash Algorithm 256-bit (SHA-256) value**: You can use this hash value to identify the file in other reputation stores or in other locations in your environment.

To take action on the file, see Take action on quarantined files.

Tip

To see details about other quarantined files without leaving the details flyout, use ![](media/updownarrows.png)**Previous item** and **Next item** at the top of the flyout.

### Take action on quarantined files

Use the following steps to select a quarantined file and view the actions available for it.

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Review** &gt; **Quarantine** &gt; **Files** tab. Or, to go directly to the **Files** tab on the **Quarantine** page, use https://security.microsoft.com/quarantine?viewid=Files.
2. On the **Files** tab, select the quarantined file by clicking anywhere in the row other than the check box.

After you select the quarantined file, the available actions in the file details flyout that opens are described in the following subsections.

[![Screenshot of the available actions in the details flyout that opens after you select a quarantined file from the Files tab of the Quarantine page.](media/quarantine-file-details-flyout-actions.png)](media/quarantine-file-details-flyout-actions.png#lightbox)

#### Release quarantined files from quarantine

The **Release file** action isn't available for files already released (the **Released status** value is **Released**).

Messages are automatically deleted from quarantine after the date shown in the **Expires** column if you don't release or manually remove the messages, but the blocked file remains in SharePoint or OneDrive in the blocked state.

After you select the file, select ![](media/defender-portal-icon-check-mark.png)**Release file** in the file details flyout that opens.

In the **Release files and report them to Microsoft** flyout that opens, view the file details in the **Release the following files** section, and then select **Release**.

Tip

Currently, you can't report quarantined files to Microsoft as you release them.

In the **Files have been released** flyout that opens, select **Done**.

Back on the file details flyout, select **Close**.

Back on the **Files** tab, the **Release status** value of the file is **Released**.

#### Download quarantined files from quarantine

After you select the file, select ![](media/defender-portal-icon-download.png)**Download file** in the details flyout that opens.

In the **Download file** flyout that opens, enter the following information:

- **Reason for downloading file**: Enter descriptive text.
- **Create password** and **Confirm password**: Enter a password required to open the downloaded file.

When you're finished on the **Download file** flyout, select **Download**.

When the download is ready, a **Save As** dialog opens for you to view or change the downloaded filename and location. By default, The file is saved in a compressed file named Quarantined Messages.zip in your **Downloads** folder. If the .zip file already exists, a number is appended to the filename (for example, Quarantined Messages(1).zip).

Accept or change the downloaded file details, and then select **Save**.

Back on the **Download file** flyout, select **Done**.

#### Delete quarantined files from quarantine

Messages are automatically deleted from quarantine after the date shown in the **Expires** column if you don't release or manually remove the messages, but the blocked file remains in SharePoint or OneDrive in the blocked state.

Warning

Deleting a file from quarantine is a destructive action that can't be undone.

After you select the file, select ![](media/defender-portal-icon-more-actions.png)**More** &gt; ![](media/defender-portal-icon-delete.png)**Delete from quarantine** in the details flyout that opens. Review the warning dialog, and then select **Continue** to proceed.

Back on the **Files** tab, the file is no longer listed.

#### Take action on multiple quarantined files

When you select multiple quarantined files on the **Files** tab by selecting the check boxes next to the first column (up to 100 files), a **Bulk actions** dropdown list appears where you can take the following actions:

- Release quarantined files from quarantine
- Delete quarantined files from quarantine
- Download quarantined files from quarantine

[![Screenshot of the available actions on the Files tab of the Quarantine page after you select the check box of multiple quarantined files.](media/quarantine-file-bulk-actions.png)](media/quarantine-file-bulk-actions.png#lightbox)

## Use the Microsoft Defender portal to manage Microsoft Teams quarantined messages

Note

Currently, the quarantine policy for Teams is set to AdminOnlyAccess, which means users can't access quarantined Teams messages. We're actively working to update quarantine policy configurations.

Quarantine in Microsoft Teams is available only in organizations with Microsoft Defender for Office 365 Plan 1 or Plan 2 (add-on licenses or included in subscriptions like Microsoft 365 E5).

When a potentially malicious chat message is detected in Microsoft Teams, zero-hour auto purge (ZAP) removes the message and quarantines it. Admins can view and manage these quarantined Teams messages. The message is quarantined for 30 days. After that the Teams message is permanently removed.

This feature is enabled by default.

### View quarantined Teams messages

In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Review** &gt; **Quarantine** &gt; **Teams messages** tab. Or, to go directly to the **Teams messages** tab on the **Quarantine** page, use https://security.microsoft.com/quarantine?viewid=Teams.

On the **Teams messages** tab, you can decrease the vertical spacing in the list by clicking ![](media/defender-portal-icon-standard.png)**Change list spacing to compact or normal** and then selecting ![](media/defender-portal-icon-compact.png)**Compact list**.

You can sort the entries by clicking on an available column header. Select ![](media/defender-portal-icon-customize.png)**Customize columns** to change the columns that are shown. The default values are marked with an asterisk (^\*^):

- **Teams message text**: Contains the subject for the Teams message.^\*^
- **Time received**: The time the recipient received the message.^\*^
- **Release status**: Shows whether the message is already reviewed and released or needs review. ^\*^
- **Participants**: The total number of users who received the message.^\*^
- **Sender**: The person who sent the message that was quarantined.^\*^
- **Quarantine reason**: Available options are "High confidence phish" and "Malware".^\*^
- **Policy type**: The organization policy responsible for the quarantined message.^\*^
- **Expires**: Indicates the time after which the message is removed from quarantine. By default, this value is 30 days.^\*^
- **Recipient address**: Email address of the recipients.^\*^
- **Message ID**: Includes the chat message ID.

To filter the entries, select ![](media/defender-portal-icon-filter.png)**Filter**. The following filters are available in the **Filters** flyout that opens:

- **Message ID**
- **Sender address**
- **Recipient address**
- **Subject**
- **Time received**:
    - **Last 24 hours**
    - **Last 7 days**
    - **Last 14 days**
    - **Last 30 days** (default)
    - **Custom**: Enter a **Start time** and **End time** (date).
- **Expires**:
    - **Custom** (default): Enter a **Start time** and **End time** (date).
    - **Today**
    - **Next 2 days**
    - **Next 7 days**
- **Quarantine reason**: Available values are **Malware** and **High confidence phishing**.
- **Recipient**: Select **All users** or **Only me**.
- **Review status**: Select **Needs review** and **Released**.

When you're finished in the **Filters** flyout, select **Apply**. To clear the filters, select ![](media/defender-portal-icon-clear-filters.png)**Clear filters**.

Use the ![](media/defender-portal-icon-search.png)**Search** box and a corresponding value to find specific Teams messages. Wildcards aren't supported.

After you find a specific quarantined Teams message, select the message to view details about it and to take action on it (for example, view, release, download, or delete the message).

### View quarantined Teams message details

On the **Teams messages** tab of the **Quarantine** page, select the quarantined message by clicking anywhere in the row other than the check box next to the first column.

The following message information is available at the top of the details flyout:

- The title of the flyout is the subject or the first 100 characters of the Teams message.
- The **Quarantine reason** value.
- The number of links in the message.
- The available actions are described in Take action on quarantined Teams messages.

Tip

To see details about other quarantined Teams messages without leaving the details flyout, use ![](media/updownarrows.png)**Previous item** and **Next item** at the top of the flyout.

The **Quarantine details** section in the details flyout contains information related to quarantined Teams messages:

- **Quarantine details**section:
    - **Expires**
    - **Time received**
    - **Quarantine reason**
    - **Release status**
    - **Policy type**: The value is **None**.
    - **Policy name**: The value is **Teams Protection Policy**.
    - **Quarantine policy**

The rest of the details flyout contains the **Message details**, **Sender**, **Participants**, **Channel details**, and **URLs** sections that are part of the *Teams message entity panel*. For more information, see [The Teams message entity panel in Microsoft Defender for Office 365](teams-message-entity-panel).

When you're finished in the details flyout, select **Close**.

[![Screenshot of the details flyout that opens after you select a quarantined Teams message from the Teams messages tab of the Quarantine page.](media/quarantine-teams-details-flyout.png)](media/quarantine-teams-details-flyout.png#lightbox)

### Take action on quarantined Teams messages

In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Review** &gt; **Quarantine** &gt; **Teams messages** tab. Or, to go directly to the **Teams messages** tab on the **Quarantine** page, use https://security.microsoft.com/quarantine?viewid=Teams.

On the **Teams messages** tab, select the quarantined message by using either of the following methods:

- Select the message from the list by selecting the check box next to the first column. The available actions are no longer grayed out.

    [![Screenshot of the available actions after you select the check box of a quarantined Teams message on the Teams message tab of the Quarantine page.](media/quarantine-teams-message-selected-message-actions.png)](media/quarantine-teams-message-selected-message-actions.png#lightbox)
- Select the message from the list by clicking anywhere in the row other than the check box. The available actions are in the details flyout that opens.

    [![Screenshot of the available actions in the details flyout that opens after you select a quarantined Teams message from the Teams messages tab of the Quarantine page.](media/quarantine-teams-details-flyout-actions.png)](media/quarantine-teams-details-flyout-actions.png#lightbox)

Using either method to select the message, some actions are available under ![](media/defender-portal-icon-more-actions.png)**More**.

After you select the quarantined Teams message, the available actions are described in the following subsections.

#### Release quarantined Teams messages

The **Release** action isn't available for Teams messages already released (the **Release status** value is **Released**).

Teams messages are automatically deleted from quarantine after the date shown in the **Expires** column if you don't release or manually remove the messages.

After you select the message, use either of the following methods to release it to all chat participants:

- **On the Teams messages tab**: Select ![](media/defender-portal-icon-check-mark.png)**Release**.
- **In the details flyout of the selected message**: Select ![](media/defender-portal-icon-check-mark.png)**Release**.

In the **Release message to your Teams app** flyout that opens, decide whether to select **Submit the message to Microsoft to improve detection (false positive)**, and then select **Release**.

#### Delete Teams messages from quarantine

Teams messages are automatically deleted from quarantine after the date shown in the **Expires** column if you don't release or manually remove the messages.

Warning

Deleting a Teams message from quarantine is a destructive action that can't be undone.

After you select the Teams message, use either of the following methods to remove it:

- **On the Teams messages tab**: Select ![](media/defender-portal-icon-delete.png)**Delete messages**.
- **In the details flyout of the selected message**: Select ![](media/defender-portal-icon-more-actions.png)**More options** &gt; ![](media/defender-portal-icon-delete.png)**Delete from quarantine**.

In the warning dialog that opens, read the information and then select **Continue**.

Back on the **Teams messages** tab, the message is no longer listed.

#### Preview Teams messages from quarantine

After you select the Teams message, use either of the following methods to preview it:

- **On the Teams messages tab**: Select ![](media/defender-portal-icon-preview-message.png)**Preview message**.
- **In the details flyout of the selected message**: Select ![](media/defender-portal-icon-more-actions.png)![](media/defender-portal-icon-preview-message.png)**Preview message**.

In the flyout that opens, choose one of the following tabs:

- **Source**: Shows the HTML version of the message body with all links disabled.
- **Plain text**: Shows the message body in plain text.

#### Submit Teams messages to Microsoft for review from quarantine

After you select the message, use either of the following methods to submit the message to Microsoft for analysis:

- **On the Teams messages tab**: Select ![](media/defender-portal-icon-more-actions.png)**More** &gt; ![](media/defender-portal-icon-create.png)**Submit for review**.
- **In the details flyout of the selected message**: Select ![](media/defender-portal-icon-more-actions.png)**More options** &gt; ![](media/defender-portal-icon-create.png)**Submit for review**.

When you select **Submit message**, the message is sent to Microsoft for analysis. You receive an **Item** submitted dialog where you select **OK**.

#### Download Teams messages from quarantine

After you select the Teams message, use either of the following methods to download it:

- **On the Teams messages tab**: Select ![](media/defender-portal-icon-more-actions.png)**More** &gt; ![](media/defender-portal-icon-download.png)**Download messages**.
- **In the details flyout of the selected message**: Select ![](media/defender-portal-icon-more-actions.png)**More options** &gt; ![](media/defender-portal-icon-download.png)**Download message**.

In the **Download messages** flyout that opens, enter the following information:

- **Reason for downloading file**: Enter descriptive text.
- **Create password** and **Confirm password**: Enter a password required to open the downloaded message file.

When you're finished on the **Download file** flyout, select **Download**.

By default, The .html message file is saved in a compressed file named Quarantined Messages.zip in your **Downloads** folder. If the .zip file already exists, a number is appended to the filename (for example, Quarantined Messages(1).zip).

Back on the **Download messages** flyout, select **Done**.

#### Remove users from quarantined Teams chats

Tip

Currently, this feature is in Preview, isn't available in all organizations, is subject to change, and is available only in organizations with Microsoft Defender for Office 365 Plan 2.

For complete instructions, see [Remove users from Teams chats in the Teams message entity panel](teams-message-entity-panel#remove-users-from-teams-chats-in-the-teams-message-entity-panel). The opening steps of the procedure are:

1. On the **Teams messages** tab, select the Teams message by clicking anywhere in the row other than the check box next to the first column.
2. In the details flyout that opens (the Teams message entity panel), select ![](media/defender-portal-icon-more-actions.png)**More actions** &gt; ![](media/defender-portal-icon-take-actions.png)**Take action** at the top of the flyout.

#### Take action on multiple quarantined Teams messages

When you select multiple quarantined messages on the **Teams messages** tab by selecting the check boxes next to the first column, the following bulk actions are available on the **Teams messages** tab:

- Release quarantined Teams messages
- Delete Teams messages from quarantine
- Submit Teams messages to Microsoft for review from quarantine
- Download Teams messages from quarantine

[![Screenshot of the available actions on the Teams messages tab of the Quarantine page after you select multiple quarantined Teams messages.](media/quarantine-teams-bulk-action.png)](media/quarantine-teams-bulk-action.png#lightbox)

#### Approve or deny release requests from users for quarantined Teams messages

When a user requests the release of a quarantined Teams message, the **Release status** value changes to **Release requested**, and an admin can approve or deny the request.

For more information, see Approve or deny release requests from users for quarantined email.

## Use PowerShell to manage quarantined messages

As an alternative to the Microsoft Defender portal, you can use the following [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell) cmdlets to view and manage quarantined messages and files:

- [Delete-QuarantineMessage](/en-us/powershell/module/exchangepowershell/delete-quarantinemessage)
- [Export-QuarantineMessage](/en-us/powershell/module/exchangepowershell/export-quarantinemessage)
- [Get-QuarantineMessage](/en-us/powershell/module/exchangepowershell/get-quarantinemessage)
- [Preview-QuarantineMessage](/en-us/powershell/module/exchangepowershell/preview-quarantinemessage): This cmdlet is for messages only, not quarantined files.
- [Release-QuarantineMessage](/en-us/powershell/module/exchangepowershell/release-quarantinemessage)

Important

The *PermissionTo\** properties returned by **Get-QuarantineMessage** reflect the permissions of the user who runs the cmdlet. For example, admins who have permission to release quarantined messages might see the value `True` for the *PermissionToRelease*, *PermissionToAllowSender*, and *PermissionToDownload* properties, even when the quarantine policy assigned to the message is `AdminOnlyAccessPolicy`. These values don't represent the actions available to message recipients. To view the end-user permissions configured in a quarantine policy, use **Get-QuarantinePolicy** as described in [View quarantine policies in PowerShell](quarantine-policies#view-quarantine-policies-in-powershell).