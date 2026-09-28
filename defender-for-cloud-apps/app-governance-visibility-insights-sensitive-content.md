---
layout: Conceptual
title: View and regulate OAuth app access to sensitive content with app governance - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/app-governance-visibility-insights-sensitive-content
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
description: Identify which Microsoft 365 services apps access and determine whether they have accessed content protected with sensitivity labels.
ms.reviewer: anandd512
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: c0e7840a-ebcf-921a-32d1-9f9cfb998099
document_version_independent_id: c0e7840a-ebcf-921a-32d1-9f9cfb998099
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/app-governance-visibility-insights-sensitive-content.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: app-governance-visibility-insights-sensitive-content
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/app-governance-visibility-insights-sensitive-content.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/9d7be3ef-f27c-4c7f-9eba-67c3cd429995
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/feeb50f3-b677-44f9-b3a6-5f2f58182b0d
platformId: a3a4590e-abd6-af70-cccf-7bde19013c3d
---

# View and regulate OAuth app access to sensitive content with app governance - Microsoft Defender for Cloud Apps | Microsoft Learn

App governance lets you quickly identify the Microsoft 365 services apps have accessed and if these apps have accessed content with sensitivity labels. This article explains how to view app access details, review sensitivity label exposure across services like SharePoint, OneDrive, and Exchange Online, and set up policies to regulate access to sensitive content.

## View apps that access sensitive content

To view apps that have accessed data across Microsoft 365 services, select **View apps** from the relevant card on the **Overview** tab. For example

![Screenshot of the Apps that accessed Microsoft Entra services card.](media/app-governance-visibility-insights-sensitive-content/image7.png)

You can also select a label listed under **Sensitivity labels access** on any app tab, such as the **Microsoft Entra apps** tab. App governance then shows how many times the app accessed that label in the last 30 days for each service type. For example:

![Screenshot of the Sensitivity labels tab on the Microsoft Entra apps tab.](media/app-governance-visibility-insights-sensitive-content/sensitive-labels-details.png)

In this example, the app accessed *Highly confidential* content seven times on SharePoint, 15 times on OneDrive, and 25 times on Exchange Online in the last 30 days.

## Regulate access to sensitive content

The built-in **Access to sensitive data** policy sends alerts when an app accesses sensitive content.

You can change this policy to:

- Select **Disable app** as the action so that apps that trigger alerts are turned off.
- Change the policy scope to include or exclude specific apps.

For more options, create a custom policy. Use the **Sensitivity labels accessed** condition with other [custom policy conditions](app-governance-app-policies-create#custom-policies).