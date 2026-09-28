---
layout: Conceptual
title: Configure tamper protection for Microsoft Defender Antivirus on Windows - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/tamper-protection-windows-configure
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
ms.reviewer: joshbregman, mattcall, pahuijbr, hayhov, oogunrinde
description: Learn how to configure tamper protection on Windows devices by using the Defender portal, Intune, Configuration Manager, or Windows Security.
ms.service: defender-endpoint
ms.localizationpriority: medium
ms.date: 2026-09-08T00:00:00.0000000Z
ms.topic: how-to
author: limwainstein
ms.author: lwainstein
ms.custom:
- msecd-doc-authoring-1016
- nextgen
- admindeeplinkDEFENDER
ms.subservice: ngp
ms.collection:
- m365-security
- tier2
- mde-ngp
ai-usage: ai-assisted
locale: en-us
document_id: 1f1a93a0-3368-a00f-73d1-8609cf35152d
document_version_independent_id: 1f1a93a0-3368-a00f-73d1-8609cf35152d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/tamper-protection-windows-configure.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: tamper-protection-windows-configure
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/tamper-protection-windows-configure.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/691e3042-55ad-4ce1-b5e9-649b1cc47b5c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b7d11190-096c-4ddb-87db-63764f603aac
platformId: 1c43ac25-a1d8-fa66-c038-9842205a44e6
---

# Configure tamper protection for Microsoft Defender Antivirus on Windows - Microsoft Defender for Endpoint | Microsoft Learn

[Tamper protection](tamper-protection-overview) helps prevent certain security settings, such as virus and threat protection, from being disabled or changed. Use the methods described in this article to configure tamper protection for Microsoft Defender Antivirus on Windows devices.

To configure tamper protection for Microsoft Defender for Endpoint on macOS, see [Configure tamper protection for Microsoft Defender for Endpoint on macOS](tamper-protection-macos-configure).

To protect organization-managed Microsoft Defender Antivirus exclusion lists from unauthorized changes, see [Protect Microsoft Defender Antivirus exclusions with tamper protection](tamper-protection-antivirus-exclusions).

For answers to common questions, see [Frequently asked questions about tamper protection](tamper-protection-faq). For help with blocked settings and exclusion protection, see [Troubleshoot problems with tamper protection](tamper-protection-troubleshoot).

Important

