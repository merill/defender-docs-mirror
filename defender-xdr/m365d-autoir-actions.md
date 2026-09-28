---
layout: Conceptual
title: View and manage actions in the Action center - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/m365d-autoir-actions
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: View and manage remediation actions for affected assets using the Action center in the Microsoft Defender portal.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.date: 2026-07-02T00:00:00.0000000Z
ms.collection:
- m365-security
- tier2
ms.topic: how-to
ms.custom:
- msecd-doc-authoring-1014
- autoir
- admindeeplinkDEFENDER
ms.reviewer: evaldm, isco
ai-usage: ai-assisted
locale: en-us
document_id: 342c6968-406c-4f1d-3454-ff7162ed897e
document_version_independent_id: 342c6968-406c-4f1d-3454-ff7162ed897e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/m365d-autoir-actions.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: m365d-autoir-actions
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/m365d-autoir-actions.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 5eb7b97c-fc50-8049-8148-7a759112daf7
---

# View and manage actions in the Action center - Microsoft Defender XDR | Microsoft Learn

Important

As of September 1, 2026, automated Investigation and Response (AIR) will no longer run as a separate investigation experience or be available for manual triggering in Microsoft Defender for Endpoint alerts and remediations.

- AIR detection and response capabilities for Defender for Endpoint are already included in Microsoft Defender for Endpoint's default antivirus protection stack and run automatically. For on-demand investigations, run a full antivirus scan as needed.
- This change applies only to Microsoft Defender for Endpoint. AIR capabilities for Defender for Office 365 remain available.

Threat protection features in Microsoft Defender XDR can result in certain remediation actions. Here are some examples:

- [Automated investigations](m365d-autoir) can result in remediation actions that are taken automatically or await your approval.
- Antivirus, anti-malware, and other threat protection features can result in remediation actions, such as blocking a file, URL, or process, or sending an artifact to quarantine.
- Your security operations team can take remediation actions manually, such as during [advanced hunting](advanced-hunting-overview) or while investigating [alerts](investigate-alerts) or [incidents](investigate-incidents).

Note

You must have [required permissions for Action center tasks](m365d-action-center#required-permissions-for-action-center-tasks) to approve or reject remediation actions. For more information, see the [prerequisites for automated investigation and response](m365d-configure-auto-investigation-response#prerequisites-for-automated-investigation-and-response-in-microsoft-365-defender).

To navigate to the Action center, take one of the following steps:

- Go to the [Microsoft Defender Action center](https://security.microsoft.com/action-center); or
- In the [Microsoft Defender portal](https://security.microsoft.com), in the Automated investigation & response card, select **Approve in Action Center**.

## Review pending actions in the Action center

It's important to approve (or reject) pending actions as soon as possible so that your automated investigations can proceed and complete in a timely manner.

1. Go to [Microsoft Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2077139) and sign in.
2. In the navigation pane under Actions and submissions, choose **Action center**.
3. In the Action center, on the **Pending** tab, select an item in the list. The item's flyout pane opens. Here's an example.

    [![The options to approve or reject an action](media/air-actioncenter-itemselected.png)](media/air-actioncenter-itemselected.png#lightbox)
4. Review the information in the flyout pane, and then take one of the following steps:

    - Select **Open investigation page** to view more details about the investigation.
    - Select **Approve** to initiate a pending action.
    - Select **Reject** to prevent a pending action from being taken.
    - Select **Go hunt** to go into [Advanced hunting](advanced-hunting-overview).

Tip

You now have more options to review and approve/reject a remediation action. In addition to using the Action center, you can also approve or reject a remediation action while reviewing an incident. For more information, see [Approve or reject remediation actions](investigate-incidents#approve-or-reject-remediation-actions).

## Undo completed actions

If you determine that a device or a file isn't a threat, you can undo the remediation actions that were taken. You can undo actions whether they were taken automatically or manually. In the Action center, on the **History** tab, you can undo any of the following actions:

| Action source | Supported Actions |
| --- | --- |
| - Automated investigation - Microsoft Defender Antivirus - Manual response actions | - Isolate device - Contain device - Contain user - Restrict code execution - Quarantine a file - Remove a registry key - Stop a service - Disable a driver - Remove a scheduled task |

Note

Only Security Administrators and higher are allowed access to undo operations such as File Quarantine.

### Undo one remediation action

To undo a single remediation action:

1. Go to the [Microsoft Defender Action center](https://security.microsoft.com/action-center) and sign in.
2. On the **History** tab, select an action that you want to undo.
3. In the pane on the right side of the screen, select **Undo**.

### Undo multiple remediation actions

To undo multiple remediation actions at once:

1. Go to the [Microsoft Defender Action center](https://security.microsoft.com/action-center) and sign in.
2. On the **History** tab, select the actions that you want to undo. Make sure to select items that have the same Action type. A flyout pane opens.
3. In the flyout pane, select **Undo**.

### Remove a file from quarantine across multiple devices

To remove a quarantined file from multiple devices at once, perform the following steps:

1. Go to the Action center (https://security.microsoft.com/action-center) and sign in.
2. On the **History** tab, select a file that has a **Quarantine file** Action type.
3. In the pane on the right side of the screen, select **Apply to X more instances of the selected quarantined file**, and then select **Undo**.