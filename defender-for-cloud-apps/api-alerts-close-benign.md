---
layout: Conceptual
title: Close benign - Alerts API - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/api-alerts-close-benign
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
description: This article describes the bulk close an alert as benign request in the Defender for Cloud Apps Alerts API.
ms.date: 2023-01-29T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: 6d244a4a-3e8c-ab47-b630-f410e178c463
document_version_independent_id: 6d244a4a-3e8c-ab47-b630-f410e178c463
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/api-alerts-close-benign.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api-alerts-close-benign
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/api-alerts-close-benign.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: c8aa945e-fc9c-787b-ca2d-03475a53a1a6
---

# Close benign - Alerts API - Microsoft Defender for Cloud Apps | Microsoft Learn

Run the POST request to close multiple alerts matching the specified filters as benign (an alert on a suspicious but not malicious activity, such as a penetration test or other authorized suspicious action).

## HTTP request

```rest
POST /api/v1/alerts/close_benign/
```

## Request BODY parameters

| Parameter | Description |
| --- | --- |
| filters | Filter objects with all the search filters for the request, see [alert filters](api-alerts#filters) for more details |
| comment | A comment about why the alerts are dismissed |
| reasonId | The reason for closing the alerts as benign. Providing a reason helps improve the accuracy of the detection over time. Possible values include:**2**: Actual severity is lower**4**: Other**5**: Confirmed with end user**6**: Triggered by test |
| sendFeedback | A boolean value indicating that feedback about this alert is provided. Default value: false |
| feedbackText | The text of the feedback |
| allowContact | A boolean value indicating that consent to contact the user is provided. Default value: false |
| contactEmail | The email address of the user |

## Example

### Request

Here is an example of the request.

```rest
curl -XPOST -H "Authorization:Token <your_token_key>" -H "Content-Type: application/json" "https://<tenant_id>.<tenant_region>.portal.cloudappsecurity.com/api/v1/alerts/close_benign/" -d '{
  "filters": {
    "id": {
      "eq": [
        "55af7415f8a0a7a29eef2e1f",
        "55af741cf8a0a7a29eef2e20"
        "5f8d70bfc1ffb25b0a541c7d"
      ]
    }
  },
  "comment": "Irrelevant",
  "reasonId": 5,
  "sendFeedback": true,
  "feedbackText": "Feedback text",
  "allowContact": true,
  "contactEmail": " user@contoso.com"
}'
```

### Response

Response if alert was properly closed:

```json
{
    "closed_benign": 1
}
```

Response if alert not found:

```json
{
    "closed_benign": 0,
    "alertsNotFound": [
        "5f843e9cfe3f6d80fe58a962"
    ]
}

```

If you run into any problems, we're here to help. To get assistance or support for your product issue, please [open a support ticket](/en-us/defender-xdr/contact-defender-support).