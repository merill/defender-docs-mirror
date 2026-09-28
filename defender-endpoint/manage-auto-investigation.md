---
layout: Conceptual
title: Review remediation actions following automated investigations - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/manage-auto-investigation
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Review and approve (or reject) remediation actions following an automated investigation.
ms.service: defender-endpoint
author: chrisda
ms.author: chrisda
ms.localizationpriority: medium
ms.date: 2026-07-02T00:00:00.0000000Z
ms.collection:
- m365-security
- tier2
- mde-edr
ms.custom: admindeeplinkDEFENDER, msecd-doc-authoring-1016
ms.topic: how-to
ms.subservice: edr
ai-usage: ai-assisted
locale: en-us
document_id: 63d3aba6-6bb0-1a20-2eb4-efc512ad3fc9
document_version_independent_id: 63d3aba6-6bb0-1a20-2eb4-efc512ad3fc9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/manage-auto-investigation.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: manage-auto-investigation
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/manage-auto-investigation.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: d0dd8af1-8d8e-f518-58c3-517d7a03b8da
---

# Review remediation actions following automated investigations - Microsoft Defender for Endpoint | Microsoft Learn

This article explains how to review, approve, or reject remediation actions that result from automated investigations in Microsoft Defender for Endpoint. Depending on your organization's automation settings, some remediation actions are taken automatically while others require approval.

## Remediation actions

When an [automated investigation](automated-investigations) runs, a verdict is generated for each piece of evidence investigated. Verdicts can be *Malicious*, *Suspicious*, or *No threats found*.

Whether remediation actions occur automatically or require approval by your organization's security operations team depends on the type of threat, the resulting verdict, and how your organization's [device groups](machine-groups) are configured.

Note

Device group creation is supported in Defender for Endpoint Plan 1 and Plan 2.

Here are a few examples:

- **Example 1**: Fabrikam's device groups are set to **Full - remediate threats automatically** (the recommended setting). With this setting, remediation actions are taken automatically for artifacts that are considered to be malicious following an automated investigation (see Review completed actions).
- **Example 2**: Contoso's devices are included in a device group that is set for **Semi - require approval for any remediation**. With this setting, Contoso's security operations team must review and approve all remediation actions following an automated investigation (see Review pending actions).
- **Example 3**: Tailspin Toys has their device groups set to **No automated response** (not recommended). With this setting, automated investigations don't occur. No remediation actions are taken or pending, and no actions are logged in the [Action center](auto-investigation-action-center) for their devices (see [Manage device groups](machine-groups#manage-device-groups)).

Whether taken automatically or upon approval, an automated investigation and remediation can result in one or more of the remediation actions:

- Quarantine a file
- Remove a registry key
- Kill a process
- Stop a service
- Disable a driver
- Remove a scheduled task

## Review pending actions

To review pending remediation actions in the Action center, perform the following steps:

