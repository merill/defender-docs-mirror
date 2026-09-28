---
layout: Conceptual
title: Set up and configure Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-business/mdb-setup-configuration
breadcrumb_path: /defender-business/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: See how to set up your Defender for Business cybersecurity solution. Onboard devices, review your policies, and edit your settings as needed.
author: chrisda
ms.author: chrisda
ms.topic: overview
ms.service: defender-business
ms.localizationpriority: medium
ms.date: 2025-09-11T00:00:00.0000000Z
ms.reviewer: efratka, nehabha
ms.collection:
- SMB
- m365-security
- m365solution-mdb-setup
- highpri
- tier1
locale: en-us
document_id: 97e3ed41-1454-77e8-fb4b-999f7a2d506a
document_version_independent_id: 97e3ed41-1454-77e8-fb4b-999f7a2d506a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-business/mdb-setup-configuration.md
site_name: Docs
depot_name: Learn.defender-business
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdb-setup-configuration
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-business/mdb-setup-configuration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b11ae577-8d18-47ab-998c-ea182a941e71
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/87b1d24d-826d-4337-90a0-b6c35e4561f2
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 4da91def-f916-2324-963a-45a6465b888e
---

# Set up and configure Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn

This article describes the overall setup process for Defender for Business.

![Overview of the setup process for Microsoft Defender for Business.](media/mdb-setup-overview.png)

The process includes:

