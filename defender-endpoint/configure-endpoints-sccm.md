---
layout: Conceptual
title: Onboard Windows devices to Microsoft Defender for Endpoint with Configuration Manager - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/configure-endpoints-sccm
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use Microsoft Configuration Manager to onboard, monitor, and offboard supported Windows devices in Microsoft Defender for Endpoint.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
audience: ITPro
ms.collection:
- m365-security
- tier1
ms.custom:
- admindeeplinkDEFENDER
- msecd-doc-authoring-1015
ms.topic: install-set-up-deploy
ms.subservice: onboard
ms.date: 2026-09-21T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 75181c25-9f4a-f130-c36f-ecda794840f6
document_version_independent_id: 75181c25-9f4a-f130-c36f-ecda794840f6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/configure-endpoints-sccm.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-endpoints-sccm
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/configure-endpoints-sccm.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: bb97da67-6779-f160-8311-88d6b1af459a
---

# Onboard Windows devices to Microsoft Defender for Endpoint with Configuration Manager - Microsoft Defender for Endpoint | Microsoft Learn

You can use Microsoft Configuration Manager current branch to onboard and monitor supported Windows client and Windows Server devices in Microsoft Defender for Endpoint. The Configuration Manager documentation contains the detailed console procedures. This article provides Defender-specific package selections, verification guidance, and offboarding behavior.

You can also use [tenant attach](/en-us/intune/configmgr/tenant-attach/endpoint-security-get-started) to manage endpoint security policies from the Microsoft Intune admin center. For the complete Configuration Manager onboarding procedure, see [Onboard devices using Configuration Manager](/en-us/intune/configmgr/protect/deploy-use/defender-advanced-threat-protection).

Note

Defender for Endpoint doesn't support onboarding during the [Out-of-Box Experience (OOBE)](/en-us/windows-hardware/test/assessments/out-of-box-experience) phase. Complete OOBE after installing or upgrading Windows before you onboard the device.

Note

The Defender deployment tool can be used to deploy Defender endpoint security on Windows and Linux devices. The tool is a lightweight, self-updating application that streamlines the deployment process. For more information, see [Deploy Microsoft Defender endpoint security to Windows devices using the Defender deployment tool](/en-us/defender-endpoint/defender-deployment-tool-windows) and [Deploy Microsoft Defender endpoint security to Linux devices using the Defender deployment tool (preview)](/en-us/defender-endpoint/linux-install-with-defender-deployment-tool).

## Prerequisites

- Review the [minimum requirements for Microsoft Defender for Endpoint](minimum-requirements).
- Use a supported version of Configuration Manager current branch, and install the Configuration Manager client on each target device.
- In Configuration Manager, your account needs the **Endpoint Protection Manager** security role.
- To download the onboarding package, you need full access to Defender for Endpoint. The Microsoft Entra **Security Administrator** role grants this access. For more information, see [Assign basic permissions](basic-permissions).
- If you use Configuration Manager to manage Microsoft Defender Antivirus or attack surface reduction settings, install the [Endpoint Protection point site system role](/en-us/intune/configmgr/protect/deploy-use/endpoint-protection-site-role).
- [Configure device connectivity](configure-device-connectivity) for the Defender for Endpoint service.

## Onboard devices using Configuration Manager

