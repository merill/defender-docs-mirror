---
layout: Conceptual
title: Microsoft Defender for Business trial user guide - Microsoft Defender for Business | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-business/trial-playbook-defender-business
breadcrumb_path: /defender-business/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: how-to
ms.collection:
- m365-security
- tier1
- essentials-get-started
ms.localizationpriority: high
ms.date: 2026-07-03T00:00:00.0000000Z
ms.service: defender-business
description: Make the most of your Defender for Business trial with this guide. Get set up quickly and get started using your new security capabilities.
ms.custom: trial-playbook, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 615a5455-df5e-42ed-b4c8-f8ef3794be85
document_version_independent_id: 615a5455-df5e-42ed-b4c8-f8ef3794be85
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-business/trial-playbook-defender-business.md
site_name: Docs
depot_name: Learn.defender-business
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: trial-playbook-defender-business
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-business/trial-playbook-defender-business.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: ee3d0f9c-0a9b-eb0c-c935-171bd714c438
---

# Microsoft Defender for Business trial user guide - Microsoft Defender for Business | Microsoft Learn

**Welcome to the Defender for Business trial user guide!**

This guide walks you through setting up your trial subscription, onboarding devices, configuring security policies, and using key features like next-generation protection, endpoint detection and response, and vulnerability management.

## What is Defender for Business?

Defender for Business is an endpoint security solution for small and medium-sized businesses with up to 300 users. It helps protect your devices from ransomware, malware, phishing, and other threats.

![Defender for Business features and capabilities.](media/mdb-offering-overview.png)

**Let's get started!**

## Set up your trial

Here's how to set up your trial subscription:

1. Visit the Microsoft Defender portal.
2. Use the setup wizard.
3. Set up and configure Defender for Business.

### Step 1: Visit the Microsoft Defender portal

