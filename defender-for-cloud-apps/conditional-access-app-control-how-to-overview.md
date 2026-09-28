---
layout: Conceptual
title: Use Defender for Cloud Apps Conditional Access app control - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/conditional-access-app-control-how-to-overview
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
description: Learn how to use Microsoft Defender for Cloud Apps Conditional Access app control to create access and session policies for real-time monitoring and control over access to cloud apps.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: AmitMishaeli
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 7ba661da-ab41-fab2-1706-c474eebd91bb
document_version_independent_id: 7ba661da-ab41-fab2-1706-c474eebd91bb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/conditional-access-app-control-how-to-overview.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: conditional-access-app-control-how-to-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/conditional-access-app-control-how-to-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 5289e07b-9489-aeda-634c-bc01278f9b02
---

# Use Defender for Cloud Apps Conditional Access app control - Microsoft Defender for Cloud Apps | Microsoft Learn

Use Microsoft Defender for Cloud Apps Conditional Access app control to create access and session policies that monitor and control user access to cloud apps in real time. This guide walks through onboarding your apps, setting up a Conditional Access policy, and creating and testing your access and session policies. Before you begin, make sure you meet the prerequisites.

## Conditional Access app control usage flow (Preview)

The following image shows the high level process for configuring and implementing Conditional Access app control:

[![Diagram of the Conditional Access app control process flow.](media/conditional-access-app-control-how-to-overview/conditional-access-policy-flow.png)](media/conditional-access-app-control-how-to-overview/conditional-access-policy-flow.png#lightbox)

## Which identity provider are you using?

Before you start using Conditional Access app control, understand whether your apps are managed by Microsoft Entra or another identity provider (IdP).

- **Microsoft Entra apps** are automatically onboarded for Conditional Access app control and are immediately available for you to use in your access and session policy conditions (Preview). Microsoft Entra apps can also be manually onboarded before you select them in your access and session policy conditions.
- **Apps that use non-Microsoft IdPs** must be manually onboarded before you can select them in your access and session policy conditions.

    - If you're working with a catalog app from a non-Microsoft IdP, configure the integration between your IdP and Defender for Cloud Apps to onboard all catalog apps. For more information, see [Onboard non-Microsoft IdP catalog apps for Conditional Access app control](proxy-deployment-featured-idp).
    - If you're working with custom apps, you need to both configure the integration between your IdP and Defender for Cloud Apps, and also onboard each custom app. For more information, see [Onboard non-Microsoft IdP custom apps for Conditional Access app control](proxy-deployment-any-app-idp).

### Sample procedures

The following articles provide sample processes for configuring a non-Microsoft IdP to work with Defender for Cloud Apps:

- [PingOne as your IdP](proxy-idp-pingone)
- [Active Directory Federation Services (AD FS) as your IdP](proxy-idp-adfs)
- [Okta as your IdP](proxy-idp-okta)

## Prerequisites:

Before you configure Conditional Access app control, make sure the following prerequisites are met:

1. Make sure your firewall allows traffic from all IP addresses listed in [Network requirements](network-requirements).
2. Check that your app has a full certificate chain. Missing parts of the chain can cause unexpected app behavior with Conditional Access app control policies.

## Create a Microsoft Entra ID Conditional Access policy

Access and session policies need a Conditional Access policy in Microsoft Entra ID. This policy controls traffic to your cloud apps.

For steps to create one, see the [access policy](access-policy-aad) and [session policy](session-policy-aad) guides.

To learn more, see [Conditional Access policies](/en-us/azure/active-directory/conditional-access/overview) and [Building a Conditional Access policy](/en-us/entra/identity/conditional-access/concept-conditional-access-policies).

## Create your access and session policies

After you've confirmed that your apps are onboarded, either automatically because they're Microsoft Entra ID apps, or manually, and you have a Microsoft Entra ID Conditional Access policy ready, you can continue with creating access and session policies for any scenario you need.

For more information, see:

- [Create a Defender for Cloud Apps access policy](access-policy-aad#create-a-defender-for-cloud-apps-access-policy)
- [Create a Defender for Cloud Apps session policy](session-policy-aad#create-a-defender-for-cloud-apps-session-policy)

## Test your policies

Make sure to test your policies and update any conditions or settings as needed. For more information, see:

- [Test your access policy](access-policy-aad#test-your-policy)
- [Test your session policy](session-policy-aad#test-your-policy)