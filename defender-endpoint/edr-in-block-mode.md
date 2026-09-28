---
layout: Conceptual
title: Endpoint detection and response in block mode - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/edr-in-block-mode
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn about endpoint detection and response in block mode.
author: limwainstein
ms.author: lwainstein
ms.reviewer: pahuijbr, kausd
ms.topic: article
ms.service: defender-endpoint
ms.subservice: edr
ms.localizationpriority: medium
ms.custom:
- msecd-doc-authoring-1015
- next-gen
- mde-edr
- admindeeplinkDEFENDER
- sfi-ga-nochange
ms.date: 2026-09-15T00:00:00.0000000Z
ai-usage: ai-assisted
ms.collection:
- m365-security
- tier2
- mde-edr
locale: en-us
document_id: 4db0e76a-4562-6523-4c34-dc837ec70c30
document_version_independent_id: 4db0e76a-4562-6523-4c34-dc837ec70c30
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/edr-in-block-mode.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: edr-in-block-mode
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/edr-in-block-mode.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: c744f947-b4ba-b924-f626-8a0e1b84d0db
---

# Endpoint detection and response in block mode - Microsoft Defender for Endpoint | Microsoft Learn

This article describes EDR in block mode, which helps protect devices that are running a non-Microsoft antivirus solution (with Microsoft Defender Antivirus in passive mode).

## Prerequisites

### Supported operating systems

- Windows

## What is EDR in block mode?

[Endpoint detection and response](overview-endpoint-detection-response) (EDR) in block mode provides added protection from malicious artifacts when Microsoft Defender Antivirus is not the primary antivirus product and is running in passive mode. EDR in block mode is available in Defender for Endpoint Plan 2.

Important

EDR in block mode cannot provide all available protection when Microsoft Defender Antivirus real-time protection is in passive mode. Some capabilities that depend on Microsoft Defender Antivirus to be the active antivirus solution will not work, such as the following examples:

- Real-time protection, including on-access scanning, is not available when Microsoft Defender Antivirus is in passive mode. To learn more about real-time protection policy settings, see **[Enable and configure Microsoft Defender Antivirus always-on protection](configure-real-time-protection-microsoft-defender-antivirus)**.
- Features like **[network protection](network-protection)** and **[attack surface reduction (ASR) rules](attack-surface-reduction-rules-overview)** and indicators (file hash, ip address, URL, and certificates) are only available when Microsoft Defender Antivirus is running in Active mode. It is expected that your non-Microsoft antivirus solution includes these capabilities.

EDR in block mode works behind the scenes to remediate malicious artifacts that were detected by EDR capabilities. Such artifacts might have been missed by the primary, non-Microsoft antivirus product. EDR in block mode allows Microsoft Defender Antivirus to take actions on post-breach, behavioral EDR detections.

EDR in block mode is integrated with [threat & vulnerability management](/en-us/defender-vulnerability-management/defender-vulnerability-management) capabilities. Your organization's security team gets a [security recommendation](api/ti-indicator) to turn EDR in block mode on if it isn't already enabled.

