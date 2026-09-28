---
layout: Conceptual
title: Investigate malicious email delivered in Microsoft 365 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/threat-explorer-investigate-delivered-malicious-email
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
keywords: TIMailData-Inline, Security Incident, incident, Microsoft Defender for Endpoint PowerShell, email malware, compromised users, email phish, email malware, read email headers, read headers, open email headers,special actions
author: chrisda
ms.author: chrisda
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.localizationpriority: medium
ms.assetid: 8f54cd33-4af7-4d1b-b800-68f8818e5b2a
ms.collection:
- m365-security
- tier1
description: Learn how to use threat investigation and response capabilities to find and investigate malicious email.
ms.custom:
- msecd-doc-authoring-1016
- seo-marvel-apr2020
- sfi-image-nochange
ms.service: defender-office-365
ai-usage: ai-assisted
locale: en-us
document_id: ea99d515-61ae-5ca3-c0d8-3ab2e0909be5
document_version_independent_id: ea99d515-61ae-5ca3-c0d8-3ab2e0909be5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/threat-explorer-investigate-delivered-malicious-email.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: threat-explorer-investigate-delivered-malicious-email
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/threat-explorer-investigate-delivered-malicious-email.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: e13aaeb5-5ac2-ce86-efe4-c5f380f9fe09
---

# Investigate malicious email delivered in Microsoft 365 - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

Microsoft 365 organizations that have [Microsoft Defender for Office 365](mdo-about) included in their subscription or purchased as an add-on have **Explorer** (also known as **Threat Explorer**) or **Real-time detections**. These features are powerful, near real-time tools to help Security Operations (SecOps) teams investigate and respond to threats. For more information, see [About Threat Explorer and Real-time detections in Microsoft Defender for Office 365](threat-explorer-real-time-detections-about).

Threat Explorer and Real-time detections allow you to investigate activities that put people in your organization at risk, and to take action to protect your organization. For example:

- Find and delete messages.
- Identify the IP address of a malicious email sender.
- Start an incident for further investigation.

This article explains how to use Threat Explorer and Real-time detections to find malicious email in recipient mailboxes.

Tip

To go directly to the remediation procedures, see [Remediate malicious email delivered in Office 365](remediate-malicious-email-delivered-office-365).

For other email scenarios using Threat Explorer and Real-time detections, see the following articles:

- [Threat hunting in Threat Explorer and Real-time detections in Microsoft Defender for Office 365](threat-explorer-threat-hunting)
- [Email security with Threat Explorer and Real-time detections in Microsoft Defender for Office 365](threat-explorer-email-security)

## What do you need to know before you begin?

Review the following licensing, permissions, and filtering considerations before you begin.

