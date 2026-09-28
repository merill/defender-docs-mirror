---
layout: Conceptual
title: Fetch - Alerts API - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/api-alerts-fetch
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
description: This article describes the fetch request in the Defender for Cloud Apps Alerts API.
ms.date: 2023-01-29T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: c066b1a9-beb4-7b2f-4b24-2c6c3be19d1b
document_version_independent_id: c066b1a9-beb4-7b2f-4b24-2c6c3be19d1b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/api-alerts-fetch.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api-alerts-fetch
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/api-alerts-fetch.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: c05f581c-166c-c0ca-407c-5fa65b067278
---

# Fetch - Alerts API - Microsoft Defender for Cloud Apps | Microsoft Learn

Run the GET request to fetch the alert matching the specified primary key.

## HTTP request

```rest
GET /api/v1/alerts/<pk>/
```

## Request URL parameters

| Parameter | Description |
| --- | --- |
| pk | The ID of the alert |

## Example

### Request

Here's an example of the request.

```rest
curl -XGET -H "Authorization:Token <your_token_key>" "https://<tenant_id>.<tenant_region>.portal.cloudappsecurity.com/api/v1/alerts/<pk>/"
```

### Response

Returns the specified alert in JSON format. For detailed information on each property, refer to the [alert properties specifications](api-alerts#properties).

```json
{
  "_id": "603f704aaf7417985bbf3b22",
  "contextId": "206e2965-6533-48a6-ba9e-794364a84bf9",
  "description": "Contoso user performed 11 suspicious activities MITRE Technique used Account Discovery (T1087) and subtechnique used Domain Account (T1087.002)",
  "entities": [
    {
      "entityRole": "Source",
      "entityType": 2,
      "id": "6204bdaf-ad46-4e99-a25d-374a0532c666",
      "inst": 0,
      "label": "user1",
      "pa": "user1@contoso.com",
      "type": "account"
    },
    {
      "entityRole": "Related",
      "id": "55017817-27af-49a7-93d6-8af6c5030fdb",
      "label": "DC3",
      "type": "device"
    },
    {
      "id": 20940,
      "label": "Active Directory",
      "type": "service"
    },
    {
      "entityRole": "Related",
      "id": "95c59b48-98c1-40ff-a444-d9040f1f68f2",
      "label": "DC4",
      "type": "device"
    },
    {
      "id": "5bfd18bfab73c36ba10d38ca",
      "label": "Honeytoken activity",
      "policyType": "ANOMALY_DETECTION",
      "type": "policyRule"
    },
    {
      "entityRole": "Source",
      "id": "34f3ecc9-6903-4df7-af79-14fe2d0d4553",
      "label": "Client1",
      "type": "device"
    },
    {
      "entityRole": "Related",
      "id": "d68772fe-1171-4124-9f73-0f410340bd54",
      "label": "DC1",
      "type": "device"
    },
    {
      "type": "groupTag",
      "id": "5f759b4d106abbe4a504ea5d",
      "label": "All Users"
    }
  ],
  "idValue": 15795464,
  "isSystemAlert": false,
  "resolutionStatusValue": 0,
  "severityValue": 1,
  "statusValue": 1,
  "stories": [
    0
  ],
  "threatScore": 34,
  "timestamp": 1621941916475,
  "title": "Honeytoken activity",
  "comment": "",
  "handledByUser": "administrator@contoso.com",
 "resolveTime": "2021-05-13T14:02:34.904Z",
  "URL": "https://contoso.portal.cloudappsecurity.com/#/alerts/603f704aaf7417985bbf3b22"
}
```

If you run into any problems, we're here to help. To get assistance or support for your product issue, [open a support ticket](/en-us/defender-xdr/contact-defender-support).