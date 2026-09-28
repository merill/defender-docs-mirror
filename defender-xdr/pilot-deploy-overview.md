---
layout: Conceptual
title: How do I pilot and deploy Microsoft Defender? - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/pilot-deploy-overview
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: How to pilot and deploy Microsoft Defender and its components in your production Microsoft 365 tenant.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.date: 2025-12-11T00:00:00.0000000Z
ms.localizationpriority: medium
ms.collection:
- m365-security
- m365solution-overview
- m365solution-evalutatemtp
- zerotrust-solution
- highpri
- tier1
ms.topic: solution-overview
locale: en-us
document_id: 96d24301-eb8f-abac-6855-08babf5342aa
document_version_independent_id: 96d24301-eb8f-abac-6855-08babf5342aa
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/pilot-deploy-overview.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: pilot-deploy-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/pilot-deploy-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: eead7c0d-319b-6391-22b7-36a677b97810
---

# How do I pilot and deploy Microsoft Defender? - Microsoft Defender XDR | Microsoft Learn

**Applies to:**

- Microsoft Defender XDR

This series of articles steps you through the entire process of piloting the components of Microsoft Defender in your production tenant so you can evaluate their features and capabilities and then completing the deployment across your organization.

An eXtended detection and response (XDR) solution is a step forward in cyber security because it takes the threat data from systems that were once isolated and unifies them so that you can see patterns and act on suspected cyberattacks faster.

Microsoft Defender XDR:

- Is an XDR solution that combines the information on cyberattacks for identities, endpoints, email, and cloud apps in one place. It leverages artificial intelligence (AI) and automation to automatically stop some types of attacks and remediate affected assets to a safe state.
- Is a cloud-based, unified, pre- and post-breach enterprise defense suite. It coordinates prevention, detection, investigation, and response across identities, endpoints, email, cloud apps, and their data.
- Contributes to a strong Zero Trust architecture by providing threat protection and detection. It helps prevent or reduce business damage from a breach. For more information, see the [Implement threat protection and XDR](/en-us/security/zero-trust/adopt/prevent-reduce-business-damage-breach-threat-protection) business scenario in the Microsoft Zero Trust adoption framework.

## Microsoft Defender components and architecture

This table lists the components of Microsoft Defender.

| Component | Description | For more information |
| --- | --- | --- |
| Microsoft Defender for Identity | Uses signals from your on-premises Active Directory Domain Services (AD DS) and Active Directory Federation Services (AD FS) to identify, detect, and investigate advanced threats, compromised identities, and malicious insider actions directed at your organization. | [What is Microsoft Defender for Identity?](/en-us/defender-for-identity/what-is) |
| The built-in security features for all cloud mailboxes | Native cloud-based SMTP relay and filtering services that help protect your organization against spam and malware. | [Built-in security features for all cloud mailboxes](/en-us/defender-office-365/eop-about) |
| Microsoft Defender for Office 365 | Safeguards your organization against malicious threats posed by email messages, links (URLs) and collaboration tools. | [Microsoft Defender for Office 365 - Office 365](/en-us/defender-office-365/defender-for-office-365-whats-new) |
| Microsoft Defender for Endpoint | A unified platform for device protection, post-breach detection, automated investigation, and recommended response. | [Microsoft Defender for Endpoint - Windows security](/en-us/defender-endpoint/microsoft-defender-endpoint) |
| Microsoft Defender for Cloud Apps | A comprehensive cross-SaaS solution bringing deep visibility, strong data controls, and enhanced threat protection to your cloud apps. | [What is Defender for Cloud Apps?](/en-us/cloud-app-security/what-is-cloud-app-security) |
| Microsoft Entra ID Protection | Evaluates risk data from billions of sign-in attempts and uses this data to evaluate the risk of each sign-in to your tenant. This data is used by Microsoft Entra ID to allow or prevent account access, depending on how Conditional Access policies are configured. Microsoft Entra ID Protection is separate from Microsoft Defender and is included with Microsoft Entra ID P2 licenses. | [What is Identity Protection?](/en-us/azure/active-directory/identity-protection/overview-identity-protection) |

