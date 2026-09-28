---
layout: Conceptual
title: Application inventory - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/applications-inventory
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
ms.date: 2026-06-14T00:00:00.0000000Z
ms.topic: overview
ms.reviewer: anandd512
description: The new Applications page located under Assets in the Microsoft Defender portal provides a centralized location for users to view and manage SaaS and SaaS connected OAuth apps information across their environment, ensuring optimal visibility and a comprehensive experience
ms.custom: sfi-image-nochange
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
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 63ecb454-3903-e7e7-30e9-95f986cc688f
---

# Application inventory - Microsoft Defender for Cloud Apps | Microsoft Learn

Protecting your SaaS ecosystem requires taking inventory of all SaaS and connected OAuth apps that are in your environment. With the increasing number of applications, having a comprehensive inventory is crucial to ensure security and compliance. The Applications page provides a centralized view of all SaaS and connected OAuth apps in your organization, enabling efficient monitoring and management. At a glance you can see information such as app name, risk score, privilege level, publisher information, and other details for easy identification of SaaS and OAuth apps most at risk.

The Applications page includes the following tabs:

- SaaS apps: A consolidated view of all SaaS applications in your network. This tab highlights key details, including app name, status (unprotected/protected app) and whether the app is marked as sanctioned or unsanctioned.
- OAuth apps: A comprehensive view of OAuth apps registered on Microsoft Entra ID, Google workspace and Salesforce. This tab highlights OAuth apps metadata, publisher info and app origin, permissions used, data accessed and other insights.

## Navigate to the Applications page

In the Defender portal at https://security.microsoft.com, go to **Assets** &gt; **Applications**. Or, go directly to the **Applications** page, by clicking on the banner links on the existing Cloud discovery and App governance pages.

