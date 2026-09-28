---
layout: Conceptual
title: Work with advanced hunting query results in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-query-results
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: View advanced hunting query results as tables or charts, export data, drill into entity details, and refine queries directly from the results pane.
ms.service: defender-xdr
ms.subservice: adv-hunting
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.custom:
- msecd-doc-authoring-1014
- cx-ti
- cx-ah
- sfi-image-nochange
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: d3def96e-ec79-9d89-4636-95606799ea8c
document_version_independent_id: d3def96e-ec79-9d89-4636-95606799ea8c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-query-results.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-query-results
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-query-results.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: eec469cc-527b-acab-c5b9-914160409194
---

# Work with advanced hunting query results in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

While you can construct your [advanced hunting](advanced-hunting-overview) queries to return precise information, you can also work with the query results to gain further insight and investigate specific activities and indicators. You can take the following actions on your query results:

- View results as a table or chart
- Export tables and charts
- Drill down to detailed entity information
- Tweak your queries directly from the results
- View query execution details and troubleshoot errors
- View timeline of events

## View query results as a table or chart

By default, advanced hunting displays query results as tabular data. You can also display the same data as a chart. Advanced hunting supports the following views:

| View type | Description |
| --- | --- |
| **Table** | Displays the query results in tabular format |
| **Column chart** | Renders a series of unique items on the x-axis as vertical bars whose heights represent numeric values from another field |
| **Pie chart** | Renders sectional pies representing unique items. The size of each pie represents numeric values from another field. |
| **Line chart** | Plots numeric values for a series of unique items and connects the plotted values |
| **Scatter chart** | Plots numeric values for a series of unique items |
| **Area chart** | Plots numeric values for a series of unique items and fills the sections below the plotted values |
| **Stacked area chart** | Plots numeric values for a series of unique items and stacks the filled sections below the plotted values |
| **Time chart** | Plots values by count on a linear time scale |

Important

