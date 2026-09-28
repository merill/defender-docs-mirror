---
layout: Conceptual
title: Apply Microsoft Defender Antivirus updates after certain events - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/manage-event-based-updates-microsoft-defender-antivirus
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Manage how Microsoft Defender Antivirus applies security intelligence updates after startup or receiving cloud-delivered detection reports.
ms.service: defender-endpoint
ms.localizationpriority: medium
ms.topic: how-to
author: chrisda
ms.author: chrisda
ms.custom: nextgen, msecd-doc-authoring-1016
ms.date: 2026-09-16T00:00:00.0000000Z
ms.reviewer: pahuijbr
ms.subservice: ngp
ms.collection:
- m365-security
- tier2
- mde-ngp
ai-usage: ai-assisted
locale: en-us
document_id: 8121fdde-834e-bd76-fe58-c57708b8b85a
document_version_independent_id: 8121fdde-834e-bd76-fe58-c57708b8b85a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/manage-event-based-updates-microsoft-defender-antivirus.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: manage-event-based-updates-microsoft-defender-antivirus
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/manage-event-based-updates-microsoft-defender-antivirus.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 9de2acd6-737b-1333-37ba-67ac522a5767
---

# Apply Microsoft Defender Antivirus updates after certain events - Microsoft Defender for Endpoint | Microsoft Learn

Microsoft Defender Antivirus lets you control whether updates occur after certain events. For example, you can trigger updates at startup or after receiving reports from the cloud protection service. This article shows how to configure event-based protection updates by using Group Policy, PowerShell, WMI, Microsoft Intune, and Microsoft Configuration Manager.

> 
> Microsoft Intune is the recommended tool for configuring and distributing Defender for Endpoint features to devices. However, Intune is a separate product that isn't part of Defender for Endpoint, and it isn't included in all subscriptions. To use Intune, you need a subscription that includes it, or you can buy it separately as a standalone subscription or add-on. If you don't have Intune, you can use any of the other methods in this article. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).

## Prerequisites

Before you configure event-based forced updates, make sure your environment meets the following requirements.

### Supported operating systems

The following operating systems are supported:

- Windows

## Check for protection updates before running a scan

You can use Microsoft Defender for Endpoint Security Settings Management, Microsoft Intune, Microsoft Configuration Manager, Group Policy, PowerShell cmdlets, and WMI to force Microsoft Defender Antivirus to check and download protection updates before running a scheduled scan.

### Use Defender for Endpoint security settings management to check for protection updates before running a scan