[![Screenshot of the Cloud Discovery page with a banner about the new unified application inventory experience.](media/banner-on-cloud-discovery-pages.png)](media/banner-on-cloud-discovery-pages.png#lightbox)

[![Screenshot of the App Governance page with a banner about the new unified application inventory experience for managing OAuth and SaaS apps](media/banner-message-on-app-governance-pages.png)](media/banner-message-on-app-governance-pages.png#lightbox)

There are several options you can choose from to customize the SaaS apps and OAuth apps list view. In the top navigation panel you can:

- Add or remove columns.
- Export the entire list in CSV format.
- Select the number of items to show per page.
- Apply filters

Note

When exporting the applications list to a CSV file, a maximum of 1000 SaaS or OAuth apps are displayed.

The following image depicts the SaaS apps list: [![Screenshot of the applications tab in the Defender portal](media/applications-tab-in-the-defender-portal.png)](media/applications-tab-in-the-defender-portal.png#lightbox)

## SaaS app details

At the top of Saas app tab, you can find actionable insights that allow you to quickly identify apps that need your attention and focus. The following details are displayed:

- **Untagged high risk apps** – Shows apps that aren't tagged and have a high-risk.
- **Untagged high traffic apps** – Shows apps that aren't tagged and have a high usage traffic (greater than 1 GB of data traffic).
- **Untagged GenAI apps** – Shows apps that aren't tagged and are Gen-AI based.

## Sort and filter the SaaS apps list

You can use the sort and filter functionality to get a more focused view. These controls also help you assess and manage the SaaS applications in your organization.

| Filter | Description |
| --- | --- |
| **App tags** | Select **Sanctioned**, **Unsanctioned**, or create custom tags to use in a customized filter. |
| **App** | Filter for specific SaaS apps. |
| **Categories** | Filter according to app categories. |
| **Compliance risk factor** | Filter for specific standards, certifications, and compliance your app might comply with. For example: HIPAA, ISO 27001, SOC 2, and PCI-DSS. |
| **Risk score** | Filter by a specific risk score, such as to view only risky apps. |
| **Security risk factor** | Filter based on specific security measures, such as encryption at rest, multifactor authentication, and others. |
|  |  |

### OAuth Apps

The OAuth apps tab provides visibility into Microsoft 365, Google workspace and Salesforce. Admins can review applications and decide to disable the apps or apply policies to monitor their behavior in their environment.

Actionable insights appear at the top of the OAuth apps tab. Select an insight to filter the list to the matching apps so you can quickly identify apps that need review.

| Insight | Description | Available for |
| --- | --- | --- |
| **New apps** | Apps added in the last 30 days. | Microsoft 365 |
| **Highly privileged apps** | Apps with powerful permissions that allow them to access data or change important settings. For Salesforce, includes Connected Apps and External Client Apps (ECAs) whose granted permissions are classified as **High**. | Microsoft 365, Google Workspace, Salesforce (Preview) |
| **Unused apps** | Apps that haven't signed in within the last 90 days. For Salesforce, includes Connected Apps and ECAs that haven't been used for more than 90 days based on the last used date. | Microsoft 365, Salesforce (Preview) |
| **Overprivileged apps** | Apps with unused permissions. | Microsoft 365 |
| **Apps from external unverified publishers** | Apps that originated from an external unverified publisher tenant. | Microsoft 365 |

For more information on how to create app policies, see [Create app policies in app governance](app-governance-app-policies-create).

The following image depicts the OAuth apps list:

[![Screenshot of a list of OAuth apps in the applications page in the Defender portal](media/oauth-tab-in-the-applications-page.png)](media/oauth-tab-in-the-applications-page.png#lightbox)

## Sort and filter the OAuth apps list

You can apply the following filters to get a more focused view:

| Column name | Description |
| --- | --- |
| **App name** | The display name of the app as registered on Microsoft Entra ID, or the connected app name in Google Workspace or Salesforce. |
| **App status** | Shows whether the app is enabled or disabled, and if disabled by whom. |
| **Graph API access** | Shows whether the app has at least one Graph API permission. (Microsoft 365 only.) |
| **Permission type** | Shows whether the app has application (app only), delegated, or mixed permissions. (Microsoft 365 only.) |
| **App origin** | Shows whether the app originated within the tenant or was registered in an external tenant. |
| **Consent type** | Shows whether the app consent has been given at the user or the admin level, and the number of users whose data is accessible to the app. |
| **Publisher** | Publisher of the app and their verification status. |
| **Last used** | Date and time when the app last signed in. For Microsoft 365, tracking goes back to June 2022. For Salesforce, requires [Salesforce real-time event monitoring (Preview)](protect-salesforce#enable-salesforce-real-time-event-monitoring-preview) to be enabled. |
| **Last modified** | Date and time when registration information was last updated on Microsoft Entra ID. |
| **Added on** | Shows the date and time when the app was registered to Microsoft Entra ID and assigned a service principal. |
| **Permission usage** | Shows whether the app has any unused Graph API permissions in the last 90 days. (Microsoft 365 only.) |
| **Data usage** | Total data downloaded or uploaded by the app in the last 30 days. (Microsoft 365 only.) |
| **Privilege level** | The app's privilege level (High, Medium, or Low). Available for Microsoft 365, Google Workspace, and Salesforce. For Salesforce, requires [Salesforce real-time event monitoring (Preview)](protect-salesforce#enable-salesforce-real-time-event-monitoring-preview) to be enabled. |
| **Certification** | Indicates if an app meets stringent security and compliance standards set by Microsoft 365 or if its publisher has publicly attested to its safety. |
| **Sensitivity label accessed** | Sensitivity labels on content accessed by the app. (Microsoft 365 only.) |
| **Service accessed** | Microsoft 365 services accessed by the app. |
| **App ID** | The app's unique identifier. For Salesforce, the **App ID** lets you pivot from a Salesforce threat detection alert directly to the matching OAuth app page. |
| **Type** | For Salesforce, indicates whether the app is a **Connected App** or an **External Client App (ECA)**. Use the **Type** filter to narrow the Salesforce inventory. |

Tip

To see all columns, you might need to do one or more of the following steps:

- Horizontally scroll in your web browser.
- Narrow the width of appropriate columns.
- Zoom out in your web browser.