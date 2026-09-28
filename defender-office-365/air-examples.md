---
layout: Conceptual
title: Automated investigation and response examples - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/air-examples
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
ms.date: 2025-02-24T00:00:00.0000000Z
description: See examples for how to start automated investigation and response (AIR) in Microsoft Defender for Office 365 Plan 2.
ms.custom:
- air
- seo-marvel-mar2020
ms.service: defender-office-365
locale: en-us
document_id: bb9ecf2a-03b9-6119-f82c-b42179d474c7
document_version_independent_id: bb9ecf2a-03b9-6119-f82c-b42179d474c7
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/air-examples.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: air-examples
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/air-examples.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 9682455c-449e-df75-d351-8c7dbbc13597
---

# Automated investigation and response examples - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

Automated investigation and response (AIR) in Microsoft Defender for Office 365 Plan 2 (included in Microsoft 365 licenses like E5 or as a standalone subscription) enables your SecOps team to operate more efficiently and effectively. AIR includes automated investigations to well-known threats, and provides recommended remediation actions. The SecOps team can review the evidence and approve or reject the recommended actions. For more information about AIR, see [Automated investigation and response (AIR) in Microsoft Defender for Office 365 Plan 2](air-about).

This article describes how AIR works through several examples:

- Example: A user-reported phishing message launches an investigation playbook
- Example: A security administrator triggers an investigation from Threat Explorer
- Example: A security operations team integrates AIR with their SIEM using the Office 365 Management Activity API

## Example: A user-reported phishing message launches an investigation playbook

A user receives an email that looks like a phishing attempt. The user reports the message using the [built-in Report button in Outlook](submissions-outlook-report-messages#use-the-built-in-report-button-in-outlook), which results in an alert that's triggered by the **Email reported by user as malware or phish**[alert policy](/en-us/defender-xdr/alert-policies#threat-management-alert-policies), which automatically launches the investigation playbook.

Various aspects of the reported email message are assessed. For example:

- The identified threat type
- Who sent the message
- Where the message was sent from (sending infrastructure)
- Whether other instances of the message were delivered or blocked
- The tenant landscape, including similar messages and their verdicts through email clustering
- Whether the message is associated with any known campaigns
- And more.

The playbook evaluates and automatically resolves submissions where no action is needed (which frequently happens on user reported messages). For the remaining submissions, a list of recommended actions to take on the original message and the associated *entities* (for example, attached files, included URLs, and recipients) is provided:

- Identify similar email messages via email cluster searches.
- Determine whether any users clicked through any malicious links in suspicious email messages.
- Risks and threats are assigned. For more information, see [Details and results of an automated investigation](air-view-investigation-results).
- Remediation steps. For more information, see [Remediation actions in Microsoft Defender for Office 365](air-remediation-actions).

## Example: A security administrator triggers an investigation from Threat Explorer

You're in Explorer (Threat Explorer) at https://security.microsoft.com/threatexplorerv3 in the **All email**, **Malware**, or **Phish** views. You're on the **Email** tab (view) of the details area below the chart. You select a message to investigate by using either of the following methods:

- Select one or more entries in the table by selecting the check box next to the first column. ![](media/defender-portal-icon-take-actions.png)**Take action** is available directly in the tab.

    [![Screenshot of the Email view (tab) of the details table with a message selected and Take action active.](media/te-rtd-all-email-view-take-action.png)](media/te-rtd-all-email-view-take-action.png#lightbox)
- Click on the **Subject** value of an entry in the table. The details flyout that opens contains ![](media/defender-portal-icon-take-actions.png)**Take action** at the top of the flyout.

    [![The actions available in the details tab after you select a Subject value in the Email tab of the details area in the All email view.](media/te-rtd-all-email-view-email-tab-details-area-subject-details-flyout-actions-only.png)](media/te-rtd-all-email-view-email-tab-details-area-subject-details-flyout-actions-only.png#lightbox)

After you select ![](media/defender-portal-icon-take-actions.png)**Take action**, select **Initiate automated investigation**. For more information, see [Email remediation](threat-explorer-threat-hunting#email-remediation).

Similar to playbooks triggered by an alert, automatic investigations that are triggered from Threat Explorer include:

- A root investigation.
- Steps to identify and correlate threats. For more information, see [Details and results of an automated investigation](air-view-investigation-results).
- Recommended actions to mitigate threats. For more information, see [Remediation actions in Microsoft Defender for Office 365](air-remediation-actions).

## Example: A security operations team integrates AIR with their SIEM using the Office 365 Management Activity API

AIR capabilities in Defender for Office 365 Plan 2 include [reports and details](air-view-investigation-results) that the SecOps team can use to monitor and address threats. But you can also integrate AIR capabilities with other solutions. For example:

- Security information and event management (SIEM) systems.
- Case management systems.
- Custom reporting solutions.

Use the [Office 365 Management Activity API](/en-us/office/office-365-management-api/office-365-management-activity-api-reference) for integration with these solutions.

For an example of a custom solution that integrates alerts from user-reported phishing messages that were already processed by AIR into a SIEM server and case management system, see [Microsoft Security Blog - Improve the Effectiveness of your SOC with Microsoft Defender for Office 365 and the Office 365 Management API](https://techcommunity.microsoft.com/blog/microsoftsecurityandcompliance/improve-the-effectiveness-of-your-soc-with-office-365-atp-and-the-o365-managemen/1525185).

The integrated solution greatly reduces the number of false positives, which allows the SecOps team to focus their time and effort on real threats.