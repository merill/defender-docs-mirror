---
layout: Conceptual
title: Review and manage spoof intelligence insight in Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/anti-spoofing-spoof-intelligence
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
ms.assetid: 978c3173-3578-4286-aaf4-8a10951978bf
ms.collection:
- m365-security
- tier2
ms.custom:
- msecd-doc-authoring-1016
- seo-marvel-apr2020
- sfi-ga-nochange
description: Learn how to review and manage spoof intelligence in Microsoft 365 to identify legitimate spoofed senders and improve anti-spoofing protection.
ms.service: defender-office-365
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 7c412300-28c1-063d-1363-598fed1e2078
document_version_independent_id: 7c412300-28c1-063d-1363-598fed1e2078
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/anti-spoofing-spoof-intelligence.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: anti-spoofing-spoof-intelligence
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/anti-spoofing-spoof-intelligence.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 946b0a20-03dc-e187-1e3f-4e9dfdd0eff6
---

# Review and manage spoof intelligence insight in Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

In all organizations with cloud mailboxes, inbound email messages are automatically protected against spoofing. Microsoft 365 uses **spoof intelligence** as part of your organization's overall defense against phishing. For more information, see [Anti-spoofing protection](anti-phishing-protection-spoofing-about).

When a sender spoofs an email address, they appear to be a user in one of your organization's domains, or a user in an external domain that sends email to your organization. Attackers who spoof senders to send spam or phishing email need to be blocked. But there are scenarios where legitimate senders are spoofing. For example:

- Legitimate scenarios for spoofing internal domains:

    - Non-Microsoft senders use your domain to send bulk mail to users in your organization (for example, for company polls).
    - An external company generates and sends advertising or product updates on your behalf.
    - An assistant regularly needs to send email for another person within your organization.
    - An internal application sends email notifications.
- Legitimate scenarios for spoofing external domains:

    - The sender is on a mailing list (also known as a discussion list), and the mailing list relays email from the original sender to all the participants on the mailing list.
    - An external company sends email on behalf of another company (for example, an automated report or a software-as-a-service company).

Use the *spoof intelligence insight* in the Microsoft Defender portal to quickly identify and manually allow spoofed senders who legitimately send you email that doesn't pass [email authentication](email-authentication-about) (SPF, DKIM, or DMARC) checks.

By allowing known senders to send spoofed messages from known locations, you can reduce false positives (good email marked as bad). By monitoring the allowed spoofed senders, you provide an extra layer of security to prevent unsafe messages from arriving in your organization.

You can also use the spoof intelligence insight to review spoofed senders allowed by spoof intelligence and manually block specific allowed spoofed senders.

The following sections explain how to use the spoof intelligence insight in the Microsoft Defender portal and in PowerShell.

Note

- Only spoofed senders detected by spoof intelligence appear in this insight. Messages from domains that fail DMARC where the DMARC policy is set to `p=reject` or `p=quarantine` don't appear in this insight. Those messages are processed based on the **Honor DMARC record policy when the message is detected as spoof** setting in [anti-phishing policy spoof protection settings](anti-phishing-policies-about#spoof-protection-and-sender-dmarc-policies).
- When you override the allow or block verdict in the spoof intelligence insight, the spoofed sender becomes a manual allow or block entry that appears only on the **Spoofed senders** tab on the **Tenant Allow/Block Lists** page at https://security.microsoft.com/tenantAllowBlockList?viewid=SpoofItem. You can also manually create allow or block entries for spoofed senders before spoof intelligence detects them. For more information, see [Spoofed senders in the Tenant Allow/Block List](tenant-allow-block-list-email-spoof-configure#spoofed-senders-in-the-tenant-allowblock-list).
- The **Action** values **Allow** or **Block** in the spoof intelligence insight refer to spoof *detection* (whether Microsoft 365 identified the message as spoofed or not). The **Action** value doesn't necessarily affect the overall filtering of the message. For example, to avoid false positives, a spoofed message might be delivered if we find that it doesn't have malicious intent.
- The spoof intelligence insight shows seven days worth of data. In Exchange Online PowerShell, the **Get-SpoofIntelligenceInsight** cmdlet shows 30 days worth of data.

