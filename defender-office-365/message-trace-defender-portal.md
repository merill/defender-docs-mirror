---
layout: Conceptual
title: Message trace in the Microsoft Defender portal - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/message-trace-defender-portal
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: how-to
ms.collection:
- m365-security
- tier2
ms.localizationpriority: medium
ms.assetid: 3e64f99d-ac33-4aba-91c5-9cb4ca476803
ms.custom:
- msecd-doc-authoring-1016
- seo-marvel-apr2020
- sfi-ga-nochange
description: Admins can use the Message trace link in the Microsoft Defender portal to find out what happened to messages.
ms.service: defender-office-365
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 87da033b-6a5f-0eb6-91ec-b8b20a1cf5c2
document_version_independent_id: 87da033b-6a5f-0eb6-91ec-b8b20a1cf5c2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/message-trace-defender-portal.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: message-trace-defender-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/message-trace-defender-portal.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 0770bb5e-0ea3-40bb-3ea2-d9f887ee338b
---

# Message trace in the Microsoft Defender portal - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

In all organizations with cloud mailboxes, message trace follows email messages as they travel through your Microsoft 365 organization. You can determine if a message was received, rejected, deferred, or delivered by the service. Message trace also shows what actions were taken on the message before it reached its final status.

You can use the information from message trace to efficiently answer user questions about what happened to messages, troubleshoot mail flow issues, and validate policy changes.

The **Summary report** in the message trace contains the information that helps you answer user questions and troubleshoot mail flow issues. The **Summary report** can be exported as a file that can be opened in Windows Explorer (also known as File Explorer).

You can use the **View in Explorer** option in the **Message trace search results** page in [Exchange admin center](https://admin.exchange.microsoft.com/). However, to use this option, you must fulfill the following prerequisite:

- You must procure the E5/A5 license to access a feature within the Office 365 Threat Intelligence licensing. The Office 365 Threat Intelligence feature only enables you to use the **View in Explorer** option.

Tip

The **Message trace** page in the Microsoft Defender portal is a really pass through to **Message trace** page in the new Exchange admin center (EAC) at https://admin.exchange.microsoft.com/#/messagetrace.

## What do you need to know before you begin?

- The maximum number of messages that are displayed in the results of a message trace depends on the report type you selected (for example, **Summary**, **Enhanced summary**, or **Extended**). Each report type has different row limits and time ranges. For details, see [Choose report type](/en-us/exchange/monitoring/trace-an-email-message/message-trace-modern-eac#choose-report-type). The [Get-HistoricalSearch](/en-us/powershell/module/exchangepowershell/get-historicalsearch) cmdlet in Exchange Online PowerShell returns all messages in the results.
- You need to be assigned permissions before you can do the procedures in this article. You have the following options:

    - [Exchange Online permissions](/en-us/exchange/permissions-exo/permissions-exo): Membership in the **Organization Management**, **Compliance Management** or **Help Desk** role groups.
    - [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): Membership in the **Global Administrator**^\*^ or **Compliance Administrator** roles gives users the required permissions *and* permissions for other features in Microsoft 365.

        Important

        ^\*^ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.

## Open message trace

In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Exchange message trace**.

After you select **Exchange message trace**, the **Message trace** page in the new EAC opens. To go directly to the **Message trace** page in the new EAC, use https://admin.exchange.microsoft.com/#/messagetrace. For more information, see [Message trace in the new Exchange admin center](/en-us/exchange/monitoring/trace-an-email-message/message-trace-modern-eac).