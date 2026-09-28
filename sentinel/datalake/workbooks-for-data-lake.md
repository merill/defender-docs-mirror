---
layout: Conceptual
title: Workbooks for Microsoft Sentinel Data Lake - Microsoft Security | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/workbooks-for-data-lake
breadcrumb_path: ../breadcrumb/toc.json
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
ms.subservice: sentinel-platform
search.appverid: met150
description: Learn how to create and use Microsoft Sentinel workbooks with data from the Microsoft Sentinel data lake to visualize and monitor security data.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: zeinam
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: ms-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: bd711b73-3639-4d00-13b9-f73e157f120e
document_version_independent_id: 0bb7d5e0-ab7b-7430-e9ed-7df9c2c64c02
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/workbooks-for-data-lake.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/workbooks-for-data-lake
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/workbooks-for-data-lake.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: db93a21d-86b4-c412-ab3e-722535bdaafb
---

# Workbooks for Microsoft Sentinel Data Lake - Microsoft Security | Microsoft Learn

Microsoft Sentinel workbooks let SOC teams visualize and monitor security data directly from the data lake. Analysts use KQL (Kusto Query Language) to query the lake without duplicating or transforming data. Select Sentinel data lake as the data source in a workbook to run the same queries used for investigations and hunting. Then render results as interactive charts and tables for monitoring and reporting. Running workbook queries directly against the Sentinel data lake keeps analytics consistent across queries, supports longer data retention, and scales with high-volume historical data. Consistent analytics, longer data retention, and high-volume scalability make workbooks ideal for threat hunting, trend analysis, and executive dashboards.

This article walks you through the process of creating workbooks for using Microsoft Sentinel data lake as the data source. For more information on using workbooks with Sentinel, see [Visualize and monitor your data by using workbooks in Microsoft Sentinel](/en-us/azure/sentinel/monitor-your-data?tabs=defender-portal).

Query performance matters because workbook visuals can autorefresh and run many times. Add time filters, summarize results, and project only the columns you need. Adding time filters, summarizing results, and projecting only the required columns prevent queries from scanning too much historical data. Well-scoped queries keep dashboards fast while still using long-term data for analysis.

## Create a workbook with Microsoft Sentinel data lake as the data source

Follow these steps to create a workbook that uses Microsoft Sentinel data lake as its data source:

1. In the Defender portal, go to **Microsoft Sentinel** &gt; **Threat management** &gt; **Workbooks**.
2. Select the cube icon in the top right corner to select the workspaces you want to store your workbooks.
3. Select **Add workbook**.

    [![Screenshot of a workbook in edit mode with the query editor open.](media/workbooks-for-data-lake/add-workbook.png)](media/workbooks-for-data-lake/add-workbook.png#lightbox)

    A new workbook opens with a basic query and a par chart visual.
4. Select the **Edit**.

    [![Screenshot of a new workbook with basic query and chart visual.](media/workbooks-for-data-lake/edit-new-workbook.png)](media/workbooks-for-data-lake/edit-new-workbook.png#lightbox)
5. Under the chart, select **Add**, and then select **Add data source and visualization**.

    [![Screenshot of the Add data source and visualization button in a Microsoft Sentinel workbook.](media/workbooks-for-data-lake/add-data-source-and-visualization.png)](media/workbooks-for-data-lake/add-data-source-and-visualization.png#lightbox)
6. Select **Sentinel data lake** as the data source.
7. Select the workspace containing your SignInLogs table in the data lake.
8. Paste the following KQL into the query editor:

    ```kql
    AWSCloudTrail
    | where isnotempty(ErrorCode)
    | summarize FailedEvents = count()
        by bin(TimeGenerated, 1h), SourceIpAddress, UserIdentityPrincipalid
    | where FailedEvents > 3
    | summarize FailedEvents = sum(FailedEvents) by UserIdentityPrincipalid
    | top 10 by FailedEvents
    ```
9. Under **Visualization** select **Bar chart**.
10. Select **Run query** to visualize the results.
11. Select **Done editing** to exit edit mode and view your visual.

    [![Screenshot showing the editing of a new query and visualization.](media/workbooks-for-data-lake/edit-new-query.png)](media/workbooks-for-data-lake/edit-new-query.png#lightbox)

    This visual shows the top 10 AWS principal identities with the most failed API calls in AWSCloudTrail logs. Failed events are counted and filtered to show identities with repeated errors. Use the failed-events bar chart to spot suspicious or misconfigured identities that produce unusual failure patterns.

    Note

    The **Visualization** type **Set by query** isn't supported.

    Relative time ranges such as `> ago(10d) ` work for up to 90 days. Absolute time ranges follow your data retention policy.
12. On the workbook page, select **Done editing**.
13. Select **Save** to save the workbook to your library, giving your workbook a name and location.
14. You can view your saved workbook in the list of workbooks, and select it to view the visualizations you created. You can also edit the workbook at any time to update the queries or visuals.

[![Screenshot showing the list of saved workbooks in Microsoft Sentinel.](media/workbooks-for-data-lake/saved-workbooks.png)](media/workbooks-for-data-lake/saved-workbooks.png#lightbox)