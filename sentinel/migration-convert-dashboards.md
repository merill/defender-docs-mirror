---
layout: Conceptual
title: Convert Dashboards to Azure Workbooks in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/migration-convert-dashboards
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
description: Review, plan, and convert your existing dashboards to Azure Workbooks for Microsoft Sentinel.
author: EdB-MSFT
ms.author: edbaynash
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: d22f4a94-3726-6605-fc2e-d7f176ae10c6
document_version_independent_id: 6bf5126f-19b9-4d65-290f-db7ee7981de0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/migration-convert-dashboards.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/migration-convert-dashboards
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/migration-convert-dashboards.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 4082325f-bfc5-1ab2-7012-49509ea5f524
---

# Convert Dashboards to Azure Workbooks in Microsoft Sentinel | Microsoft Learn

Convert dashboards from your existing security information and event management (SIEM) solution to an Azure workbook for Microsoft Sentinel. Azure Workbooks provide versatility to create custom dashboards for Microsoft Sentinel. This article describes how to review, plan, and convert your current dashboards to Azure Workbooks.

## Review dashboards in your current SIEM

Consider the following steps when you design your migration.

- **Analyze dashboards**: Gather information about your dashboards, including design, parameters, data sources, and other details. Identify the purpose or usage of each dashboard.
- **Be selective**: Don't migrate all dashboards without consideration. Focus on dashboards that are critical and used regularly.
- **Consider permissions**: Consider who are the target users for workbooks. Azure Workbooks use Azure role-based access control (Azure RBAC). For more information, see [Assess control in Azure Workbooks](/en-us/azure/azure-monitor/visualize/workbooks-overview#access-control). To create dashboards outside Azure, for example for business executives without Azure access, use a reporting tool such as Power BI.

## Prepare for the dashboard conversion

After reviewing your dashboards, complete the following tasks to prepare for your dashboard migration:

- Review all of the visualizations in each dashboard. The dashboards in your current SIEM might contain several charts or panels. It's crucial to review the content of your short-listed dashboards to eliminate any unwanted visualizations or data.
- Capture the dashboard design and interactivity.
- Identify any design elements that are important to your users. For example, the layout of the dashboard, the arrangement of the charts, or even the font size or color of the graphs.
- Capture any interactivity such as drilldown, filtering, and others that you need to carry over to Azure Workbooks.
- Identify required parameters or user inputs. In most cases, you need to define parameters for users to perform search, filtering, or scoping the results (for example, date range, account name and others). Hence, it's crucial to capture the details around parameters. Here are some of the key parameter requirements to collect:

    - The type of parameter for users to perform selection or input; for example, date range, text, or others.
    - How the parameters are represented, such as drop-down, text box, or others.
    - The expected value format; for example, time, string, integer, or others.
    - Other properties, such as the default value, allow multi-select, conditional visibility, or others.

## Convert dashboards

To convert your dashboard, complete the following tasks in Azure Workbooks and Microsoft Sentinel.

### 1. Identify data sources

Azure Workbooks are compatible with a large number of data sources. For more information, see [Azure Workbooks data sources](/en-us/azure/azure-monitor/visualize/workbooks-data-sources). In most cases, use the Azure Monitor logs data source and Kusto Query Language (KQL) queries to visualize the underlying logs in your Microsoft Sentinel workspace.

### 2. Construct or review KQL queries

To construct or review your queries, you mainly work with KQL to visualize your data. You can construct and test your queries in Microsoft Sentinel before converting them to Azure Workbooks. To test the queries from Microsoft Sentinel in the Azure portal, go to **Logs**. From Microsoft Sentinel in the Defender portal, go to **Investigation & response** &gt; **Hunting** &gt; **Advanced hunting**.

Before finalizing your KQL queries, always review and tune the queries to improve query performance. Optimized queries:

- Run faster, reduce the overall duration of the query execution.
- Have a smaller chance of being throttled or rejected.

For more information, see the following resources:

- [KQL query best practices](/en-us/kusto/query/best-practices?view=microsoft-sentinel&amp;preserve-view=true&amp;toc=/azure/sentinel/TOC.json&amp;bc=/azure/sentinel/breadcrumb/toc.json)
- [Optimize queries in Azure Monitor Logs](/en-us/azure/azure-monitor/logs/query-optimization)
- [Optimizing KQL performance (webinar)](https://youtu.be/jN1Cz0JcLYU)

### 3. Create or update the workbook

Create a workbook, update the workbook, or clone an existing workbook so that you don't have to start from scratch. Also, specify how the data or visualizations is represented, arranged, and grouped. There are two common designs:

- Vertical workbook
- Tabbed workbook

For more information, see the following articles:

- [Visualize and monitor your data by using workbooks in Microsoft Sentinel](monitor-your-data)
- [Add groups in Azure Workbooks](/en-us/azure/azure-monitor/visualize/workbooks-create-workbook#add-groups)

### 4. Create or update workbook parameters or user inputs

After defining the workbook structure, you should have identified the required parameters for your workbook. With parameters, you can collect input from the consumers and reference the input in other parts of the workbook. This input is typically used to scope the result set, to set the correct visualization, and allows you to build interactive reports and experiences.

Workbooks allow you to control how your parameter controls are presented to consumers. For example, you select whether the controls are presented as a text box vs. drop-down, or single- vs. multi-select. You can also select which values to use, from text, JSON, KQL, or Azure Resource Graph, and more.

Review the [supported workbook parameters](/en-us/azure/azure-monitor/visualize/workbooks-parameters). You can reference these parameter values in other parts of the same workbook by using bindings or value expansions.

### 5. Create or update visualizations

Workbooks provide a rich set of capabilities for visualizing your data. Review the following detailed examples of each visualization type.

- [Text visualizations](/en-us/azure/azure-monitor/visualize/workbooks-text-visualizations)
- [Chart visualizations](/en-us/azure/azure-monitor/visualize/workbooks-chart-visualizations)
- [Grid visualizations](/en-us/azure/azure-monitor/visualize/workbooks-grid-visualizations)
- [Tile visualizations](/en-us/azure/azure-monitor/visualize/workbooks-tile-visualizations)
- [Tree visualizations](/en-us/azure/azure-monitor/visualize/workbooks-tree-visualizations)
- [Graph visualizations](/en-us/azure/azure-monitor/visualize/workbooks-graph-visualizations)
- [Map visualizations](/en-us/azure/azure-monitor/visualize/workbooks-map-visualizations)
- [Honeycomb visualizations](/en-us/azure/azure-monitor/visualize/workbooks-honey-comb)
- [Composite bar visualizations](/en-us/azure/azure-monitor/visualize/workbooks-composite-bar)

### 6. Preview and save the workbook

After you save your workbook, specify the parameters and validate the results. You can also try the [auto-refresh workbook data](tutorial-monitor-your-data#refresh-your-workbook-data) or the print feature to [print a workbook or save as PDF](monitor-your-data#print-a-workbook-or-save-as-pdf-azure-portal-only).