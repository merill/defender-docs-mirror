---
layout: Conceptual
title: Work with discovered apps via Graph API - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/discovered-apps-api-graph
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
description: Learn how to work with apps discovered by Microsoft Defender for Cloud Apps via Graph API.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.reviewer: Mravela
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 92b49d7b-e724-9af1-2161-705d47353960
document_version_independent_id: 92b49d7b-e724-9af1-2161-705d47353960
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/discovered-apps-api-graph.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: discovered-apps-api-graph
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/discovered-apps-api-graph.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d774b87-7dcb-40bf-a0b9-5a7a9efff0d1
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/89dc5f37-0e4e-4b05-ad87-5fcd2b941a8a
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 460e3e4b-d646-4f19-d320-d768b5f24126
---

# Work with discovered apps via Graph API - Microsoft Defender for Cloud Apps | Microsoft Learn

Microsoft Defender for Cloud Apps supports a Microsoft Graph API that you can use to work with discovered cloud apps, to customize and automate the **Discovered apps** page functionality in the Microsoft Defender portal.

This article provides sample procedures for using the [uploadedStreams API](/en-us/graph/api/security-datadiscoveryreport-list-uploadedstreams?view=graph-rest-beta&amp;preserve-view=true&amp;tabs=http) for common purposes.

## Prerequisites

Before you start using the Graph API, make sure to create an app and get an access token to call the API. Then, use the access token to access the Defender for Cloud Apps API.

- Make sure to give the app permissions to access Defender for Cloud Apps, by granting it with `CloudApp-Discovery.Read.All` permissions and admin consent.
- Take note of your app secret and copy its value to use later on in your scripts.
- You need cloud app data streaming into Microsoft Defender for Cloud Apps.

For more information, see:

- [Manage admin access](manage-admins)
- [Graph API authentication and authorization basics](/en-us/graph/auth/auth-concepts)
- [Use the Microsoft Graph API](/en-us/graph/use-the-api)
- [Set up Cloud Discovery](set-up-cloud-discovery)

## Get data about discovered apps

To list all available uploaded streams and get a high-level summary of the data available on your **Discovered apps** page, run the following GET command. The response includes the stream IDs you need for subsequent queries:

```http
GET https://graph.microsoft.com/beta/security/dataDiscovery/cloudAppDiscovery/uploadedStreams
```

To drill down to data for a specific stream returned by the previous GET request:

1. Copy the relevant `<streamID>` value (the `id` property of the uploaded stream) from the `GET .../uploadedStreams` response.
2. Run the following GET command, replacing `<streamId>` with the `id` value from the previous response:

    ```http
    GET https://graph.microsoft.com/beta/security/dataDiscovery/cloudAppDiscovery/uploadedStreams/<streamId>/aggregatedAppsDetails(period=duration'P90D')
    ```

## Filter for a specific time period and risk score

Filter your API commands using `$select` and `$filter` to get data for a specific time period and risk score. For example, to view the names of all apps discovered in the last 30 days with a risk score lower or equal to 4, run:

```http
GET https://graph.microsoft.com/beta/security/dataDiscovery/cloudAppDiscovery/uploadedStreams/<streamId>/aggregatedAppsDetails (period=duration'P30D')?$filter=riskRating  le 4 &$select=displayName
```

## Get the userIdentifier of all users, devices, or IP addresses using a specific app

After retrieving an app `<id>` from the `aggregatedAppsDetails` response, run one of the following commands to identify the users, devices, or IP addresses that are currently using that app:

- **To return users**:

    ```http
    GET  https://graph.microsoft.com/beta/security/dataDiscovery/cloudAppDiscovery/uploadedStreams/<streamId>/aggregatedAppsDetails (period=duration'P30D')/ <id>/users  
    ```
- **To return IP addresses**:

    ```http
    GET  https://graph.microsoft.com/beta/security/dataDiscovery/cloudAppDiscovery/uploadedStreams/<streamId>/aggregatedAppsDetails (period=duration'P30D')/ <id>/ipAddress  
    ```
- **To return devices** (lists the device names that accessed the specified app during the period):

    ```http
    GET  https://graph.microsoft.com/beta/security/dataDiscovery/cloudAppDiscovery/uploadedStreams/<streamId>/aggregatedAppsDetails (period=duration'P30D')/ <id>/name  
    ```

## Use filters to see apps by category

Use filters to see apps of a specific category, such as apps that are categorized as *Marketing*, and are also not HIPPA compliant. For example, the following request returns marketing-category apps from the specified stream that are marked as not HIPAA compliant:

```http
GET  https://graph.microsoft.com/beta/security/dataDiscovery/cloudAppDiscovery/uploadedStreams/<MDEstreamId>/aggregatedAppsDetails (period=duration 'P30D')?$filter= (appInfo/Hippa eq 'false') and category eq 'Marketing'  
```