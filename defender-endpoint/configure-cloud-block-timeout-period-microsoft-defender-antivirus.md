---
layout: Conceptual
title: Configure Microsoft Defender Antivirus cloud block time-out - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/configure-cloud-block-timeout-period-microsoft-defender-antivirus
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: You can configure how long Microsoft Defender Antivirus blocks a file from running while waiting for a cloud determination.
ms.service: defender-endpoint
ms.localizationpriority: medium
author: chrisda
ms.author: chrisda
ms.custom: nextgen, msecd-doc-authoring-1015
ms.reviewer: yongrhee
ms.subservice: ngp
ms.topic: how-to
ms.date: 2026-09-02T00:00:00.0000000Z
ms.collection:
- m365-security
- tier2
- mde-ngp
ai-usage: ai-assisted
locale: en-us
document_id: 51283634-fdea-1986-fdd5-fb8af3a999f8
document_version_independent_id: 51283634-fdea-1986-fdd5-fb8af3a999f8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/configure-cloud-block-timeout-period-microsoft-defender-antivirus.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-cloud-block-timeout-period-microsoft-defender-antivirus
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/configure-cloud-block-timeout-period-microsoft-defender-antivirus.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/a72e95ff-4b4f-4cc1-90c6-7dcba67ff05f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/24dc3ccd-591a-4415-a1fe-8759afafcb12
platformId: d44b2076-06bd-6f4f-abe6-9af72eeaeef1
---

# Configure Microsoft Defender Antivirus cloud block time-out - Microsoft Defender for Endpoint | Microsoft Learn

When Microsoft Defender Antivirus finds a suspicious file, it can prevent the file from running while it queries the [Microsoft Defender Antivirus cloud service](cloud-protection-microsoft-defender-antivirus).

By default, [Block at first sight](configure-block-at-first-sight-microsoft-defender-antivirus) blocks the file for 10 seconds while waiting for a cloud determination. You can add up to 50 seconds, for a maximum time-out period of 60 seconds. Before you begin, review the prerequisites for this feature.

## Prerequisites

Before you specify an extended time-out period, enable [Block at first sight](configure-block-at-first-sight-microsoft-defender-antivirus), cloud protection, and automatic sample submission. Keep Microsoft Defender Antivirus up to date on the devices.

### Supported operating systems

The following operating systems support this feature:

