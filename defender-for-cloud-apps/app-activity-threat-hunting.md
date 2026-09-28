---
layout: Conceptual
title: Hunt for threats in app activities - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/app-activity-threat-hunting
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
ms.date: 2026-08-07T00:00:00.0000000Z
ms.topic: how-to
description: Learn how app governance in Microsoft Defender for Cloud Apps helps you hunt for resources accessed and activities carried out by apps in your environment.
ms.reviewer: shragar
ms.custom: sfi-image-nochange, msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: d894cda4-f715-539f-e17d-a2b7a0449aac
document_version_independent_id: d894cda4-f715-539f-e17d-a2b7a0449aac
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/app-activity-threat-hunting.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: app-activity-threat-hunting
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/app-activity-threat-hunting.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 2b1a165e-7e4c-8a14-0d83-3cf28db62c49
---

# Hunt for threats in app activities - Microsoft Defender for Cloud Apps | Microsoft Learn

Apps can be a valuable entry point for attackers, so we recommend monitoring anomalies and suspicious behaviors that use apps. While investigating an app governance alert or reviewing the app behavior in the environment, it becomes important to quickly get visibility into details of activities done by such suspicious apps and take remediation actions to protect assets in your organization.

Using app governance and advanced hunting capabilities, you can get complete visibility into activities done by the apps and the resources the app has accessed.

This article describes how you can simplify app-based threat hunting using app governance in Microsoft Defender for Cloud Apps.

## Step 1: Find the app in app governance

The Defender for Cloud Apps **App governance** page lists [all Microsoft Entra ID OAuth apps](https://security.microsoft.com/cloudapps/app-governance?viewid=allApps).

If you're looking to get more details on the data accessed by a specific app, search for that app on the app list in app governance. Alternatively, use the **Data usage** or **Services accessed** filters to view apps that have accessed data on one or more of the supported Microsoft 365 services.

## Step 2: View data accessed by apps

1. Once you’ve identified an app, select the app to open the app details pane.
2. Select the **Data usage** tab on the app details pane to view information on the size and count of resources accessed by the app in the last 30 days.

For example:

![Screenshot of the app details pane with data usage details.](media/app-governance-secure-apps-app-hygiene-features/data-usage.png)

App governance provides data usage-based insights for resources such as emails, files, and chat and channel messages across Exchange Online, OneDrive, SharePoint and Teams.

## Step 3: Hunt for related activities and resources accessed

Once you have a high-level overview of the data used by the app across services and resources, you may want to know the details of the app activities and the resources it accessed while performing these activities.

1. Select the **go-hunt** icon next to each resource to view details of the resources accessed by the app in the last 30 days. A new tab is opened, redirecting you to the **Advanced hunting** page with a prepopulated KQL query.
2. Once the page loads, select the **Run query** button to run the KQL query and view the results.

After the query runs, the query results display in tabular form. Each row in the table corresponds to an activity done by the app to access the specific resource type. Each column in the table provides comprehensive context about the app itself, the resource, the user, and the activity.

For example, when you select the **go-hunt** icon beside the **Email** resource, app governance enables you to view the following information for all the emails accessed by the app in the last 30 days in Advanced hunting:

- **Details of the email:** InternetMessageId, NetworkMessageId, Subject, Sender name and address, Recipient address, AttachmentCount and UrlCount
- **App details**: OAuthApplicationId of the app used to send or access the email
- **User context**: ObjectId, AccountDisplayName, IPAddress, and UserAgent
- **App activity context**: OperationType, Timestamp of the activity, Workload

For example:

![Screenshot of an Advanced Hunting page for emails.](media/app-governance-secure-apps-app-hygiene-features/advanced-hunting-for-emails.png)

Similarly, use the **go-hunt** icon in app governance to get details for other supported resources such as files, chat messages and channel messages. Use the **go-hunt** icon beside any user in the **Users** tab in the app details pane to get details on all the activities done by the app in the context of a specific user.

For example:

![Screenshot of an Advanced Hunting page for users.](media/app-governance-secure-apps-app-hygiene-features/advanced-hunting-for-users.png)

## Step 4: Apply advanced hunting capabilities

Use the **Advanced hunting** page to modify or adjust a KQL query to fetch results based on your specific requirements. You might choose to save the query for future users or share a link with others in your organization, or export the results to a CSV file.

For more information, see [Proactively hunt for threats with advanced hunting in Microsoft Defender XDR](/en-us/microsoft-365/security/defender/advanced-hunting-overview).

## Known limitations

When using the **Advanced hunting** page to investigate data from app governance, you might notice discrepancies in the data. These discrepancies can be due to one of the below reasons:

- App governance and advanced hunting process data separately. Any problems encountered by either solution during processing can result in a discrepancy.
- App governance data processing can take several hours longer to complete. Because of this delay, app governance data might not cover recent app activity that is available on Advanced Hunting.
- The advanced hunting queries return up to 1,000 results by default. You can edit the queries to return up to 100,000 rows, the advanced hunting limit. If the results exceed 64 MB, advanced hunting returns partial results and displays a notification. These limits don't apply to app governance.