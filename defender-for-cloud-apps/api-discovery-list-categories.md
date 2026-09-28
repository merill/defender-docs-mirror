---
layout: Conceptual
title: List continuous report categories - cloud discovery API - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/api-discovery-list-categories
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
description: This article describes the list continuous report categories request in the Defender for Cloud Apps cloud discovery API.
ms.date: 2023-01-29T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: c92b6c94-00fe-f9fb-ac17-5c9f5d8b2cbe
document_version_independent_id: c92b6c94-00fe-f9fb-ac17-5c9f5d8b2cbe
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/api-discovery-list-categories.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api-discovery-list-categories
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/api-discovery-list-categories.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: f2e12c27-8a32-3360-7e2f-149c8c039e91
---

# List continuous report categories - cloud discovery API - Microsoft Defender for Cloud Apps | Microsoft Learn

Run the POST request to fetch a list of categories associated with a continuous report.

## HTTP request

```rest
POST api/v1/discovery/discovered_apps/categories/
```

## Request BODY parameters

| Parameter | Description |
| --- | --- |
| filters (*optional*) | Filter objects with all the search filters for the request by category id |
| sortDirection (*optional*) | The sorting direction. Possible values are: `asc` and `desc` |
| sortField (*optional*) | Fields used to sort entities. Possible values are:- **score**: The total number of apps in this category |
| skip (*optional*) | Skips the specified number of records |
| limit (*optional*) | Maximum number of records returned by the request |
| streamId | Filter records by continuous report ID |
| timeFrame (*optional*) | Filter records by the number of days since the continuous report was last used |

## Example

### Request

Here is an example of the request.

```rest
curl -XPOST -H "Authorization:Token <your_token_key>" -H "Content-Type: application/json" "https://<tenant_id>.<tenant_region>.portal.cloudappsecurity.com/api/v1/discovery/discovered_apps/categories/" -d '{
  "filters": {
    // some filters
  },
  "skip": 5,
  "limit": 10,
  "streamId": <continuous_report_id>
}'
```

### Response

Returns a list of app tags in JSON format.

```json
[
  {
    "id": "SAASDB_CATEGORY_PRODUCT_DESIGN",
    "total": 2
  }
]
```

The response object defines the following properties.

| Field name | Field type | Field description |
| --- | --- | --- |
| id | string | The id of the category |
| total | int | The total number of services in the category |

## Supported log types

The following category IDs are currently supported:

| ID | Name |
| --- | --- |
| SAASDB\_CATEGORY\_ACCOUNTING\_AND\_FINANCE | Accounting and finance |
| SAASDB\_CATEGORY\_ADVERTISING | Advertising |
| SAASDB\_CATEGORY\_ALL | All categories |
| SAASDB\_CATEGORY\_BUSINESS\_INTELLIGENCE | Business intelligence |
| SAASDB\_CATEGORY\_BUSINESS\_MANAGEMENT | Business management |
| SAASDB\_CATEGORY\_CLOUD\_COMPUTING\_PLATFORM | Cloud computing platform |
| SAASDB\_CATEGORY\_CLOUD\_STORAGE | Cloud storage |
| SAASDB\_CATEGORY\_CODE\_HOSTING | Code hosting |
| SAASDB\_CATEGORY\_COLLABORATION | Collaboration |
| SAASDB\_CATEGORY\_COMMUNICATIONS | Communications |
| SAASDB\_CATEGORY\_CONSUMER | Consumer |
| SAASDB\_CATEGORY\_CONTENT\_MANAGEMENT | Content management |
| SAASDB\_CATEGORY\_CONTENT\_SHARING | Content sharing |
| SAASDB\_CATEGORY\_CRM | CRM |
| SAASDB\_CATEGORY\_CUSTOMER\_SUPPORT | Customer support |
| SAASDB\_CATEGORY\_DATA\_ANALYTICS | Data analytics |
| SAASDB\_CATEGORY\_DEVELOPMENT\_TOOLS | Development tools |
| SAASDB\_CATEGORY\_ECOMMERCE | E-commerce |
| SAASDB\_CATEGORY\_EDUCATION | Education |
| SAASDB\_CATEGORY\_FORUMS | Forums |
| SAASDB\_CATEGORY\_GENERATIVE\_AI | Generative AI |
| SAASDB\_CATEGORY\_HEALTH | Health |
| SAASDB\_CATEGORY\_HOSTING\_SERVICES | Hosting services |
| SAASDB\_CATEGORY\_HUMAN\_RESOURCE\_MANAGEMENT | Human-resource management |
| SAASDB\_CATEGORY\_INTERNET\_OF\_THINGS | Internet of Things |
| SAASDB\_CATEGORY\_IT\_SERVICES | IT services |
| SAASDB\_CATEGORY\_MARKETING | Marketing |
| SAASDB\_CATEGORY\_MEDIA | Media |
| SAASDB\_CATEGORY\_NEWS\_AND\_ENTERTAINMENT | News and entertainment |
| SAASDB\_CATEGORY\_ONLINE\_MEETINGS | Online meetings |
| SAASDB\_CATEGORY\_OPERATIONS\_MANAGEMENT | Operations management |
| SAASDB\_CATEGORY\_PERSONAL\_INSTANT\_MESSAGING | Personal instant messaging |
| SAASDB\_CATEGORY\_PRODUCT\_DESIGN | Product design |
| SAASDB\_CATEGORY\_PRODUCTIVITY | Productivity |
| SAASDB\_CATEGORY\_PROJECT\_MANAGEMENT | Project management |
| SAASDB\_CATEGORY\_PROPERTY\_MANAGEMENT | Property management |
| SAASDB\_CATEGORY\_SALES | Sales |
| SAASDB\_CATEGORY\_SECURITY | Security |
| SAASDB\_CATEGORY\_SOCIAL\_NETWORK | Social network |
| SAASDB\_CATEGORY\_SUPLLY\_CHAIN\_AND\_LOGISTICS | Supply chain and logistics |
| SAASDB\_CATEGORY\_TIME\_TRACKING | Time tracking |
| SAASDB\_CATEGORY\_TRANSPORTATION\_AND\_TRAVEL | Transportation and travel |
| SAASDB\_CATEGORY\_UNCLASSIFIED | Unclassified |
| SAASDB\_CATEGORY\_VENDOR\_MANAGEMENT\_SYSTEM | Vendor management system |
| SAASDB\_CATEGORY\_WEB\_ANALYTICS | Web analytics |
| SAASDB\_CATEGORY\_WEBMAIL | Webmail |
| SAASDB\_CATEGORY\_WEBSITE\_MONITORING | Website monitoring |
| SAASDB\_SUBCATEGORY\_INSURANCE\_AND\_INVESTMENTS | Accounting and finance |

If you run into any problems, we're here to help. To get assistance or support for your product issue, please [open a support ticket](/en-us/defender-xdr/contact-defender-support).