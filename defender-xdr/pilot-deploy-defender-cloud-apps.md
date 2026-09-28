---
layout: Conceptual
title: How do I pilot and deploy Microsoft Defender for Cloud Apps? - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/pilot-deploy-defender-cloud-apps
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to pilot and deploy Microsoft Defender for Cloud Apps as part of Microsoft Defender XDR to enhance your organization's security posture.
search.appverid: met150
ms.service: defender-xdr
f1.keywords:
- NOCSH
ms.author: abbyweisberg
author: AbbyMSFT
ms.reviewer: maelgami
ms.date: 2025-03-14T00:00:00.0000000Z
ms.localizationpriority: medium
audience: ITPro
ms.collection:
- m365-security
- m365solution-scenario
- m365solution-evalutatemtp
- zerotrust-solution
- highpri
- tier1
ms.topic: concept-article
locale: en-us
document_id: c091bbb6-1fc4-ca7e-a33c-96f8d1d2ec1e
document_version_independent_id: c091bbb6-1fc4-ca7e-a33c-96f8d1d2ec1e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/pilot-deploy-defender-cloud-apps.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: pilot-deploy-defender-cloud-apps
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/pilot-deploy-defender-cloud-apps.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: f543f160-1b2d-2b52-b571-21d093843453
---

# How do I pilot and deploy Microsoft Defender for Cloud Apps? - Microsoft Defender XDR | Microsoft Learn

This article provides a workflow for piloting and deploying Microsoft Defender for Cloud Apps in your organization. Use these recommendations to onboard Microsoft Defender for Cloud Apps as part of an end-to-end solution with Microsoft Defender.

This article assumes you have a production Microsoft 365 tenant and are piloting and deploying Microsoft Defender for Cloud Apps in this environment. This practice will maintain any settings and customizations you configure during your pilot for your [full deployment](/en-us/defender-cloud-apps/get-started).

Defender for Office 365 contributes to a Zero Trust architecture by helping to prevent or reduce business damage from a breach. For more information, see the [Prevent or reduce business damage from a breach](/en-us/security/zero-trust/adopt/prevent-reduce-business-damage-breach) business scenario in the Microsoft Zero Trust adoption framework.

## End-to-end deployment for Microsoft Defender

This is article 5 of 6 in a series to help you deploy the components of Microsoft Defender XDR, including investigating and responding to incidents.

