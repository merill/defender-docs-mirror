---
layout: Conceptual
title: Visit the Action center to see remediation actions - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/auto-investigation-action-center
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use the action center to view details and results following an automated investigation
ms.service: defender-endpoint
ms.subservice: edr
author: chrisda
ms.author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-edr
ms.custom: msecd-doc-authoring-1016 - admindeeplinkDEFENDER - sfi-image-nochange
ms.topic: how-to
ms.reviewer: ramarom, evaldm, isco, mabraitm, chriggs
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 14931acd-c32f-86e1-9287-3b383e3b8c78
document_version_independent_id: 14931acd-c32f-86e1-9287-3b383e3b8c78
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/auto-investigation-action-center.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: auto-investigation-action-center
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/auto-investigation-action-center.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 82943d8b-b01e-5e0c-0f6e-eb160795058d
---

# Visit the Action center to see remediation actions - Microsoft Defender for Endpoint | Microsoft Learn

This article explains how to use the Action center in Microsoft Defender for Endpoint to review pending and completed remediation actions, approve actions when required, and understand action status.

During and after an automated investigation, remediation actions for threat detections are identified. Depending on the particular threat and how [automated investigation and remediation capabilities are configured](configure-automated-investigations-remediation) for your organization, some remediation actions are taken automatically, and others require approval. If you're part of your organization's security operations team, you can view pending and completed [remediation actions](manage-auto-investigation#remediation-actions) in the **Action center**.

## Overview of the unified Action center

Recently, the Action center was updated. You now have a unified Action center experience. To access your Action center, go to the [Action center in the Microsoft Defender portal](https://security.microsoft.com/action-center) and sign in.

[![The Action center page in the Microsoft Defender portal](media/mde-action-center-unified.png)](media/mde-action-center-unified.png#lightbox)

### What's changed?

The following table compares the new, unified Action center to the previous Action center.

| The new, unified Action center | The previous Action center |
| --- | --- |
| Lists pending and completed actions for devices and email in one location ([Microsoft Defender for Endpoint](microsoft-defender-endpoint) plus [Microsoft Defender for Office 365](/en-us/defender-office-365/mdo-about) | Lists pending and completed actions for devices  ([Microsoft Defender for Endpoint](microsoft-defender-endpoint) only) |
| Is located at:[Microsoft Defender Action center](https://security.microsoft.com/action-center) | Is located at:[Previous Action center portal](https://securitycenter.windows.com/action-center) |
| In the [Microsoft Defender portal](https://security.microsoft.com), choose **Action center**. <br>[![The navigation pane to the Action Center in the Microsoft Defender portal](media/action-center-nav-new.png)](media/action-center-nav-new.png#lightbox) | In the Microsoft Defender portal, choose **Automated investigations** &gt; **Action center**. <br>[![An older version of the navigation pane to the Action Center in the Microsoft Defender portal](media/action-center-nav-old.png)](media/action-center-nav-old.png#lightbox) |

The unified Action center brings together remediation actions across Defender for Endpoint and Defender for Office 365. It defines a common language for all remediation actions, and provides a unified investigation experience.

You can use the unified Action center if you have appropriate permissions and one or more of the following subscriptions:

- [Microsoft Defender XDR](/en-us/defender-xdr/microsoft-365-defender)
- [Defender for Endpoint](microsoft-defender-endpoint)
- [Defender for Office 365](/en-us/defender-office-365/mdo-about)
- [Defender for Business](/en-us/defender-business/mdb-overview)

## Use the Action center

To get to the unified Action center in the improved Microsoft Defender portal:

1. Go to the [Microsoft Defender portal](https://security.microsoft.com) and sign in.
2. In the navigation pane, select **Action center**.
3. Use the **Pending actions** and **History** tabs. The following table summarizes what you'll see on each tab:

    | Tab | Description |
    | --- | --- |
    | **Pending** | Displays a list of actions that require attention. You can approve or reject actions one at a time, or select multiple actions if they have the same type of action (such as **Quarantine file**). <br>**TIP**: Make sure to [review and approve (or reject) pending actions](manage-auto-investigation) as soon as possible so that your automated investigations can complete in a timely manner. |
    | **History** | Serves as an audit log for actions that were taken, such as:<br>    - Remediation actions that were taken as a result of automated investigations<br>    - Remediation actions that were approved by your security operations team<br>    - Commands that were run and remediation actions that were applied during Live Response sessions<br>    - Remediation actions that were taken by threat protection features in Microsoft Defender Antivirus<br><br><br> Provides a way to undo certain actions (see [Undo completed actions](manage-auto-investigation#undo-completed-actions)). |
4. To customize, sort, filter, and export data in the Action center, take one or more of the following steps:

    [![The Action center with Columns and filters](media/new-action-center-columnsfilters.png)](media/new-action-center-columnsfilters.png#lightbox)

    - Select a column heading to sort items in ascending or descending order.
    - Use the time period filter to view data for the past day, week, 30 days, or 6 months.
    - Choose the columns that you want to view.
    - Specify how many items to include on each page of data.
    - Use filters to view just the items you want to see.
    - Select **Export** to export results to a .csv file.