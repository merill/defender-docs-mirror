---
layout: Conceptual
title: Overview - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/what-is-defender-for-cloud-apps
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: This article describes Microsoft Defender for Cloud Apps and how it works.
ms.date: 2024-06-14T00:00:00.0000000Z
ms.topic: overview
locale: en-us
document_id: 1358211a-0055-bf0a-136c-8ae7fb7a3769
document_version_independent_id: 1358211a-0055-bf0a-136c-8ae7fb7a3769
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/what-is-defender-for-cloud-apps.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: what-is-defender-for-cloud-apps
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/what-is-defender-for-cloud-apps.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 1c5e336e-3718-73fa-5d13-b34a286e5dce
---

# Overview - Microsoft Defender for Cloud Apps | Microsoft Learn

Tip

You might be looking for Microsoft 365 Cloud App Security. For more information, see [What are the differences between Microsoft Defender for Cloud Apps and Microsoft 365 Cloud App Security?](editions-cloud-app-security-o365)

Software as a service (SaaS) apps are ubiquitous across hybrid work environments, and protecting SaaS apps and the important data they store is a big challenge for organizations. The rise in app usage, combined with employees accessing company resources outside of the corporate perimeter has also introduced new attack vectors. To combat these attacks effectively, security teams need an approach that protects their data within cloud apps beyond the traditional scope of cloud access security brokers (CASBs).

![Diagram of the Defender for Cloud App pillars.](media/overview/defender-for-cloud-apps-pillars.png)

Microsoft Defender for Cloud Apps delivers full protection for SaaS applications, helping you monitor and protect your cloud app data across the following feature areas:

- **Fundamental cloud access security broker (CASB) functionality**, such as Shadow IT discovery, visibility into cloud app usage, protection against app-based threats from anywhere in the cloud, and information protection and compliance assessments.
- **SaaS Security Posture Management (SSPM) features**, enabling security teams to improve the organization’s security posture
- **Advanced threat protection**, as part of Microsoft's extended detection and response (XDR) solution, enabling powerful correlation of signal and visibility across the full kill chain of advanced attacks
- **App-to-app protection**, extending the core threat scenarios to OAuth-enabled apps that have permissions and privileges to critical data and resources.

## Discover SaaS applications

Defender for Cloud Apps shows the full picture of risks to your environment from SaaS app usage and resources, and gives you control of what’s being used and when.

- **Identify**: Defender for Cloud apps uses data based on an assessment of network traffic and an extensive app catalog to identify apps accessed by users across your organization. Defender for Cloud Apps provides details on which apps are really being used both on and off your corporate network.

    Defender for Cloud Apps detects all your cloud services, assigns each a risk ranking, and also identifies all the users and third-party apps able to sign in.
- **Assess**: Evaluate discovered apps for more than 90 risk indicators, allowing you to sort through the discovered apps and assess your orgs security and compliance posture.
- **Manage**: Set policies that monitor apps around the clock. For example, if anomalous behavior happens, like unusual spikes in usage, you're automatically alerted and guided to action.

For more information, see [Set up cloud discovery](set-up-cloud-discovery).

## SaaS Security Posture Management (SSPM)

While optimizing an organization's security posture is a critical focus area, security teams are challenged by needing to research best practices for each app individually. Defender for Cloud Apps helps you by surfacing misconfigurations and recommending specific actions to strengthen the security posture for each connected app. Recommendations are based on industry standards like the Center for Internet Security and follow best practices set by the specific app provider.

Defender for Cloud Apps automatically provides SSPM data in Microsoft Secure Score, for any supported and connected app. For more information, see [User, app governance, and security configuration visibility](enable-instant-visibility-protection-and-governance-actions-for-your-apps#user-app-governance-and-security-configuration-visibility).

## Information protection

Defender for Cloud Apps identifies and helps you control sensitive information with data loss protection (DLP) features, and helps you respond to sensitivity labels on detected content.

The Defender for Cloud Apps integration with Microsoft Purview also enables security teams to leverage out-of-the-box data classification types in their information protection policies. Microsoft provides an expansive suite of data loss protection capabilities to ensure your data is protected no matter where it is being accessed.

Defender for Cloud Apps connects to SaaS apps to scan for files containing sensitive data uncovering which data is stored where and who is accessing it. To protect this data, organizations can implement controls such as:

- Apply a sensitivity label
- Block downloads to an unmanaged device
- Remove external collaborators on confidential files

For more information, see [Integrate Microsoft Purview Information Protection](azip-integration).

## Continuous threat protection in eXtended detection and response (XDR)

While cloud apps continue to be a target for adversaries trying to exfiltrate corporate data, sophisticated attacks often cross modalities—moving laterally from email as the most common entry point, to compromise endpoints and identities, before ultimately gaining access to in-app data.

Defender for Cloud Apps offers built-in adaptive access control (AAC), provides user and entity behavior analysis (UEBA), and helps you mitigate malware.

Defender for Cloud Apps is also integrated directly into Microsoft Defender, correlating cross-domain signals from the Microsoft Defender suite and providing incident-level detection, investigation, and powerful response capabilities. Integrating SaaS security into Microsoft's unified security experience gives SOC teams full kill chain visibility and improves operational efficiency and effectivity.

For more information, see [Microsoft Defender for Cloud Apps in Microsoft Defender](/en-us/microsoft-365/security/defender/microsoft-365-security-center-defender-cloud-apps).

## App to app protection with app governance

OAuth apps often behave unnoticed, while still having extensive permissions to access data in other apps on behalf of an employee, making OAuth apps susceptible to a compromise.

Defender for Cloud Apps closes the gap on OAuth app security, helping you protect inter-app data exchange with application governance. Watch for unused apps and monitor both current and expired credentials to govern the apps used in your organization and maintain app hygiene.

For more information, see [App governance in Microsoft Defender for Cloud Apps](app-governance-manage-app-governance).