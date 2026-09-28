---
layout: Conceptual
title: How do I pilot and deploy Microsoft Defender for Endpoint? - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/pilot-deploy-defender-endpoint
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: How to pilot and deploy Microsoft Defender for Endpoint in your production Microsoft 365 tenant.
search.appverid: met150
ms.service: defender-xdr
f1.keywords:
- NOCSH
ms.author: guywild
author: guywi-ms
ms.date: 2025-06-19T00:00:00.0000000Z
ms.localizationpriority: medium
audience: ITPro
ms.collection:
- m365-security
- m365solution-scenario
- m365solution-evalutatemtp
- zerotrust-solution
- highpri
- tier1
ms.topic: install-set-up-deploy
locale: en-us
document_id: e1d2a427-344c-c483-3da0-6a1a0da406ce
document_version_independent_id: e1d2a427-344c-c483-3da0-6a1a0da406ce
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/pilot-deploy-defender-endpoint.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: pilot-deploy-defender-endpoint
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/pilot-deploy-defender-endpoint.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 8134b60f-c0f9-5a50-d638-0be75acd2f1c
---

# How do I pilot and deploy Microsoft Defender for Endpoint? - Microsoft Defender XDR | Microsoft Learn

This article provides a workflow for piloting and deploying Microsoft Defender for Endpoint in your organization. You can use these recommendations to onboard Microsoft Defender for Endpoint as an individual cybersecurity tool or as part of an end-to-end solution with Microsoft Defender.

This article assumes you have a production Microsoft 365 tenant and are piloting and deploying Microsoft Defender for Endpoint in this environment. This practice will maintain any settings and customizations you configure during your pilot for your full deployment.

Defender for Endpoint contributes to a Zero Trust architecture by helping to prevent or reduce business damage from a breach. For more information, see the [Prevent or reduce business damage from a breach](/en-us/security/zero-trust/adopt/prevent-reduce-business-damage-breach) business scenario in the Microsoft Zero Trust adoption framework.

Important

If you want to run multiple security solutions side by side, see [Considerations for performance, configuration, and support](/en-us/defender-endpoint/mde-side-by-side).

