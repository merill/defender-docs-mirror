---
layout: Conceptual
title: Onboarding using Microsoft Configuration Manager - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/onboarding-endpoint-configuration-manager
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to onboard to Microsoft Defender for Endpoint using Microsoft Configuration Manager
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
ms.custom:
- admindeeplinkDEFENDER
- sfi-image-nochange
ms.topic: install-set-up-deploy
ms.subservice: onboard
ms.date: 2025-03-26T00:00:00.0000000Z
locale: en-us
document_id: b2817db1-d17c-70b2-6445-554f9e4e2f72
document_version_independent_id: b2817db1-d17c-70b2-6445-554f9e4e2f72
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/onboarding-endpoint-configuration-manager.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: onboarding-endpoint-configuration-manager
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/onboarding-endpoint-configuration-manager.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/4c50f262-d533-4ba4-9d4a-08899ec3a3d1
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6a8c83be-f1de-4e90-bde0-bd097999a60c
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: b0579247-ef3f-6796-60ae-0c472bfde29a
---

# Onboarding using Microsoft Configuration Manager - Microsoft Defender for Endpoint | Microsoft Learn

This article acts as an example onboarding method.

In the [Planning](deployment-strategy) article, there were several methods provided to onboard devices to the service. This article covers the co-management architecture.

