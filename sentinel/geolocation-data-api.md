---
layout: Conceptual
title: Enrich entities with geolocation data in Microsoft Sentinel using REST API | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/geolocation-data-api
breadcrumb_path: breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
description: This article describes how you can enrich entities in Microsoft Sentinel with geolocation data via REST API.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: reference
ms.date: 2023-01-09T00:00:00.0000000Z
locale: en-us
document_id: 8cd352db-f5b3-b59d-898b-74e4d900aa5c
document_version_independent_id: 4dac5cbd-01a0-4ee0-0b9e-baad532ec570
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/geolocation-data-api.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/geolocation-data-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/geolocation-data-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 3895fa29-1537-7ebf-2ccc-355a1c16f855
---

# Enrich entities with geolocation data in Microsoft Sentinel using REST API | Microsoft Learn

This article shows you how to enrich entities in Microsoft Sentinel with geolocation data using the REST API.

Important

This feature is currently in PREVIEW. The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

## Common URI parameters

The following are the common URI parameters for the geolocation API:

| Name | In | Required | Type | Description |
| --- | --- | --- | --- | --- |
| **{subscriptionId}** | path | yes | GUID | The Azure subscription ID |
| **{resourceGroupName}** | path | yes | string | The name of the resource group within the subscription |
| **{api-version}** | query | yes | string | The version of the protocol used to make this request. As of April 30 2021, the geolocation API version is *2019-01-01-preview*. |
| **{ipAddress}** | query | yes | string | The IP Address for which geolocation information is needed, in an IPv4 or IPv6 format. |
|  |  |  |  |  |

## Enrich IP Address with geolocation information

This command retrieves geolocation data for a given IP Address.

### Request URI

| Method | Request URI |
| --- | --- |
| **GET** | `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.SecurityInsights/enrichment/ip/geodata/?ipaddress={ipAddress}&api-version={api-version}` |
|  |  |

### Responses

| Status code | Description |
| --- | --- |
| **200** | Success |
| **400** | IP address not provided or is in invalid format |
| **404** | Geolocation data not found for this IP address |
| **429** | Too many requests, try again in the specified timeframe |

### Fields returned in the response

| Field name | Description |
| --- | --- |
| **ASN** | The autonomous system number associated with this IP address |
| **carrier** | The name of the carrier for this IP address |
| **city** | The city where this IP address is located |
| **cityCf** | A numeric rating of confidence that the value in the 'city' field is correct, on a scale of 0-100 |
| **continent** | The continent where this IP address is located |
| **country** | The country/region where this IP address is located |
| **countryCf** | A numeric rating of confidence that the value in the 'country' field is correct on a scale of 0-100 |
| **ipAddr** | The dotted-decimal or colon-separated string representation of the IP address |
| **ipRoutingType** | A description of the connection type for this IP address |
| **latitude** | The latitude of this IP address |
| **longitude** | The longitude of this IP address |
| **organization** | The name of the organization for this IP address |
| **organizationType** | The type of the organization for this IP address |
| **region** | The geographic region where this IP address is located |
| **state** | The state where this IP address is located |
| **stateCf** | A numeric rating of confidence that the value in the 'state' field is correct on a scale of 0-100 |
| **stateCode** | The abbreviated name for the state where this IP address is located |

## Throttling limits for the API

This API has a limit of 100 calls, per user, per hour.

### Sample response

```rest
"body":
{
    "asn": "12345",
    "carrier": "Microsoft",
    "city": "Redmond",
    "cityCf": 90,
    "continent": "north america",
    "country": "united states",
    "countryCf": 99
    "ipAddr": "1.2.3.4",
    "ipRoutingType": "fixed",
    "latitude": "40.2436",
    "longitude": "-100.8891",
    "organization": "Microsoft",
    "organizationType": "tech",
    "region": "western usa",
    "state": "washington",
    "stateCf": null
    "stateCode": "wa"
}
```