When tamper protection is turned on, [tamper-protected settings](tamper-protection-overview#what-happens-when-tamper-protection-is-turned-on) can't be changed. Changes to these settings might appear to succeed, but tamper protection blocks the changes. Use [troubleshooting mode](troubleshooting-mode-enable) to temporarily disable tamper protection when you need to change a protected setting.

A policy that manages tamper protection takes precedence over the organization-wide setting in the Microsoft Defender portal. A policy or portal setting also takes precedence over a setting that a local administrator configures in the Windows Security app.

## Prerequisites

For operating system, product version, licensing, permissions, and device-management requirements, see [Requirements for tamper protection](tamper-protection-overview#requirements-for-tamper-protection).

## Configure tamper protection in Microsoft Intune

Microsoft Intune is the recommended tool for configuring and distributing Defender for Endpoint features to devices. However, Intune is a separate product that isn't part of Defender for Endpoint, and it isn't included in all subscriptions. To use Intune, you need a subscription that includes it, or you can buy it separately as a standalone subscription or add-on. If you don't have Intune, you can use any of the other methods in this article. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).

To configure tamper protection in Intune, use an endpoint security **Antivirus** policy. For detailed instructions, see [Create endpoint security policies](/en-us/intune/intune-service/protect/endpoint-security-policy#create-endpoint-security-policies) or [Modify existing policies](/en-us/intune/device-configuration/endpoint-security/manage-policies#modify-existing-policies) (links open new tabs in the Intune documentation).

Assign the policy to your entire organization or to selected user or device groups. You can also exclude specific groups from the policy assignment.

When you create the policy, use these specific settings:

- **Policy type**: Go to **Manage** &gt; **Antivirus** on the **Endpoint security | Overview** page at [https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/~/overview](https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/%7E/overview), and then select ![](media/defender-portal-icon-create.png)**Create policy**.
- **Platform**: Select **Windows**.
- **Profile**: Select **Windows Security Experience**.

When you create or modify the policy, use these specific settings on the **Configuration settings** tab:

- **Tamper protection (device)** in the **Defender** section: Select **On**.

## Configure tamper protection in the Microsoft Defender portal

Note

Tamper protection is on by default for new deployments as part of [built-in protection](built-in-protection).

If tamper protection is deployed and managed through Intune, the Intune policy takes precedence. Changing the setting in the Defender portal doesn't change the policy-managed state. Instead, the Defender portal setting restricts tamper-protected settings to their secure default values.

On the **Advanced features** page in the Microsoft Defender portal at https://security.microsoft.com/preferences2/endpoints, slide the **Tamper protection** toggle to ![](media/toggle-on.png)**On** or ![](media/toggle-off.png)**Off**.

[![Screenshot of tamper protection turned on in the Microsoft Defender portal.](/en-us/defender/media/mde-turn-tamperprotectionon.png)](/en-us/defender/media/mde-turn-tamperprotectionon.png#lightbox)

## Configure tamper protection using Microsoft Configuration Manager

Note

Configuration Manager doesn't support configuring tamper protection directly. Use [tenant attach](/en-us/intune/configmgr/tenant-attach/endpoint-security-get-started) to deploy the setting from the Intune admin center. Tenant attach synchronizes on-premises Configuration Manager devices with the Microsoft Intune admin center so you can deploy endpoint security policies to device collections.

To configure tamper protection for tenant-attached devices, use an endpoint security **Antivirus** policy. For detailed instructions, see [Create endpoint security policies](/en-us/intune/intune-service/protect/endpoint-security-policy#create-endpoint-security-policies) or [Modify existing policies](/en-us/intune/device-configuration/endpoint-security/manage-policies#modify-existing-policies) (links open new tabs in the Intune documentation).

When you create the policy, use these specific settings:

- **Policy type**: Go to **Manage** &gt; **Antivirus** on the **Endpoint security | Overview** page at [https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/~/overview](https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/%7E/overview), and then select ![](media/defender-portal-icon-create.png)**Create policy**.
- **Platform**: Select **Windows (ConfigMgr)**.
- **Profile**: Select **Windows Security experience (ConfigMgr)**.

When you create or modify the policy, use these specific settings on the **Configuration settings** tab:

- **Enable tamper protection to prevent Microsoft Defender from being disabled** in the **Windows Security** section: Select **Enabled**.

![Screenshot of Windows Security settings with tamper protection enabled.](media/tamper-protect-configmgr.png)

## Configure tamper protection using the Windows Security app

You can use the [Windows Security app](https://support.microsoft.com/Windows/Security/Windows-Security/stay-protected-with-the-windows-security-app) to configure tamper protection on an individual device.

Use the following steps to turn tamper protection on or off:

1. In the **Windows Security** app on the device, go to **Virus & threat protection**.
2. In the **Virus & threat protection** pane, in the **Virus & threat protection settings** section, select **Manage settings**.
3. In the **Virus & threat protection settings** pane, slide the **Tamper Protection** toggle to ![](media/toggle-on.png)**On** or ![](media/toggle-off.png)**Off**.

    [![Screenshot of tamper protection turned on in the Windows Security app.](media/tamperprotectionturnedon.png)](media/tamperprotectionturnedon.png#lightbox)

## Configure tamper protection using PowerShell

You can't use PowerShell to configure tamper protection during normal operation.

### Temporarily disable tamper protection using PowerShell

The PowerShell command to temporarily disable tamper protection works only while the device is in [Defender for Endpoint troubleshooting mode](troubleshooting-mode-enable).

For instructions, see [Temporarily disable tamper protection using PowerShell](troubleshooting-mode-enable#temporarily-disable-tamper-protection-using-powershell).

### Determine the status of tamper protection and real-time protection using PowerShell

To determine the current status of tamper protection and real-time protection on a device, run the following command:

```powershell
Get-MpComputerStatus | Select-Object IsTamperProtected, RealTimeProtectionEnabled
```

The value `True` means the setting is enabled. The value `False` means the setting is disabled.