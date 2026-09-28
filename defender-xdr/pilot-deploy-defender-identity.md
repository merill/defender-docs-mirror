---
layout: Conceptual
title: How do I pilot and deploy Microsoft Defender for Identity - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/pilot-deploy-defender-identity
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to pilot and deploy Microsoft Defender for Identity as part of Microsoft Defender XDR to enhance your organization's security posture.
search.appverid: met150
ms.service: defender-xdr
f1.keywords:
- NOCSH
ms.author: guywild
author: guywi-ms
ms.date: 2025-01-12T00:00:00.0000000Z
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
document_id: fd97b079-4331-ad31-825d-99344eb9e1bb
document_version_independent_id: fd97b079-4331-ad31-825d-99344eb9e1bb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/pilot-deploy-defender-identity.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: pilot-deploy-defender-identity
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/pilot-deploy-defender-identity.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: a470e027-4db7-40b5-f97e-375a360a2f90
---

# How do I pilot and deploy Microsoft Defender for Identity - Microsoft Defender XDR | Microsoft Learn

This article provides a workflow for piloting and deploying Microsoft Defender for Identity in your organization. Use these recommendations to onboard Microsoft Defender for Identity as part of an end-to-end solution with Microsoft Defender.

This article assumes you have a production Microsoft 365 tenant and are piloting and deploying Microsoft Defender for Identity in this environment. This practice will maintain any settings and customizations you configure during your pilot for your [full deployment](/en-us/defender-for-identity/deploy/deploy-defender-identity).

Defender for Identity contributes to a Zero Trust architecture by helping to prevent or reduce business damage from a breach. For more information, see the [Prevent or reduce business damage from a breach](/en-us/security/zero-trust/adopt/prevent-reduce-business-damage-breach) business scenario in the Microsoft Zero Trust adoption framework.

## End-to-end deployment for Microsoft Defender

This is article 2 of 6 in a series to help you deploy the components of Microsoft Defender XDR, including investigating and responding to incidents.

