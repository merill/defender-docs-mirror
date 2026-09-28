---
layout: Conceptual
title: Generate block script - cloud discovery API - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/api-discovery-script
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
description: This article describes the discovery_block_scripts request in the Defender for Cloud Apps cloud discovery API.
ms.date: 2023-01-29T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: a0c56eb6-d676-9d03-440e-a0c64dd516f7
document_version_independent_id: a0c56eb6-d676-9d03-440e-a0c64dd516f7
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/api-discovery-script.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api-discovery-script
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/api-discovery-script.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: a9f2b825-f399-4f61-0f4c-df6850688bb6
---

# Generate block script - cloud discovery API - Microsoft Defender for Cloud Apps | Microsoft Learn

Note

This request is not available for Microsoft 365 Cloud App Security.

Run the GET request to get a block script for your network appliance.

## HTTP request

```rest
GET /api/discovery_block_scripts/
```

## Request URL parameters

| Parameter | Description |
| --- | --- |
| format | The format of the network appliance. |

The following formats are currently supported:

| Appliance | Format |
| --- | --- |
| BlueCoat ProxySG | 102 |
| Cisco ASA | 104 |
| Fortinet FortiGate | 108 |
| Juniper SRX | 129 |
| Palo Alto | 112 |
| Websense | 135 |
| Zscaler | 120 |

Note

If you can't find your appliance, generate a block script manually using the portal.

## Response

This request returns the block script as text.

## Example

### Request

Here is an example of the request.

Bearer token:

```rest
curl -XGET -H "Authorization:Bearer <your_token>" "https://<tenant_id>.<tenant_region>.portal.cloudappsecurity.com/api/discovery_block_scripts/?format=102&type=banned"
```

Legacy token:

```rest
curl -XGET -H "Authorization:Token <your_token_key>" "https://<tenant_id>.<tenant_region>.portal.cloudappsecurity.com/api/discovery_block_scripts/?format=102&type=banned"
```

Note

This API supports both `token` and `bearer` options. When using the `token` option, enter the token you generated in the **API Token** tab. When using the `bearer` option, provide the token you generated through Azure AD Graph.

### Response example

```text
url.domain=application.com deny
url.domain=application.be deny
url.domain=application.co deny
```

If you run into any problems, we're here to help. To get assistance or support for your product issue, please [open a support ticket](/en-us/defender-xdr/contact-defender-support).