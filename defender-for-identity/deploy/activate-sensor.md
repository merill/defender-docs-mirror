---
layout: Conceptual
title: Activate the Microsoft Defender for Identity sensor v3.x - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/deploy/activate-sensor
feedback_system: Standard
feedback_product_url: https://aka.ms/MDIcommunity
breadcrumb_path: /azure-advanced-threat-protection/bread/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: microsoft-defender-for-identity
uhfHeaderId: MSDocsHeader-MicrosoftDefender
ms.suite: ems
description: Learn how to automatically or manually activate the Microsoft Defender for Identity sensor v3.x on eligible identity-role servers.
ms.date: 2026-09-14T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: rlitinsky
ms.custom: msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: 5575bdb0-cdf3-33bb-ac68-25e4e059d795
document_version_independent_id: 5575bdb0-cdf3-33bb-ac68-25e4e059d795
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/deploy/activate-sensor.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: deploy/activate-sensor
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/deploy/activate-sensor.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 6dfc672c-4e94-b9f1-bed3-3c261304a302
---

# Activate the Microsoft Defender for Identity sensor v3.x - Microsoft Defender for Identity | Microsoft Learn

For complete protection of your on-premises deployment, activate the Microsoft Defender for Identity sensor v3.x on all eligible servers. Supported server types include domain controllers. They also include Active Directory Federation Services (AD FS), Active Directory Certificate Services (AD CS), and Microsoft Entra Connect servers that aren't domain controllers. Eligible servers must meet the sensor v3.x prerequisites, including Windows Server 2019 or later. For supported servers running older operating systems, [deploy the Defender for Identity sensor v2.x](install-sensor) instead.

Note

Activating the Defender for Identity sensor v3.x on AD FS, AD CS, and Microsoft Entra Connect servers that aren't domain controllers is in preview.

## Prerequisites

See [Microsoft Defender for Identity sensor v3.x prerequisites](deploy-sensor-v3) for system requirements and [Sensor version limitations](deploy-sensor-v3#sensor-version-limitations) for supported scenarios before activating the Defender for Identity sensor v3.x on eligible servers.

## Turn on automatic sensor activation

Automatic activation applies only to eligible domain controllers onboarded to Defender for Endpoint.

To turn on automatic sensor activation:

1. In the Microsoft Defender portal, go to **Settings** &gt; **Identities** &gt; **Advanced features**.
2. Turn on **Automatic sensor v3.x activation**.

The **Advanced features** page also includes **Automatic Windows auditing configuration**. For details, see [Configure automatic Windows event auditing](configure-windows-event-collection#configure-defender-for-identity-to-collect-windows-events-automatically).

## Activate the Defender for Identity sensor v3.x

To activate the Defender for Identity sensor v3.x on an eligible server, follow these steps:

1. On the **Sensor management** tab of the **On-premises** page in the Microsoft Defender portal, select the eligible server where you want to activate Defender for Identity.
2. Select **Activate**, and confirm your selection when prompted.
3. When v3.x sensor activation for the selected server is complete, a green success banner appears. In the banner, select **Click here to see the onboarded servers**. The **Sensor management** tab opens, where you can check the sensor's health.

    [![Screenshot of the successful sensor activation banner with a link to view onboarded servers.](media/activated-sensor.png)](media/activated-sensor.png#lightbox)

## Onboard a domain controller without Defender for Endpoint deployment (preview)

Use onboarding without Defender for Endpoint deployment to activate the Defender for Identity sensor v3.x without first onboarding the domain controller to Defender for Endpoint:

Important

This onboarding method supports new sensor v3.x deployments on eligible domain controllers that don't have sensor v2.x installed.

1. [Configure your network environment to ensure connectivity with Defender for Endpoint](/en-us/defender-endpoint/configure-environment#enable-access-to-microsoft-defender-for-endpoint-service-urls-in-the-proxy-server) by using [streamlined URLs](/en-us/defender-endpoint/configure-device-connectivity#option-1-configure-connectivity-using-the-simplified-domain).
2. On the **Sensor management** tab of the **On-premises** page in the Microsoft Defender portal, select **Download onboarding package**.
3. In the **Download onboarding package** pane, expand **Windows Server 2019 or later**, enter a **Package name**, and select **Generate package**.

    [![Screenshot of the Download onboarding package pane with package name and Generate package options for Windows Server 2019 or later.](media/activate-sensor/sensor-deployment-package-options.png)](media/activate-sensor/sensor-deployment-package-options.png#lightbox)
4. When the package is ready, download it and copy the access key.

    Important

    The access key is used only during sensor installation. Regenerating the key invalidates the existing key, and installations that use the previous key fail.
5. Copy the downloaded package to the domain controller.
6. Extract the package, making sure the `resources` subfolder is preserved.
7. Open PowerShell as an administrator, change to the extracted folder, and run the onboarding script:

    ```powershell
    Set-Location .\DfiOnboarding
    .\DefenderForIdentityV3StandaloneOnboardingScript.cmd
    ```
8. When prompted, enter the access key from the Microsoft Defender portal. The input is masked.

## Confirm sensor activation

To confirm that the v3.x sensor is working:

1. On the **Sensor management** tab of the **On-premises** page in the Microsoft Defender portal, check that the activated server is listed.

Note

The first Defender for Identity sensor v3.x activation in your environment might take up to an hour to show as **Running** on the **Sensor management** tab. Subsequent activations appear within five minutes. Activation doesn't require a restart.

## What if I want to add Defender for Endpoint later?

If you onboarded a domain controller with Defender for Identity only and now want to add Defender for Endpoint, follow these steps:

1. [Offboard the domain controller and remove the sensor](../uninstall-sensor#offboard-a-domain-controller-that-isnt-onboarded-to-defender-for-endpoint-preview).
2. [Onboard the domain controller to Defender for Endpoint](/en-us/defender-endpoint/onboard-server).
3. After the domain controller appears on the **Sensor management** tab, activate the Defender for Identity sensor v3.x.