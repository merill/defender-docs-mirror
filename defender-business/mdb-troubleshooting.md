---
layout: FAQ
title: Microsoft Defender for Business troubleshooting - Microsoft Defender for Business | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-business/mdb-troubleshooting
summary: >
  <p>Use this article as a guide to resolve issues you might encounter in Defender for Business.</p>
breadcrumb_path: /defender-business/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Troubleshoot issues in Microsoft Defender for Business. See how to resolve problems with setup or device management.
search.appverid: MET150
author: chrisda
ms.author: chrisda
audience: Admin
ms.topic: faq
ms.service: defender-business
ms.localizationpriority: medium
ms.date: 2023-05-05T00:00:00.0000000Z
ms.reviewer: efratka
f1.keywords: NOCSH
ms.collection:
- SMB
- m365-security
- tier1
locale: en-us
document_id: d02c3750-61da-fa35-078e-7d317847186c
document_version_independent_id: d02c3750-61da-fa35-078e-7d317847186c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-business/mdb-troubleshooting.yml
site_name: Docs
depot_name: Learn.defender-business
page_type: faq
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdb-troubleshooting
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-business/mdb-troubleshooting.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b11ae577-8d18-47ab-998c-ea182a941e71
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/87b1d24d-826d-4337-90a0-b6c35e4561f2
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: f24ad4a9-f348-d5d6-944e-7739efa7b2d8
---

# Microsoft Defender for Business troubleshooting - Microsoft Defender for Business | Microsoft Learn

Use this article as a guide to resolve issues you might encounter in Defender for Business.

## My setup and configuration process failed

If you're using the simplified configuration process in Defender for Business and something went wrong, you can still configure your security settings and policies manually. See [Set up and configure Defender for Business](mdb-setup-configuration).

## I'm seeing indications that some devices aren't protected even though they're onboarded to Defender for Business

If devices are running a non-Microsoft antivirus/antimalware solution, real-time protection might be turned off when those devices are onboarded to Defender for Business. Real-time protection is turned on by default in Defender for Business, but a non-Microsoft antivirus/antimalware solution might affect your settings. When real-time protection is turned off, you see notifications in the Microsoft Defender portal (https://security.microsoft.com) that some devices aren't protected. In these cases, make sure real-time protection is turned on.

To confirm that real-time protection is turned on, you can view, and if necessary, edit your next-generation protection policies. See [View or edit your security policies and settings](mdb-configure-security-settings).

We recommend using Microsoft Defender Antivirus together with Defender for Business to get better coordinated protection across products and services. To learn more, see [Better together - Microsoft Defender Antivirus and Microsoft Defender for Endpoint](/en-us/defender-endpoint/why-use-microsoft-defender-antivirus).

## Users are unable to onboard mobile devices using the Microsoft Defender app.

If Defender for Business isn't finished provisioning, users might not be able to onboard their mobile devices using the Microsoft Defender app. To confirm whether provisioning is complete, follow these steps:

1. Go to the [Microsoft Defender portal](https://security.microsoft.com) and sign in.
2. In the navigation bar, go to **Assets** &gt; **Devices**.

    - If you see a message that says, "Hang on! We're preparing new spaces for your data and connecting them," it means that Defender for Business isn't finished provisioning. This process is happening now, and can take up to 24 hours to complete.
    - If you see a list of devices, or you're prompted to onboard devices, it means Defender for Business provisioning is complete. Users should now be able to onboard their mobile devices as expected.

## Users are running into issues with the Microsoft Defender app on their mobile devices.

If users are reporting issues with the Microsoft Defender app, see the following resources to help troubleshoot their issues:

- [Troubleshooting issues on Microsoft Defender for Endpoint on Android](/en-us/defender-endpoint/android-support-signin)
- [Troubleshoot issues and find answers to FAQs on Microsoft Defender for Endpoint on iOS](/en-us/defender-endpoint/ios-troubleshoot)

## I need to resolve a policy conflict

Policy conflicts can arise when security policies are defined using multiple tools or methods. Here's an example:

Suppose that Lee has been using Microsoft Intune to manage devices and security settings. Lee recently started using Defender for Business. Lee chose to use the simplified configuration process in Defender for Business. Now, Lee sees policy conflicts in Intune and in the Microsoft Defender portal.

Fortunately, policy conflicts can be resolved by taking one or more of the following actions:

- Delete your existing policies in the Intune admin center
- See [Troubleshoot policies in Microsoft Intune](/en-us/troubleshoot/mem/intune/device-configuration/troubleshoot-policies-in-microsoft-intune)

See the following articles to learn more about your security policies in Defender for Business:

- [Set up your security policies and settings](mdb-configure-security-settings)
- [View or edit policies](mdb-view-edit-create-policies)

## There's an integration issue between Defender for Business and Microsoft Intune

During your setup and configuration process, you might see an error message that says:

*Something went wrong, and we couldn't complete your setup process. There's an integration issue between Defender for Business and Microsoft Endpoint Manager.*

The error message means that a configuration channel must be established between Defender for Business and Microsoft Intune. If you see the error message, it means that something went wrong with integration. To resolve the issue, use the following three procedures:

**Procedure 1: Turn on the Microsoft Intune connection in the Microsoft Defender portal**

1. Go to the Microsoft Defender portal (https://security.microsoft.com) and sign in.
2. Choose **Settings** &gt; **Endpoints**. Then, under **General**, select **Advanced features**.
3. Scroll down to **Microsoft Intune connection**, and make sure it's on.

**Procedure 2: Set the enforcement scope for Defender for Business**

1. Go to the Microsoft Defender portal (https://security.microsoft.com), and sign in.
2. Choose **Settings** &gt; **Endpoints**. Under **Configuration management**, select **Enforcement scope**.
3. Under **OS platform**, turn on **Windows Client devices**.
4. Select **Save**.

**Procedure 3: Turn on Endpoint Security Profile settings in Intune**

1. Go to Intune (https://intune.microsoft.com) and sign in.
2. Select **Endpoint security**, and then, under **Setup**, select **Microsoft Defender for Endpoint**.
3. Under **Endpoint Security Profile Settings**, set **Allow Microsoft Defender for Endpoint to enforce Endpoint Security Configurations** to **On**.

## Something went wrong with onboarding devices in the Microsoft Defender portal

If something goes wrong when you're onboarding devices in the Microsoft Defender portal (https://security.microsoft.com), an error message is displayed. For example, you're onboarding devices using any of the following methods:

- A downloadable onboarding package for Microsoft Intune.
- Group Policy.
- System Center Configuration Manager.
- Mobile Device Management capabilities with Defender for Business.

Defender for Business uses a capability called *Security Management for Microsoft Defender for Endpoint*. If onboarding in Defender for Business fails, the cause most likely has to do with Security Management for Defender for Endpoint. To resolve the issue, see the following articles:

- [Troubleshoot onboarding issues related to Security Management for Microsoft Defender for Endpoint](/en-us/defender-endpoint/troubleshoot-security-config-mgt)
- [Run Microsoft Defender for Endpoint Client Analyzer on Windows](/en-us/defender-endpoint/troubleshoot-security-config-mgt#run-microsoft-defender-for-endpoint-client-analyzer-on-windows)

Alternately, you can try onboarding devices manually. See [Onboard devices](mdb-onboard-devices).