This illustration shows the architecture and integration of Microsoft Defender XDR components.

[![A diagram that shows the high-level architecture of Microsoft Defender XDR.](media/eval-defender-xdr/m365-defender-eval-architecture.svg)](media/eval-defender-xdr/m365-defender-eval-architecture.svg#lightbox)

In this illustration:

- Microsoft Defender combines the signals from all of the Defender components to provide XDR across domains. This includes a unified incident queue, automated response to stop attacks, self-healing (for compromised devices, user identities, and mailboxes), cross-threat hunting, and threat analytics.
- Microsoft Defender for Office 365 safeguards your organization against malicious threats posed by email messages, links (URLs), and collaboration tools. It shares signals resulting from these activities with Microsoft Defender. [The built-in security features for all cloud mailboxes](/en-us/defender-office-365/eop-about) is integrated to provide end-to-end protection for incoming email and attachments.
- Microsoft Defender for Identity gathers signals from AD DS domain controllers and servers running AD FS and AD CS. It uses these signals to protect your hybrid identity environment, including protecting against hackers that use compromised accounts to move laterally across workstations in the on-premises environment.
- Microsoft Defender for Endpoint gathers signals from and protects devices managed by your organization.
- Microsoft Defender for Cloud Apps gathers signals from your organization's use of cloud apps and protects data flowing between your IT environment and these apps, including both sanctioned and unsanctioned cloud apps.
- Microsoft Entra ID Protection evaluates risk data from billions of sign-in attempts and uses this data to evaluate the risk of each sign-in to your tenant. This data is used by Microsoft Entra ID to allow or prevent account access based on the conditions and restrictions of your [Conditional Access policies](/en-us/security/zero-trust/zero-trust-identity-device-access-policies-overview). Microsoft Entra ID Protection is separate from Microsoft Defender and is included with Microsoft Entra ID P2 licenses.

### Microsoft Defender components and SIEM integration

You can integrate Microsoft Defender XDR components with Microsoft Sentinel or a generic security information and event management (SIEM) service to enable centralized monitoring of alerts and activities from connected apps.

[![A diagram that shows Microsoft Defender XDR integration with SIEM.](media/eval-defender-xdr/defender-xdr-siem-integration.svg)](media/eval-defender-xdr/defender-xdr-siem-integration.svg#lightbox)

Microsoft Sentinel is a cloud-native solution that provides SIEM and security orchestration, automation, and response (SOAR) capabilities. Together, Microsoft Sentinel and Microsoft Defender XDR components provide a comprehensive solution to help organizations defend against modern attacks.

Microsoft Sentinel includes connectors for Microsoft Defender components. This allows you to not only gain visibility into your cloud apps but to also get sophisticated analytics to identify and combat cyberthreats and to control how your data travels. For more information, see [Overview of Microsoft Defender and Microsoft Sentinel integration](/en-us/azure/sentinel/microsoft-365-defender-sentinel-integration) and [Integration steps for Microsoft Sentinel and Microsoft Defender](/en-us/azure/sentinel/connect-microsoft-365-defender?tabs=MDE).

For more information about SOAR in Microsoft Sentinel (including links to playbooks in the Microsoft Sentinel GitHub Repository), see [Automate threat response with playbooks in Microsoft Sentinel](/en-us/azure/sentinel/automate-responses-with-playbooks).

For information about integration with third-party SIEM systems, see [Generic SIEM integration](/en-us/cloud-app-security/siem).

## Microsoft Defender XDR and an example cyber security attack

This diagram shows a common cyber-attack and the components of Microsoft Defender XDR that help detect and remediate it.

[![A diagram that shows the various attempts of a cyber security attack.](media/eval-defender-xdr/m365-defender-eval-threat-chain.svg)](media/eval-defender-xdr/m365-defender-eval-threat-chain.svg#lightbox)

The cyber-attack starts with a phishing email that arrives at the Inbox of an employee in your organization, who unknowingly opens the email attachment. This attachment installs malware, which can lead to a chain of attack attempts that can result in the theft of sensitive data.

In the illustration:

- **The built-in security features for all cloud mailboxes**, part of Microsoft Defender for Office 365, can detect the phishing email and use Exchange mail flow rules (also known as transport rules) to make certain it never arrives in a user's Inbox.
- **Defender for Office 365** uses Safe Attachments to test the attachment and determine that it's harmful, so the mail that arrives either isn't actionable by the user, or policies prevent the mail from arriving at all.
- **Defender for Endpoint** detects device and network vulnerabilities that might otherwise be exploited for devices managed by your organization.
- **Defender for Identity** takes note of sudden on-premises user account changes like privilege escalation or high-risk lateral movement. It also reports on easily exploited identity issues like unconstrained Kerberos delegation, for correction by your security team.
- **Microsoft Defender for Cloud Apps** detects anomalous behavior such as impossible-travel, credential access, and unusual downloading, file sharing, or mail forwarding activity and reports these to your security team.

## The pilot and deploy process for Microsoft Defender

Microsoft recommends enabling the components of Microsoft 365 Defender in the following order.

[![A diagram that shows the pilot and deploy process for Microsoft Defender XDR.](media/eval-defender-xdr/defender-xdr-pilot-deploy-flow.svg)](media/eval-defender-xdr/defender-xdr-pilot-deploy-flow.svg#lightbox)

| Phase | Link |
| --- | --- |
| A. Start the pilot | Start the pilot |
| B. Pilot and deploy Microsoft Defender components | - [Pilot and deploy Defender for Identity](pilot-deploy-defender-identity) - [Pilot and deploy Defender for Office 365](pilot-deploy-defender-office-365) - [Pilot and deploy Defender for Endpoint](pilot-deploy-defender-endpoint) - [Pilot and deploy Microsoft Defender for Cloud Apps](pilot-deploy-defender-cloud-apps) |
| C. Investigate and respond to threats | [Practice incident investigation and response](pilot-deploy-investigate-respond) |

This order is designed to leverage the value of the capabilities quickly based on how much effort is typically required to deploy and configure the capabilities. For example, Defender for Office 365 can be configured in less time than it takes to enroll devices in Defender for Endpoint. Prioritize the components to meet your business needs.

## Start the pilot

Microsoft recommends you start your pilot in your existing production subscription of Microsoft 365 to gain real-world insights immediately and you can tune settings to work against current threats in your Microsoft 365 tenant. After you've gained experience and are comfortable with the platform, simply expand the use of each component, one at a time, to full deployment.

An alternative is to [Set up your Microsoft Defender trial lab environment](setup-m365deval). However, this environment won't show any real cybersecurity information such as threats or attacks on your production Microsoft 365 tenant while you are piloting and you won't be able to move security settings from this environment to your production tenant.

### Using Microsoft 365 E5 trial licenses

If you do not have Microsoft 365 E5 and want to advantage of Microsoft 365 E5 trial licenses for your pilot:

1. Sign in to your existing Microsoft 365 tenant administration portal.
2. Select **Purchase Services** from the navigation menu.
3. From the Office 365 section select **Details** under Office 365 E5 license.

    [![Screenshot of the Details button in the Microsoft Defender portal.](media/pilot-deploy-overview/2_mdo-eval-license-details.png)](media/pilot-deploy-overview/2_mdo-eval-license-details.png#lightbox)
4. Select **Start free trial**.

    [![Screenshot of the Start free trial button in the Microsoft Defender portal.](media/pilot-deploy-overview/3-m365-purchase-button.png)](media/pilot-deploy-overview/3-m365-purchase-button.png#lightbox)
5. Confirm your request and select **Try now**.

    [![Screenshot of the Try Now button in the Microsoft Defender portal.](media/pilot-deploy-overview/4_mdo-trial-order.png)](media/pilot-deploy-overview/4_mdo-trial-order.png#lightbox)

Your pilot using Microsoft 365 E5 trial licenses in your existing production tenant will let you keep any security settings and methods when the trial expires and you purchase equivalent licenses.