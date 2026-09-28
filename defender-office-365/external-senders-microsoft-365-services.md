---
layout: Conceptual
title: Services for external organizations sending mail to Microsoft 365 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/external-senders-microsoft-365-services
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: overview
ms.localizationpriority: medium
ms.assetid: 19fd3e0f-8dbf-4049-a810-2c8ee6cefd48
ms.collection:
- m365-security
- tier2
description: To help maintain user trust in the use of email, Microsoft has put in place various policies and technologies to help protect our users.
ms.service: defender-office-365
ms.date: 2023-10-09T00:00:00.0000000Z
locale: en-us
document_id: 23bf9d8d-0aca-3dbb-2cf0-828b8a3b2f1c
document_version_independent_id: 23bf9d8d-0aca-3dbb-2cf0-828b8a3b2f1c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/external-senders-microsoft-365-services.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-senders-microsoft-365-services
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/external-senders-microsoft-365-services.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 5809f96b-9914-7333-e22f-08c4615df5e7
---

# Services for external organizations sending mail to Microsoft 365 - Microsoft Defender for Office 365 | Microsoft Learn

Email abuse, junk email, and fraudulent email (phishing) continue to burden internet email. To help maintain trust in the use of email, Microsoft uses several features to help protect our users. However, we understand the importance of not affecting legitimate email. Therefore, we have a suite of services to help external senders proactively manage their sender reputation and improve their ability to deliver email to Microsoft 365 users.

This overview provides information about the benefits we provide to your organization, even if you aren't a Microsoft 365 customer.

Tip

If you're not a Microsoft 365 customer, and you're trying to send email to Microsoft 365, this article is for you. If you're an admin in Microsoft 365 and you need help with fighting spam, this article isn't for you. Instead, see [anti-spam](anti-spam-protection-about) and [anti-malware](anti-malware-protection-about).

## Microsoft support

Microsoft offers several support options for people having trouble sending mail to Microsoft 365 recipients. We recommend that you:

- Follow the instructions in any non-delivery report (also known as an NDR or bounce message) that you receive.
- Check out the most common problems that external senders encounter in [External senders - Troubleshoot email sent to Microsoft 365](external-senders-mail-flow-troubleshooting).
- Ask the Microsoft 365 recipient to contact Microsoft Support and open a support ticket on your behalf. Typically, external senders can't open support tickets in Microsoft 365. But, there are legal reasons that might require Microsoft Support to communicate directly with owner of the blocked source IP address space.

    For more information about Microsoft Technical support for Microsoft 365, see [Support](/en-us/office365/servicedescriptions/office-365-platform-service-description/support).

## Anti-Spam IP Delist Portal

This self-service portal at https://sender.office.com/ allows you to request your removal from the Microsoft 365 blocked senders list. Use the portal if you get errors sending messages to Microsoft 365 recipients. For more information, see [Use the delist portal to remove yourself from the blocked senders list](external-senders-use-the-delist-portal-to-unblock-yourself).

## Abuse and spam reporting for junk email originating from Exchange Online

Third parties occasionally violate our terms of use and use Microsoft 365 to send junk email. If you receive junk email from Microsoft 365 senders, you can report these messages to Microsoft. For instructions, see [Report messages and files to Microsoft](submissions-report-messages-files-to-microsoft).

## Legal stuff you need to know

The following article explains how external organizations can avoid having their email blocked by adhering to our anti-spam rules, and contains legal stuff that you need to know: [External senders - Policies, practices, and guidelines](external-senders-policies-practices-guidelines).