---
layout: Conceptual
title: Bulk senders insight - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/anti-spam-bulk-senders-insight
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: article
ms.localizationpriority: medium
ms.assetid: 
ms.collection:
- m365-security
- tier2
description: Admins can learn about the Bulk senders insight page in the Microsoft Defender portal to simulate the effect of the bulk complaint level (BCL) on allowed or blocked messages.
ms.service: defender-office-365
ms.date: 2025-07-03T00:00:00.0000000Z
ms.custom: sfi-ga-nochange
locale: en-us
document_id: 6167011a-0192-642d-dce5-1a6b7ee184ff
document_version_independent_id: 6167011a-0192-642d-dce5-1a6b7ee184ff
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/anti-spam-bulk-senders-insight.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: anti-spam-bulk-senders-insight
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/anti-spam-bulk-senders-insight.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: f9f2d5c0-cb60-c41f-825b-8607dd8f769e
---

# Bulk senders insight - Microsoft Defender for Office 365 | Microsoft Learn

In all organizations with cloud mailboxes, the bulk senders insight in the Microsoft Defender portal allows you to view information about bulk email (also known as gray mail) detections in your organization.

Microsoft 365 assigns a bulk complaint level (BCL) value to inbound messages from bulk senders. A higher BCL value indicates a bulk message is more likely to be spam. The bulk email threshold in anti-spam policies uses a specified BCL threshold value to identify messages a bulk and take action on them. For more information about the BCL, see [Bulk complaint level (BCL)](anti-spam-bulk-complaint-level-bcl-about).

The bulk senders insight has the following capabilities:

- View how much mail is identified as bulk at every BCL level (1 to 9) for the last 60 days.
- Simulate changes to the bulk email threshold in anti-spam policies. The results show the number of messages that would be delivered vs. identified as bulk.

    Tip

    You can modify the BCL threshold in the default anti-spam policy and custom anti-spam policies. You can't modify the BCL threshold in the Standard or Strict [preset security policies](preset-security-policies).
- View information about message senders affected by the bulk email threshold, including filtering based on the quality of the sender.

This article describes how to use the bulk senders insight in the Microsoft Defender portal.

## What do you need to know before you begin?

- You open the Microsoft Defender portal at https://security.microsoft.com. To go directly to the **Bulk senders insight** page, use https://security.microsoft.com/senderinsights.
- Bulk simulation and detection might not work correctly if the MX record for your Microsoft 365 domain points to a non-Microsoft service or device.
- You need to be assigned permissions before you can do the procedures in this article. You have the following options:

    - [Microsoft Defender XDR Unified role based access control (RBAC)](/en-us/defender-xdr/manage-rbac) (If **Email & collaboration** &gt; **Defender for Office 365** permissions is ![](media/scc-toggle-on.png)**Active**. Affects the Defender portal only, not PowerShell): **Authorization and settings/Security settings/Core Security settings (manage)** or **Authorization and settings/Security settings/Core Security settings (read)**.
    - [Exchange Online permissions](/en-us/exchange/permissions-exo/permissions-exo):

        - *Add, modify, and delete policies*: Membership in the **Organization Management** or **Security Administrator** role groups.
        - *Read-only access to policies*: Membership in the **Global Reader**, **Security Reader**, or **View-Only Organization Management** role groups.
    - [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): Membership in the following roles gives users the required permissions *and* permissions for other features in Microsoft 365:

        - *Add, modify, and delete policies*: Membership in the **Organization Management**^\*^ or **Security Administrator** roles.
        - *Read-only access to policies*: Membership in the **Global Reader** or **Security Reader** roles.

        Important

        ^\*^ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.
