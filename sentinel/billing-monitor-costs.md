---
layout: Conceptual
title: Manage and Monitor Costs for Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/billing-monitor-costs
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
description: Learn how to manage and monitor costs and billing for Microsoft Sentinel by using cost analysis in the Azure portal and other methods.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: daniha
ms.custom: subject-cost-optimization, msecd-doc-authoring-1016
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
locale: en-us
document_id: 7daefb12-0e2e-eb85-0e29-c40d838c70ad
document_version_independent_id: 3052bf43-4c72-d820-9ab6-0235c543f5d2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/billing-monitor-costs.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/billing-monitor-costs
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/billing-monitor-costs.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1d9b4802-f23d-41f1-9e27-65deeceacb8d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/820483fb-3aa1-4b86-bc99-9a906a24f579
platformId: 37ae7173-e370-fa76-51ad-c5544e397b7d
---

# Manage and Monitor Costs for Microsoft Sentinel | Microsoft Learn

After you start using Microsoft Sentinel resources, use built-in Cost Management features to confidently manage budgets, monitor costs and security performance. You can also review forecasted costs and identify spending trends to optimize. With the Sentinel data lake enabled, you can also view your usage directly in the Microsoft Defender portal.

Microsoft Sentinel costs are only a portion of your monthly Azure bill. Although this article explains how to manage and monitor costs for Microsoft Sentinel, you're billed for all Azure services and resources your Azure subscription uses, including Partner services.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Prerequisites

To view cost data and perform cost analysis in Cost Management, you must have a supported Azure account type with at least read access.

While cost analysis in Cost Management supports most Azure account types, not all are supported. To view the full list of supported account types, see [Understand Cost Management data](/en-us/azure/cost-management-billing/costs/understand-cost-mgt-data?WT.mc_id=costmanagementcontent_docsacmhorizontal_-inproduct-learn).

For information about assigning access to Microsoft Cost Management data, see [Assign access to data](/en-us/azure/cost-management/assign-access-acm-data?WT.mc_id=costmanagementcontent_docsacmhorizontal_-inproduct-learn).

## Manage and monitor costs for the analytics tier

As you use Azure resources with Microsoft Sentinel, you incur costs. Azure resource usage unit costs vary by time intervals such as seconds, minutes, hours, and days, or by unit usage like bytes and megabytes.

### View costs by using cost analysis

As soon as Microsoft Sentinel starts to ingest billable data, it incurs costs. View these costs by using cost analysis in the Azure portal. For more information, see [Start using cost analysis](/en-us/azure/cost-management/quick-acm-cost-analysis?WT.mc_id=costmanagementcontent_docsacmhorizontal_-inproduct-learn).

When you use cost analysis, you view Microsoft Sentinel costs in graphs and tables for different time intervals. Some examples are by day, current and prior month, and year. You also view costs against budgets and forecasted costs. Switching to longer views over time can help you identify spending trends. And you see where overspending might have occurred. If you created budgets, you can also easily see where they're exceeded.

The [Microsoft Cost Management + Billing](/en-us/azure/cost-management-billing/costs/quick-acm-cost-analysis) hub provides useful functionality. After you open **Cost Management + Billing** in the Azure portal, select **Cost Management** in the left navigation and then select the [Cost Management scope](/en-us/azure/cost-management-billing/costs/understand-work-scopes) or set of resources to investigate, such as an Azure subscription or resource group.

The **Cost Analysis** screen shows detailed views of your Azure usage and costs, with the option to apply various controls and filters.

For example, to see charts of your daily costs for a certain time frame:

