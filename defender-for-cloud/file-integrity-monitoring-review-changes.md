---
layout: Conceptual
title: Review Changes in File Integrity Monitoring - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/file-integrity-monitoring-review-changes
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Learn how to review changes in file integrity monitoring in Microsoft Defender for Cloud.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 1e65bfe8-d60f-636b-fcf9-a5c36436baba
document_version_independent_id: 25b75e56-6cd0-74bd-2a18-61dbbba18cf1
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/file-integrity-monitoring-review-changes.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/file-integrity-monitoring-review-changes
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/file-integrity-monitoring-review-changes.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 8cb2a162-744a-ab11-6734-c6ee624db3c3
---

# Review Changes in File Integrity Monitoring - Microsoft Defender for Cloud | Microsoft Learn

In Defender for Servers Plan 2 in Microsoft Defender for Cloud, the [file integrity monitoring feature](file-integrity-monitoring-overview) helps keep enterprise assets and resources secure by scanning and analyzing files, and comparing their current state with previous scans.

File integrity monitoring uses the Microsoft Defender for Endpoint agent to collect data from machines, in accordance with collection rules. [Defender for Endpoint is integrated by default](integration-defender-for-endpoint) with Defender for Cloud.

Note

The older method of data collection uses the Log Analytics agent, also known as the Microsoft Monitoring agent (MMA). Support for using the MMA ended in November 2024.

Use File Integrity Monitoring in Defender for Cloud to review tracked file and registry changes.

## Prerequisites

Before you review file changes, make sure the following prerequisites are met:

- Defender for Servers Plan 2 is enabled.
- [File integrity monitoring with the Defender for Endpoint agent](file-integrity-monitoring-enable-defender-endpoint) is enabled. If file integrity monitoring with the Defender for Endpoint agent isn't enabled, this message appears: **File Integrity Monitoring is not enabled**. To enable it, select **Onboard subscriptions**, and then enable file integrity monitoring.

## Monitor entities and files

To monitor entities and files, follow these steps:

1. From Defender for Cloud's sidebar, go to **Workload protections** &gt; **File integrity monitoring**.

    [![Screenshot of how to access File Integrity Monitoring in Workload protections.](media/file-integrity-monitoring-enable-defender-endpoint/workload-protections-file-integrity-monitoring.png)](media/file-integrity-monitoring-enable-defender-endpoint/workload-protections-file-integrity-monitoring.png#lightbox)
2. A window opens with all resources that contain tracked changed files and registries.

    [![Screenshot of the File Integrity Monitoring results.](media/file-integrity-monitoring-enable-defender-endpoint/file-integrity-monitoring-results.png)](media/file-integrity-monitoring-enable-defender-endpoint/file-integrity-monitoring-results.png#lightbox)
3. If you select a resource, a window opens with a query showing the changes made to the tracked files and registries on that resource.

    [![Screenshot of the File Integrity Monitoring query.](media/file-integrity-monitoring-enable-defender-endpoint/file-integrity-monitoring-query.png)](media/file-integrity-monitoring-enable-defender-endpoint/file-integrity-monitoring-query.png#lightbox)
4. If you select the subscription of the resource, under the column **Subscription name**, a query opens with all the tracked files and registries in that subscription.

Note

If you previously used File Integrity Monitoring over the Log Analytics agent, also known as the Microsoft Monitoring Agent (MMA), you can return to that method by selecting **Change to previous experience**. The **Change to previous experience** option remains available until the FIM over MMA feature is deprecated. For information on the deprecation plan, see [Prepare for retirement of the Log Analytics agent](prepare-deprecation-log-analytics-mma-agent).

## Retrieve and analyze file integrity monitoring data

The file integrity monitoring data resides within the Azure Log Analytics workspace in the `MDCFileIntegrityMonitoringEvents` table.

1. Set a time range to retrieve a summary of changes by resource. This example gets all changes in the last 14 days in the categories of registry and files:

    ```kusto
    MDCFileIntegrityMonitoringEvents  
    | where TimeGenerated > ago(14d)  
    | where MonitoredEntityType in ('Registry', 'Files')  
    | summarize count() by Computer, MonitoredEntityType  
    ```
2. To view detailed information about registry changes:

    1. Remove `Files` from the `where` clause.
    2. Replace the summarization line with an ordering clause:

    ```kusto
    MDCFileIntegrityMonitoringEvents  
    | where TimeGenerated > ago(14d)  
    | where MonitoredEntityType == 'Registry'  
    | order by Computer, RegistryKey  
    ```
3. You can export the reports to CSV for archival purposes or send them to Power BI for further analysis.