---
layout: Conceptual
title: Deploy, manage, and report on Microsoft Defender Antivirus - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/deploy-manage-report-microsoft-defender-antivirus
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: You can deploy and manage Microsoft Defender Antivirus with Intune, Microsoft Configuration Manager, Group Policy, PowerShell, or WMI.
ms.service: defender-endpoint
ms.localizationpriority: medium
ms.date: 2026-09-15T00:00:00.0000000Z
ms.topic: install-set-up-deploy
author: chrisda
ms.author: chrisda
ms.custom: nextgen
ms.reviewer: pahuijbr
ms.subservice: ngp
ms.collection:
- m365-security
- tier2
- mde-ngp
locale: en-us
document_id: 61d0aa71-feb4-207a-ff15-9e62dd27e17a
document_version_independent_id: 61d0aa71-feb4-207a-ff15-9e62dd27e17a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/deploy-manage-report-microsoft-defender-antivirus.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: deploy-manage-report-microsoft-defender-antivirus
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/deploy-manage-report-microsoft-defender-antivirus.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 7c4ec7db-3c55-4f84-c0ac-85871aff0fcb
---

# Deploy, manage, and report on Microsoft Defender Antivirus - Microsoft Defender for Endpoint | Microsoft Learn

You can manage and report on Microsoft Defender Antivirus using one of several tools, such as:

- Deploy, manage, and report on Microsoft Defender Antivirus
    - Microsoft Intune
    - Configuration Manager
    - PowerShell
    - Group Policy and Microsoft Entra ID
    - Windows Management Instrumentation

This article describes these options for deployment, management, and reporting.

## Prerequisites

### Supported operating systems

Microsoft Defender Antivirus is installed as a core part of Windows 10 and 11, and is included in Windows Server 2016 and later.

Note

Windows Server 2012 requires Microsoft Defender for Endpoint.

## Microsoft Intune

Microsoft Intune is the recommended tool for configuring and distributing Defender for Endpoint features to devices. However, Intune is a separate product that isn't part of Defender for Endpoint, and it isn't included in all subscriptions. To use Intune, you need a subscription that includes it, or you can buy it separately as a standalone subscription or add-on. If you don't have Intune, you can use any of the other methods in this article. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).

