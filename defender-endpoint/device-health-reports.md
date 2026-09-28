---
layout: Conceptual
title: Device health reporting in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/device-health-reports
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use the device health report to track device health, antivirus status and versions, OS platforms, and Windows 10 versions.
ms.service: defender-endpoint
ms.author: lwainstein
author: limwainstein
ms.localizationpriority: medium
ms.date: 2026-07-03T00:00:00.0000000Z
ms.collection:
- m365-security
- tier2
ms.topic: how-to
ms.subservice: ngp
ms.reviewer: mkaminska
ms.custom: sfi-ga-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 00ad28af-a22b-2460-3473-63d0a874515e
document_version_independent_id: 00ad28af-a22b-2460-3473-63d0a874515e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/device-health-reports.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: device-health-reports
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/device-health-reports.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: beebe01f-29b6-c17c-de84-82c335e202c8
---

# Device health reporting in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

- [Microsoft Defender for Business](/en-us/defender-business/mdb-overview)

The Device Health report provides information about the devices in your organization. The Device Health report includes trending information showing the sensor health state, antivirus status, OS platforms, Windows 10 versions, and Microsoft Defender Antivirus update versions.

Important

For Windows Server 2012 R2 and Windows Server 2016 to appear in device health reports, these devices must be onboarded using the modern unified solution package. For more information, see [New functionality in the modern unified solution for Windows Server 2012 R2 and 2016](onboard-server#functionality-in-the-modern-unified-solution-for-windows-server-2016-and-windows-server-2012-r2).

In the Microsoft Defender portal navigation panel, select **Reports**, and then open **Device health and compliance**. The **Device health and compliance** dashboard in the Microsoft Defender portal is structured in two tabs:

- The [**Sensor health & OS** tab](device-health-sensor-health-os#sensor-health--os-tab) provides general operating system information, divided into three cards that display the following device attributes:

    - [Sensor health card](device-health-sensor-health-os#sensor-health-card)
    - [Operating systems and platforms card](device-health-sensor-health-os#operating-systems-and-platforms-card)
    - [Windows versions card](device-health-sensor-health-os#windows-versions-card)
- The [**Microsoft Defender Antivirus health** tab](device-health-microsoft-defender-antivirus-health#microsoft-defender-antivirus-health-tab) has eight cards that report on aspects of Microsoft Defender Antivirus:

    - [Antivirus mode card](device-health-microsoft-defender-antivirus-health#antivirus-mode-card)
    - [Antivirus engine version card](device-health-microsoft-defender-antivirus-health#antivirus-engine-version-card)
    - [Antivirus security intelligence version card](device-health-microsoft-defender-antivirus-health#antivirus-security-intelligence-version-card)
    - [Antivirus platform version card](device-health-microsoft-defender-antivirus-health#antivirus-platform-version-card)
    - [Recent antivirus scan results card](device-health-microsoft-defender-antivirus-health#recent-antivirus-scan-results-card)
    - [Antivirus engine updates card](device-health-microsoft-defender-antivirus-health#antivirus-engine-updates-card)
    - [Security intelligence updates card](device-health-microsoft-defender-antivirus-health#security-intelligence-updates-card)
    - [Antivirus platform updates card](device-health-microsoft-defender-antivirus-health#antivirus-platform-updates-card)

## Report access permissions

To access the Device Health report (the **Device health and compliance** dashboard) in the Microsoft Defender portal, the following permissions are required:

| Permission name | Permission type |
| --- | --- |
| View Data | Threat and vulnerability management (TVM) |

Important

Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

To assign the View Data - Threat and vulnerability management (TVM) permission for the Device health and antivirus compliance report:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com) using account with Security administrator or Global administrator role assigned.
2. In the navigation pane, select **Settings** &gt; **Endpoints** &gt; **Roles** (under **Permissions**).
3. Select the role you'd like to edit.
4. Select **Edit**.
5. In **Edit role**, on the **General** tab, in **Role name**, type a name for the role.
6. In **Description** type a brief summary of the role.
7. In **Permissions**, select **View Data**, and under **View Data** select **Threat and vulnerability management** (TVM).