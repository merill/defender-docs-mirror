---
layout: Conceptual
title: Search for Specific Events Across Large Datasets in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/search-jobs
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
description: Learn how to use search jobs to search large datasets.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.collection: usx-security
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: e3b656e1-d8e3-8159-aa8f-f5c9372849fb
document_version_independent_id: 7fea52df-12cb-4804-8b11-a31f3f6a90b8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/search-jobs.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/search-jobs
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/search-jobs.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 4ab31304-3bb0-3980-db88-2bd357d2660f
---

# Search for Specific Events Across Large Datasets in Microsoft Sentinel | Microsoft Learn

Use a search job to retrieve data stored in [long-term retention](/en-us/azure/azure-monitor/logs/data-retention-configure#interactive-long-term-and-total-retention), or to scan through large volumes of data, if the log query time-out of 10 minutes isn't sufficient. A search job scans through up to a year of data in a table for specific events. The search job sends its results to a new Analytics table in the same workspace as the source data.

This article explains how to run a search job in Microsoft Sentinel and how to work with the search job results.

Search jobs across certain data sets might incur extra charges. For more information, see [Microsoft Sentinel pricing page](billing).

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Implementation considerations

See [Search job considerations](/en-us/azure/azure-monitor/logs/search-jobs#considerations) in the Azure Monitor documentation.

## Start a search job

Go to **Search** in Microsoft Sentinel from the Azure portal or the Microsoft Defender portal to enter your search criteria. Depending on the size of the target dataset, search times vary. While most search jobs take a few minutes to complete, searches across massive data sets that run up to 24 hours are also supported.

1. For Microsoft Sentinel in the [Defender portal](https://security.microsoft.com/), select **Microsoft Sentinel** &gt; **Search**. For Microsoft Sentinel in the [Azure portal](https://portal.azure.com), under **General**, select **Search**.
2. Select the **Table** menu and choose a table for your search.
3. In the **Search** box, enter a search term.

# [Defender portal](#tab/defender-portal)
[![Screenshot of search page with search criteria of administrator, time range last 90 days, and table selected.](media/search-jobs/search-job-defender-portal.png)](media/search-jobs/search-job-defender-portal.png#lightbox)

# [Azure portal](#tab/azure-portal)
## [![Screenshot of search page with search criteria of administrator, time range last 90 days, and table selected.](media/search-jobs/search-job-criteria.png)](media/search-jobs/search-job-criteria.png#lightbox)

---
4. Select the **Start** to preview your results for a set time range in **Simple Mode**. If needed, go to the dropdown menu and switch from **Simple mode** to **KQL mode** to open the advanced Kusto Query Language (KQL) editor.
5. Change the KQL query as needed and select **Run** to get an updated preview of the search results. Resolve any KQL issues indicated by a squiggly red line in the editor.

    ![Screenshot of KQL editor with revised search.](media/search-jobs/search-job-advanced-kql-edit.png)
6. When you're satisfied with the query and the search results preview, select the ellipses **...** and select **Search job** to open the **Search Job Mode** window.

    [![Screenshot of KQL editor with revised search with ellipsis highlighted in order to select Search job, which will open the Search Job Mode window.](media/search-jobs/search-job-advanced-kql-ellipsis.png)](media/search-jobs/search-job-advanced-kql-ellipsis.png#lightbox)
7. Specify the search job date range using the **Time range** selector. If your query also specifies a time range, Microsoft Sentinel runs the search job on the union of the time ranges.
8. Enter a new table name to store the search job results.
9. Select **Run search job**.
10. Wait for the notification **Search job is done** and select the button to go to the table and view the results.

## View search job results

View the status and results of your search job by going to the **Saved Searches** tab.

1. In Microsoft Sentinel, select **Search** &gt; **Saved Searches**.
2. On the search card, select **View search results**.

    [![Screenshot that shows the link to view search results at the bottom of the search job card.](media/search-jobs/view-search-results.png)](media/search-jobs/view-search-results.png#lightbox)

    By default, you see all the results that match the criteria used for the selected search job.
3. To refine the list of results returned from the search table, select **Add filter**.
4. As you're reviewing your search job results, select **Add bookmark**, or select the bookmark icon to preserve a row. Adding a bookmark allows you to tag events, add notes, and attach these events to an incident for later reference.

    [![Screenshot that shows search job results with a bookmark in the process of being added.](media/search-jobs/search-results-add-bookmark.png)](media/search-jobs/search-results-add-bookmark.png#lightbox)
5. Select the **Columns** button and select the checkbox next to columns you'd like to add to the results view.
6. Add the **Bookmarked** filter to only show preserved entries.
7. Select **View all bookmarks** to go the **Hunting** page where you can add a bookmark to an existing incident.