You can view up to 100,000 advanced hunting query results in Microsoft Defender portal. [Learn more about advanced hunting quotas and usage parameters](advanced-hunting-limits#understand-advanced-hunting-quotas-and-usage-parameters).

### Construct queries for effective charts

When rendering charts, advanced hunting automatically identifies columns of interest and the numeric values to aggregate. To get meaningful charts, construct your queries to return the specific values you want to see visualized. Here are some sample queries and the resulting charts.

#### Example chart: Alerts by severity

Use the `summarize` operator to get a numeric count of the values you want to chart. The following query counts alerts by severity so you can visualize their distribution:

```kusto
AlertInfo
| summarize Total = count() by Severity
```

When rendering the results, a column chart displays each severity value as a separate column. You can also add the `render` operator to the query to explicitly render the results as a column chart:

```kusto
AlertInfo
| summarize Total = count() by Severity
| render columnchart
```

[![An example of a chart that displays advanced hunting results in the Microsoft Defender portal](media/advanced-hunting-query-results/advanced-hunting-column-chart-new.png)](media/advanced-hunting-query-results/advanced-hunting-column-chart-new.png#lightbox)

#### Example chart: Phishing emails across top ten sender domains

If you're dealing with a list of values that isn't finite, use the `top` operator, which returns only the highest-ranking rows by a specified column, to chart the values with the most instances. For example, the following query summarizes phishing-related email events by sender domain and returns the top 10 most common sources:

```kusto
EmailEvents
| where ThreatTypes has "Phish"
| summarize Count = count() by SenderFromDomain
| top 10 by Count
```

Use the pie chart view to effectively show distribution across the top domains:

[![The pie chart that displays advanced hunting results in the Microsoft Defender portal](media/advanced-hunting-query-results/advanced-hunting-pie-chart-new.png)](media/advanced-hunting-query-results/advanced-hunting-pie-chart-new.png#lightbox)

#### Example chart: File activities over time

By using the `summarize` operator with the `bin()` function, you can check for events involving a particular indicator over time. The following query searches across cloud app and device file events for activity involving the file `invoice.doc`, counting matches at 30-minute intervals to show spikes in activity:

```kusto
CloudAppEvents
| union DeviceFileEvents
| where FileName == "invoice.doc"
| summarize FileCount = count() by bin(Timestamp, 30m)
```

The following line chart clearly highlights time periods with more activity involving `invoice.doc`:

[![The line chart that displays advanced hunting results in the Microsoft Defender portal](media/advanced-hunting-query-results/line-chart-a.png)](media/advanced-hunting-query-results/line-chart-a.png#lightbox)

## Export tables and charts

After running a query, select **Export** to save the results to a local file. Your chosen view determines how the results are exported:

- **Table view**—The query results are exported in tabular form as a Microsoft Excel workbook.
- **Any chart**—The query results are exported as a JPEG image of the rendered chart.

## Filter results

After running a query, select **Filter** to narrow down the results.

[![Screenshot of filters in advanced hunting.](media/advanced-hunting-query-results/add-filter1.png)](media/advanced-hunting-query-results/add-filter1.png#lightbox)

To add a filter, select the data you want to filter for by selecting one or more of the check boxes. Then select **Add**.

[![Screenshot of filters dropdown in advanced hunting.](media/advanced-hunting-query-results/add-filter2.png)](media/advanced-hunting-query-results/add-filter2.png#lightbox)

You can narrow the results down even further to specific data by selecting the newly added filter.

[![Screenshot of new filter pill in advanced hunting.](media/advanced-hunting-query-results/add-filter3.png)](media/advanced-hunting-query-results/add-filter3.png#lightbox)

Selecting the newly added filter opens a dropdown showing the possible filters you can use. Select one or more of the check boxes, and then select **Apply**.

[![Screenshot of new filter's dropdown in advanced hunting.](media/advanced-hunting-query-results/add-filter4.png)](media/advanced-hunting-query-results/add-filter4.png#lightbox)

Confirm that you added the filters you want by checking the **Filters** section.

[![Screenshot of filters added advanced hunting.](media/advanced-hunting-query-results/add-filter5.png)](media/advanced-hunting-query-results/add-filter5.png#lightbox)

## Drill down from query results

You can explore the results in-line by using the following features:

- Expand a result by selecting the dropdown arrow at the left of each result.
- Where applicable, expand details for results that are in JSON and array formats by selecting the dropdown arrow at the left of applicable column names for added readability.
- Open the side pane to see a record's details (concurrent with expanded rows).

[![Screenshot of expanding results to drill down](media/advanced-hunting-query-results/advanced-hunting-query-results-expand.png)](media/advanced-hunting-query-results/advanced-hunting-query-results-expand.png#lightbox)

You can also right-click on any result value in a row so that you can use it to add more filters to the existing query or copy the value for use in further investigation.

[![Screenshot of options upon right-clicking an option](media/advanced-hunting-query-results/advanced-hunting-query-results-rightclick.png)](media/advanced-hunting-query-results/advanced-hunting-query-results-rightclick.png#lightbox)

For JSON and array fields, you can right-click and update the existing query to include or exclude the field, or to extend the field to a new column.

[![Screenshot of options upon right-clicking an option for JSON and array fields](media/advanced-hunting-query-results/advanced-hunting-query-results-json-right.png)](media/advanced-hunting-query-results/advanced-hunting-query-results-json-right.png#lightbox)

To quickly inspect a record in your query results, select the corresponding row to open the **Inspect record** panel. The panel provides the following information based on the selected record:

- **Assets**—Summarized view of the main assets (mailboxes, devices, and users) found in the record, enriched with available information, such as risk and exposure levels.
- **All details**—All the values from the columns in the record.

[![The selected record with panel for inspecting the record in the Microsoft Defender portal](media/advanced-hunting-query-results/results-inspect-record.png)](media/advanced-hunting-query-results/results-inspect-record.png#lightbox)

To view more information about a specific entity in your query results, such as a machine, file, user, IP address, or URL, select the entity identifier to open a detailed profile page for that entity.

## Tweak your queries from the results

Select the three dots to the right of any column in the **Inspect record** panel. Use the options to:

- Explicitly look for the selected value (`==`)
- Exclude the selected value from the query (`!=`)
- Get more advanced operators for adding the value to your query, such as `contains`, `starts with`, and `ends with`

[![Screenshot of the Action Type pane on the Inspect record page in the Microsoft Defender portal.](media/advanced-hunting-query-results/work-with-query-tweak-query.png)](media/advanced-hunting-query-results/work-with-query-tweak-query.png#lightbox)

## View query execution details and troubleshoot errors

View a query's execution details to understand why the query behaved the way it did, whether it succeeds or fails. This feature provides more visibility into query execution and helps you troubleshoot any problems more efficiently.

After running a query, select **Query Details** above the query results to open a side panel:

[![Screenshot of the advanced hunting page in the Defender portal with Query Details button highlighted.](media/advanced-hunting-query-results/advance-hunting-view-query-details.png)](media/advanced-hunting-query-results/advance-hunting-view-query-details.png#lightbox)

In the **Query Details** side panel, select the **Overview**, **Raw Statistics**, and **Errors** tabs to explore your query's execution time breakdown, data source and scope, resource utilization, and other details:

[![Screenshot of the Query Details side panel.](media/advanced-hunting-query-results/advance-hunting-query-details-panel.png)](media/advanced-hunting-query-results/advance-hunting-query-details-panel.png#lightbox)

If your query fails, select **View full query details** at the bottom of the error message to open the **Query Details** side panel. The error message might also provide an explanation why the query failed and actionable suggestions to fix it.

[![Screenshot of advanced hunting page in the Defender portal with View full query details button highlighted on an error message.](media/advanced-hunting-query-results/advance-hunting-query-details-error.png)](media/advanced-hunting-query-results/advance-hunting-query-details-error.png#lightbox)

## Add items to Favorites

Add your frequently used schemas, functions, queries, and detection rules to the **Favorites** section of each tab in the advanced hunting page for quick access.

[![Screenshot of the advanced hunting page with the Favorites section highlighted.](media/advanced-hunting-query-results/faves-1.png)](media/advanced-hunting-query-results/faves-1.png#lightbox)

For example, to add `AlertInfo` to your **Favorites**, go to the **Schema** tab, select the three dots to the right of the table, and select **Add to favorites**.

[![Screenshot of the Add to Favorites option in the advanced hunting page.](media/advanced-hunting-query-results/faves-2.png)](media/advanced-hunting-query-results/faves-2.png#lightbox)

A notification appears to inform you that the item was successfully added to **Favorites**.

![Screenshot of notification that a new item was added to Favorites in advanced hunting.](media/advanced-hunting-query-results/faves-3.png)

You can do the same for your saved functions, queries, and custom detections in their respective **Favorites** sections right under each tab (**Functions**, **Queries**, and **Detection Rules**).

Note

Some tables in this article might not be available at Microsoft Defender for Endpoint. [Turn on Microsoft Defender](m365d-enable) to hunt for threats using more data sources. You can move your advanced hunting workflows from Microsoft Defender for Endpoint to Microsoft Defender by following the steps in [Migrate advanced hunting queries from Microsoft Defender for Endpoint](advanced-hunting-migrate-from-mde).

## Automatic timeline rendering

By default, a timeline appears above the advanced hunting results that displays event counts over time. The timeline automatically renders based on the `Timestamp` or `timeGenerated` column in the query results. It automatically updates when you apply filters and can help you quickly identify abnormal behavior and trends and focus on interesting results.

Note

The timeline appears only when your results include more than 40 events and contain a `Timestamp` or `timeGenerated` column.

[![Screenshot of the timeline above the query results in advanced hunting.](media/advanced-hunting-query-results/advanced-hunting-query-results-timeline.png)](media/advanced-hunting-query-results/advanced-hunting-query-results-timeline.png#lightbox)

You can select whether to display the timeline by default in the **Chart preferences** settings.

[![Screenshot of the Page preferences settings in advanced hunting.](media/advanced-hunting-query-results/advanced-hunting-chart-preferences.png)](media/advanced-hunting-query-results/advanced-hunting-chart-preferences.png#lightbox)

The timeline automatically adjusts its resolution based on the range of results.

### Filter the timeline results

Select any point on the timeline to filter both the results and the timeline to that specific time range. The timeline also updates its scale to match the selected time period. When you filter by a specific range, the timeline zooms in to show event distribution in high resolution.

# [Unfiltered timeline](#tab/unfiltered)
The following screenshot shows the results of a query that returns 1,000 email events. The timeline is unfiltered, so it displays the full range of results with a timestamp for each day. Select a day or range of days to filter the results for that time period.

[![Screenshot of an advanced hunting query of 1,000 email events with all the results unfiltered.](media/advanced-hunting-query-results/advanced-hunting-unfiltered-results.png)](media/advanced-hunting-query-results/advanced-hunting-unfiltered-results.png#lightbox)

# [Filtered timeline](#tab/filtered)
The following screenshot shows the zoomed in results of a query filtered to a specific date.

[![Screenshot of an advanced hunting query of 1,000 email events with the results filtered to a specific date.](media/advanced-hunting-query-results/advanced-hunting-filtered-results.png)](media/advanced-hunting-query-results/advanced-hunting-filtered-results.png#lightbox)

---

### Split the timeline by values

You can split the results in the timeline by any column that has at least two but fewer than 50 unique values.

# [Ungrouped timeline](#tab/ungrouped)
The following screenshot shows the results of a query that returns 1,000 email events. The timeline is ungrouped, so it displays all the results in a single line.

[![Screenshot of an advanced hunting query of 1,000 email events with the results all together in one line.](media/advanced-hunting-query-results/advanced-hunting-ungrouped.png)](media/advanced-hunting-query-results/advanced-hunting-ungrouped.png#lightbox)

# [Grouped timeline](#tab/grouped)
The following screenshot shows the results grouped by last email action with a separate line for each action.

[![Screenshot of an advanced hunting query of 1,000 email events with the results grouped by last email action.](media/advanced-hunting-query-results/advanced-hunting-grouped.png)](media/advanced-hunting-query-results/advanced-hunting-grouped.png#lightbox)

---

### Change chart type

You can change the chart type of the timeline by selecting a different option from the chart type dropdown menu. The available chart types include:

- Line chart
- Column chart
- Pie chart

[![Screenshot of an advanced hunting query of 1,000 email events with the results displayed in a column chart.](media/advanced-hunting-query-results/advanced-hunting-column-chart.png)](media/advanced-hunting-query-results/advanced-hunting-column-chart.png#lightbox)

### Rendering conditions

The timeline appears only if your results meet the following conditions:

- Your results include more than 40 events.
- Your results include a `Timestamp` or `timeGenerated` column.