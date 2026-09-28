---
layout: Conceptual
title: Recommendations for Microsoft 365 security settings - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/recommended-settings-for-eop-and-office365
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
keywords: Office 365 security recommendations, Sender Policy Framework, Domain-based Message Reporting and Conformance, DomainKeys Identified Mail, steps, how does it work, security baselines, baselines for default protections, baselines for Defender for Office 365, set up Defender for Office 365, configure Defender for Office 365, security configuration
author: chrisda
ms.author: chrisda
ms.topic: article
ms.localizationpriority: medium
ms.assetid: 6f64f2de-d626-48ed-8084-03cc72301aa4
ms.collection:
- m365-security
- m365initiative-defender-office365
- highpri
- tier1
description: What are best practices for email and collaboration security settings in Microsoft 365? What are the current recommendations for standard protection? What should you use to be more strict? And what extras do you get if you also use Microsoft Defender for Office 365?
ai-usage: ai-assisted
ms.service: defender-office-365
ms.date: 2026-08-10T00:00:00.0000000Z
ms.custom: sfi-ga-nochange, msecd-doc-authoring-1015
locale: en-us
document_id: 9b8cd133-9717-375d-95cd-201981cd1e77
document_version_independent_id: 9b8cd133-9717-375d-95cd-201981cd1e77
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/recommended-settings-for-eop-and-office365.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: recommended-settings-for-eop-and-office365
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/recommended-settings-for-eop-and-office365.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 68e14559-de81-f776-5e68-4a477f365d04
---

# Recommendations for Microsoft 365 security settings - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

Although all organizations with cloud mailboxes include [built-in security features](eop-about), Microsoft Defender for Office 365 is the primary email and collaboration security solution for Microsoft 365.

We recommend two security levels: **Standard** and **Strict**. Although customer environments and needs are different, these levels of filtering help keep unwanted email out of user mailboxes in most situations.

To automatically apply the Standard or Strict settings to users, use [Preset security policies](preset-security-policies).

This article describes the default threat policy settings, and also the recommended Standard and Strict settings to help protect users. The tables contain the settings in the Microsoft Defender portal and Exchange Online PowerShell.

Note

- Threat policies work best when the source email domains for your organization are correctly authenticated. Before tuning anti-phishing or other threat policies, verify the [email authentication](email-authentication-about) settings for outbound mail from each sending domains:

    - [Sender Policy Framework (SPF)](email-authentication-spf-configure): Authorizes the services permitted to send mail on behalf of your domain.
    - [DomainKeys Identified Mail (DKIM)](email-authentication-dkim-configure): Signs messages so recipients can verify the message wasn't altered and is authorized by the signing domain.
    - [Domain-based Message Authentication, Reporting, and Conformance (DMARC)](email-authentication-dmarc-configure): Tells recipient systems how to handle messages that fail authentication and whether authentication aligns with the visible From: domain.

    If SPF, DKIM, or DMARC are missing or misconfigured, legitimate messages might be delivered to the Junk Email folder or quarantine, even with the recommended threat policy settings. Fix authentication first, then review and tune policy settings.
