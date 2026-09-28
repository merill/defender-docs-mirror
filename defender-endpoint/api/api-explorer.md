---
layout: Conceptual
title: API Explorer in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/api-explorer
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
ms.reviewer: 
description: Use the API Explorer to construct and do API queries, test, and send requests for any available API
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- must-keep
ms.topic: reference
ms.subservice: reference
ms.custom: api
ms.date: 2020-12-18T00:00:00.0000000Z
locale: en-us
document_id: f51946d5-b70b-52bc-3a8e-5b29cb13aa6e
document_version_independent_id: f51946d5-b70b-52bc-3a8e-5b29cb13aa6e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/api-explorer.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/api-explorer
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/api-explorer.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 6de60b1e-a447-9ada-2d32-e7c0c9e25692
---

# API Explorer in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

The Microsoft Defender for Endpoint API Explorer is a tool that helps you explore various Defender for Endpoint APIs interactively.

The API Explorer makes it easy to construct and do API queries, test, and send requests for any available Defender for Endpoint API endpoint. Use the API Explorer to take actions or find data that might not yet be available through the user interface.

The tool is useful during app development. It allows you to perform API queries that respect your user access settings, reducing the need to generate access tokens.

You can also use the tool to explore the gallery of sample queries, copy result code samples, and generate debug information.

With the API Explorer, you can:

- Run requests for any method and see responses in real-time.
- Quickly browse through the API samples and learn what parameters they support.
- Make API calls with ease; no need to authenticate beyond the management portal signin.

## Access API Explorer

From the left navigation menu, select **Partners & APIs** &gt; **[API Explorer](https://security.microsoft.com/interoperability/api-explorer)**.

## Supported APIs

API Explorer supports all the APIs offered by Defender for Endpoint.

The list of supported APIs is available in the [APIs documentation](apis-intro).

## Get started with the API Explorer

1. In the left pane, there's a list of sample requests that you can use.
2. Follow the links and click **Run query**.

Some of the samples may require specifying a parameter in the URL, for example, {machine- ID}.

## FAQ

### Do I need to have an API token to use the API Explorer?\*\*

Credentials to access an API aren't needed. The API Explorer uses the Defender for Endpoint management portal token whenever it makes a request.

The logged-in user authentication credential is used to verify that the API Explorer is authorized to access data on your behalf.

Specific API requests are limited based on your RBAC privileges. For example, a request to "Submit indicator" is limited to the security admin role.

Tip

Do you want to learn more? Engage with the Microsoft Security community in our Tech Community: [Microsoft Defender for Endpoint Tech Community](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/bd-p/MicrosoftDefenderATP).