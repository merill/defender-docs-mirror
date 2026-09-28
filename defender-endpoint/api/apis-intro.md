---
layout: Conceptual
title: Access the Microsoft Defender for Endpoint APIs - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/apis-intro
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
ms.reviewer: 
description: Learn how you can use APIs to automate workflows and innovate based on Microsoft Defender for Endpoint capabilities
ms.service: defender-endpoint
ms.subservice: reference
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.date: 2025-11-11T00:00:00.0000000Z
ms.collection:
- m365-security
- tier3
- must-keep
ms.topic: reference
ms.custom: api
locale: en-us
document_id: 0625f879-e90f-8545-038d-55b85bf5341e
document_version_independent_id: 0625f879-e90f-8545-038d-55b85bf5341e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/apis-intro.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/apis-intro
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/apis-intro.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 6324e92d-f419-662a-46f6-2caaec96b4ea
---

# Access the Microsoft Defender for Endpoint APIs - Microsoft Defender for Endpoint | Microsoft Learn

Important

Advanced hunting capabilities are not included in Defender for Business.

Note

If you're a US Government customer, use the URIs listed in [Microsoft Defender for Endpoint for US Government customers](/en-us/defender-endpoint/gov#api).

Defender for Endpoint exposes much of its data and actions through a set of programmatic APIs. Those APIs will enable you to automate workflows and innovate based on Defender for Endpoint capabilities. The API access requires OAuth2.0 authentication. For more information, see [OAuth 2.0 Authorization Code Flow](/en-us/azure/active-directory/develop/active-directory-v2-protocols-oauth-code).

Watch this video for a quick overview of Defender for Endpoint's APIs.

In general, you'll need to take the following steps to use the APIs:

- Create a [Microsoft Entra application](exposed-apis-create-app-nativeapp)
- Get an access token using this application
- Use the token to access Defender for Endpoint API

You can access Defender for Endpoint API with **Application Context** or **User Context**.

- **Application Context: (Recommended)**

    Used by apps that run without a signed-in user present. for example, apps that run as background services or daemons.

    Steps that need to be taken to access Defender for Endpoint API with application context:

    1. Create a Microsoft Entra Web-Application.
    2. Assign the desired permission to the application, for example, 'Read Alerts', 'Isolate Machines'.
    3. Create a key for this Application.
    4. Get token using the application with its key.
    5. Use the token to access the Microsoft Defender for Endpoint API

        For more information, see [Get access with application context](exposed-apis-create-app-webapp).
- **User Context:**

    Used to perform actions in the API on behalf of a user.

    Steps to take to access Defender for Endpoint API with user context:

    1. Create Microsoft Entra Native-Application.
    2. Assign the desired permission to the application, e.g 'Read Alerts', 'Isolate Machines' etc.
    3. Get token using the application with user credentials.
    4. Use the token to access the Microsoft Defender for Endpoint API

        For more information, see [Get access with user context](exposed-apis-create-app-nativeapp).

Tip

When more than one query request is required to retrieve all the results, Microsoft Graph returns an `@odata.nextLink` property in the response that contains a URL to the next page of results. For more information, see [Paging Microsoft Graph data in your app](/en-us/graph/paging).