1. [Getting Defender for Business](get-defender-business).
2. [Adding users and assigning licenses](mdb-add-users).
3. [Assigning security roles and permissions for your security team](mdb-roles-permissions).
4. [Setting up email notifications for your security team](mdb-email-notifications).
5. [Onboarding devices so they're protected as soon as possible](mdb-onboard-devices).
6. [Setting up and reviewing your security policies and settings](mdb-configure-security-settings).

## Setup options

When you're ready to set up and configure Defender for Business, you can choose from several options:

- **Use the setup wizard** to grant access to your security team, set up email notifications for your security team, onboard your company's Windows devices, and apply default security settings to those devices; or
- **Work through the setup process manually**, step by step, and complete the setup steps yourself.

Note

Using the setup wizard is optional. If you choose not to use the wizard, or if the wizard is closed before your setup process is complete, you can complete the setup and configuration process on your own.

# [Setup wizard](#tab/Wizard)
1. **Get Defender for Business**. Start a trial or paid subscription today. You can choose from the standalone version of Defender for Business, or get it as part of Microsoft 365 Business Premium. See [Get Microsoft Defender for Business](get-defender-business). And, if you're planning to onboard servers, see [How to get Microsoft Defender for Business servers](get-defender-business#how-to-get-microsoft-defender-for-business-servers).

    In the Microsoft Defender portal (https://security.microsoft.com), in the navigation pane, select **Assets** &gt; **Devices**. If Defender for Business isn't provisioned yet, that process begins now.
2. **Add users and assign Defender for Business licenses**. Do this task before you run the setup wizard. See [Add users and assign licenses in Microsoft Defender for Business](mdb-add-users).

    While you're adding users, make sure to create a list of your security team's names and email addresses. This list comes in handy while you're using the setup wizard. To view a list of users, in the Microsoft 365 admin center (https://admin.microsoft.com), go to **Users** &gt; **Active users**.
3. In the Microsoft Defender portal (https://security.microsoft.com), in the navigation pane, select **Assets** &gt; **Devices**. You should see the setup wizard home screen, as shown in the following image:

    [![Screenshot of wizard home screen to set up Defender for Business.](media/mdb-wizard-start.png)](media/mdb-wizard-start.png#lightbox)

    Select **Get started** to begin using the wizard.
4. **Assign user permissions**. In this first step of the setup wizard, you grant your security team access to the Microsoft Defender portal (https://security.microsoft.com). This portal is where you and your security team manage your security capabilities, view alerts, and take any needed actions on detected threats. Portal access is granted through roles that imply certain permissions. [Learn more about roles and permissions](mdb-roles-permissions).

    In Defender for Business, members of your security team can be assigned one of the following three roles:

    - **Security Administrator**: A security administrator can view and edit security settings, and take action when threats are detected.
    - **Security Reader**: A security reader can view information in reports, but can't change any security settings.
5. **Set up email notifications**. In this step of the setup wizard, you can set up email notifications for your security team using the list you created in step 2.

    When an alert is generated or a new vulnerability is discovered, your security team is notified, even if they're away from their desk. [Learn more about email notifications](mdb-email-notifications).
6. **Onboard and configure Windows devices**. In this step of the setup wizard, you can onboard Windows devices to Defender for Business. Onboarding devices right away helps to protect those devices from day one.

    This step applies to Windows devices only. You can onboard other devices later. For more information, see [Onboard devices to Microsoft Defender for Business](mdb-onboard-devices).

    Note

    If your organization already has devices enrolled in Microsoft Intune, Defender for Business prompts you to continue using Intune, or switch to the simplified configuration process in the Microsoft Defender portal. For more information, see [Choose where to manage security policies and devices](mdb-configure-security-settings#choose-where-to-manage-security-policies-and-devices).

    Defender for Business also offers automatic onboarding for Windows devices enrolled in Intune. Automatic onboarding is a simplified way to onboard Windows devices to Defender for Business. We recommend selecting the "all devices enrolled" option so that as Windows devices are enrolled in Intune, they're onboarded to Defender for Business automatically.
7. **Configure your security policies**. Defender for Business includes default security policies for next-generation protection and firewall protection that can be applied to your company's devices. These default policies use recommended settings and are designed to provide strong protection for your devices. You can start with your default policies and add policies later. For more information, see [Set up, review, and edit your security policies and settings](mdb-configure-security-settings).
8. **Select your next step**. After the setup wizard is complete, you're prompted to choose a next step. For example, you can onboard devices, view your security dashboard, or view your security policies.

# [Manual setup](#tab/Manual)
1. **Get Defender for Business**. Start a trial or paid subscription today. You can choose from the standalone version of Defender for Business, or get it as part of Microsoft 365 Business Premium. For more information, see [Get Microsoft Defender for Business](get-defender-business). And, if you're planning to onboard servers, see [How to get Microsoft Defender for Business servers](get-defender-business#how-to-get-microsoft-defender-for-business-servers).
2. **Add users and assign licenses**. Assign a license for Defender for Business (or Microsoft 365 Business Premium) to each member of your organization to protect their devices. Make sure multifactor authentication is enabled for all users. For more information, see [Add users and assign licenses in Microsoft Defender for Business](mdb-add-users).
3. **Assign roles and permissions to your security team**. People on your security team need certain permissions to perform tasks such as reviewing detected threats & remediation actions, viewing & editing policies, onboarding devices, and using reports. You can grant these permissions through roles. For more information, see [Assign roles and permissions](mdb-roles-permissions).
4. **Set up email notifications for your security team**. As alerts are generated, or new vulnerabilities are discovered, people on your security team can be notified automatically, via email messages. For more information, see [Set up email notifications](mdb-email-notifications).
5. **Onboard devices to Defender for Business**. The sooner you get your devices onboarded to Defender for Business, the sooner they're protected. You can onboard devices in the Microsoft Defender portal. Or, if your organization is already using Microsoft Intune, you can use it to enroll devices. For more information, see [Onboard devices to Defender for Business](mdb-onboard-devices).
6. **Set up and review your security policies and settings**. Some security policies and settings are preconfigured with default settings in Defender for Business. Other policies, such as web content filtering and attack surface reduction rules, must be set up. For more information, see [Configure your security settings and policies](mdb-configure-security-settings).

Important

If you have Microsoft 365 Business Premium, you have more capabilities to set up and configure. For more information, see [What is Microsoft Defender for Business?](/en-us/microsoft-365/business-premium/m365bp-overview).

---