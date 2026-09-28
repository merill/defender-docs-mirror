---
layout: Conceptual
title: ASF settings in anti-spam policies - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/anti-spam-policies-asf-settings-about
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
ms.assetid: b286f853-b484-4af0-b01f-281fffd85e7a
ms.collection:
- m365-security
- tier2
ms.custom:
- seo-marvel-apr2020
- msecd-doc-authoring-1015
description: Advanced Spam Filter (ASF) settings in anti-spam policies mark messages as spam based on properties common in spam. Learn what each ASF setting does.
ms.service: defender-office-365
ms.date: 2026-08-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: abfd1841-a762-e6b0-ad50-90ea7a37fe63
document_version_independent_id: abfd1841-a762-e6b0-ad50-90ea7a37fe63
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/anti-spam-policies-asf-settings-about.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: anti-spam-policies-asf-settings-about
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/anti-spam-policies-asf-settings-about.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 709dec83-1245-7bd6-d388-34dfc271c662
---

# ASF settings in anti-spam policies - Microsoft Defender for Office 365 | Microsoft Learn

In all organizations with cloud mailboxes, Advanced Spam Filter (ASF) settings in anti-spam policies allow admins to mark messages as spam based on specific message properties. ASF specifically targets these properties because they're commonly found in spam. Depending on the property, ASF detections mark the message as **Spam** or **High confidence spam**.

Note

Enabling one or more of the ASF settings is an aggressive approach to spam filtering. You can't report messages that are filtered by ASF as false positives to Microsoft. You can identify messages that were filtered by ASF by:

- Periodic quarantine notifications from spam and high confidence spam filter verdicts.
- The presence of filtered messages in quarantine.
- The specific `X-CustomSpam:` X-header fields that are added to messages as described in this article.

ASF adds `X-CustomSpam:` X-header fields to messages *after* the messages have been processed by Exchange mail flow rules (also known as transport rules), so you can't use mail flow rules to identify and act on messages that were filtered by ASF. You can use [Inbox rules](https://support.microsoft.com/office/8400435c-f14e-4272-9004-1548bb1848f2) in mailboxes to affect the delivery of the message.

The following sections describe the ASF settings and options that are available in anti-spam policies in the Microsoft Defender portal, and in [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell) ([New-HostedContentFilterPolicy](/en-us/powershell/module/exchangepowershell/new-hostedcontentfilterpolicy) and [Set-HostedContentFilterPolicy](/en-us/powershell/module/exchangepowershell/set-hostedcontentfilterpolicy)).

