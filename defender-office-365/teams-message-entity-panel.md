---
layout: Conceptual
title: Investigate Teams Messages in Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/teams-message-entity-panel
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: how-to
ms.localizationpriority: high
ms.assetid: e100fe7c-f2a1-4b7d-9e08-622330b83653
ms.collection:
- m365-security
- tier1
- highpri
description: Describes the Teams message entity panel for Microsoft Teams in Microsoft Defender for Office 365, how it does post-breach work like ZAP and Safe Links and gives admins a single pane of glass on Teams chat and channel threats like suspicious URLs..
ms.service: defender-office-365
ms.date: 2026-09-18T00:00:00.0000000Z
ms.custom:
- sfi-ga-nochange
- sfi-image-nochange
- msecd-doc-authoring-1028
ai-usage: ai-assisted
locale: en-us
document_id: 429ce83a-61df-3a50-5d55-a7379bcfd935
document_version_independent_id: 429ce83a-61df-3a50-5d55-a7379bcfd935
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/teams-message-entity-panel.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: teams-message-entity-panel
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/teams-message-entity-panel.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: cdf2bc24-bb39-52da-799e-5c49e316f9a0
---

# Investigate Teams Messages in Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn

Like [the Email summary panel](mdo-email-entity-page#the-email-summary-panel), the Microsoft Teams message entity panel brings message details and response actions together in the Microsoft Defender portal. Use the Teams message entity panel to investigate suspicious or malicious chats, channels, and group chats and respond to threats.

The available actions depend on your license and permissions. Defender for Office 365 Plan 1 includes block and submission actions but not **Remove user from conversation**. This article explains the information and actions available in the Teams message entity panel.

## Permissions and licensing for the Teams message entity panel

To use the Teams message entity panel, you need to be assigned permissions. You have the following options:

- *Full access*:

    - [Email & collaboration permissions in the Microsoft Defender portal](mdo-portal-permissions): Membership in the **Organization Management**, **Security Administrator**, or **Quarantine Administrator** role groups.
    - [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): Membership in one of the following roles gives users the required permissions *and* permissions for other features in Microsoft 365: **Global Administrator**^\*^, **Security Administrator**, or **Security Operator**.
- *Read-only access*:

    - Microsoft Entra permissions: **Global Reader** or **Security Reader**.
- *Remove users from Teams chats*: Requires membership in one of the following Microsoft Entra roles: **Global Administrator**^\*^, **Security Administrator**, or **Security Operator**.

    Important

    ^\*^ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.

## Where to find the Teams message entity panel

There are no direct links to the Teams message entity panel from the top levels of the Defender portal. Instead, the Teams message entity panel is available in the following locations:

- From the **Quarantine** page at https://security.microsoft.com/quarantine: Select the **Teams message** tab &gt; select an entry by clicking anywhere in the row other than the check box. The details flyout that opens is the Teams message entity panel.
- From the **Submissions** page at https://security.microsoft.com/reportsubmission:

    - Select the **Teams messages** tab &gt; select an entry by clicking anywhere in the row other than the check box.
    - Select the **User reported** tab &gt; select a Teams entry by clicking anywhere in the row other than the check box. The details flyout that opens is the Teams message entity panel.

        You can filter the entries by selecting ![](media/defender-portal-icon-filter.png)**Filter** &gt; **Message type** &gt; **Teams**.
- From the **Advanced Hunting** page at https://security.microsoft.com/v2/advanced-hunting, select a **TeamsMessageId** value (link) from the **MessageEvents** table in the query results. The details flyout that opens is the Teams message entity panel. For example:

    ```kusto
    UrlClickEvents
    | where ThreatTypes !="" and Workload =="Teams"
    | summarize count() by Url, ThreatTypes, ActionType, Workload
    | project Url, ThreatTypes, ActionType, Workload, ClickCount=count_
    | top 20 by ClickCount
    
    UrlClickEvents
    | limit 100
    
    MessageEvents
    | limit 100
    ```

## What's on the Teams message entity panel

The following information is available at the top of the Teams message entity panel:

- The title of the flyout is the subject or the first 100 characters of the Teams message.
- The current message verdict.
- The number of links in the message.
- The actions that are available at the top of the flyout depend on where you opened the Teams message entity panel.

Tip

To see details about other Teams messages without leaving the Teams message entity panel of the current message, use ![](media/updownarrows.png)**Previous item** and **Next item** at the top of the flyout.

The following sections in the Teams message entity panel depend on where you opened it:

- [Quarantined Teams messages](quarantine-admin-manage-messages-files#view-quarantined-teams-message-details)
- [View Teams admin submission details](submissions-admin#view-teams-admin-submission-details)
- [View user reported Teams message details in Defender for Office 365 Plan 2](submissions-admin#view-user-reported-teams-message-details-in-defender-for-office-365-plan-2)

The rest of the Teams message entity panel contains the following information, regardless of where you opened it:

- **Message details** section:

    - **Threats**
    - **Message location**
    - **Sender address**
    - **Time received**
    - **Detection tech**
    - **Teams message ID**: You can use this value as an identifier of a Teams message in Defender for Office 365.
- **Sender** section:

    - The sender's name and email address
    - **Domain**
    - **External**: The value **Yes** indicates the message was sent between an internal user and an external user.
- One of the following sections, depending on whether the message if from a chat or a channel:

    - Chat: The **Participants**section:
        - **Conversation type**
        - **Chat name**
        - **Name and email**: Contains the name and email addresses of all of the participants (including the sender). If there are more than 10 participants, it also links to a secondary panel that lists all the participants in the chat at the time of the suspected threat.
    - Channel: The **Channel details**section:
        - **Conversation type**
        - **Conversation name**: Contains the name of the channel.
        - **Name and email**: Contains the name and address of the channel.
- **URLs** section:

    - **Name and type** Contains the URL from the Teams message.
    - **Threat**

    If the message has more than 10 URLs, select **View all URLs** to see all of them.

[![Screenshot of the Teams Message Entity panel from a quarantined Teams message showing the common sections.](media/teams-message-entity-panel-shown-in-quarantine.png)](media/teams-message-entity-panel-shown-in-quarantine.png#lightbox)

## Remove users from Teams chats in the Teams message entity panel

Use the following steps to remove users from a Teams chat from the Teams message entity panel.

Tip

You can only remove *internal* users in your organization from a chat.

When you remove users from a chat, the sender of the chat isn't blocked, and the removed users can start new chats with the sender.

In the Teams entity panel, you can select ![](media/defender-portal-icon-take-actions.png)**Take action** at the top of the flyout (often under ![](media/defender-portal-icon-more-actions.png)**More actions**) to remove users from a Teams chat.

Do the following steps in the **Take action** wizard:

1. On the **Choose response actions** page, select **Remove user from conversation** from the **Conversation level actions** section, and then select **Next**.
2. On the **Choose target entities** page, configure the following options:

    - **Name** Enter a unique, descriptive name for the remove user scenario.
    - **Description**: Enter optional details.

    The rest of the page contains a details table with the following information about the users in the chat:

    - **Impacted asset**: The email address of the user.
    - **Action**: This value is always **Remove user from conversation**.
    - **Target entity**: The **Thread id** GUID value of the chat.
    - **Expires on**

    By default, all users in the chat are selected, including external users you can't remove from the chat. Verify the *internal* users to remove from the chat are selected.

    When you're finished on the **Choose target entities** page, select **Next**.

    [![Screenshot of the Choose target entities page of the Take action wizard of the Teams message entity panel in the Microsoft Defender portal.](media/teams-message-entity-panel-choose-target-entities.png)](media/teams-message-entity-panel-choose-target-entities.png#lightbox)
3. On the **Review and submit** page, review your previous selections.

    Select **Back** to go back and change your selections.

    When you're finished on the **Review and submit** page, select **Submit**.

Removing users from a Teams chat is recorded on the **History** tab of the **Action center** page at https://security.microsoft.com/action-center/history. You can filter the results by **Action type** &gt; **Remove users from Teams conversations** and/or **Entity type** &gt; **Teams message**. In the alert details, you can confirm users were or were not removed from the Teams chat.

Tip

Removing users from Teams chats doesn't create an investigation ID or an automated investigation.

## Block senders and domains and submit Teams messages

Use the **Take action** wizard to block an external sender or domain, submit a Teams message to Microsoft for review, or combine these actions. The wizard is available from every Teams message entity panel, including panels opened from Submissions, Advanced Hunting, and Quarantine.

Note

In Defender for Office 365 Plan 1, the wizard includes the block and submission actions, but **Remove user from conversation** is hidden.

Blocking a sender or domain requires membership in the **Security Administrator** or **Security Operator** role. Without the required permissions, the block actions are unavailable.

Complete the following steps in the **Take action** wizard:

1. In the Teams message entity panel, select **Take action** at the top of the flyout.

    ![Screenshot of the Take Action button in the Teams message entity panel.](media/microsoft-teams-message-take-action-button.png)
2. On the **Choose response actions** page, select one or more of the following options in the **Entity-level actions** section:

    - **Block a domain**: The wizard prepopulates external domains from the participants and senders in the chat.
    - **Block a user**: The wizard prepopulates the external sender.
    - **Submit to Microsoft for review**: The available reasons depend on the message verdict:
        - If the message has a threat verdict, **I've confirmed it's clean** and **It appears clean** are available. The suspicious and threat reasons are unavailable.
        - If the message doesn't have a threat verdict, **It appears suspicious** and **I've confirmed it's a threat** are available. The clean reasons are unavailable.
        - If you select **I've confirmed it's a threat**, select **Spam**, **Phish**, or **Malware** as the verdict.

    To make all submission reasons available, select **Show all response actions**.

    You can select multiple actions. For example, submit the message to Microsoft and block a sender or domain. You can also remove users when **Remove user from conversation** is available.

    [![Screenshot of the Take action wizard with options to block a domain or user and submit a Teams message to Microsoft.](media/teams-message-entity-panel-choose-response-actions.png)](media/teams-message-entity-panel-choose-response-actions.png#lightbox)

    When you select **Block a domain** or **Block a user**, the **Select entities to block** flyout opens:

    - Review the domains or sender that the wizard prepopulated for the message.
    - To add domains that aren't listed, enter up to 20 domains separated by commas or line breaks. Select **Block** to add the domains to the **Entity** list.
    - Use **Search** to find an entity in the list.
    - Select the entities to block, and then select **Add to block rule**. **Add to block rule** is unavailable until you select at least one entity.

    The following screenshot shows the empty entity list, where you can enter domains to add to the block rule.

    [![Screenshot of the Select entities to block flyout with an empty entity list and controls to enter and search for domains.](media/teams-message-entity-panel-select-entities-to-block.png)](media/teams-message-entity-panel-select-entities-to-block.png#lightbox)

    When you're finished on the **Choose response actions** page, select **Next**.
3. On the **Choose target entities** page, configure the following options:

    - **Name**: Enter a unique, descriptive name for the response actions.
    - **Description**: Enter optional details.

    Select the prepopulated senders and domains to add to the Tenant Allow/Block List. Review the impacted assets, actions, and target entities, and then select **Next**.

    [![Screenshot of the Choose target entities page with placeholders for the external domain, sender, and Teams message.](media/teams-message-entity-panel-block-target-entities.png)](media/teams-message-entity-panel-block-target-entities.png#lightbox)
4. On the **Review and submit** page, review your selections. To make changes, select **Back**. To complete the actions, select **Submit**.

After you submit the actions, the wizard displays the results:

- Results for **Block a domain** show the domain in the **Entity** column and **Domain** in the **Type** column. The **Status** value is **Blocked**, **Allowed**, or **No action**. If the domain is already blocked in the Tenant Allow/Block List, the results show the existing state.
- Results for sender and submission actions include the **Impacted asset**, **Action**, **Target entity**, **Expires on**, **Scope**, and **Status** columns. The target entity is the Teams message ID. The scope is **MDO Teams Protection** (**Microsoft Defender for Office 365 Teams Protection**).

Blocked domains and senders appear on the Tenant Allow/Block List page. Submitting a message to Microsoft and blocking a domain or sender create audit log entries. **Remove user from conversation** also creates an Action center entry and an audit log entry.

For details about Teams submissions, see [User reported message settings in Teams](submissions-teams) and [Report Teams messages to Microsoft](submissions-admin#report-teams-messages-to-microsoft-in-defender-for-office-365-plan-2).

To manage blocked domains, see [Block domains in Microsoft Teams using the Tenant Allow/Block List](tenant-allow-block-list-teams-domains-configure).