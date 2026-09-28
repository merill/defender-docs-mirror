---
layout: Conceptual
title: Assess and Tune your Filtering for Bulk Mail in Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/step-by-step-guides/tune-bulk-mail-filtering-walkthrough
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Tune bulk filtering settings within Exchange Online and Microsoft Defender for Office 365
ms.service: defender-office-365
author: MSFTBen
ms.author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-guidance-templates
- m365-security
- tier3
ms.topic: how-to
ms.date: 2026-06-12T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1014
locale: en-us
document_id: f67763db-a1e9-c872-70bc-9d8ee1af87fb
document_version_independent_id: f67763db-a1e9-c872-70bc-9d8ee1af87fb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/step-by-step-guides/tune-bulk-mail-filtering-walkthrough.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: step-by-step-guides/tune-bulk-mail-filtering-walkthrough
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/step-by-step-guides/tune-bulk-mail-filtering-walkthrough.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: af9a92c9-4329-2350-4154-13e468249979
---

# Assess and Tune your Filtering for Bulk Mail in Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn

This guide describes how to tune your bulk email filtering settings in Exchange Online or Microsoft Defender for Office 365. This process includes configuring the delivery location of detected bulk mail and, if necessary, optional transport rules you can use to achieve a more aggressive filtering stance should this suit your organization's needs.

## Prerequisites

Before you begin, make sure you have the following prerequisites:

- Exchange Online as a minimum. (Microsoft Defender for Office 365 offers extra functionality)
- Sufficient permissions. (Security Administrator)
- Basic understanding of checking message headers (for more information, see [View internet message headers in Outlook](https://support.microsoft.com/office/view-internet-message-headers-in-outlook-cd039382-dc6e-4264-ac74-c048563d212c))
- 30 minutes to complete the following steps

## Understanding the bulk (BCL) value

The Bulk Complaint Level (BCL) indicates how likely a message is to be bulk mail. Bulk mail is typically advertising emails or marketing messages. These emails can be more challenging to filter as some customers want these emails. Other customers consider these emails spam and don't want to receive them. We add a "BCL" value stamp on emails based on the number of complaints we get about that sender and allow you to select the threshold to accept so you can tune the number of bulk messages you receive.

## Check the BCL value of an email and the threshold in your policies

Use the following steps to find a message's BCL value and compare it with your current policy threshold:

1. Take the headers of a message you're concerned with and search for the **"X-Microsoft-Antispam:"** header, which contains a **BCL value**. Make a note of this number.
2. Repeat the header review for additional messages until you have an average BCL value. We'll use this value as the threshold. Any mail with a **BCL** value **above** this number will be impacted by the changes we make.
3. **Login** to the Microsoft Security portal at https://security.microsoft.com.
4. On the **left nav**, under **Email & collaboration**, select **Policies & rules**.
5. Select **Threat policies** and then **Anti-Spam**.
6. When the page loads, the next action you'll take depends on the type of policy you're using:
    - You can't edit the Standard and Strict preset security policies. The BCL threshold is 6 in standard, 5 in strict.
    - The default anti-spam policy and custom anti-spam policies use the BCL threshold 7 by default, but you can change it.
7. **Edit** (or create a custom anti-spam policy) to set the BCL threshold that meets your needs. For example, if most of the messages you collected (which were all unwanted) have a BCL value of 4 or higher, setting the BCL value to 4 in the policy would filter out these messages for your end users.
8. Within that policy, under the **"Edit actions"** section, select the **"bulk message action"** and select what to do when the threshold is exceeded. For example, you could select Quarantine if you would like to keep all bulk out of the mailbox or use the Junk email folder for a less aggressive stance.
9. If you receive complaints from users about too many bulk emails being blocked, you can adjust this threshold, or alternatively, submit the message to us, which will also add the sender to the Tenant Allow/Block List.

Tip

For more details on allowing senders using the Tenant Allow/Block List, see [How to handle legitimate emails getting blocked from delivery using Microsoft Defender for Office 365](how-to-handle-false-positives-in-microsoft-defender-for-office-365).

## More aggressive strategies for managing bulk senders

In some cases, the sender of bulk mail doesn't generate enough complaints for its messages to be assigned a BCL value high enough to be caught by your tuned threshold value. If the sender's messages don't receive a high enough BCL value to be caught by your threshold, you can use transport rules to take a more aggressive approach; however, use caution, as false positives (unwanted blocking) will occur. Tune the rules with exceptions and management to stay relevant for your organization's mail patterns.

Tip

To better protect certain groups of users, such as your c-suite and priority accounts, you can create a specialized policy specifically scoped to them and set a higher BCL threshold, alongside a separate transport rule (if applicable). These groups of users might be more vulnerable to unsolicited emails due to their email addresses being readily accessible in the public domain.

For detailed instructions on creating transport rules for bulk email, see [Use mail flow rules to filter bulk email in Exchange Online | Microsoft Learn](/en-us/exchange/security-and-compliance/mail-flow-rules/use-rules-to-filter-bulk-mail).

## Bulk mail filtering options in Microsoft Defender for Office 365

If you have Microsoft Defender for Office 365, you can use the following additional methods to inspect bulk mail values:

- Customers with Microsoft Defender for Office 365 Plan 1 or higher can use the [email entity page](https://techcommunity.microsoft.com/blog/microsoftdefenderforoffice365blog/introducing-the-email-entity-page-in-microsoft-defender-for-office-365/2275420) to discover the BCL value of messages instead of interrogating headers.
- Customers with Microsoft Defender for Office 365 Plan 2 can interrogate bulk values at scale using [advanced hunting queries to tune bulk email](../anti-spam-spam-vs-bulk-about#how-to-tune-bulk-email).

For step-by-step guidance on tuning bulk email at scale, see [How to tune bulk email](../anti-spam-spam-vs-bulk-about#how-to-tune-bulk-email).