---
layout: Conceptual
title: Access the Microsoft Defender XDR APIs - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/api-access
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to access the Microsoft Defender XDR APIs
ms.service: defender-xdr
ms.author: edbaynash
author: EdB-MSFT
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- must-keep
ms.topic: reference
ms.custom: api
ms.date: 2025-04-15T00:00:00.0000000Z
locale: en-us
document_id: 882b183b-f2a7-ba15-ea8e-2a6644b7f459
document_version_independent_id: 882b183b-f2a7-ba15-ea8e-2a6644b7f459
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/api-access.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/api-access.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 54782348-f550-a166-828f-1e86c0d4c476
---

# Access the Microsoft Defender XDR APIs - Microsoft Defender XDR | Microsoft Learn

Note

**Try our new APIs using MS Graph security API**. Find out more at: [Use the Microsoft Graph security API - Microsoft Graph | Microsoft Learn](/en-us/graph/api/resources/security-api-overview).

Important

Some information relates to prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

Microsoft Defender exposes much of its data and actions through a set of programmatic APIs. These APIs help you automate workflows and make full use of Microsoft Defender's capabilities.

In general, you'll need to take the following steps to use the APIs:

- Create a Microsoft Entra application
- Get an access token using this application
- Use the token to access the Microsoft Defender API

Note

API access requires OAuth2.0 authentication. For more information, see [OAuth 2.0 Authorization Code Flow](/en-us/azure/active-directory/develop/active-directory-v2-protocols-oauth-code).

Once you've accomplished these steps, you're ready to access the Microsoft Defender API using a particular context.

## Application context (Recommended)

Use this context for apps that run without a signed-in user present, such as background services or daemons.

1. Create a Microsoft Entra web application.
2. Assign the desired permissions to the application.
3. Create a key for the application.
4. Get a security token using the application and its key.
5. Use the token to access the Microsoft Defender API.

For more information, see **[Create an app to access Microsoft Defender without a user](api-create-app-web)**.

## User context

Use this context to perform actions on behalf of a single user.

1. Create a Microsoft Entra native application.
2. Assign the desired permission to the application.
3. Get a security token using the user credentials for the application.
4. Use the token to access the Microsoft Defender API.

For more information, see **[Create an app to access Microsoft Defender APIs on behalf of a user](api-create-app-user-context)**.

## Partner context

Use this context when you need to provide an app to many users in [multiple tenants](/en-us/azure/active-directory/develop/single-and-multi-tenant-apps).

1. Create a Microsoft Entra multi-tenant application.
2. Assign the desired permission to the application.
3. Get [admin consent](/en-us/azure/active-directory/develop/v2-permissions-and-consent#requesting-consent-for-an-entire-tenant) for the app from each tenant.
4. Get a security token using user credentials based on a customer's tenant ID.
5. Use the token to access the Microsoft Defender API.

For more information, see **[Create an app with partner access to Microsoft Defender APIs](api-partner-access)**.