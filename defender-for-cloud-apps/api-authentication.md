---
layout: Conceptual
title: Managing API tokens - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/api-authentication
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
description: This article provides information about generating and managing API tokens for Defender for Cloud Apps.
ms.date: 2023-01-29T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: 89ba9f49-f3cd-0605-e595-2053171908fa
document_version_independent_id: 89ba9f49-f3cd-0605-e595-2053171908fa
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/api-authentication.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api-authentication
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/api-authentication.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 06de29e8-e28a-d600-de14-6836bf1bd020
---

# Managing API tokens - Microsoft Defender for Cloud Apps | Microsoft Learn

Defender for Cloud Apps exposes much of its data and actions through a set of programmatic APIs. Those APIs will enable you to automate workflows and innovate based on Defender for Cloud Apps capabilities.

To access the Defender for Cloud Apps API, you have to create an API token and use it in your software to connect to the API. This token will be included in the header when Defender for Cloud Apps makes API requests.

The API access requires OAuth2.0 authentication. For more information, see [OAuth 2.0 Authorization Code Flow](/en-us/azure/active-directory/develop/active-directory-v2-protocols-oauth-code).

In general, you’ll need to take the following steps to use the APIs:

- Create a Microsoft Entra application
- Get an access token using this application
- Use the token to access the Defender for Cloud Apps API

You can access the Defender for Cloud Apps API with **Application Context** or **User Context**.

Note

[The legacy method](api-tokens-legacy) of accessing the Defender for Cloud Apps API is still supported. However, it is on a deprecation path, so we recommend using the methods described on this page.

## Application context (recommended)

Used by apps that run without a signed-in user present. For example, apps that run as background services or daemons.

Steps that need to be taken to access Defender for Cloud Apps API with application context:

1. Create a Microsoft Entra Web-Application.
2. Assign the desired permission to the application. For example, **Read Alerts** or **Upload Discovery Report**.
3. Create a key for this application.
4. Get the token using the application with its key.
5. Use the token to access the Defender for Cloud Apps API.

For more detailed steps on how to perform these steps, see [Get access with application context](api-authentication-application).

## User context

Used to perform actions in the API on behalf of a user.

Steps to take to access the Defender for Cloud Apps API with application context:

1. Create a Microsoft Entra Native-Application.
2. Assign the desired permission to the application. For example, **Read Alerts** or **Upload Discovery Report**.
3. Get the token using the application with user credentials.
4. Use the token to access the Defender for Cloud Apps API.

For more detailed steps on how to perform these step, see [Get access with user context](api-authentication-user).