1. Go to the [Microsoft Defender portal](https://security.microsoft.com) and sign in.
2. In the navigation pane, choose **Action center**.
3. Review the items on the **Pending** tab.
4. Select an action to open its flyout pane.
5. In the flyout pane, review the information, and then take one of the following steps:

    - Select **Open investigation page** to view more details about the investigation.
    - Select **Approve** to initiate a pending action.
    - Select **Reject** to prevent a pending action from being taken.
    - Select **Go hunt** to go into [Advanced hunting](/en-us/defender-xdr/advanced-hunting-overview).

### Approve or reject remediation actions

For incidents with a remediation status of **Pending approval**, you can also approve or reject a remediation action from within the incident.

1. In the navigation pane, go to **Incidents & alerts** &gt; **Incidents**.
2. Filter on **Pending action** for the Automated investigation state (optional).
3. Select an incident name to open its summary page.
4. Select the **Evidence and Response** tab.
5. Select an item in the list to open its flyout pane.
6. Review the information, and then take one of the following steps:
    - Select the Approve pending action option to initiate a pending action.
    - Select the Reject pending action option to prevent a pending action from being taken.

[![The Approve\Reject option in the Evidence and Response management pane for an incident in the Microsoft Defender portal](/en-us/defender/media/defender/m365-defender-approve-reject-action.png)](/en-us/defender/media/defender/m365-defender-approve-reject-action.png#lightbox)

## Review completed actions

To review completed remediation actions, follow these steps:

1. Go to the [Microsoft Defender portal](https://security.microsoft.com) and sign in.
2. In the navigation pane, choose **Action center**.
3. Review the items on the **History** tab.
4. Select an item to view more details about that remediation action.

## Undo completed actions

If you've determined that a device or a file isn't a threat, you can undo remediation actions that were taken, whether those actions were taken automatically or manually. In the Action center, on the **History** tab, you can undo any of the following actions:

| Action source | Supported Actions |
| --- | --- |
| - Automated investigation<br>- Manual response actions (see the note below)<br>- Microsoft Defender Antivirus | - Disable a driver<br>- Isolate device<br>- Quarantine a file<br>- Remove a registry key<br>- Remove a scheduled task<br>- Restrict code execution<br>- Stop a service |

Note

[Defender for Endpoint Plan 1](defender-endpoint-plan-1) and [Microsoft Defender for Business](/en-us/defender-business/mdb-overview) include only the following manual response actions:

- Run antivirus scan
- Isolate device
- Stop and quarantine a file
- Add an indicator to block or allow a file

### To undo multiple actions at one time

Use the following steps to undo multiple remediation actions at once:

1. Go to the [Action center](https://security.microsoft.com/action-center) and sign in.
2. On the **History** tab, select the actions that you want to undo. Make sure to select items that have the same Action type. A flyout pane opens.
3. In the flyout pane, select **Undo**.

### To remove a file from quarantine across multiple devices

Use the following steps to remove a quarantined file from multiple devices at once:

1. Go to the [Action center](https://security.microsoft.com/action-center) and sign in.
2. On the **History** tab, select an item that has the Action type **Quarantine file**.
3. In the flyout pane, select **Apply to X more instances of this file**, and then select **Undo**.

## Automation levels, automated investigation results, and resulting actions

Automation levels control whether remediation actions run automatically or need approval. Your security operations team might need to take extra steps based on the investigation results. The following table lists each automation level, its results, and what to do.

| Device group setting | Automated investigation results | What to do |
| --- | --- | --- |
| **Full - remediate threats automatically**(recommended) | A verdict of *Malicious* is reached for a piece of evidence. <br> Appropriate remediation actions are taken automatically. | Review completed actions |
| **Semi - require approval for any remediation** | A verdict of either *Malicious* or *Suspicious* is reached for a piece of evidence. <br> Remediation actions are pending approval to proceed. | Approve (or reject) pending actions |
| **Semi - require approval for core folders remediation** | A verdict of *Malicious* is reached for a piece of evidence. <br> If the artifact is a file or executable and is in an operating system directory, such as the Windows folder or the Program files folder, then remediation actions are pending approval. <br><br> If the artifact isn't\* in an operating system directory, remediation actions are taken automatically. | 1. Approve (or reject) pending actions<br>2. Review completed actions |
| **Semi - require approval for core folders remediation** | A verdict of *Suspicious* is reached for a piece of evidence. <br> Remediation actions are pending approval. | Approve (or reject) pending actions. |
| **Semi - require approval for non-temp folders remediation** | A verdict of *Malicious* is reached for a piece of evidence. <br> If the artifact is a file or executable that isn't in a temporary folder, such as the user's downloads folder or temp folder, remediation actions are pending approval. <br><br> If the artifact is a file or executable that *is* in a temporary folder, remediation actions are taken automatically. | 1. Approve (or reject) pending actions<br>2. Review completed actions |
| **Semi - require approval for non-temp folders remediation** | A verdict of *Suspicious* is reached for a piece of evidence. <br> Remediation actions are pending approval. | Approve (or reject) pending actions |
| Any of the **Full** or **Semi** automation levels | A verdict of *No threats found* is reached for a piece of evidence. <br> No remediation actions are taken, and no actions are pending approval. | [View details and results of automated investigations](auto-investigation-action-center) |
| **No automated response** (not recommended) | No automated investigations run, so no verdicts are reached, and no remediation actions are taken or awaiting approval. | [Consider setting up or changing your device groups to use **Full** or **Semi** automation](machine-groups) |

All verdicts are tracked in the [Action center](auto-investigation-action-center#the-unified-action-center).

Note

In [Defender for Business](/en-us/defender-business/mdb-overview), automated investigation and remediation capabilities are preset to use **Full - remediate threats automatically**. These capabilities are applied to all devices by default.