Configuration Manager version 2207 and later can deploy the modern unified Defender for Endpoint client to Windows Server 2012 R2 and Windows Server 2016. For prerequisites and the complete onboarding procedure, see [Onboard devices using Configuration Manager 2207 and later](/en-us/intune/configmgr/protect/deploy-use/defender-advanced-threat-protection#bkmk_2207).

### Select a device collection

Deploy the onboarding policy to an existing device collection, or create a limited collection for testing. Don't use a fixed operating-system build query unless the query accurately represents every supported operating system that you intend to onboard. For current collection guidance, see [Create collections in Configuration Manager](/en-us/intune/configmgr/core/clients/manage/collections/create-collections#create-a-collection).

### Download the onboarding package

On the **Onboarding** page in the Microsoft Defender portal at https://security.microsoft.com/securitysettings/endpoints/onboarding, select these values:

- **Step 1: Select an operating system to start deployment**: Select **Windows 10 and 11**. The downloaded configuration file is also used for supported up-level Windows Server operating systems. Don't select **Windows**, which starts the separate [Defender deployment tool workflow](defender-deployment-tool-windows).
- **Deployment method**: Select **Microsoft Endpoint Configuration Manager current branch and later**.

For the complete download procedure, see [Get an onboarding configuration file for up-level devices](/en-us/intune/configmgr/protect/deploy-use/defender-advanced-threat-protection#get-an-onboarding-configuration-file-for-up-level-devices).

Important

The Defender for Endpoint configuration file contains organization-specific information. Store and transfer the file securely.

### Create and deploy the onboarding policy

Create the onboarding policy from the downloaded configuration file, and deploy the policy to the target device collection. For the complete procedure, see [Onboard the up-level devices using Configuration Manager](/en-us/intune/configmgr/protect/deploy-use/defender-advanced-threat-protection#onboard-the-up-level-devices). The Configuration Manager console retains the legacy labels **Microsoft Defender ATP Policies** and **Create Microsoft Defender ATP Policy**.

Note

For Windows Server 2012 R2 and Windows Server 2016, select **MDE Client (recommended)** in the Configuration Manager client settings. For mixed collections that include devices that still require Microsoft Monitoring Agent (MMA), see [Onboard devices with MDE Client and MMA](/en-us/intune/configmgr/protect/deploy-use/defender-advanced-threat-protection#bkmk_2207_any_os). To migrate servers from MMA, see [Migrate servers to the unified solution](application-deployment-via-mecm).

## Configure sample collection

The onboarding policy wizard lets you choose **None** or **All file types** for sample sharing. You can also use a remediating Configuration Manager compliance rule to configure the sample collection registry value on targeted devices.

Note

Configuration Manager typically manages sample collection through the onboarding policy wizard or a compliance rule.

The compliance rule can configure this registry entry:

```console
Path: "HKLM\SOFTWARE\Policies\Microsoft\Windows Advanced Threat Protection"
Name: "AllowSampleCollection"
Value: 0 or 1
```

The key type is `DWORD`. Supported values are:

- `0`: Don't allow sample sharing from the device.
- `1`: Allow all file types to be shared from the device.

If the registry value doesn't exist, the default value is `1`.

For current compliance-setting guidance, see [Plan for and configure compliance settings](/en-us/intune/configmgr/compliance/plan-design/plan-for-and-configure-compliance-settings).

## Configure endpoint protection settings

Onboarding doesn't configure Microsoft Defender Antivirus or other endpoint protection features. Use Configuration Manager policies or tenant attach to configure the security controls required by your organization.

Important

Install the Endpoint Protection point site system role before you configure Configuration Manager client settings for Endpoint Protection.

- To configure Endpoint Protection roles, alerts, update sources, antimalware policies, and client settings, see [Configure Endpoint Protection](/en-us/intune/configmgr/protect/deploy-use/endpoint-protection-configure).
- To review Endpoint Protection client settings, see [About client settings](/en-us/intune/configmgr/core/clients/deploy/about-client-settings#endpoint-protection).
- To refresh assigned policy on clients, see [Initiate policy retrieval for a Configuration Manager client](/en-us/intune/configmgr/core/clients/manage/manage-clients).
- To configure and test attack surface reduction rules, see [Configure ASR rules in Microsoft Configuration Manager](attack-surface-reduction-rules-configure#configure-asr-rules-and-global-asr-rule-exclusions-in-microsoft-configuration-manager).

### Configure network protection

Configure network protection by using a Windows Defender Exploit Guard policy. Test network protection in audit mode before you enable block mode. For prerequisites and deployment instructions, see [Configure network protection in Microsoft Configuration Manager](enable-network-protection#configure-network-protection-in-microsoft-configuration-manager).

### Configure controlled folder access

Test controlled folder access in audit mode before you enable block mode. Review audit events and add trusted applications only when needed. For more information, see [Configure controlled folder access](controlled-folder-access-configure) and [Monitor controlled folder access activity](controlled-folder-access-monitor).

## Monitor device configuration

Use the built-in Configuration Manager dashboard to review onboarding status and agent health. For the dashboard procedure and status definitions, see [Monitor Microsoft Defender for Endpoint onboarding](/en-us/intune/configmgr/protect/deploy-use/defender-advanced-threat-protection#monitor).

On the **Device inventory** page in the Microsoft Defender portal at https://security.microsoft.com/machines?category=all-devices, search for the target devices and verify that their sensor health state is active.

You can also use a non-remediating compliance rule to monitor this registry entry:

```console
Path: "HKLM\SOFTWARE\Microsoft\Windows Advanced Threat Protection\Status"
Name: "OnboardingState"
Value: "1"
```

If deployment fails or a device doesn't report as expected, see [Troubleshoot Microsoft Defender for Endpoint onboarding issues](troubleshoot-onboarding).

## Run a detection test to verify onboarding

To generate a test alert and confirm end-to-end reporting, see [Run a detection test on a newly onboarded device](run-detection-test).

## Offboard devices using Configuration Manager

For Configuration Manager current branch, the offboarding configuration file expires 30 days after you download it. Defender for Endpoint rejects expired files.

Important

The Defender for Endpoint offboarding configuration file contains organization-specific information. Store and transfer the file securely.

Don't deploy onboarding and offboarding policies to the same device at the same time. Remove the target devices from the onboarding policy deployment before you deploy the offboarding policy.

### Offboard devices using Microsoft Configuration Manager current branch

On the **Offboarding** page in the Microsoft Defender portal at https://security.microsoft.com/securitysettings/endpoints/offboarding, select **Windows 10 and 11** and **Microsoft Endpoint Configuration Manager current branch and later**. The **Windows 10 and 11** package also offboards supported Windows Server devices in the collection and removes MMA when needed. Don't select **Windows**, which starts the separate Defender deployment tool workflow.

For instructions to create and deploy the Configuration Manager offboarding policy, see [Create an offboarding configuration file](/en-us/intune/configmgr/protect/deploy-use/defender-advanced-threat-protection#create-an-offboarding-configuration-file).

Important

Offboarding stops the device from sending new detection, vulnerability, and security data to Defender for Endpoint. Historical data remains in the Defender portal until the configured retention period expires. The device profile, without data, remains in the device inventory for up to 180 days. For more information, see [Offboard devices](offboard-machines).

### Offboard devices using System Center 2012 R2 Configuration Manager

System Center 2012 and System Center 2012 R2 reached end of support on July 12, 2022. Upgrade to Configuration Manager current branch before you deploy or manage Defender for Endpoint. For more information, see [System Center 2012 end of support](/en-us/lifecycle/announcements/system-center-2012-end-of-support).

The following archived documentation remains available for organizations completing a migration:

- [Configure application detection methods in System Center 2012 R2 Configuration Manager](/en-us/previous-versions/system-center/system-center-2012-R2/gg682159%28v=technet.10%29#step-4-configure-detection-methods-to-indicate-the-presence-of-the-deployment-type).
- [Introduction to compliance settings in System Center 2012 R2 Configuration Manager](/en-us/previous-versions/system-center/system-center-2012-R2/gg682139%28v=technet.10%29).
- [Packages and programs in System Center 2012 R2 Configuration Manager](/en-us/previous-versions/system-center/system-center-2012-R2/gg699369%28v=technet.10%29).