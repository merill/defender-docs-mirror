---
layout: Conceptual
title: Configure Junk Email Settings on Exchange Online Mailboxes - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/configure-junk-email-settings-on-exo-mailboxes
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
- tier2
description: Admins can learn how to configure the junk email settings in Exchange Online mailboxes. Many of these settings are available to users in Outlook or Outlook on the web.
ms.service: defender-office-365
ms.date: 2026-08-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 8b4c46b5-fc6d-46c1-a06c-a149b1c8944c
document_version_independent_id: 8b4c46b5-fc6d-46c1-a06c-a149b1c8944c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/configure-junk-email-settings-on-exo-mailboxes.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-junk-email-settings-on-exo-mailboxes
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/configure-junk-email-settings-on-exo-mailboxes.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 51ab43d6-e34e-2f15-9fd8-9f6f8aa34c3d
---

# Configure Junk Email Settings on Exchange Online Mailboxes - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

All Microsoft 365 organizations with cloud mailboxes include anti-spam protection. For more information, see [Anti-spam protection](anti-spam-protection-about).

But, there are also specific anti-spam settings that admins can configure on individual mailboxes in Exchange Online:

- **Deliver messages to the Junk Email folder based on anti-spam policies**: When an anti-spam policy is configured with the action **Move message to Junk Email folder** for a spam filtering verdict, the message is delivered to the mailbox's Junk Email folder. For more information about spam filtering verdicts in anti-spam policies, see [Configure anti-spam policies](anti-spam-policies-configure). Similarly, if zero-hour auto purge (ZAP) determines that a delivered message is spam or phishing, the message is moved to the Junk Email folder for **Move message to Junk Email folder** spam filtering verdict actions. For more information about ZAP, see [Zero-hour auto purge (ZAP) in Exchange Online](zero-hour-auto-purge).
- **Junk email settings that users configure for themselves in Outlook or Outlook on the web**: The *safelist collection* is the Safe Senders list, the Safe Recipients list, and the Blocked Senders list on each mailbox. The entries in these lists determine whether the message is delivered to the Inbox or the Junk Email folder. Users can configure the safelist collection for their own mailboxes in Outlook or Outlook on the web (formerly known as Outlook Web App or OWA). Admins can configure the safelist collection on any user's mailbox.

