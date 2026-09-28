---
layout: Conceptual
title: Campaigns in Microsoft Defender for Office 365 Plan - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/campaigns
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.reviewer: mcostea
ms.topic: article
ms.localizationpriority: medium
ms.assetid: 
ms.collection:
- m365-security
- tier1
ms.custom:
- sfi-ga-nochange
- sfi-image-nochange
description: Learn about Campaigns in Microsoft Defender for Office 365.
ms.service: defender-office-365
ms.date: 2026-07-27T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: e68aef77-1041-5772-f670-b8f6a1a26859
document_version_independent_id: e68aef77-1041-5772-f670-b8f6a1a26859
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/campaigns.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: campaigns
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/campaigns.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 61a228b0-bb6c-9171-1c38-1b5365502e49
---

# Campaigns in Microsoft Defender for Office 365 Plan - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

In Microsoft 365 organizations with Microsoft Defender for Office 365 Plan 2, the *campaigns* feature identifies and categorizes coordinated phishing and malware email attacks. Microsoft's categorization of email attacks into discrete campaigns helps you to:

- Efficiently investigate and respond to email attacks.
- Better understand the scope of the email attack that's targeting your organization.
- Show the value of Microsoft Defender for Office 365 to decision makers in preventing email threats.

The campaigns feature lets you see the overall picture of an email attack faster and more completely than any human.

Watch this short video on how campaigns in Microsoft Defender for Office 365 help you understand coordinated email attacks that target your organization.

## What is a campaign?

A campaign is a coordinated email attack against one or many organizations. Email attacks that steal credentials and company data are a large and lucrative industry. As technologies increase to stop attacks, attackers modify their methods to ensure continued success.

Microsoft applies the vast amounts of anti-phishing, anti-spam, and anti-malware data from the entire service to identify campaigns. We analyze and classify the attack information according to several factors. For example:

- **Attack source**: The source IP addresses and sender email domains.
- **Message properties**: The content, style, and tone of the messages.
- **Message recipients**: How recipients are related. For example, recipient domains, recipient job functions (admins, executives, etc.), company types (large, small, public, private, etc.), and industries.
- **Attack payload**: Malicious links, attachments, or other payloads in the messages.

A campaign might be short-lived, or could span several days, weeks, or months with active and inactive periods. A campaign might be launched against your organization specifically, or your organization might be part of a larger campaign across multiple companies.

## Required licenses and permissions

- The campaigns feature is available in organizations with Defender for Office 365 Plan 2 (add-on licenses or included in subscriptions like Microsoft 365 E5).
- You need to be assigned permissions to view information about campaigns as described in this article. You have the following options:
    - [Microsoft Defender Unified role based access control (RBAC)](/en-us/defender-xdr/manage-rbac) (If **Email & collaboration** &gt; **Defender for Office 365** permissions is ![](media/scc-toggle-on.png)**Active**. Affects the Defender portal only, not PowerShell): **Security operations/Raw data (email & collaboration)/Email message headers (read)**.
    - [Email & collaboration permissions in the Microsoft Defender portal](mdo-portal-permissions): Membership in the **Organization Management**, **Security Administrator**, or **Security Reader** role group.
    - [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): Membership in the **Global Administrator**^\*^, **Security Administrator**, or **Security Reader** roles gives users the required permissions *and* permissions for other features in Microsoft 365.

        Important

        ^\*^ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.

## Campaigns page in the Microsoft Defender portal

To open the **Campaigns** page in the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Campaigns**. Or, to go directly to the **Campaigns** page, use https://security.microsoft.com/campaigns.

The **Campaigns** page consists of the following elements:

- A filter/query builder at the top of the page.
- A chart area where you can use the available pivots to organize the chart in different ways. By default, the chart uses the **Campaign Type** pivot, even though that pivot doesn't appear to be selected.
- A details area, which is set to the **Campaign** tab by default

