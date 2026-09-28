---
layout: Conceptual
title: Configure local overrides for Microsoft Defender Antivirus settings - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/configure-local-policy-overrides-microsoft-defender-antivirus
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Configure Group Policy local overrides and local administrator merge behavior for Microsoft Defender Antivirus settings on managed Windows devices.
ms.service: defender-endpoint
ms.subservice: ngp
ms.localizationpriority: medium
author: paulinbar
ms.author: painbar
ms.topic: how-to
ms.custom: nextgen, msecd-doc-authoring-1016
ms.date: 2026-09-02T00:00:00.0000000Z
ms.reviewer: yongrhee
ms.collection:
- m365-security
- tier2
- mde-ngp
ai-usage: ai-assisted
locale: en-us
document_id: b785cf51-decf-4746-104e-b9662d7f4572
document_version_independent_id: b785cf51-decf-4746-104e-b9662d7f4572
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/configure-local-policy-overrides-microsoft-defender-antivirus.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-local-policy-overrides-microsoft-defender-antivirus
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/configure-local-policy-overrides-microsoft-defender-antivirus.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 90cb2054-90fc-1d2d-2d56-11c196741c08
---

# Configure local overrides for Microsoft Defender Antivirus settings - Microsoft Defender for Endpoint | Microsoft Learn

By default, Microsoft Defender Antivirus settings that you deploy through a Group Policy Object (GPO) prevent users from changing those settings locally. However, some users might need to change settings on their own devices. For example, security researchers and threat investigators often need more control over individual settings.

The following procedures configure local overrides and control how local and global exclusion lists are merged.

Tip

If you're looking for antivirus-related information for other platforms, see the following articles:

- [Set preferences for Microsoft Defender for Endpoint on macOS](mac-preferences)
- [Microsoft Defender for Endpoint on Mac](microsoft-defender-endpoint-mac)
- [macOS Antivirus policy settings for Microsoft Defender Antivirus for Intune](/en-us/intune/intune-service/protect/antivirus-microsoft-defender-settings-macos)
- [Set preferences for Microsoft Defender for Endpoint on Linux](linux-preferences)
- [Microsoft Defender for Endpoint on Linux](microsoft-defender-endpoint-linux)
- [Configure Defender for Endpoint on Android features](android-configure)
- [Configure Microsoft Defender for Endpoint on iOS features](ios-configure-features)

## Prerequisites

### Supported operating systems

- Windows

## Configure local overrides for Microsoft Defender Antivirus settings using Group Policy

Group Policy is the only supported method for configuring these local override policies. By default, the policies are set to **Disabled**. If you set a policy to **Enabled**, users can change the related setting on their devices by using one of the following methods:

- The [Windows Security app](microsoft-defender-security-center-antivirus).
- The Local Group Policy Editor (`gpedit.msc`).
- The [**Set-MpPreference**](/en-us/powershell/module/defender/set-mppreference) cmdlet (where supported).

To configure local override policies by using Group Policy, follow these steps:

1. Open the [Group Policy Management Console (GPMC)](/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-management-console) on your Group Policy management computer.
2. In the GPMC console tree, expand Group Policy Objects in the forest and domain containing the GPO you want to edit.
3. Right-click the GPO, and then select **Edit**.
4. In the **Group Policy Management Editor**, go to **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus**.
5. Go to the **Location** identified in the following table (for example, **MAPS**).

    | Location | Setting | Article |
    | --- | --- | --- |
    | MAPS | Configure local setting override for reporting to Microsoft MAPS | [Enable cloud-delivered protection](cloud-protection-configure) |
    | Quarantine | Configure local setting override for the removal of items from Quarantine folder | [Configure remediation for scans](configure-remediation-microsoft-defender-antivirus) |
    | Real-time protection | Configure local setting override for monitoring file and program activity on your computer | [Enable and configure Microsoft Defender Antivirus always-on protection and monitoring](configure-real-time-protection-microsoft-defender-antivirus) |
    | Real-time protection | Configure local setting override for monitoring for incoming and outgoing file activity | [Enable and configure Microsoft Defender Antivirus always-on protection and monitoring](configure-real-time-protection-microsoft-defender-antivirus) |
    | Real-time protection | Configure local setting override for scanning all downloaded files and attachments | [Enable and configure Microsoft Defender Antivirus always-on protection and monitoring](configure-real-time-protection-microsoft-defender-antivirus) |
    | Real-time protection | Configure local setting override to turn on behavior monitoring | [Enable and configure Microsoft Defender Antivirus always-on protection and monitoring](configure-real-time-protection-microsoft-defender-antivirus) |
    | Real-time protection | Configure local setting override to turn on real-time protection | [Enable and configure Microsoft Defender Antivirus always-on protection and monitoring](configure-real-time-protection-microsoft-defender-antivirus) |
    | Remediation | Configure local setting override for the time of day to run a scheduled full scan to complete remediation | [Configure remediation for scans](configure-remediation-microsoft-defender-antivirus) |
    | Scan | Configure local setting override for maximum percentage of CPU utilization | [Configure and run scans](run-scan-microsoft-defender-antivirus) |
    | Scan | Configure local setting override for the scheduled scan day | [About scheduled scans](schedule-antivirus-scans) |
    | Scan | Configure local setting override for scheduled quick scan time | [About scheduled scans](schedule-antivirus-scans) |
    | Scan | Configure local setting override for scheduled scan time | [About scheduled scans](schedule-antivirus-scans) |
    | Scan | Configure local setting override for the scan type to use for a scheduled scan | [About scheduled scans](schedule-antivirus-scans) |
