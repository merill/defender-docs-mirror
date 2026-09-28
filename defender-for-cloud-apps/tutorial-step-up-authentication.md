---
layout: Conceptual
title: Require step-up authentication (authentication context) upon risky action - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/tutorial-step-up-authentication
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
description: This tutorial provides instructions for requiring step-up authentication (authentication context) upon risky action.
ms.date: 2024-05-15T00:00:00.0000000Z
ms.topic: tutorial
locale: en-us
document_id: 9f6ab683-1d42-5c18-f3ad-f96e04f2a633
document_version_independent_id: 9f6ab683-1d42-5c18-f3ad-f96e04f2a633
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/tutorial-step-up-authentication.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: tutorial-step-up-authentication
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/tutorial-step-up-authentication.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/9d7be3ef-f27c-4c7f-9eba-67c3cd429995
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/feeb50f3-b677-44f9-b3a6-5f2f58182b0d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: fee87d93-e635-112a-68bb-07a5cb054456
---

# Require step-up authentication (authentication context) upon risky action - Microsoft Defender for Cloud Apps | Microsoft Learn

As an IT admin today, you're stuck between a rock and hard place. You want to enable your employees to be productive. That means allowing employees to access apps so they can work at any time, from any device. However, you want to protect the company's assets including proprietary and privileged information. How can you enable employees to access your cloud apps while protecting your data?

This tutorial allows you to reevaluate Microsoft Entra Conditional Access policies when users take sensitive actions during a session.

## The threat

An employee logged in to SharePoint Online from the corporate office. During the same session, their IP address registered outside of the corporate network. Maybe they went to the coffee shop downstairs, or maybe their token was compromised or stolen by a malicious attacker.

## The solution

Protect your organization by requiring Microsoft Entra Conditional Access policies to be reassessed during sensitive session actions the Defender for Cloud Apps conditional access app control.

## Prerequisites

- A valid license for Microsoft Entra ID P1 license
- Your cloud app, in this case SharePoint Online, configured as a Microsoft Entra ID app and using SSO via SAML 2.0 or OpenID Connect
- Make sure the [app is deployed to Defender for Cloud Apps](proxy-deployment-aad)

## Create a policy to enforce step-up authentication

Defender for Cloud Apps session policies allow you to restrict a session based on device state. To accomplish control of a session using its device as a condition, create both a Conditional Access policy **and** a session policy.

**To create your policy**:

1. In the Microsoft Defender Portal, under **Cloud Apps**, go to **Polices** -&gt; **Policy management**.
2. In the **Policies** page, select **Create policy** followed by **Session policy**.
3. In the **Create session policy** page, give your policy a name and description. For example, **Require step-up authentication on downloads from SharePoint Online from unmanaged devices**.
4. Assign a **Policy severity** and **Category**.
5. For the **Session control type**, select **Block activities,** **Control file upload (with inspection),** **Control file download (with inspection)**.
6. Under **Activity source** in the **Activities matching all the following** section, select the filters:

    - **Device tag**: Select **Does not equal**, and then select **Intune compliant**, **Microsoft Entra hybrid joined**, or **Valid client certificate**. Your selection depends on the method used in your organization for identifying managed devices.
    - **App**: Select **Automated Azure AD onboarding** and then select **SharePoint Online** from the list.
    - **Users**: Select the users you want to monitor.
7. Under **Activity source** in the **Files matching all of the following** section, set the following filters:

    - **Sensitivity labels**: If you use sensitivity labels from Microsoft Purview Information Protection, filter the files based on a specific Microsoft Purview Information Protection sensitivity label.
    - Select **File name** or **File type** to apply restrictions based on file name or type.
8. Enable **Content inspection** to enable the internal DLP to scan your files for sensitive content.
9. Under **Actions**, select **Require step-up authentication**.

    Note

    This requires [authentication context to be created in Microsoft Entra ID](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/StepUpTags).
10. Set the alerts you want to receive when the policy is matched. You can set a limit so that you don't receive too many alerts. Select if to get the alerts as an email message.
11. Select **Create**.

## Validate your policy

1. To simulate this policy, sign in to the app from an unmanaged device or a non-corporate network location. Then, try to download a file.
2. You should be required to perform the action configured in the authentication context policy.
3. In the Microsoft Defender Portal, under **Cloud Apps**, go to **Polices** -&gt; **Policy management**. Then select the policy you've created to view the policy report. A session policy match should appear shortly.
4. In the policy report, you can see which logins where redirected to Microsoft Defender for Cloud Apps for session control, and which files were downloaded or blocked from the monitored sessions.