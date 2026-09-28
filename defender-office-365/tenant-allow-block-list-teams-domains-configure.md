---
layout: Conceptual
title: Block domains and addresses in Microsoft Teams using the Tenant Allow/Block List - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/tenant-allow-block-list-teams-domains-configure
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
description: Admins can learn how to block domains and addresses in Microsoft Teams using the Tenant Allow/Block List.
ms.service: defender-office-365
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: sfi-ga-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 4112269a-1faa-b089-d2a2-0133a0cc0052
document_version_independent_id: 4112269a-1faa-b089-d2a2-0133a0cc0052
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/tenant-allow-block-list-teams-domains-configure.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: tenant-allow-block-list-teams-domains-configure
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/tenant-allow-block-list-teams-domains-configure.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 8d74f005-b54f-ec68-2779-95bbbc3b2086
---

# Block domains and addresses in Microsoft Teams using the Tenant Allow/Block List - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

In all organizations with Microsoft Teams and cloud mailboxes, admins can create and manage block entries for domains and email addresses in Microsoft Teams using the Tenant Allow/Block List.

These entries also appear on the **Organization settings** tab of the **External access** page in the Microsoft Teams admin center at https://admin.teams.microsoft.com/company-wide-settings/external-communications:

- **Blocked domains**: Entries are in the **Allow or block external domains** section:

    [![Screenshot of the External access page in the Microsoft Teams admin center showing blocked domains.](media/tenant-allow-block-list-teams-domains.png)](media/tenant-allow-block-list-teams-domains.png#lightbox)
- **Blocked email addresses**: Entries are in the **Block specific users from communicating with people in my organization** section:

    [![Screenshot of the External access page in the Microsoft Teams admin center showing blocked users.](media/tenant-allow-block-list-teams-senders.png)](media/tenant-allow-block-list-teams-senders.png#lightbox)

For more information about the Tenant Allow/Block List, see [Manage allows and blocks in the Tenant Allow/Block List](tenant-allow-block-list-about).

The following guidance explains how security admins can manage blocked domain and sender entries for Teams in the Microsoft Defender portal. These entries also appear in the Microsoft Teams admin center. Before you begin, review the required permissions and settings in What do you need to know before you begin?.

## What do you need to know before you begin?

Review the following requirements and considerations before you create or manage block entries for Teams senders.

- You open the Microsoft Defender portal at https://security.microsoft.com. To go directly to the **Tenant Allow/Block Lists** page, use https://security.microsoft.com/tenantAllowBlockList. Then, go to the **Teams senders** tab.
- Before adding a block entry, check the [Microsoft Teams external domain anomalies report](/en-us/microsoftteams/teams-analytics-and-reports/external-domain-anomalies-report) to identify suspicious external domains that might need to be blocked.
- After you add the block entry for the domain or sender address in Teams, all new Teams communication from that organization is blocked. Block communication includes new Teams meetings, chats, channels, and calls.
- On the **Organization settings** tab of the **External access** page in the Microsoft Teams admin center at https://admin.teams.microsoft.com/company-wide-settings/external-communications, the following settings are required to create and manage block entries for domains and senders in Teams using the Tenant Allow/Block List:

    - **Teams and Skype for Business users in external organizations** must be **Allow all external domains** or **Block only specific external domains**.
    - **Allow my security team to manage blocked domains** must be ![](media/scc-toggle-on.png)**On**.
    - **Block specific users from communicating with people in my organization**![](media/scc-toggle-on.png)**On**.
- The maximum number of domain block entries for Microsoft Teams is 4,000.
- The maximum number of users block entries for Microsoft Teams is 200.
- Block entries for domains and senders in Teams never expire.
- A blocked domain or sender entry in Teams should be active within 24 hours.
- You need to be assigned permissions before you can do the procedures in this article. You have the following options:

    - [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): Membership in these roles gives users the required permissions and\_ permissions for other features in Microsoft 365:

        - *Add, modify, and delete entries*: Membership in the **Global Administrator**^\*^, **Teams Administrator**, **Security Administrator**, or **Security Operator** roles.
        - *Read-only access to entries*: **Global Reader** or **Security Reader** roles.

        Important

        ^\*^ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.

## Create block entries for domains and addresses in Teams in the Tenant Allow/Block List

Tip

See the requirements in the What do you need to know before you begin? section to managed blocked domains and senders in Teams in the Tenant Allow/Block list. If you don't meet the prerequisites, you get errors adding domains or senders on **Teams senders** tab of the **Tenant Allow/Block Lists** page.

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Policies & rules** &gt; **Threat policies** &gt; **Rules** section &gt; **Tenant Allow/Block Lists**. Or, to go directly to the **Tenant Allow/Block Lists** page, use https://security.microsoft.com/tenantAllowBlockList.
2. On the **Tenant Allow/Block Lists** page, select the **Teams senders** tab.
3. On the **Teams senders** tab, select ![](media/defender-portal-icon-create.png)**Block**.
4. In the **Block sender domains & addresses on Teams** flyout that opens, enter up to 20 domains separated by commas or line breaks, and then select **Add**.

    Back on the **Teams senders** tab, the domain and addresses block entries are listed. After a few minutes, the blocked domains and addresses also appear on the **Organization settings** tab of the **External access** page in the Microsoft Teams admin center at https://admin.teams.microsoft.com/company-wide-settings/external-communications.

## View block entries for domains and addresses in Teams in the Tenant Allow/Block List

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Policies & rules** &gt; **Threat policies** &gt; **Tenant Allow/Block Lists** in the **Rules** section. Or, to go directly to the **Tenant Allow/Block Lists** page, use https://security.microsoft.com/tenantAllowBlockList.
2. Select the **Teams senders** tab.
3. On the **Teams senders** tab, you can sort the entries by clicking on an available column header. The following columns are available:

    - **Value**: The domain or email address.
4. Use the ![](media/defender-portal-icon-search.png)**Search** box and a corresponding value to find specific entries.

### Remove block entries for domains and addresses in Teams in the Tenant Allow/Block List

Use the following steps to remove blocked domain or sender address entries from the Teams senders list.

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Policies & rules** &gt; **Threat policies** &gt; **Rules** section &gt; **Tenant Allow/Block Lists**. You can also go directly to the **Tenant Allow/Block Lists** page via https://security.microsoft.com/tenantAllowBlockList.
2. On the **Tenant Allow/Block Lists** page, select the **Teams senders** tab.
3. On **Teams senders** tab, select the entry from the list by selecting the check box next to the first column, and then select the ![](media/defender-portal-icon-delete.png)**Delete** action that appears.

    Tip

    You can select multiple entries by selecting each check box, or select all entries by selecting the check box next to the **Value** column header.
4. Warning

    Deleting entries removes the blocked domains or addresses from the Teams senders list. The change also propagates to Teams external access settings after a few minutes.

    In the warning dialog that opens, select **Delete**.

    Back on the **Teams senders** tab, the entry is no longer listed. After a few minutes, the blocked domain and addresses disappears from the **Organization settings** tab of the **External access** page in the Microsoft Teams admin center at https://admin.teams.microsoft.com/company-wide-settings/external-communications.