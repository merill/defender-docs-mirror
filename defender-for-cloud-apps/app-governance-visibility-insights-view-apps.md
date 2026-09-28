---
layout: Conceptual
title: View your OAuth app details with app governance - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/app-governance-visibility-insights-view-apps
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
description: Learn how to view app details with app governance in Microsoft Defender XDR with Microsoft Defender for Cloud Apps.
ms.reviewer: anandd512
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 81bdfa8e-8ad0-2142-2392-a625524d8907
document_version_independent_id: 81bdfa8e-8ad0-2142-2392-a625524d8907
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/app-governance-visibility-insights-view-apps.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: app-governance-visibility-insights-view-apps
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/app-governance-visibility-insights-view-apps.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 40de39e6-0254-aa47-9292-908c5f3e23fe
---

# View your OAuth app details with app governance - Microsoft Defender for Cloud Apps | Microsoft Learn

Use app governance to gain visibility and meaningful insights on your app ecosystem.

For example, view a list of apps in your tenant, together with relevant app metadata and usage data. Select a specific app to open its details pane and view more data and insights.

## Prerequisites

Your sign-in account must have one of the [required app governance roles](app-governance-get-started#roles) to view app governance data.

## View the apps in your tenant

For a summary of apps in your tenant, in Microsoft 365, go to **Cloud app &gt; App governance** and select any of the apps tabs.

By default, the app governance page sorts the grid alphabetically, by **App name**. To sort the list by another attribute, select the column name. You can also select **Search** to search for an app by name.

[![Screenshot of the Azure AD apps tab on the App governance page.](media/app-governance-visibility-insights-view-apps/app-governance-app-list-view.png)](media/app-governance-visibility-insights-view-apps/app-governance-app-list-view.png#lightbox)

On the **Microsoft 365** tab, the apps in your tenant are listed with the following details:

| Column name | Description |
| --- | --- |
| **App name** | The display name of the app as registered on Microsoft Entra ID |
| **App status** | Shows whether the app is enabled or disabled, and if disabled by whom |
| **Graph API access** | Shows whether the app has at least one Graph API permission |
| **Permission type** | Shows the app's permission type: <br>- **Delegated**: Delegated API permissions only, no roles.<br>- **Application**: Application API permissions only, no roles.<br>- **Microsoft Entra roles**: Microsoft Entra roles only, no API permissions.<br>- **Mixed**: A combination of any two or more of the above.<br>- **None**: No API permissions or Entra roles assigned. |
| **App origin** | Shows whether the app originated within the tenant or was registered in an external tenant |
| **Consent type** | Shows whether the app consent is given at the user or the admin level, and the number of users whose data is accessible to the app |
| **Publisher** | Publisher of the app and their verification status |
| **Last used** | Shows the last time when the app signed in. Tracking of this data goes back to June, 2022. |
| **Last modified** | Date and time when registration information was last updated on Microsoft Entra ID |
| **Added on** | Shows the date and time when the app was registered to Microsoft Entra ID and assigned a service principal |
| **Permission usage** | Shows whether the app has any unused Graph API permissions in the last 90 days |
| **Data usage** | Total data downloaded or uploaded by the app in the last 30 days |
| **Privilege level** | The app's privilege level |
| **Certification** | Indicates if an app meets stringent security and compliance standards set by Microsoft 365 or if its publisher has publicly attested to its safety |
| **App ID** | The app ID |
| **Sensitivity label accessed** | Sensitivity labels on content accessed by the app |
| **Service accessed** | Microsoft 365 services accessed by the app |
| **Community use** | Shows how popular the app is across all your users (*common*, *uncommon*, *rare*) |
| **Consent grants** | Shows all app consent grants in the last 30 days |
| **App activities** | Shows all app activities in the last 30 days |

## Get detailed information about an app

Select a specific app in the grid to view more details on an app details pane. Some tabs are available only for specific app types.

Company administrators can use the **Disable app** and **Enable app** controls in the details pane to enable or disable an app.

### Review app details on the Summary tab

The **Summary** tab shows more data about the app, such as the date first consented and the App ID. To see the properties of the app as registered in Microsoft Entra ID, select **View in Microsoft Entra ID**.

[![Screenshot of an app details pane with the Summary tab showing.](media/app-governance-visibility-insights-view-apps/app-governance-app-summary.png)](media/app-governance-visibility-insights-view-apps/app-governance-app-summary.png#lightbox)

### Review risk details on the Risk score tab

The **Risk score** tab shows a 1-100 risk score for the app, where higher values mean greater risk. The risk score helps you quickly prioritize which apps need attention first. The **Risk score** tab also shows the risk summary, including the factors behind the app's risk score.

Note

The Risk score tab is available only for OAuth apps registered in Microsoft Entra ID.

[![Screenshot of an app details pane with the Risk score tab showing.](media/app-governance-visibility-insights-view-apps/app-governance-app-risk-score.png)](media/app-governance-visibility-insights-view-apps/app-governance-app-risk-score.png#lightbox)

### Review app connections on the Graph tab

The **Graph** tab shows a visual identity graph that illustrates how the app connects to other entities in your organization, like users, resources, SaaS workloads, and critical assets. Select any node or edge in the graph to open a details pane with deeper context. When applicable, the graph details pane also shows attack paths involving the selected nodes or edges. To explore further, select **View in map** below the graph to open the full Attack Map experience in a new window.

The graph can also surface the AI agent behind an app. For OAuth apps tied to Microsoft Copilot Studio agents, expand the OAuth app node to view the connected agent.

Note

The Graph tab is available only for OAuth apps registered in Microsoft Entra ID.

[![Screenshot of an app details pane with the Graph tab showing.](media/app-governance-visibility-insights-view-apps/app-governance-app-graph.png)](media/app-governance-visibility-insights-view-apps/app-governance-app-graph.png#lightbox)

### Review app activity on the Data usage tab

The **Data usage** tab shows a graph of data usage over time, for Exchange, SharePoint, OneDrive, and Teams resources via Microsoft Graph and Exchange Web Services (EWS) APIs. The **Data usage** tab supports filtering usage insights by priority accounts only.

[![Screenshot of the Data usage tab.](media/app-governance-visibility-insights-view-apps/app-governance-app-data-usage.png)](media/app-governance-visibility-insights-view-apps/app-governance-app-data-usage.png#lightbox)

### Review user access on the Users tab

The **Users** tab shows a list of users who are using the app, whether they're a priority account, and the amount of data downloaded and uploaded.

If an app has been granted admin consent (approved for the entire organization by an administrator), the **Total consented users** are all users in the tenant.

[![Screenshot of an app details pane with the Users tab showing.](media/app-governance-visibility-insights-view-apps/app-governance-app-users.png)](media/app-governance-visibility-insights-view-apps/app-governance-app-users.png#lightbox)

### Review app permissions on the Permissions tab

The **Permissions** tab shows a summary and list of the Graph API and legacy permissions granted to the app, consent type, privilege level, and whether they're in use. This also shows the Microsoft Entra roles granted to the app, including its type (built-in or custom), privilege level, and whether it grants tenant-wide access. Select a role to view its granular permissions, descriptions, and privilege levels.

Note

Only directly assigned Microsoft Entra roles are shown. Roles inherited through group membership and Azure role-based access control (Azure RBAC) roles aren't included.

[![Screenshot of the Permissions tab.](media/app-governance-visibility-insights-view-apps/app-governance-app-permissions.png)](media/app-governance-visibility-insights-view-apps/app-governance-app-permissions.png#lightbox)

For more information, see the [Microsoft Graph permissions reference](/en-us/graph/permissions-reference).

### Review sensitivity labels on the Sensitivity labels tab

The **Sensitivity labels** tab shows how frequently items with certain sensitivity labels were accessed by the app on Microsoft 365.

[![Screenshot of the Sensitivity labels tab.](media/app-governance-visibility-insights-view-apps/app-governance-app-sensitive-labels-details.png)](media/app-governance-visibility-insights-view-apps/app-governance-app-sensitive-labels-details.png#lightbox)

## Manage Google Workspace and Salesforce OAuth apps

If you enable the [Google Workspace](connect-google-workspace) or [Salesforce](connect-salesforce) connector, you can use the **App governance** page to view information about app permissions in apps connected to Google Workspace and Salesforce. You can view the permissions granted to each app and revoke or block apps as needed.

On the **App governance** page, select the **Google apps** or **Salesforce apps** tabs to view your apps. For example:

[![Screenshot of the Google apps tab](media/app-governance-visibility-insights-view-apps/google-apps.png)](media/app-governance-visibility-insights-view-apps/google-apps.png#lightbox)

To manage your Google Workspace or Salesforce apps on the **App governance** page, use the following options:

| Option | Description |
| --- | --- |
| **Queries** | Use the filtering options at the top of the page to define or load a saved query. By default, the **App governance** page has a set of saved, basic queries, with one applied as a default filter. Do any of the following actions to change the filter applied as needed: <br>- Select **Save as** to save your updated filter.<br>- Select **Select a query** to select a different saved query, such as **Apps authorized by admins** or **Apps authorized by external users**<br>- Select the **Advanced filters** toggle on the right to add more filtering options. Select a filter, an operator, and the value you want to filter by. |
| **Bulk selection** | Select to either select all listed apps, or clear the selection on all selected apps. |
| **New policy from search** | Select to create a new OAuth app policy based on the current query results, For more information, see [Create app policies in app governance](app-governance-app-policies-create). |
| **Export** | Select to export the currently listed apps to a CSV file. |

### View Google Workforce and Salesforce OAuth app details

The **Google** and **Salesforce** pages provide the following information about each OAuth app that users grant permissions to:

| Column name | Description |
| --- | --- |
| **Name** | The app's name. Select to show or hide more details about the app. |
| **Authorized by** | The number of users who authorized this app to access their app's account, and granted the app permissions. Select to view more information, including a list of user emails and whether an admin previously consented to the app. On the **Users who added...** pane, select **Export** to export the listed users to a CSV file. |
| **Permission level** | *High*, *Medium*, or *Low*. The level indicates how much access this app has to the app's data. For example, *Low* might indicate that the app only accesses user profile and name. Select the level to view more information, including permissions granted to the app, community use, or related activity in the [Governance log](/en-us/defender-cloud-apps/governance-actions). |
| **Last authorized** | The most recent date on which a user granted permissions to this app. This information is available for Salesforce only. |
| **Actions** | Select an option to mark an app as approved or banned. |

Select **Show details** at the top right to view more information about all of the apps displayed, including:

| Column name | Description |
| --- | --- |
| **Permissions** | A list of all permissions currently granted to the app. Available for Google Workspace and Salesforce (Preview). |
| **Community use** | Common, Uncommon, Rare. Indicates how popular the app is across all your users. |
| **App ID** | The app's ID |
| **App activities** | A link to the app's activity log, which you can use to understand the app's recent usage. |
| **Last used** | The most recent date on which this app was used by anyone in your organization. This information is available for Salesforce only. |