For more information, see [Configure anti-spam policies](anti-spam-policies-configure). For troubleshooting information about ASF false positives, see [ASF settings that cause false positives](anti-spam-policies-troubleshooting#asf-settings-that-cause-false-positives).

Tip

ASF settings aren't enabled in [Standard or Strict preset security policies](preset-security-policies), so you can configure ASF settings in the default anti-spam policy or custom anti-spam policies only. For more information about using threat policies, see [Determine your threat policy strategy](mdo-deployment-guide#determine-your-threat-policy-strategy).

## Enable, disable, or test ASF settings

For each ASF setting, the following options are available in anti-spam policies:

- **On**: ASF adds the corresponding X-header field to the message:

    - For Increase spam score settings, the message has a higher chance of being marked as **Spam**.
    - For Mark as spam settings, the message is marked as **Spam** or **High confidence spam**.
- **Off**: The ASF setting is disabled. This value is the default.
- **Test**: The ASF setting is in Test mode. What happens to the message is determined by the **Test mode** (*TestModeAction*) value:

    - **None**: Message delivery is unaffected by the ASF detection. The message is still subject to other types of filtering and rules.
    - **Add default X-header text** (*AddXHeader*): The X-header value `X-CustomSpam: This message was filtered by the custom spam filter option` is added to the message. You can use this value in Inbox rules (not mail flow rules) to affect the delivery of the message.
    - **Send Bcc message** (*BccMessage*): The specified email addresses (the *TestModeBccToRecipients* parameter value in PowerShell) are added to the Bcc field of the message, and the message is delivered to the additional Bcc recipients. In the Microsoft Defender portal, you separate multiple email addresses by semicolons (;). In PowerShell, you separate multiple email addresses by commas.

    Test mode isn't available for the following ASF settings:

    - **Conditional Sender ID filtering: hard fail** (*MarkAsSpamFromAddressAuthFail*)
    - **NDR backscatter** (*MarkAsSpamNdrBackscatter*)
    - **SPF record: hard fail** (*MarkAsSpamSpfRecordHardFail*)

    The same test mode action is applied to *all* ASF settings that are set to **Test**. You can't configure different test mode actions for different ASF settings.

## Increase spam score settings

The following **Increase spam score** ASF settings mark matching messages as spam and apply the corresponding action in anti-spam policies, unless another detection results in a higher-priority verdict.

| Anti-spam policy setting | Description | X-header added |
| --- | --- | --- |
| **Image links to remote websites** (*IncreaseScoreWithImageLinks*) | Messages that contain `<Img>` HTML tag links to remote sites (for example, using http) are marked as spam. | `X-CustomSpam: Image links to remote sites` |
| **Numeric IP address in URL** (*IncreaseScoreWithNumericIps*) | Messages that contain numeric-based URLs (typically, IP addresses) are marked as spam. | `X-CustomSpam: Numeric IP in URL` |
| **URL redirect to other port** (*IncreaseScoreWithRedirectToOtherPort*) | Messages that contain hyperlinks that redirect to TCP ports other than 80 (HTTP), 8080 (alternate HTTP), or 443 (HTTPS) are marked as spam. | `X-CustomSpam: URL redirect to other port` |
| **Links to .biz or .info websites** (*IncreaseScoreWithBizOrInfoUrls*) | Messages that contain `.biz` or `.info` links in the body of the message are marked as spam.  URLs such as `contoso.info.com` (where `.biz` or `.info` isn't the top-level domain) also match. | `X-CustomSpam: URL to .biz or .info websites` |

## Mark as spam settings

The following **Mark as spam** ASF settings mark detected messages with a **High confidence spam** filter verdict and the corresponding action in anti-spam policies.

| Anti-spam policy setting | Description | X-header added |
| --- | --- | --- |
| **Empty messages** (*MarkAsSpamEmptyMessages*) | Messages with no subject, no content in the message body, and no attachments are marked as high confidence spam. | `X-CustomSpam: Empty Message` |
| **Embedded tags in HTML** (*MarkAsSpamEmbedTagsInHtml*) | Messages that contain `<embed>` HTML tags are marked as high confidence spam.  This tag allows the embedding of different kinds of documents in an HTML document (for example, sounds, videos, or pictures). | `X-CustomSpam: Embed tag in html` |
| **JavaScript or VBScript in HTML** (*MarkAsSpamJavaScriptInHtml*) | Messages that use JavaScript or Visual Basic Script Edition in HTML are marked as high confidence spam.  These scripting languages are used in email messages to cause specific actions to automatically occur. | `X-CustomSpam: Javascript or VBscript tags in HTML` |
| **Form tags in HTML** (*MarkAsSpamFormTagsInHtml*) | Messages that contain `<form>` HTML tags are marked as high confidence spam.  This tag is used to create website forms. Email advertisements often include this tag to solicit information from the recipient. | `X-CustomSpam: Form tag in html` |
| **Frame or iframe tags in HTML** (*MarkAsSpamFramesInHtml*) | Messages that contain `<frame>` or `<iframe>` HTML tags are marked as high confidence spam.  These tags are used in email messages to format the page for displaying text or graphics. | `X-CustomSpam: IFRAME or FRAME in HTML` |
| **Web bugs in HTML** (*MarkAsSpamWebBugsInHtml*) | A *web bug* (also known as a *web beacon*) is a graphic element (often as small as one pixel by one pixel) that determines whether the recipient read the message.  Messages that contain web bugs are marked as high confidence spam.  Legitimate newsletters might use web bugs, although many consider them an invasion of privacy. | `X-CustomSpam: Web bug` |
| **Object tags in HTML** (*MarkAsSpamObjectTagsInHtml*) | Messages that contain `<object>` HTML tags are marked as high confidence spam.  This tag allows plug-ins or applications to run in an HTML window. | `X-CustomSpam: Object tag in html` |
| **Sensitive words** (*MarkAsSpamSensitiveWordList*) | Microsoft maintains a dynamic but non-editable list of words that are associated with potentially offensive messages.  Messages that contain words from the sensitive word list in the subject or message body are marked as high confidence spam. | `X-CustomSpam: Sensitive word in subject/body` |
| **SPF record: hard fail** (*MarkAsSpamSpfRecordHardFail*) | Messages sent from an IP address that isn't specified in the Sender Policy Framework (SPF) record in DNS for the source email domain are marked as high confidence spam.  Test mode isn't available for this setting. | `X-CustomSpam: SPF Record Fail` |

The following **Mark as spam** ASF settings mark detected messages with a **Spam** filter verdict and the corresponding action in anti-spam policies.

| Anti-spam policy setting | Description | X-header added |
| --- | --- | --- |
| **Sender ID filtering hard fail** (*MarkAsSpamFromAddressAuthFail*) | Messages that hard fail a conditional Sender ID check are marked as spam.  This setting combines an SPF check with a Sender ID check to help protect against message headers that contain forged senders.  Test mode isn't available for this setting. | `X-CustomSpam: SPF From Record Fail` |
| **Backscatter** (*MarkAsSpamNdrBackscatter*) | *Backscatter* is useless non-delivery reports (also known as NDRs or bounce messages) caused by forged senders in email messages. For more information, see [Backscatter messages](anti-spam-backscatter-about).  You don't need to configure this setting in the following environments, because legitimate NDRs are delivered and backscatter is marked as spam: <br>- Microsoft 365 organizations with Exchange Online mailboxes.<br>- On-premises email organizations where you route *outbound* email through Microsoft 365.<br><br> In Microsoft 365 environments that protect inbound email to on-premises mailboxes, turning this setting on or off has the following result: <br>- **On**: Legitimate NDRs are delivered, and backscatter is marked as spam.<br>- **Off**: Legitimate NDRs and backscatter go through normal spam filtering. Most legitimate NDRs are delivered to the original message sender. Some, but not all backscatter is marked as spam. By definition, backscatter can be delivered only to the spoofed sender, not to the original sender.<br><br> Test mode isn't available for this setting. | `X-CustomSpam: Backscatter NDR` |