For detailed instructions, see [Create an endpoint security policy](endpoint-security-policies-configure#create-an-endpoint-security-policy) or [Edit an endpoint security policy](endpoint-security-policies-configure#edit-an-endpoint-security-policy) (links open new tabs).

When you create the policy on the **Windows policies** tab of the **Endpoint security policies** page in the Defender portal at https://security.microsoft.com/policy-inventory?osPlatform=Windows, use these specific settings:

- **Select platform**: Select **Windows**.
- **Select template**: Select **Microsoft Defender Antivirus**.

When you create or modify the policy, use the same setting described in Use Microsoft Intune to check for protection updates before running a scan on the **Configuration settings** tab.

When you assign the policy, assignment group limitations apply to devices managed through Defender for Endpoint security settings management. For details, see the [Assignments step](endpoint-security-policies-configure#create-an-endpoint-security-policy).

### Use Microsoft Intune to check for protection updates before running a scan

To configure protection update checks before scans in Microsoft Intune, perform the following steps:

1. In the [Microsoft Intune admin center](https://intune.microsoft.com/), go to **Endpoints** &gt; **Configuration management** &gt; **Endpoint security policies**, and then select **Create new policy**.

    - In the **Platform** list, select **Windows 10, Windows 11, and Windows Server**.
    - In the **Select Templates** list, select **Microsoft Defender Antivirus**.
2. Fill in the name and description, and then select **Next**.
3. Go to the **Scheduled scans** section, and set **Check For Signatures Before Running Scan** to **Enabled**.
4. Save and deploy the policy.

### Use Configuration Manager to check for protection updates before running a scan

To configure protection update checks before scans in Configuration Manager, perform the following steps:

1. On your Microsoft Configuration Manager console, open the antimalware policy you want to change (select **Assets and Compliance** in the navigation pane, then expand the tree to **Overview** &gt; **Endpoint Protection** &gt; **Antimalware Policies**).
2. Go to the **Scheduled scans** section and set **Check for the latest security intelligence updates before running a scan** to **Yes**.
3. Select **OK**.
4. [Deploy the updated policy as usual](/en-us/sccm/protect/deploy-use/endpoint-antimalware-policies#deploy-an-antimalware-policy-to-client-computers).

### Use Group Policy to check for protection updates before running a scan

To configure protection update checks before scans in Group Policy, perform the following steps:

1. On your Group Policy management machine, open the [Group Policy Management Console](/en-us/previous-versions/windows/desktop/gpmc/group-policy-management-console-portal).
2. Right-click the Group Policy Object you want to configure, and then select **Edit**.
3. Using the **Group Policy Management Editor** go to **Computer configuration**.
4. Select **Policies** then **Administrative templates**.
5. Expand the tree to **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **Scan**.
6. Double-click **Check for the latest virus and spyware definitions before running a scheduled scan** and set the option to **Enabled**.
7. Select **OK**.

### Use PowerShell cmdlets to check for protection updates before running a scan

To require Microsoft Defender Antivirus to check for updated signatures before starting a scheduled scan, run the following cmdlet:

```PowerShell
Set-MpPreference -CheckForSignaturesBeforeRunningScan
```

For more information, see [Use PowerShell cmdlets to configure and run Microsoft Defender Antivirus](use-powershell-cmdlets-microsoft-defender-antivirus) and [Defender Antivirus cmdlets](/en-us/powershell/module/defender/index).

### Use Windows Management Instrumentation (WMI) to check for protection updates before running a scan

To configure Microsoft Defender Antivirus to check for updated signatures before running a scan, use the [**Set** method of the **MSFT\_MpPreference**](/en-us/previous-versions/windows/desktop/legacy/dn455323%28v=vs.85%29) class with the following property:

```WMI
CheckForSignaturesBeforeRunningScan
```

For more information, see [Windows Defender WMIv2 APIs](/en-us/previous-versions/windows/desktop/defender/windows-defender-wmiv2-apis-portal).

## Check for protection updates on startup

You can use Group Policy to force Microsoft Defender Antivirus to check and download protection updates when the machine is started.

1. On your Group Policy management computer, open the [Group Policy Management Console](/en-us/previous-versions/windows/desktop/gpmc/group-policy-management-console-portal), right-click the Group Policy Object you want to configure and select **Edit**.
2. Using the **Group Policy Management Editor** go to **Computer configuration**.
3. Select **Policies** then **Administrative templates**.
4. Expand the tree to **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **Security Intelligence Updates**.
5. Double-click **Check for the latest virus and spyware definitions on startup** and set the option to **Enabled**.
6. Select **OK**.

You can also use Group Policy, PowerShell, or WMI to configure Microsoft Defender Antivirus to check for updates at startup even when it isn't running.

### Use Group Policy to download updates when Microsoft Defender Antivirus is not present

To configure Group Policy to download updates when Microsoft Defender Antivirus is not present, perform the following steps:

1. On your Group Policy management machine, open the [Group Policy Management Console](/en-us/previous-versions/windows/desktop/gpmc/group-policy-management-console-portal), right-click the Group Policy Object you want to configure and select **Edit**.
2. Using the **Group Policy Management Editor**, go to **Computer configuration**.
3. Select **Policies** then **Administrative templates**.
4. Expand the tree to **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **Security Intelligence Updates**.
5. Double-click **Initiate security intelligence update on startup** and set the option to **Enabled**.
6. Select **OK**.

### Use PowerShell cmdlets to download updates when Microsoft Defender Antivirus is not present

To control whether Microsoft Defender Antivirus downloads signature updates at startup when the antimalware engine isn't running, run the following cmdlet:

```PowerShell
Set-MpPreference -SignatureDisableUpdateOnStartupWithoutEngine
```

For more information, see [Use PowerShell cmdlets to manage Microsoft Defender Antivirus](use-powershell-cmdlets-microsoft-defender-antivirus) and [Defender Antivirus cmdlets](/en-us/powershell/module/defender/index) for more information on how to use PowerShell with Microsoft Defender Antivirus.

### Use Windows Management Instrumentation (WMI) to download updates when Microsoft Defender Antivirus is not present

To configure whether signature updates occur at startup when the antimalware engine isn't running, use the [**Set** method of the **MSFT\_MpPreference**](/en-us/previous-versions/windows/desktop/legacy/dn455323%28v=vs.85%29) class with the following property:

```WMI
SignatureDisableUpdateOnStartupWithoutEngine
```

For more information, see [Windows Defender WMIv2 APIs](/en-us/previous-versions/windows/desktop/defender/windows-defender-wmiv2-apis-portal).

## Allow ad hoc changes to protection based on cloud-delivered protection

Microsoft Defender Antivirus can update its protection based on cloud-delivered protection. These updates can happen outside of normal or scheduled updates.

When cloud-delivered protection is turned on, Microsoft Defender Antivirus sends suspicious files to the cloud for analysis. If the cloud reports that a file is malicious, you can use Group Policy to get that protection update right away. Microsoft Defender Antivirus can also automatically apply other critical protection updates identified by the cloud service.

### Use Group Policy to automatically download recent updates based on cloud-delivered protection

To configure Group Policy to automatically download recent updates based on cloud-delivered protection, perform the following steps:

1. On your Group Policy management machine, open the [Group Policy Management Console](/en-us/previous-versions/windows/desktop/gpmc/group-policy-management-console-portal), right-click the Group Policy Object you want to configure and select **Edit**.
2. Using the **Group Policy Management Editor** go to **Computer configuration**.
3. Select **Policies** then **Administrative templates**.
4. Expand the tree to **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **Security Intelligence Updates**.
5. Double-click **Allow real-time security intelligence updates based on reports to Microsoft MAPS** and set the option to **Enabled**. Then select **OK**.
6. **Allow notifications to disable definitions-based reports to Microsoft MAPS** and set the option to **Enabled**. Then select **OK**.

    Note

    **Allow notifications to disable definitions based reports** enables Microsoft MAPS to disable those definitions known to cause false-positive reports. You must configure your computer to join Microsoft MAPS for this function to work.

Tip

If you're looking for Antivirus related information for other platforms, see:

- [Set preferences for Microsoft Defender for Endpoint on macOS](mac-preferences)
- [Microsoft Defender for Endpoint on Mac](microsoft-defender-endpoint-mac)
- [macOS Antivirus policy settings for Microsoft Defender Antivirus for Intune](/en-us/intune/intune-service/protect/antivirus-microsoft-defender-settings-macos)
- [Set preferences for Microsoft Defender for Endpoint on Linux](linux-preferences)
- [Microsoft Defender for Endpoint on Linux](microsoft-defender-endpoint-linux)
- [Configure Defender for Endpoint on Android features](android-configure)
- [Configure Microsoft Defender for Endpoint on iOS features](ios-configure-features)