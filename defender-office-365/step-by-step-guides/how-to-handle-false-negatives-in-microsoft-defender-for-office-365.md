---
layout: Conceptual
title: Investigate and remediate false negative malicious emails in Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/step-by-step-guides/how-to-handle-false-negatives-in-microsoft-defender-for-office-365
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to investigate false negative email, remove malicious messages delivered to users, and reduce the chance of similar deliveries in the future.
ms.service: defender-office-365
author: chrisda
ms.author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-guidance-templates
- m365-security
- tier3
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 96fad833-dfb5-6de6-fb00-2886a0d83184
document_version_independent_id: 96fad833-dfb5-6de6-fb00-2886a0d83184
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/step-by-step-guides/how-to-handle-false-negatives-in-microsoft-defender-for-office-365.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: step-by-step-guides/how-to-handle-false-negatives-in-microsoft-defender-for-office-365
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/step-by-step-guides/how-to-handle-false-negatives-in-microsoft-defender-for-office-365.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
platformId: 19f1cd26-fd46-6abb-a13f-eb9aa218def9
---

# Investigate and remediate false negative malicious emails in Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn

Microsoft Defender for Office 365 helps deal with undetected malicious email delivered to recipients (known as false negatives) that put your organizational productivity at risk.

Defender for Office 365 can help admins understand *why* malicious emails were delivered, how to quickly resolve the issue, and how to prevent similar issues from happening in the future.

## Prerequisites

Before you begin, make sure you meet the following requirements:

- Microsoft Defender for Office 365 Plan 1 or Plan 2. Microsoft 365 A5/E5/G5 includes Plan 2.
- Sufficient permissions. For example, membership in the **Security Administrator** role in [Microsoft Entra ID](/en-us/entra/identity/role-based-access-control/manage-roles-portal).
- 5-10 minutes to perform the following steps.

## Handling malicious emails in the Inbox folder of end users

Perform the following steps to handle malicious emails that reached end users' Inbox folders:

1. Ask end users to report the email as **Phishing** or **Junk** using the [built-in **Report** button in supported versions of Outlook](../submissions-outlook-report-messages#use-the-built-in-report-button-in-outlook).
2. End users can also add senders to their **[Blocked Senders List](https://support.microsoft.com/office/block-or-unblock-senders-in-outlook-9bf812d4-6995-4d19-901a-76d6e26939b0#picktab=classic_outlook)** in Outlook to prevent emails from this sender from being delivered to their inbox.
3. Admins can triage the user reported messages from [User reported tab on the Submissions page](../submissions-admin#view-user-reported-messages-to-microsoft).

    Tip

    In organizations with Defender for Office 365 Plan 2 and Security Copilot, the [Phishing Triage Agent](/en-us/defender-xdr/phishing-triage-agent) can autonomously triage and classify user-reported phishing emails, reducing manual investigation work for security teams.
4. From the user-reported messages on the Submissions page, admins can **submit to**[notify users about admin-submitted messages to Microsoft](../submissions-admin-review-user-reported-messages#notify-users-from-within-the-portal) to learn why the reported message was allowed in the first place.
5. If needed, while submitting to Microsoft for analysis, admins can [create a block entry for the sender](../tenant-allow-block-list-email-spoof-configure#create-block-entries-for-domains-and-email-addresses) to mitigate the problem.
6. Once the results for submissions are available, read the verdict to understand why emails were allowed, and how your organization setup could be improved to prevent similar issues from happening in the future.

## Handling malicious emails in the Junk Email folder of end users

Perform the following steps to handle malicious emails that were delivered to end users' Junk Email folders:

1. Ask end users to report the email as **phishing** using the [built-in **Report** button in supported versions of Outlook](../submissions-outlook-report-messages#use-the-built-in-report-button-in-outlook).
2. Admins can triage the user reported messages from the [User reported tab on the Submissions page](../submissions-admin#view-user-reported-messages-to-microsoft).

    Tip

    In organizations with Defender for Office 365 Plan 2 and Security Copilot, the [Phishing Triage Agent](/en-us/defender-xdr/phishing-triage-agent) can autonomously triage and classify user-reported phishing emails, reducing manual investigation work for security teams.
3. From the user-reported messages on the Submissions page, admins can **submit to**[notify users about admin-submitted messages to Microsoft](../submissions-admin#notify-users-about-admin-submitted-messages-to-microsoft) and learn why the reported message was allowed in the first place.
4. If needed, while submitting to Microsoft for analysis, admins can [create a block entry for the sender](../tenant-allow-block-list-email-spoof-configure#create-block-entries-for-domains-and-email-addresses) to mitigate the problem.
5. Once the results for submissions are available, read the verdict to understand why emails were allowed, and how your organization setup could be improved to prevent similar issues from happening in the future.

## Handling malicious emails landing in the quarantine folder of end users

Use the following workflow for malicious emails that were quarantined for end users:

1. End users receive an [email digest](../quarantine-quarantine-notifications) about quarantined messages as per the settings enabled by admins.
2. End users can preview the messages in quarantine, block the sender, and submit those messages to Microsoft for analysis.

## Handling malicious emails landing in the quarantine folder of admins

Perform the following steps for malicious emails that appear in the admin quarantine:

1. Admins can view the quarantined emails (including the ones asking permission to request release) from the [Manage quarantined messages and files](../quarantine-admin-manage-messages-files) page.
2. Admins can submit any malicious, or suspicious messages to Microsoft for analysis, and create a block to mitigate the issue while waiting for a verdict.
3. Once the results for submissions are available, read the verdict to learn why the emails were allowed, and how your organization setup could be improved to prevent similar issues from happening in the future.