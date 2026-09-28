---
layout: Conceptual
title: Investigate activities using the API - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/api-activities-investigate-script
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
description: Use the Activities API in Defender for Cloud Apps to scan and retrieve large volumes of user activity data across connected cloud apps.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: Naama-Goldbart
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 2e29425d-7b9d-905e-fb8a-ff0bb634d34c
document_version_independent_id: 2e29425d-7b9d-905e-fb8a-ff0bb634d34c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/api-activities-investigate-script.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api-activities-investigate-script
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/api-activities-investigate-script.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: 1f7445d3-49a8-b423-2134-de6452395021
---

# Investigate activities using the API - Microsoft Defender for Cloud Apps | Microsoft Learn

You can use the Activities APIs to investigate the activities performed by your users across connected cloud apps.

The activities API mode is optimized for scanning and retrieval of large quantities of data (over 5,000 activities). The API scan queries the activity data repeatedly until all the results have been scanned.

Note

For large quantities of activities and large scale deployments, we recommended that you use the [SIEM agent](siem) for activity scanning.

## Use the activity scan script

To scan activity data, send a POST request to the activities endpoint with scan mode enabled:

1. Run the query on your data.
2. If there are more records than could be listed in a single scan, the response includes `nextQueryFilters`. Use `nextQueryFilters` as the filter parameter in each subsequent query until all matching activity records have been returned.

## Request body parameters

The request body supports the following parameters:

- "filters": Filter objects with all the search filters for the request, see [Activity filters](activity-filters-queries) for more information. To avoid having your requests be throttled, make sure to include a limitation on your query, for example, query the last day's activities, or filter for a particular app.
- "isScan": Boolean. Enables the scanning mode.
- "sortDirection": The sorting direction. Possible values are `asc` and `desc`.
- "sortField": Fields used to sort activities. Possible values are:
    - `date` - The date when then the activity occurred (this is the default).
    - `created` - The [timestamp](api-introduction#timestamps) when the activity was saved.
- "limit": Integer. In scan mode, between 500 and 5000 (defaults to 500). Controls the number of iterations used for scanning all the data.

## Response parameters

The response includes the following parameters:

- "data": the returned data. Will contain up to "limit" number of records each iteration. If there are more records to be pulled (hasNext=true), the last few records are dropped to ensure that all data is listed only once.
- "hasNext": Boolean. Denotes whether another iteration on the data is needed.
- "nextQueryFilters": If another iteration is needed, it contains the consecutive JSON query to be run. Use this as the "filters" parameter in the next request. If the "hasNext" parameter is set to False, this parameter will be missing since you've iterated over all of the data.

The following Python example gets all the activities from the past day from Exchange Online. The script sends the prepared filters to the Activities API in scan mode and iterates through paginated responses using `nextQueryFilters` until all matching activity records are retrieved.

```python
import requests
import json
ACTIVITIES_URL = 'https://<your_tenant>.<tenant_region>.portal.cloudappsecurity.com/api/v1/activities/'

your_token = '<your_token>'
headers = {
'Authorization': 'Token {}'.format(your_token),
}

filters = {
  # optionally, edit to match your filters
  'date': {'gte_ndays': 1},
  'service': {'eq': [20893]}
}
request_data = {
  'filters': filters,
  'isScan': True
}

records = []
has_next = True
while has_next:
    content = json.loads(requests.post(ACTIVITIES_URL, json=request_data, headers=headers).content)
    response_data = content.get('data', [])
    records += response_data
    print('Got {} more records'.format(len(response_data)))
    has_next = content.get('hasNext', False)
    request_data['filters'] = content.get('nextQueryFilters')

print('Got {} records in total'.format(len(records)))
```