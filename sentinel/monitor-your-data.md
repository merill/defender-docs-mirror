---
layout: Conceptual
title: Visualize your Data by using Workbooks in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/monitor-your-data
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
description: Create and customize Microsoft Sentinel workbooks to visualize and monitor security data using built-in templates or custom designs, with access managed through Azure RBAC.
author: EdB-MSFT
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.author: edbaynash
ms.collection: usx-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 660f62ae-bcdc-7c53-93a6-523097435bd1
document_version_independent_id: 8526895c-7c4d-956f-0b0b-b2d955a110a5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/monitor-your-data.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/monitor-your-data
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/monitor-your-data.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 1ac455d6-d383-2f56-dada-863ca48b76e0
---

# Visualize your Data by using Workbooks in Microsoft Sentinel | Microsoft Learn

After you connect your data sources to Microsoft Sentinel, visualize and monitor the data using workbooks in Microsoft Sentinel. Microsoft Sentinel workbooks are based on Azure Monitor workbooks, and add tables and charts with analytics for your logs and queries to the tools already available in Azure.

Microsoft Sentinel allows you to create custom workbooks across your data or use existing workbook templates available with packaged solutions or as standalone content from the content hub. Each workbook is an Azure resource like any other, and you can assign it with Azure role-based access control (RBAC) to define and limit who can access.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Prerequisites

Before you create or use workbooks, make sure you meet the following prerequisites:

- You must have at least **Workbook reader** or **Workbook contributor** permissions on the resource group of the Microsoft Sentinel workspace.

    The workbooks that you see in Microsoft Sentinel are saved within the Microsoft Sentinel workspace's resource group and are tagged by the workspace in which they were created.
- To use a workbook template, install the solution that contains the workbook or install the workbook as a standalone item from the **Content Hub**. For more information, see [Discover and manage Microsoft Sentinel out-of-the-box content](sentinel-solutions-deploy).
- If you're working in the Defender portal with an Azure Data Explorer data source, make sure to configure and authenticate to Azure Data Explorer from the Defender portal.

## Create a workbook from a template

Use a template installed from the content hub to create a workbook.

1. In Microsoft Sentinel, select **Threat management &gt; Workbooks**.
2. On the **Workbooks** page, select the **Templates** tab to see the list of workbook templates installed. Select a template to view its details.

    Some workbooks require specific data connections to function. Before saving a workbook, check for a **Required data types** field ensure that you have that type of data ingested.

    For example:

