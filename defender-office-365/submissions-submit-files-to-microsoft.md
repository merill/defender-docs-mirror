---
layout: Conceptual
title: Submit malware and good files to Microsoft for analysis - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/submissions-submit-files-to-microsoft
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
ms.assetid: 12eba50e-661d-44b8-ae94-a34bc47fb84d
ms.collection:
- m365-security
- tier1
description: Admins and end-users can learn about submitting undetected malware or mis-identified malware attachments to Microsoft for analysis.
ms.service: defender-office-365
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: ec79b2e5-b881-d8b2-b2df-9e4719e8112c
document_version_independent_id: ec79b2e5-b881-d8b2-b2df-9e4719e8112c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/submissions-submit-files-to-microsoft.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: submissions-submit-files-to-microsoft
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/submissions-submit-files-to-microsoft.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 758d2538-d952-d135-64ae-a7fafb416f3e
---

# Submit malware and good files to Microsoft for analysis - Microsoft Defender for Office 365 | Microsoft Learn

Note

If you're an admin in an organization with Exchange Online mailboxes, we recommend that you use the **Submissions** page in the Microsoft Defender portal to submit messages to Microsoft for analysis. For more information, see [Use the Submissions page to submit suspected spam, phish, URLs, legitimate email getting blocked, and email attachments to Microsoft](submissions-admin).

You've probably heard the following best practices for years:

- Avoid opening messages that look suspicious.
- Never open an attachment from someone you don't know.
- Avoid opening attachments in messages that urge you to open them.
- Avoid opening files downloaded from the internet unless they're from a verified source.
- Don't use anonymous USB drives.

But what can you do if you receive a message with a suspicious attachment or have a suspicious file on your system? In these cases, you should submit the suspicious attachment or file to Microsoft. Conversely, if an attachment in an email message or file was incorrectly identified as malware or some other threat, you can submit the attachment or file, too.

## What do you need to know before you begin?

Before you begin, review the following information about what qualifies as malware, phishing, and related submissions:

- All Microsoft 365 organizations that send or receive email include anti-malware protection that's automatically enabled. For more information, see [Anti-malware protection](anti-malware-protection-about).
- Messages with attachments that contain scripts or other malicious executables are considered malware, and you can use the submission options described in this section to report them.
- Messages with links to malicious sites are considered phishing. For more information about reporting phishing and good messages, see [Report messages and files to Microsoft](submissions-report-messages-files-to-microsoft).
- Files that block you from your accessing your system and demand money to open them are considered ransomware.

## Submit malware files to Microsoft

Organizations that have a Microsoft Defender subscription, or Microsoft Defender for Endpoint Plan 2 can submit files using the **Submissions** page in the Microsoft Defender portal. For more information, see [Use admin submission for submitting files in Microsoft Defender for Endpoint](/en-us/defender-endpoint/admin-submissions-mde).

Or, you can go to the Microsoft Security Intelligence page at https://www.microsoft.com/wdsi/filesubmission to submit the file. To receive analysis updates, sign in or enter a valid email address. We recommend using your Microsoft work or school account.

After you've uploaded the file or files, note the **Submission ID** that's created for your sample submission (for example, `7c6c214b-17d4-4703-860b-7f1e9da03f7f`).

[![The submission details in the Windows Defender Security Intelligence website](media/eop-malware-protection-center.png)](media/eop-malware-protection-center.png#lightbox)

After we receive the submitted file, we'll investigate. If we determine that the sample file is malicious, we take corrective action to prevent the malware from going undetected.

If you continue receiving infected messages or attachments, then you should copy the message headers from the email message, and contact Microsoft Customer Service and Support for further assistance. Be sure to have your **Submission ID** ready as well.

## Submit good files to Microsoft

Organizations that have a Microsoft Defender Subscription or Microsoft Defender for Endpoint Plan 2 can submit files using the **Submissions** page in the Microsoft Defender portal. For more information, see [Use admin submission for submitting files in Microsoft Defender for Endpoint](/en-us/defender-endpoint/admin-submissions-mde).

Or, you can go to the Microsoft Security Intelligence page at https://www.microsoft.com/wdsi/filesubmission to submit the file. To receive analysis updates, sign in or enter a valid email address. We recommend using your Microsoft work or school account.

You can also submit a file that you believe was incorrectly identified as malware to the website. (Just select **No** for the question **Do you believe this file contains malware?**)

After we receive the submitted file, we'll investigate. If we determine that the submitted file is clean, we take corrective action to prevent the file from being detected as malware.