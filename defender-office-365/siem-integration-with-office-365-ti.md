---
layout: Conceptual
title: SIEM integration with Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/siem-integration-with-office-365-ti
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
f1.keywords:
- NOCSH
ms.author: deniseb
author: denisebmsft
audience: ITPro
ms.topic: article
ms.localizationpriority: low
search.appverid:
- MET150
- MOE150
ms.assetid: eb56b69b-3170-4086-82cf-ba40a530fa1b
ms.date: 2023-06-20T00:00:00.0000000Z
ms.collection:
- m365-security
- tier2
description: Integrate your organization's SIEM server with Microsoft Defender for Office 365 and related threat events in the Office 365 Activity Management API.
ms.custom:
- seo-marvel-apr2020
- sfi-ga-nochange
ms.service: defender-office-365
locale: en-us
document_id: bb9d4129-9f7e-c5aa-c730-dd7033f45a33
document_version_independent_id: bb9d4129-9f7e-c5aa-c730-dd7033f45a33
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/siem-integration-with-office-365-ti.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: siem-integration-with-office-365-ti
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/siem-integration-with-office-365-ti.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: e18ee62c-7b45-8476-cfd3-15aa638b7140
---

# SIEM integration with Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

If your organization is using a security information and event management (SIEM) server, you can integrate Microsoft Defender for Office 365 with your SIEM server. You can set up this integration by using the [Office 365 Activity Management API](/en-us/office/office-365-management-api/office-365-management-activity-api-reference).

SIEM integration enables you to view information, such as malware or phish detected by Microsoft Defender for Office 365, in your SIEM server reports.

- To see an example of SIEM integration with Microsoft Defender for Office 365, see [this blog post](https://techcommunity.microsoft.com/blog/microsoftsecurityandcompliance/improve-the-effectiveness-of-your-soc-with-office-365-atp-and-the-o365-managemen/1525185).
- To learn more about the Office 365 Management APIs, see [Office 365 Management APIs overview](/en-us/office/office-365-management-api/office-365-management-apis-overview).

## How SIEM integration works

The Office 365 Activity Management API retrieves information about user, admin, system, and policy actions and events from your organization's Microsoft 365 and Microsoft Entra activity logs. If your organization has Microsoft Defender for Office 365 Plan 1 or 2, or Office 365 E5, you can use the [Microsoft Defender for Office 365 schema](/en-us/office/office-365-management-api/office-365-management-activity-api-schema#office-365-advanced-threat-protection-and-threat-investigation-and-response-schema).

Recently, events from automated investigation and response capabilities in [Microsoft Defender for Office 365 Plan 2](mdo-about#defender-for-office-365-plan-1-vs-plan-2-cheat-sheet) were added to the Office 365 Management Activity API. In addition to including data about core investigation details such as ID, name and status, the API also contains high-level information about investigation actions and entities.

The SIEM server or other similar system polls the **audit.general** workload to access detection events. To learn more, see [Get started with Office 365 Management APIs](/en-us/office/office-365-management-api/get-started-with-office-365-management-apis).

## Enum: AuditLogRecordType - Type: Edm.Int32

### AuditLogRecordType

The following table summarizes the values of **AuditLogRecordType** that are relevant for Microsoft Defender for Office 365 events:

| Value | Member name | Description |
| --- | --- | --- |
| 28 | ThreatIntelligence | Phishing and malware events from [the built-in security features for all cloud mailboxes](eop-about) and from Microsoft Defender for Office 365. |
| 41 | ThreatIntelligenceUrl | Safe Links time-of-click and block override events from Microsoft Defender for Office 365. |
| 47 | ThreatIntelligenceAtpContent | Phishing and malware events for files in SharePoint, OneDrive, and Microsoft Teams, from Microsoft Defender for Office 365. |
| 64 | AirInvestigation | Automated investigation and response events, such as investigation details and relevant artifacts, from Microsoft Defender for Office 365 Plan 2. |

Important

You must have either the Global Administrator^\*^ or Security Administrator role assigned to set up SIEM integration with Microsoft Defender for Office 365. For more information, see [Permissions in the Microsoft Defender portal](mdo-portal-permissions).

^\*^Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.

Audit logging must be turned on for your Microsoft 365 environment (it's on by default). To verify that audit logging is turned on or to turn it on, see [Turn auditing on or off](/en-us/purview/audit-log-enable-disable).