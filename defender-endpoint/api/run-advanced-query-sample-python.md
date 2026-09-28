---
layout: Conceptual
title: Advanced Hunting with Python API Guide - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/run-advanced-query-sample-python
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
ms.reviewer: 
description: Learn how to query using the Microsoft Defender for Endpoint API, by using Python, with examples.
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
ms.date: 2026-01-08T00:00:00.0000000Z
locale: en-us
document_id: ffb19875-2a87-b825-70ee-63df14352357
document_version_independent_id: ffb19875-2a87-b825-70ee-63df14352357
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/run-advanced-query-sample-python.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/run-advanced-query-sample-python
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/run-advanced-query-sample-python.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 5ffdd968-e72a-2f8b-067a-91e44a2d9975
---

# Advanced Hunting with Python API Guide - Microsoft Defender for Endpoint | Microsoft Learn

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

Run advanced queries using Python, see [Advanced Hunting API](run-advanced-query-api).

In this section, we share Python samples to retrieve a token and use it to run a query.

> 
> **Prerequisite**: You first need to [create an app](apis-intro).

## Get token

- Run the following commands:

Tip

Some Microsoft Defender for Endpoint APIs continue to require access tokens issued for the legacy resource `https://api.securitycenter.microsoft.com`. If the token audience doesn't match the resource expected by the API, requests fail with `403 Forbidden`, even if the API endpoint uses `https://api.security.microsoft.com`. Use `https://api.securitycenter.microsoft.com` as the resource or scope when acquiring tokens.

```python
import json
import urllib.request
import urllib.parse

tenantId = '00000000-0000-0000-0000-000000000000' # Paste your own tenant ID here
appId = '11111111-1111-1111-1111-111111111111' # Paste your own app ID here
appSecret = '22222222-2222-2222-2222-222222222222' # Paste your own app secret here

url = "https://login.microsoftonline.com/%s/oauth2/token" % (tenantId)

resourceAppIdUri = 'https://api.securitycenter.microsoft.com'

body = {
    'resource' : resourceAppIdUri,
    'client_id' : appId,
    'client_secret' : appSecret,
    'grant_type' : 'client_credentials'
}

data = urllib.parse.urlencode(body).encode("utf-8")

req = urllib.request.Request(url, data)
response = urllib.request.urlopen(req)
jsonResponse = json.loads(response.read())
aadToken = jsonResponse["access_token"]
```

Where:

- `tenantId`: ID of the tenant on behalf of which you want to run the query (that is, the query is run on the data of this tenant)
- `appId`: ID of your Microsoft Entra app (the app must have 'Run advanced queries' permission to Microsoft Defender for Endpoint)
- `appSecret`: Secret of your Microsoft Entra app

## Run query

Run the following query:

```python
query = 'DeviceRegistryEvents | limit 10' # Paste your own query here

url = "https://api.security.microsoft.com/api/advancedqueries/run"
headers = {
    'Content-Type' : 'application/json',
    'Accept' : 'application/json',
    'Authorization' : "Bearer " + aadToken
}

data = json.dumps({ 'Query' : query }).encode("utf-8")

req = urllib.request.Request(url, data, headers)
response = urllib.request.urlopen(req)
jsonResponse = json.loads(response.read())
schema = jsonResponse["Schema"]
results = jsonResponse["Results"]
```

- schema contains the schema of the results of your query
- results contain the results of your query

### Complex queries

If you want to run complex queries (or multiline queries), save your query in a file and, instead of the first line in the previous example, run the following command:

```python
queryFile = open("D:\\Temp\\myQuery.txt", 'r') # Replace with the path to your file
query = queryFile.read()
queryFile.close()
```

## Work with query results

You can now use the query results.

To iterate over the results, use the following command:

```python
for result in results:
    print(result) # Prints the whole result
    print(result["EventTime"]) # Prints only the property 'EventTime' from the result
```

To output the results of the query in CSV format in file file1.csv, use the following command:

```python
import csv

outputFile = open("D:\\Temp\\file1.csv", 'w')
output = csv.writer(outputFile)
output.writerow(results[0].keys())
for result in results:
    output.writerow(result.values())

outputFile.close()
```

To output the results of the query in JSON format in file file1.json, use the following command:

```python
outputFile = open("D:\\Temp\\file1.json", 'w')
json.dump(results, outputFile)
outputFile.close()
```