---
layout: Conceptual
title: Usage card in Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/mdo-usage-card-about
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
keywords: AIR, autoIR, Microsoft Defender for Endpoint, automated, investigation, response, remediation, threats, advanced, threat, protection
f1.keywords:
- NOCSH
author: chrisda
ms.author: chrisda
audience: ITPro
ms.topic: article
ms.localizationpriority: medium
search.appverid:
- MET150
- MOE150
ms.collection:
- m365-security
- tier2
ms.custom:
- sfi-ga-nochange
description: Learn about your organization's active usage of Microsoft Defender for Office 365 licenses versus the actual number of licenses purchased.
ms.service: defender-office-365
ms.date: 2024-01-17T00:00:00.0000000Z
locale: en-us
document_id: 0eda7222-407f-de1d-ba65-e5aa0787c1be
document_version_independent_id: 0eda7222-407f-de1d-ba65-e5aa0787c1be
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/mdo-usage-card-about.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdo-usage-card-about
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/mdo-usage-card-about.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
platformId: 1499940d-7733-e245-a9a7-958c8166d05d
---

# Usage card in Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

In organizations with Microsoft Defender for Office 365, the usage card is available to help admins and Security Operations (SecOps) teams understand the usage of Defender for Office 365. Specifically, they can compare the active usage of Defender for Office 365 licenses vs the actual number of available licenses.

Tip

The usage card is enabled for tenants with at least one paid Defender for Office 365 Plan 1 or Defender for Office 365 Plan 2 license.

Usage cards can help determine the following scenarios:

- The active usage of Exchange Online licenses and how many of those licenses are active usage of Microsoft Defender for Office 365.
- A Breakdown of active usage across key Plan 1 and Plan 2 capabilities (Plan 1: protection and detection; Plan 2: SecOps capabilities).
- The Number of active Plan 1 and Plan 2 licenses purchased.

## View the usage card

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Reports** &gt; **Email & collaboration** section &gt; **Email & collaboration reports**. Or, to go directly to the **Email & collaboration reports and insights** page, use https://security.microsoft.com/emailandcollabreport.
2. On the **Email & collaboration reports and insights** page, go to the **Email & collaboration insights** section, and find the **Defender for Office 365 usage** card.

    [![The Defender for Office 365 usage card in the Defender portal.](media/usage-card-mdo.png)](media/usage-card-mdo.png#lightbox)

For members of **Billing Administrator** and **Global Administrator**^\*^ roles in [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal), following items are available on the card:

- **Add more licenses**
- **See licensing details**

These items aren't available for member of **Global Reader**, **Security Administrator**, **Security Operator**, or **Security Reader** roles.

Important

^\*^ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.

## Understand usage details

On the **Defender for Office 365 usage** card, select **Show details**.

[![The details flyout of the Defender for Office 365 usage card in the Defender portal.](media/usage-card-detail-flyout.png)](media/usage-card-detail-flyout.png#lightbox)

The details flyout that opens contains the following information from the last 28 days:

- The number of active users in the organization and the number of Plan 2 licenses.
- **Configured prevention and detection**section:
    - **Users with Office protection**: The number of active users of Safe Links or Safe Attachments for Office 365.
    - **Users with email protection**: The number of active users of Safe Links or Safe Attachments for emails.
    - **Users with Teams protection**: The number of active users of Safe Links for Teams.
- **Security Operations capabilities**section: The number of active users for the following categories:
    - **Users for whom manual and automated investigations were triggered**.
    - **Users for whom remediations were triggered**.
    - **Users targeted by phishing simulation training**.

**Threat protection status report** takes you to the [Threat protection status report](reports-email-security#threat-protection-status-report).

**See licensing details** is available for members of the **Security Operator** and **Global Administrators**^\*^ roles in [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal).

Important

^\*^ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.

## Frequently asked questions

### What are the different types of active users?

There are three types of active users:

- **Defender for Office 365 active users**: The distinct user count with active usage of Microsoft Defender for Office 365 Plan 1 and/or Plan 2 licenses over a period of 28 days for a specific paid Microsoft Defender for Office 365 tenant.
- **Active users**: The distinct user count with active usage of licenses over the past 28 days for a specific paid Microsoft Defender for Office 365 tenant.
- **Other active users**: Active users without the Microsoft Defender for Office 365 active users.

### What is the usage count?

Usage count can be determined by:

- **Users with Office 365 protection**: Distinct count of active users of Safe Links for Office 365 or Safe Attachments for Office 365.
- **Users with email protection**: Distinct count of active users of Safe Links for email or Safe Attachments for email.
- **Users for whom manual and automated investigations were triggered**: Manual investigations triggered from Threat Explorer or auto investigations actions approved or rejected by SecOps in Incidents or in Action center.
- **Users for whom remediations were triggered**: Manual remediations in Threat Explorer, Email entity, Advanced Hunting, Automation, or Action center.
- **Users targeted by Attack simulation training**: Users who were targeted as part of simulations over past 28 days.

### I have Defender for Office 365 Plan 1 or Plan 2 paid license. Why can I not see the usage card?

If you have at least one Defender for Office 365 Plan 1 or Plan 2 license, but you're still unable to see the card because of one of the following reasons:

- You don't have the required role to be able to view the card.
- Your organization had no active usage in the past 28 days.

### What does Collecting license and usage data status mean?

If you see **Collecting license and usage data** status in your usage card, it means Microsoft is still collecting your current licensing and usage data. When it's available, you can see the full usage card and other details.

[![Screenshot of the usage card showing the collecting data status.](media/usage-card-collecting-data.png)](media/usage-card-collecting-data.png#lightbox)

### Why does the Usage card show an overage even though you don't have Defender for Office 365 Plan 2 and no usage of SecOps capabilities?

The usage card shows usage of both Defender for Office 365 Plan 1 and Plan 2. If you don't have any Plan 2 licenses, the usage is coming from Plan 1 features (for example, Safe Links or Safe Attachments). You can fix this overage by purchasing more Plan 1 licenses.