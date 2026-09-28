---
layout: Conceptual
title: Custom reporting solutions with automated investigation and response - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/air-custom-reporting
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: concept-article
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
description: Learn how to integrate automated investigation and response with a custom or non-Microsoft reporting solution.
ms.date: 2024-07-10T00:00:00.0000000Z
ms.custom:
- air
ms.service: defender-office-365
locale: en-us
document_id: 73e08e62-9193-aa34-89af-4cbe91e3517d
document_version_independent_id: 73e08e62-9193-aa34-89af-4cbe91e3517d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/air-custom-reporting.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: air-custom-reporting
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/air-custom-reporting.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 8f3f33a3-ddfc-80d4-075a-1f7efd1c3ab1
---

# Custom reporting solutions with automated investigation and response - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

Automated investigation and response (AIR) in Microsoft Defender for Office 365 Plan 2 returns detailed information about the results. For more information, see [Details and results of automated investigation and response (AIR) in Microsoft Defender for Office 365 Plan 2](air-view-investigation-results).

However, some Microsoft 365 organizations use custom or non-Microsoft reporting solutions. Those organizations can use the **Office 365 Management Activity APIs** to integrate information from AIR into other reporting solutions.

| Resource | Description |
| --- | --- |
| [Office 365 Management APIs overview](/en-us/office/office-365-management-api/office-365-management-apis-overview) | The Office 365 Management Activity API provides information about various user, admin, system, and policy actions and events from Microsoft 365 and Microsoft Entra activity logs. |
| [Get started with Office 365 Management APIs](/en-us/office/office-365-management-api/get-started-with-office-365-management-apis) | The Office 365 Management API uses Microsoft Entra ID to provide authentication services for your application to access Microsoft 365 data. Follow the steps in this article to set this up. |
| [Office 365 Management Activity API reference](/en-us/office/office-365-management-api/office-365-management-activity-api-reference) | You can use the Office 365 Management Activity API to retrieve information about user, admin, system, and policy actions and events from Microsoft 365 and Microsoft Entra activity logs. Read this article to learn more about how this works. |
| [Office 365 Management Activity API schema](/en-us/office/office-365-management-api/office-365-management-activity-api-schema) | Get an overview of the [Common schema](/en-us/office/office-365-management-api/office-365-management-activity-api-schema#common-schema) and the [Defender for Office 365 and threat investigation and response schema](/en-us/office/office-365-management-api/office-365-management-activity-api-schema#office-365-advanced-threat-protection-and-threat-investigation-and-response-schema) to learn about specific kinds of data available through the Office 365 Management Activity API. |