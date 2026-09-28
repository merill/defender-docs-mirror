---
layout: Conceptual
title: Get started with app governance in Microsoft Defender for Cloud Apps in Microsoft Defender XDR. - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/app-governance-trial-user-guide
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
ms.date: 2025-08-18T00:00:00.0000000Z
ms.topic: quickstart
description: Step-by-step guide to help you quickly get started with app governance in Microsoft Defender for Cloud Apps and Microsoft Defender XDR.
ms.reviewer: shragar
locale: en-us
document_id: b1299c13-7049-6349-5157-d73d3616a2df
document_version_independent_id: b1299c13-7049-6349-5157-d73d3616a2df
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/app-governance-trial-user-guide.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: app-governance-trial-user-guide
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/app-governance-trial-user-guide.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: 6a167d81-ab48-28b2-65ec-7b2e6ce8b475
---

# Get started with app governance in Microsoft Defender for Cloud Apps in Microsoft Defender XDR. - Microsoft Defender for Cloud Apps | Microsoft Learn

App governance solutions require a deep understanding of app behavior within an environment to identify and address activities that fall within a tolerance level that requires more review to assess malicious intent. When layered over Defender for Cloud Apps, app governance gives you in-depth governance against risky app behavior in your environment.

This article describes how to get started using app governance features in Microsoft Defender for Cloud Apps.

## Prerequisites

- If you haven’t already, [sign up for app governance](https://security.microsoft.com/cloudapps/settings?tabid=activateAppG) and complete the steps to add it to your tenant. After you've signed up for app governance, you'll need to wait up to 10 hours to see and use the product.

    For more information, see [Turn on app governance for Microsoft Defender for Cloud Apps](app-governance-get-started).
- Your sign-in account must have a supported [app governance administrator role](app-governance-get-started#roles) to view any app governance data.
- To use full functionality for app governance alerts, you must have provisioned both Defender for Cloud Apps and Microsoft Defender by accessing their respective portals at least once.

## Step 1: Get visibility and insights

Start by using the following steps to get visibility and insights about your apps:

1. **Sign in**: In your browser, go to the **Microsoft Defender XDR &gt; Cloud Apps &gt; [App governance](https://aka.ms/appgovernance)** page.
2. **[Determine compliance posture](app-governance-visibility-insights-compliance-posture)**: Use the data on the **App governance &gt; Overview** tab to assess the compliance posture of your apps and incidents in your tenant. View details like how many overprivileged apps are in your tenant, the number of active incidents, the total Graph API data access, and more.

    Tip

    You can also view app governance-related recommendations in [Secure Score](https://security.microsoft.com/securescore?viewid=overview&amp;tid=b5304409-74ae-42bf-a3e3-d62da4845129) to help you holistically manage your posture.
3. **[View your apps](app-governance-visibility-insights-view-apps)**: Sort the data on the **App governance** tabs by apps with high data usage or number of consents given, or filter by high privileged apps, unused apps, apps with unused permissions, or unverified publisher, and more.

    Use these sorting and filtering options to gain deeper insights into your OAuth apps, including relevant app metadata and usage data.
4. **[Get detailed app information](app-governance-visibility-insights-view-apps#get-detailed-information-about-an-app)**: On the **App governance** tabs, select an app in the grid to view an app details page. Investigate [priority account](/en-us/microsoft-365/admin/setup/priority-accounts) data usage for a specific app, trace exactly whose data is being accessed, which permissions are being used, and which permissions aren't used.

For more information, see [Get started with visibility and insights](app-governance-visibility-insights-overview#get-started-with-visibility-and-insights).

## Step 2: Implement app policies

App governance uses machine learning-based detection algorithms to detect anomalous app behavior in your environment, and then generates alerts that you can see, investigate, and resolve.

Beyond this built-in detection capability, use a set of default policy templates or create your own app policies to generate other alerts.

Policies for app and user patterns and behaviors can protect your users from using noncompliant or malicious apps, and limit the access of risky apps to your tenant data.

App governance supports the following types of policies:

| Policy type | Description |
| --- | --- |
| **Predefined policies** | App governance is equipped with a set of predefined policies tailored to your environment. Predefined policies allow you to start monitoring your apps even before you set up any policies. Use predefined policies to ensure that you're notified of any app anomalies early on. |
| **User defined policies** | In addition to predefined policies, admins can also use the available conditions to create their custom policies or pick from the available recommended policies. |

To see your list of current app governance policies, go to the **Microsoft Defender XDR &gt; Cloud apps &gt; App governance &gt; Policies** tab.

Note

Built-in threat detection policies are *not* listed on the **App governance** page. For more information, see [Investigate threat detection alerts](app-governance-anomaly-detection-alerts).

**To implement app policies**:

1. **[Work with predefined policies](app-governance-app-policies-overview#work-with-predefined-policies)**: App governance contains a set of out of the box policies to detect anomalous app behaviors. These policies are activated by default, but you can deactivate them if you choose to.
2. **[Create app policies:](app-governance-app-policies-create)** App governance offers over 20 policy conditions and templates for you to use. App governance policies help you:

    - Specify conditions by which app governance can alert you to app behavior for automatic or manual remediation.
    - Implement the app compliance policies for your organization.
3. **[Manage app policies](app-governance-app-policies-create#manage-app-policies)**: To keep up with the latest apps your organization is using, respond to new app-based attacks, and for ongoing changes to your app compliance needs, you might need to manage your app policies as follows:

    - Create new policies targeted at new apps
    - Change the status of an existing policy (active, inactive, audit mode)
    - Change the conditions of an existing policy
    - Change the actions of an existing policy for autoremediation of alerts

For more information, see [Learn about app policies](app-governance-app-policies-overview).

## Step 3: Detect and remediate app threats

Use app governance to monitor the threat alerts that are generated by built-in app governance detection methods for malicious app activities and policy-based alerts generated by active app policies that you create.

These alerts can indicate anomalies in app activity and when noncompliant, malicious, or risky apps are used. You can also use patterns in alerts to create new app policies or modify the settings of existing policies for more restrictive actions.

You can also remediate alerts, manually after investigation, or automatically through the action settings on active app policies.

**Do any of the following steps to detect and remediate threats**:

- **[Get started with app threat detection and remediation:](app-governance-detect-remediate-overview#view-alerts)** App governance collects threat alerts that are generated by built-in, machine-learning-driven app governance detection methods. The threat alerts are based on malicious app activities and policy-based alerts generated by active app policies that you create.
- **[Monitor and respond to apps with unusual data usage:](app-governance-detect-remediate-overview#monitor-and-respond-to-apps-with-unusual-data-usage)** App governance provides data usage information that can help you identify unwanted and potentially malicious app activity.
- **[Investigate anomaly detection alerts:](app-governance-anomaly-detection-alerts)** App governance provides security detections and alerts for malicious activities. The purpose of this guide is to provide you with general and practical information on each alert, to help with your investigation and remediation tasks.
- [**Remediate app threats:**](app-governance-manage-alerts) You remediate harmful app and app activity identified by app governance alerts in the Defender portal.

For more information, see [Learn about app threat detection and remediation](app-governance-detect-remediate-overview).