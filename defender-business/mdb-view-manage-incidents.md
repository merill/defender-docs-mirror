---
layout: Conceptual
title: View and manage incidents in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-business/mdb-view-manage-incidents
breadcrumb_path: /defender-business/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to monitor and manage incidents and alerts, and understand alert severity levels in Microsoft Defender for Business.
author: chrisda
ms.author: chrisda
ms.topic: how-to
ms.service: defender-business
ms.localizationpriority: medium
ms.date: 2026-07-03T00:00:00.0000000Z
ms.reviewer: nehabha
ms.collection:
- SMB
- m365-security
- m365-initiative-defender-business
- tier1
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 933d9c03-cac6-d857-df0a-647c2192e119
document_version_independent_id: 933d9c03-cac6-d857-df0a-647c2192e119
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-business/mdb-view-manage-incidents.md
site_name: Docs
depot_name: Learn.defender-business
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdb-view-manage-incidents
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-business/mdb-view-manage-incidents.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b11ae577-8d18-47ab-998c-ea182a941e71
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/87b1d24d-826d-4337-90a0-b6c35e4561f2
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 63f11864-038b-fbc0-535b-9bf734a029fa
---

# View and manage incidents in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn

As threats are detected and alerts are triggered, incidents are created. Your company's security team can view and manage incidents in the Microsoft Defender portal. You must have appropriate permissions assigned to perform the tasks in this article. See [Security roles and permissions in Microsoft Defender for Business](mdb-roles-permissions).

**This article includes**:

- How to monitor your incidents and alerts
- Understand alert severity levels
- Next steps

## Monitor your incidents and alerts

Use the following steps to view and manage incidents in the Microsoft Defender portal:

Important

If you see an incident tagged with `Attack disruption`, it means an advanced attack was detected. See [Automatic attack disruption](mdb-attack-disruption).

1. In the [Microsoft Defender portal](https://security.microsoft.com), in the navigation pane, go to **Incidents & alerts**, and then select **Incidents**. Any incidents that were created are listed on the page.
2. Select an alert to open its flyout pane, where you can learn more about the alert.

    ![Screenshot of incident selected with flyout open](media/mdb-incident-flyout.png)
3. In the flyout pane, you can do the following tasks:

    - See the alert title.
    - View a list of assets (such as devices or user accounts) that were affected.
    - Take available actions.
    - Use links to view more information and even open the details page for the selected alert.

Tip

Defender for Business is designed to help you address detected threats by recommending actions you can take. When you view an alert, look for these suggestions. The detected threat severity and the level of risk to your company determines the alert severity.

## Alert severity

When a threat is detected, a severity level is assigned to each alert that is generated.

- Microsoft Defender Antivirus assigns an alert severity based on the absolute severity of a detected threat (such as malware) and the potential risk to an individual device (if infected).
- Defender for Business assigns an alert severity based on the following factors:
    - The severity of the detected behavior.
    - The actual risk to a device.
    - The potential risk to your company.

The following table lists a few examples of alerts and their severity levels:

| Scenario | Alert severity and reason |
| --- | --- |
| [Automated attack disruption](mdb-attack-disruption) detects an advanced attack, and contains devices or user accounts to help prevent the attack from proceeding. | **High**. Attack disruption capabilities help contain an attack so your IT/security team can address it. |
| Microsoft Defender Antivirus detects and stops a threat before it does any damage. | **Informational**. The threat was stopped before any damage was done. |
| Microsoft Defender Antivirus detects malware that was executing within your company. The malware is stopped and remediated. | **Low**. Although some damage might occur to an individual device, the malware no longer poses a threat to your company. |
| Defender for Business detects active malware. The malware is blocked almost immediately. | **Medium** or **High**. The malware poses a threat to individual devices and to your company. |
| Suspicious behavior is detected but no remediation actions are taken yet. | **Low**, **Medium**, or **High**. The severity depends on the degree to which the behavior poses a threat to your company. |