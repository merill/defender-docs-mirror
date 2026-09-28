---
layout: Conceptual
title: Onboard Windows devices to Microsoft Defender for Endpoint using Microsoft Intune - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/onboarding-endpoint-manager
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use Microsoft Intune to onboard Windows devices to Microsoft Defender for Endpoint, configure security policies, and validate the deployment.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- m365solution-endpointprotect
- m365solution-scenario
- highpri
- tier1
ms.topic: how-to
ms.subservice: onboard
ms.date: 2026-09-14T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: 95172cc6-165e-911c-0fe1-5c60fb408726
document_version_independent_id: 95172cc6-165e-911c-0fe1-5c60fb408726
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/onboarding-endpoint-manager.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: onboarding-endpoint-manager
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/onboarding-endpoint-manager.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/a72e95ff-4b4f-4cc1-90c6-7dcba67ff05f
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/24dc3ccd-591a-4415-a1fe-8759afafcb12
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 94805241-f33b-5a77-925b-184cdddb2e80
---

# Onboard Windows devices to Microsoft Defender for Endpoint using Microsoft Intune - Microsoft Defender for Endpoint | Microsoft Learn

Use Microsoft Intune to onboard a test group of Windows devices to Microsoft Defender for Endpoint. Then configure Microsoft Defender Antivirus, network protection, and attack surface reduction (ASR) rules, and validate each policy.

This article continues the deployment process described in [Identify Defender for Endpoint architecture and deployment method](deployment-strategy) and covers the cloud-native architecture that uses Microsoft Intune.

