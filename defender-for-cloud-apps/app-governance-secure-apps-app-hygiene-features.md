---
layout: Conceptual
title: Secure OAuth apps with app governance hygiene features - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/app-governance-secure-apps-app-hygiene-features
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
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
description: Use app governance hygiene features to identify unused apps, manage unused credentials, and review expiring credentials in Microsoft Defender.
ms.reviewer: anandd512
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 7a9b916a-6d36-92bb-6dfa-2916a9d1fc16
document_version_independent_id: 7a9b916a-6d36-92bb-6dfa-2916a9d1fc16
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/app-governance-secure-apps-app-hygiene-features.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: app-governance-secure-apps-app-hygiene-features
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/app-governance-secure-apps-app-hygiene-features.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f233afb4-f511-4877-ab18-c53e36c47c54
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/aa758f63-7086-440d-afba-dcb5819f0b6f
platformId: 204760be-dda2-8c02-d3b8-92687a1a58c5
---

# Secure OAuth apps with app governance hygiene features - Microsoft Defender for Cloud Apps | Microsoft Learn

Note

Management of unused credentials and expiring credentials is available to app governance customers with a Microsoft Entra Workload ID Premium license. For more information, see [What are workload identities?](/en-us/azure/active-directory/workload-identities/workload-identities-overview)

Have you ever wanted to find apps that your organization owns but doesn't use? Or clean up unused or expiring credentials more easily? Microsoft Entra ID includes recommendations to help you identify such apps. The **App governance** page in Microsoft Defender provides an app hygiene feature suite with controls and insights on unused apps, unused credentials, and expiring credentials.

App hygiene features enable automatic control over flagged apps and provide extra behavior context to help you determine the risk each app poses in your environment.

Watch this video for a brief explanation of the app hygiene features for unused apps, unused credentials, and expiring credentials:

## Review app insights

App governance allows you to sort and filter on app last used date, credential unused since, and credential expiration date. You can export the filtered app list for easy reporting and triage across your organization.

- Due to data history or app scope constraints, some apps show *Over 30 days ago* in the **Last used** or **Credential unused since** column. These apps haven't signed in the last 30 days, but we don't currently have an exact last sign-in date.
- Apps that don't have a last sign-in date or credential expiration date available have *Not available* in the respective column.
- Apps with *No credentials* in the **Credential unused since** or **Credential expiration** column don’t have any credentials assigned to the app.

## Create app hygiene policies

App governance provides customizable policies for unused apps, apps with unused credentials, and apps with expiring credentials.

For example, create a policy to automatically disable any app that hasn’t been used in the past 90 days, has high privilege permissions, and can access [priority accounts in Microsoft 365](/en-us/microsoft-365/admin/setup/priority-accounts). Like all app governance alerts, these alerts are aggregated into incidents in your Defender alerts queue and flow to Advanced hunting and Microsoft Sentinel.

The following image shows an example of policy conditions for an app hygiene policy:

![Screenshot of the Edit policy conditions page.](media/app-governance/edit-policy-conditions.png)

Clean up unused apps and expiring credentials to keep your SaaS app inventory lean. This helps you cut SaaS spend and reduce your app attack surface.