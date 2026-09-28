---
layout: FAQ
title: Frequently asked questions about app governance - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/app-governance-faq
summary: >
  <p>Read this article to quickly get answers to your app governance questions.</p>
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
ms.date: 2025-07-17T00:00:00.0000000Z
description: Get answers to your questions about app governance.
locale: en-us
document_id: 55381f2a-d12d-f4af-1220-0ddb41a18aea
document_version_independent_id: 55381f2a-d12d-f4af-1220-0ddb41a18aea
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/app-governance-faq.yml
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: faq
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: app-governance-faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/app-governance-faq.yml
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 2745218f-e080-26d7-2a61-5878f7cc7805
---

# Frequently asked questions about app governance - Microsoft Defender for Cloud Apps | Microsoft Learn

Read this article to quickly get answers to your app governance questions.

## What is app governance?

App governance is a feature in Microsoft Defender for Cloud Apps. It provides expanded visibility and control over apps that access your Microsoft 365 data. For more information, see [App governance in Microsoft Defender for Cloud Apps](app-governance-manage-app-governance).

## What types of apps does app governance secure?

App governance tracks non-Microsoft apps that use OAuth to authenticate to Microsoft Entra ID, as well as Google and Salesforce. For apps that authenticate to Microsoft Entra ID, app governance identifies and excludes Microsoft apps whose home tenant is the ["first-party app"](/en-us/troubleshoot/azure/active-directory/verify-first-party-apps-sign-in#application-ids-of-commonly-used-microsoft-applications) tenant owned by Microsoft (tenant ID: f8cdef31-a31e-4b4a-93e4-5f571e91255a).

These apps represent modern apps that can access various resources, including Microsoft 365 data in mailboxes, OneDrive folders, SharePoint sites, and Teams. End users regularly introduce these apps and can give them consent to access data.

While Defender for Cloud Apps also tracks apps that use OAuth to access Microsoft 365, app governance provides extra out-of-box detections and highly customizable policies that track various app attributes and behaviors.

## How can I get app governance?

App governance is a feature in Defender for Cloud Apps. To use app governance, Defender for Cloud Apps must be present in your account either as a standalone product or as part of a license package. If you have the appropriate administrator role and satisfy all the prerequisites, you can navigate to [Microsoft Defender XDR settings](https://security.microsoft.com/cloudapps/settings?tabid=activateAppG) page and turn on app governance.

## What can app governance detect?

App governance generates two types of alerts:

- **Threat detection alerts** are based on Microsoft threat intelligence and are designed to identify apps that are malicious. These out-of-box detections utilize machine learning and anomaly detection to find applications that are likely involved in an attack. [View threat detection alert types](app-governance-anomaly-detection-alerts)
- **Policy alerts**track various app attributes and behaviors—certification, data use, API access errors, unused permissions—that can indicate misuse and risk. The policies themselves are either customizable (user-defined) or predefined:
    - User-defined policies can use one or many conditions to identify risky apps. You can set custom thresholds to determine when these policies are triggered.
    - Predefined policies track the same app attributes and behaviors, but look into other signals and dynamically adjust thresholds.

## What types of actions can app governance take on cloud apps that trigger policy?

App governance can deactivate apps that match either user-defined or predefined policies. Deactivated apps aren't able to authenticate to Microsoft Entra ID and access resources, until they're activated manually. [Learn about app governance policies](app-governance-app-policies-create)

## Can I customize my policies?

You can create policies by combining conditions that track various app attributes and behaviors. When these conditions are met, policies trigger alerts and take the action you've specified. App governance also provides predefined policies that you switch on or off. You can also set the action on predefined policies. [Learn about app governance policies](app-governance-app-policies-create)

## Is app governance integrated with Microsoft Defender XDR?

App governance alerts and related incidents are available in the Microsoft Defender XDR queue. Microsoft Defender XDR correlates the alerts with signals from other solutions, such as Defender for Endpoint, to associate related attack activities and identify security incidents. App governance alerts and incidents are also integrated with Microsoft Sentinel.

## What roles do I need to activate app governance

For the list of supported roles, see [Get started with app governance](app-governance-get-started#roles).

## What roles do I need to have to use app governance?

For the list of supported roles, see [Get started with app governance](app-governance-get-started#roles).

## Is app governance available in all regions?

App governance is currently not available in Singapore, Poland, Italy, Qatar, Israel, Spain, Mexico and Taiwan. To use app governance, your billing location must be in another country/region.

## Why is app governance empty or showing inaccurate data?

It can take up to 10 hours to fully prepare app governance and retrieve data after you first initiate it. During this period data access statistics and app counts can be inaccurate.

## How does app governance integrate with Microsoft Sentinel?

App governance is integrated with Microsoft Defender XDR for a unified alert experience. The Microsoft Defender XDR connector for Microsoft Sentinel (preview) sends all Microsoft Defender XDR incidents and alerts information to Microsoft Sentinel and keeps the incidents synchronized.

The Microsoft Defender XDR connector enables you to automatically detect, triage, investigate and remediate app governance incidents and alerts on Microsoft Sentinel. For more information, see [Microsoft Defender XDR integration with Microsoft Sentinel](/en-us/microsoft-365/security/defender/microsoft-365-defender-integration-with-azure-sentinel) and [Connect data from Microsoft Defender XDR to Microsoft Sentinel](/en-us/azure/sentinel/connect-microsoft-365-defender)

## Where can I get more information about app governance?

You can find more information about app governance in the following resources:

- [Protect your business with Microsoft Security's comprehensive protection](https://www.microsoft.com/security/blog/2021/11/02/protect-your-business-with-microsoft-securitys-comprehensive-protection/)
- [Announcing Microsoft Defender for Cloud Apps](https://techcommunity.microsoft.com/t5/security-compliance-and-identity/announcing-microsoft-defender-for-cloud-apps/ba-p/2835842)
- [How to Prevent App Cyber Attacks—Cloud & Hybrid](https://www.youtube.com/watch?v=KmE8LW_tJ1M)
- [Twitter: Microsoft is tracking a recent consent phishing campaign, reported by @ffforward, that abuses OAuth.](https://twitter.com/MsftSecIntel/status/1484623341155610624)
- [Microsoft shifts to a comprehensive SaaS security solution - Microsoft Security Blog](https://www.microsoft.com/en-us/security/blog/2023/02/15/microsoft-shifts-to-a-comprehensive-saas-security-solution)
- [Improve your app posture and hygiene using Microsoft Defender for Cloud Apps](https://techcommunity.microsoft.com/t5/microsoft-defender-xdr-blog/improve-your-app-posture-and-hygiene-using-microsoft-defender/ba-p/3742361)
- [App governance is a key part of customers’ zero trust journey](https://www.youtube.com/watch?v=XuGZu8ja134)