The Microsoft Defender portal ([Microsoft Defender portal](https://security.microsoft.com)) is the one-stop shop where you use and manage Defender for Business. It includes callouts to help you get started, cards that surface relevant information, and a navigation bar that provides easy access to the various features and capabilities.

- **[Visit the Microsoft Defender portal](mdb-get-started)**.
- **[Explore the navigation bar](mdb-get-started#the-navigation-bar)** on the left side of the screen to access your incidents, view reports, and manage your security policies and settings.

### Step 2: Use the setup wizard in Defender for Business

Defender for Business was designed to save small and medium-sized businesses time and effort. You can do initial setup and configuration through a setup wizard. The setup wizard helps you grant access to your security team, set up email notifications for your security team, and onboard your company's Windows devices. **[Use the setup wizard](mdb-setup-configuration)**.

Note

You don't have to use the wizard, but we highly recommended it. You can only use the setup wizard once.

#### Setup wizard flow: what to expect

Tip

**Using the setup wizard is optional.** If you choose not to use the wizard, or if the wizard is closed before your setup process is complete, you can complete the setup and configuration process on your own. See Step 3: Set up and configure Defender for Business.

1. **[Assign user permissions](mdb-roles-permissions#view-and-edit-role-assignments)**. Grant your security team access to the Microsoft Defender portal.
2. **[Set up email notifications](mdb-email-notifications#view-and-edit-email-notifications)** for your security team.
3. **[Onboard and configure Windows devices](mdb-onboard-devices)**. Onboarding devices right away helps protect those devices from day one.

    Note

    When you use the setup wizard, the system detects if you have Windows devices that are already enrolled in Intune. You're asked if you want to use automatic onboarding for all or some of those devices. You can onboard all Windows devices at once or select specific devices at first and then add more devices later.

    To onboard other devices, see Step 3: Set up and configure Defender for Business.
4. **[View and edit your security policies](mdb-configure-security-settings)**. Defender for Business includes default security policies for next-generation protection and firewall protection that can be applied to your company's devices. These preconfigured security policies use recommended settings, so you're protected as soon as your devices are onboarded to Defender for Business. And you can edit the policies or create new ones.

### Step 3: Set up and configure Defender for Business

If you choose not to use the setup wizard, the [overall setup and configuration process](mdb-setup-configuration) for Defender for Business is shown in the setup and configuration diagram:

[!\[Setup and configuration process for Defender for Business.\](media/mdb-setup-process-2.png)](mdb-setup-configuration)

If you used the setup wizard but you need to onboard more devices, such as non-Windows devices, go directly to [onboard devices](mdb-onboard-devices).

1. **[Review the requirements](mdb-requirements)** to configure and use Defender for Business.
2. **[Assign roles and permissions](mdb-roles-permissions)** in the Microsoft Defender portal.

    - [Learn about roles in Defender for Business](mdb-roles-permissions#roles-in-defender-for-business).
    - [View or edit role assignments for your security team](mdb-roles-permissions#view-and-edit-role-assignments).
3. **[Set up email notifications](mdb-email-notifications)** for your security team.

    - [Learn about types of email notifications](mdb-email-notifications#types-of-email-notifications).
    - [View and edit email notification settings](mdb-email-notifications#view-and-edit-email-notifications).
4. **[Onboard devices](mdb-onboard-devices)**. To onboard Windows and Mac clients, you can use a local script.
5. **[View and configure your security policies](mdb-configure-security-settings)**. After you onboard your company's devices to Defender for Business, the next step is to view and edit your security policies and settings.

Defender for Business includes preconfigured security policies that use recommended settings. But you can edit the policy settings to suit your business needs.

Security policies to review and configure include:

- [Next-generation protection policies](mdb-next-generation-protection): Determine antivirus and anti-malware protection for your company's devices
- [Firewall protection and rules](mdb-firewall): Determine what network traffic is allowed to flow to and from your company's devices
- [Web content filtering](mdb-web-content-filtering): Prevents people from visiting certain websites (URLs) based on categories, such as adult content or legal liability
- [Advanced features](mdb-portal-advanced-feature-settings#view-settings-for-advanced-features) such as automated investigation and response and endpoint detection and response (EDR) in block mode

## Start using Defender for Business

For the next 30 days, here's guidance from the product team on key features to try:

1. Use your dashboard.
2. View and respond to detected threats.
3. Review security policies.
4. Prepare for ongoing security management.

### Step 1: Use the dashboard

Defender for Business includes a dashboard designed to save your security team time and effort. Learn how to [use your dashboard](mdb-view-tvm-dashboard).

- View your exposure score, which is associated with devices in your organization.
- View your top security recommendations, such as address impaired communications with devices, turn on firewall protection, or update Microsoft Defender Antivirus definitions.
- View remediation activities, such as any files that were sent to quarantine, or vulnerabilities found on devices.

### Step 2: View and respond to detected threats

As threats are detected and alerts are triggered, incidents are created. Your organization's security team can view and manage incidents in the Microsoft Defender portal. Learn how to [view and respond to detected threats](mdb-view-manage-incidents).

- [View and manage incidents](mdb-view-manage-incidents).
- [Respond to and mitigate threats](mdb-respond-mitigate-threats).
- [Review mediation actions in the Action Center](mdb-review-remediation-actions).
- [View and use reports](mdb-reports).

### Step 3: Review security policies

In Defender for Business, security settings are applied to devices via policies that safeguard your organization against identity, device, application, and document security threats. Defender for Business includes preconfigured policies to help protect company devices as soon as they're onboarded.

Learn how to [review security policies](mdb-view-edit-create-policies).

### Step 4: Prepare for ongoing security management

New security events require management. For example:

- Threat detection on a device.
- Adding new devices
- Users joining or leaving the organization.

In Defender for Business, there are many ways for you to manage device security:

- [View a list of onboarded devices](mdb-manage-devices#view-the-list-of-onboarded-devices) to see their risk level, exposure level, and health state.
- [Take action on a device](mdb-manage-devices#take-action-on-a-device-that-has-threat-detections) that has threat detections.
- [Onboard a device to Defender for Business](mdb-manage-devices#onboard-a-device).
- [Offboard a device from Defender for Business](mdb-manage-devices#offboard-a-device).