# [Defender portal](#tab/defender-portal)
[![Screenshot of a workbook template in the Defender portal that shows the required data types.](media/monitor-your-data/workbook-template-defender-portal.png)](media/monitor-your-data/workbook-template-defender-portal.png#lightbox)

# [Azure portal](#tab/azure-portal)
[![Screenshot of a workbook template with required data types shown in the details pane.](media/monitor-your-data/workbook-template-azure-portal.png)](media/monitor-your-data/workbook-template-azure-portal.png#lightbox)

---
3. From the details pane, select **Save**, then select the location where you want to save the workbook. Saving the workbook creates an Azure resource in the selected location based on the relevant template. Only the workbook's JSON file is saved in this location, and no data.
4. From the details pane, select **View saved workbook** to open it for editing.
5. With the workbook open, select **Edit** to customize the workbook according to your needs.

# [Defender portal](#tab/defender-portal)
[![Screenshot that shows the saved workbook.](media/monitor-your-data/workbook-graph-defender.png)](media/monitor-your-data/workbook-graph.png#lightbox)

When working in the Defender portal, some visualizations can only be viewed in the Azure portal. In such cases, select **Open in Azure** to open the workbook in the Azure portal.

# [Azure portal](#tab/azure-portal)
[![Screenshot that shows the saved workbook.](media/monitor-your-data/workbook-graph.png)](media/monitor-your-data/workbook-graph.png#lightbox)

---

    For example, select the **TimeRange** filter to view data for a different time range than the current selection. To edit a specific workbook area, either select **Edit** or select the ellipsis (**...**) to add elements, or move, clone, or remove the area.

    To clone your workbook, select **Save as**. Save the clone with another name, under the same subscription and resource group. Cloned workbooks are also displayed under the **My workbooks** tab in the **Microsoft Sentinel &gt; Threat management &gt; Workbooks** page.
6. When you're done, select **Done Editing** to save your changes.

For more information, see:

- [Create interactive reports with Azure Monitor Workbooks](/en-us/azure/azure-monitor/visualize/workbooks-overview)
- [Tutorial: Visual data in Log Analytics](/en-us/azure/azure-monitor/visualize/tutorial-logs-dashboards)

## Create a new workbook

Create a workbook from scratch in Microsoft Sentinel.

1. In Microsoft Sentinel, select **Threat management &gt; Workbooks**, and then select **Add workbook**.
2. To edit the workbook, select **Edit**, and then add text, queries, and parameters as necessary.

    For more information on how to customize the workbook, see how to [Create interactive reports with Azure Monitor Workbooks](/en-us/azure/azure-monitor/visualize/workbooks-overview).

    [![Screenshot that shows a new workbook.](media/monitor-your-data/create-workbook.png)](media/monitor-your-data/create-workbook.png#lightbox)
3. When building a query, set the **Data source** to **Logs** and **Resource type** to **Log Analytics**, then choose one or more workspaces.

    We recommend that your query uses an [Advanced Security Information Model (ASIM) parser](normalization-about-parsers) and not a built-in table. A query that uses an ASIM parser supports any current or future relevant data source rather than a single data source.
4. When you're done with your edits, select **Done editing** and then **Save**. In the side pane, enter a meaningful name for your workbook, and select the subscription and resource group for your workspace.
5. When working in the Azure portal, switch between workbooks in your workspace by selecting **Open**![Screenshot of the Open button used to switch between saved workbooks in your workspace.](media/monitor-your-data/switch.png) in the toolbar of any workbook. The workbook view switches to a list of other saved workbooks you can open.

    Select the workbook you want to open:

    [![Screenshot that shows how to switch workbooks.](media/monitor-your-data/switch-workbooks.png)](media/monitor-your-data/switch-workbooks.png#lightbox)

## Create new tiles for your workbooks

To add a custom tile to a Microsoft Sentinel workbook, first create the tile in Log Analytics. For more information, see [Visual data in Log Analytics](/en-us/azure/azure-monitor/visualize/tutorial-logs-dashboards).

Once you create a tile, select **Pin** and then select the workbook where you want the tile to appear.

## Refresh your workbook data

Refresh your workbook to display updated data. In the toolbar, select one of the following options:

- ![](media/monitor-your-data/manual-refresh-button.png)**Refresh**, to manually refresh your workbook data.
- ![](media/monitor-your-data/auto-refresh-workbook.png)**Auto refresh**, to set your workbook to automatically refresh at a configured interval.

    - Supported auto refresh intervals range from **5 minutes** to **1 day**.
    - Auto refresh is paused while you're editing a workbook, and intervals are restarted each time you switch back to view mode from edit mode.
    - Auto refresh intervals are also restarted if you manually refresh your data.

        By default, auto refresh is turned off. If you've turned auto-refresh on, it's turned off again each time you close the notebook to optimize perforamnce and prevent it from running in the background. Turn auto refresh back on as needed the next time you open the workbook.

## Print a workbook or save as PDF (Azure portal only)

To print a workbook, or save it as a PDF, use the options menu to the right of the workbook title. The print and Save as PDF options are available only in the Azure portal. If you're working in the Defender portal, select **Open in Azure** to open the workbook in the Azure portal.

1. Select options &gt; ![](media/monitor-your-data/print-icon.png)**Print content**.
2. In the print screen, adjust your print settings as needed or select **Save as PDF** to save it locally.

    For example:

    ![Screenshot that shows how to print your workbook or save as PDF.](media/monitor-your-data/print-workbook.png)

## Delete one or more workbooks

You can delete both saved templates and customized workbooks from the **My workbooks** tab. Templates themselves can't be deleted.

Warning

Deleting a workbook permanently removes the workbook resource and any customizations you made to the template. This action can't be undone. The workbook template that the deleted workbook was based on remains available.

To delete a workbook, select the workbook in the **My workbooks** tab, and then select **Delete**.

## Workbook recommendations

The following recommendations help you use Microsoft Sentinel workbooks effectively.

### Add Microsoft Entra ID workbooks

If you use Microsoft Entra ID with Microsoft Sentinel, we recommend that you install the Microsoft Entra solution for Microsoft Sentinel and use the following workbooks:

- **Microsoft Entra sign-ins** analyzes sign-ins over time to see if there are anomalies. This workbook provides failed sign-ins by applications, devices, and locations so that you can notice, at a glance if something unusual happens. Pay attention to multiple failed sign-ins.
- **Microsoft Entra audit logs** analyzes admin activities, such as changes in users (add, remove, etc.), group creation, and modifications.

### Add firewall workbooks

We recommend that you install the appropriate solution from the **Content hub** to add a workbook for your firewall.

For example, install the Palo Alto firewall solution for Microsoft Sentinel to add the Palo Alto workbooks. The Palo Alto workbooks analyze your firewall traffic, providing you with correlations between your firewall data and threat events, and highlight suspicious events across entities.

![Screenshot of the Palo Alto workbook.](media/qs-get-visibility/palo-alto-week-query.png)

### Create different workbooks for different uses

We recommend creating different visualizations for each type of persona that uses workbooks, based on the persona's role and what they're looking for. For example, create a workbook for your network admin that includes the firewall data.

Alternately, create workbooks based on how frequently you want to look at them, whether there are things you want to review daily, and others items you want to check once an hour. For example, you might want to look at your Microsoft Entra sign-ins every hour to search for anomalies.

### Sample query for comparing traffic trends across weeks

Use the following query to create a visualization that compares traffic trends across weeks. Switch the device vendor and data source you run the query on, depending on your environment.

The following sample query uses the **SecurityEvent** table from Windows. You might want to switch it to run on the **AzureActivity** or **CommonSecurityLog** table, on any other firewall.

The query compares daily security event counts between the current week and the previous week, so you can quickly spot unusual changes in event volume.

```kusto
// week over week query
SecurityEvent
| where TimeGenerated > ago(14d)
| summarize count() by bin(TimeGenerated, 1d)
| extend Week = iff(TimeGenerated>ago(7d), "This Week", "Last Week"), TimeGenerated = iff(TimeGenerated>ago(7d), TimeGenerated, TimeGenerated + 7d)
```

### Sample query with data from multiple sources

You might want to create a query that incorporates data from multiples sources. For example, create a query that looks at Microsoft Entra audit logs for new users that were created, and then checks your Azure activity logs to see if the user started making Azure RBAC role assignment changes within 24 hours of creation. That suspicious activity would show up in a visualization with the following query.

The following query finds newly created users in Microsoft Entra audit logs and joins them with Azure activity logs to detect role assignment changes made within 24 hours of user creation.

```kusto
AuditLogs
| where OperationName == "Add user"
| project AddedTime = TimeGenerated, user = tostring(TargetResources[0].userPrincipalName)
| join (AzureActivity
| where OperationName == "Create role assignment"
| project OperationName, RoleAssignmentTime = TimeGenerated, user = Caller) on user
| project-away user1
```

See more information on the following items used in the preceding examples in the Kusto documentation:

- [***where*** operator](/en-us/kusto/query/where-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***extend*** operator](/en-us/kusto/query/extend-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***project*** operator](/en-us/kusto/query/project-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***project-away*** operator](/en-us/kusto/query/project-away-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***join*** operator](/en-us/kusto/query/join-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***summarize*** operator](/en-us/kusto/query/summarize-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***ago()*** function](/en-us/kusto/query/ago-function?view=microsoft-sentinel&amp;preserve-view=true)
- [***bin()*** function](/en-us/kusto/query/bin-function?view=microsoft-sentinel&amp;preserve-view=true)
- [***iff()*** function](/en-us/kusto/query/iff-function?view=microsoft-sentinel&amp;preserve-view=true)
- [***tostring()*** function](/en-us/kusto/query/tostring-function?view=microsoft-sentinel&amp;preserve-view=true)
- [***count()*** aggregation function](/en-us/kusto/query/count-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true)

For more information on KQL, see [Kusto Query Language (KQL) overview](/en-us/kusto/query/?view=microsoft-sentinel&amp;preserve-view=true).

Other resources:

- [KQL quick reference](/en-us/kusto/query/kql-quick-reference?view=microsoft-sentinel&amp;preserve-view=true)
- [Kusto Query Language learning resources](/en-us/kusto/query/kql-learning-resources?view=microsoft-sentinel&amp;preserve-view=true)