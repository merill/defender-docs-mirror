---
layout: Conceptual
title: Get notified about remediation actions - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/m365d-remediation-actions
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Get an overview of remediation actions that follow automated investigations in the Microsoft Defender portal
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.topic: concept-article
ms.custom: autoir
ms.reviewer: evaldm, isco
ms.date: 2025-04-28T00:00:00.0000000Z
locale: en-us
document_id: 4786f62a-77f4-a32b-3268-83e2f0ce5d3d
document_version_independent_id: 4786f62a-77f4-a32b-3268-83e2f0ce5d3d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/m365d-remediation-actions.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: m365d-remediation-actions
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/m365d-remediation-actions.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 6579c092-946d-1784-fdd0-45eb90ec883e
---

# Get notified about remediation actions - Microsoft Defender XDR | Microsoft Learn

Important

As of September 1, 2026, automated Investigation and Response (AIR) will no longer run as a separate investigation experience or be available for manual triggering in Microsoft Defender for Endpoint alerts and remediations.

- AIR detection and response capabilities for Defender for Endpoint are already included in Microsoft Defender for Endpoint's default antivirus protection stack and run automatically. For on-demand investigations, run a full antivirus scan as needed.
- This change applies only to Microsoft Defender for Endpoint. AIR capabilities for Defender for Office 365 remain available.

During and after an automated investigation, remediation actions are identified for malicious or suspicious items. Some kinds of remediation actions are taken on devices, also referred to as endpoints. Other remediation actions are taken on identities, accounts, and email content. In addition, some types of remediation actions can occur automatically, whereas other types of remediation actions are taken manually by your organization's security team. When an automated investigation results in one or more remediation actions, the investigation completes only when the remediation actions are taken, approved, or rejected.

Important

Whether remediation actions are taken automatically or only upon approval depends on certain settings, such as automation levels. To learn more, see the following articles:

- [Configure your automated investigation and response capabilities in Microsoft Defender XDR](m365d-configure-auto-investigation-response)
- [Configure action accounts in Microsoft Defender for Identity](/en-us/defender-for-identity/manage-action-accounts)
- [How threats are remediated on devices](/en-us/defender-endpoint/automated-investigations)
- [Threats and remediation actions on email & collaboration content](/en-us/defender-office-365/air-remediation-actions#threats-and-remediation-actions)

The following table summarizes remediation actions that are currently supported in Microsoft Defender XDR.

| Device (endpoint) remediation actions | Email remediation actions | Users (accounts) |
| --- | --- | --- |
| - Collect investigation package - Isolate device (this action can be undone)- Offboard machine - Release code execution - Release from quarantine - Request sample - Restrict code execution (this action can be undone) - Run antivirus scan - Stop and quarantine - Contain devices from the network | - Block URL (time-of-click)- Soft delete email messages or clusters- Quarantine email- Quarantine an email attachment- Turn off external mail forwarding | - Disable user- Reset user password- Confirm user as compromised |

Remediation actions, whether pending approval or already complete, can be viewed in the [Action center](m365d-action-center).

## Remediation actions that follow automated investigations

When an automated investigation completes, a verdict is reached for every piece of evidence involved. Depending on the verdict, remediation actions are identified. In some cases, remediation actions are taken automatically; in other cases, remediation actions await approval. It all depends on how [automated investigation and response is configured](m365d-configure-auto-investigation-response).

The following table lists possible verdicts and outcomes:

| Verdict | Affected entities | Outcomes |
| --- | --- | --- |
| Malicious | Devices (endpoints) | Remediation actions are taken automatically (assuming your organization's [device groups](m365d-configure-auto-investigation-response#review-or-change-the-automation-level-for-device-groups) are set to **Full - remediate threats automatically**) |
| Compromised | Users | Remediation actions are taken automatically |
| Malicious | Email content (URLs or attachments) | Recommended remediation actions are pending approval |
| Suspicious | Devices or email content | Recommended remediation actions are pending approval |
| No threats found | Devices or email content | No remediation actions are needed |

## Remediation actions that are taken manually

In addition to remediation actions that follow automated investigations, your security operations team can take certain remediation actions manually. These actions include:

- Manual device action, such as device isolation or file quarantine
- Manual email action, such as soft-deleting email messages
- Manual user action, such as disable user or reset user password
- [Advanced hunting](advanced-hunting-overview) action on devices, users, or email
- [Explorer](/en-us/defender-office-365/threat-explorer-real-time-detections-about) action on email content, such as moving email to junk, soft-deleting email, or hard-deleting email
- Manual [live response](/en-us/windows/security/threat-protection/microsoft-defender-atp/live-response) action, such as deleting a file, stopping a process, and removing a scheduled task
- Live response action with [Microsoft Defender for Endpoint APIs](/en-us/defender-endpoint/api/management-apis#microsoft-defender-for-endpoint-apis), such as isolating a device, running an antivirus scan, and getting information about a file