[![Screenshot that shows the Campaigns in the Microsoft Defender portal.](media/campaigns-overview.png)](media/campaigns-overview.png#lightbox)

Tip

- If you don't see any campaign data or very limited data, try changing the date range or filters.
- You can also view the same information about campaigns in [Threat Explorer](threat-explorer-real-time-detections-about) at https://security.microsoft.com/threatexplorerv3:

    - **Campaigns** view.
    - **All email** view &gt; **Campaign** tab in the details area below the chart.
    - **Malware** view &gt; **Campaign** tab in the details area below the chart.
    - **Phish** view &gt; **Campaign** tab in the details area below the chart.
- If you have a Microsoft Defender for Endpoint subscription, campaigns information is connected with Microsoft Defender for Endpoint.

### Chart area on the Campaigns page

On the **Campaigns** page, the chart area shows a bar graph that shows the number of recipients per day. By default, the graph shows both **Malware** and **Phish** data.

To filter the information that's shown in the chart and in the details table, change the filters.

Change the organization of the chart by selecting **Campaign Type**, and then selecting one of the following values in the dropdown list:

- **Campaign Name**
- **Campaign Subtype**
- **Sender domain**
- **Sender IP**
- **Delivery action**
- **Detection technology**
- **Full URL**
- **URL domain**
- **URL domain and path**

Use ![](media/defender-portal-icon-download.png)**Export chart data** to export the data in the chart to a CSV file.

To remove the chart from the page (which maximizes the size of the details area), do either of the following steps:

- Select ![](media/defender-portal-icon-chart-view.png)**Chart View** &gt; ![](media/defender-portal-icon-list-view.png)**List View** at the top of the page.
- Select ![](media/defender-portal-icon-show-list-view.png)**Show list view** between the chart and the views for the details table.

### Details area on the Campaigns page

To filter the information that's shown in the chart and in the details table, change the filters.

On the **Campaigns** page, the **Campaign** tab below the chart shows the following information in the details table:

- **Name**
- **Sample subject**: The subject line of one of the messages in the campaign. All messages in the campaign don't necessarily have the same subject.
- **Targeted**: The percentage as calculated by: (the number of campaign recipients in your organization) / (the total number of recipients in the campaign across all organizations in the service). This value indicates the degree to which the campaign is directed only at your organization (a higher value) vs. also directed at other organizations in the service (a lower value).
- **Type**: The value is either **Phish** or **Malware**.
- **Subtype**: The value contains more details about the campaign. For example:
    - **Phish**: Where available, the brand that is being phished by this campaign. For example, `Microsoft`, `365`, `Unknown`, `Outlook`, or `DocuSign`. When the detection is driven by Defender for Office 365 technology, the prefix **ATP-** is added to the subtype value.
    - **Malware**: For example, `W32/<MalwareFamilyName>` or `VBS/<MalwareFamilyName>`.
- **Tags**: For more information about user tags, see [User tags](user-tags-about).
- **Recipients**: The number of users that were targeted by this campaign.
- **Inboxed**: The number of users that received messages from this campaign in their Inbox (not delivered to their Junk Email folder).
- **Clicked**: The number of users that selected the URL or opened the attachment in the phishing message.
- **Click rate**: In phishing campaigns, the percentage as calculated by "**Clicked** / **Inboxed**". This value is an indicator of the effectiveness of the campaign. In other words, were the recipients able to identify the message as phishing, and therefore avoided the payload URL? **Click rate** isn't used in malware campaigns.
- **Visited**: How many users actually made it through to the payload website. If there are **Clicked** values, but [Safe Links](safe-links-about) blocked access to the website, this value is zero.

Select a column header to sort by that column. To remove columns, select ![](media/defender-portal-icon-customize.png)**Customize columns**. By default, all available columns are selected.

Use ![](media/defender-portal-icon-download.png)**Export** to export the data in the details table to a CSV file.

On the **Campaigns** page, the **Campaign origin** tab below the chart shows the message sources on a map of the world.

### Filters on the Campaigns page

At the top of the **Campaign** page, there are several filter settings to help you find and isolate specific campaigns. The filters you select affect the chart and the details table.

By default, the view is filtered by yesterday and today. To change the date filter, select the date range, and then select **Start Date** and **End date** values up to 30 days ago.

[![Campaign filters on the Campaigns page.](media/campaign-filters-and-settings.png)](media/campaign-filters-and-settings.png#lightbox)

You can also filter the results by one or more message or campaign properties. The basic syntax is:

&lt;Property&gt; &lt;**Equal any of** | **Equal none of**&gt; &lt;Property value or values&gt;

- Select the message or campaign property from the **Campaign Type** dropdown list (**Campaign Type** is the default value that's selected).
- The property values that you need to enter are completely dependent on the property. Some properties allow freeform text with multiple values separated by commas, and some properties allow multiple values selected from a list.

The available properties and their associated values are described in the following table:

| Property | Type |
| --- | --- |
| **Basic** |  |
| Campaign Type | Select one or more values¹: <br>- **Malware**<br>- **Phish** |
| Campaign Name | Text. Separate multiple values by commas. |
| Campaign Subtype | Text. Separate multiple values by commas. |
| Sender address | Text. Separate multiple values by commas. |
| Recipients | Text. Separate multiple values by commas. |
| Sender domain | Text. Separate multiple values by commas. |
| Recipient domain | Text. Separate multiple values by commas. |
| Subject | Text. Separate multiple values by commas. |
| Sender display name | Text. Separate multiple values by commas. |
| Sender mail from address | Text. Separate multiple values by commas. |
| Sender mail from domain | Text. Separate multiple values by commas. |
| Malware family | Text. Separate multiple values by commas. |
| Tags | Text. Separate multiple values by commas.  For more information about user tags, see [User tags](user-tags-about). |
| Delivery action | Select one or more values¹: <br>- **Blocked**<br>- **Delivered**<br>- **Delivered to junk**<br>- **Replaced** |
| Additional action | Select one or more values¹: <br>- **Automated remediation**<br>- **Dynamic Delivery**: For more information, see [Dynamic Delivery in Safe Attachments policies](safe-attachments-about#dynamic-delivery-in-safe-attachments-policies).<br>- **Manual remediation**<br>- **None**<br>- **Quarantine release**<br>- **Reprocessed**<br>- **ZAP**: For more information, see [Zero-hour auto purge (ZAP) in Microsoft Defender for Office 365](zero-hour-auto-purge). |
| Directionality | Select one or more values¹: <br>- **Inbound**<br>- **Intra-irg**<br>- **Outbound** |
| Detection technology | Select one or more values¹: <br>- **Advanced filter**: Signals based on machine learning.<br>- **Antimalware protection**<br>- **Bulk**<br>- **Campaign**<br>- **Domain reputation**<br>- **File detonation**: [Safe Attachments](safe-attachments-about) detected a malicious attachment during detonation analysis.<br>- **File detonation reputation**: File attachments previously detected by [Safe Attachments](safe-attachments-about) detonations in other Microsoft 365 organizations.<br>- **File reputation**: The message contains a file that was previously identified as malicious in other Microsoft 365 organizations.<br>- **Fingerprint matching**: The message closely resembles a previous detected malicious message.<br>- **General filter**<br>- **Impersonation brand**: Sender impersonation of well-known brands.<br>- **Impersonation domain**: Impersonation of sender domains that you own or specified for protection in [anti-phishing policies](anti-phishing-policies-about#impersonation-settings-in-anti-phishing-policies-in-microsoft-defender-for-office-365)<br>- **Impersonation user**<br>- **IP reputation**<br>- **LLM content analysis**: Analysis by Microsoft's purpose-built large language models to detect harmful email.<br>- **Mail bombing**: A distributed denial of service (DDoS) attack that typically subscribes recipients to a large number of legitimate newsletters and services. The resulting volume of incoming email within minutes intends to overwhelm the recipient's mailbox and email security systems, and acts as a precursor to malware, ransomware, or data exfiltration.<br>- **Mailbox intelligence impersonation**: Impersonation detections from mailbox intelligence in [anti-phishing policies](anti-phishing-policies-about#impersonation-settings-in-anti-phishing-policies-in-microsoft-defender-for-office-365).<br>- **Mixed analysis detection**: Multiple filters contributed to the message verdict.<br>- **spoof DMARC**: The message failed [DMARC authentication](email-authentication-dmarc-configure).<br>- **Spoof external domain**: Sender email address spoofing using a domain that's external to your organization.<br>- **Spoof intra-org**: Sender email address spoofing using a domain that's internal to your organization.<br>- **URL detonation**: [Safe Links](safe-links-about) detected a malicious URL in the message during detonation analysis.&lt;/li<br>- **URL detonation reputation**: URLs previously detected by [Safe Links](safe-links-about) detonations in other Microsoft 365 organizations.<br>- **URL malicious reputation**: The message contains a URL that was previously identified as malicious in other Microsoft 365 organizations. |
| Original delivery location | Select one or more values¹: <br>- **Deleted Items folder**<br>- **Dropped**<br>- **Failed**<br>- **Inbox/folder**<br>- **Junk folder**<br>- **On-prem/external**<br>- **Quarantine**<br>- **Unknown** |
| Latest delivery location | Same values as **Original delivery location** |
| System overrides | Select one or more values¹: <br>- **Allowed by user policy**<br>- **Blocked by user policy**<br>- **Allowed by organization policy**<br>- **Blocked by organization policy**<br>- **File extension blocked by organization policy**<br>- **None** |
| System override source | Select one or more values¹: <br>- **3rd party filter**<br>- **Admin initiated time travel** (ZAP)<br>- **Anti-malware policy block by file type**<br>- **Anti-spam policy settings**<br>- **Connection policy**<br>- **Exchange transport rule** (mail flow rule)<br>- **Filtering skipped due to on-prem organization**<br>- **IP region filter from policy**<br>- **Language filter from policy**<br>- **Phishing simulation**<br>- **Quarantine release**<br>- **SecOPs mailbox**<br>- **Sender address list (admin override)**<br>- **Sender address list (user override)**<br>- **Sender domain list (admin override)** |
| **Advanced** |  |
| Internet Message ID | Text. Separate multiple values by commas.  Available in the **Message-ID** header field in the message header. An example value is `<08f1e0f6806a47b4ac103961109ae6ef@server.domain>` (note the angle brackets). |
| Network Message ID | Text. Separate multiple values by commas.  A GUID value that's available in the **X-MS-Exchange-Organization-Network-Message-Id** header field in the message header. |
| Sender IP | Text. Separate multiple values by commas. |
| Attachment SHA256 | Text. Separate multiple values by commas.  To find the SHA256 hash value of a file, run the following command in PowerShell: `Get-FileHash -Path "<Path>\<Filename>" -Algorithm SHA256`. |
| Cluster ID | Text. Separate multiple values by commas. |
| Alert ID | Text. Separate multiple values by commas. |
| Alert Policy ID | Text. Separate multiple values by commas. |
| Campaign ID | Text. Separate multiple values by commas. |
| ZAP URL signal | Text. Separate multiple values by commas. |
| **Urls** |  |
| URL domain | Text. Separate multiple values by commas. |
| URL domain and path | Text. Separate multiple values by commas. |
| URL | Text. Separate multiple values by commas. |
| URL path | Text. Separate multiple values by commas. |
| Click verdict | Select one or more values¹: <br>- **Allowed**<br>- **Block overridden**<br>- **Blocked**<br>- **Error**<br>- **Failure**<br>- **None**<br>- **Pending verdict**<br>- **Pending verdict bypassed** |
| **File** |  |
| Attachment filename | Text. Separate multiple values by commas. |

¹ Not using this property filter or using this property filter with no values selected has the same result as using this property filter with all values selected.

After you select a property from the **Campaign Type** dropdown, select **Equal any of** or **Not equal any of**, and then enter or select a value in the property box, the filter query appears below the filter area.

[![Screenshot showing a campaign filter selected.](media/campaign-filters-selected.png)](media/campaign-filters-selected.png#lightbox)

To add more conditions, select another property/value pair, and then select **AND** or **OR**. Repeat these steps as many times as necessary.

To remove existing property/value pairs, select ![](media/defender-portal-icon-remove-selection.png) next to the entry.

When you're finished building your filter query, select **Refresh**.

To save your filter query, select **Save query** &gt; ![](media/defender-portal-icon-save.png)**Save query**. In the **Save query** flyout that opens, configure the following settings:

- **Query name**: Enter a unique value.
- Select one of the following values:
    - **Exact dates**: Select the date range.
    - **Relative dates**: Select from one to 30 days.
- **Track this query**

When you're finished in the **Save query** flyout, select **Save**, and then select **OK** in the confirmation dialog.

When you return to the **Campaigns** page, you can load a saved filter by selecting **Save query** &gt; ![](media/defender-portal-icon-gear.png)**Saved query settings**.

## Campaign details

When you select an entry from the details table by clicking anywhere in the row other than the check box next to the name, a flyout opens that contains details about the campaign.

What's shown in the campaign details flyout is described in the following subsections.

### Campaign information

At the top of the campaign details flyout, the following campaign information is available:

- **Campaign ID**: The unique campaign identifier.
- **Activity**: The duration and activity of the campaign.
- The following data for the date range filter you selected (or that you select in the timeline):
    - **Impact**
    - **Messages**: The total number of recipients.
    - **Inboxed**: The number of messages that were delivered to the Inbox, not to the Junk Email folder.
    - **Clicked link**: How many users selected the payload URL in the phishing message.
    - **Visited link**: How many users visited the URL.
    - **Targeted(%)**: The percentage as calculated by: (the number of campaign recipients in your organization) / (the total number of recipients in the campaign across all organizations in the service). This value is calculated over the entire lifetime of the campaign, and isn't changed by date filters.
- Start date/time and end data/time filters for the campaign flow as described in the next section.
- An interactive timeline of campaign activity: The timeline shows activity over the entire lifetime of the campaign. You can hover over the data points in the graph to see the number of detected messages.

[![The Campaign information](media/campaign-details-campaign-info.png)](media/campaign-details-campaign-info.png#lightbox)

### Campaign flow

In the middle of the campaign details flyout, important details about the campaign are presented in a horizontal flow diagram (known as a *Sankey* diagram). These details help you to understand the elements of the campaign and the potential impact in your organization.

Tip

The information that's displayed in the flow diagram is controlled by the date range filter in the timeline as described in the previous section.

[![The Campaign details that don't contain user URL clicks](media/campaign-details-no-recipient-actions.png)](media/campaign-details-no-recipient-actions.png#lightbox)

If you hover over a horizontal band in the diagram, you see the number of related messages (for example, messages from a particular source IP, messages from the source IP using the specified sender domain, etc.).

The diagram contains the following information:

- **Sender IPs**
- **Sender domains**
- **Filter verdicts**: Verdict values are related to the available phishing and spam filtering verdicts as described in [Anti-spam message headers](message-headers-eop-mdo). The available values are described in the following table:

    | Value | Spam filter verdict | Description |
    | --- | --- | --- |
    | **Allowed** | `SFV:SKN`&lt;br/ `SFV:SKI` | The message was marked as not spam and/or skipped filtering before being evaluated by spam filtering. For example, the message was marked as not spam by a mail flow rule (also known as a transport rule). &lt;br/ The message skipped spam filtering for other reasons. For example, the sender and recipient appear to be in the same organization. |
    | **Blocked** | `SFV:SKS` | The message was marked as spam before spam filtering evaluated it, either by [Exchange mail flow rule (transport rule) that set the SCL](/en-us/exchange/security-and-compliance/mail-flow-rules/use-rules-to-set-scl), or by a spam decision passed from on-premises Exchange in a [hybrid deployment](/en-us/exchange/exchange-hybrid). The request to mark the message as spam is an input to filtering, not a final decision, so `SFV:SKS` appears only when the request is honored. |
    | **Detected** | `SFV:SPM` | The message was marked as spam by spam filtering. |
    | **Not Detected** | `SFV:NSPM` | The message was marked as not spam by spam filtering. |
    | **Released** | `SFV:SKQ` | The message skipped spam filtering because it was released from quarantine. |
    | **Tenant Allow**¹ | `SFV:SKA` | The message skipped spam filtering because of the settings in an anti-spam policy. For example, the sender was in the allowed senders list or allowed domain list. |
    | **Tenant Block**² | `SFV:SKA` | The message was blocked by spam filtering because of the settings in an anti-spam policy. For example, the sender was in the allowed senders list or allowed domain list. |
    | **User Allow**¹ | `SFV:SFE` | The message skipped spam filtering because the sender was in a user's Safe Senders list. |
    | **User Block**² | `SFV:BLK` | The message was blocked by spam filtering because the sender was in a user's Blocked Senders list. |
    | **ZAP** | n/a | [Zero-hour auto purge (ZAP)](zero-hour-auto-purge) moved the delivered message to the Junk Email folder or quarantine. You configure the action in [anti-spam policies](anti-spam-policies-configure). |

    ¹ Review your anti-spam policies, because the allowed message would have likely been blocked by the service.

    ² Review your anti-spam policies, because these messages should be quarantined, not delivered.
- **Message destinations**: Investigate messages that were delivered to recipients (either to the Inbox or the Junk Email folder), even if users didn't select the payload URL in the message. You can also remove the quarantined messages from quarantine. For more information, see [Quarantine](quarantine-about).

    - **Deleted folder**
    - **Dropped**
    - **External**: The recipient is located in your on-premises email organization in hybrid environments.
    - **Failed**
    - **Forwarded**
    - **Inbox**
    - **Junk folder**
    - **Quarantine**
    - **Unknown**
- **URL clicks**: These values are described in the next section.

Note

In all layers that contain more than 10 items, the top 10 items are shown, while the rest are bundled together in **Others**.

#### URL clicks

When a phishing message is delivered to a recipient's Inbox or Junk Email folder, there's always a chance that the user will select the payload URL. Not selecting the URL is a small measure of success, but you need to determine why the phishing message was delivered to the mailbox in the first place.

If a user selected the payload URL in the phishing message, the actions are displayed in the **URL clicks** area of the diagram in the campaign details view.

- **Allowed**
- **BlockPage**: The recipient selected the payload URL, but their access to the malicious website was blocked by a [Safe Links](safe-links-about) policy in your organization.
- **BlockPageOverride**: The recipient selected the payload URL in the message, Safe Links tried to stop them, but they were allowed to override the block. Inspect your [Safe Links policies](safe-links-policies-configure) to see why users are allowed to override the Safe Links verdict and continue to the malicious website.
- **PendingDetonationPage**: Safe Attachments in Microsoft Defender for Office 365 is opening and investigating the payload URL in a virtual environment.
- **PendingDetonationPageOverride**: The recipient was allowed to override the payload detonation process and open the URL without waiting for the results.

### Tabs

Tip

The information that's displayed on the tabs is controlled by the date range filter in the campaign details flyout as described in the Campaign information section.

The tabs in the campaign details flyout allow you to further investigate the campaign. The following tabs are available:

- **URL clicks**: If users didn't select the payload URL in the message, this section is blank. If a user was able to select the URL, the following values are populated:

    - **User**^\*^
    - **Tags**
    - **URL**^\*^
    - **Click time**
    - **Click verdict**
- **Sender IPs**

    - **Sender IP**^\*^
    - **Total count**
    - **Inboxed**
    - **Not Inboxed**
    - **SPF passed**: The sender was authenticated by the [Sender Policy Framework (SPF)](email-authentication-spf-configure). A sender that doesn't pass SPF validation indicates an unauthenticated sender, or the message is spoofing a legitimate sender.
- **Senders**

    - **Sender**: This address is the actual sender address in the SMTP **MAIL FROM** command, which isn't necessarily the **From:** email address that users see in their email clients.
    - **Total count**
    - **Inboxed**
    - **Not Inboxed**
    - **DKIM passed**: The sender was authenticated by [Domain Keys Identified Mail (DKIM)](email-authentication-dkim-configure). A sender that doesn't pass DKIM validation indicates an unauthenticated sender, or the message is spoofing a legitimate sender.
    - **DMARC passed**: The sender was authenticated by [Domain-based Message Authentication, Reporting, and Conformance (DMARC)](email-authentication-dmarc-configure). A sender that doesn't pass DMARC validation indicates an unauthenticated sender, or the message is spoofing a legitimate sender.
- **Attachments**

    - **Filename**
    - **SHA256**
    - **Malware family**
    - **Total count**
- **URLs**

    - **URL**^\*^
    - **Total Count**

^\*^ Selecting this value opens a new flyout that contains more details about the specified item (user, URL, etc.) on top of the campaign details view. To return to the campaign details flyout, select **Done** in the new flyout.

On each tab, select a column header to sort by that column. To remove columns, select ![](media/defender-portal-icon-customize.png)**Customize columns**. By default, all available columns on each tab are selected.

### Additional actions

The actions at the bottom the campaign details flyout allow you to investigate and record details about the campaign:

- Select **Yes** or **No** in **Do you think this campaign has accurately grouped these messages together?**.
- **Explore messages**: Use the power of Threat Explorer to further investigate the campaign by selecting one of the following values in the dropdown list:
    - **All messages**: Opens a new Threat Explorer search tab using the **Campaign ID** value as the search filter.
    - **Inboxed messages**: Opens a new Threat Explorer search tab using the **Campaign ID** and **Delivery location: Inbox** as the search filter.
    - **Internal messages**: Opens a new Threat Explorer search tab using the **Campaign ID** and **Directionality: Intra-org** as the search filter.
- **Download threat report**: Download the campaign details to a Word document (by default, named CampaignReport.docx). The download contains details over the entire lifetime of the campaign (not just the date filter you selected).