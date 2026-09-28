---
layout: Conceptual
title: Prioritize and manage Automated Investigations and Response (AIR) - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/step-by-step-guides/how-to-prioritize-and-manage-automated-investigations-and-response-air
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Analyze investigations and approve Automated Investigation and Response (AIR) actions from the Action Center. Learn how AIR assesses threat scope and recommends remediation actions in Microsoft Defender for Office 365.
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
document_id: 635b9004-5187-38e4-4356-4cd4be9eeca7
document_version_independent_id: 635b9004-5187-38e4-4356-4cd4be9eeca7
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/step-by-step-guides/how-to-prioritize-and-manage-automated-investigations-and-response-air.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: step-by-step-guides/how-to-prioritize-and-manage-automated-investigations-and-response-air
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/step-by-step-guides/how-to-prioritize-and-manage-automated-investigations-and-response-air.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 9839126f-a475-5628-eba0-123834549a72
---

# Prioritize and manage Automated Investigations and Response (AIR) - Microsoft Defender for Office 365 | Microsoft Learn

Automated Investigation and Response (AIR) saves your security operations team time and effort. This article explains how to review, approve, and manage AIR actions from the Action Center in the Microsoft Defender portal.

- When alerts are triggered, automated investigation will determine the scope of impact of a threat in your organization and provide recommended remediation actions.
- Security teams can save time by leveraging AIR automation to reduce the need for manual hunting.
- These investigations can identify emails that haven't been cleaned-up by Zero-hour Auto Purge (ZAP) or other remediation.
- AIR investigations also identify mailbox configurations that may be risky or indicate a compromised mailbox.

Investigation actions (and investigations) are accessible from several points in the Microsoft Security portal: via *Incidents*, via *Alerts*, or via *Action Center*. Whether an admin uses Incidents, Alerts, or Action Center depends on the workflow the admin is pursuing.

## Why use the Action Center workflow

As automated investigations on *Email & collaboration* content results in verdicts, such as *Malicious* or *Suspicious*, certain remediation actions are created. The remediation actions suggested aren't carried out automatically. SecOps must navigate to each investigation to *approve* those suggested actions. In the *Action Center* all the pending actions are aggregated for quick approval.

## Prerequisites

- Microsoft Defender for Office 365 Plan 2 or higher (Included with E5)
- Sufficient permissions (Security reader, security operations, or security administrator, plus [Search and purge](../mdo-portal-permissions) role)

## Steps to analyze and approve AIR actions directly from the Action Center

Perform the following steps to review and approve pending AIR actions in the Action Center:

1. Navigate to [Microsoft Defender portal](https://security.microsoft.com/action-center) and sign in.
2. When the Action center loads, filter and prioritize by clicking columns to sort the actions, or press **Filters** to apply a filter such as *entity type* (for a particular URL) or action type (such as soft delete email).
3. A flyout will open once an action is clicked. The flyout appears on the right-hand side of the screen for review.
4. For more information about why an action is requested, select **Open investigation page** in the flyout to learn more about the investigation or alerts linked to the selected action. (Admins can also approve actions seen on the investigation page by selecting the *Pending Actions* tab.)
5. If you don't need more investigation details, select **Approve** to take the recommended action directly from the Action Center.
6. Reject the action, if you determine it's unnecessary.

## Check AIR history

Use the following steps to review the history of AIR actions in the Action Center:

1. Navigate to the [Microsoft Defender portal](https://security.microsoft.com) and sign in.
2. In the left-hand navigation pane, expand **Action & submissions** then click **Action Center**.
3. When the Action Center loads press the **History** tab.
4. View the history of AIR, including decisions made, source of action, and admin who made the decision, if appropriate.