- Threat Explorer is included in Defender for Office 365 Plan 2. Real-time detections is included in Defender for Office Plan 1:

    - The differences between Threat Explorer and Real-time detections are described in [About Threat Explorer and Real-time detections in Microsoft Defender for Office 365](threat-explorer-real-time-detections-about).
    - The differences between Defender for Office 365 Plan 2 and Defender for Office Plan 1 are described in the [Defender for Office 365 Plan 1 vs. Plan 2 cheat sheet](mdo-about#defender-for-office-365-plan-1-vs-plan-2-cheat-sheet).
- For filter properties that require you to select one or more available values, using the property in the filter condition with all values selected has the same result as not using the property in the filter condition.
- For permissions and licensing requirements for Threat Explorer and Real-time detections, see [Permissions and licensing for Threat Explorer and Real-time detections](threat-explorer-real-time-detections-about#permissions-and-licensing-for-threat-explorer-and-real-time-detections).

## Find suspicious email that was delivered

Use the following steps to locate suspicious delivered email in Threat Explorer or Real-time detections.

1. Use one of the following steps to open Threat Explorer or Real-time detections:

    - **Threat Explorer**: In the Defender portal at https://security.microsoft.com, go to **Email & Security** &gt; **Explorer**. Or, to go directly to the **Explorer** page, use https://security.microsoft.com/threatexplorerv3.
    - **Real-time detections**: In the Defender portal at https://security.microsoft.com, go to **Email & Security** &gt; **Real-time detections**. Or, to go directly to the **Real-time detections** page, use https://security.microsoft.com/realtimereportsv3.
2. On the **Explorer** or **Real-time detections** page, select an appropriate view:

    - **Threat Explorer**: Verify the [All email view](threat-explorer-real-time-detections-about#all-email-view-in-threat-explorer) is selected.
    - **Real-time detections**: Verify the [Malware view](threat-explorer-real-time-detections-about#malware-view-in-threat-explorer-and-real-time-detections) is selected, or select the [Phish view](threat-explorer-real-time-detections-about#phish-view-in-threat-explorer-and-real-time-detections).
3. Select the date/time range. The default is yesterday and today.

    [![Screenshot of the date filter used in Threat Explorer and Real-time detections in the Defender portal.](media/te-rtd-date-filter.png)](media/te-rtd-date-filter.png#lightbox)
4. Create one or more filter conditions using some or all of the following targeted properties and values. For complete instructions, see [Property filters in Threat Explorer and Real-time detections](threat-explorer-real-time-detections-about#property-filters-in-threat-explorer-and-real-time-detections). For example:

    - **Delivery action**: The action taken on an email due to existing policies or detections. Useful values are:

        - **Delivered**: Email delivered to the user's Inbox or other folder where the user can access the message.
        - **Junked**: Email delivered to the user's Junk Email folder or Deleted Items folder where the user can access the message.
        - **Blocked**: Email messages that were quarantined, that failed delivery, or were dropped.
    - **Original delivery location**: Where email went before any automatic or manual post-delivery actions by the system or admins (for example, [ZAP](zero-hour-auto-purge) or moved to quarantine). Useful values are:

        - **Deleted items folder**
        - **Dropped**: The message was lost somewhere in mail flow.
        - **Failed**: The message failed to reach the mailbox.
        - **Inbox/folder**
        - **Junk folder**
        - **On-prem/external**: The mailbox doesn't exist in the Microsoft 365 organization.
        - **Quarantine**
        - **Unknown**: For example, after delivery, an Inbox rule moved the message to a default folder (for example, Draft or Archive) instead of to the Inbox or Junk Email folder.
    - **Last delivery location**: Where email ended-up after any automatic or manual post-delivery actions by the system or admins. The available values are the same as **Original delivery location**: Deleted items folder, Dropped, Failed, Inbox/folder, Junk folder, On-prem/external, Quarantine, and Unknown.
    - **Directionality**: Valid values are:

        - **Inbound**
        - **Intra-org**
        - **Outbound**

        This information can help identify spoofing and impersonation. For example, messages from internal domain senders should be **Intra-org**, not **Inbound**.
    - **Additional action**: Valid values are:

        - **Automated remediation** (Defender for Office 365 Plan 2)
        - **Dynamic Delivery**: For more information, see [Dynamic Delivery in Safe Attachments policies](safe-attachments-about#dynamic-delivery-in-safe-attachments-policies).
        - **Manual remediation**
        - **None**
        - **Quarantine release**
        - **Reprocessed**: The message was retroactively identified as good.
        - **ZAP**: For more information, see [Zero-hour auto purge (ZAP) in Microsoft Defender for Office 365](zero-hour-auto-purge).
    - **Primary override**: If organization or user settings allowed or blocked messages that would have otherwise been blocked or allowed. Values are:

        - **Allowed by organization policy**
        - **Allowed by user policy**
        - **Blocked by organization policy**
        - **Blocked by user policy**
        - **None**

        These categories are further refined by the **Primary override source** property.
    - **Primary override source** The type of organization policy or user setting that allowed or blocked messages that would have otherwise been blocked or allowed. Values are:

        - **3rd Party Filter**
        - **Admin initiated time travel**
        - **Antimalware policy block by file type**: [Common attachments filter in anti-malware policies](anti-malware-protection-about#common-attachments-filter-in-anti-malware-policies)
        - **Antispam policy settings**
        - **Connection policy**: [Connection filtering](connection-filter-policies-configure)
        - **Exchange transport rule** (mail flow rule)
        - **Exclusive mode (User override)**: The **Only trust email from addresses in my Safe senders and domains list and Safe mailing lists** setting in the [safelist collection on a mailbox](configure-junk-email-settings-on-exo-mailboxes#use-exchange-online-powershell-to-configure-the-safelist-collection-on-a-mailbox).
        - **Filtering skipped due to on-prem organization**
        - **IP region filter from policy**: The **From these countries** filter in [anti-spam policies](anti-spam-protection-about#spam-properties-in-anti-spam-policies).
        - **Language filter from policy**: The **Contains specific languages** filter in [anti-spam policies](anti-spam-protection-about#spam-properties-in-anti-spam-policies).
        - **Phishing Simulation**: [Configure non-Microsoft phishing simulations in the advanced delivery policy](advanced-delivery-policy-configure#use-the-microsoft-defender-portal-to-configure-non-microsoft-phishing-simulations-in-the-advanced-delivery-policy)
        - **Quarantine release**: [Release quarantined email](quarantine-admin-manage-messages-files#release-quarantined-email)
        - **SecOps Mailbox**: [Configure SecOps mailboxes in the advanced delivery policy](advanced-delivery-policy-configure#use-the-microsoft-defender-portal-to-configure-secops-mailboxes-in-the-advanced-delivery-policy)
        - **Sender address list (Admin Override)**: The allowed senders list or blocked senders list in [anti-spam policies](anti-spam-protection-about#allow-and-block-lists-in-anti-spam-policies).
        - **Sender address list (User override)**: Sender email addresses in the **Blocked Senders** list in the [safelist collection on a mailbox](configure-junk-email-settings-on-exo-mailboxes#use-exchange-online-powershell-to-configure-the-safelist-collection-on-a-mailbox).
        - **Sender domain list (Admin Override)**: The allowed domains list or blocked domains list in [anti-spam policies](anti-spam-protection-about#allow-and-block-lists-in-anti-spam-policies).
        - **Sender domain list (User override)**: Sender domains in the **Blocked Senders** list in the [safelist collection on a mailbox](configure-junk-email-settings-on-exo-mailboxes).
        - **Tenant Allow/Block List file block**: [Create block entries for files](tenant-allow-block-list-files-configure#create-block-entries-for-files)
        - **Tenant Allow/Block List sender email address block**: [Create block entries for domains and email addresses](tenant-allow-block-list-email-spoof-configure#create-block-entries-for-domains-and-email-addresses)
        - **Tenant Allow/Block List spoof block**: [Create block entries for spoofed senders](tenant-allow-block-list-email-spoof-configure#create-block-entries-for-spoofed-senders)
        - **Tenant Allow/Block List URL block**: [Create block entries for URLs](tenant-allow-block-list-urls-configure#create-block-entries-for-urls)
        - **Trusted contact list (User override)**: The **Trust email from my contacts** setting in the [safelist collection on a mailbox](configure-junk-email-settings-on-exo-mailboxes#use-exchange-online-powershell-to-configure-the-safelist-collection-on-a-mailbox).
        - **Tenant Allow/Block List file block**: [Create block entries for files](tenant-allow-block-list-files-configure#create-block-entries-for-files)
        - **Trusted domain (User override)**: Sender domains in the **Safe Senders** list in the [safelist collection on a mailbox](configure-junk-email-settings-on-exo-mailboxes#use-exchange-online-powershell-to-configure-the-safelist-collection-on-a-mailbox).
        - **Trusted recipient (User override)**: Recipient email addresses or domains in the **Safe Recipients** list in the [safelist collection on a mailbox](configure-junk-email-settings-on-exo-mailboxes#use-exchange-online-powershell-to-configure-the-safelist-collection-on-a-mailbox).
        - **Trusted senders only (User override)**: The **Safe Lists Only: Only mail from people or domains on your Safe Senders List or Safe Recipients List will be delivered to your Inbox** setting in the [safelist collection on a mailbox](configure-junk-email-settings-on-exo-mailboxes#use-exchange-online-powershell-to-configure-the-safelist-collection-on-a-mailbox).
    - **Override source**: Same available values as **Primary override source**.

        Tip

        In the **Email** tab (view) in the details area of the **[All email](threat-explorer-real-time-detections-about#email-view-for-the-details-area-of-the-all-email-view-in-threat-explorer)**, **[Malware](threat-explorer-real-time-detections-about#email-view-for-the-details-area-of-the-malware-view-in-threat-explorer-and-real-time-detections)**, and **[Phish](threat-explorer-real-time-detections-about#email-view-for-the-details-area-of-the-phish-view-in-threat-explorer-and-real-time-detections)** views, the corresponding override columns are named **System overrides** and **System overrides source**.
    - **URL threat**: Valid values are:

        - **Malware**
        - **Phish**
        - **Spam**
5. When you're finished configuring date/time and property filters, select **Refresh**.

The **Email** tab (view) in the details area of the **[All email](threat-explorer-real-time-detections-about#email-view-for-the-details-area-of-the-all-email-view-in-threat-explorer)**, **[Malware](threat-explorer-real-time-detections-about#email-view-for-the-details-area-of-the-malware-view-in-threat-explorer-and-real-time-detections)**, or **[Phish](threat-explorer-real-time-detections-about#email-view-for-the-details-area-of-the-phish-view-in-threat-explorer-and-real-time-detections)** views contains the details you need to investigate suspicious email.

For example, use the **Delivery Action**, **Original delivery location**, and **Last delivery location** columns in the **Email** tab (view) to get a complete picture of where the affected messages went. **Delivery Action** shows whether the message was delivered, junked, or blocked. **Original delivery location** shows where the message went initially (for example, Inbox, Junk folder, or Quarantine), and **Last delivery location** shows where the message ended up after any post-delivery actions by the system or admins.

Use ![](media/defender-portal-icon-download.png)**Export** to selectively export up to 200,000 filtered or unfiltered results to a CSV file.

## Remediate malicious email that was delivered

After you identify the malicious email messages that were delivered, you can remove them from recipient mailboxes. For instructions, see [Remediate malicious email delivered in Office 365](remediate-malicious-email-delivered-office-365).