## What do you need to know before you begin?

- You open the Microsoft Defender portal at https://security.microsoft.com. To go directly to the **Spoofed senders** tab on the **Tenant Allow/Block Lists** page, use https://security.microsoft.com/tenantAllowBlockList?viewid=SpoofItem. To go directly to the **Spoof intelligence insight** page, use https://security.microsoft.com/spoofintelligence.
- To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- You need to be assigned permissions before you can do the procedures in this article. You have the following options:

    - [Microsoft Defender XDR Unified role based access control (RBAC)](/en-us/defender-xdr/manage-rbac) (If **Email & collaboration** &gt; **Defender for Office 365** permissions is ![](media/scc-toggle-on.png)**Active**. Affects the Defender portal only, not PowerShell): **Authorization and settings/Security settings/Core Security settings (manage)** or **Authorization and settings/Security settings/Core Security settings (read)**.
    - [Exchange Online permissions](/en-us/exchange/permissions-exo/permissions-exo):

        - *Allow or block spoofed senders or turn on or turn off spoof intelligence*: Membership in one of the following role groups:
            - **Organization Management**
            - **Security Administrator**and**View-Only Configuration** or **View-Only Organization Management**.
        - *Read-only access to the spoof intelligence insight*: Membership in the **Global Reader**, **Security Reader**, or **View-Only Organization Management** role groups.
    - [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): Membership in the **Global Administrator**^\*^, **Security Administrator**, **Global Reader**, or **Security Reader** roles gives users the required permissions *and* permissions for other features in Microsoft 365.

        Important

        ^\*^ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.
