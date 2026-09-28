---
layout: Conceptual
title: 'Microsoft Sentinel Migration: Export QRadar Data to Target Platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/migration-qradar-historical-data
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
description: Export historical QRadar data for Microsoft Sentinel migration by using the QRadar REST API and AQL queries, with guidance on limiting query scope and preparing for ingestion.
author: EdB-MSFT
ms.author: edbaynash
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: a3ea557d-cc35-cf2d-6dd6-04089ca0c0ce
document_version_independent_id: 36b32d11-3be8-a21c-a9ed-6c2b4b0a5820
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/migration-qradar-historical-data.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/migration-qradar-historical-data
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/migration-qradar-historical-data.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 4a32a98a-6ffa-f64e-c1ac-257ccf1eb727
---

# Microsoft Sentinel Migration: Export QRadar Data to Target Platform | Microsoft Learn

This article describes how to export your historical data from QRadar. After you complete the steps in this article, you can [select a target platform](migration-ingestion-target-platform) to host the exported data, and then [select an ingestion tool](migration-ingestion-tool) to migrate the data.

[![Diagram illustrating steps involved in export and ingestion.](media/migration-export-ingest/export-data.png)](media/migration-export-ingest/export-data.png#lightbox)

To export your QRadar data, you use the QRadar REST API to run Ariel Query Language (AQL) queries on data stored in an Ariel database. Because the export process is resource intensive, we recommend that you use small time ranges in your queries, and only migrate the data you need.

## Create AQL query

To create or select an AQL query for export:

1. In the QRadar Console, select the **Log Activity** tab.
2. Create a new AQL search query or select a saved search query to export the data. Ensure that the query includes the `START` and `STOP` functions to set the date and time range.

    Learn how to use [AQL](https://www.ibm.com/docs/en/qsip/7.5?topic=aql-ariel-query-language) and how to [save search criteria](https://www.ibm.com/docs/en/qsip/7.5?topic=searches-saving-search-criteria) in AQL.
3. Copy the AQL query for later use.
4. Encode the AQL query to the URL encoded format. Paste the query you copied in step 3 into the [URL Encode/Decode tool](https://www.url-encode-decode.com/). Copy the encoded format output.

## Execute search query

You can execute the search query using one of these methods:

- **QRadar Console user ID**: To use this method, ensure that the console user ID being used for data migration is assigned to a [security profile](https://www.ibm.com/docs/en/qradar-on-cloud?topic=management-security-profiles) that can access the data you need for the export.
- **API token**: To use this method, [generate an API token in QRadar](https://www.ibm.com/docs/en/qradar-common?topic=app-creating-authorized-service-token-qradar-operations).

To execute the search query:

1. Log in to the system from which you'll download the historical data. Ensure that this system has access to the QRadar Console and QRadar API on TCP/443 via HTTPS.
2. To execute the search query that retrieves the historical data, open a command prompt and run one of these commands:

    - For the QRadar Console user ID method, run:

        ```
        curl -s -X POST -u <enter_qradar_console_user_id> -H 'Version: 12.0' -H 'Accept: application/json' 'https://<enter_qradar_console_ip_or_hostname>/api/ariel/searches?query_expression=<enter_encoded_AQL_from_previous_step>'
        ```
    - For the API token method, run:

        ```
        curl -s -X POST -H 'SEC: <enter_api_token>' -H 'Version: 12.0' -H 'Accept: application/json' 'https://<enter_qradar_console_ip_or_hostname>/api/ariel/searches?query_expression=<enter_encoded_AQL_from_previous_step> 
        ```

        The search job execution time may vary, depending on the AQL time range and amount of queried data. We recommended that you run the query in small time ranges, and to query only the data you need for the export.

        The output should return a status, such as `COMPLETED`, `EXECUTE`, `WAIT`, a `progress` value, and a `search_id` value. For example:

        ![Screenshot of the output of the search query command.](media/migration-qradar-historical-data/export-output.png)
3. Copy the value in the `search_id` field. You'll use this ID to check the progress and status of the search query execution, and to download the results after the search execution is complete.
4. To check the status and the progress of the search, run one of these commands:

    - For the QRadar Console user ID method, run:

        ```
        curl -s -X POST -u <enter_qradar_console_user_id> -H 'Version: 12.0' -H 'Accept: application/json' 'https:// <enter_qradar_console_ip_or_hostname>/api/ariel/searches/<enter_search_id_from_previous_step>' 
        ```
    - For the API token method, run:

        ```
        curl -s -X POST -H 'SEC: <enter_api_token>' -H 'Version: 12.0' -H 'Accept: application/json' 'https:// <enter_qradar_console_ip_or_hostname>/api/ariel/searches/<enter_search_id_from_previous_step>' 
        ```
5. Review the output. If the value in the `status` field is `COMPLETED`, continue to the next step. If the status isn't `COMPLETED`, check the value in the `progress` field, and after 5-10 minutes, run the command you ran in step 4.
6. Review the output and ensure that the status is `COMPLETED`.
7. Run one of these commands to download the results or returned data from the JSON file to a folder on the current system:

    - For the QRadar Console user ID method, run:

        ```
        curl -s -X GET -u <enter_qradar_console_user_id> -H 'Version: 12.0' -H 'Accept: application/json' 'https:// <enter_qradar_console_ip_or_hostname>/api/ariel/searches/<enter_search_id_from_previous_step>/results' > <enter_path_to_file>.json 
        ```
    - For the API token method, run:

        ```
        curl -s -X GET -H 'SEC: <enter_api_token>' -H 'Version: 12.0' -H 'Accept: application/json' 'https:// <enter_qradar_console_ip_or_hostname>/api/ariel/searches/<enter_search_id_from_previous_step>/results' > <enter_path_to_file>.json 
        ```
8. To retrieve the data that you need to export, create the AQL query (steps 1-4) and execute the query (steps 1-7) again. Adjust the time range and search queries to get the data you need.