6. In the details pane for the selected **Location**, find the setting listed in the **Setting** column of the table. For example, select **Configure local setting override for reporting to Microsoft MAPS**. Open the setting by using any of the following methods:

    - Double-click the setting.
    - Right-click the setting, and then select **Edit**.
    - Select the setting, and then select **Action** &gt; **Edit**.
7. In the setting window that opens, select the required configuration (for example, **Enabled** or **Disabled**), and then select **OK**.

    Repeat these steps for each setting you want to configure.
8. Deploy the GPO to the devices you want to manage.

## Configure how locally and globally defined threat remediation and exclusions lists are merged

You can also control how locally and globally defined lists are merged. The local administrator merge behavior setting applies to the following features:

- [Exclusion lists](microsoft-defender-antivirus-exclusions-configure)
- [Specified remediation lists](configure-remediation-microsoft-defender-antivirus)
- [File and folder exclusions for attack surface reduction (ASR) rules](attack-surface-reduction-rules-overview#file-and-folder-exclusions-for-asr-rules)

By default, lists configured in Local Group Policy and the Windows Security app merge with lists from your deployed GPO. If the lists conflict, the deployed GPO takes precedence. You can disable local list merging so that only lists from management policies are used.

### Use Microsoft Intune to disable local list merging

Microsoft Intune is the recommended tool for configuring and distributing Defender for Endpoint features to devices. However, Intune is a separate product that isn't part of Defender for Endpoint, and it isn't included in all subscriptions. To use Intune, you need a subscription that includes it, or you can buy it separately as a standalone subscription or add-on. If you don't have Intune, you can use any of the other methods in this article. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).

To disable local list merging in Microsoft Intune, use an endpoint security **Antivirus** policy. For detailed instructions, see [Create endpoint security policies](/en-us/intune/intune-service/protect/endpoint-security-policy#create-endpoint-security-policies) or [Modify existing policies](/en-us/intune/device-configuration/endpoint-security/manage-policies#modify-existing-policies) (links open new tabs in the Intune documentation).

When you create the policy, use these specific settings:

- **Policy type**: Go to **Manage** &gt; **Antivirus** on the **Endpoint security | Overview** page at [https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/~/overview](https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/%7E/overview), and then select ![](media/defender-portal-icon-create.png)**Create policy**.
- **Platform**: Select **Windows**.
- **Profile**: Select **Microsoft Defender Antivirus**.

When you create or modify the policy, use these specific settings on the **Configuration settings** tab:

- **Disable local admin merge**: Select **Disable local admin merge**.

For more information about antivirus policy profiles available in Microsoft Intune, see [Antivirus policy for endpoint security in Intune](/en-us/intune/device-configuration/endpoint-security/antivirus).

### Use the Microsoft Defender portal to disable local list merging

If your organization [manages endpoint security policies in the Microsoft Defender portal](endpoint-security-policies-configure), use a Microsoft Defender Antivirus policy to disable local list merging.

For detailed instructions, see [Create an endpoint security policy](endpoint-security-policies-configure#create-an-endpoint-security-policy) or [Edit an endpoint security policy](endpoint-security-policies-configure#edit-an-endpoint-security-policy) (links open new tabs).

When you create the policy on the **Windows policies** tab of the **Endpoint security policies** page in the Defender portal at https://security.microsoft.com/policy-inventory?osPlatform=Windows, use these specific settings:

- **Select platform**: Select **Windows**.
- **Select template**: Select **Microsoft Defender Antivirus**.

When you create or modify the policy, use this specific setting on the **Configuration settings** tab:

- **Disable local admin merge**: Select **Disable local admin merge**.

### Use Group Policy to disable local list merging

To disable local list merging by using Group Policy, follow these steps:

1. Open the [Group Policy Management Console (GPMC)](/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-management-console) on your Group Policy management computer.
2. In the GPMC console tree, expand Group Policy Objects in the forest and domain containing the GPO you want to edit.
3. Right-click the GPO, and then select **Edit**.
4. In the **Group Policy Management Editor**, go to **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus**.
5. In the details pane of **Microsoft Defender Antivirus**, open the **Configure local administrator merge behavior for lists** setting by using any of the following methods:

    - Double-click the setting.
    - Right-click the setting, and then select **Edit**.
    - Select the setting, and then select **Action** &gt; **Edit**.
6. In the setting window that opens, select **Disabled**, and then select **OK**.

Note

In the following administrative templates, set **Configure local administrator merge behavior for lists** to **Enabled** to disable the local administrator merge behavior:

- Administrative Templates (.admx) for Windows 11 2022 Update (22H2)
- Administrative Templates (.admx) for Windows 10 November 2021 Update (21H2)

Note

Disabling local list merging overrides controlled folder access settings. It also overrides any protected folders or allowed apps set by the local administrator. For more information about controlled folder access settings, see [Allow a blocked app in Windows Security](https://support.microsoft.com/Windows/Security/Threat-Malware-Protection/virus-and-threat-protection-in-the-windows-security-app).