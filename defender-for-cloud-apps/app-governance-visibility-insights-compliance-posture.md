---
layout: Conceptual
title: Determine your OAuth app compliance posture with app governance - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/app-governance-visibility-insights-compliance-posture
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
ms.topic: concept-article
description: Determine your app compliance posture with app governance in Microsoft Defender XDR with Microsoft Defender for Cloud Apps.
ms.reviewer: shragar
locale: en-us
document_id: 58f4835e-5228-bfd6-5608-5384ff3689dd
document_version_independent_id: 58f4835e-5228-bfd6-5608-5384ff3689dd
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/app-governance-visibility-insights-compliance-posture.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: app-governance-visibility-insights-compliance-posture
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/app-governance-visibility-insights-compliance-posture.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: af8e90cb-594c-d8c7-a222-0f524e1323fd
---

# Determine your OAuth app compliance posture with app governance - Microsoft Defender for Cloud Apps | Microsoft Learn

This article describes the cards shown on the **App governance &gt; Overview** page with compliance posture data.

The **Overview** page shows the following details:

| Apps / incidents | Details shown | Use this data to... |
| --- | --- | --- |
| **OAuth-enabled apps that use the Microsoft Graph API** | - How many apps are in your tenant  - How many apps are unused in the last 90 days  - How many apps might be overprivileged  - How many apps are highly privileged | Determine the level of risk to your organization by unused, overprivileged and highly privileged apps. |
| **For incidents** | - How many active incidents your tenant has - How many are based on app governance detections (**Threat incidents**)  - How many are based on app policies you have in place (**Policy incidents**) - The 10 latest incidents | Determine how quickly incidents are being generated and the relative number of detected and policy-based incidents. |

For example:

![Screenshot showing relative number of detected and policy-based incidents.](media/incidents-summary1.png)

![Screenshot showing top alerts.](media/app-governance-visibility-insights-compliance-posture/top-alerts.png)

## Data usage cards

Data usage cards show the following types of information:

- **Total data accessed by apps** in the tenant through Microsoft Graph and EWS APIs over the current month and previous three calendar months. (Currently includes emails, files, and chat and channel messages read and written by apps that access Microsoft 365 using Microsoft Graph and EWS APIs)
- **Data usage over the current month and previous three calendar months**, broken down by resource type. (Currently includes emails, files, and chat and channel messages read and written by apps that access Microsoft 365 using Microsoft Graph and EWS APIs)

For example:

![Screenshot showing total data accessed by apps.](media/app-governance-visibility-insights-compliance-posture/data-usage-chart.png)

## Apps that access data on Microsoft 365

For apps that access data on Microsoft 365, cards show the number of apps that have accessed data on SharePoint, OneDrive, Exchange Online, or Teams using Microsoft Graph and EWS APIs in the last 30 days.

For example:

![Screenshot showing apps that have accessed data on SharePoint, OneDrive, Exchange Online, or Teams in the last 30 days.](media/app-governance-visibility-insights-compliance-posture/apps-accessed-m365-services-chart.png)

## Sensitivity labels accessed

For sensitivity labeling data, cards show the number apps that have accessed content with sensitivity labels on SharePoint, OneDrive, Exchange Online or Teams using Microsoft Graph and EWS APIs in the last 30 days.

For example:

The number of apps that have accessed content with sensitivity labels.

![Screenshot showing the number of apps that have accessed content with sensitivity labels.](media/sensitive-data-accessed-chart1.png)