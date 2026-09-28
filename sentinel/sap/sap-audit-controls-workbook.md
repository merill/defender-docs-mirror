---
layout: Conceptual
title: Check for SAP security controls with Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/sap/sap-audit-controls-workbook
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
ms.subservice: sentinel-siem
search.appverid: met150
ms.reviewer: mapankra
description: Learn about the SAP - Security Audit Controls workbook, used to monitor and track security control framework compliance across your SAP systems.
ms.author: monaberdugo
author: mberdugo
ms.topic: concept-article
ms.date: 2024-07-04T00:00:00.0000000Z
ms.collection: usx-security
locale: en-us
document_id: 3a988ccb-3f85-7c15-573e-6b71e375915a
document_version_independent_id: d0aa2c90-ce8b-3eed-88de-53d90a3c9eec
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/sap/sap-audit-controls-workbook.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/sap/sap-audit-controls-workbook
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/sap/sap-audit-controls-workbook.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 518f9b33-af04-3637-f54a-9e2175fe979a
---

# Check for SAP security controls with Microsoft Sentinel | Microsoft Learn

This article describes how you can use the *SAP - Security Audit Controls* workbook to monitor and track security control framework compliance across your SAP systems, including the following functionality:

- See recommendations on which analytics rules to enable, and enable them in place with proper preset configuration.
- Associate your analytics rules to the SOX or NIST control framework, or apply your own custom control framework.
- Review incidents and alerts summarized by control, according to the selected control framework.
- Export relevant incidents for further analysis, for auditing and reporting purposes.

For example:

![Screenshot of the top of the SAP Audit Controls workbook.](media/sap-audit-controls-workbook/workbook-overview.png)

Content in this article is intended for your **security** team.

## Prerequisites

Before you can start using the **SAP - Security Audit log and Initial Access** workbook, you must have:

- A Microsoft Sentinel solution for SAP installed and a data connector configured. For more information, see [Deploy Microsoft Sentinel solution for SAP applications](deployment-overview).
- The **SAP Audit Controls** workbook installed in your Log Analytics workspace enabled for Microsoft Sentinel. For more information, see and [Visualize and monitor your data by using workbooks in Microsoft Sentinel](../monitor-your-data).
- At least one incident in your workspace, with at least one entry available in the `SecurityIncident` table. This doesn't need to be an SAP incident, and you can generate a demo incident using a basic analytics rule if you don't have another one.