[![The cloud-native architecture](media/co-management-architecture.png)](media/co-management-architecture.png#lightbox)*Diagram of environment architectures*

While Defender for Endpoint supports onboarding of various endpoints and tools, this article doesn't cover them. For information on general onboarding using other supported deployment tools and methods, see [Onboarding overview](onboarding).

This article guides users in:

- Step 1: Onboarding Windows devices to the service
- Step 2: Configuring Defender for Endpoint capabilities

This onboarding guidance walks you through the following basic steps that you need to take when using Microsoft Configuration Manager:

- **Creating a collection in Microsoft Configuration Manager**
- **Configuring Microsoft Defender for Endpoint capabilities using Microsoft Configuration Manager**

Note

Only Windows devices are covered in this example deployment.

## Step 1: Onboard Windows devices using Microsoft Configuration Manager

### Collection creation

To onboard Windows devices with Microsoft Configuration Manager, the deployment can target an existing collection or a new collection can be created for testing.

Onboarding using tools such as Group policy or manual method doesn't install any agent on the system.

Within the Microsoft Configuration Manager, console the onboarding process will be configured as part of the compliance settings within the console.

Any system that receives this required configuration maintains that configuration for as long as the Configuration Manager client continues to receive this policy from the management point.

Follow the steps below to onboard endpoints using Microsoft Configuration Manager.

1. In Microsoft Configuration Manager console, navigate to **Assets and Compliance &gt; Overview &gt; Device Collections**.

    [![The Microsoft Configuration Manager wizard1](media/configmgr-device-collections.png)](media/configmgr-device-collections.png#lightbox)
2. Right select **Device Collection** and select **Create Device Collection**.

    [![The Microsoft Configuration Manager wizard2](media/configmgr-create-device-collection.png)](media/configmgr-create-device-collection.png#lightbox)
3. Provide a **Name** and **Limiting Collection**, then select **Next**.

    [![The Microsoft Configuration Manager wizard3](media/configmgr-limiting-collection.png)](media/configmgr-limiting-collection.png#lightbox)
4. Select **Add Rule** and choose **Query Rule**.

    [![The Microsoft Configuration Manager wizard4](media/configmgr-query-rule.png)](media/configmgr-query-rule.png#lightbox)
5. Select **Next** on the **Direct Membership Wizard** and select on **Edit Query Statement**. [![The Microsoft Configuration Manager wizard5](media/configmgr-direct-membership.png)](media/configmgr-direct-membership.png#lightbox)
6. Select **Criteria** and then choose the star icon.

    [![The Microsoft Configuration Manager wizard6](media/configmgr-criteria.png)](media/configmgr-criteria.png#lightbox)
7. Keep criterion type as **simple value**, choose whereas **Operating System - build number**, operator as **is greater than or equal to** and value **14393** and select on **OK**. [![The Microsoft Configuration Manager wizard7](media/configmgr-simple-value.png)](media/configmgr-simple-value.png#lightbox)
8. Select **Next** and **Close**.

    [![The Microsoft Configuration Manager wizard8](media/configmgr-membership-rules.png)](media/configmgr-membership-rules.png#lightbox)
9. Select **Next**.

    [![The Microsoft Configuration Manager wizard9](media/configmgr-confirm.png)](media/configmgr-confirm.png#lightbox)

After completing this task, you now have a device collection with all the Windows endpoints in the environment.

## Step 2: Configure Microsoft Defender for Endpoint capabilities

This section guides you in configuring the following capabilities using Microsoft Configuration Manager on Windows devices:

- **Endpoint detection and response**
- **Next-generation protection**
- **Attack surface reduction**

### Endpoint detection and response

#### Windows 10 and Windows 11

From within the Microsoft Defender portal it's possible to download the `.onboarding` policy that can be used to create the policy in System Center Configuration Manager and deploy that policy to Windows 10 and Windows 11 devices.

1. In the [Microsoft Defender portal](https://security.microsoft.com), select [Settings and then Onboarding](https://security.microsoft.com/preferences2/onboarding).
2. Under Deployment method, select the supported version of **Microsoft Configuration Manager**.

    [![The Microsoft Configuration Manager wizard10](media/mdatp-onboarding-wizard.png)](media/mdatp-onboarding-wizard.png#lightbox)
3. Select **Download package**.

    [![The Microsoft Configuration Manager wizard11](media/mdatp-download-package.png)](media/mdatp-download-package.png#lightbox)
4. Save the package to an accessible location.
5. In Microsoft Configuration Manager, navigate to: **Assets and Compliance &gt; Overview &gt; Endpoint Protection &gt; Microsoft Defender ATP Policies**.
6. Right-click **Microsoft Defender ATP Policies** and select **Create Microsoft Defender ATP Policy**.

    [![The Microsoft Configuration Manager wizard12](media/configmgr-create-policy.png)](media/configmgr-create-policy.png#lightbox)
7. Enter the name and description, verify **Onboarding** is selected, then select **Next**.

    [![The Microsoft Configuration Manager wizard13](media/configmgr-policy-name.png)](media/configmgr-policy-name.png#lightbox)
8. Select **Browse**.
9. Navigate to the location of the downloaded file from step 4 above.
10. Select **Next**.
11. Configure the Agent with the appropriate samples (**None** or **All file types**).

    [![The configuration settings1](media/configmgr-config-settings.png)](media/configmgr-config-settings.png#lightbox)
12. Select the appropriate telemetry (**Normal** or **Expedited**) then select **Next**.

    [![The configuration settings2](media/configmgr-telemetry.png)](media/configmgr-telemetry.png#lightbox)
13. Verify the configuration, then select **Next**.

    [![The configuration settings3](media/configmgr-verify-configuration.png)](media/configmgr-verify-configuration.png#lightbox)
14. Select **Close** when the Wizard completes.
15. In the Microsoft Configuration Manager console, right-click the Defender for Endpoint policy you created and select **Deploy**.

    [![The configuration settings4](media/configmgr-deploy.png)](media/configmgr-deploy.png#lightbox)
16. On the right panel, select the previously created collection and select **OK**.

    [![The configuration settings5](media/configmgr-select-collection.png)](media/configmgr-select-collection.png#lightbox)

#### Previous versions of Windows Client (Windows 7 and Windows 8.1)

Follow the steps below to identify the Defender for Endpoint Workspace ID and Workspace Key that will be required for the onboarding of previous versions of Windows.

1. In the [Microsoft Defender portal](https://security.microsoft.com), select **Settings** &gt; **Endpoints** &gt; **Onboarding** (under **Device Management**).
2. Under operating system, choose **Windows 7 SP1 and 8.1**.
3. Copy the **Workspace ID** and **Workspace Key** and save them. They'll be used later in the process.

    [![The onboarding process](media/91b738e4b97c4272fd6d438d8c2d5269.png)](media/91b738e4b97c4272fd6d438d8c2d5269.png#lightbox)
4. Install the Microsoft Monitoring Agent (MMA).

    MMA is currently (as of January 2019) supported on the following Windows Operating Systems:

    - Server SKUs: Windows Server 2008 SP1 or Newer
    - Client SKUs: Windows 7 SP1 and later

    The MMA agent needs to be installed on Windows devices. To install the agent, some systems need to download the [Update for customer experience and diagnostic telemetry](https://support.microsoft.com/servicing/os/windows/2019/11/update-for-customer-experience-and-diagnostic-telemetry) in order to collect the data with MMA. These system versions include but may not be limited to:

    - Windows 8.1
    - Windows 7
    - Windows Server 2016
    - Windows Server 2012 R2
    - Windows Server 2008 R2

    Specifically, for Windows 7 SP1, the following patches must be installed:

    - Install [KB4074598](https://support.microsoft.com/servicing/os/windows-7/2018/02/february-13-2018-kb4074598-monthly-rollup)
    - Install either [.NET Framework 4.5 or later](/en-us/dotnet/framework/install/guide-for-developers)**or**[KB3154518](https://support.microsoft.com/topic/support-for-tls-system-default-versions-included-in-the-net-framework-3-5-1-on-windows-7-sp1-and-server-2008-r2-sp1-5ef38dda-8e6c-65dc-c395-62d2df58715a). Do not install both on the same system.
5. If you're using a proxy to connect to the Internet see the Configure proxy settings section.

Once completed, you should see onboarded endpoints in the portal within an hour.

### Next generation protection

Microsoft Defender Antivirus is a built-in anti-malware solution that provides next generation protection for desktops, portable computers, and servers.

1. In the Microsoft Configuration Manager console, navigate to **Assets and Compliance &gt; Overview &gt; Endpoint Protection &gt; Antimalware Polices** and choose **Create Antimalware Policy**.

    [![The antimalware policy](media/9736e0358e86bc778ce1bd4c516adb8b.png)](media/9736e0358e86bc778ce1bd4c516adb8b.png#lightbox)
2. Select **Scheduled scans**, **Scan settings**, **Default actions**, **Real-time protection**, **Exclusion settings**, **Advanced**, **Threat overrides**, **Cloud Protection Service** and **Security intelligence updates** and choose **OK**.

    [![The next-generation protection pane1](media/1566ad81bae3d714cc9e0d47575a8cbd.png)](media/1566ad81bae3d714cc9e0d47575a8cbd.png#lightbox)

    In certain industries or some select enterprise customers might have specific needs on how Antivirus is configured.

    [Quick scan versus full scan and custom scan](schedule-antivirus-scans#comparing-the-quick-scan-full-scan-and-custom-scan)

    For more information, see [Windows Security configuration framework](https://github.com/microsoft/SecCon-Framework/blob/master/windows-security-configuration-framework.md).

    [![The next-generation protection pane2](media/cd7daeb392ad5a36f2d3a15d650f1e96.png)](media/cd7daeb392ad5a36f2d3a15d650f1e96.png#lightbox)

    [![The next-generation protection pane3](media/36c7c2ed737f2f4b54918a4f20791d4b.png)](media/36c7c2ed737f2f4b54918a4f20791d4b.png#lightbox)

    [![The next-generation protection pane4](media/a28afc02c1940d5220b233640364970c.png)](media/a28afc02c1940d5220b233640364970c.png#lightbox)

    [![The next-generation protection pane5](media/5420a8790c550f39f189830775a6d4c9.png)](media/5420a8790c550f39f189830775a6d4c9.png#lightbox)

    [![The next-generation protection pane6](media/33f08a38f2f4dd12a364f8eac95e8c6b.png)](media/33f08a38f2f4dd12a364f8eac95e8c6b.png#lightbox)

    [![The next-generation protection pane7](media/41b9a023bc96364062c2041a8f5c344e.png)](media/41b9a023bc96364062c2041a8f5c344e.png#lightbox)

    [![The next-generation protection pane8](media/945c9c5d66797037c3caeaa5c19f135c.png)](media/945c9c5d66797037c3caeaa5c19f135c.png#lightbox)

    [![The next-generation protection pane9](media/3876ca687391bfc0ce215d221c683970.png)](media/3876ca687391bfc0ce215d221c683970.png#lightbox)
3. Right-click on the newly created anti-malware policy and select **Deploy**.

    [![The next-generation protection pane10](media/f5508317cd8c7870627cb4726acd5f3d.png)](media/f5508317cd8c7870627cb4726acd5f3d.png#lightbox)
4. Target the new anti-malware policy to your Windows collection and select **OK**.

    [![The next-generation protection pane11](media/configmgr-select-collection.png)](media/configmgr-select-collection.png#lightbox)

After completing this task, you now have successfully configured Microsoft Defender Antivirus.

### Attack surface reduction

The attack surface reduction pillar of Defender for Endpoint includes the feature set that is available under Exploit Guard. Attack surface reduction (ASR) rules, Controlled Folder Access, Network Protection, and Exploit Protection.

All these features provide a test mode and a block mode. In test mode, there's no end-user impact. All it does is collect other telemetry and make it available in the Microsoft Defender portal. The goal with a deployment is to step-by-step move security controls into block mode.

To set attack surface reduction rules in test mode:

1. In the Microsoft Configuration Manager console, navigate to **Assets and Compliance &gt; Overview &gt; Endpoint Protection &gt; Windows Defender Exploit Guard** and choose **Create Exploit Guard Policy**.

    [![The Microsoft Configuration Manager console0](media/728c10ef26042bbdbcd270b6343f1a8a.png)](media/728c10ef26042bbdbcd270b6343f1a8a.png#lightbox)
2. Select **Attack Surface Reduction**.
3. Set rules to **Audit** and select **Next**.

    [![The Microsoft Configuration Manager console1](media/d18e40c9e60aecf1f9a93065cb7567bd.png)](media/d18e40c9e60aecf1f9a93065cb7567bd.png#lightbox)
4. Confirm the new Exploit Guard policy by selecting **Next**.

    [![The Microsoft Configuration Manager console2](media/0a6536f2c4024c08709cac8fcf800060.png)](media/0a6536f2c4024c08709cac8fcf800060.png#lightbox)
5. Once the policy is created select **Close**.

    [![The Microsoft Configuration Manager console3](media/95d23a07c2c8bc79176788f28cef7557.png)](media/95d23a07c2c8bc79176788f28cef7557.png#lightbox)
6. Right-click on the newly created policy and choose **Deploy**.

    [![The Microsoft Configuration Manager console4](media/8999dd697e3b495c04eb911f8b68a1ef.png)](media/8999dd697e3b495c04eb911f8b68a1ef.png#lightbox)
7. Target the policy to the newly created Windows collection and select **OK**.

    [![The Microsoft Configuration Manager console5](media/0ccfe3e803be4b56c668b220b51da7f7.png)](media/0ccfe3e803be4b56c668b220b51da7f7.png#lightbox)

After completing this task, you now have successfully configured attack surface reduction rules in test mode.

Below are more steps to verify whether attack surface reduction rules are correctly applied to endpoints. (This may take few minutes)

1. From a web browser, go to [Microsoft Defender XDR](https://go.microsoft.com/fwlink/p/?linkid=2077139).
2. Select **Configuration management** from left side menu.
3. Select **Go to attack surface management** in the Attack surface management panel.

    [![The attack surface management](media/security-center-attack-surface-mgnt-tile.png)](media/security-center-attack-surface-mgnt-tile.png#lightbox)
4. Select **Configuration** tab in Attack surface reduction rules reports. It shows attack surface reduction rules configuration overview and attack surface reduction rules status on each device.

    [![The attack surface reduction rules reports1](media/f91f406e6e0aae197a947d3b0e8b2d0d.png)](media/f91f406e6e0aae197a947d3b0e8b2d0d.png#lightbox)
5. Select each device shows configuration details of attack surface reduction rules.

    [![The attack surface reduction rules reports2](media/24bfb16ed561cbb468bd8ce51130ca9d.png)](media/24bfb16ed561cbb468bd8ce51130ca9d.png#lightbox)

See [Monitor ASR rule activity](attack-surface-reduction-rules-monitor) for more details.

#### Set Network Protection rules in test mode

1. In the Microsoft Configuration Manager console, navigate to **Assets and Compliance &gt; Overview &gt; Endpoint Protection &gt; Windows Defender Exploit Guard** and choose **Create Exploit Guard Policy**.

    [![The System Center Configuration Manager1](media/728c10ef26042bbdbcd270b6343f1a8a.png)](media/728c10ef26042bbdbcd270b6343f1a8a.png#lightbox)
2. Select **Network protection**.
3. Set the setting to **Audit** and select **Next**.

    [![The System Center Configuration Manager2](media/c039b2e05dba1ade6fb4512456380c9f.png)](media/c039b2e05dba1ade6fb4512456380c9f.png#lightbox)
4. Confirm the new Exploit Guard Policy by selecting **Next**. [![The Exploit Guard policy1](media/0a6536f2c4024c08709cac8fcf800060.png)](media/0a6536f2c4024c08709cac8fcf800060.png#lightbox)
5. Once the policy is created select on **Close**.

    [![The Exploit Guard policy2](media/95d23a07c2c8bc79176788f28cef7557.png)](media/95d23a07c2c8bc79176788f28cef7557.png#lightbox)
6. Right-click on the newly created policy and choose **Deploy**. [![The Microsoft Configuration Manager-1](media/8999dd697e3b495c04eb911f8b68a1ef.png)](media/8999dd697e3b495c04eb911f8b68a1ef.png#lightbox)
7. Select the policy to the newly created Windows collection and choose **OK**.

    [![The Microsoft Configuration Manager-2](media/0ccfe3e803be4b56c668b220b51da7f7.png)](media/0ccfe3e803be4b56c668b220b51da7f7.png#lightbox)

After completing this task, you now have successfully configured Network Protection in test mode.

#### To set Controlled Folder Access rules in test mode

1. In the Microsoft Configuration Manager console, navigate to **Assets and Compliance** &gt; **Overview** &gt; **Endpoint Protection** &gt; **Windows Defender Exploit Guard** and then choose **Create Exploit Guard Policy**.

    [![The Microsoft Configuration Manager-3](media/728c10ef26042bbdbcd270b6343f1a8a.png)](media/728c10ef26042bbdbcd270b6343f1a8a.png#lightbox)
2. Select **Controlled folder access**.
3. Set the configuration to **Audit** and select **Next**.

    [![The Microsoft Configuration Manager-4](media/a8b934dab2dbba289cf64fe30e0e8aa4.png)](media/a8b934dab2dbba289cf64fe30e0e8aa4.png#lightbox)
4. Confirm the new Exploit Guard Policy by selecting **Next**. [![The Microsoft Configuration Manager-5](media/0a6536f2c4024c08709cac8fcf800060.png)](media/0a6536f2c4024c08709cac8fcf800060.png#lightbox)
5. Once the policy is created select on **Close**.

    [![The Microsoft Configuration Manager-6](media/95d23a07c2c8bc79176788f28cef7557.png)](media/95d23a07c2c8bc79176788f28cef7557.png#lightbox)
6. Right-click on the newly created policy and choose **Deploy**. [![The Microsoft Configuration Manager-7](media/8999dd697e3b495c04eb911f8b68a1ef.png)](media/8999dd697e3b495c04eb911f8b68a1ef.png#lightbox)
7. Target the policy to the newly created Windows collection and select **OK**.

[![The Microsoft Configuration Manager-8](media/0ccfe3e803be4b56c668b220b51da7f7.png)](media/0ccfe3e803be4b56c668b220b51da7f7.png#lightbox)

You have now successfully configured Controlled folder access in test mode.

## Related article

- [Onboard Windows devices to Microsoft Defender for Endpoint using Microsoft Intune](onboarding-endpoint-manager)