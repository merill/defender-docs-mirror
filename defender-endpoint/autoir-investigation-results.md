---
layout: Conceptual
title: View the details and results of an automated investigation - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/autoir-investigation-results
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: During and after an automated investigation, you can view the results and key findings
author: chrisda
ms.author: chrisda
ms.service: defender-endpoint
ms.subservice: edr
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-edr
ms.topic: how-to
ms.custom:
- msecd-doc-authoring-1016
- autoir
- admindeeplinkDEFENDER
ms.reviewer: evaldm, isco
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: b878bacd-e29c-559c-7828-0ad7b66101db
document_version_independent_id: b878bacd-e29c-559c-7828-0ad7b66101db
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/autoir-investigation-results.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: autoir-investigation-results
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/autoir-investigation-results.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 97be1788-8cb9-d9cb-adaf-0ee52ad0bde0
---

# View the details and results of an automated investigation - Microsoft Defender for Endpoint | Microsoft Learn

This article explains how to open and use the investigation details view in Microsoft Defender for Endpoint to monitor [automated investigation](automated-investigations) status, review evidence, and approve pending remediation actions. You can access investigation details both during and after the investigation process if you have the required permissions.

Important

As of September 1, 2026, Automated Investigation and Response (AIR) will no longer run as a separate investigation experience or be available for manual triggering in Microsoft Defender.

AIR detection and response capabilities are already included in Microsoft Defender's default antivirus protection stack and run automatically. For on-demand investigations, run a full antivirus scan as needed.

## Overview of the unified investigation page

The unified investigation page shows information about your devices, email, and collaboration content in one place. It uses a common language and gives a consistent experience for automatic investigations across [Microsoft Defender for Endpoint](microsoft-defender-endpoint) and [Microsoft Defender for Office 365](/en-us/defender-office-365/mdo-about). For more information, see [Details and results of an automated investigation](/en-us/defender-xdr/m365d-autoir-results).

## Open the investigation details view

You can open the investigation details view by using one of the following methods:

- Select an item in the Action center
- Select an investigation from an incident details page

### Select an item in the Action center

