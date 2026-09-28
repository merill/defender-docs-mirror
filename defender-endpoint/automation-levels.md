---
layout: Conceptual
title: Automation levels in automated investigation and remediation - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/automation-levels
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Get an overview of automation levels and how they work in Microsoft Defender for Endpoint
author: chrisda
ms.service: defender-endpoint
ms.subservice: edr
ms.author: chrisda
ms.localizationpriority: medium
ms.date: 2025-04-04T00:00:00.0000000Z
ms.collection:
- m365-security
- tier3
- mde-edr
ms.topic: article
ms.custom: AIR
locale: en-us
document_id: 8ce370b3-9431-a7f5-5bdf-8fe6b400ba4c
document_version_independent_id: 8ce370b3-9431-a7f5-5bdf-8fe6b400ba4c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/automation-levels.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: automation-levels
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/automation-levels.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
platformId: 2e604ed7-dd49-948b-501c-300b64151fb7
---

# Automation levels in automated investigation and remediation - Microsoft Defender for Endpoint | Microsoft Learn

Automated investigation and remediation (AIR) capabilities in Microsoft Defender for Business are preconfigured and aren't configurable. In Microsoft Defender for Endpoint, you can configure AIR to one of several levels of automation. Your automation level affects whether remediation actions following AIR investigations are taken automatically or only upon approval.

Important

As of September 1, 2026, Automated Investigation and Response (AIR) will no longer run as a separate investigation experience or be available for manual triggering in Microsoft Defender.

AIR detection and response capabilities are already included in Microsoft Defender's default antivirus protection stack and run automatically. For on-demand investigations, run a full antivirus scan as needed.

- *Full automation* (recommended) means remediation actions are taken automatically on artifacts determined to be malicious. (*Full automation is set by default in Defender for Business*.)
- *Semi-automation* means some remediation actions are taken automatically, but other remediation actions await approval before being taken. (See the table in Levels of automation.)
- All remediation actions, whether pending or completed, are tracked in the Action Center (https://security.microsoft.com).

Tip

For best results, we recommend using full automation when you [configure AIR](configure-automated-investigations-remediation). Data collected and analyzed over the past year shows that customers who are using full automation had 40% more high-confidence malware samples removed than customers who are using lower levels of automation. Full automation can help free up your security operations resources to focus more on your strategic initiatives.

Note

Device group creation is supported in Defender for Endpoint Plan 1 and Plan 2.

## Levels of automation

| Automation level | Description |
| --- | --- |
| **Full - remediate threats automatically** (also referred to as *full automation*) | With full automation, remediation actions are performed automatically on entities that are considered to be malicious. All remediation actions that are taken can be viewed in the [Action Center](auto-investigation-action-center) on the **History** tab. If necessary, a remediation action can be undone. <br>***Full automation is recommended** and is selected by default for tenants with Defender for Endpoint that were created on or after August 16, 2020, with no device groups defined yet.*<br><br>*Full automation is set by default in Defender for Business.* |
| **Semi - require approval for all folders** (also referred to as *semi-automation*) | With this level of semi-automation, approval is required for remediation actions on all files. Such pending actions can be viewed and approved in the [Action Center](auto-investigation-action-center), on the **Pending** tab. Pending actions time out after seven days. If an action times out, the behavior is the same as if the action is rejected. <br>*This level of semi-automation is selected by default for tenants that were created before August 16, 2020 with Microsoft Defender for Endpoint, with no device groups defined.* |
| **Semi - require approval for core folders remediation** (also a type of *semi-automation*) | With this level of semi-automation, approval is required for any remediation actions needed on files or executables that are in core folders. Core folders include operating system directories, such as the **Windows** (`\windows\*`). <br> Remediation actions can be taken automatically on files or executables that are in other (noncore) folders. <br><br> Pending actions for files or executables in core folders can be viewed and approved in the [Action Center](auto-investigation-action-center), on the **Pending** tab. <br><br> Actions that were taken on files or executables in other folders can be viewed in the [Action Center](auto-investigation-action-center), on the **History** tab. |
| **Semi - require approval for non-temp folders remediation** (also a type of *semi-automation*) | With this level of semi-automation, approval is required for any remediation actions needed on files or executables that aren't\* in temporary folders. <br> Temporary folders can include the following examples: <br><br>- `\users\*\appdata\local\temp\*`<br>- `\documents and settings\*\local settings\temp\*`<br>- `\documents and settings\*\local settings\temporary\*`<br>- `\windows\temp\*`<br>- `\users\*\downloads\*`<br>- `\program files\`<br>- `\program files (x86)\*`<br>- `\documents and settings\*\users\*`<br><br><br> Remediation actions can be taken automatically on files or executables that are in temporary folders. <br><br> Pending actions for files or executables that aren't in temporary folders can be viewed and approved in the [Action Center](auto-investigation-action-center), on the **Pending** tab. <br><br> Actions that were taken on files or executables in temporary folders can be viewed and approved in the [Action Center](auto-investigation-action-center), on the **History** tab. |
| **No automated response** (also referred to as *no automation*) | With no automation, automated investigation doesn't run on your organization's devices. As a result, no remediation actions are taken or pending as a result of automated investigation. However, other threat protection features, such as [protection from potentially unwanted applications](detect-block-potentially-unwanted-apps-microsoft-defender-antivirus), can be in effect, depending on how your antivirus and next-generation protection features are configured. <br> \***Using the *no automation* option is not recommended**, because it reduces the security posture of your organization's devices. [Consider setting up your automation level to full automation (or at least semi-automation)](machine-groups). |

## Important points about automation levels

- Full automation has proven to be reliable, efficient, and safe, and is recommended for all customers. Full automation frees up your critical security resources so they can focus more on your strategic initiatives.
- New tenants (which include tenants that were created on or after August 16, 2020) with Defender for Endpoint are set to full automation by default.
- [Defender for Business](/en-us/defender-business/mdb-overview) uses full automation by default. Defender for Business doesn't use device groups the same way as Defender for Endpoint. Thus, full automation is turned on and applied to all devices in Defender for Business.
- If your security team has defined device groups with a level of automation, those settings aren't changed by the new default settings that are rolling out.
- You can keep your default automation settings, or change them according to your organizational needs. To change your settings, [set your level of automation](configure-automated-investigations-remediation#set-up-device-groups).

Note

[Defender for Business](/en-us/defender-business/mdb-overview) depends on real-time protection for automatic investigation. Real-time protection must be enabled and in active mode to enable automatic investigation.