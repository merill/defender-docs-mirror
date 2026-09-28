---
layout: Conceptual
title: Manage IP address ranges using the API - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/api-data-enrichment-manage-script
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
description: Use the Data Enrichment APIs in Defender for Cloud Apps to create, update, and delete IP address ranges programmatically, with request and response details and a Python CSV sync example.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 2621680f-392f-2600-a298-ce2cd9552f2a
document_version_independent_id: 2621680f-392f-2600-a298-ce2cd9552f2a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/api-data-enrichment-manage-script.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api-data-enrichment-manage-script
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/api-data-enrichment-manage-script.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 23fc525f-47a8-89d7-31a7-72a0fa55a0cb
---

# Manage IP address ranges using the API - Microsoft Defender for Cloud Apps | Microsoft Learn

Use the Data Enrichment APIs in Microsoft Defender for Cloud Apps to create, update, and delete IP address ranges programmatically. This article describes the request and response parameters for the API and provides a Python script that reads IP address ranges from a CSV file and synchronizes them with your tenant.

## Manage IP address ranges with the script

Perform the following steps to use the Python script to manage IP address ranges in your tenant:

1. Create a CSV file with the following expected fields: Name, IP\_Address\_Ranges, Category, Tag(id), and Override\_ISP\_Name. Here's an example of the CSV file contents:

    ```csv
    name, ip_address_ranges, category, tag(id), isp_name
    Test 1,200.200.200.200/24 201.201.201.201/24,1, ,
    Test 2,1.1.1.5/32 31.31.31.4/24,1,000000290000000000000000 0000002d0000000000000000  ,
    Test 3,2.2.2.2/32,1,0000002d0000000000000000,
    Test 4,5.6.5.4/32,2,,test
    ```
2. Update the values for the following script variables: **OPTION\_DELETE\_ENABLED**, **IP\_RANGES\_BASE\_URL**, **CSV\_ABSOLUTE\_PATH**, **YOUR\_TOKEN**
3. Run the script to create new records and update existing rules with the matching name.

    Important

    If you set **OPTION\_DELETE\_ENABLED** to **True**, any IP address ranges that are defined in your tenant but don't exist in the CSV files will be deleted from the tenant by the script. If you set **OPTION\_DELETE\_ENABLED** to **True**, make sure that the CSV file defines all the IP address ranges you want in your tenant.

## Request body parameters

The request body supports the following parameters:

