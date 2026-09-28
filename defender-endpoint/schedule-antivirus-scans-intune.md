---
layout: Conceptual
title: Schedule antivirus scans using Microsoft Intune - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/schedule-antivirus-scans-intune
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Configure scheduled Microsoft Defender Antivirus scans in Intune, including daily and weekly schedules, CPU usage, and catch-up scans for Windows devices.
author: chrisda
ms.author: chrisda
ms.reviewer: yongrhee
ms.service: defender-endpoint
ms.topic: how-to
ms.custom: nextgen, msecd-doc-authoring-1015
ms.collection:
- m365-security
- tier2
- mde-ngp
ms.date: 2026-09-15T00:00:00.0000000Z
ms.subservice: ngp
ms.localizationpriority: medium
ai-usage: ai-assisted
locale: en-us
document_id: 021f57c4-6cc8-e3c0-24ea-798c6e9c6d97
document_version_independent_id: 021f57c4-6cc8-e3c0-24ea-798c6e9c6d97
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/schedule-antivirus-scans-intune.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: schedule-antivirus-scans-intune
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/schedule-antivirus-scans-intune.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/a72e95ff-4b4f-4cc1-90c6-7dcba67ff05f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/24dc3ccd-591a-4415-a1fe-8759afafcb12
platformId: b9f776e9-da59-bd06-081f-e5bfdd53ff4c
---

# Schedule antivirus scans using Microsoft Intune - Microsoft Defender for Endpoint | Microsoft Learn

Security administrators can use Microsoft Intune to schedule Microsoft Defender Antivirus scans on managed Windows devices. This article explains how to create an antivirus policy, schedule daily and weekly scans, and configure CPU usage and catch-up scan settings. For guidance on choosing a scan type, see [About scheduled quick or full Microsoft Defender Antivirus scans](schedule-antivirus-scans).

## Prerequisites

Before you configure scheduled antivirus scans in Intune, verify that your devices use a supported operating system.

### Supported operating systems

Intune supports scheduled antivirus scans on the following operating systems:

- Windows
- Windows Server

## Configure antivirus scans using Intune

The procedures in this article require Microsoft Intune. Intune is a separate product that isn't part of Microsoft Defender for Endpoint, and it isn't included in all subscriptions. To use Intune, you need a subscription that includes it, or you can buy it separately as a standalone subscription or add-on. If you don't have Intune, see [Schedule Microsoft Defender Antivirus scans](schedule-antivirus-scans) for other configuration methods. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).

To configure scheduled antivirus scans in Microsoft Intune, use an endpoint security **Antivirus** policy. For detailed instructions, see [Create endpoint security policies](/en-us/intune/intune-service/protect/endpoint-security-policy#create-endpoint-security-policies) or [Modify existing policies](/en-us/intune/device-configuration/endpoint-security/manage-policies#modify-existing-policies) (links open new tabs in the Intune documentation).

When you create the policy, use these specific settings:

- **Policy type**: Go to **Manage** &gt; **Antivirus** on the **Endpoint security | Overview** page at [https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/~/overview](https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/%7E/overview), and then select ![](media/defender-portal-icon-create.png)**Create policy**.
- **Platform**: Select **Windows**.
- **Profile**: Select **Microsoft Defender Antivirus**.

When you create or modify the policy, use the settings described in this article on the **Configuration settings** tab. For descriptions of all available settings, see [Configure Microsoft Defender Antivirus using Microsoft Intune](use-intune-config-manager-microsoft-defender-antivirus).

For more information, see [Antivirus policy for endpoint security in Intune](/en-us/intune/intune-service/protect/endpoint-security-antivirus-policy).

### Schedule daily quick scans using Intune

Use the following Intune setting to schedule a daily quick scan on Windows devices:

- **Setting**: **Schedule Quick Scan Time**
- **Values**:
    - ![](media/toggle-off.png)**Not Configured**
    - ![](media/toggle-on.png)**Configured**
        - Enter a time of day from **0** (12:00 AM) through **1380** (11:00 PM). The default value is **120** (2:00 AM).

For example, a value of **720** schedules the daily quick scan for 12:00 PM.

### Schedule weekly quick or full scans using Intune

Use the following Intune settings to schedule a weekly quick or full scan on Windows devices:

- **Setting**: **Scan parameter**
- **Values**:

    - **Not configured**
    - **Quick scan (Default)**
    - **Full scan**
- **Setting**: **Schedule Scan Day**
- **Values**:

    - **Not configured**
    - **Every day (Default)**
    - **Sunday** to **Saturday**
    - **No scheduled scan**
- **Setting**: **Schedule Scan Time**
- **Values**:

    - ![](media/toggle-off.png)**Not Configured**
    - ![](media/toggle-on.png)**Configured**
        - Enter a time of day from **0** (12:00 AM) through **1380** (11:00 PM). The default value is **120** (2:00 AM).

The following example schedules a quick scan on Windows devices every Wednesday at 5:00 PM (**1020**):

| Setting | Value |
| --- | --- |
| Scan parameter | Quick scan (Default) |
| Schedule Scan Day | Wednesday |
| Schedule Scan Time | ![](media/toggle-on.png)**Configured** **1020** |

Tip

Microsoft recommends using quick scans with always-on real-time protection and [cloud protection](cloud-protection-microsoft-defender-antivirus). This combination provides strong coverage against malware that starts with the system and kernel-level malware. Quick scans with always-on real-time protection and cloud protection are the default configuration.

In general, you don't need to schedule a full scan, and most users never need to run full scans manually. For more information, see [Comparing quick scan, full scan, and custom scan](schedule-antivirus-scans).

### Configure general settings for scheduled scans

Review the following general scheduled-scan settings when you configure the policy:

- **Setting**: **Check For Signatures Before Running Scan**
- **Values**:

    - **Not configured**
    - **Disabled (Default)**
    - **Enabled** (recommended)
- **Setting**: **Randomize Schedule Task Times**
- **Values**:

    - **Not configured**
    - **Widen or narrow the randomization period for scheduled scans (Default)** (use **Scheduler Randomization Time** to set the randomization window)
    - **Scheduled tasks will not be randomized** (recommended)
- **Setting**: **Scheduler Randomization Time**
- **Values**:

    - ![](media/toggle-off.png)**Not Configured** (recommended)
    - ![](media/toggle-on.png)**Configured**
        - Enter a value between **1** and **23** hours. The default value is **4** hours.
- **Setting**: **Avg CPU Load Factor**
- **Values**:

    - ![](media/toggle-off.png)**Not Configured** (recommended)
    - ![](media/toggle-on.png)**Configured**
        - Enter a percentage from **0** to **100**. The default value is **50**.
- **Setting**: **Enable Low CPU Priority**
- **Values**:

    - **Not configured**
    - **Disabled (Default)** (recommended)
    - **Enabled**
- **Setting**: **Disable Catchup Full Scan**
- **Values**:

    - **Not configured**
    - **Disabled** (enables catch-up full scans)
    - **Enabled (Default)** (disables catch-up full scans and matches the Microsoft Defender Antivirus client default)
- **Setting**: **Disable Catchup Quick Scan**
- **Values**:

    - **Not configured**
    - **Disabled** (enables catch-up quick scans)
    - **Enabled (Default)** (disables catch-up quick scans and matches the Microsoft Defender Antivirus client default)