[![Diagram of the cloud-native architecture for Microsoft Defender for Endpoint.](media/cloud-native-architecture.png)](media/cloud-native-architecture.png#lightbox)

*Cloud-native architecture.*

## Prerequisites

- A Microsoft Intune subscription. Intune is a separate product that isn't part of Defender for Endpoint, and it isn't included in all subscriptions. You need a subscription that includes Intune, or you can buy it separately as a standalone subscription or add-on. For licensing details, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).
- Windows devices enrolled in Intune. For more information, see [Device enrollment in Microsoft Intune](/en-us/intune/intune-service/fundamentals/deployment-guide-enrollment).
- An account with the Intune **Endpoint Security Manager** role or equivalent permissions.
- A connection between Intune and Defender for Endpoint. For instructions and required permissions, see [Configure Microsoft Defender for Endpoint with Intune and onboard devices](/en-us/intune/device-security/microsoft-defender/configure-integration).
- Access to the [Microsoft Intune admin center](https://aka.ms/memac) and the [Microsoft Defender portal](https://security.microsoft.com).

This procedure uses targeted endpoint security policies instead of [Intune security baselines](/en-us/intune/intune-service/protect/security-baseline-settings-defender). For an overview of Intune, see [What is Microsoft Intune?](/en-us/intune/intune-service/fundamentals/what-is-intune). For information about Configuration Manager, see [Microsoft Configuration Manager](/en-us/intune/configmgr).

If you don't have Intune, review the other architectures and onboarding methods in [Identify Defender for Endpoint architecture and deployment method](deployment-strategy) and [Onboarding overview](onboarding).

## Step 1: Create a test device group

Create a Microsoft Entra device group that contains the Windows devices where you want to evaluate the Defender for Endpoint configurations. For instructions to create the group and add members, see [Add groups to organize users and devices](/en-us/intune/intune-service/fundamentals/groups-add).

## Step 2: Create and assign Defender for Endpoint policies

Create and assign separate endpoint security policies for endpoint detection and response (EDR), next-generation protection, and ASR rules.

### Endpoint detection and response

Create an endpoint detection and response (EDR) policy to onboard the devices. For detailed instructions, see [Onboard Windows devices to Microsoft Defender for Endpoint by using Microsoft Intune](configure-endpoints-mdm#onboard-devices-using-microsoft-intune).

When you create the policy, use these specific settings:

- **Platform**: Select **Windows**.
- **Profile**: Select **Endpoint detection and response**.

On the **Assignments** page, include the test group that you created in Create a test device group.

### Next-generation protection

Create an endpoint security **Antivirus** policy to configure Microsoft Defender Antivirus. For detailed instructions and descriptions of the available settings, see [Configure Microsoft Defender Antivirus using Microsoft Intune](use-intune-config-manager-microsoft-defender-antivirus#configure-microsoft-defender-antivirus-settings-in-intune).

For this evaluation, use these specific settings:

- **Platform**: Select **Windows**.
- **Profile**: Select **Microsoft Defender Antivirus**.
- **Configuration settings**: Configure the cloud protection, exclusions, real-time protection, and remediation settings required by your organization. Set **Turn on cloud-delivered protection** and **Allow Real-Time Monitoring** to **Allowed**.

In the same policy, configure **Enable network protection** as **Enabled (audit mode)**. Microsoft recommends using audit mode in a test environment before enabling block mode. For detailed instructions, see [Configure network protection in Intune using endpoint security policies](enable-network-protection#configure-network-protection-in-intune-using-endpoint-security-policies).

On the **Assignments** page, include the test group that you created in Create a test device group.

### Attack surface reduction rules

Create an endpoint security **Attack surface reduction** policy. For detailed instructions, see [Configure ASR rules and exclusions in Intune using endpoint security policies](attack-surface-reduction-rules-configure#configure-asr-rules-and-exclusions-in-intune-using-endpoint-security-policies).

For this evaluation, use **Audit** mode for rules that require testing before enforcement. You can enable the [standard protection rules](attack-surface-reduction-rules-overview#asr-rules) in **Block** or **Warn** mode without testing. For information about the available rules and modes, see [Attack surface reduction rules reference](attack-surface-reduction-rules-reference).

On the **Assignments** page, include the test group that you created in Create a test device group.

## Step 3: Validate the configuration

### Confirm policy assignment status

After you assign a policy, devices receive it the next time they check in with Intune. For information about policy refresh intervals, see [Common questions and answers about device policies and profiles in Microsoft Intune](/en-us/intune/intune-service/configuration/device-profile-troubleshoot#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned).

For each policy, use the policy reports in the Intune admin center to review the **Device and user check-in status**, **Device assignment status**, and **Per setting status**. Confirm that the test devices have a **Succeeded** status. For detailed instructions, see [View details on a policy](/en-us/intune/intune-service/configuration/device-profile-monitor#view-details-on-a-policy).

Use **Per setting status** to identify settings that conflict with another policy.

### Confirm endpoint detection and response

1. On a test device that isn't already onboarded to Defender for Endpoint, run the following PowerShell command to check the service status:

    ```powershell
    Get-Service "Sense" | Format-List Status,Name,DisplayName
    ```

    The Microsoft Defender for Endpoint service shouldn't be running, as shown in the following output:

    ```console
    Status      : Stopped
    Name        : Sense
    DisplayName : Windows Defender Advanced Threat Protection Service
    ```
2. After Intune reports that the EDR policy was applied successfully, run the same PowerShell command on the device:

    ```powershell
    Get-Service "Sense" | Format-List Status,Name,DisplayName
    ```

    The Microsoft Defender for Endpoint service should be running, as shown in the following output:

    ```console
    Status      : Running
    Name        : Sense
    DisplayName : Windows Defender Advanced Threat Protection Service
    ```
3. On the **Device inventory** page in the Microsoft Defender portal at https://security.microsoft.com/machines, verify that the device appears. A newly onboarded device typically appears within 15 to 30 minutes.

[![Screenshot of the Microsoft Defender portal showing an onboarded device in the device inventory.](media/df0c64001b9219cfbd10f8f81a273190.png)](media/df0c64001b9219cfbd10f8f81a273190.png#lightbox)

### Confirm next-generation protection

1. Before applying the policy on a test device, verify that you can manually manage cloud-delivered protection and real-time protection:

[![Screenshot of Windows Security settings before Microsoft Defender Antivirus policy management.](media/88efb4c3710493a53f2840c3eac3e3d3.png)](media/88efb4c3710493a53f2840c3eac3e3d3.png#lightbox)
2. After the policy is applied, verify that **Turn on cloud-delivered protection** and **Turn on real-time protection** are turned on and unavailable for local changes:

[![Screenshot of Windows Security settings managed by a Microsoft Defender Antivirus policy.](media/9341428b2d3164ca63d7d4eaa5cff642.png)](media/9341428b2d3164ca63d7d4eaa5cff642.png#lightbox)

### Confirm attack surface reduction rules

1. On a test device without existing ASR rule settings, run the following command in an elevated PowerShell session to view the ASR configuration:

    ```powershell
    Get-MpPreference | Select-Object AttackSurfaceReduction*
    ```

    The result should show empty values for the ASR rule properties:

    ```console
    AttackSurfaceReductionOnlyExclusions                  :
    AttackSurfaceReductionRules_Actions                   :
    AttackSurfaceReductionRules_Ids                       :
    AttackSurfaceReductionRules_RuleSpecificExclusions    :
    AttackSurfaceReductionRules_RuleSpecificExclusions_Id :
    ```
2. After Intune reports that the ASR policy was applied successfully, run the following command in an elevated PowerShell session to view all configured ASR rule values:

    ```powershell
    $FormatEnumerationLimit = -1; Get-MpPreference | Format-List AttackSurfaceReduction*
    ```

    The output should list the configured rule IDs and their corresponding action values. The exact values depend on the rules and modes that you configured. The following output is an example:

    ```console
    AttackSurfaceReductionOnlyExclusions                  :
    AttackSurfaceReductionRules_Actions                   : {1, 1, 1, 1, 1, 1, 1, 1, 1, 5, 1, 1, 1, 1, 1, 1}
    AttackSurfaceReductionRules_Ids                       : {26190899-1602-49e8-8b27-eb1d0a1ce869,
                                                            33ddedf1-c6e0-47cb-833e-de6133960387,
                                                            3B576869-A4EC-4529-8536-B80A7769E899,
                                                            56a863a9-875e-4185-98a7-b882c64b5ce5,
                                                            5BEB7EFE-FD9A-4556-801D-275E5FFC04CC,
                                                            75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84,
                                                            7674ba52-37eb-4a4f-a9a1-f0f9a1619a2c,
                                                            92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B,
                                                            9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2,
                                                            a8f5898e-1dc8-49a9-9878-85004b8a61e6,
                                                            b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4,
                                                            BE9BA2D9-53EA-4CDC-84E5-9B1EEEE46550,
                                                            c1db55ab-c21a-4637-bb3f-a12568109d35,
                                                            D3E037E1-3EB8-44C8-A917-57927947596D,
                                                            D4F940AB-401B-4EFC-AADC-AD5F3C50688A,
                                                            e6db77e5-3df2-4cf1-b95a-636979351e5b}
    AttackSurfaceReductionRules_RuleSpecificExclusions    :
    AttackSurfaceReductionRules_RuleSpecificExclusions_Id :
    ```

### Confirm network protection

1. On a test device where network protection isn't already configured, run the following PowerShell command to view its status:

    ```powershell
    (Get-MpPreference).EnableNetworkProtection
    ```

    The result should be the value `0`, which indicates that network protection is off.
2. After Intune reports that the Antivirus policy was applied successfully, run the same PowerShell command:

    ```powershell
    (Get-MpPreference).EnableNetworkProtection
    ```

    The result should be the value `2`, which indicates that network protection is on in audit mode.