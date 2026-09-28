---
layout: Conceptual
title: Search for emails and remediate threats using Threat Explorer in Microsoft Defender XDR - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/step-by-step-guides/search-for-emails-and-remediate-threats
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use manual email remediation in Threat Explorer in Microsoft Defender XDR, including how to create and track remediation actions, and common scenarios for email remediation.
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
document_id: 0060617c-8fed-3745-0430-8e589b1a73e0
document_version_independent_id: 0060617c-8fed-3745-0430-8e589b1a73e0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/step-by-step-guides/search-for-emails-and-remediate-threats.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: step-by-step-guides/search-for-emails-and-remediate-threats
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/step-by-step-guides/search-for-emails-and-remediate-threats.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
platformId: c4fb2f4f-5673-e0fa-6c0e-07b5a6127342
---

# Search for emails and remediate threats using Threat Explorer in Microsoft Defender XDR - Microsoft Defender for Office 365 | Microsoft Learn

Email remediation is an already existing feature that helps admins act on emails that are threats. Before you use this feature, make sure you meet the required permissions and licensing prerequisites.

## Prerequisites

Before you begin, make sure you have the following prerequisites:

- Microsoft Defender for Office 365 Plan 2 (Included in E5 plans)
- Sufficient permissions (be sure to grant the account [Search and Purge](https://sip.security.microsoft.com/securitypermissions) role)

## Create and track the remediation

Perform the following steps to create a remediation action and track it in Action Center:

Important

For better performance, remediation should be done in batches of *50,000 or fewer*. Narrow down the search result by using *latest delivery location* and trigger email remediation if the email is in remediable folder like Inbox, Junk, Deleted, for example.

1. **Select a threat to remediate** in [Threat Explorer](https://security.microsoft.com/threatexplorer) and select ![](../media/defender-portal-icon-take-actions.png)**Take action**, which offers you options such as *Soft Delete* or *Hard Delete*.
2. The side pane opens and asks for details, like a name for the remediation, severity, and description. Once the information is reviewed, select **Submit**.
3. As soon as the admin approves the remediation action, the admin sees the Approval ID and a link to the [Microsoft Defender XDR Action Center history](https://security.microsoft.com/action-center/history) page. The Action Center History page is where **actions can be tracked**.
    1. **Admin action alert** - A system alert shows up in the alert queue with the name 'Administrative action submitted by an Administrator'. The alert indicates that an admin submitted a remediation action for an entity. It gives details such as the name of the admin who took the action, and the investigation link and time. The alert helps admins track important actions, like remediation, taken on entities.
    2. **Admin action investigation** - Since the analysis on entities was already done by the admin and that analysis led to the remediation action, no more analysis is done by the system. The admin action investigation shows details such as related alert, entity selected for remediation, action taken, remediation status, entity count, and approver of the action. The admin action investigation record allows admins to keep track of the investigation and actions carried out *manually*.
4. **Action logs in unified action center** - History and action logs for email actions like soft delete and move to deleted items folder, are *all available in a centralized view* under the unified **Action Center** &gt; **History tab**.
5. **Filters in unified action center** - There are multiple filters such as remediation name, approval ID, Investigation ID, status, action source, and action type. These filters are useful for finding and tracking email actions in the unified Action Center.

Important

For better performance, remediation should be done in batches of *50,000 or fewer*. Narrow down the search result by using *latest delivery location* and trigger email remediation if the email is in remediable folder like Inbox, Junk, Deleted, for example.

## Scenarios that call for email remediation

Here are scenarios of email remediation:

1. As part of an investigation, a security operations (SecOps) team identifies a threat in an end-user's mailbox and wants to clear out the problem emails.
2. When suggested email actions in Automated Investigation and Response (AIR) are approved by SecOps, the remediation action triggers automatically for the email or email cluster identified by AIR.

Two manual email remediation scenarios:

1. The main scenario:
    1. Manual actions taken on emails (for example, using Threat Explorer or Advanced Hunting) are only visible in the legacy Defender for Office 365 Action Center (Email and Collaboration &gt; Review &gt; Action Center in Action center - Microsoft 365 security).
2. Two-step approval scenario:
    1. Manual actions pending approval using the two-step approval process (1. The email was added to remediation by one analyst, 2. The email was reviewed and approved by another analyst).

Given the common scenarios, email remediation can be triggered in three different ways.

1. **Query based remediation**: By selecting all the search results with a query (200,000 emails can be submitted at a maximum).
2. **Handpicked remediation**: Selecting emails one-by-one by clicking on the check box (100 emails can be submitted at one time).
3. **Query based remediation with exclusions**: Selecting all emails, and then manually removing a few messages (the query can hold a maximum of 1,000 emails and the maximum number of exclusions is 100).