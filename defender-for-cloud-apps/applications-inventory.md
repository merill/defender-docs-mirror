---
layout: Conceptual
title: Application inventory - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/applications-inventory
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: anandd512
manager: bagol
ms.author: andeshpande
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
ms.date: 2026-09-28T00:00:00.0000000Z
ms.topic: overview
ms.reviewer: anandd512
description: Learn how the Applications page in Microsoft Defender centralizes SaaS and OAuth app inventory so you can review risk, permissions, and usage.
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 4bbe39a6-d832-6866-5cba-33ed5ef20ce0
document_version_independent_id: 4bbe39a6-d832-6866-5cba-33ed5ef20ce0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/applications-inventory.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: applications-inventory
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/applications-inventory.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 63ecb454-3903-e7e7-30e9-95f986cc688f
---

# Application inventory - Microsoft Defender for Cloud Apps | Microsoft Learn

Protecting your SaaS ecosystem requires taking inventory of all SaaS and connected OAuth apps that are in your environment. With the increasing number of applications, having a comprehensive inventory is crucial to ensure security and compliance. The Applications page provides a centralized view of all SaaS and connected OAuth apps in your organization, enabling efficient monitoring and management.

At a glance, you can see information such as app name, risk score, privilege level, publisher information, and other details for easy identification of SaaS and OAuth apps most at risk.

The Applications page includes the following tabs:

- SaaS apps: A consolidated view of all SaaS applications in your network. This tab highlights key details, including app name, status (unprotected/protected app) and whether the app is marked as sanctioned or unsanctioned.
- OAuth apps: A comprehensive view of OAuth apps registered on Microsoft Entra ID, Google Workspace, and Salesforce. This tab highlights OAuth app metadata, publisher information, app origin, permissions used, data accessed, and other insights.

## Navigate to the Applications page

In the Defender portal at https://security.microsoft.com, go to **Assets** &gt; **Applications**. Or, go directly to the **Applications** page, by clicking on the banner links on the existing Cloud discovery and App governance pages.

[![Screenshot of the Cloud Discovery page with a banner about the new unified application inventory experience.](media/banner-on-cloud-discovery-pages.png)](media/banner-on-cloud-discovery-pages.png#lightbox)

[![Screenshot of the App Governance page with a banner about the new unified application inventory experience for managing OAuth and SaaS apps](media/banner-message-on-app-governance-pages.png)](media/banner-message-on-app-governance-pages.png#lightbox)

There are several options you can choose from to customize the SaaS apps and OAuth apps list view. In the top navigation panel you can:

- Add or remove columns.
- Export the entire list in CSV format.
- Select the number of items to show per page.
- Apply filters.

Note

When exporting the applications list to a CSV file, a maximum of 1000 SaaS or OAuth apps are displayed.

The following image depicts the SaaS apps list: [![Screenshot of the applications tab in the Defender portal.](media/applications-tab-in-the-defender-portal.png)](media/applications-tab-in-the-defender-portal.png#lightbox)

## SaaS app details

At the top of the SaaS apps tab, you can find actionable insights that allow you to quickly identify apps that need your attention. The following details are displayed:

- **Untagged high-risk apps** - Shows apps that aren't tagged and have a high risk score.
- **Untagged high-traffic apps** - Shows apps that aren't tagged and have high usage traffic (greater than 1 GB of data traffic).
- **Untagged GenAI apps** - Shows apps that aren't tagged and are based on generative AI.

## Sort and filter the SaaS apps list

Use sorting and filtering to focus the SaaS apps list on the applications you want to assess and manage. For filter descriptions and query options, see [Filter and query discovered apps](discovered-app-queries#discovered-app-filters).

## OAuth app details

The OAuth apps tab provides visibility into OAuth apps from Microsoft Entra ID, Salesforce, and Google Workspace. Admins can review applications and decide to disable the apps or apply policies to monitor their behavior in their environment.

The OAuth app inventory includes the following app types:

- **Entra ID**: Service principals registered in Microsoft Entra ID. These apps access resources through API permissions or Microsoft Entra role assignments.
- **Salesforce**: OAuth apps connected through Salesforce. The inventory includes both Connected Apps and External Client Apps (ECAs).
- **Google Workspace**: OAuth apps connected through Google Workspace. Users authorize these apps, which have varying levels of access to Google Workspace resources.

Actionable insights appear at the top of the OAuth apps tab. Select an insight to filter the list to the matching apps so you can quickly identify apps that need review.

| Insight | Description | Available for |
| --- | --- | --- |
| **New apps** | Apps added in the last 30 days. | Microsoft 365 |
| **Highly privileged apps** | Apps with powerful permissions that allow them to access data or change important settings. For Salesforce, includes Connected Apps and External Client Apps (ECAs) whose granted permissions are classified as **High**. | Microsoft 365, Google Workspace, Salesforce |
| **Risky apps** | Apps with a high risk score. | Microsoft 365, Google Workspace, Salesforce |
| **Unused apps** | Apps that haven't signed in within the last 90 days. For Salesforce, includes Connected Apps and ECAs that haven't been used for more than 90 days based on the last used date. | Microsoft 365, Google Workspace, Salesforce |
| **Overprivileged apps** | Apps with unused permissions. | Microsoft 365 |
| **Apps from external unverified publishers** | Apps that originated from an external unverified publisher tenant. | Microsoft 365 |
| **Used by AI Agents** | Apps identified as being used by AI agent platforms. | Microsoft 365 |

For more information on how to create app policies, see [Create app policies in app governance](app-governance-app-policies-create).

The following image shows the OAuth apps list:

[![Screenshot of the OAuth apps inventory showing Entra ID, Salesforce, and Google Workspace app types.](media/oauth-tab-in-the-applications-page.png)](media/oauth-tab-in-the-applications-page.png#lightbox)

## Sort and filter the OAuth apps list

Use sorting and filtering to focus the OAuth apps list on the applications you want to investigate. For the available columns and filters, see [View your OAuth app details with app governance](app-governance-visibility-insights-view-apps#view-the-apps-in-your-tenant) and [View app insights](app-governance-visibility-insights-overview#view-app-insights).