- You can use the configuration analyzer to compare the settings in custom threat policies to the recommended Standard or Strict values. For more information, see [Configuration analyzer for threat policies](configuration-analyzer-for-security-policies).
- The Office 365 Advanced Threat Protection Recommended Configuration Analyzer (ORCA) module for PowerShell can help admins find the current values of these settings. Specifically, the **Get-ORCAReport** cmdlet generates an assessment of anti-spam, anti-phishing, and other message hygiene settings. You can download the ORCA module at https://www.powershellgallery.com/packages/ORCA/.
- We recommend that you leave the Junk Email Filter in Outlook set to **No automatic filtering** to prevent unnecessary conflicts (both positive and negative) with the spam filtering verdicts from Microsoft 365. For more information, see the following articles:

    - [Configure junk email settings on cloud mailboxes](configure-junk-email-settings-on-exo-mailboxes)
    - [About junk email settings in Outlook](configure-junk-email-settings-on-exo-mailboxes#about-outlook-junk-email-settings)
    - [Change the level of protection in the Junk Email Filter](https://support.microsoft.com/office/e89c12d8-9d61-4320-8c57-d982c8d52f6b)
    - [Create sender allowlists](create-safe-sender-lists-in-office-365)
    - [Create sender blocklists](create-block-sender-lists-in-office-365)

## Built-in security features for all cloud mailboxes

The [the built-in security features](eop-about) in this section are available in all organizations with cloud mailboxes. We recommend the Standard or Strict configurations as described in the tables in the following subsections.

### Anti-malware policy settings

To create and configure anti-malware policies, see [Configure anti-malware policies](anti-malware-policies-configure).

Quarantine policies define what users are able to do to quarantined messages, and whether users receive quarantine notifications. For more information, see [Anatomy of a quarantine policy](quarantine-policies#anatomy-of-a-quarantine-policy).

The policy named AdminOnlyAccessPolicy enforces the historical capabilities of messages quarantined as malware as described in the table [in this article](quarantine-end-user).

Users can't release their own messages quarantined as malware, regardless of how the quarantine policy is configured. If the policy is configured for users to release these quarantined messages, users are instead allowed to *request* the release of these quarantined messages.

| Security feature name | Details |
| --- | --- |
| **Protection settings** |  |
| **Enable the common attachments filter** (*EnableFileFilter*) | Show details<br>**Default**: Selected (`$true`)^\*^**Standard**: Selected (`$true`)**Strict**: Selected (`$true`)**Comment**: For the list of file types in the common attachments filter, see [Common attachments filter in anti-malware policies](anti-malware-protection-about#common-attachments-filter-in-anti-malware-policies).^\*^ The common attachments filter is **on** by default in new anti-malware policies that you create in the Defender portal or in PowerShell, and in the default anti-malware policy in organizations created after December 1, 2023. |
| Common attachment filter notifications: **When these file types are found** (*FileTypeAction*) | Show details<br>**Default**: **Reject the message with a non-delivery report (NDR)** (`Reject`)**Standard**: **Reject the message with a non-delivery report (NDR)** (`Reject`)**Strict**: **Reject the message with a non-delivery report (NDR)** (`Reject`) |
| **Enable zero-hour auto purge for malware** (*ZapEnabled*) | Show details<br>**Default**: Selected (`$true`)**Standard**: Selected (`$true`)**Strict**: Selected (`$true`) |
| **Quarantine policy** (*QuarantineTag*) | Show details<br>**Default**: AdminOnlyAccessPolicy**Standard**: AdminOnlyAccessPolicy**Strict**: AdminOnlyAccessPolicy |
| **Admin notifications** |  |
| **Notify an admin about undelivered messages from internal senders** (*EnableInternalSenderAdminNotifications* and *InternalSenderAdminAddress*) | Show details<br>**Default**: Not selected (`$false`)**Standard**: Not selected (`$false`)**Strict**: Not selected (`$false`)**Comment**: We have no specific recommendation for this setting. |
| **Notify an admin about undelivered messages from external senders** (*EnableExternalSenderAdminNotifications* and *ExternalSenderAdminAddress*) | Show details<br>**Default**: Not selected (`$false`)**Standard**: Not selected (`$false`)**Strict**: Not selected (`$false`)**Comment**: We have no specific recommendation for this setting. |
| **Customize notifications** | **Comment**: We have no specific recommendations for these settings. |
| **Use customized notification text** (*CustomNotifications*) | Show details<br>**Default**: Not selected (`$false`)**Standard**: Not selected (`$false`)**Strict**: Not selected (`$false`) |
| **From name** (*CustomFromName*) | Show details<br>**Default**: Blank**Standard**: Blank**Strict**: Blank |
| **From address** (*CustomFromAddress*) | Show details<br>**Default**: Blank**Standard**: Blank**Strict**: Blank |
| **Customize notifications for messages from internal senders** | Show details<br>**Comment**: These settings are used only if **Notify an admin about undelivered messages from internal senders** is selected. |
| **Subject** (*CustomInternalSubject*) | Show details<br>**Default**: Blank**Standard**: Blank**Strict**: Blank |
| **Message** (*CustomInternalBody*) | Show details<br>**Default**: Blank**Standard**: Blank**Strict**: Blank |
| **Customize notifications for messages from external senders** | **Comment**: These settings are used only if **Notify an admin about undelivered messages from external senders** is selected. |
| **Subject** (*CustomExternalSubject*) | Show details<br>**Default**: Blank**Standard**: Blank**Strict**: Blank |
| **Message** (*CustomExternalBody*) | Show details<br>**Default**: Blank**Standard**: Blank**Strict**: Blank |

### Anti-spam policy settings

To create and configure anti-spam policies, see [Configure anti-spam policies](anti-spam-policies-configure).

Wherever you select **Quarantine message** as the action for a spam filter verdict, a **Select quarantine policy** box is available. Quarantine policies define what users are able to do to quarantined messages, and whether users receive quarantine notifications. For more information, see [Anatomy of a quarantine policy](quarantine-policies#anatomy-of-a-quarantine-policy).

If you *change* the action of a spam filtering verdict to **Quarantine message** as you create anti-spam policies in the Defender portal, the **Select quarantine policy** box is blank by default. A blank value means the default quarantine policy for that spam filtering verdict is used. These default quarantine policies enforce the historical capabilities of the spam filter verdict that quarantined the message as described in the table [in this article](quarantine-end-user). When you later view or edit the anti-spam policy settings, the quarantine policy name is shown.

Admins can create or use quarantine policies with more restrictive or less restrictive capabilities. For instructions, see [Create quarantine policies in the Microsoft Defender portal](quarantine-policies#step-1-create-quarantine-policies-in-the-microsoft-defender-portal).

| Security feature name | Details |
| --- | --- |
| **Bulk email threshold & spam properties** |  |
| **Bulk email threshold** (*BulkThreshold*) | Show details<br>**Default**: 7**Standard**: 6**Strict**: 5**Comment**: For details, see [Bulk complaint level (BCL)](anti-spam-bulk-complaint-level-bcl-about). |
| **Bulk email spam** (*MarkAsSpamBulkMail*) | Show details<br>**Default**: (`On`)**Standard**: (`On`)**Strict**: (`On`)**Comment**: This setting is only available in PowerShell. |
| **Increase spam score** settings | Show details<br>**Comment**: All of these settings are part of the Advanced Spam Filter (ASF). For more information, see the ASF settings in anti-spam policies section in this article. |
| **Mark as spam** settings | Show details<br>**Comment**: Most of these settings are part of ASF. For more information, see the ASF settings in anti-spam policies section in this article. |
| **Contains specific languages** (*EnableLanguageBlockList* and *LanguageBlockList*) | Show details<br>**Default**: **Off** (`$false` and Blank)**Standard**: **Off** (`$false` and Blank)**Strict**: **Off** (`$false` and Blank)**Comment**: We have no specific recommendation for this setting. You can block messages in specific languages based on your business needs. |
| **From these regions** (*EnableRegionBlockList* and *RegionBlockList*) | Show details<br>**Default**: **Off** (`$false` and Blank)**Standard**: **Off** (`$false` and Blank)**Strict**: **Off** (`$false` and Blank)**Comment**: We have no specific recommendation for this setting. You can block messages from specific regions based on your business needs. |
| **Test mode** (*TestModeAction*) | Show details<br>**Default**: **None** **Standard**: **None** **Strict**: **None** **Comment**: This setting is part of ASF. For more information, see the ASF settings in anti-spam policies section in this article. |
| **Actions** |  |
| **Spam** detection action (*SpamAction*) | Show details<br>**Default**: **Move message to Junk Email folder** (`MoveToJmf`)**Standard**: **Move message to Junk Email folder** (`MoveToJmf`)**Strict**: **Quarantine message** (`Quarantine`) |
| **Quarantine policy** for **Spam** (*SpamQuarantineTag*) | Show details<br>**Default**: DefaultFullAccessPolicy¹**Standard**: DefaultFullAccessPolicy**Strict**: DefaultFullAccessWithNotificationPolicy**Comment**: The quarantine policy is meaningful only if spam detections are quarantined. |
| **High confidence spam** detection action (*HighConfidenceSpamAction*) | Show details<br>**Default**: **Move message to Junk Email folder** (`MoveToJmf`)**Standard**: **Quarantine message** (`Quarantine`)**Strict**: **Quarantine message** (`Quarantine`) |
| **Quarantine policy** for **High confidence spam** (*HighConfidenceSpamQuarantineTag*) | Show details<br>**Default**: DefaultFullAccessPolicy¹**Standard**: DefaultFullAccessWithNotificationPolicy**Strict**: DefaultFullAccessWithNotificationPolicy**Comment**: The quarantine policy is meaningful only if high confidence spam detections are quarantined. |
| **Phishing** detection action (*PhishSpamAction*) | Show details<br>**Default**: **Move message to Junk Email folder** (`MoveToJmf`)^\*^**Standard**: **Quarantine message** (`Quarantine`)**Strict**: **Quarantine message** (`Quarantine`)**Comment**: ^\*^ The default value is **Move message to Junk Email folder** in the default anti-spam policy and in new anti-spam policies that you create in PowerShell. The default value is **Quarantine message** in new anti-spam policies that you create in the Defender portal. |
| **Quarantine policy** for **Phishing** (*PhishQuarantineTag*) | Show details<br>**Default**: DefaultFullAccessPolicy¹**Standard**: DefaultFullAccessWithNotificationPolicy**Strict**: DefaultFullAccessWithNotificationPolicy**Comment**: The quarantine policy is meaningful only if phishing detections are quarantined. |
| **High confidence phishing** detection action (*HighConfidencePhishAction*) | Show details<br>**Default**: **Quarantine message** (`Quarantine`)**Standard**: **Quarantine message** (`Quarantine`)**Strict**: **Quarantine message** (`Quarantine`)**Comment**: Users can't release their own messages quarantined as high confidence phishing, regardless of how the quarantine policy is configured. If the policy is configured for users to release these quarantined messages, users are instead allowed to *request* the release of these quarantined messages. |
| **Quarantine policy** for **High confidence phishing** (*HighConfidencePhishQuarantineTag*) | Show details<br>**Default**: AdminOnlyAccessPolicy**Standard**: AdminOnlyAccessPolicy**Strict**: AdminOnlyAccessPolicy |
| **Bulk compliant level (BCL) met or exceeded** (*BulkSpamAction*) | Show details<br>**Default**: **Move message to Junk Email folder** (`MoveToJmf`)**Standard**: **Move message to Junk Email folder** (`MoveToJmf`)**Strict**: **Quarantine message** (`Quarantine`) |
| **Quarantine policy** for **Bulk compliant level (BCL) met or exceeded** (*BulkQuarantineTag*) | Show details<br>**Default**: DefaultFullAccessPolicy¹**Standard**: DefaultFullAccessPolicy**Strict**: DefaultFullAccessWithNotificationPolicy**Comment**: The quarantine policy is meaningful only if bulk detections are quarantined. |
| **Bulk moves enabled** (currently in Preview) (*BulkMovesEnabled*) | Show details<br>**Default**: **Off** (`NotSet`)**Standard**: **Off** (`NotSet`)**Strict**: **Off** (`NotSet`)**Comment**: For more information, see [Deliver bulk mail below the BCL threshold to the Promotions folder](anti-spam-bulk-complaint-level-bcl-about#deliver-bulk-mail-below-the-bcl-threshold-to-the-promotions-folder). |
| **Intra-Organizational messages to take action on** (*IntraOrgFilterState*) | Show details<br>**Default**: **Default** (Default)**Standard**: **Default** (Default)**Strict**: **Default** (Default)**Comment**: The value **Default** is the same as selecting **High confidence phishing messages**. Currently, in U.S. Government organizations (Microsoft 365 GCC, GCC High, and DoD), the value **Default** is the same as selecting **None**. |
| **Retain spam in quarantine for this many days** (*QuarantineRetentionPeriod*) | Show details<br>**Default**: 15 days**Standard**: 30 days**Strict**: 30 days**Comment**: This value also affects messages quarantined by anti-phishing policies. For more information, see [Quarantine retention](quarantine-about#quarantine-retention). |
| **Enable spam safety tips** (*InlineSafetyTipsEnabled*) | Show details<br>**Default**: Selected (`$true`)**Standard**: Selected (`$true`)**Strict**: Selected (`$true`) |
| Enable zero-hour auto purge (ZAP) for phishing messages (*PhishZapEnabled*) | Show details<br>**Default**: Selected (`$true`)**Standard**: Selected (`$true`)**Strict**: Selected (`$true`) |
| Enable ZAP for spam messages (*SpamZapEnabled*) | Show details<br>**Default**: Selected (`$true`)**Standard**: Selected (`$true`)**Strict**: Selected (`$true`) |
| **Allow & block list** |  |
| Allowed senders (*AllowedSenders*) | Show details<br>**Default**: None**Standard**: None**Strict**: None |
| Allowed sender domains (*AllowedSenderDomains*) | Show details<br>**Default**: None**Standard**: None**Strict**: None**Comment**: Adding domains to the allowed domains list is a bad idea. Attackers would be able to send you email that would otherwise be filtered out.Use the [spoof intelligence insight](anti-spoofing-spoof-intelligence) and the [Tenant Allow/Block List](tenant-allow-block-list-email-spoof-configure#spoofed-senders-in-the-tenant-allowblock-list) to review who's spoofing sender email addresses in your domains or external domains. |
| Blocked senders (*BlockedSenders*) | Show details<br>**Default**: None**Standard**: None**Strict**: None |
| Blocked sender domains (*BlockedSenderDomains*) | Show details<br>**Default**: None**Standard**: None**Strict**: None |

¹ As described in [Full access permissions and quarantine notifications](quarantine-policies#full-access-permissions-and-quarantine-notifications), your organization might use NotificationEnabledPolicy instead of DefaultFullAccessPolicy. Quarantine notifications are turned on in NotificationEnabledPolicy and turned off in DefaultFullAccessPolicy.

#### ASF settings in anti-spam policies

For more information about Advanced Spam Filter (ASF) settings in anti-spam policies, see [Advanced Spam Filter (ASF) settings in anti-spam policies](anti-spam-policies-asf-settings-about).

| Security feature name | Details |
| --- | --- |
| **Image links to remote sites** (*IncreaseScoreWithImageLinks*) | Show details<br>**Default**: Off**Recommended Standard**: Off**Recommended Strict**: Off |
| **Numeric IP address in URL** (*IncreaseScoreWithNumericIps*) | Show details<br>**Default**: Off**Recommended Standard**: Off**Recommended Strict**: Off |
| **URL redirect to other port** (*IncreaseScoreWithRedirectToOtherPort*) | Show details<br>**Default**: Off**Recommended Standard**: Off**Recommended Strict**: Off |
| **Links to .biz or .info websites** (*IncreaseScoreWithBizOrInfoUrls*) | Show details<br>**Default**: Off**Recommended Standard**: Off**Recommended Strict**: Off |
| **Empty messages** (*MarkAsSpamEmptyMessages*) | Show details<br>**Default**: Off**Recommended Standard**: Off**Recommended Strict**: Off |
| **Embed tags in HTML** (*MarkAsSpamEmbedTagsInHtml*) | Show details<br>**Default**: Off**Recommended Standard**: Off**Recommended Strict**: Off |
| **JavaScript or VBScript in HTML** (*MarkAsSpamJavaScriptInHtml*) | Show details<br>**Default**: Off**Recommended Standard**: Off**Recommended Strict**: Off |
| **Form tags in HTML** (*MarkAsSpamFormTagsInHtml*) | Show details<br>**Default**: Off**Recommended Standard**: Off**Recommended Strict**: Off |
| **Frame or iframe tags in HTML** (*MarkAsSpamFramesInHtml*) | Show details<br>**Default**: Off**Recommended Standard**: Off**Recommended Strict**: Off |
| **Web bugs in HTML** (*MarkAsSpamWebBugsInHtml*) | Show details<br>**Default**: Off**Recommended Standard**: Off**Recommended Strict**: Off |
| **Object tags in HTML** (*MarkAsSpamObjectTagsInHtml*) | Show details<br>**Default**: Off**Recommended Standard**: Off**Recommended Strict**: Off |
| **Sensitive words** (*MarkAsSpamSensitiveWordList*) | Show details<br>**Default**: Off**Recommended Standard**: Off**Recommended Strict**: Off |
| **SPF record: hard fail** (*MarkAsSpamSpfRecordHardFail*) | Show details<br>**Default**: Off**Recommended Standard**: Off**Recommended Strict**: Off |
| **Sender ID filtering hard fail** (*MarkAsSpamFromAddressAuthFail*) | Show details<br>**Default**: Off**Recommended Standard**: Off**Recommended Strict**: Off |
| **Backscatter** (*MarkAsSpamNdrBackscatter*) | Show details<br>**Default**: Off**Recommended Standard**: Off**Recommended Strict**: Off |
| **Test mode** (*TestModeAction*) | Show details<br>**Default**: None**Recommended Standard**: None**Recommended Strict**: None**Comment**: For ASF settings that support **Test** as an action, you can configure the test mode action to **None**, **Add default X-Header text**, or **Send Bcc message** (`None`, `AddXHeader`, or `BccMessage`). For more information, see [Enable, disable, or test ASF settings](anti-spam-policies-asf-settings-about#enable-disable-or-test-asf-settings). |

Note

ASF adds `X-CustomSpam:` X-header fields to messages *after* Exchange mail flow rules (also known as transport rules) processes messages, so you can't use mail flow rules to identify and act on messages filtered by ASF.

#### Outbound spam policy settings

To create and configure outbound spam policies, see [Configure outbound spam filtering](outbound-spam-policies-configure).

For more information about the default sending limits in the service, see [Sending limits](/en-us/office365/servicedescriptions/exchange-online-service-description/exchange-online-limits#sending-limits-1).

Note

Outbound spam policies aren't part of Standard or Strict preset security policies. The **Standard** and **Strict** values indicate our **recommended** values in the default outbound spam policy or custom outbound spam policies that you create.

| Security feature name | Details |
| --- | --- |
| **Set an external message limit** (*RecipientLimitExternalPerHour*) | Show details<br>**Default**: 0**Recommended Standard**: 500**Recommended Strict**: 400**Comment**: The default value 0 means use the service defaults. |
| **Set an internal message limit** (*RecipientLimitInternalPerHour*) | Show details<br>**Default**: 0**Recommended Standard**: 1000**Recommended Strict**: 800**Comment**: The default value 0 means use the service defaults. |
| **Set a daily message limit** (*RecipientLimitPerDay*) | Show details<br>**Default**: 0**Recommended Standard**: 1000**Recommended Strict**: 800**Comment**: The default value 0 means use the service defaults. |
| **Restriction placed on users who reach the message limit** (*ActionWhenThresholdReached*) | Show details<br>**Default**: **Restrict the user from sending mail until the following day** (`BlockUserForToday`)**Recommended Standard**: **Restrict the user from sending mail** (`BlockUser`)**Recommended Strict**: **Restrict the user from sending mail** (`BlockUser`) |
| **Automatic forwarding rules** (*AutoForwardingMode*) | Show details<br>**Default**: **Automatic - System-controlled** (`Automatic`)**Recommended Standard**: **Off - Forwarding is disabled** (`Off`)**Recommended Strict**: **Off - Forwarding is disabled** (`Off`)**Comment**: The behavior of **Automatic - System-controlled** (`Automatic`) can differ by organization. Configure **Off - Forwarding is disabled** (`Off`) to explicitly disable automatic external forwarding. For more information, see [Control automatic external email forwarding](outbound-spam-policies-external-email-forwarding). |
| **Send a copy of outbound messages that exceed these limits to these users and groups** (*BccSuspiciousOutboundMail* and *BccSuspiciousOutboundAdditionalRecipients*) | Show details<br>**Default**: Not selected (`$false` and Blank)**Recommended Standard**: Not selected (`$false` and Blank)**Recommended Strict**: Not selected (`$false` and Blank)**Comment**: This setting works only in the default outbound spam policy. It doesn't work in custom outbound spam policies that you create.The Microsoft SecureScore recommendation **Ensure Exchange Online Spam Policies are set to notify administrators** suggests that you configure this value. |
| **Notify these users and groups if a sender is blocked due to sending outbound spam** (*NotifyOutboundSpam* and *NotifyOutboundSpamRecipients*) | Show details<br>**Default**: Not selected (`$false` and Blank)**Recommended Standard**: Not selected (`$false` and Blank)**Recommended Strict**: Not selected (`$false` and Blank)**Comment**: The default [alert policy](/en-us/defender-xdr/alert-policies#threat-management-alert-policies) named **User restricted from sending email** already sends email notifications to members of the **TenantAdmins** group (**Global Administrator** members) when users are blocked due to exceeding the limits in the policy. For instructions, see [Verify the alert settings for restricted users](outbound-spam-restore-restricted-users#verify-the-alert-settings-for-restricted-users).Although we recommend that you use the alert policy rather than this setting in the outbound spam policy to notify admins and other users, the Microsoft SecureScore recommendation **Ensure Exchange Online Spam Policies are set to notify administrators** suggests that you configure this value. |

### Anti-phishing policy settings for all cloud mailboxes

The anti-phishing policy settings described in this section are part of [the built-in security features](eop-about) included in all organizations with cloud mailboxes. For more information about these settings, see [Spoof settings](anti-phishing-policies-about#spoof-settings). To configure these settings, see [Configure anti-phishing policies for all cloud mailboxes](anti-phishing-policies-eop-configure).

The spoof settings are inter-related, but the **Show first contact safety tip** setting has no dependency on spoof settings.

Quarantine policies define what users are able to do to quarantined messages, and whether users receive quarantine notifications. For more information, see [Anatomy of a quarantine policy](quarantine-policies#anatomy-of-a-quarantine-policy).

Although the **Apply quarantine policy** value appears unselected when you create an anti-phishing policy in the Defender portal, the quarantine policy named DefaultFullAccessPolicy¹ is used if you don't select a quarantine policy. This policy enforces the historical capabilities of messages quarantined as spoof as described in the table [in this article](quarantine-end-user). When you later view or edit the anti-phishing policy settings, the quarantine policy name is shown.

Admins can create or use quarantine policies with more restrictive or less restrictive capabilities. For instructions, see [Create quarantine policies in the Microsoft Defender portal](quarantine-policies#step-1-create-quarantine-policies-in-the-microsoft-defender-portal).

| Security feature name | Details |
| --- | --- |
| **Spoof** |  |
| **Enable spoof intelligence** (*EnableSpoofIntelligence*) | Show details<br>**Default**: Selected (`$true`)**Standard**: Selected (`$true`)**Strict**: Selected (`$true`) |
| **Actions** |  |
| **Honor DMARC record policy when the message is detected as spoof** (*HonorDmarcPolicy*) | Show details<br>**Default**: Selected (`$true`)**Standard**: Selected (`$true`)**Strict**: Selected (`$true`)**Comment**: When this setting is turned on, you control what happens to messages where the sender fails explicit [DMARC](email-authentication-dmarc-configure) checks when the policy action in the DMARC TXT record is set to `p=quarantine` or `p=reject`. For more information, see [Spoof protection and sender DMARC policies](anti-phishing-policies-about#spoof-protection-and-sender-dmarc-policies). |
| **If the message is detected as spoof and DMARC Policy is set as p=quarantine** (*DmarcQuarantineAction*) | Show details<br>**Default**: **Quarantine the message** (`Quarantine`)**Standard**: **Quarantine the message** (`Quarantine`)**Strict**: **Quarantine the message** (`Quarantine`)**Comment**: This action is meaningful only when **Honor DMARC record policy when the message is detected as spoof** is turned on. |
| **If the message is detected as spoof and DMARC Policy is set as p=reject** (*DmarcRejectAction*) | Show details<br>**Default**: **Reject the message** (`Reject`)**Standard**: **Reject the message** (`Reject`)**Strict**: **Reject the message** (`Reject`)**Comment**: This action is meaningful only when **Honor DMARC record policy when the message is detected as spoof** is turned on. |
| **If the message is detected as spoof by spoof intelligence** (*AuthenticationFailAction*) | Show details<br>**Default**: **Move the message to the recipients' Junk Email folders** (`MoveToJmf`)**Standard**: **Move the message to the recipients' Junk Email folders** (`MoveToJmf`)**Strict**: **Quarantine the message** (`Quarantine`)**Comment**: This setting applies to spoofed senders that were automatically blocked as shown in the [spoof intelligence insight](anti-spoofing-spoof-intelligence) or manually blocked in the [Tenant Allow/Block List](tenant-allow-block-list-email-spoof-configure#create-block-entries-for-spoofed-senders).If you select **Quarantine the message** as the action for the spoof verdict, an **Apply quarantine policy** box is available. |
| **Quarantine policy** for **Spoof** (*SpoofQuarantineTag*) | Show details<br>**Default**: DefaultFullAccessPolicy¹**Standard**: DefaultFullAccessPolicy**Strict**: DefaultFullAccessWithNotificationPolicy**Comment**: The quarantine policy is meaningful only if spoof detections are quarantined. |
| **Show first contact safety tip** (*EnableFirstContactSafetyTips*) | Show details<br>**Default**: Not selected (`$false`)**Standard**: Selected (`$true`)**Strict**: Selected (`$true`)**Comment**: For more information, see [First contact safety tip](anti-phishing-policies-about#first-contact-safety-tip). |
| **Show (?) for unauthenticated senders for spoof** (*EnableUnauthenticatedSender*) | Show details<br>**Default**: Selected (`$true`)**Standard**: Selected (`$true`)**Strict**: Selected (`$true`)**Comment**: Adds a question mark (?) to the sender's photo in Outlook for unidentified spoofed senders. For more information, see [Unauthenticated sender indicators](anti-phishing-policies-about#unauthenticated-sender-indicators). |
| **Show "via" tag** (*EnableViaTag*) | Show details<br>**Default**: Selected (`$true`)**Standard**: Selected (`$true`)**Strict**: Selected (`$true`)**Comment**: Adds a via tag (`chris@contoso.com via fabrikam.com`) to the From address if it's different from the domain in the DKIM signature or the **MAIL FROM** address.For more information, see [Unauthenticated sender indicators](anti-phishing-policies-about#unauthenticated-sender-indicators). |

¹ As described in [Full access permissions and quarantine notifications](quarantine-policies#full-access-permissions-and-quarantine-notifications), your organization might use NotificationEnabledPolicy instead of DefaultFullAccessPolicy. Quarantine notifications are turned on in NotificationEnabledPolicy and turned off in DefaultFullAccessPolicy.

## Microsoft Defender for Office 365 security

If your Microsoft 365 subscription includes Defender for Office 365 or you purchased Defender for Office 365 as an add-on, you get the extra security features as described in the following subsections. For the latest news and information about Defender for Office 365 features, see [What's new in Defender for Office 365](defender-for-office-365-whats-new).

Important

- The default anti-phishing policy in Defender for Office 365 provides [spoof protection](anti-phishing-policies-about#spoof-settings) and mailbox intelligence for all recipients. However, the other available impersonation protection and phishing email thresholds settings aren't configured in the default policy. To enable all anti-phishing protection features, do one or more of the following steps:

    - Turn on and use the Standard and/or Strict [preset security policies](preset-security-policies) and configure impersonation protection there.
    - Modify the default anti-phishing policy.
    - Create custom anti-phishing policies.
- Although there's no default Safe Attachments policy or Safe Links policy, the **Built-in protection** preset security policy provides Safe Attachments protection and Safe Links protection to all recipients who aren't defined in the Standard preset security policy, the Strict preset security policy, or in custom Safe Attachments or Safe Links policies. For more information, see [Preset security policies](preset-security-policies).
- [Safe Attachments for SharePoint, OneDrive, and Microsoft Teams](safe-attachments-for-spo-odfb-teams-about) protection and [Safe Documents](safe-documents-in-e5-plus-security-about) protection have no dependencies on Safe Links policies.
- Microsoft Teams protection settings in Microsoft Defender for Office 365 have no dependency on preset security policies, any custom threat policies, or the default threat policies.

We recommend the Standard or Strict configurations for Defender for Office 365 as described in the tables in the following subsections.

### Anti-phishing policy settings in Microsoft Defender for Office 365

All Microsoft 365 organizations with cloud mailboxes get anti-phishing protection as previously described. But Defender for Office 365 includes more features and control to help prevent, detect, and remediate phishing attacks. To create and configure these anti-phishing policies, see [Configure anti-phishing policies in Defender for Office 365](anti-phishing-policies-mdo-configure).

#### Phishing email thresholds in anti-phishing policies in Microsoft Defender for Office 365

For more information about this setting, see [Phishing email thresholds in anti-phishing policies in Microsoft Defender for Office 365](anti-phishing-policies-about#phishing-email-thresholds-in-anti-phishing-policies-in-microsoft-defender-for-office-365). To configure this setting, see [Configure anti-phishing policies in Defender for Office 365](anti-phishing-policies-mdo-configure).

| Security feature name | Details |
| --- | --- |
| **Phishing email threshold** (*PhishThresholdLevel*) | **Default**: **1 - Standard** (`1`)**Standard**: **3 - More aggressive** (`3`)**Strict**: **4 - Most aggressive** (`4`) |

#### Impersonation settings in anti-phishing policies in Microsoft Defender for Office 365

For more information about these settings, see [Impersonation settings in anti-phishing policies in Microsoft Defender for Office 365](anti-phishing-policies-about#impersonation-settings-in-anti-phishing-policies-in-microsoft-defender-for-office-365). To configure these settings, see [Configure anti-phishing policies in Defender for Office 365](anti-phishing-policies-mdo-configure).

Wherever you select **Quarantine the message** as the action for an impersonation verdict, an **Apply quarantine policy** box is available. Quarantine policies define what users are able to do to quarantined messages, and whether users receive quarantine notifications. For more information, see [Anatomy of a quarantine policy](quarantine-policies#anatomy-of-a-quarantine-policy).

Although the **Apply quarantine policy** value appears unselected when you create an anti-phishing policy in the Defender portal, the quarantine policy named DefaultFullAccessPolicy is used if you don't select a quarantine policy. This policy enforces the historical capabilities of messages quarantined as impersonation as described in the table [in this article](quarantine-end-user). When you later view or edit the anti-phishing policy settings, the quarantine policy name is shown.

Admins can create or use quarantine policies with more restrictive or less restrictive capabilities. For instructions, see [Create quarantine policies in the Microsoft Defender portal](quarantine-policies#step-1-create-quarantine-policies-in-the-microsoft-defender-portal).

| Security feature name | Details |
| --- | --- |
| **Impersonation** |  |
| User impersonation protection: **Enable users to protect** (*EnableTargetedUserProtection* and *TargetedUsersToProtect*) | Show details<br>**Default**: Not selected (`$false` and none)**Standard**: Selected (`$true` and &lt;list of users&gt;)**Strict**: Selected (`$true` and &lt;list of users&gt;)**Comment**: We recommend adding users (message senders) in key roles. Internally, protected senders might be your CEO, CFO, and other senior leaders. Externally, protected senders could include council members or your board of directors. |
| Domain impersonation protection: **Enable domains to protect** | Show details<br>**Default**: Not selected**Standard**: Selected**Strict**: Selected |
| **Include domains I own** (*EnableOrganizationDomainsProtection*) | Show details<br>**Default**: Off (`$false`)**Standard**: Selected (`$true`)**Strict**: Selected (`$true`) |
| **Include custom domains** (*EnableTargetedDomainsProtection* and *TargetedDomainsToProtect*) | Show details<br>**Default**: Off (`$false` and none)**Standard**: Selected (`$true` and &lt;list of domains&gt;)**Strict**: Selected (`$true` and &lt;list of domains&gt;)**Comment**: We recommend adding domains (sender domains) that you don't own, but you frequently interact with. |
| **Add trusted senders and domains** (*ExcludedSenders* and *ExcludedDomains*) | Show details<br>**Default**: None**Standard**: None**Strict**: None**Comment**: Depending on your organization, we recommend adding senders or domains that are incorrectly identified as impersonation attempts. |
| **Enable mailbox intelligence** (*EnableMailboxIntelligence*) | Show details<br>**Default**: Selected (`$true`)**Standard**: Selected (`$true`)**Strict**: Selected (`$true`) |
| **Enable intelligence for impersonation protection** (*EnableMailboxIntelligenceProtection*) | Show details<br>**Default**: Off (`$false`)**Standard**: Selected (`$true`)**Strict**: Selected (`$true`)**Comment**: This setting allows the specified action for impersonation detections by mailbox intelligence. |
| **Actions** |  |
| **If a message is detected as user impersonation** (*TargetedUserProtectionAction*) | Show details<br>**Default**: **Don't apply any action** (`NoAction`)**Standard**: **Quarantine the message** (`Quarantine`)**Strict**: **Quarantine the message** (`Quarantine`) |
| **Quarantine policy** for **user impersonation** (*TargetedUserQuarantineTag*) | Show details<br>**Default**: DefaultFullAccessPolicy¹**Standard**: DefaultFullAccessWithNotificationPolicy**Strict**: DefaultFullAccessWithNotificationPolicy**Comment**: The quarantine policy is meaningful only if user impersonation detections are quarantined. |
| **If a message is detected as domain impersonation** (*TargetedDomainProtectionAction*) | Show details<br>**Default**: **Don't apply any action** (`NoAction`)**Standard**: **Quarantine the message** (`Quarantine`)**Strict**: **Quarantine the message** (`Quarantine`) |
| **Quarantine policy** for **domain impersonation** (*TargetedDomainQuarantineTag*) | Show details<br>**Default**: DefaultFullAccessPolicy¹**Standard**: DefaultFullAccessWithNotificationPolicy**Strict**: DefaultFullAccessWithNotificationPolicy**Comment**: The quarantine policy is meaningful only if domain impersonation detections are quarantined. |
| **If mailbox intelligence detects an impersonated user** (*MailboxIntelligenceProtectionAction*) | Show details<br>**Default**: **Don't apply any action** (`NoAction`)**Standard**: **Move the message to the recipients' Junk Email folders** (`MoveToJmf`)**Strict**: **Quarantine the message** (`Quarantine`) |
| **Quarantine policy** for **mailbox intelligence impersonation** (*MailboxIntelligenceQuarantineTag*) | Show details<br>**Default**: DefaultFullAccessPolicy¹**Standard**: DefaultFullAccessPolicy**Strict**: DefaultFullAccessWithNotificationPolicy**Comment**: The quarantine policy is meaningful only if mailbox intelligence detections are quarantined. |
| **Show user impersonation safety tip** (*EnableSimilarUsersSafetyTips*) | Show details<br>**Default**: Off (`$false`)**Standard**: Selected (`$true`)**Strict**: Selected (`$true`) |
| **Show domain impersonation safety tip** (*EnableSimilarDomainsSafetyTips*) | Show details<br>**Default**: Off (`$false`)**Standard**: Selected (`$true`)**Strict**: Selected (`$true`) |
| **Show user impersonation unusual characters safety tip** (*EnableUnusualCharactersSafetyTips*) | Show details<br>**Default**: Off (`$false`)**Standard**: Selected (`$true`)**Strict**: Selected (`$true`) |

¹ As described in [Full access permissions and quarantine notifications](quarantine-policies#full-access-permissions-and-quarantine-notifications), your organization might use NotificationEnabledPolicy instead of DefaultFullAccessPolicy. Quarantine notifications are turned on in NotificationEnabledPolicy and turned off in DefaultFullAccessPolicy.

#### Anti-phishing policy settings for all cloud mailboxes in Defender for Office 365

The previously described anti-phishing policy settings for all cloud mailboxes are also available in Defender for Office 365.

### Safe Attachments settings

Safe Attachments in Defender for Office 365 includes global settings that have no relationship to Safe Attachments policies, and settings that are specific to each Safe Attachments policy. For more information, see [Safe Attachments in Microsoft Defender for Office 365](safe-attachments-about).

Although there's no default Safe Attachments policy, the **Built-in protection** preset security policy provides Safe Attachments protection to all recipients who aren't defined in the Standard or Strict preset security policies or in custom Safe Attachments policies. For more information, see [Preset security policies](preset-security-policies).

#### Global settings for Safe Attachments

Note

The global settings for Safe Attachments are set by the **Built-in protection** preset security policy, but not by the **Standard** or **Strict** preset security policies. Either way, admins can modify these global Safe Attachments settings at any time.

The **Default** column in the following table shows the values before the existence of the **Built-in protection** preset security policy. The **Built-in protection** column shows the values that are set by the **Built-in protection** preset security policy, which are also our recommended values.

To configure these settings, see [Turn on Safe Attachments for SharePoint, OneDrive, and Microsoft Teams](safe-attachments-for-spo-odfb-teams-configure) and [Safe Documents in Microsoft 365 E5](safe-documents-in-e5-plus-security-about).

In [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell), you use the [Set-AtpPolicyForO365](/en-us/powershell/module/exchangepowershell/set-atppolicyforo365) cmdlet for these settings.

| Security feature name | Details |
| --- | --- |
| **Turn on Defender for Office 365 for SharePoint, OneDrive, and Microsoft Teams** (*EnableATPForSPOTeamsODB*) | Show details<br>**Default**: Off (`$false`)**Built-in protection**: On (`$true`)**Comment**: To prevent users from downloading malicious files, see [Use SharePoint Online PowerShell to prevent users from downloading malicious files](safe-attachments-for-spo-odfb-teams-configure#step-2-recommended-use-sharepoint-online-powershell-to-prevent-users-from-downloading-malicious-files). |
| **Turn on Safe Documents for Office clients** (*EnableSafeDocs*) | Show details<br>**Default**: Off (`$false`)**Built-in protection**: On (`$true`)**Comment**: This feature is available and meaningful only with licenses that aren't included in Defender for Office 365 (for example, Microsoft 365 A5 or Microsoft Defender Suite). For more information, see [Safe Documents in Microsoft 365 A5 or E5 Security](safe-documents-in-e5-plus-security-about). |
| **Allow people to click through Protected View even if Safe Documents identified the file as malicious** (*AllowSafeDocsOpen*) | Show details<br>**Default**: Off (`$false`)**Built-in protection**: Off (`$false`)**Comment**: This setting is related to Safe Documents. |

#### Safe Attachments policy settings

To configure these settings, see [Set up Safe Attachments policies in Defender for Office 365](safe-attachments-policies-configure).

In [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell), you use the [New-SafeAttachmentPolicy](/en-us/powershell/module/exchangepowershell/new-safeattachmentpolicy) and [Set-SafeAttachmentPolicy](/en-us/powershell/module/exchangepowershell/set-safelinkspolicy) cmdlets for these settings.

Note

As described earlier, although there's no default Safe Attachments policy, the **Built-in protection** preset security policy provides Safe Attachments protection to all recipients who aren't defined in the Standard preset security policy, the Strict preset security policy, or in custom Safe Attachments policies.

The **Default in custom** column in the following table refers to the default values in new Safe Attachments policies that you create. The remaining columns indicate (unless otherwise noted) the values that are configured in the corresponding preset security policies.

Quarantine policies define what users are able to do to quarantined messages, and whether users receive quarantine notifications. For more information, see [Anatomy of a quarantine policy](quarantine-policies#anatomy-of-a-quarantine-policy).

The policy named AdminOnlyAccessPolicy enforces the historical capabilities of messages quarantined as malware as described in the table [in this article](quarantine-end-user).

Users can't release their own messages quarantined as malware or phishing by Safe Attachments, regardless of how the quarantine policy is configured. If the policy is configured for users to release these quarantined messages, users are instead allowed to *request* the release of these quarantined messages.

| Security feature name | Details |
| --- | --- |
| **Safe Attachments unknown malware response** (*Enable* and *Action*) | Show details<br>**Default in custom**: **Off** (`-Enable $false` and `-Action Block`)**Built-in protection**: **Block** (`-Enable $true` and `-Action Block`)**Standard**: **Block** (`-Enable $true` and `-Action Block`)**Strict**: **Block** (`-Enable $true` and `-Action Block`)**Comment**: When the *Enable* parameter is $false, the value of the *Action* parameter doesn't matter. |
| **Quarantine policy** (*QuarantineTag*) | Show details<br>**Default in custom**: AdminOnlyAccessPolicy**Built-in protection**: AdminOnlyAccessPolicy**Standard**: AdminOnlyAccessPolicy**Strict**: AdminOnlyAccessPolicy |
| **Redirect attachment with detected attachments** : **Enable redirect** (*Redirect* and *RedirectAddress*) | Show details<br>**Default in custom**: Not selected and no email address specified. (`-Redirect $false` and *RedirectAddress* is blank)**Built-in protection**: Not selected and no email address specified. (`-Redirect $false` and *RedirectAddress* is blank)**Standard**: Not selected and no email address specified. (`-Redirect $false` and *RedirectAddress* is blank)**Strict**: Not selected and no email address specified. (`-Redirect $false` and *RedirectAddress* is blank)**Comment**: Redirection of messages is available only when the **Safe Attachments unknown malware response** value is **Monitor** (`-Enable $true` and `-Action Allow`). |
| **Block messages containing encrypted attachments that could not be scanned** | This section and the following settings are available only when the **Safe Attachments unknown malware response** value is **Block** (`-Enable $true` and `-Action Block`). |
| **Block unscanned attachments** (*EnableBlockingEncryptedAttachments*) | Show details<br>**Default in custom**: Not selected (`$false`)**Built-in protection**: Not selected (`$false`)**Standard**: Not selected (`$false`)**Strict**: Not selected (`$false`) |
| **Exclude these attachment types** (*ExcludedTypesFromBlockingEncryptedAttachments*) | Show details<br>**Default in custom**: None selected (`{}`)**Built-in protection**: None selected (`{}`)**Standard**: None selected (`{}`)**Strict**: None selected (`{}`) |
| **Quarantine policy** (*QuarantineTagForBlockingEncryptedAttachments*) | Show details<br>**Default in custom**: DefaultFullAccessWithNotificationPolicy**Built-in protection**: DefaultFullAccessWithNotificationPolicy**Standard**: DefaultFullAccessWithNotificationPolicy**Strict**: DefaultFullAccessWithNotificationPolicy**Comment**: This quarantine policy applies only to messages quarantined by Safe Attachments because they contain encrypted (password-protected) attachments that can't be scanned. |

### Safe Links policy settings

For more information about Safe Links protection, see [Safe Links in Defender for Office 365](safe-links-about).

Although there's no default Safe Links policy, the **Built-in protection** preset security policy provides Safe Links protection to all recipients who aren't defined in the Standard preset security policy, the Strict preset security policy or in custom Safe Links policies. For more information, see [Preset security policies](preset-security-policies).

To configure Safe Links policy settings, see [Set up Safe Links policies in Microsoft Defender for Office 365](safe-links-policies-configure).

In [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell), you use the [New-SafeLinksPolicy](/en-us/powershell/module/exchangepowershell/new-safelinkspolicy) and [Set-SafeLinksPolicy](/en-us/powershell/module/exchangepowershell/set-safelinkspolicy) cmdlets for Safe Links policy settings.

Note

The **Default in custom** column refers to the default values in new Safe Links policies you create. The remaining columns indicate the values configured in the corresponding preset security policies.

| Security feature name | Details |
| --- | --- |
| **URL & click protection settings** |  |
| **Email** | **Comment**: The settings in this section affect URL rewriting and time of click protection in email messages. |
| **On: Safe Links checks a list of known, malicious links when users click links in email. URLs are rewritten by default.** (*EnableSafeLinksForEmail*) | Show details<br>**Default in custom**: Selected (`$true`)**Built-in protection**: Selected (`$true`)**Standard**: Selected (`$true`)**Strict**: Selected (`$true`) |
| **Apply Safe Links to email messages sent within the organization** (*EnableForInternalSenders*) | Show details<br>**Default in custom**: Selected (`$true`)**Built-in protection**: Not Selected (`$false`)**Standard**: Selected (`$true`)**Strict**: Selected (`$true`) |
| **Apply real-time URL scanning for suspicious links and links that point to files** (*ScanUrls*) | Show details<br>**Default in custom**: Selected (`$true`)**Built-in protection**: Selected (`$true`)**Standard**: Selected (`$true`)**Strict**: Selected (`$true`) |
| **Wait for URL scanning to complete before delivering the message** (*DeliverMessageAfterScan*) | Show details<br>**Default in custom**: Selected (`$true`)**Built-in protection**: Selected (`$true`)**Standard**: Selected (`$true`)**Strict**: Selected (`$true`) |
| **Do not rewrite URLs, do checks via Safe Links API only** (*DisableURLRewrite*) | Show details<br>**Default in custom**: Selected (`$false`)^\*^**Built-in protection**: Selected (`$true`)**Standard**: Not selected (`$false`)**Strict**: Not selected (`$false`)**Comment**: ^\*^ In new policies created in the Defender portal, this setting is selected by default. In new policies created in PowerShell, the default value is `$false`. |
| **Do not rewrite the following URLs in email** (*DoNotRewriteUrls*) | Show details<br>**Default in custom**: Blank**Built-in protection**: Blank**Standard**: Blank**Strict**: Blank**Comment**: We have no specific recommendation for this setting.**Note**: Safe Links doesn't scan or wrap entries in the "Don't rewrite the following URLs" list during mail flow. Report the URL as **I've confirmed it's clean** and then select **Allow this URL** to add an allow entry to the Tenant Allow/Block List so the URL isn't scanned or wrapped by Safe Links during mail flow *and* at time of click. For instructions, see [Report good URLs to Microsoft](submissions-admin#report-good-urls-to-microsoft). |
| **Teams** | **Comment**: The setting in this section affects time of click protection in Microsoft Teams. |
| **On: Safe Links checks a list of known, malicious links when users click links in Microsoft Teams. URLs are not rewritten.** (*EnableSafeLinksForTeams*) | Show details<br>**Default in custom**: Selected (`$true`)**Built-in protection**: Selected (`$true`)**Standard**: Selected (`$true`)**Strict**: Selected (`$true`) |
| **Office 365 apps** | **Comment**: The setting in this section affects time of click protection in Office apps. |
| **On: Safe Links checks a list of known, malicious links when users click links in Microsoft Office apps. URLs are not rewritten.** (*EnableSafeLinksForOffice*) | Show details<br>**Default in custom**: Selected (`$true`)**Built-in protection**: Selected (`$true`)**Standard**: Selected (`$true`)**Strict**: Selected (`$true`)**Comment**: Use Safe Links in supported Office 365 desktop and mobile (iOS and Android) apps. For more information, see [Safe Links settings for Office apps](safe-links-about#safe-links-settings-for-office-apps). |
| **Click protection settings** |  |
| **Track user clicks** (*TrackClicks*) | Show details<br>**Default in custom**: Selected (`$true`)**Built-in protection**: Selected (`$true`)**Standard**: Selected (`$true`)**Strict**: Selected (`$true`) |
| **Let users click through to the original URL** (*AllowClickThrough*) | Show details<br>**Default in custom**: Selected (`$false`)^\*^**Built-in protection**: Selected (`$true`)**Standard**: Not selected (`$false`)**Strict**: Not selected (`$false`)**Comment**: ^\*^ In new policies created in the Defender portal, this setting is selected by default. In new policies created in PowerShell, the default value is `$false`. |
| **Display the organization branding on notification and warning pages** (*EnableOrganizationBranding*) | Show details<br>**Default in custom**: Not selected (`$false`)**Built-in protection**: Not selected (`$false`)**Standard**: Not selected (`$false`)**Strict**: Not selected (`$false`)**Comment**: We have no specific recommendation for this setting.Before you turn on this setting, you need to follow the instructions in [Customize the Microsoft 365 theme for your organization](/en-us/microsoft-365/admin/setup/customize-your-organization-theme) to upload your company logo. |
| **Notification** |  |
| **How would you like to notify your users?** (*CustomNotificationText* and *UseTranslatedNotificationText*) | Show details<br>**Default in custom**: **Use the default notification text** (Blank and `$false`)**Built-in protection**: **Use the default notification text** (Blank and `$false`)**Standard**: **Use the default notification text** (Blank and `$false`)**Strict**: **Use the default notification text** (Blank and `$false`)**Comment**: We have no specific recommendation for this setting.You can select **Use custom notification text** (`-CustomNotificationText "<Custom text>"`) to enter and use customized notification text. If you specify custom text, you can also select **Use Microsoft Translator for automatic localization** (`-UseTranslatedNotificationText $true`) to automatically translate the text into the user's language. |

### Microsoft Teams protection settings in Microsoft Defender for Office 365

For more information about Microsoft Teams protection, see [Microsoft Defender for Office 365 support for Microsoft Teams](mdo-support-teams-about).

In [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell), you use the [New-TeamsProtectionPolicy](/en-us/powershell/module/exchangepowershell/new-teamsprotectionpolicy) and [Set-TeamsProtectionPolicy](/en-us/powershell/module/exchangepowershell/set-teamsprotectionpolicy) cmdlets for Microsoft Teams protection settings.

Note

Microsoft Teams protection isn't part of the Standard or Strict preset security policies, any custom threat policies, or the default threat policies. The **Standard** and **Strict** values indicate our **recommended** values.

| Security feature name | Details |
| --- | --- |
| **Zero-hour auto purge (ZAP)** (*ZapEnabled*) | Show details<br>**Default**: **On** (`$true`)**Standard**: **On** (`$true`)**Strict**: **On** (`$true`) |
| **Quarantine policies** |  |
| **Malware** (*MalwareQuarantineTag*) | Show details<br>**Default**: AdminOnlyAccessPolicy**Standard**: AdminOnlyAccessPolicy**Strict**: AdminOnlyAccessPolicy |
| **High confidence phishing** (*HighConfidencePhishQuarantineTag*) | Show details<br>**Default**: AdminOnlyAccessPolicy**Standard**: AdminOnlyAccessPolicy**Strict**: AdminOnlyAccessPolicy |