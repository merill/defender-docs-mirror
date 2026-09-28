---
layout: Conceptual
title: Address false positives or false negatives in Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/m365d-autoir-report-false-positives-negatives
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Was something missed or wrongly detected by AIR in Microsoft Defender XDR? Learn how to submit false positives or false negatives to Microsoft for analysis.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.topic: how-to
ms.custom:
- msecd-doc-authoring-1014
- autoir
- admindeeplinkDEFENDER
ms.reviewer: evaldm, isco
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 8f201301-88e6-61e1-cf83-381755ff6544
document_version_independent_id: 8f201301-88e6-61e1-cf83-381755ff6544
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/m365d-autoir-report-false-positives-negatives.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: m365d-autoir-report-false-positives-negatives
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/m365d-autoir-report-false-positives-negatives.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: ff934ebf-efee-a434-be79-6a79a54a7a10
---

# Address false positives or false negatives in Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn

Important

As of September 1, 2026, automated Investigation and Response (AIR) will no longer run as a separate investigation experience or be available for manual triggering in Microsoft Defender for Endpoint alerts and remediations.

- AIR detection and response capabilities for Defender for Endpoint are already included in Microsoft Defender for Endpoint's default antivirus protection stack and run automatically. For on-demand investigations, run a full antivirus scan as needed.
- This change applies only to Microsoft Defender for Endpoint. AIR capabilities for Defender for Office 365 remain available.

False positives or negatives can occasionally occur with any threat protection solution. If [automated investigation and response capabilities](m365d-autoir) in Microsoft Defender XDR missed or wrongly detected something, there are steps your security operations team can take:

- Report a false positive/negative to Microsoft
- Adjust your alerts (if needed)
- Undo remediation actions that were taken on devices

The following sections describe how to perform these tasks.

## Report a false positive/negative to Microsoft for analysis

Use the following table to determine where to submit false positives or false negatives for analysis.

| Item missed or wrongly detected | Service | What to do |
| --- | --- | --- |
| - Email message - Email attachment - URL in an email message- URL in an Office file | [Microsoft Defender for Office 365](/en-us/defender-office-365/mdo-about) | [Submit suspected spam, phish, URLs, and files to Microsoft for scanning](/en-us/defender-office-365/submissions-admin) |
| File or app on a device | [Microsoft Defender for Endpoint](/en-us/windows/security/threat-protection) | [Submit a file to Microsoft for malware analysis](https://www.microsoft.com/wdsi/filesubmission) |

## Adjust an alert to prevent false positives from recurring

Use the following table to choose the appropriate method for preventing similar false positives from recurring.

| Scenario | Service | What to do |
| --- | --- | --- |
| - An alert is triggered by legitimate use - An alert is inaccurate | [Microsoft Defender for Cloud Apps](/en-us/cloud-app-security) or [Azure threat protection](/en-us/azure/security/fundamentals/threat-detection) | [Manage alerts in Defender for Cloud Apps](/en-us/cloud-app-security/managing-alerts) |
| A file, IP address, URL, or domain is treated as malware on a device, even though it's safe | [Microsoft Defender for Endpoint](/en-us/windows/security/threat-protection) | [Create a custom indicator with an "Allow" action](/en-us/windows/security/threat-protection/microsoft-defender-atp/manage-indicators) |

## Undo a remediation action that was taken on a device

If a remediation action was taken on an entity (such as a device or an email message) and the affected entity is not actually a threat, your security operations team can undo the remediation action in the [Action center](m365d-action-center).

1. Go to [Microsoft Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2077139) and sign in.
2. In the navigation pane, choose **Action center**.
3. On the **History** tab, select an action that you want to undo. Its flyout pane opens.
4. In the flyout pane, select **Undo**.

Tip

See [Undo completed actions](m365d-autoir-actions#undo-completed-actions).