The improved [Action center](auto-investigation-action-center) brings together [remediation actions](manage-auto-investigation#remediation-actions) across your devices, email & collaboration content, and identities. Listed actions include remediation actions that were taken automatically or manually. In the Action center, you can view actions that are awaiting approval and actions that were already approved or completed. You can also navigate to more details, such as an investigation page.

1. Go to [Microsoft Defender XDR](https://go.microsoft.com/fwlink/p/?linkid=2077139) and sign in.
2. In the navigation pane, choose **Action center**.
3. On either the **Pending** or **History** tab, select an item. Its flyout pane opens.
4. Review the information in the flyout pane, and then take one of the following steps:
    - Select **Open investigation page** to view more details about the investigation.
    - Select **Approve** to initiate a pending action.
    - Select **Reject** to prevent a pending action from being taken.
    - Select **Go hunt** to go into [Advanced hunting](/en-us/defender-xdr/advanced-hunting-overview).

### Open an investigation from an incident details page

Use an incident details page to view detailed information about an incident, including alerts that were triggered information about any affected devices, user accounts, or mailboxes.

1. Go to [Microsoft Defender XDR](https://go.microsoft.com/fwlink/p/?linkid=2077139) and sign in.
2. In the navigation pane, choose **Incidents & alerts** &gt; **Incidents**.
3. Select an item in the list, and then choose **Open incident page**.
4. Select the **Investigations** tab, and then select an investigation in the list. Its flyout pane opens.
5. Select **Open investigation page**.

## Review investigation details

Use the investigation details view to see past, current, and pending activity pertaining to an investigation. The following table describes the **Investigation graph**, **Alerts**, **Devices**, **Identities**, **Key findings**, **Entities**, **Log**, and **Pending actions** tabs available in the investigation details view.

Note

- The specific tabs you see in an investigation details page depends on what your subscription includes. For example, if your subscription doesn't include Microsoft Defender for Office 365 Plan 2, you won't see a **Mailboxes** tab.
- Device group creation is supported in Defender for Endpoint Plan 1 and Plan 2.

| Tab | Description |
| --- | --- |
| **Investigation graph** | Provides a visual representation of the investigation. Depicts entities and lists threats found, along with alerts and whether any actions are awaiting approval. <br> You can select an item on the graph to view more details. For example, selecting the **Evidence** icon takes you to the **Evidence** tab, where you can see detected entities and their verdicts. |
| **Alerts** | Lists alerts associated with the investigation. Alerts can come from threat protection features on a user's device, in Office apps, Defender for Cloud Apps, and other Microsoft Defender XDR features. |
| **Devices** | Lists devices included in the investigation along with their remediation level. (Remediation levels correspond to the [automation level for device groups](automation-levels).) |
| **Mailboxes** | Lists mailboxes that are affected by detected threats. |
| **Users** | Lists user accounts that are affected by detected threats. |
| **Evidence** | Lists pieces of evidence raised by alerts/investigations. Includes verdicts (*Malicious*, *Suspicious*, or *No threats found*) and remediation status. |
| **Entities** | Provides details about each analyzed entity, including a verdict for each entity type (*Malicious*, *Suspicious*, or *No threats found*). |
| **Log** | Provides a chronological, detailed view of all the investigation actions taken after an alert was triggered. |
| **Pending actions** | Lists items that require approval to proceed. Go to the Action center (https://security.microsoft.com/action-center) to approve pending actions. |

## Understand investigation states

The following table lists investigation states and what they indicate.

| Investigation state | Definition |
| --- | --- |
| Benign | Artifacts were investigated and a determination was made that no threats were found. |
| PendingResource | An automated investigation is paused because either a remediation action is pending approval, or the device on which an artifact was found is temporarily unavailable. |
| UnsupportedAlertType | An automated investigation isn't available for this type of alert. Further investigation can be done manually, by using advanced hunting. |
| Failed | At least one investigation analyzer ran into a problem where it couldn't complete the investigation. If an investigation fails after remediation actions were approved, the remediation actions might still have succeeded. |
| Successfully remediated | An automated investigation completed, and all remediation actions were completed or approved. |

To provide more context about how investigation states appear in the Microsoft Defender portal, the following table lists alerts and their corresponding automated investigation state. This table is included as an example of what a security operations team might see in the Microsoft Defender portal.

| Alert name | Severity | Investigation state | Status | Category |
| --- | --- | --- | --- | --- |
| Malware was detected in a wim disk image file | Informational | Benign | Resolved | Malware |
| Malware was detected in a rar archive file | Informational | PendingResource | New | Malware |
| Malware was detected in a rar archive file | Informational | UnsupportedAlertType | New | Malware |
| Malware was detected in a rar archive file | Informational | UnsupportedAlertType | New | Malware |
| Malware was detected in a rar archive file | Informational | UnsupportedAlertType | New | Malware |
| Malware was detected in a zip archive file | Informational | PendingResource | New | Malware |
| Malware was detected in a zip archive file | Informational | PendingResource | New | Malware |
| Malware was detected in a zip archive file | Informational | PendingResource | New | Malware |
| Malware was detected in a zip archive file | Informational | PendingResource | New | Malware |
| Wpakill hacktool was prevented | Low | Failed | New | Malware |
| GendowsBatch hacktool was prevented | Low | Failed | New | Malware |
| Keygen hacktool was prevented | Low | Failed | New | Malware |
| Malware was detected in a zip archive file | Informational | PendingResource | New | Malware |
| Malware was detected in a rar archive file | Informational | PendingResource | New | Malware |
| Malware was detected in a rar archive file | Informational | PendingResource | New | Malware |
| Malware was detected in a zip archive file | Informational | PendingResource | New | Malware |
| Malware was detected in a rar archive file | Informational | PendingResource | New | Malware |
| Malware was detected in a rar archive file | Informational | PendingResource | New | Malware |
| Malware was detected in an iso disc image file | Informational | PendingResource | New | Malware |
| Malware was detected in an iso disc image file | Informational | PendingResource | New | Malware |
| Malware was detected in a pst outlook data file | Informational | UnsupportedAlertType | New | Malware |
| Malware was detected in a pst outlook data file | Informational | UnsupportedAlertType | New | Malware |
| MediaGet detected | Medium | PartiallyInvestigated | New | Malware |
| TrojanEmailFile | Medium | SuccessfullyRemediated | Resolved | Malware |
| CustomEnterpriseBlock malware was prevented | Informational | SuccessfullyRemediated | Resolved | Malware |
| An active CustomEnterpriseBlock malware was blocked | Low | SuccessfullyRemediated | Resolved | Malware |
| An active CustomEnterpriseBlock malware was blocked | Low | SuccessfullyRemediated | Resolved | Malware |
| An active CustomEnterpriseBlock malware was blocked | Low | SuccessfullyRemediated | Resolved | Malware |
| TrojanEmailFile | Medium | Benign | Resolved | Malware |
| CustomEnterpriseBlock malware was prevented | Informational | UnsupportedAlertType | New | Malware |
| CustomEnterpriseBlock malware was prevented | Informational | SuccessfullyRemediated | Resolved | Malware |
| TrojanEmailFile | Medium | SuccessfullyRemediated | Resolved | Malware |
| TrojanEmailFile | Medium | Benign | Resolved | Malware |
| An active CustomEnterpriseBlock malware was blocked | Low | PendingResource | New | Malware |