- For our recommended settings for anti-phishing policies, including spoof intelligence, see [Anti-phishing policy settings for all cloud mailboxes](recommended-settings-for-eop-and-office365#anti-phishing-policy-settings-for-all-cloud-mailboxes).
- You enable and disable spoof intelligence in anti-phishing policies. Spoof intelligence is enabled by default. For more information, see one of the following articles:

    - [Configure anti-phishing policies if you don't have Microsoft Defender for Office 365](anti-phishing-policies-eop-configure)
    - [Configure anti-phishing policies in Microsoft Defender for Office 365](anti-phishing-policies-mdo-configure)

## Find the spoof intelligence insight in the Microsoft Defender portal

### Open the spoof intelligence insight

To open the spoof intelligence insight in the Microsoft Defender portal, perform the following steps:

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Policies & rules** &gt; **Threat policies** &gt; **Tenant Allow/Block Lists** in the **Rules** section. Or, to go directly to the **Tenant Allow/Block Lists** page, use https://security.microsoft.com/tenantAllowBlockList.
2. Select the **Spoofed senders** tab.
3. On the **Spoofed senders** tab, the spoof intelligence insight appears as shown in the following image:

    ![The Spoof intelligence insight on the Anti-phishing policy page](media/m365-sc-spoof-intelligence-insight.png)

    The insight has two modes:

    - **Insight mode**: If spoof intelligence is enabled, the insight shows how many messages spoof intelligence detected during the past seven days.
    - **What if mode**: If spoof intelligence is disabled, the insight shows how many messages spoof intelligence *would have* detected during the past seven days.

To view information about the spoof intelligence detections, select **View spoofing activity** in the spoof intelligence insight to go to the **Spoof intelligence insight** page.

### View information about spoof detections

Note

Remember, only spoofed senders detected by spoof intelligence appear in this insight. Messages from domains that fail DMARC where the DMARC policy is set to `p=reject` or `p=quarantine` don't appear in this insight. Those messages are processed based on the **Honor DMARC record policy when the message is detected as spoof** setting in [anti-phishing policy spoof protection settings](anti-phishing-policies-about#spoof-protection-and-sender-dmarc-policies).

The **Spoof intelligence insight** page at https://security.microsoft.com/spoofintelligence is available when you select **View spoofing activity** from the spoof intelligence insight on the **Spoofed senders** tab on the **Tenant Allow/Block Lists** page.

On the **Spoof intelligence insight** page, you can sort the entries by clicking on an available column header. The following columns are available:

- **Spoofed user**: The **domain** of the spoofed user in the **From** box in email clients (also known as the `5322.From` address or P2 address).
- **Sending infrastructure**: Also known as the *infrastructure*. The sending infrastructure is one of the following values:
    - The domain found in a reverse DNS lookup (PTR record) of the source email server's IP address.
    - If the source IP address has no PTR record, then the sending infrastructure is identified as &lt;source IP&gt;/24 (for example, 192.168.100.100/24).
    - A verified DKIM domain.
- **Message count**: The number of messages from the combination of the spoofed domain *and* the sending infrastructure to your organization within the last seven days.
- **Last seen**: The last date when a message was received from the sending infrastructure that contains the spoofed domain.
- **Spoof type**: One of the following values:
    - **Internal**: The spoofed sender is in a domain that belongs to your organization (an [accepted domain](/en-us/exchange/mail-flow-best-practices/manage-accepted-domains/manage-accepted-domains)).
    - **External**: The spoofed sender is in an external domain.
- **Action**: This value is **Allowed** or **Blocked**:
    - **Allowed**: The domain failed explicit email authentication checks [SPF](email-authentication-spf-configure), [DKIM](email-authentication-dkim-configure), and [DMARC](email-authentication-dmarc-configure). However, the domain passed our implicit email authentication checks ([composite authentication](email-authentication-about#composite-authentication)). As a result, no anti-spoofing action was taken on the message.
    - **Blocked**: Messages from the spoofed domain *and* sending infrastructure are marked as bad by spoof intelligence. The action taken on spoofed messages with malicious intent is controlled by:

        - The [Standard or Strict preset security policies](preset-security-policies).
        - The default anti-phishing policy.
        - Custom anti-phishing policies.

        For more information, see [Configure anti-phishing policies in Microsoft Defender for Office 365](anti-phishing-policies-mdo-configure).

To change the list of spoofed senders from normal to compact spacing, select ![](media/defender-portal-icon-standard.png)**Change list spacing to compact or normal**, and then select ![](media/defender-portal-icon-compact.png)**Compact list**.

To filter the entries, select ![](media/defender-portal-icon-filter.png)**Filter**. The following filters are available in the **Filter** flyout that opens:

- **Spoof type**: The available values are **Internal** and **External**.
- **Action**: The available values are **Allow** and **Block**

When you're finished in the **Filter** flyout, select **Apply**. To clear the filters, select ![](media/defender-portal-icon-clear-filters.png)**Clear filters**.

Use the ![](media/defender-portal-icon-search.png)**Search** box and a corresponding value to find specific entries.

Use ![](media/defender-portal-icon-download.png)**Export** to export the list of spoof detections to a CSV file.

### View details about spoof detections

When you select a spoof detection from the list by clicking anywhere in the row other than the check box next to the first column, a details flyout opens that contains the following information:

- **Why did we catch this?** section: Why we detected this sender as spoof, and what you can do for further information.
- **Domain summary** section: Includes the same information from the main **Spoof intelligence insight** page.
- **WhoIs data** section: Technical information about the sender's domain.
- **Explorer investigation** section: In Defender for Office 365 organization, this section contains a link to open [Threat Explorer](threat-explorer-real-time-detections-about) to see more details about the sender on the **Phish** tab.
- **Similar Emails** section: Contains the following information about the spoof detection:

    - **Date**
    - **Subject**
    - **Recipient**
    - **Sender**
    - **Sender IP**

    Select **Customize columns** to remove the columns that are shown. When you're finished, select **Apply**.

Tip

To see details about other entries without leaving the details flyout, use ![](media/updownarrows.png)**Previous item** and **Next item** at the top of the flyout.

To change the spoof detection from **Allow** to **Block** or vice-versa, see Override the spoof intelligence verdict.

### Override the spoof intelligence verdict

Important

When you override the spoof intelligence verdict, the entry is removed from the **Spoof intelligence insight** page and added to the **Spoofed senders** tab on the **Tenant Allow/Block Lists** page at https://security.microsoft.com/tenantAllowBlockList?viewid=SpoofItem.

On the **Spoof intelligence insight** page at https://security.microsoft.com/spoofintelligence, use either of the following methods to override the spoof intelligence verdict:

- Select one or more entries from the list by selecting the check box next to the first column.

    1. Select the ![](media/defender-portal-icon-bulk-actions.png)**Bulk actions** action that appears.
    2. In the **Bulk actions** flyout that opens, select **Allow to spoof** or **Block from spoofing**, and then select **Apply**.
- Select the entry from the list by clicking anywhere in the row other than the check box.

    In the details flyout that opens, select **Allow to spoof** or **Block from spoofing** at the top of the flyout, and then select **Apply**.

Back on the **Spoof intelligence insight** page, the entry is removed from the list, and is added to the **Spoofed senders** tab on the **Tenant Allow/Block Lists** page at https://security.microsoft.com/tenantAllowBlockList?viewid=SpoofItem.

### About allowed spoofed senders

Messages from an allowed spoofed sender (automatically detected or manually configured) are allowed only using the combination of the spoofed domain *and* the sending infrastructure. For example, the following spoofed sender is allowed to spoof:

- **Domain**: gmail.com
- **Infrastructure**: tms.mx.com

Only email from that domain/sending infrastructure pair is allowed to spoof. Other senders attempting to spoof gmail.com aren't automatically allowed. Spoof intelligence checks messages from senders in other domains that originate from tms.mx.com, and those messages can still be blocked.

## Use the spoof intelligence insight in PowerShell

In [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell), you use the **Get-SpoofIntelligenceInsight** cmdlet to *view* allowed and blocked spoofed senders that were detected by spoof intelligence. To manually allow or block the spoofed senders, you need to use the **New-TenantAllowBlockListSpoofItems** cmdlet. For more information, see [Use PowerShell to create allow entries for spoofed senders in the Tenant Allow/Block List](tenant-allow-block-list-email-spoof-configure#use-powershell-to-create-allow-entries-for-spoofed-senders-in-the-tenant-allowblock-list) and [Use PowerShell to create block entries for spoofed senders in the Tenant Allow/Block List](tenant-allow-block-list-email-spoof-configure#use-powershell-to-create-block-entries-for-spoofed-senders-in-the-tenant-allowblock-list).

To view the information in the spoof intelligence insight, run the following command:

```powershell
Get-SpoofIntelligenceInsight
```

For detailed syntax and parameter information, see [Get-SpoofIntelligenceInsight](/en-us/powershell/module/exchangepowershell/get-spoofintelligenceinsight).

## Additional tools to manage spoofing and phishing

Be diligent about spoofing and phishing protection. Here are related ways to check on senders who are spoofing your domain and help prevent them from damaging your organization:

- Check the **Spoof Mail Report**. Use this report often to view and help manage spoofed senders. For information, see [Spoof Detections report](reports-email-security#spoof-detections-report).
- Review your SPF, DKIM, and DMARC configuration. For more information, see the following articles:

    - [Email authentication](email-authentication-about)
    - [Set up SPF to identify valid email sources for your custom cloud domains](email-authentication-spf-configure)
    - [Set up DKIM to sign mail from your cloud domain](email-authentication-dkim-configure)
    - [Set up DMARC to validate the From address domain for cloud senders](email-authentication-dmarc-configure)
    - [Configure trusted ARC sealers](email-authentication-arc-configure)