[![A diagram that shows Microsoft Defender for Cloud Apps in the pilot and deploy Microsoft Defender XDR process.](media/eval-defender-xdr/defender-xdr-pilot-deploy-flow-cloud-apps.svg)](media/eval-defender-xdr/defender-xdr-pilot-deploy-flow-cloud-apps.svg#lightbox)

The articles in this series correspond to the following phases of end-to-end deployment:

| Phase | Link |
| --- | --- |
| A. Start the pilot | [Start the pilot](pilot-deploy-overview#start-the-pilot) |
| B. Pilot and deploy Microsoft Defender components | - [Pilot and deploy Defender for Identity](pilot-deploy-defender-identity) - [Pilot and deploy Defender for Office 365](pilot-deploy-defender-office-365) - [Pilot and deploy Defender for Endpoint](pilot-deploy-defender-endpoint) - **Pilot and deploy Microsoft Defender for Cloud Apps** (this article) |
| C. Investigate and respond to threats | [Practice incident investigation and response](pilot-deploy-investigate-respond) |

## Pilot and deploy workflow for Defender for Cloud Apps

The following diagram illustrates a common process to deploy a product or service in an IT environment.

[![A diagram of the pilot, evaluate, and full deployment adoption phases.](media/eval-defender-xdr/adoption-phases.svg)](media/eval-defender-xdr/adoption-phases.svg#lightbox)

You start by evaluating the product or service and how it will work within your organization. Then, you pilot the product or service with a suitably small subset of your production infrastructure for testing, learning, and customization. Then, gradually increase the scope of the deployment until your entire infrastructure or organization is covered.

Here is the workflow for piloting and deploying Defender for Cloud Apps in your production environment.

[![A diagram that shows the pilot and deploy workflow for Microsoft Defender for Cloud Apps.](media/eval-defender-xdr/defender-cloud-apps-pilot-deploy-steps.svg)](media/eval-defender-xdr/defender-cloud-apps-pilot-deploy-steps.svg#lightbox)

Follow these steps:

1. Connect to Defender for Cloud Apps
2. Integrate with Microsoft Defender for Endpoint
3. Deploy the log collector on your firewalls and other proxies
4. Create a pilot group
5. Discover and manage cloud apps
6. Configure conditional access app control
7. Apply session policies to cloud apps
8. Try out additional capabilities

Here are the recommended steps for each deployment stage.

| Deployment stage | Description |
| --- | --- |
| Evaluate | Perform product evaluation for Defender for Cloud Apps. |
| Pilot | Perform Steps 1-4 and then 5-8 for a suitable subset of cloud apps in your production environment. |
| Full deployment | Perform Steps 5-8 for your remaining cloud apps, adjusting the scoping for pilot user groups or adding user groups to expand beyond the pilot and include all of your user accounts. |

### Protecting your organization from hackers

Defender for Cloud Apps provides powerful protection on its own. However, when combined with the other capabilities of Microsoft Defender, Defender for Cloud Apps provides data into the shared signals which together help stop attacks.

Here's an example of a cyber-attack and how the components of Microsoft Defender XDR help detect and mitigate it.

[![A diagram that shows how Microsoft Defender XDR stops a threat chain.](media/eval-defender-xdr/m365-defender-eval-threat-chain.svg)](media/eval-defender-xdr/m365-defender-eval-threat-chain.svg#lightbox)

Defender for Cloud Apps detects anomalous behavior like impossible-travel, credential access, and unusual download, file share, or mail forwarding activity and displays these behaviors in the Defender for Cloud Apps. Defender for Cloud Apps also helps prevent lateral movement by hackers and exfiltration of sensitive data.

Microsoft Defender correlates the signals from all the Microsoft Defender components to provide the full attack story.

### Defender for Cloud Apps role as a CASB and more

A cloud access security broker (CASB) acts as a gatekeeper to broker access in real time between your enterprise users and cloud resources they use, wherever your users are located and regardless of the device they are using. Software as a service (SaaS) apps are ubiquitous across hybrid work environments, and protecting SaaS apps and the important data they store is a big challenge for organizations.

The rise in app usage, combined with employees accessing company resources outside of the corporate perimeter has also introduced new attack vectors. To combat these attacks effectively, security teams need an approach that protects their data within cloud apps beyond the traditional scope of cloud access security brokers (CASBs).

Microsoft Defender for Cloud Apps delivers full protection for SaaS applications, helping you monitor and protect your cloud app data across the following feature areas:

- **Fundamental cloud access security broker (CASB) functionality**, such as Shadow IT discovery, visibility into cloud app usage, protection against app-based threats from anywhere in the cloud, and information protection and compliance assessments.
- **SaaS Security Posture Management (SSPM) features**, enabling security teams to improve the organization’s security posture
- **Advanced threat protection**, as part of Microsoft's extended detection and response (XDR) solution, enabling powerful correlation of signal and visibility across the full kill chain of advanced attacks
- **App-to-app protection**, extending the core threat scenarios to OAuth-enabled apps that have permissions and privileges to critical data and resources.

## Cloud app discovery methods

Without Defender for Cloud Apps, cloud apps that are used by your organization are unmanaged and unprotected. To discover cloud apps used in your environment, you can implement one or both of the following methods:

- Get up and running quickly with Cloud Discovery by integrating with Microsoft Defender for Endpoint. This native integration enables you to immediately start collecting data on cloud traffic across your Windows 10 and Windows 11 devices, on and off your network.
- To discover all cloud apps accessed by all devices connected to your network, deploy the Defender for Cloud Apps log collector on your firewalls and other proxies. This deployment helps collect data from your endpoints and sends it to Defender for Cloud Apps for analysis. Defender for Cloud Apps natively integrates with some third-party proxies for even more capabilities.

This article includes guidance for both methods.

## Step 1. Connect to Defender for Cloud Apps

To verify licensing and to connect to Defender for Cloud Apps, see [Quickstart: Get started with Microsoft Defender for Cloud Apps](/en-us/cloud-app-security/getting-started-with-cloud-app-security).

If you're not immediately able to connect to the portal, you might need to add the IP address to the allow list of your firewall. For more information, see [Basic setup for Defender for Cloud Apps](/en-us/defender-cloud-apps/general-setup).

If you're still having trouble, review [Network requirements](/en-us/defender-cloud-apps/network-requirements).

## Step 2: Integrate with Microsoft Defender for Endpoint

Microsoft Defender for Cloud Apps integrates with Microsoft Defender for Endpoint natively. The integration simplifies roll out of Cloud Discovery, extends Cloud Discovery capabilities beyond your corporate network and enables device-based investigation. This integration reveals cloud apps and services being accessed from IT-managed Windows 10 and Windows 11 devices.

If you've already set up Microsoft Defender for Endpoint, configuring integration with Defender for Cloud Apps is a toggle in Microsoft Defender. After integration is turned on, you can return to Defender for Cloud Apps and view rich data in the Cloud Discovery Dashboard.

To accomplish these tasks, see [Integrate Microsoft Defender for Endpoint with Microsoft Defender for Cloud Apps](/en-us/defender-cloud-apps/mde-integration).

## Step 3: Deploy the Defender for Cloud Apps log collector on your firewalls and other proxies

- **For coverage on all devices connected to your network**, deploy the Defender for Cloud Apps log collector on your firewalls and other proxies to collect data from your endpoints and send it to Defender for Cloud Apps for analysis. For more information, see [Configure automatic log upload for continuous reports](/en-us/defender-cloud-apps/discovery-docker).
- **Defender for Cloud Apps provides built-in app connectors for popular cloud apps**. These connectors use the APIs of app providers to enable greater visibility and control over how these apps are used in your organization. For more information, see [Connect apps to get visibility and control with Microsoft Defender for Cloud Apps](/en-us/defender-cloud-apps/enable-instant-visibility-protection-and-governance-actions-for-your-apps).
- **If you're using one of the following Secure Web Gateways (SWG)**, Defender for Cloud Apps provides seamless deployment and integration:

    - [Zscaler](/en-us/defender-cloud-apps/zscaler-integration)
    - [iboss](/en-us/defender-cloud-apps/iboss-integration)
    - [Corrata](/en-us/defender-cloud-apps/corrata-integration)
    - [Menlo Security](/en-us/defender-cloud-apps/menlo-integration)
    - [Open Systems](/en-us/defender-cloud-apps/open-systems-integration)

For more information, see [Cloud app discovery overview](/en-us/defender-cloud-apps/set-up-cloud-discovery).

## Step 4. Create a pilot group — Scope your pilot deployment to certain user groups

Microsoft Defender for Cloud Apps enables you to scope your deployment. Scoping allows you to select certain user groups to be monitored for apps or excluded from monitoring. You can include or exclude user groups.

For more information, see [Scope your deployment to specific users or user groups](/en-us/defender-cloud-apps/scoped-deployment).

## Step 5. Discover and manage cloud apps

For Defender for Cloud Apps to provide the maximum amount of protection, you must discover all the cloud apps in your organization and manage how they are used.

### Discover cloud apps

The first step to managing the use of cloud apps is to discover which cloud apps are used by your organization. The following diagram illustrates how cloud discovery works with Defender for Cloud Apps.

[![A diagram that shows the architecture for Microsoft Defender for Cloud Apps with cloud discovery.](media/eval-defender-xdr/m365-defender-mcas-architecture-b.svg)](media/eval-defender-xdr/m365-defender-mcas-architecture-b.svg#lightbox)

In this illustration, there are two methods that can be used to monitor network traffic and discover cloud apps that are being used by your organization.

1. Cloud App Discovery integrates with Microsoft Defender for Endpoint natively. Defender for Endpoint reports cloud apps and services being accessed from IT-managed Windows 10 and Windows 11 devices.
2. For coverage on all devices connected to a network, you install the Defender for Cloud Apps log collector on firewalls and other proxies to collect data from endpoints. The collector sends this data to Defender for Cloud Apps for analysis.

### View the Cloud Discovery dashboard to see what apps are being used in your organization

The **Cloud discovery dashboard** is designed to give you more insight into how cloud apps are being used in your organization. It provides an at-a-glance overview of what kinds of apps are being used, your open alerts, and the risk levels of apps in your organization.

For more information, see [View discovered apps with the Cloud discovery dashboard](/en-us/defender-cloud-apps/discovered-apps).

### Manage cloud apps

After you discover cloud apps and analyze how these apps are used by your organization, you can begin managing cloud apps that you choose.

[![A diagram that shows the architecture for Microsoft Defender for Cloud Apps for managing cloud apps.](media/eval-defender-xdr/m365-defender-mcas-architecture-c.svg)](media/eval-defender-xdr/m365-defender-mcas-architecture-c.svg#lightbox)

In this illustration, some apps are sanctioned for use. Sanctioning is a simple way of beginning to manage apps. For more information, see [Govern discovered apps](/en-us/defender-cloud-apps/governance-discovery).

## Step 6. Configure conditional access app control

One of the most powerful protections you can configure is Conditional access app control. This protection requires integration with Microsoft Entra ID. It allows you to apply Conditional Access policies, including related policies (like requiring healthy devices), to cloud apps you've sanctioned.

You might already have SaaS apps added to your Microsoft Entra tenant to enforce multifactor authentication and other conditional access policies. Microsoft Defender for Cloud Apps natively integrates with Microsoft Entra ID. All you must do is configure a policy in Microsoft Entra ID to use conditional access app control in Defender for Cloud Apps. This routes network traffic for these managed SaaS apps through Defender for Cloud Apps as a proxy, which allows Defender for Cloud Apps to monitor this traffic and to apply session controls.

[![A diagram that shows the architecture for Defender for Cloud Apps conditional access app control.](media/eval-defender-xdr/m365-defender-mcas-architecture-e.svg)](media/eval-defender-xdr/m365-defender-mcas-architecture-e.svg#lightbox)

In this illustration:

- SaaS apps are integrated with the Microsoft Entra tenant. This integration allows Microsoft Entra ID to enforce conditional access policies, including multifactor authentication.
- A policy is added to Microsoft Entra ID to direct traffic for SaaS apps to Defender for Cloud Apps. The policy specifies which SaaS apps to apply this policy to. After Microsoft Entra ID enforces any conditional access policies that apply to these SaaS apps, Microsoft Entra ID then directs (proxies) the session traffic through Defender for Cloud Apps.
- Defender for Cloud Apps monitors this traffic and applies any session control policies that have been configured by administrators.

You might have discovered and sanctioned cloud apps using Defender for Cloud Apps that have not been added to Microsoft Entra ID. You can take advantage of conditional access app control by adding these cloud apps to your Microsoft Entra tenant and the scope of your conditional access rules.

The first step in using Microsoft Defender for Cloud Apps to manage SaaS apps is to discover these apps and then add them to your Microsoft Entra tenant. If you need help with discovery, see [Discover and manage SaaS apps in your network](/en-us/defender-cloud-apps/tutorial-shadow-it). After you've discovered apps, [add these apps to your Microsoft Entra tenant](/en-us/azure/active-directory/manage-apps/add-application-portal).

You can begin to manage these apps with the following tasks:

1. In Microsoft Entra ID, create a new conditional access policy and configure it to **Use conditional access app control.** This configuration helps to redirect the request to Defender for Cloud Apps. You can create one policy and add all SaaS apps to this policy.
2. Next, in Defender for Cloud Apps, create session policies. Create one policy for each control you want to apply. For more information, including supported apps and clients, see [Create Microsoft Defender for Cloud Apps session policies](/en-us/defender-cloud-apps/proxy-intro-aad).

For sample policies, see [Recommended Microsoft Defender for Cloud Apps policies for SaaS apps](/en-us/security/zero-trust/zero-trust-identity-device-access-policies-mcas-saas). These policies build on a set of [common identity and device access policies](/en-us/security/zero-trust/zero-trust-identity-device-access-policies-overview) that are recommended as a starting point for all customers.

## Step 7. Apply session policies to cloud apps

Once you have session policies configured, apply them to your cloud apps to provide controlled access to those apps.

[![A diagram that shows how cloud apps are accessed via session control policies with Defender for Cloud Apps.](media/eval-defender-xdr/m365-defender-mcas-architecture-d.svg)](media/eval-defender-xdr/m365-defender-office-architecture.svg#lightbox)

In the illustration:

- Access to sanctioned cloud apps from users and devices in your organization is routed through Defender for Cloud Apps where session policies can be applied to specific apps.
- Cloud apps that you have not sanctioned or explicitly unsanctioned are not affected.

Session policies allow you to apply parameters to how cloud apps are used by your organization. For example, if your organization is using Salesforce, you can configure a session policy that allows only managed devices to access your organization's data at Salesforce. A simpler example could be configuring a policy to monitor traffic from unmanaged devices so you can analyze the risk of this traffic before applying stricter policies.

For more information, see [Create Microsoft Defender for Cloud Apps session policies](/en-us/defender-cloud-apps/session-policy-aad).

## Step 8. Try out additional capabilities

Use these Defender for Cloud Apps articles to help you discover risk and protect your environment:

- [Detect suspicious user activity](/en-us/defender-cloud-apps/tutorial-suspicious-activity)
- [Investigate risky users](/en-us/defender-cloud-apps/tutorial-ueba)
- [Investigate risky OAuth apps](/en-us/defender-cloud-apps/investigate-risky-oauth)
- [Discover and protect sensitive information](/en-us/defender-cloud-apps/tutorial-dlp)
- [Protect any app in your organization in real time](/en-us/defender-cloud-apps/tutorial-proxy)
- [Block downloads of sensitive information](/en-us/defender-cloud-apps/use-case-proxy-block-session-aad)
- [Protect your files with admin quarantine](/en-us/defender-cloud-apps/use-case-admin-quarantine)
- [Require step-up authentication upon risky action](/en-us/defender-cloud-apps/tutorial-step-up-authentication)

For more information on advanced hunting in Microsoft Defender for Cloud Apps data, see this [video](https://learn-video.azurefd.net/vod/player?id=ffdedc73-6edf-45a9-8c90-566296e8d4ec).

## SIEM integration

You can integrate Defender for Cloud Apps with Microsoft Sentinel for unified security operations in the [Defender portal](/en-us/defender-xdr/isoc-overview), or with a generic security information and event management (SIEM) service to enable centralized monitoring of alerts and activities from connected apps. With Microsoft Sentinel, you can more comprehensively analyze security events across your organization and build playbooks for effective and immediate response.

The Defender portal supports unified security operations with Microsoft Sentinel, bringing signals from Defender, including Defender for Cloud Apps, to Microsoft Sentinel.

For more information, see:

- [Connect Microsoft Sentinel to the Microsoft Defender portal](/en-us/azure/sentinel/microsoft-sentinel-onboard)
- [Microsoft Sentinel integration](/en-us/defender-cloud-apps/siem-sentinel)
- [Generic SIEM integration](/en-us/defender-cloud-apps/siem)