- "filters": Filter objects with all the search filters for the request. For more information, see: [Data Enrichment filters](api-data-enrichment#filters) for more information. To avoid having your requests be throttled, make sure to include a limitation on your query.
- "limit": Integer. In scan mode, between 500 and 5000 (defaults to 500). Controls the number of iterations used for scanning all the data.

## Response parameters

The response includes the following parameters:

- "data": the returned data. Will contain up to "limit" number of records each iteration. If there are more records to be pulled (hasNext=true), the last few records are dropped to ensure that all data is listed only once.
- "hasNext": Boolean. Denotes whether another iteration on the data is needed.
- "nextQueryFilters": If another iteration is needed, it contains the consecutive JSON query to be run. Use the "nextQueryFilters" value as the "filters" parameter in the next request.

This Python example uses the contents of a CSV file to manage (create, update, or delete) IP address ranges in your Defender for Cloud Apps environment.

```python
import csv
import http
import requests
import json
 
OPTION_DELETE_ENABLED = False
IP_RANGES_BASE_URL = 'https://<tenant_id>.<tenant_region>.portal.cloudappsecurity.com/api/v1/subnet/'
IP_RANGES_UPDATE_SUFFIX = 'update_rule/'
IP_RANGES_CREATE_SUFFIX = 'create_rule/'
CSV_ABSOLUTE_PATH = 'rules.csv'
YOUR_TOKEN = '<your_token>'
HEADERS = {
  'Authorization': 'Token {}'.format(YOUR_TOKEN),
  'Content-Type': 'application/json'
}
 
# Get all records.
def get_records():
  list_request_data = {
    # Optionally, edit to match your filters
    'filters': {},
    "skip": 0,
    "limit": 20
  }
  records = []
  has_next = True
  while has_next:
    response = requests.post(IP_RANGES_BASE_URL, json=list_request_data, headers=HEADERS)
    if response.status_code != http.HTTPStatus.OK:
      raise Exception(f'Error getting existing subnets from tenant. Stopping script run. Error: {response.content}')
    content = json.loads(response.content)
    response_data = content.get('data', [])
    records += response_data
    has_next = content.get('hasNext', False)
    list_request_data["skip"] += len(response_data)
  return records
 
# Rule fields are compared to the CSV row.
def rule_matching(record, ip_address_ranges, category, tag, isp_name, ):
  new_tags = sorted([new_tag for new_tag in tag.split(' ') if new_tag != ''])
  existing_tags = sorted([existing_tag.get('id') for existing_tag in record.get('tags', [])])
  rule_exists_conditions = [sorted([subnet.get('originalString', False) for subnet in record.get('subnets', [])]) !=
  sorted(ip_address_ranges.split(' ')),
  str(record.get('category', False)) != category,
  existing_tags != new_tags,
  bool(record.get('organization', False)) != bool(isp_name) or
  (record.get('organization', False) is not None and not isp_name)]
  if any(rule_exists_conditions):
    return False
  return True
 
def create_update_rule(name, ip_address_ranges, category, tag, isp_name, records, request_data):
  for record in records:
    # Records are compared by name(unique).
    # This can be changed to id (to update the name), it will include adding id to the CSV and changing row shape.
    if record["name"] == name:
    # request_data["_tid"] = record["_tid"]
      if not rule_matching(record, ip_address_ranges, category, tag, isp_name):
        # Update existing rule
        request_data['_id'] = record['_id']
        response = requests.post(f"{IP_RANGES_BASE_URL}{record['_id']}/{IP_RANGES_UPDATE_SUFFIX}", json=request_data, headers=HEADERS)
        if response.status_code == http.HTTPStatus.OK:
          print('Rule updated', request_data)
        else:
          print('Error updating rule. Request data:', request_data, ' Response:', response.content)
          json.loads(response.content)
        return record
      else:
        # The exact same rule exists. no need for change.
        print('The exact same rule exists. no need for change. Rule name: ', name)
        return record
  # Create new rule.
  response = requests.post(f"{IP_RANGES_BASE_URL}{IP_RANGES_CREATE_SUFFIX}", json=request_data, headers=HEADERS)
  if response.status_code == http.HTTPStatus.OK:
    print('Rule created:', request_data)
  else:
    print('Error creating rule. Request data:', request_data, ' Response:', response.content)
    # added record
    return record
 
# Request data creation.
def create_request_data(name, ip_address_ranges, category, tag, isp_name):
  tags = [new_tag for new_tag in tag.split(' ') if new_tag != '']
  request_data = {"name": name, "subnets": ip_address_ranges.split(' '), "category": category, "tags": tags}
  if isp_name:
    request_data["overrideOrganization"] = True
    request_data["organization"] = isp_name
  return request_data
 
def main():
  # CSV fields are: Name,IP_Address_Ranges,Category,Tag(id),Override_ISP_Name
  # Multiple values (eg: multiple subnets) will be space-separated. (eg: value1 value2)
  records = get_records()
  with open(CSV_ABSOLUTE_PATH, newline='\n') as your_file:
    reader = csv.reader(your_file, delimiter=',')
    # move the reader object to point on the next row, headers are not needed
    next(reader)
    for row in reader:
      name, ip_address_ranges, category, tag, isp_name = row
      request_data = create_request_data(name, ip_address_ranges, category, tag, isp_name)
      if records:
      # Existing records were retrieved from your tenant
        record = create_update_rule(name, ip_address_ranges, category, tag, isp_name, records, request_data)
        record_id = record['_id']
      else:
        # No existing records were retrieved from your tenant
        response = requests.post(f"{IP_RANGES_BASE_URL}{IP_RANGES_CREATE_SUFFIX}", json=request_data, headers=HEADERS)
        if response.status_code == http.HTTPStatus.OK:
          record_id = json.loads(response.content)
          print('Rule created:', request_data)
        else:
          print('Error creating rule. Request data:', request_data, ' Response:', response.content)
      if OPTION_DELETE_ENABLED:
        # Remove CSV file record from tenant records.
        if record_id:
          for record in records:
            if record['_id'] == record_id:
              records.remove(record)
  if OPTION_DELETE_ENABLED:
    # Delete remaining tenant records, i.e. records that aren't in the CSV file.
    for record in records:
      requests.delete(f"{IP_RANGES_BASE_URL}{record['_id']}/", headers=HEADERS)
 
if __name__ == '__main__':
  main()
```