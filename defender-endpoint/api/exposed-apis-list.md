---
layout: Conceptual
title: Supported Microsoft Defender for Endpoint APIs - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/exposed-apis-list
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
ms.reviewer: 
description: Learn about the specific supported Microsoft Defender for Endpoint entities where you can create API calls to.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.date: 2025-03-21T00:00:00.0000000Z
ms.collection:
- m365-security
- tier3
- must-keep
ms.topic: reference
ms.subservice: reference
ms.custom: api
locale: en-us
document_id: 36b3113a-9c54-61be-90e5-9d73c3c9d0ae
document_version_independent_id: 36b3113a-9c54-61be-90e5-9d73c3c9d0ae
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/exposed-apis-list.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/exposed-apis-list
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/exposed-apis-list.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 6f92423e-68a0-c6f9-9792-7e4b3a11b6db
---

# Supported Microsoft Defender for Endpoint APIs - Microsoft Defender for Endpoint | Microsoft Learn

Important

Advanced hunting capabilities are not included in Defender for Business.

## Endpoint URI and versioning

### Endpoint URI

> 
> The service base URI is: https://api.security.microsoft.com
> 
> The queries based OData have the '/api' prefix. For example, to get Alerts you can send GET request to https://api.security.microsoft.com/api/alerts

### Versioning

> 
> The API supports versioning.
> 
> 
> > 
> > The current version is **V1.0**. To use a specific version, use this format: `https://api.security.microsoft.com/api/{Version}`. For example: `https://api.security.microsoft.com/api/v1.0/alerts`
> 
> 
> If you don't specify any version (e.g. `https://api.security.microsoft.com/api/alerts`) you will get to the latest version.

Note

If you're a US Government customer, use the URIs listed in [Microsoft Defender for Endpoint for US Government customers](/en-us/defender-endpoint/gov#api).

Tip

For better performance, instead of using api.security.microsoft.com, use a server closer to your geolocation:

- us.api.security.microsoft.com
- eu.api.security.microsoft.com
- uk.api.security.microsoft.com
- au.api.security.microsoft.com
- swa.api.security.microsoft.com
- ina.api.security.microsoft.com
- aea.api.security.microsoft.com

Learn more about the individual supported entities where you can run API calls to and details such as HTTP request values, request headers and expected responses.