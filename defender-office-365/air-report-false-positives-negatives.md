---
layout: Conceptual
title: Report false positives or false negatives following automated investigation and response - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/air-report-false-positives-negatives
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Was something missed or wrongly detected by AIR in Microsoft Defender for Office 365 Plan 2? Learn how to submit false positives or false negatives to Microsoft for analysis.
author: chrisda
ms.author: chrisda
ms.service: defender-office-365
ms.date: 2026-07-03T00:00:00.0000000Z
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.topic: how-to
ms.custom:
- msecd-doc-authoring-1016
- autoir
ai-usage: ai-assisted
locale: en-us
document_id: 0faaa3b3-36ec-a886-f4fe-6f28164a8b28
document_version_independent_id: 0faaa3b3-36ec-a886-f4fe-6f28164a8b28
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/air-report-false-positives-negatives.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: air-report-false-positives-negatives
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/air-report-false-positives-negatives.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 36c8b422-10be-ac3d-1d35-a7d2216c10e1
---

# Report false positives or false negatives following automated investigation and response - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

Automated investigation and response (AIR) in Microsoft Defender for Office 365 Plan 2 includes powerful capabilities to detect and investigate threats. For more information, see [Automated investigation and response](air-about).

But what if AIR incorrectly identifies an email message, attachment, or URL as a threat (a false positive) or missed an item that turned out to be a threat (a false negative)? This article explains the options that are available to security operations (SecOps) personnel to deal with false positives and false negatives from AIR.

## Submit false positives or false negatives to Microsoft

You can submit or resubmit false positive and false negative items to Microsoft. These items include email messages, email attachments, and URLs. For instructions, see [Use the Submissions page to submit suspected spam, phish, URLs, legitimate email getting blocked, and email attachments to Microsoft](submissions-admin).

## Adjust alerts to prevent false positives from recurring

The instructions depend on the available subscriptions in your organization:

- **Microsoft Defender XDR**: [Tune an alert](/en-us/defender-xdr/investigate-alerts#tune-an-alert)
- **Defender for Endpoint**: Create **Allow** actions for files, IP addresses URLs or domains that are misidentified as malware on devices. For instructions, see [Create indicators](/en-us/defender-endpoint/manage-indicators).

## Prerequisites

Before you undo remediation actions, verify that you have the required permissions and licensing. For details, see [Required permissions and licensing for AIR](air-about#required-permissions-and-licensing-for-air).

## Undo remediation actions

SecOps personnel can often use ![](media/defender-portal-icon-take-actions.png)**Take action** to undo the remediation action that AIR applied to the item. For example:

- From Explorer (Threat Explorer). For details, see [Email remediation](threat-explorer-threat-hunting#email-remediation).
- From the Email entity page. For more information, see [Actions on the Email entity page](mdo-email-entity-page#actions-on-the-email-entity-page).
- From the details flyout of entries on the **History** tab of the Action center at https://security.microsoft.com/action-center/history.

For details about the available actions in ![](media/defender-portal-icon-take-actions.png)**Take action**, see the [Take action wizard](threat-explorer-threat-hunting#the-take-action-wizard).

- To take action on messages that were moved to the Junk Email folder in the mailbox, use **Take action** &gt; **Move to mailbox folder**and then select one of the following destinations:
    - **Inbox** for false positives.
    - **Deleted Items**, **Soft deleted items**, or **Hard deleted items** for false negatives.
- To take action on messages that were quarantined, do one of the following steps:
    - To release the message, use **Take action** &gt; **Move to mailbox folder** &gt; **Inbox** and then select **Release to one or more of the original recipients of the email** or **Release to all recipients**. Or, you can [release the message directly from quarantine](quarantine-admin-manage-messages-files#release-quarantined-email).
    - [Delete the message directly from quarantine](quarantine-admin-manage-messages-files#delete-email-from-quarantine) if the user has access to the quarantined message.
    - If the user doesn't have access to the quarantined message, you don't need to do anything (the message eventually expires based on the [quarantine retention](quarantine-about#quarantine-retention) period).
- To take action on files that were quarantined, do one of the following steps:
    - [Release the quarantined file from quarantine](quarantine-admin-manage-messages-files#release-quarantined-files-from-quarantine).
    - [Delete the quarantined file from quarantine](quarantine-admin-manage-messages-files#delete-quarantined-files-from-quarantine) if the user has access to the quarantined file.
    - If the user doesn't have access to the quarantined file, you don't need to do anything (the file eventually expires based on the [quarantine retention](quarantine-about#quarantine-retention) period).