- Windows
- Windows Server

    Note

    Windows Server supports this Microsoft Defender Antivirus setting when you configure it directly by using Microsoft Configuration Manager, Group Policy, or PowerShell. The Microsoft Intune and Microsoft Defender portal procedures in this article can manage supported Windows Server versions through [Defender for Endpoint security settings management](endpoint-security-policies-configure).

    To onboard and manage servers through Defender for Endpoint, you need an eligible server license. If your organization accesses Defender for Endpoint only through Defender for Servers, you also need at least one active Defender for Endpoint user subscription license to use security settings management. For more information, see [Server plans](onboard-server#server-plans) and [Licensing and subscriptions for security settings management](/en-us/intune/device-security/microsoft-defender/security-settings-management#licensing-and-subscriptions).

## Specify the extended time-out period using Microsoft Intune

Microsoft Intune is the recommended tool for configuring and distributing Defender for Endpoint features to devices. However, Intune is a separate product that isn't part of Defender for Endpoint, and it isn't included in all subscriptions. To use Intune, you need a subscription that includes it, or you can buy it separately as a standalone subscription or add-on. If you don't have Intune, you can use any of the other methods in this article. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).

To specify the cloud block time-out period in Microsoft Intune, use an endpoint security **Antivirus** policy. For detailed instructions, see [Create endpoint security policies](/en-us/intune/intune-service/protect/endpoint-security-policy#create-endpoint-security-policies) or [Modify existing policies](/en-us/intune/device-configuration/endpoint-security/manage-policies#modify-existing-policies) (links open new tabs in the Intune documentation).

When you create the policy, use these specific settings:

- **Policy type**: Go to **Manage** &gt; **Antivirus** on the **Endpoint security | Overview** page at [https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/~/overview](https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/%7E/overview), and then select ![](media/defender-portal-icon-create.png)**Create policy**.
- **Platform**: Select **Windows**.
- **Profile**: Select **Microsoft Defender Antivirus**.

When you create or modify the policy, use these specific settings on the **Configuration settings** tab:

- Slide the toggle for **Cloud Extended Timeout** to ![](media/toggle-on.png)**Configured**.
- In the box that appears, specify a value from 0 to 50 seconds. The value is added to the default 10-second time-out period. For example, enter `50` for a total time-out period of 60 seconds.

## Specify the extended time-out period using the Microsoft Defender portal

If your organization [manages endpoint security policies in the Microsoft Defender portal](endpoint-security-policies-configure), you specify the cloud block time-out period with the same endpoint security policies that Intune uses.

For detailed instructions, see [Create an endpoint security policy](endpoint-security-policies-configure#create-an-endpoint-security-policy) or [Edit an endpoint security policy](endpoint-security-policies-configure#edit-an-endpoint-security-policy) (links open new tabs).

When you create the policy on the **Windows policies** tab of the **Endpoint security policies** page in the Defender portal at https://security.microsoft.com/policy-inventory?osPlatform=Windows, use these specific settings:

- **Select platform**: Select **Windows**.
- **Select template**: Select **Microsoft Defender Antivirus**.

When you create or modify the policy, use these specific settings on the **Configuration settings** tab:

- Slide the toggle for **Cloud Extended Timeout** to ![](media/toggle-on.png)**Configured**.
- In the box that appears, specify a value from 0 to 50 seconds. The value is added to the default 10-second time-out period. For example, enter `50` for a total time-out period of 60 seconds.

## Specify the extended time-out period using Microsoft Configuration Manager

For instructions to create and deploy an antimalware policy, see [Endpoint Protection antimalware policies in Configuration Manager](/en-us/intune/configmgr/protect/deploy-use/endpoint-antimalware-policies).

In the **Cloud Protection Service** settings of the antimalware policy, configure **Allow extended cloud check to block and scan for up to (seconds)**. Enter a value from `0` to `50`. The value is added to the default 10-second time-out period.

## Specify the extended time-out period using Group Policy

You can use Group Policy to specify an extended time-out period for cloud checks.

1. In Centralized Group Policy, open the [Group Policy Management Console (GPMC)](/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-management-console) on your Group Policy management computer.
2. In the GPMC console tree, expand Group Policy Objects in the forest and domain containing the GPO you want to edit.
3. Right-click the GPO, and then select **Edit**.
4. In the **Group Policy Management Editor**, go to **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **MpEngine**.

    Note

    Group Policy paths before Windows 10, version 2004 (May 2020) might use *Windows* Defender Antivirus instead of *Microsoft* Defender Antivirus. Both names refer to the same policy location.
5. In the details pane of **MpEngine**, open the **Configure extended cloud check** setting. To open the setting, use any of the following methods:

    - Double-click the setting.
    - Right-click the setting, and then select **Edit**.
    - Select the setting, and then select **Action** &gt; **Edit**.
6. In the setting window that opens, select **Enabled**.
7. In the **Options** section, for **Specify the extended cloud check time in seconds**, enter the extra time that Defender Antivirus prevents the file from running while waiting for a cloud determination. Enter a value from `0` to `50`. The value is added to the default 10-second time-out period.
8. Select **OK**.

Tip

You can also configure Group Policy locally on individual devices by using the Local Group Policy Editor (`gpedit.msc`). Navigate to the same path: **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **MpEngine**.

## Specify the extended time-out period using PowerShell

In an elevated PowerShell session (a PowerShell window you opened by selecting **Run as administrator**), replace &lt;0-50&gt; with an integer from 0 to 50, and then run the following command:

```powershell
Set-MpPreference -CloudExtendedTimeout <0-50>
```

For example, the following command adds 50 seconds to the default 10-second period, for a total of 60 seconds:

```powershell
Set-MpPreference -CloudExtendedTimeout 50
```

For detailed syntax and parameter information, see [Set-MpPreference](/en-us/powershell/module/defender/set-mppreference).