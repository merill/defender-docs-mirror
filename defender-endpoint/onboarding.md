---
layout: Conceptual
title: Onboard devices to Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/onboarding
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to onboard endpoints to Microsoft Defender for Endpoint service.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- m365solution-endpointprotect
- m365solution-scenario
- m365-initiative-defender-endpoint
- highpri
- tier1
ms.topic: install-set-up-deploy
ms.subservice: onboard
ms.date: 2025-05-08T00:00:00.0000000Z
locale: en-us
document_id: f9bd821b-1f19-bdc0-3544-3fd37952fd11
document_version_independent_id: f9bd821b-1f19-bdc0-3544-3fd37952fd11
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/onboarding.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: onboarding
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/onboarding.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 5ac78a88-f6b5-696d-cdde-344042158d5f
---

# Onboard devices to Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Important

If you want to run multiple security solutions side by side, see [Considerations for performance, configuration, and support](/en-us/defender-endpoint/mde-side-by-side).

You might have already configured mutual security exclusions for devices onboarded to Microsoft Defender for Endpoint. If you still need to set mutual exclusions to avoid conflicts, see [Add Microsoft Defender for Endpoint to the exclusion list for your existing solution](/en-us/defender-endpoint/switch-to-mde-phase-2#step-2-add-microsoft-defender-for-endpoint-to-the-exclusion-list-for-your-existing-solution).

## Onboard devices using any of the supported management tools

The deployment tool you use influences how you onboard endpoints to the service. Refer to your selected [deployment method](deployment-strategy#step-2-select-your-deployment-method).

If you're onboarding devices in the Microsoft Defender portal, follow these steps:

1. Make sure to review the [Minimum requirements for Defender for Endpoint](minimum-requirements).
2. In the [Microsoft Defender portal](https://security.microsoft.com), go to **System** &gt; **Settings** &gt; **Endpoints**, and then, under **Device management**, select **Onboarding**.

    ![Screenshot showing device onboarding in the Microsoft Defender portal for Defender for Endpoint.](media/mde-device-onboarding-ui.png)
3. Under **Select operating system to start onboarding process**, select the operating system for the device.
4. Under **Connectivity type**, select either **Streamlined** or **Standard**. (See [prerequisites for streamlined connectivity](configure-device-connectivity#prerequisites).)
5. Under **Deployment method**, select an option. Then download the onboarding package (and installation package, as appropriate). For more information, see the following articles:

    - [Onboard client devices running Windows or macOS to Microsoft Defender for Endpoint](onboard-client)
    - [Onboard servers through Microsoft Defender for Endpoint's onboarding experience](onboard-server)

## Video: Device onboarding

The following video provides a quick overview of the onboarding process and the different tools and methods:

## Deploy using a ring-based approach

### New deployments

A ring-based approach is a method of identifying a set of endpoints to onboard and verifying that certain criteria are met before proceeding to deploy the service to a larger set of devices. You can define the exit criteria for each ring and ensure that they're satisfied before moving on to the next ring. Adopting a ring-based deployment helps reduce potential issues that could arise while rolling out the service.

This table provides an example of the deployment rings you might use:

| Deployment ring | Description |
| --- | --- |
| Evaluate | Ring 1: Identify 50 devices to onboard to the service for testing. |
| Pilot | Ring 2: Identify and onboard the next 50-100 endpoints in a production environment. Microsoft Defender for Endpoint supports various endpoints that you can onboard to the service. For more information, see [Select deployment method](deployment-strategy#step-2-select-your-deployment-method). |
| Full deployment | Ring 3: Roll out service to the rest of environment in larger increments. For more information, see [Get started with your Microsoft Defender for Endpoint deployment](mde-planning-guide). |

### Exit criteria

An example set of exit criteria for each ring can include:

- Devices show up in the device inventory list
- Alerts appear in dashboard
- [Run a detection test](run-detection-test)
- [Run a simulated attack on a device](attack-simulations)

## Existing deployments

### Windows endpoints

For Windows and/or Windows Servers, you select several machines to test ahead of time (before patch Tuesday) by using the **Security Update Validation program (SUVP)**.

For more information, see:

- [What is the Security Update Validation Program](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/what-is-the-security-update-validation-program/ba-p/275767)
- [Software Update Validation Program and Microsoft Malware Protection Center Establishment - TwC Interactive Timeline Part 4](https://www.microsoft.com/security/blog/2012/03/28/software-update-validation-program-and-microsoft-malware-protection-center-establishment-twc-interactive-timeline-part-4/)

### Non-Windows endpoints

With macOS and Linux, you could take a couple of systems and run in the Beta channel.

Note

Ideally at least one security admin and one developer so that you are able to find compatibility, performance and reliability issues before the build makes it into the Current channel.

The choice of the channel determines the type and frequency of updates that are offered to your device. Devices in Beta are the first ones to receive updates and new features, followed later by Preview and lastly by Current.

[![The insider rings.](media/insider-rings.png)](media/insider-rings.png#lightbox)

In order to preview new features and provide early feedback, it's recommended that you configure some devices in your enterprise to use either Beta or Preview.

Warning

Switching the channel after the initial installation requires the product to be reinstalled. To switch the product channel: uninstall the existing package, re-configure your device to use the new channel, and follow the steps in this document to install the package from the new location.

## Example deployments

To provide some guidance on your deployments, in this section we guide you through using two deployment tools to onboard endpoints.

The tools in the example deployments are:

- [Onboarding using Microsoft Configuration Manager](onboarding-endpoint-configuration-manager)
- [Deploy endpoint detection and response policy with Intune](/en-us/intune/device-configuration/endpoint-security/deploy-edr).

For some additional information and guidance, check out the [PDF](https://download.microsoft.com/download/5/6/0/5609001f-b8ae-412f-89eb-643976f6b79c/mde-deployment-strategy.pdf) or [Visio](https://download.microsoft.com/download/5/6/0/5609001f-b8ae-412f-89eb-643976f6b79c/mde-deployment-strategy.vsdx) to see the various paths for deploying Defender for Endpoint.

The example deployments will guide you on configuring some of the Defender for Endpoint capabilities, but you'll find more detailed information on configuring Defender for Endpoint capabilities in the next step.