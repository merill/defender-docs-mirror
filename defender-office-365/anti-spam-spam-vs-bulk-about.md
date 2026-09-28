---
layout: Conceptual
title: What's the difference between junk email and bulk email? - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/anti-spam-spam-vs-bulk-about
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
ms.assetid: 8079f193-1b40-4081-9e5d-d0e50dfbcc59
ms.collection:
- m365-security
- tier2
ms.custom:
- seo-marvel-apr2020
description: Admins can learn about the differences between junk email (spam) and bulk email (gray mail) in Microsoft 365.
ms.service: defender-office-365
ms.date: 2024-07-25T00:00:00.0000000Z
locale: en-us
document_id: 0026b268-75dd-6a7c-bb19-79c25c69617d
document_version_independent_id: 0026b268-75dd-6a7c-bb19-79c25c69617d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/anti-spam-spam-vs-bulk-about.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: anti-spam-spam-vs-bulk-about
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/anti-spam-spam-vs-bulk-about.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 34c59e4a-03d9-86bf-01a7-e81c30dfc916
---

# What's the difference between junk email and bulk email? - Microsoft Defender for Office 365 | Microsoft Learn

In all organizations with cloud mailboxes, customers sometimes ask: "What's the difference between junk email and bulk email?" This article explains the difference and describes the available controls.

- **Junk email** is spam, which is an unsolicited and universally unwanted message (when identified correctly). Microsoft 365 rejects spam based on the reputation of the source email server. If a message passes source IP inspection, it continues through spam filtering. If the message is classified as **Spam** or **High confidence spam** by spam filtering, what happens to the message depends on the verdict and the anti-spam policy that detected the message.

    For the default actions that are taken on spam and high confidence spam messages in the default anti-spam policy and in the Standard and Strict [preset security policies](preset-security-policies), see the **Spam** and **High confidence spam** entries in [Anti-spam policy settings](recommended-settings-for-eop-and-office365#anti-spam-policy-settings).

    In the default anti-spam policy and in custom anti-spam policies, you can configure the action to take on spam filtering verdicts. For instructions, see [Configure anti-spam policies](anti-spam-policies-configure).

    If you disagree with the spam filtering verdict, you can report messages as spam or good to Microsoft in several ways, as described in [Report messages and files to Microsoft](submissions-report-messages-files-to-microsoft).
- **Bulk email** (also known as *gray mail*), is more difficult to classify. Whereas spam is a constant threat, bulk email is often one-time advertisements or marketing messages. Some users want bulk email messages (and in fact, they have deliberately signed up to receive them), while other users consider bulk email to be spam. For example, some users want to receive advertising messages from the Contoso Corporation or invitations to an upcoming conference on cybersecurity, while other users consider these same messages to be spam.

    For more information about how bulk email is identified, see [Bulk complaint level (BCL)](anti-spam-bulk-complaint-level-bcl-about).

## How to manage bulk email

Because of the mixed reaction to bulk email, there isn't universal guidance that applies to every organization.

Anti-spam policies have a default BCL threshold that's used to identify bulk email as spam, and a specific action to take on those bulk messages. For more information, see the following articles:

- [Bulk complaint level (BCL)](anti-spam-bulk-complaint-level-bcl-about)
- [Configure anti-spam policies](anti-spam-policies-configure).
- [Anti-spam policy settings](recommended-settings-for-eop-and-office365#anti-spam-policy-settings)

Another option that's easy to overlook: if a user complains about receiving bulk email, but the messages are from reputable senders that pass spam filtering, have the user check for an unsubscribe option in the bulk email message.

## How to tune bulk email

Admins can follow the [recommended bulk threshold values](recommended-settings-for-eop-and-office365#anti-spam-policy-settings) or choose a bulk threshold value that suits the needs of their organization.

### Tune bulk email in Microsoft 365

In all organizations with cloud mailboxes, the bulk senders insight shows much mail was identified as bulk at the current BCL threshold in anti-spam policies, and simulates identified vs. allowed bulk email based on changes in the BCL threshold.

For more information, see [Bulk senders insight](anti-spam-bulk-senders-insight).

### Tune bulk email in Microsoft Defender for Office 365 Plan 1 or Plan 2

If your Microsoft 365 organization has Defender for Office 365 Plan 1 or Plan 2 (included or in an add-on subscription), you can use the [Threat protection status report](reports-email-security#threat-protection-status-report) to identify wanted and unwanted bulk senders:

1. Open the **Threat protection status** report at https://security.microsoft.com/reports/TPSAggregateReportATP.
2. Select **View data by Email &gt; Spam** and **Chart breakdown by Detection Technology**.
3. Select ![](media/defender-portal-icon-filter.png)**Filter**. In the **Filters** flyout that opens, select only **Bulk** in the **Detection** section.

    Use the **Bulk complaint level** slider to adjust the bulk detections by BCL value.

    When you're finished in the **Filters** flyout, select **Apply**.
4. Back on the **Threat protection status** page, select one of the bulk messages from the details table below the chart by clicking anywhere in the row other than the check box next to the first column.

    In the message details flyout that opens, select ![](media/defender-portal-icon-open.png)**Open email entity** at the top of the flyout to see details about the message in [the Email entity page in Microsoft Defender for Office 365](mdo-email-entity-page).
5. After you identify wanted and unwanted bulk senders, adjust the bulk threshold in the default anti-spam policy and in custom anti-spam policies. If some bulk senders don't fit within your bulk threshold, [report the messages to Microsoft for analysis](submissions-admin#report-good-email-to-microsoft).

### Tune bulk email in organizations with Defender for Office 365 Plan 2

As of September 2022, Microsoft Defender for Office 365 Plan 2 customers can access BCL from [advanced hunting](/en-us/defender-xdr/advanced-hunting-overview). This feature allows admins to look at all bulk senders who sent mail to their organization, their corresponding BCL values, and the amount of email received. You can drill down into the bulk senders by using other columns in **EmailEvents** table in the **Email & collaboration** schema. For more information, see [EmailEvents](/en-us/defender-xdr/advanced-hunting-emailevents-table).

For example, if Contoso sets their bulk threshold to 7 in anti-spam policies, Contoso recipients receive email from all senders in their Inbox if the BCL value is 6 or less. Admins can run the following query to get a list of all bulk senders in the organization:

```console
EmailEvents
| where BulkComplaintLevel >= 1 and Timestamp > datetime(2022-09-XXT00:00:00Z)
| summarize count() by SenderMailFromAddress, BulkComplaintLevel
```

This query allows admins to identify wanted and unwanted senders. If a bulk sender has a BCL score that's more than the bulk threshold, admins can [report the sender's messages to Microsoft for analysis](submissions-admin#report-good-email-to-microsoft). This action also adds the sender as an allow entry in the Tenant Allow/Block List.

Organizations without Defender for Office 365 Plan 2 can try the features in Microsoft Defender XDR for Office 365 Plan 2 for free. Use the 90-day Defender for Office 365 evaluation at https://security.microsoft.com/atpEvaluation. Learn about who can sign up and trial terms [here](try-microsoft-defender-for-office-365).