You might have already configured mutual security exclusions for devices onboarded to Microsoft Defender for Endpoint. If you still need to set mutual exclusions to avoid conflicts, see [Add Microsoft Defender for Endpoint to the exclusion list for your existing solution](/en-us/defender-endpoint/switch-to-mde-phase-2#step-2-add-microsoft-defender-for-endpoint-to-the-exclusion-list-for-your-existing-solution).

## End-to-end deployment for Microsoft Defender XDR

This is article 4 of 6 in a series to help you deploy the components of Microsoft Defender XDR, including investigating and responding to incidents.

[![A diagram that shows Microsoft Defender for Endpoint in the pilot and deploy Microsoft Defender XDR process.](media/eval-defender-xdr/defender-xdr-pilot-deploy-flow-endpoint.svg)](media/eval-defender-xdr/defender-xdr-pilot-deploy-flow-endpoint.svg#lightbox)

The articles in this series correspond to the following phases of end-to-end deployment:

| Phase | Link |
| --- | --- |
| A. Start the pilot | [Start the pilot](pilot-deploy-overview#start-the-pilot) |
| B. Pilot and deploy Microsoft Defender components | - [Pilot and deploy Defender for Identity](pilot-deploy-defender-identity) - [Pilot and deploy Defender for Office 365](pilot-deploy-defender-office-365) - **Pilot and deploy Defender for Endpoint** (this article)  - [Pilot and deploy Microsoft Defender for Cloud Apps](pilot-deploy-defender-cloud-apps) |
| C. Investigate and respond to threats | [Practice incident investigation and response](pilot-deploy-investigate-respond) |

## Pilot and deploy workflow for Defender for Endpoint

The following diagram illustrates a common process to deploy a product or service in an IT environment.

[![Diagram of the pilot, evaluate, and full deployment adoption phases.](media/eval-defender-xdr/adoption-phases.svg)](media/eval-defender-xdr/adoption-phases.svg#lightbox)

You start by evaluating the product or service and how it will work within your organization. Then, you pilot the product or service with a suitably small subset of your production infrastructure for testing, learning, and customization. Then, gradually increase the scope of the deployment until your entire infrastructure or organization is covered.

Here is the workflow for piloting and deploying Defender for Endpoint in your production environment.

[![A diagram that shows the steps to pilot and deploy Microsoft Defender for Endpoint.](media/eval-defender-xdr/defender-endpoint-pilot-deploy-steps.svg)](media/eval-defender-xdr/defender-endpoint-pilot-deploy-steps.svg#lightbox)

Follow these steps:

1. Check license state
2. Onboard endpoints using any of the supported management tools
3. Verify pilot group
4. Try out capabilities

Here are the recommended steps for each deployment stage.

| Deployment stage | Description |
| --- | --- |
| Evaluate | Perform product evaluation for Defender for Endpoint. |
| Pilot | Perform Steps 1-4 for a pilot group. |
| Full deployment | Configure the pilot group in Step 3 or add groups to expand beyond the pilot and eventually include all of your devices. |

### Protecting your organization from hackers

Defender for Identity provides powerful protection on its own. However, when combined with the other capabilities of Microsoft Defender, Defender for Endpoint provides data into the shared signals which together help stop attacks.

Here's an example of a cyber-attack and how the components of Microsoft Defender XDR help detect and mitigate it.

[![A diagram that shows how Microsoft Defender XDR stops a threat chain.](media/eval-defender-xdr/m365-defender-eval-threat-chain.svg)](media/eval-defender-xdr/m365-defender-eval-threat-chain.svg#lightbox)

Defender for Endpoint detects device and network vulnerabilities that might otherwise be exploited for devices managed by your organization.

Microsoft Defender correlates the signals from all the Microsoft Defender components to provide the full attack story.

## Defender for Endpoint architecture

The following diagram illustrates Microsoft Defender for Endpoint architecture and integrations.

[![A diagram that shows the steps for adding Microsoft Defender for Endpoint to the Microsoft Defender XDR evaluation environment.](media/eval-defender-xdr/m365-defender-endpoint-architecture.svg)](media/eval-defender-xdr/m365-defender-endpoint-architecture.svg#lightbox)

This table describes the illustration.

| Call-out | Description |
| --- | --- |
| 1 | Devices are on-boarded through one of the supported management tools. |
| 2 | On-boarded devices provide and respond to Microsoft Defender for Endpoint signal data. |
| 3 | Managed devices are joined and/or enrolled in Microsoft Entra ID. |
| 4 | Domain-joined Windows devices are synchronized to Microsoft Entra ID using Microsoft Entra Connect. |
| 5 | Microsoft Defender for Endpoint alerts, investigations, and responses are managed in Microsoft Defender. |

Tip

Microsoft Defender for Endpoint also comes with an in-product evaluation lab where you can add pre-configured devices and run simulations to evaluate the capabilities of the platform. The lab comes with a simplified set-up experience that can help quickly demonstrate the value of Microsoft Defender for Endpoint including guidance for many features like advanced hunting and threat analytics. For more information, see [Evaluate capabilities](/en-us/defender-endpoint/evaluation-lab). The main difference between the guidance provided in this article and the evaluation lab is the evaluation environment uses production devices whereas the evaluation lab uses non-production devices.

## Step 1: Check license state

You'll first need to check the license state to verify that it was properly provisioned. You can do this through the admin center or through the **Microsoft Azure portal**.

1. To view your licenses, go to the **Microsoft Azure portal** and navigate to the [Microsoft Azure portal license section](https://portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Products).

    [![Screenshot of the Azure Licensing page in the Microsoft Defender portal.](media/pilot-deploy-defender-endpoint/atp-licensing-azure-portal.png)](media/pilot-deploy-defender-endpoint/atp-licensing-azure-portal.png#lightbox)
2. Alternately, in the admin center, navigate to **Billing** &gt; **Subscriptions**.

    On the screen, you'll see all the provisioned licenses and their current **Status**.

    [![Screenshot of the Billing licenses page in the Microsoft Azure portal.](media/pilot-deploy-defender-endpoint/atp-billing-subscriptions.png)](media/pilot-deploy-defender-endpoint/atp-billing-subscriptions.png#lightbox)

## Step 2: Onboard endpoints using any of the supported management tools

After verifying that the license state has been provisioned properly, you can start onboarding devices to the service.

For the purpose of evaluating Microsoft Defender for Endpoint, we recommend choosing a couple of Windows devices to conduct the evaluation on.

You can choose to use any of the supported management tools, but Intune provides optimal integration. For more information, see [Configure Microsoft Defender for Endpoint in Microsoft Intune](/en-us/mem/intune/protect/advanced-threat-protection-configure#enable-microsoft-defender-for-endpoint-in-intune).

The [Plan deployment](/en-us/defender-endpoint/deployment-strategy) topic outlines the general steps you need to take to deploy Defender for Endpoint.

Watch this video for a quick overview of the onboarding process and learn about the available tools and methods.

### Onboarding tool options

The following table lists the available tools based on the endpoint that you need to onboard.

| Endpoint | Tool options |
| --- | --- |
| **Windows** | - [Local script (up to 10 devices)](/en-us/defender-endpoint/configure-endpoints-script)- [Group Policy](/en-us/defender-endpoint/configure-endpoints-gp)- [Microsoft Intune / Mobile Device Manager](/en-us/defender-endpoint/configure-endpoints-mdm)- [Microsoft Endpoint Configuration Manager](/en-us/defender-endpoint/configure-endpoints-sccm)- [VDI scripts](/en-us/defender-endpoint/configure-endpoints-vdi) |
| **macOS** | - [Local scripts](/en-us/defender-endpoint/mac-install-manually)- [Microsoft Intune](/en-us/defender-endpoint/mac-install-with-intune)- [JAMF Pro](/en-us/defender-endpoint/mac-install-with-jamf)- [Mobile Device Management](/en-us/defender-endpoint/mac-install-with-other-mdm) |
| **iOS** | [App-based](/en-us/defender-endpoint/ios-install) |
| **Android** | [Microsoft Intune](/en-us/intune/intune-service/protect/microsoft-defender-deploy-android) |

When you pilot Microsoft Defender for Endpoint, you may choose to onboard a few devices to the service before onboarding your entire organization.

You can then try out capabilities that are available such as running attack simulations and seeing how Defender for Endpoint surfaces malicious activities and enables you to conduct an efficient response.

## Step 3: Verify pilot group

After completing the onboarding steps outlined in the Enable evaluation section, you should see the devices in the Device inventory list approximately after an hour.

When you see your onboarded devices you can then proceed with trying out capabilities.

## Step 4: Try out capabilities

Now that you've completed onboarding some devices and verified that they are reporting to the service, familiarize yourself with the product by trying out the powerful capabilities that are available right out of the box.

During the pilot, you can easily get started with trying out some of the features to see the product in action without going through complex configuration steps.

Let's start by checking out the dashboards.

### View the device inventory

The device inventory is where you'll see the list of endpoints, network devices, and IoT devices in your network. Not only does it provide you with a view of the devices in your network, but it also gives you in-depth information about them such as domain, risk level, OS platform, and other details for easy identification of devices most at risk.

### View the Microsoft Defender Vulnerability Management dashboard

Defender Vulnerability Management helps you focus on the weaknesses that pose the most urgent and the highest risk to the organization. From the dashboard, get a high-level view of the organization exposure score, Microsoft Secure Score for Devices, device exposure distribution, top security recommendations, top vulnerable software, top remediation activities, and top exposed device data.

### Run a simulation

Microsoft Defender for Endpoint comes with ["Do It Yourself" attack scenarios](https://securitycenter.windows.com/tutorials) that you can run on your pilot devices. Each document includes OS and application requirements as well as detailed instructions that are specific to an attack scenario. These scripts are safe, documented, and easy to use. These scenarios will reflect Defender for Endpoint capabilities and walk you through investigation experience.

To run any of the provided simulations, you need at least [one onboarded device](/en-us/defender-endpoint/onboard-configure).

1. In **Help** &gt; **Simulations & tutorials**, select which of the available attack scenarios you would like to simulate:

    - **Scenario 1: Document drops backdoor** - simulates delivery of a socially engineered lure document. The document launches a specially crafted backdoor that gives attackers control.
    - **Scenario 2: PowerShell script in fileless attack** - simulates a fileless attack that relies on PowerShell, showcasing attack surface reduction and device learning detection of malicious memory activity.
    - **Scenario 3: Automated incident response** - triggers automated investigation, which automatically hunts for and remediates breach artifacts to scale your incident response capacity.
2. Download and read the corresponding walkthrough document provided with your selected scenario.
3. Download the simulation file or copy the simulation script by navigating to **Help** &gt; **Simulations & tutorials**. You can choose to download the file or script on the test device but it's not mandatory.
4. Run the simulation file or script on the test device as instructed in the walkthrough document.

Note

Simulation files or scripts mimic attack activity but are actually benign and will not harm or compromise the test device.

## SIEM integration

You can integrate Defender for Endpoint with Microsoft Sentinel or a generic security information and event management (SIEM) service to enable centralized monitoring of alerts and activities from connected apps. With Microsoft Sentinel, you can more comprehensively analyze security events across your organization and build playbooks for effective and immediate response.

[![A diagram that shows the architecture for Microsoft Defender for Endpoint with SIEM integration.](media/eval-defender-xdr/defender-endpoint-siem-integration.svg)](media/eval-defender-xdr/defender-endpoint-siem-integration.svg#lightbox)

Microsoft Sentinel includes a Defender for Endpoint connector. For more information, see [Microsoft Defender for Endpoint connector for Microsoft Sentinel](/en-us/azure/sentinel/data-connectors/microsoft-defender-for-endpoint).

For information about integration with generic SIEM systems, see [Enable SIEM integration in Microsoft Defender for Endpoint](/en-us/defender-endpoint/configure-siem).