We recommend that you configure auditing for *all* messages from the audit log, instead of only specific logs. Ingestion cost differences are generally minimal and the data is useful for Microsoft Sentinel detections and in post-compromise investigations and hunting. For more information, see [Configure SAP auditing](preparing-sap#configure-sap-auditing).

## View a demo

View a demonstration of this workbook: 

For more information, see the [Microsoft Security Community YouTube channel](https://www.youtube.com/@MicrosoftSecurityCommunity):

## Supported filters

The **SAP Audit Controls** workbook supports the following filters to help you focus on the data you need:

| Filter option | Description |
| --- | --- |
| **Subscription** and **Workspace** | Select the workspace whose SAP systems' compliance you wish to audit. This can be a different workspace than where Microsoft Sentinel is deployed. |
| **Incident creation time** | Select a range from the last four hours to the last 30 days, or a custom range that you determine. |
| Other incident attributes, including **Status**, **Severity**, **Tactics**, **Owner** | For each of these, select from the available choices, which correspond to the values represented in the incidents in the selected time range. |
| **System roles** | The SAP system roles, such as *Production*. |
| **System usage** | The SAP system usage, such as *SAP ERP*. |
| **Systems** | Select all SAP system IDs, a specific system ID, or multiple system IDs. |
| **Control framework**, **Control families**, **Control IDs** | Select the control framework by which you want to evaluate your coverage, and the specific controls by which you want to filter the workbook data. |

## Data retention recommendations

The **SAP Audit Controls** dashboards provide an aggregated view of incidents and alerts based on the *SecurityAlert* and *SecurityIncident* tables, which, by default, retain 30 days of data.

Consider extending the retention period for these tables to match your organization's compliance requirements. Regardless of the choice you make for the retention policy of these tables, the incident data is never deleted, though it might not show here. Alert data is kept according to the table's retention policy.

The actual retention policy of the *SecurityAlert* and *SecurityIncident* tables might well be defined as something other than the default 30 days. See the notice on the blue-shaded background in the workbook, showing the actual time range of data in the tables according to their current retention policy.

For more information, see [Configure a data retention policy for a table in a Log Analytics workspace](../configure-data-retention).

## Configure tab - create analytics rules from yet-unused templates

The **Templates ready to be used** table on the **Configure** tab shows the [analytics rule templates](../detect-threats-built-in) from the Microsoft Sentinel solution for SAP applications that haven't yet been implemented as active rules. You might need to create these rules to achieve compliance. For example:

![Screenshot of table of analytics rule templates from which to create rules.](media/sap-audit-controls-workbook/configure-templates.png)

By default, this table is filtered for **SAP**, with **SAP** selected in the **Solution templates to configure** dropdown. Select any or all other solutions from this dropdown to populate the **Templates ready to be used** table further.

For each row in the table, select **View** for more read-only details about rule configuration.

The **Recommended configuration** column shows the purpose of the rule: is it meant to create [incidents](../incident-investigation) for investigation? Or only to create alerts to be held aside and added to other incidents to be used as evidence in their investigations?

Select **Activate rule** in the side pane to create an analytics rule from the template, with the recommended configuration already built in. This functionality saves you the trouble of having to guess at the right configuration and [define it manually](../detect-threats-custom).

## Configure tab - View or change security control assignments of your analytics rules

The **Select a rule to configure** table on the **Configure** tab shows a list of activated analytics rules relevant to SAP. For example:

[![Screenshot of selecting a rule to configure.](media/sap-audit-controls-workbook/configure-rule.png)](media/sap-audit-controls-workbook/configure-rule-zoom.png#lightbox)

In the table, check:

- The count and graph lines generated by each rule in the **Incidents** and **Alerts** columns. Identical counts suggest that [alert grouping is disabled](../detect-threats-custom#alert-grouping).
- The **Incidents** and **Source** column values to understand whether the rule is [set to create incidents](../detect-threats-custom#configure-the-incident-creation-settings) .
- Whether the **Recommended configuration** for a rule is *As alert only*. If so, consider [turning off the incident creation setting](../detect-threats-custom#configure-the-incident-creation-settings) in the rule.

Select a rule to view a details pane with more information. For example:

![Screenshot of rule configuration side panel.](media/sap-audit-controls-workbook/rule-configuration.png)

- The upper part of this side panel has recommendations regarding enabling or disabling incident creation in the analytics rule configuration.
- The next section of the side pane shows which security controls and control families the rule is identified with, for each of the available frameworks.

    - For the SOX and NIST frameworks, customize the control assignment by choosing a different control or control family from the relevant drop-downs.
    - For custom frameworks, enter in controls and control families of your choosing in the **MyOrg** text boxes. If you make any changes, select **Save changes**.

    If a particular analytics rule hasn't been assigned a security control or control family for a given framework, you're prompted to set the controls manually. After you select the controls, select **Save changes**.

    To see the rest of the details of the selected rule as currently defined, select **Rule overview**.

## Monitor tab

The **Monitor** tab contains several graphical representations of various groupings of the incidents in your environment that match the filters at the top of the workbook:

- A trend line graph, labeled **Incidents trend**, shows the numbers of incidents over time. These incidents are grouped, and represented by different colored lines and shadings, by default according to the control family represented by the rule that generated them. Select alternate groupings for these incidents from the **Detail incidents by** drop-down. For example:

    ![Screenshot of trendline of numbers of incidents, grouped by rule.](media/sap-audit-controls-workbook/incident-trend-graph.png)
- The **Incidents hive** graph shows numbers of incidents grouped in two ways. The defaults for the SOX framework are first by **SOX Control family**, which is the *honeycomb* array of cells, and then by **System ID**, which is each cell in the honeycomb. Select different criteria by which to display the groupings, using the **Drill by** and **And then by** selectors.

Zoom in to the hive graph to make the text large enough to read clearly, and zoom out to see all the groupings together. Drag the whole graph to see different parts of it. For example:

![Screenshot of hive graphs of numbers of incidents, grouped by control family and system ID.](media/sap-audit-controls-workbook/incident-hive-graph.png)

## Report tab

The **Report** tab contains a list of all the incidents in your environment that match the filters at the top of the workbook.

- The incidents are grouped by control family and control ID.
- The link in the **Incident URL** column opens a new browser window open to the incident investigation page for that incident. This link is persistent, and will work regardless of the retention policy for the *SecurityIncident* table.
- Scroll down to the end of the window (the outer scroll bar) to see the horizontal scroll bar, which you can use to see the rest of the columns in the report.
- Export this report to a spreadsheet by selecting the ellipsis (the three dots) in the upper right-hand corner of the report, then selecting **Export to Excel**.

    [![Screenshot of the Report tab in the workbook.](media/sap-audit-controls-workbook/incidents-report.png)](media/sap-audit-controls-workbook/incidents-report.png#lightbox)

    ![Screenshot of the export to excel option.](media/sap-audit-controls-workbook/export-report.png)