[![A diagram that shows Microsoft Defender for Identity in the pilot and deploy Microsoft Defender XDR process.](media/eval-defender-xdr/defender-xdr-pilot-deploy-flow-identity.svg)](media/eval-defender-xdr/defender-xdr-pilot-deploy-flow-identity.svg#lightbox)

The articles in this series correspond to the following phases of end-to-end deployment:

| Phase | Link |
| --- | --- |
| A. Start the pilot | [Start the pilot](pilot-deploy-overview#start-the-pilot) |
| B. Pilot and deploy Microsoft Defender components | - **Pilot and deploy Defender for Identity** (this article)  - [Pilot and deploy Defender for Office 365](pilot-deploy-defender-office-365) - [Pilot and deploy Defender for Endpoint](pilot-deploy-defender-endpoint) - [Pilot and deploy Microsoft Defender for Cloud Apps](pilot-deploy-defender-cloud-apps) |
| C. Investigate and respond to threats | [Practice incident investigation and response](pilot-deploy-investigate-respond) |

## Pilot and deploy workflow for Defender for Identity

The following diagram illustrates a common process to deploy a product or service in an IT environment.

[![Diagram of the pilot, evaluate, and full deployment adoption phases.](media/eval-defender-xdr/adoption-phases.svg)](media/eval-defender-xdr/adoption-phases.svg#lightbox)

You start by evaluating the product or service and how it will work within your organization. Then, you pilot the product or service with a suitably small subset of your production infrastructure for testing, learning, and customization. Then, gradually increase the scope of the deployment until your entire infrastructure or organization is covered.

Here is the workflow for piloting and deploying Defender for Identity in your production environment.

[![A diagram that shows the steps to pilot and deploy Microsoft Defender for Identity.](media/eval-defender-xdr/defender-identity-pilot-deploy-steps.svg)](media/eval-defender-xdr/defender-identity-pilot-deploy-steps.svg#lightbox)

Follow these steps:

1. Set up the Defender for Identity instance
2. Install and configure sensors
3. Configure event log and proxy settings on machines with the sensor
4. Allow Defender for Identity to identify local admins on other computers
5. Try out capabilities

Here are the recommended steps for each deployment stage.

| Deployment stage | Description |
| --- | --- |
| Evaluate | Perform product evaluation for Defender for Identity. |
| Pilot | Perform Steps 1-5 for a suitable subset of servers with sensors in your production environment. |
| Full deployment | Perform Steps 2-4 for your remaining servers, expanding beyond the pilot to include all of them. |

### Protecting your organization from hackers

Defender for Identity provides powerful protection on its own. However, when combined with the other capabilities of Microsoft Defender, Defender for Identity provides data into the shared signals which together help stop attacks.

Here's an example of a cyber-attack and how the components of Microsoft Defender XDR help detect and mitigate it.

[![A diagram that shows how Microsoft Defender XDR stops a threat chain.](media/eval-defender-xdr/m365-defender-eval-threat-chain.svg)](media/eval-defender-xdr/m365-defender-eval-threat-chain.svg#lightbox)

Defender for Identity gathers signals from Active Directory Domain Services (AD DS) domain controllers and servers running Active Directory Federation Services (AD FS) and Active Directory Certificate Services (AD CS). It uses these signals to protect your hybrid identity environment, including protecting against hackers that use compromised accounts to move laterally across workstations in the on-premises environment.

Microsoft Defender correlates the signals from all the Microsoft Defender components to provide the full attack story.

## Defender for Identity architecture

Microsoft Defender for Identity is fully integrated with Microsoft Defender and leverages signals from on-premises Active Directory identities to help you better identify, detect, and investigate advanced threats directed at your organization.

Deploy Microsoft Defender for Identity to help your Security Operations (SecOps) teams deliver a modern identity threat detection and response (ITDR) solution across hybrid environments, including:

- Prevent breaches, using proactive identity security posture assessments
- Detect threats, using real-time analytics and data intelligence
- Investigate suspicious activities, using clear, actionable incident information
- Respond to attacks, using automatic response to compromised identities. For more information, see [What is Microsoft Defender for Identity?](/en-us/defender-for-identity/what-is)

Defender for Identity protects your on-premises AD DS user accounts and user accounts synchronized to your Microsoft Entra ID tenant. To protect an environment made up of only Microsoft Entra user accounts, see [Microsoft Entra ID Protection](/en-us/azure/active-directory/identity-protection/overview-identity-protection).

The following diagram illustrates the architecture for Defender for Identity.

[![A diagram that shows the architecture for Microsoft Defender for Identity.](media/eval-defender-xdr/m365-defender-identity-architecture.svg)](media/eval-defender-xdr/m365-defender-identity-architecture.svg#lightbox)

In this illustration:

- Sensors installed on AD DS domain controllers and AD CS servers parse logs and network traffic and send them to Microsoft Defender for Identity for analysis and reporting.
- Sensors can also parse AD FS authentications for third-party identity providers and when Microsoft Entra ID is configured to use federated authentication (the dotted lines in the illustration).
- Microsoft Defender for Identity shares signals to Microsoft Defender.

Defender for Identity sensors can be directly installed on the following servers:

- **AD DS domain controllers**. The sensor directly monitors domain controller traffic, without the need for a dedicated server or the configuration of port mirroring.
- **AD FS servers / AD CS servers**. The sensor directly monitors network traffic and authentication events.

For a deeper look into the architecture of Defender for Identity, see [Microsoft Defender for Identity architecture](/en-us/defender-for-identity/architecture).

## Step 1: Set up the Defender for Identity instance

Sign in to the Defender portal to start deploying supported services, including Microsoft Defender for Identity. For more information, see [Start using Microsoft Defender](/en-us/defender-for-identity/deploy/deploy-defender-identity##start-using-microsoft-defender-xdr).

## Step 2: Install your sensors

Defender for Identity requires some prerequisite work to ensure that your on-premises identity and networking components meet minimum requirements for you to install the Defender for Identity sensor in your environment.

Once you're sure of your environment's readiness, plan your capacity, and verify connectivity to Defender for Identity. Then when you're ready, download, install, and configure the Defender for Identity sensor on the domain controllers, AD FS, and AD CS servers in your on-premises environment.

| Step | Description | More information |
| --- | --- | --- |
| 1 | Confirm that your environment meets Defender for Identity prerequisites. | [Microsoft Defender for Identity prerequisites](/en-us/defender-for-identity/prerequisites) |
| 2 | Determine how many Microsoft Defender for Identity sensors you need. | [Plan capacity for Microsoft Defender for Identity](/en-us/defender-for-identity/capacity-planning) |
| 3 | Verify connectivity to the Defender for Identity service | [Check network activity](/en-us/defender-for-identity/deploy/quick-installation-guide#check-network-connectivity) |
| 4 | Download and install the Defender for Identity sensor | [Install Defender for Identity](/en-us/defender-for-identity/deploy/quick-installation-guide#install-defender-for-identity) |
| 5 | Configure the sensor | [Configure Microsoft Defender for Identity sensor settings](/en-us/defender-for-identity/deploy/configure-sensor-settings) |

## Step 3: Configure event log and proxy settings on machines with the sensor

On the machines that you installed the sensor on, configure Windows event log collection to enable and enhance detection capabilities.

| Step | Description | More information |
| --- | --- | --- |
| 1 | Configure Windows event log collection | [Configure Windows event auditing](/en-us/defender-for-identity/deploy/configure-windows-event-collection) |

## Step 4: Allow Defender for Identity to identify local admins on other computers

Microsoft Defender for Identity lateral movement path (LMP) detection relies on queries that identify local admins on specific machines. These queries are performed with the SAM-R protocol, using the Defender for Identity Service account.

To ensure Windows clients and servers allow your Defender for Identity account to perform SAM-R, a modification to Group Policy must be made to add the Defender for Identity service account in addition to the configured accounts listed in the Network access policy. Make sure to apply group policies to all computers **except domain controllers**.

For instructions on how to do this, see [Configure SAM-R to enable lateral movement path detection in Microsoft Defender for Identity](/en-us/defender-for-identity/deploy/remote-calls-sam).

## Step 5: Try out capabilities

The Defender for Identity documentation includes the following articles that walk through the process of identifying and remediating various attack types:

- [Investigate assets](/en-us/defender-for-identity/investigate-assets), including suspicious users, groups, and devices
- [Understand and investigate LMPs with Microsoft Defender for Identity](/en-us/defender-for-identity/understand-lateral-movement-paths)
- [Understand security alerts](/en-us/defender-for-identity/understanding-security-alerts)

For more information, see:

- [Reconnaissance alerts](/en-us/defender-for-identity/reconnaissance-alerts)
- [Compromised credential alerts](/en-us/defender-for-identity/compromised-credentials-alerts)
- [Lateral movement alerts](/en-us/defender-for-identity/lateral-movement-alerts)
- [Domain dominance alerts](/en-us/defender-for-identity/domain-dominance-alerts)
- [Exfiltration alerts](/en-us/defender-for-identity/exfiltration-alerts)
- [Investigate a user](/en-us/defender-for-identity/investigate-a-user)
- [Investigate a computer](/en-us/defender-for-identity/investigate-a-computer)
- [Investigate lateral movement paths](/en-us/defender-for-identity/investigate-lateral-movement-path)
- [Investigate entities](/en-us/defender-for-identity/investigate-entity)

## SIEM integration

You can integrate Defender for Identity with Microsoft Sentinel for unified security operations in the [Defender portal](/en-us/defender-xdr/isoc-overview), or with a generic security information and event management (SIEM) service to enable centralized monitoring of alerts and activities from connected apps. With Microsoft Sentinel, you can more comprehensively analyze security events across your organization and build playbooks for effective and immediate response.

The Defender portal supports unified security operations with Microsoft Sentinel, bringing signals from Defender, including Defender for Identity, to Microsoft Sentinel.

For more information, see:

- [Connect Microsoft Sentinel to the Microsoft Defender portal](/en-us/azure/sentinel/microsoft-sentinel-onboard)
- [Generic SIEM integration](/en-us/cloud-app-security/siem)