Microsoft 365 adds the header `X-Forefront-Antispam-Report: SFV:BLK` to incoming messages from senders in a user's Blocked Senders list, and any future messages from that sender are classified as spam. The message is delivered to the user's Junk Email folder or to quarantine based on the action configured in the applicable anti-spam policy (our [recommended anti-spam policy setting](recommended-settings-for-eop-and-office365#anti-spam-policy-settings) is **Move message to Junk Email folder**).

If the sender is in the user's Safe Senders list, the message is delivered to their Inbox.

Admins can use Exchange Online PowerShell to configure entries in the safelist collection on mailboxes (the Safe Senders list, the Safe Recipients list, and the Blocked Senders list).

Note

Entries in user Safe Senders lists are inputs to spam filtering, but don't determine the final verdict. Malware, high confidence phishing, and other detections take precedence. For more information, see [Secure by default in Office 365](secure-by-default).

To prevent users from adding entries to their Safe Senders lists, use [Group Policy](/en-us/microsoft-365-apps/outlook/email-security/deploy-junk-email-settings) to configure client-side Junk Email Filter settings in Outlook.

Microsoft 365 uses a mail flow delivery agent to route messages to the Junk Email folder. It doesn't use the junk email rule in the mailbox. The *Enabled* parameter on the **Set-MailboxJunkEmailConfiguration** cmdlet in Exchange Online PowerShell has no effect on mail flow in cloud mailboxes. Microsoft 365 routes messages based on the actions set in anti-spam policies. The user's Safe Senders list and Blocked Senders list continue to work as usual.

## Prerequisites

- You can only use Exchange Online PowerShell to do the procedures in this article. To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- You need to be assigned permissions in Exchange Online before you can do the procedures in this article. Specifically, you need the **Mail Recipients** role (which is assigned to the **Organization Management**, **Recipient Management**, and **Custom Mail Recipients** role groups by default) or the **User Options** role (which is assigned to the **Organization Management** and **Help Desk** role groups by default). To add users to role groups in Exchange Online, see [Modify role groups in Exchange Online](/en-us/Exchange/permissions-exo/role-groups#modify-role-groups). Users with default permissions can do these same procedures on their own mailboxes, as long as they have [access to Exchange Online PowerShell](/en-us/powershell/exchange/disable-access-to-exchange-online-powershell).
- In hybrid environments where the built-in security features for cloud mailboxes protect on-premises Exchange mailboxes, you need to configure Exchange mail flow rules (transport rules) in your on-premises Exchange organization to recognize the spam filtering verdicts from the cloud. For details, see [Deliver cloud-detected spam to the Junk Email folder in on-premises mailboxes](/en-us/exchange/standalone-eop/configure-eop-spam-protection-hybrid).

    After you manually create the rule in Microsoft 365 to match the rule in on-premises Exchange, the rule replicates in hybrid environments.
- By design, safe senders for shared mailboxes aren't synchronized to Microsoft Entra ID or Microsoft 365.

## Use Exchange Online PowerShell to configure the safelist collection on a mailbox

A mailbox's *safelist collection* consists of the Safe Senders list, the Safe Recipients list, and the Blocked Senders list. By default, users can configure the safelist collection on their own mailboxes in Outlook or Outlook on the web. Admins can use the corresponding parameters on the **Set-MailboxJunkEmailConfiguration** cmdlet to configure the safelist collection on a user's mailbox. The following table maps each **Set-MailboxJunkEmailConfiguration** parameter to the corresponding junk email setting in Outlook and Outlook on the web.

| Parameter on`Set-MailboxJunkEmailConfiguration` | Junk Email Options in Outlook | Junk email settings in Outlook on the web |
| --- | --- | --- |
| *BlockedSendersAndDomains* | **Blocked Senders** tab | **Blocked Senders and domains** section |
| *ContactsTrusted* | **Safe Senders** tab &gt; **Also trust email from my Contacts** | **Filters** sections &gt; **Trust email from my contacts** |
| *TrustedListsOnly* | **Options** tab &gt; **Safe Lists Only: Only mail from people or domains on your Safe Senders List or Safe Recipients List will be delivered to your Inbox** | **Filters** section &gt; **Only trust email from addresses in my Safe senders and domains list and Safe mailing lists** |
| *TrustedSendersAndDomains*^\*^ | **Safe Senders** tab | **Safe senders and domains** section |

^\*^ You can't directly modify the **Safe Recipients** list by using the **Set-MailboxJunkEmailConfiguration** cmdlet (the *TrustedRecipientsAndDomains* parameter doesn't work). You modify the Safe Senders list, and those changes are synchronized to the Safe Recipients list.

- In Exchange Online, whether entries in the Safe Senders list or *TrustedSendersAndDomains*parameter work or don't work depends on the verdict and action in the policy that identified the message:
    - **Move messages to Junk Email folder**: Domain entries and sender email address entries are honored. Messages from those senders aren't moved to the Junk Email folder.
    - **Quarantine**: Domain entries aren't honored (messages from those senders are quarantined). Email address entries are honored (messages from those senders aren't quarantined) if either of the following statements is true:
        - The message isn't identified as malware or high confidence phishing (malware and high confidence phishing messages are quarantined).
        - The email address, URL, or file in the email message isn't in a block entry in the [Tenant Allow/Block](tenant-allow-block-list-about#block-entries-in-the-tenant-allowblock-list).
- With directory synchronization, domain entries aren't synchronized by default, but you can enable synchronization for domains. For more information, see [Configure content filtering to use safe domain data](/en-us/exchange/configure-content-filtering-to-use-safe-domain-data-exchange-2013-help).

To configure the safelist collection on a mailbox, use the following syntax:

```powershell
Set-MailboxJunkEmailConfiguration <MailboxIdentity> -BlockedSendersAndDomains <EmailAddressesOrDomains | $null> -ContactsTrusted <$true | $false> -TrustedListsOnly <$true | $false> -TrustedSendersAndDomains  <EmailAddresses | $null>
```

To enter multiple values and overwrite any existing entries for the *BlockedSendersAndDomains* and *TrustedSendersAndDomains* parameters, use the following syntax: `"<Value1>","<Value2>"...`. To add or remove one or more values without affecting other existing entries, use the following syntax: `@{Add="<Value1>","<Value2>"... ; Remove="<Value3>","<Value4>...}`

The following example configures the following settings for the safelist collection on Ori Epstein's mailbox:

- Add the value `shopping@fabrikam.com` to the Blocked Senders list.
- Remove the value `chris@fourthcoffee.com` from the Safe Senders list and the Safe Recipients list.
- Configure contacts in the Contacts folder to be treated as trusted senders.

```powershell
Set-MailboxJunkEmailConfiguration "Ori Epstein" -BlockedSendersAndDomains @{Add="shopping@fabrikam.com"} -TrustedSendersAndDomains @{Remove="chris@fourthcoffee.com"} -ContactsTrusted $true
```

To remove a blocked domain from the Blocked Senders list of every user mailbox in the organization, run the following bulk update command:

```powershell
$All = Get-Mailbox -RecipientTypeDetails UserMailbox -ResultSize Unlimited; $All | foreach {Set-MailboxJunkEmailConfiguration $_.Name -BlockedSendersAndDomains @{Remove="contoso.com"}}
```

For detailed syntax and parameter information, see [Set-MailboxJunkEmailConfiguration](/en-us/powershell/module/exchangepowershell/set-mailboxjunkemailconfiguration).

Note

The Outlook Junk Email Filter has more safelist collection settings (for example, **Automatically add people I email to the Safe Senders list**). For more information, see [Use Junk Email Filters to control which messages you see](https://support.microsoft.com/office/274ae301-5db2-4aad-be21-25413cede077).

### How do you know you successfully configured the safelist collection on a mailbox?

To verify you successfully configured the safelist collection on a mailbox, use any of the following procedures:

- Replace &lt;MailboxIdentity&gt; with the name, alias, or email address of the mailbox, and run the following command to verify the property values:

    ```PowerShell
    Get-MailboxJunkEmailConfiguration -Identity "<MailboxIdentity>" | Format-List trusted*,contacts*,blocked*
    ```

    If the list of values is too long, use this syntax:

    ```PowerShell
    (Get-MailboxJunkEmailConfiguration -Identity <MailboxIdentity>).BlockedSendersAndDomains
    ```

## About Outlook junk email settings

To enable, disable, and configure the client-side Junk Email Filter settings that are available in Outlook, use [Group Policy](/en-us/microsoft-365-apps/outlook/email-security/deploy-junk-email-settings). For more information, see [Administrative Template files (ADMX/ADML) and Office Customization Tool for Microsoft 365 Apps for enterprise, Office 2019, and Office 2016](https://www.microsoft.com/download/details.aspx?id=49030).

When the Outlook Junk Email Filter is set to the default value **No automatic filtering** in **Home** &gt; **Junk** &gt; **Junk E-Mail Options** &gt; **Options**, Outlook doesn't attempt to classify messages as spam, but still uses the safelist collection (the Safe Senders list, the Safe Recipients list, and the Blocked Senders list) to move messages to the Junk Email folder after delivery. For more information about these settings, see [Overview of the Junk Email Filter](https://support.microsoft.com/office/5ae3ea8e-cf41-4fa0-b02a-3b96e21de089).

Note

In Microsoft 365 organizations, we recommend that you leave the Junk Email Filter in Outlook set to **No automatic filtering** to prevent unnecessary conflicts (both positive and negative) with the spam filtering verdicts from Microsoft 365.

When the Outlook Junk Email Filter is set to **Low** or **High**, the Outlook Junk Email Filter uses its own SmartScreen filter technology to identify and move spam to the Junk Email folder. This spam classification is separate from the spam filtering verdict from Microsoft 365. For more information about these settings, see [Change the level of protection in the Junk Email Filter](https://support.microsoft.com/Outlook/change-the-level-of-protection-in-the-junk-email-filter-in-outlook).

Outlook and Outlook on the web both support the safelist collection. The safelist collection is saved in the Exchange Online mailbox so that the changes to the safelist collection in Outlook appear in Outlook on the web, and vice-versa.

## Limits for junk email settings

The safelist collection (the Safe Senders list, the Safe Recipients list, and the Blocked Senders list) stored in the user's mailbox is also synchronized to Microsoft 365. With directory synchronization, the safelist collection is synchronized to Microsoft Entra ID.

- The safelist collection in the user's mailbox has a limit of 510 KB, which includes all lists, plus other junk email filter settings. If a user exceeds this limit, they receive an Outlook error that looks like the following message:

> 
> Cannot/Unable add to the server Junk E-mail lists. You are over the size allowed on the server. The Junk E-mail filter on the server is disabled until your Junk E-mail lists have been reduced to the size allowed by the server.

    For more information about this limit and how to change it, see [Junk email filter size limit in Exchange Online (KB2669081)](https://support.microsoft.com/help/2669081).
- The synchronized safelist collection in Microsoft 365 has the following synchronization limits:

    - 65,535 total entries in the Blocked Senders list and the Blocked Domains list.

        Note

        Only the first 500 blocked sender entries have their hashes synced to Microsoft Entra ID. These 500 synced entries determine whether messages from blocked senders receive a **User Block** verdict:

        - **Blocked senders in the first 500 entries** (hashes synced): Messages are quarantined with a **User Block** verdict. These quarantined messages have the following characteristics:

            - The messages are hidden when the **Don't show blocked senders** filter is active in quarantine.
            - Quarantine notifications aren't sent for these messages.
            - The **Sender address override reason** property has the value **Message sender is blocked by recipient settings**.
        - **Blocked senders beyond the first 500 entries** (hashes not synced): Messages don't receive a **User Block** verdict. If the messages are quarantined, they have the following characteristics:

            - The messages are visible, even if the **Don't show blocked senders** filter is active in quarantine.
            - Quarantine notifications are sent for these messages.
            - The **Sender address override reason** property has the value **None**.

            Messages from these senders that aren't otherwise detected as malicious are delivered to the Junk Email folder instead of quarantine.

        In other words, two nearly identical spam messages from two different blocked senders could have different behavior in quarantine, or one message might not even be quarantined at all.
    - 1,024 total entries in the Safe Senders list, the Safe Recipients list, and external contacts if **Trust email from my contacts** is enabled.

        - When the 1,024 entry limit is reached, the following things happen:
            - The list stops accepting entries in PowerShell and Outlook on the web, but no error is displayed.

                Outlook users can continue to add more than 1,024 entries until they reach the Outlook limit of 510 KB. Outlook can use these extra entries, as long as a Microsoft 365 filter doesn't block the message before delivery to the mailbox (mail flow rules, anti-spoofing, and so on).
        - With directory synchronization, the entries are synchronized to Microsoft Entra ID in the following order:
            1. Mail contacts if **Trust email from my contacts** is enabled.
            2. The Safe Senders list and the Safe Recipient list are combined, deduplicated, and sorted alphabetically whenever a change is made for the first 1,024 entries.
        - The first 1,024 entries are used, and relevant information is stamped in the message headers.
        - For remaining entries over 1,024, Outlook processes unsynchronized entries, but no information is stamped in the message headers. This behavior doesn't occur in Outlook on the web.
        - Enabling the **Trust email from my contacts**setting reduces the number of Safe Senders and Safe Recipients that can be synchronized. If this reduction is a concern, we recommend using Group Policy to turn off this feature:
            - File name: outlk16.opax
            - Policy setting: **Trust e-mail from contacts**

Important

The following button helps identify and resolve issues with the safelist collection in user mailboxes (the Safe Senders list and Blocked Senders list) which includes individual senders and domains: