---
layout: Conceptual
title: Automatically onboard Microsoft Entra ID apps - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/app-onboarding
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: Adipkmic
manager: bagol
ms.author: adipavekatz
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: Learn how to automatically onboard Microsoft Entra ID apps to Microsoft Defender for Cloud Apps conditional access app control
ms.date: 2024-10-10T00:00:00.0000000Z
ms.topic: concept-article
ms.custom: QuickDraft, ai-usage
ms.reviewer: adipavekatz
search.appverid: MET150
locale: en-us
document_id: 361f7039-5be2-438d-8d1b-a29a301be278
document_version_independent_id: 361f7039-5be2-438d-8d1b-a29a301be278
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/app-onboarding.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: app-onboarding
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/app-onboarding.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
platformId: f8c43c81-0baa-3968-b76d-9a8842af21f7
---

# Automatically onboard Microsoft Entra ID apps - Microsoft Defender for Cloud Apps | Microsoft Learn

All SaaS applications that exist in the Microsoft Entra ID catalog will be available automatically in the policy app filter. The following image shows the high-level process for configuring and implementing Conditional Access app control:

![Diagram of the process for configuring and implementing conditional access app control.](media/caac-app-onboarding/process.png)

## Prerequisites

- Your organization must have the following licenses to use Conditional Access App Control:
    - Microsoft Defender for Cloud Apps
- Apps must be configured with single sign-on in Microsoft Entra ID

Fully performing and testing the procedures in this article requires that you have a session or access policy configured. For more information, see:

- [Create Microsoft Defender for Cloud Apps access policies](access-policy-aad)
- [Create Microsoft Defender for Cloud Apps session policies](session-policy-aad)

## Supported Apps

All SaaS apps listed in the Microsoft Entra ID catalog will be available for filtering within the Microsoft Defender for Cloud Apps session and access policies. Each app chosen in the filter will automatically be onboarded into the system and will be controlled.

![Screenshot of the filter showing automatically onboarded apps.](media/caac-app-onboarding/filter.png)

If an application isn't listed, you have the option to manually onboard it as outlined in the provided instructions.

**Note:** Dependency on Microsoft Entra ID Conditional Access policy:

All apps listed in the Microsoft Entra ID catalog will be available for filtering within Microsoft Defender for Cloud Apps session and access policies. However, only those applications that are included in Microsoft Entra ID's conditional policy with Microsoft Defender for Cloud Apps permissions will be actively managed within access or session policies.

When creating a policy, if the relevant Microsoft Entra ID's conditional policy is missing, an alert will appear, both during the policy creation process and upon saving the policy.

**Note:** To ensure that this policy runs as expected, we recommend checking the Microsoft Entra Conditional Access policies created in Microsoft Entra ID. You can see the full Microsoft Entra Conditional Access policies list in a banner on the create policy page.

![Screenshot of the recommendation shown in the portal.](media/caac-app-onboarding/recommendation.png)

## Conditional Access App Control Configuration Page

Admins will be able to control app configurations such as:

- **Status:** App status - Disable or Enable
- **Policies:** Does at least one inline policy connect
- **IDP:** Onboarded app via IDP via Microsoft Entra or Non-MS IDP
- **Edit app:** Edit app configuration such as adding domains or disabling the app.

All apps that automatically onboarded will be set to "enabled" by default. Following the initial sign-in by a user, administrators will have the ability to view the application under **Settings** &gt; **Connected apps** &gt; **Conditional Access App Control apps**.

## Common App Misconfigurations

- [Second sign-in (also known as 'second sign-in')](troubleshooting-proxy#second-sign-in-also-known-as-second-login)
- [Missing domains](troubleshooting-proxy#add-domains-for-your-app)