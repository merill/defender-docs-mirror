---
layout: Conceptual
title: OAuth app visibility and insights with app governance - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/app-governance-visibility-insights-overview
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
ms.topic: concept-article
description: Learn about visibility and insights available for app governance with Microsoft Defender for Cloud Apps in Microsoft Defender XDR.
ms.reviewer: shragar
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: f7481f78-2987-1cda-5d81-70caa5b8b8fd
document_version_independent_id: f7481f78-2987-1cda-5d81-70caa5b8b8fd
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/app-governance-visibility-insights-overview.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: app-governance-visibility-insights-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/app-governance-visibility-insights-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/7428317a-e6c2-4461-ad3e-8a8ad3608734
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/e4f59707-f107-48f2-8d75-0afd91868cd7
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
platformId: deef384d-4b88-5668-1a75-92bc2663b2d6
---

# OAuth app visibility and insights with app governance - Microsoft Defender for Cloud Apps | Microsoft Learn

Use app governance to gain visibility and meaningful insights on your app ecosystem.

For example, view a list of the OAuth-enabled apps registered to Microsoft Entra ID in your tenant, and react or respond to a rich view on app activities.

## Required administrator roles

For more information, see [App governance roles](app-governance-get-started#roles).

## Visibility and insight scope

App governance provides access to the following data:

- A dashboard of all insights on the **App governance &gt; Overview** tab
- Data accessed and permissions used by all apps with workload and user level insights.
- App information and metadata, such as Graph API and legacy permissions, registration date, last used date and certification.
- Publisher information and metadata, such as name and verification status.
- Usage of top resources, such as emails and files throughout the tenant.
- A cumulative view of users accessing apps.
- Insights on alerts, policies, and the following entities:

    - High-privileged apps.
    - Overprivileged apps.
    - Unused apps.
    - High-usage apps.
    - Top consented users whose data a specific app can access.
    - Priority accounts who have data that a specific app can access.
    - OAuth applications that have accessed sensitive or regular content on SharePoint, OneDrive, Exchange Online, or Teams.

Also use the **App governance** page to:

- Drill down to a single app details page, with all associated insights
- Understand top users and priority accounts based on app governance data
- Export a list of your apps plus respective insights

## Limitations to Microsoft 365 activity insights

To provide insights into how OAuth apps use Microsoft 365 data, including data with sensitivity labels, app governance tracks a set of commonly used Graph API operations.

While these insights don’t cover all app activity on Microsoft 365, they can flag risky behavior associated with increased data usage and access to potentially sensitive data.

To get detailed information about app activity on Microsoft 365, search the Microsoft Purview audit log. For more information, see [Microsoft Purview documentation](/en-us/microsoft-365/compliance/audit-log-search).

## Get started with visibility and insights

Start by viewing the [app governance dashboard](https://aka.ms/appgovernance) on the **App governance &gt; Overview** tab in the Microsoft Defender Portal.

Your sign-in account must have one of the [required app governance administrator roles](app-governance-get-started#roles) to view any app governance data.

For example:

[![Screenshot of the App governance overview page in Microsoft Defender XDR.](media/app-governance-visibility-insights-get-started/overview.png)](media/app-governance-visibility-insights-get-started/overview.png#lightbox)

### What's available on the Overview tab

The dashboard on the **Overview** tab contains a summary of your app ecosystem:

| Dashboard element | Description |
| --- | --- |
| **Tenant summary** | The count of key app and incident categories. |
| **Latest incidents** | The 10 most recent active incidents in the tenant |
| **Data usage** | Mouse over each month column in the graph to see the corresponding value: - **Total data usage**: Tracks total data accessed by all apps in the tenant through Graph API over the last four calendar months. Currently includes emails, files, and chat and channel messages read and written by apps that access Microsoft 365 using Graph API. - **Data usage by resource type**: Data usage over the last four calendar months, broken down by resource type. Currently includes emails, files, and chat and channel messages read and written by apps that access Microsoft 365 using Graph API. |
| **Apps that accessed data in Microsoft 365 services** | The count of apps that have accessed data with and without sensitivity labels on SharePoint, OneDrive, Exchange Online, and Teams in the last 30 days. For example, in the screenshot above, 99 apps accessed OneDrive in the last 30 days, out of which 27 apps accessed data with sensitivity labels. |
| **Sensitivity labels accessed** | Count of apps that accessed labeled data in SharePoint, OneDrive, Exchange Online, and Teams in the last 30 days, sorted by the count. For example, in the screenshot above, 90 apps accessed confidential data on SharePoint, OneDrive, Exchange Online, and Teams. |
| **Predefined policies** | Count of active and total predefined policies that identify risky apps, such as apps with excessive privileges, unusual characteristics, or suspicious activities. |
| **App categories** | The top apps sorted by these categories: - **All categories**: Sorts by all available categories. - **Highly privileged**: High privilege is an internally determined category based on platform machine learning and signals. - **Risky apps**: Apps with a high risk score. - **Overprivileged**: When app governance receives data that indicates that a permission granted to an application hasn't been used in the last 90 days, that application is overprivileged. App governance must be operating for at least 90 days to determine if any app is overprivileged. - **Unused**: Apps that have not signed in within the last 90 days - **Unverified publisher**: Applications that haven't received [publisher certification](/en-us/azure/active-directory/develop/publisher-verification-overview) are considered unverified. - **App only permissions**: [Application permissions](/en-us/azure/active-directory/develop/v2-permissions-and-consent#permission-types) are used by apps that can run without a signed-in user present. Apps with permissions to access data in the tenant are potentially a higher risk.- **New apps**: New apps that have been registered in the last seven days. |

### View app insights

One of the primary value points for app governance is the ability to quickly view app alerts and insights.

**To view insights for your apps**:

1. On the **App governance** page, select one of the apps tabs to display your apps.

    The apps listed depend on the apps present in your tenant.
2. Filter the apps listed using one or more of the following default filter options:

    - **API access**
    - **Risk score**
    - **Privilege level**
    - **Permission**
    - **Permission usage**
    - **App origin**
    - **Permission type**
    - **Roles** (built-in Microsoft Entra roles only)
    - **Publisher verified**
    - **Last used**
    - **Services accessed**
    - **Sensitivity labels accessed**

        Use one of the following nondefault filters to further customize the apps listed:

        - **Last modified**
        - **Added on**
        - **Certification**
        - **Users**
        - **Data usage**

    Tip

    Save the query to save the currently selected filters for use again in the future.
3. Select the name of an app to view more details. For example:

    [![Screenshot of the app details pan showing an app summary.](media/app-governance-visibility-insights-get-started/app-governance-app-list-view.png)](media/app-governance-visibility-insights-get-started/app-governance-app-list-view.png#lightbox)

The details pane lists the app usage over the past 30 days, the users who have consented to the app, and the permissions assigned to the app.

For example, an administrator might review the activity and permissions of an app that is generating alerts and make a decision to disable the app using the **Disable App** button towards the bottom of the app details pane.