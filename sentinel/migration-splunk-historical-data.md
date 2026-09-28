---
layout: Conceptual
title: Export Splunk Data to Target Platform - Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/migration-splunk-historical-data
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
description: Learn how to export your historical data from Splunk for a Microsoft Sentinel migration of security monitoring use cases.
author: EdB-MSFT
ms.author: edbaynash
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 531a5d22-6ac9-1085-278d-f5897e1ba378
document_version_independent_id: ca21c899-a337-6d66-2078-e44f3ca4208d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/migration-splunk-historical-data.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/migration-splunk-historical-data
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/migration-splunk-historical-data.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: df782ae5-1a2b-e8cb-b62e-0b9c5139f3a3
---

# Export Splunk Data to Target Platform - Microsoft Sentinel | Microsoft Learn

Use these methods to export historical data from Splunk in CSV format before migrating it to Azure. After you export your data, you can [select a target Azure platform for your exported historical data](migration-ingestion-target-platform), and then [select a data ingestion tool for migrating historical data](migration-ingestion-tool).

![Diagram illustrating steps involved in export and ingestion.](media/migration-export-ingest/export-data.png)

You can export data from Splunk in several ways. Your selection of an export method depends on the data volumes involved and your level of interactivity. For example, exporting a single, on-demand search via Splunk Web might be appropriate for a low-volume export. Alternatively, if you want to set up a higher-volume, scheduled export, the SDK and REST options work best.

For large exports, the most stable method for data retrieval is `dump` or the Command Line Interface (CLI). You can export the logs to a local folder on the Splunk server or to another server accessible by Splunk.

To export your historical data from Splunk, use one of the [Splunk export methods](https://docs.splunk.com/Documentation/Splunk/8.2.5/Search/Exportsearchresults). The output format should be CSV.

## CLI example

This CLI example searches for events from the `_internal` index that occur during the time window specified in the search command. The example then specifies to output the events in a CSV format to the **data.csv** file.You can export a maximum of 100 events by default. To increase this number, set the `-maxout` argument. For example, if you set `-maxout` to `0`, you can export an unlimited number of events.

This CLI command exports data recorded between 23:59 and 01:00 on September 14, 2021 to a CSV file:

```spl
splunk search "index=_internal earliest=09/14/2021:23:59:00 latest=09/16/2021:01:00:00 " -output csv > c:/data.csv  
```

## dump example

This `dump` command exports all events from the `bigdata` index to the `YYYYmmdd/HH/host` location under the `$SPLUNK_HOME/var/run/splunk/dispatch/<sid>/dump/` directory on a local disk. The command uses `MyExport` as the prefix for export filenames, and outputs the results to a CSV file. The command partitions the exported data using the `eval` function before the `dump` command.

```spl
index=bigdata | eval _dstpath=strftime(_time, "%Y%m%d/%H") + "/" + host | dump basefilename=MyExport format=csv 
```