- For our recommended settings for anti-spam policies, see [Anti-spam policy settings](recommended-settings-for-eop-and-office365#anti-spam-policy-settings).

Tip

Settings in the default or custom anti-spam policies are ignored if a recipient is also included in the [Standard or Strict preset security policies](preset-security-policies). For more information, see [Order and precedence of email protection](how-policies-and-protections-are-combined).

The **Bulk threshold** value in an anti-spam policy determines the BCL threshold that's used to identify a message as bulk. For example, the **Bulk threshold** value 7 means that messages with the BCL value 7, 8, or 9 are identified as bulk. What happens to bulk messages is determined by the **Bulk complaint level (BCL) met or exceeded** action in the anti-spam policy (for example, **Move message to Junk Email folder**, **Quarantine**, or **Delete message**). For simplicity, identifying a message as bulk and taking action on the message is called **blocked** in the bulk senders insight.

## Open the bulk senders insight in the Microsoft Defender portal

The bulk senders insight is available in the following locations:

- In the properties of the default anti-spam policy or custom anti-spam policies:

    1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Policies & rules** &gt; **Threat policies** &gt; **Anti-spam** in the **Policies** section. Or, to go directly to the **Anti-spam policies** page, use https://security.microsoft.com/antispam.
    2. On the **Anti-spam policies** page, select a custom anti-spam policy (the **Type** value is **Custom anti-spam policy**) or the default anti-spam policy named **Anti-spam inbound policy (Default)** by clicking anywhere in the row other than the check box next to the first column.
    3. In the details flyout that opens, select **Edit spam threshold and properties** at the bottom of the **Bulk email threshold & spam properties** section.
    4. In the **Spam threshold and properties** flyout that opens, the bulk senders insight contains the following information about all bulk email detected by all anti-spam policies in the organization for the last 60 days:

        - By default, the insight shows the number of messages that were delivered and identified as bulk at the current BCL threshold of the anti-spam policy.

            [![The bulk senders insight in the properties of the default anti-spam policy with the default BCL threshold value.](media/anti-spam-policy-bulk-senders-insight-bcl-default.png)](media/anti-spam-policy-bulk-senders-insight-bcl-default.png#lightbox)
        - Decreasing the bulk email threshold value shows:

            - How many fewer messages would be delivered.
            - How many more messages would be identified as bulk.
            - How many bulk message identifications are likely to be false positives (good email identified as bad).

            [![The bulk senders insight in the properties of the default anti-spam policy with BCL threshold lower than the original value.](media/anti-spam-policy-bulk-senders-insight-bcl-lower.png)](media/anti-spam-policy-bulk-senders-insight-bcl-lower.png#lightbox)
        - Increasing the bulk email threshold value shows:

            - How many more messages would be delivered.
            - How many fewer messages would be identified as bulk.
            - How many bulk message identifications are likely to be false negatives (bad email delivered).

            [![The bulk senders insight in the properties of the default anti-spam policy with BCL threshold higher than the original value.](media/anti-spam-policy-bulk-senders-insight-bcl-higher.png)](media/anti-spam-policy-bulk-senders-insight-bcl-higher.png#lightbox)
- On the **Email & collaboration reports and insights** page:

    1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Reports** &gt; **Email & collaboration** section &gt; **Email & collaboration reports and insights**. Or, to go directly to the **Email & collaboration reports and insights** page, use https://security.microsoft.com/emailandcollabreport.
    2. On the **Email & collaboration reports and insights** page, go to the **Email & collaboration insights** section and find the **Bulk senders insight**.

    [![The bulk senders insight on the Email &amp; collaboration reports and insights page in the Microsoft Defender portal.](media/insights-page-bulk-senders-insight.png)](media/insights-page-bulk-senders-insight.png#lightbox)

To view detailed information about bulk detections and senders, select **View bulk senders insight** or **View details** to open the **Bulk senders insight** page.

## View the Bulk senders insight page

The **Bulk senders insight** page is available using the following methods:

- Directly at https://security.microsoft.com/senderinsights.
- When you select **View bulk senders insight** from the **Spam threshold and properties** flyout in the details of a custom anti-spam policy or the default anti-spam policy from the **Anti-spam policies** page at https://security.microsoft.com/antispam.
- When you select **View details** from the **Bulk senders insight** card on the **Email & collaboration reports and insights** page at https://security.microsoft.com/emailandcollabreport.

[![The Bulk senders insight page in the Microsoft Defender portal.](media/anti-spam-policy-bulk-senders-insight-page.png)](media/anti-spam-policy-bulk-senders-insight-page.png#lightbox)

Before you run a simulation, values in the table in the middle of the page indicate the following values:

- **Bulk complaint level (BCL)**: The range of possible BCL values (1 to 9).
- **All email**: The total number of messages that were identified at each BCL value (some of which might be 0).
- **Delivered at current BCL threshold**: The number of messages that were delivered (not identified as bulk) for each BCL value:
    - If the BCL value is less that the **Current bulk email threshold**value, the message was delivered (wasn't identified as bulk):
        - The **Delivered at current BCL threshold** and **All email** values are the same.
        - The **Delivered at current BCL threshold** value matches the **Email delivered at current config** value.
    - If the BCL value is greater than or equal to the **Current bulk email threshold**value, the message was identified as bulk and blocked.
        - The **Delivered at current BCL threshold** value for the BCL value is 0.
        - The **All email** value matches the **Email identified at current BCL threshold** value.
- **Delivered at new BCL threshold**: The number of messages that weren't identified as bulk email **after** you run a simulation. Before you run a simulation, the value is meaningless.

To run a simulation, use the following elements on the page:

- The unmodifiable **Current bulk email threshold** slider shows the current BCL threshold value based on how you got to the **Bulk senders insight**page:
    - **Directly**: The BCL threshold value is 7.
    - **From the properties of an anti-spam policy**: The BCL threshold value is the current value in the anti-spam policy.
- The **New bulk email threshold** slider allows you to simulate the effect of increasing and decreasing the BCL threshold on delivered or blocked messages.
- The **Simulation sender quality threshold** slider specifies a good/bad sender trustworthiness threshold to use in the BCL update simulation. A higher value indicates simulated BCL threshold results based on more reliable senders. The **Simulation sender quality threshold**value for senders is based on the following factors:
    - Past interactions with the sender.
    - Message frequency from the sender.
    - Admin or user feedback on messages from the sender.

After you select the **New bulk email threshold** and **Simulation sender quality threshold** values, select **Simulate**:

- The page is updated with the number of blocked vs. allowed messages for the current and new simulated BCL threshold levels.
- The bottom of the page is updated with information about senders that would be identified as bulk.

### View information about bulk senders on the Bulk senders insight page

The bulk sender details table at the bottom of the page contains data about bulk senders whose messages were identified as bulk.

The table might contain sender data when you first open the **Bulk senders insight** page if the **Current bulk email threshold** and **Simulation sender quality threshold** values already resulted in bulk email identification before you run any simulations.

Otherwise, senders are included in the sender details table based on the **Current bulk email threshold** and **Simulation sender quality threshold** values after you run a simulation.

For entries in the sender details table, the following columns are always available:

- **Sender**: The sender's email address.
- **BCL**
- **Simulation sender quality threshold**

The remaining columns in the sender details table depend on the relationship between the **Current bulk email threshold** and **New bulk email threshold** values after you run a simulation:

- **New bulk email threshold** equals **Current bulk email threshold**:

    - **Potential false positive**
    - **Potential false negative**

    To filter the results, select **All senders** and then select one of the following values:

    - **Potential false positive**: Only senders where **Potential false positive** is **True** are shown.
    - **Potential false negative**: Only senders where **Potential false negative** is **True** are shown.

    [![The Bulk senders insight page before you run a simulation or after you run a simulation where the new BCL threshold equals the current BCL threshold.](media/anti-spam-policy-bulk-senders-insight-page.png)](media/anti-spam-policy-bulk-senders-insight-page.png#lightbox)
- **New bulk email threshold** is less than **Current bulk email threshold**:

    - **New sender blocked**
    - **Potential false positive**

    To filter the results, select **All senders** and then select one of the following values:

    - **New sender blocked**: Only senders where **New sender blocked** is **True** are shown.
    - **Potential false positive**: Only senders where **Potential false positive** is **True** are shown.

    [![The Bulk senders insight page after you run a simulation where the new BCL threshold is less than the current BCL threshold.](media/anti-spam-policy-bulk-senders-insight-page-less-than-current.png)](media/anti-spam-policy-bulk-senders-insight-page-less-than-current.png#lightbox)
- **New bulk email threshold** is greater than **Current bulk email threshold**:

    - **New sender allowed**
    - **Potential false negative**

    To filter the results, select **All senders** and then select one of the following values:

    - **New sender allowed**: Only senders where **New sender allowed** is **True** are shown.
    - **Potential false negative**: Only senders where **Potential false negative** is **True** are shown.

    [![The Bulk senders insight page after you run a simulation where the new BCL threshold is greater than the current BCL threshold.](media/anti-spam-policy-bulk-senders-insight-page-greater-than-current.png)](media/anti-spam-policy-bulk-senders-insight-page-greater-than-current.png#lightbox)

To change the list of entries from normal to compact spacing, select ![](media/defender-portal-icon-standard.png)**Change list spacing to compact or normal**, and then select ![](media/defender-portal-icon-compact.png)**Compact list**.

Use the ![](media/defender-portal-icon-search.png)**Search** box and a corresponding value to find specific senders in the table.

Use ![](media/defender-portal-icon-download.png)**Export** to save the currently displayed list of senders to a CSV file. The default filename is Bulk sender insights - Microsoft Defender.csv, and the default location is the local Downloads folder. If an exported file already exists in that location, the filename is incremented (for example, Bulk sender insights - Microsoft Defender(1).csv).

### View detailed information about a bulk sender on the Bulk senders insight page

To view details about a specific sender from the sender details table at the bottom of the **Bulk senders insight** page, click anywhere in the row other than the check box next to the first column. The **Sender details** flyout that opens contains the following information about the sender:

- **Sender**: The sender's email address.
- **Messages**: The number of messages from the sender.
- **Messages in Inbox**: The number of messages from the sender that were delivered to user Inboxes.
- **Messages in quarantine or Junk Email**: The number of messages from the sender that were delivered to user Junk Email folders or quarantined.
- **Admin setting**: Whether the [Tenant Allow/Block List](tenant-allow-block-list-about)allowed or blocked the sender. Valid values are:
    - **Allow**: An allow entry exists for the message sender.
    - **Block**: A block entry exists for the message sender.
- **User allowed messages**: The number of messages from the sender where the sender is in the Safe Senders list in user mailboxes.
- **User blocked messages**: The number of messages from the sender where the sender is in the Blocked Senders list in user mailboxes.
- **False positive submissions**: The number of messages from the sender that were submitted as good mail accidentally blocked.
- **False negative submissions**: The number of messages from the sender that were submitted as bad mail accidentally delivered.
- **User moved from Junk Email to Inbox**
- **User moved from Inbox to Junk Email**
- **User deleted messages**
- **Admin quarantined messages**
- **Admin moved emails from Inbox to Junk Email**
- **Admin deleted messages**

[![The sender details flyout from the sender details table on the Bulk senders insight page.](media/anti-spam-policy-bulk-senders-insight-page-sender-details-flyout.png)](media/anti-spam-policy-bulk-senders-insight-page-sender-details-flyout.png#lightbox)