1. Select the drop-down caret in the **View** field and select **Accumulated costs** or **Daily costs**.
2. Select the drop-down caret in the date field and select a date range.
3. Select the drop-down caret next to **Granularity** and select **Daily**.

    The costs shown in the following image are for illustrative purposes only. They're not intended to reflect actual costs.

    [![Screenshot of a cost management + billing cost analysis screen.](media/billing-monitor-costs/cost-management.png)](media/billing-monitor-costs/cost-management.png#lightbox)

You could also apply further controls. For example, to view only the costs associated with Microsoft Sentinel, select **Add filter**, select **Service name**, and then select the service names **Sentinel**, **Log Analytics**, and **Azure Monitor**.

Microsoft Sentinel analytics tier data ingestion volumes appear under **Security Insights** in some portal Usage Charts.

The Microsoft Sentinel classic pricing tiers don't include Log Analytics charges, so you might see those charges billed separately. Microsoft Sentinel simplified pricing combines the two costs into one set of tiers. To learn more about Microsoft Sentinel's pricing tiers, see [Understand the full billing model for Microsoft Sentinel](billing#understand-the-full-billing-model-for-microsoft-sentinel).

For more information on reducing costs, see [Create budgets](billing-monitor-costs#create-budgets) and [Reduce costs in Microsoft Sentinel](billing-reduce-costs).

### Run queries to understand your analytics tier data ingestion

Microsoft Sentinel uses an extensive query language to analyze, interact with, and derive insights from huge volumes of operational data in seconds. Here are some Kusto queries you can use to understand your data ingestion volume.

Run the following query to show data ingestion volume by solution:

```kusto
Usage
| where StartTime >= startofday(ago(31d)) and EndTime < startofday(now())
| where IsBillable == true
| summarize BillableDataGB = sum(Quantity) / 1000. by bin(StartTime, 1d), Solution
| extend Solution = iff(Solution == "SecurityInsights", "AzureSentinel", Solution)
| render columnchart
```

Run the following query to show data ingestion volume by data type:

```kusto
Usage
| where StartTime >= startofday(ago(31d)) and EndTime < startofday(now())
| where IsBillable == true
| summarize BillableDataGB = sum(Quantity) / 1000. by bin(StartTime, 1d), DataType
| render columnchart
```

Run the following query to show data ingestion volume by both solution and data type:

```kusto
Usage
| where TimeGenerated > ago(32d)
| where StartTime >= startofday(ago(31d)) and EndTime < startofday(now())
| where IsBillable == true
| summarize BillableDataGB = sum(Quantity) / 1000. by Solution, DataType
| extend Solution = iff(Solution == "SecurityInsights", "AzureSentinel", Solution)
| sort by Solution asc, DataType asc
```

See more information on the following items used in the preceding examples in the Kusto documentation:

- [***where*** operator](/en-us/kusto/query/where-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***extend*** operator](/en-us/kusto/query/extend-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***summarize*** operator](/en-us/kusto/query/summarize-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***render*** operator](/en-us/kusto/query/render-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***sort*** operator](/en-us/kusto/query/sort-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***iff()*** function](/en-us/kusto/query/iff-function?view=microsoft-sentinel&amp;preserve-view=true)
- [***ago()*** function](/en-us/kusto/query/ago-function?view=microsoft-sentinel&amp;preserve-view=true)
- [***now()*** function](/en-us/kusto/query/now-function?view=microsoft-sentinel&amp;preserve-view=true)
- [***bin()*** function](/en-us/kusto/query/bin-function?view=microsoft-sentinel&amp;preserve-view=true)
- [***startofday()*** function](/en-us/kusto/query/startofday-function?view=microsoft-sentinel&amp;preserve-view=true)
- [***count()*** aggregation function](/en-us/kusto/query/count-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true)
- [***sum()*** aggregation function](/en-us/kusto/query/sum-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true)

For more information on KQL, see [Kusto Query Language (KQL) overview](/en-us/kusto/query/?view=microsoft-sentinel&amp;preserve-view=true).

Other resources:

- [KQL quick reference](/en-us/kusto/query/kql-quick-reference?view=microsoft-sentinel&amp;preserve-view=true)
- [Kusto Query Language learning resources](/en-us/kusto/query/kql-learning-resources?view=microsoft-sentinel&amp;preserve-view=true)

### Deploy a workbook to visualize data ingestion into the analytics tier

The **Workspace Usage Report workbook** provides your workspace's data consumption, cost, and usage statistics. The workbook gives the workspace's data ingestion status and amount of free and billable data. You can use the workbook logic to monitor data ingestion and costs, and to build custom views and rule-based alerts.

This workbook also provides granular ingestion details. The workbook breaks down the data in your workspace by data table, and provides volumes per table and entry to help you better understand your ingestion patterns.

To enable the Workspace Usage Report workbook:

1. In the Microsoft Sentinel left navigation, select **Threat management** &gt; **Workbooks**.
2. Enter *workspace usage* in the Search bar, then select **Workspace Usage Report**.
3. Select **View template** to use the workbook as is, or select **Save** to create an editable copy of the workbook. If you save a copy, select **View saved workbook**.
4. In the workbook, select the **Subscription** and **Workspace** you want to view, then set the **TimeRange** to the time frame you want to see. You can set the **Show help** toggle to **Yes** to display in-place explanations in the workbook.

## Export cost data

You can also [export your cost data](/en-us/azure/cost-management-billing/costs/tutorial-improved-exports?WT.mc_id=costmanagementcontent_docsacmhorizontal_-inproduct-learn) to a storage account. Exporting cost data is helpful when you need or others to do more data analysis for costs. For example, a finance team can analyze the data using Excel or Power BI. You can export your costs on a daily, weekly, or monthly schedule and set a custom date range. Exporting cost data is the recommended way to retrieve cost datasets.

### Create budgets

You can create [Cost Management budgets](/en-us/azure/cost-management/tutorial-acm-create-budgets?WT.mc_id=costmanagementcontent_docsacmhorizontal_-inproduct-learn) to track costs and create [cost management alerts](/en-us/azure/cost-management-billing/costs/cost-mgt-alerts-monitor-usage-spending?WT.mc_id=costmanagementcontent_docsacmhorizontal_-inproduct-learn) that automatically notify stakeholders of spending anomalies and overspending risks. Alerts are based on spending compared to budget and cost thresholds. Budgets and alerts are created for Azure subscriptions and resource groups, so they're useful as part of an overall cost monitoring strategy.

You can create budgets with filters for specific resources or services in Azure if you want finer granularity in your monitoring. Filters help ensure that you don't accidentally create new resources that cost you more money. For more information about the filter options available when you create a budget, see [Group and filter options](/en-us/azure/cost-management-billing/costs/group-filter?WT.mc_id=costmanagementcontent_docsacmhorizontal_-inproduct-learn).

### Use a playbook for cost management alerts

To help you control your Analytics tier budget, you can create a cost management playbook. The playbook sends you an alert if your Microsoft Sentinel workspace exceeds a budget, which you define, within a given timeframe.

The Microsoft Sentinel GitHub community provides the [`Send-IngestionCostAlert`](https://github.com/Azure/Azure-Sentinel/tree/master/Playbooks/Send-IngestionCostAlert) cost management playbook on GitHub. This playbook is activated by a recurrence trigger, and gives you a high level of flexibility. You can control execution frequency, ingestion volume, and the message to trigger, based on your requirements.

## Manage and monitor costs for the data lake tier

After your workspace is onboarded to the Microsoft Sentinel data lake tier, usage of data lake tier capabilities is billed using new Microsoft Sentinel data lake meters. For more information on the new meters, see [Data lake tier](billing#data-lake-tier).

### Microsoft Sentinel cost management in the Microsoft Defender portal

The new cost-management experience, currently in preview and under **Microsoft Sentinel** &gt; **Cost management** in the [Microsoft Defender portal](https://security.microsoft.com), helps you manage and monitor costs associated with your use of the data lake tier.

Important

To **view usage and limits** (read-only access), you need the **Security Reader** role. To **set limits and configure alerts**, you need either the **Billing Administrator** or **Security Administrator** role.

#### Usage

The Usage summary lets you visualize usage by capability over time. Select a meter from the **Meters** dropdown to view its usage. Once selected, daily usage is displayed for the chosen time range. By default, data is shown for a single month, but you can adjust the time window using the filter. The summary card shows the total usage for the selected period.

[![Screenshot of the Usage summary chart in Microsoft Sentinel cost management.](media/billing-monitor-costs/usage-summary-chart.png)](media/billing-monitor-costs/usage-summary-chart.png#lightbox)

After the summary chart, usage details vary by meter. For **Data lake query** and **Advanced data insights**, usage is split between **interactive analysis** and **scheduled analysis**.

[![Screenshot of usage details split by analysis type for selected meters.](media/billing-monitor-costs/usage-details-by-analysis-type.png)](media/billing-monitor-costs/usage-details-by-analysis-type.png#lightbox)

After the charts, a table provides a breakdown of the resources contributing to the selected meter’s usage.

[![Screenshot of the usage table showing resources contributing to meter usage.](media/billing-monitor-costs/usage-resource-contributors-table.png)](media/billing-monitor-costs/usage-resource-contributors-table.png#lightbox)

Select a resource to view a detailed breakdown in the side panel.

[![Screenshot of the side panel with detailed resource usage breakdown.](media/billing-monitor-costs/resource-usage-side-panel.png)](media/billing-monitor-costs/resource-usage-side-panel.png#lightbox)

#### Notification

The **Configure Policies** wizard lets you set threshold‑based alerts for Microsoft Sentinel data lake capabilities. These policies help you track usage and receive email notifications before unexpected charges occur. Currently, email notifications are sent to the billing administrator who configured the policy.

You can also enable **threshold enforcement** to block usage after a configured limit is exceeded. Enforcement is supported for:

- **Data Lake Query** (interactive KQL queries and jobs)
- **Advanced Data Insights** (notebook runs and notebook jobs)

After enforcement is enabled and the threshold is exceeded, future queries, jobs, or sessions fail. Users see a **Limit exceeded** error indicating that you reached the configured limit.

Note

Enforcement isn't real time. After a limit is reached, it can take up to **four hours** for the enforced threshold to take effect.

To configure alerts or enforced thresholds on a capability:

1. In **Microsoft Sentinel** &gt; **Cost management**, select **Configure Policies** in the top right corner.

    [![Screenshot of the Configure Policies button in Microsoft Sentinel cost management.](media/billing-monitor-costs/configure-policies-button.png)](media/billing-monitor-costs/configure-policies-button.png#lightbox)
2. On the **Configure Policies** page, select the policy you want to edit.

    [![Screenshot of the Configure Policies page with a selected policy.](media/billing-monitor-costs/configure-policies-page.png)](media/billing-monitor-costs/configure-policies-page.png#lightbox)
3. In the **Edit policy** side panel, enter a value for the total threshold.

    [![Screenshot of the Edit policy panel with total threshold input.](media/billing-monitor-costs/edit-policy-total-threshold.png)](media/billing-monitor-costs/edit-policy-total-threshold.png#lightbox)
4. Enter an **Alert percentage** to define when email notifications are sent relative to the total threshold.

    [![Screenshot of the alert percentage setting in the Edit policy panel.](media/billing-monitor-costs/edit-policy-alert-percentage.png)](media/billing-monitor-costs/edit-policy-alert-percentage.png#lightbox)
5. To block usage after the threshold is exceeded, enable **Enforcement.**

    [![Screenshot of the enforcement toggle enabled in the Edit policy panel.](media/billing-monitor-costs/edit-policy-enforcement-toggle.png)](media/billing-monitor-costs/edit-policy-enforcement-toggle.png#lightbox)
6. Review your settings and select **Submit.**

    [![Screenshot of submitting policy settings in the Configure Policies workflow.](media/billing-monitor-costs/configure-policies-submit.png)](media/billing-monitor-costs/configure-policies-submit.png#lightbox)
7. After enforcement is enabled and usage exceeds the configured threshold, supported actions fail. For KQL and Notebooks, users see a **Limit exceeded** error.

    [![Screenshot of the Limit exceeded error after threshold enforcement is triggered.](media/billing-monitor-costs/limit-exceeded-error.png)](media/billing-monitor-costs/limit-exceeded-error.png#lightbox)

## Using Azure Prepayment with Microsoft Sentinel

You can pay for Microsoft Sentinel charges with your Azure Prepayment credit. You can't use Azure Prepayment credit to pay non-Microsoft organizations for their products and services, or for products from Azure Marketplace.