[![The recommendation to turn on EDR in block mode](media/edrblockmode-tvmrecommendation.png)](media/edrblockmode-tvmrecommendation.png#lightbox)

Tip

To get the best protection, make sure to **[deploy Microsoft Defender for Endpoint baselines](configure-machines-security-baseline)**.

Watch this video to learn why and how to turn on endpoint detection and response (EDR) in block mode, enable behavioral blocking, and containment at every stage from pre-breach to post-breach.

## What happens when something is detected?

When EDR in block mode is turned on, and a malicious artifact is detected, Defender for Endpoint remediates that artifact. Your security operations team sees the detection status as **Blocked** or **Prevented** in the [Action center](respond-machine-alerts#check-activity-details-and-status), listed as completed actions. The following image shows an instance of unwanted software that was detected and remediated through EDR in block mode:

[![The detection by EDR in block mode](media/edr-in-block-mode-detection.png)](media/edr-in-block-mode-detection.png#lightbox)

## Enable EDR in block mode

Important

- Make sure the requirements are met before turning on EDR in block mode.
- Defender for Endpoint Plan 2 licenses are required.
- Beginning with [platform version 4.18.2202.X](microsoft-defender-antivirus-updates), you can set EDR in block mode to target specific device groups using Intune CSPs. You can continue to set EDR in block mode tenant-wide in the [Microsoft Defender portal](https://security.microsoft.com).
- EDR in block mode is primarily recommended for devices that are running Microsoft Defender Antivirus in passive mode (a non-Microsoft antivirus solution is installed and active on the device).

### Microsoft Defender portal

1. Go to the Microsoft Defender portal (https://security.microsoft.com/) and sign in.
2. Choose **Settings** &gt; **Endpoints** &gt; **General** &gt; **Advanced features**.
3. Scroll down, and then turn on **Enable EDR in block mode**.

### Intune

Microsoft Intune is the recommended tool for configuring and distributing Defender for Endpoint features to devices. However, Intune is a separate product that isn't part of Defender for Endpoint, and it isn't included in all subscriptions. To use Intune, you need a subscription that includes it, or you can buy it separately as a standalone subscription or add-on. If you don't have Intune, you can use any of the other methods in this article. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).

To create a custom policy in Intune, see [Deploy OMA-URIs to target a CSP through Intune, and a comparison to on-premises](/en-us/troubleshoot/mem/intune/device-configuration/deploy-oma-uris-to-target-csp-via-intune).

For more information on the Defender CSP used for EDR in block mode, see "Configuration/PassiveRemediation" under [Defender CSP](/en-us/windows/client-management/mdm/defender-csp).

### Group Policy

You can use Group Policy to enable EDR in block mode.

1. In Centralized Group Policy, open the [Group Policy Management Console (GPMC)](/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-management-console) on your Group Policy management computer.
2. In the GPMC console tree, expand Group Policy Objects in the forest and domain containing the GPO you want to edit.
3. Right-click the GPO, and then select **Edit**.
4. In the **Group Policy Management Editor**, go to **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **Features**.
5. In the details pane of **Features**, open the **Enable EDR in block mode** setting. To open the setting, use any of the following methods:

    - Double-click the setting.
    - Right-click the setting, and then select **Edit**.
    - Select the setting, and then select **Action** &gt; **Edit**.
6. In the setting window that opens, select **Enabled**, and then select **OK**.

Tip

You can also configure Group Policy locally on individual devices by using the Local Group Policy Editor (`gpedit.msc`). Navigate to the same path: **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **Features**.

## Requirements for EDR in block mode

The following table lists requirements for EDR in block mode:

| Requirement | Details |
| --- | --- |
| Permissions | You must have either the Global Administrator or Security Administrator role assigned in [Microsoft Entra ID](/en-us/azure/active-directory/fundamentals/active-directory-users-assign-role-azure-portal). For more information, see [Basic permissions](basic-permissions). |
| Operating system | Devices must be running one of the following versions of Windows: - Windows 11- Windows 10 (all releases)- Windows Server 2019 or later- Windows Server, version 1803 or later- Windows Server 2016 and Windows Server 2012 R2 (with the [new unified client solution](onboard-server#functionality-in-the-modern-unified-solution-for-windows-server-2016-and-windows-server-2012-r2)) |
| Microsoft Defender for Endpoint Plan 2 | Devices must be onboarded to Defender for Endpoint. See the following articles: - [Minimum requirements for Microsoft Defender for Endpoint](minimum-requirements)- [Onboard devices and configure Microsoft Defender for Endpoint capabilities](onboard-configure)- [Onboard Windows servers to the Defender for Endpoint service](onboard-server)- [New Windows Server 2012 R2 and 2016 functionality in the modern unified solution](onboard-server#functionality-in-the-modern-unified-solution-for-windows-server-2016-and-windows-server-2012-r2)(See [Is EDR in block mode supported on Windows Server 2016 and Windows Server 2012 R2?](edr-block-mode-faqs)) |
| Microsoft Defender Antivirus | Devices must have Microsoft Defender Antivirus installed and running in either active mode or passive mode. [Confirm Microsoft Defender Antivirus is in active or passive mode](edr-block-mode-faqs). |
| Cloud-delivered protection | Microsoft Defender Antivirus must be configured such that [cloud-delivered protection is enabled](cloud-protection-configure). |
| Microsoft Defender Antivirus platform | Devices must be up to date. To confirm, using PowerShell, run the [Get-MpComputerStatus](/en-us/powershell/module/defender/get-mpcomputerstatus) cmdlet as an administrator. In the **AMProductVersion** line, you should see **4.18.2001.10** or above.  To learn more, see [Manage Microsoft Defender Antivirus updates and apply baselines](microsoft-defender-antivirus-updates). |
| Microsoft Defender Antivirus engine | Devices must be up to date. To confirm, using PowerShell, run the [Get-MpComputerStatus](/en-us/powershell/module/defender/get-mpcomputerstatus) cmdlet as an administrator. In the **AMEngineVersion** line, you should see **1.1.16700.2** or above.  To learn more, see [Manage Microsoft Defender Antivirus updates and apply baselines](microsoft-defender-antivirus-updates). |

Important

To get the best protection value, make sure your antivirus solution is configured to receive regular updates and essential features, and that your [exclusions are configured](microsoft-defender-antivirus-exclusions-configure). EDR in block mode respects exclusions that are defined for Microsoft Defender Antivirus, but not [indicators](indicators-overview) that are defined for Microsoft Defender for Endpoint.

Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.