With Intune, you can manage device security through policies, such as a policy to configure Microsoft Defender Antivirus and other security capabilities in Defender for Endpoint. To learn more, see [Use policies to manage device security](/en-us/intune/intune-service/protect/endpoint-security#use-policies-to-manage-device-security).

For reporting, you can choose from several options:

- [Use the Microsoft Defender portal](/en-us/defender-xdr/microsoft-365-defender-portal), which includes a [device inventory list](machines-view-overview). To access the device inventory, in the Microsoft Defender portal (https://security.microsoft.com/), go to **Assets** &gt; **Devices**. The device inventory list displays onboarded devices along with their health state and risk level.
- [Manage devices with Intune](/en-us/intune/intune-service/remote-actions/device-management), which includes the ability to view detailed information about devices and take action. [Available actions](/en-us/intune/intune-service/remote-actions/device-management#available-device-actions) include starting an antivirus scan, restarting a device, locating a device, wiping a device, and more.

## Configuration Manager

With Configuration Manager, you can manage security and malware on Configuration Manager client computers. Use the [Endpoint Protection point site system role](/en-us/intune/configmgr/protect/deploy-use/endpoint-protection-site-role) and [enable Endpoint Protection with custom client settings](/en-us/intune/configmgr/protect/deploy-use/endpoint-protection-configure-client). You can use [default and customized antimalware policies](/en-us/defender-office-365/anti-malware-policies-configure).

For reporting, you can choose from several options:

- [Use the Microsoft Defender portal](/en-us/defender-xdr/microsoft-365-defender-portal), which includes a [device inventory list](machines-view-overview). To access the device inventory, in the Microsoft Defender portal (https://security.microsoft.com/), go to **Assets** &gt; **Devices**. The device inventory list displays onboarded devices along with their health state and risk level.
- [Use Intune to view device details](/en-us/intune/intune-service/remote-actions/device-inventory).
- Use the default [Configuration Manager Monitoring workspace](/en-us/intune/configmgr/apps/deploy-use/monitor-applications-from-the-console).
- [Create email alerts](/en-us/intune/configmgr/protect/deploy-use/endpoint-configure-alerts).
- If your organization has Defender for Endpoint, you can also use the [Microsoft Defender portal](/en-us/defender-xdr/microsoft-365-defender-portal), which includes a [device inventory list](machines-view-overview). To access the device inventory, in the Microsoft Defender portal (https://security.microsoft.com/), go to **Assets** &gt; **Devices**. The device inventory list displays onboarded devices along with their health state and risk level.

## PowerShell

You can use PowerShell with Group Policy or Configuration Manager to manage Microsoft Defender Antivirus on client devices. You can also use PowerShell to manage Microsoft Defender Antivirus manually on individual devices that aren't managed by a security team.

- Use the appropriate [Get- cmdlets available in the Defender module](/en-us/powershell/module/defender).
- Use the [Set-MpPreference](/en-us/powershell/module/defender/set-mppreference) and [Update-MpSignature](/en-us/powershell/module/defender/update-mpsignature) cmdlets that are available in the Defender module.

For reporting, you can choose from the following options:

- [Use the Microsoft Defender portal](/en-us/defender-xdr/microsoft-365-defender-portal), which includes a [device inventory list](machines-view-overview). To access the device inventory, in the Microsoft Defender portal (https://security.microsoft.com/), go to **Assets** &gt; **Devices**. The device inventory list displays onboarded devices along with their health state and risk level.
- [Use Intune to view device details](/en-us/intune/intune-service/remote-actions/device-inventory).
- Use the default [Configuration Manager Monitoring workspace](/en-us/intune/configmgr/apps/deploy-use/monitor-applications-from-the-console).

## Group Policy and Microsoft Entra ID

You can use a Group Policy Object to deploy configuration changes and ensure Microsoft Defender Antivirus is enabled. Use Group Policy Objects (GPOs) to [configure update options for Microsoft Defender Antivirus](manage-protection-update-schedule-microsoft-defender-antivirus) and [configure Windows Defender features](configure-microsoft-defender-antivirus-features).

For reporting, keep in mind that device reporting isn't available with Group Policy.

- You can generate a list of Group Policies to determine if any settings or policies aren't applied.
- If your organization has Defender for Endpoint, you can also use the [Microsoft Defender portal](/en-us/defender-xdr/microsoft-365-defender-portal), which includes a [device inventory list](machines-view-overview). To access the device inventory, in the Microsoft Defender portal (https://security.microsoft.com/), go to **Assets** &gt; **Devices**. The device inventory list displays onboarded devices along with their health state and risk level.

## Windows Management Instrumentation

With Windows Management Instrumentation (WMI), you can manage Microsoft Defender Antivirus with Group Policy or Configuration Manager. You can also use WMI to manage Microsoft Defender Antivirus manually on individual devices that aren't managed by a security team.

- Use the [Set method of the MSFT_MpPreference class](/en-us/previous-versions/windows/desktop/defender/set-msft-mppreference) and the [Update method of the MSFT_MpSignature class](/en-us/previous-versions/windows/desktop/defender/update-msft-mpsignature).
- Use the [MSFT_MpComputerStatus](/en-us/previous-versions/windows/desktop/defender/msft-mpcomputerstatus) class and the get method of associated classes in the [Windows Defender WMIv2 Provider](/en-us/windows/win32/wmisdk/wmi-providers).

For reporting, Windows events comprise several security event sources, including Security Account Manager (SAM) events ([enhanced for Windows 10](/en-us/windows/whats-new/whats-new-windows-10-version-1507-and-1511)). Also see [Security auditing](/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/auditing/security-auditing-overview) and [Windows Defender events](troubleshoot-microsoft-defender-antivirus).