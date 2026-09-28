---
layout: Conceptual
title: Work with threat intelligence - Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/work-with-threat-indicators
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
description: This article explains how to view, create, manage, and visualize threat intelligence in Microsoft Sentinel.
ms.author: guywild
author: guywi-ms
ms.reviewer: yoninave
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.collection: usx-security
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 997835ae-56e1-5cad-7894-08dcafd12cf5
document_version_independent_id: e4c59ef7-f3b0-619e-1a9f-d75ba8a7b05c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/work-with-threat-indicators.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/work-with-threat-indicators
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/work-with-threat-indicators.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: 7fd02022-77da-a58b-6fa8-79b1e623372b
---

# Work with threat intelligence - Microsoft Sentinel | Microsoft Learn

Use Microsoft Sentinel threat intelligence to create, manage, search, and visualize threat intelligence. In the Defender portal, manage threat intelligence in **Intel explorer**. In the Azure portal, use the **Threat intelligence** page.

- Create threat intelligence objects using structured threat information expression (STIX).
- Manage threat intelligence by viewing, curating, and visualizing it.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Prerequisites

- You need the permissions of a [Microsoft Sentinel Contributor](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-contributor) or higher role assigned to your user account to manage threat intelligence.
- To import and export threat intelligence, you need to install the Threat Intelligence solution in Microsoft Sentinel and enable the relevant connectors, as described in [Use STIX/TAXII to import and export threat intelligence in Microsoft Sentinel](connect-threat-intelligence-taxii#enable-the-threat-intelligence---taxii-export-data-connector).

## Access threat intelligence

Access threat intelligence from either the Defender portal or the Azure portal. The navigation and search experience differ between portals, while creation and other management tasks use the same workflows.

# [Access Intel explorer in the Defender portal](#tab/defender-portal)
In the Defender portal, navigate to **Threat intelligence** &gt; **Intel explorer**.

# [Access threat intelligence in the Azure portal](#tab/azure-portal)
In the Azure portal, navigate to **Threat management** &gt; **Threat intelligence**.

![Screenshot showing threat intelligence menu for Microsoft Sentinel in the Azure portal.](media/work-with-threat-indicators/threat-intelligence-sentinel.png)

---

## Create threat intelligence

Use the management interface to create STIX objects and perform other common threat intelligence tasks such as indicator tagging and establishing connections between objects.

- Define relationships as you create new STIX objects.
- Quickly create multiple objects by using the duplicate feature to copy the metadata from a new or existing TI object.

For more information on supported STIX objects, see [Threat intelligence in Microsoft Sentinel](understand-threat-intelligence#create-and-manage-threat-intelligence).

### Create a new STIX object

To create a new STIX object in the management interface, complete the following steps.

1. Select **Add new** &gt; **TI object**.

    [![Screenshot that shows adding a new threat indicator.](media/work-with-threat-indicators/threat-intel-add-new-indicator.png)](media/work-with-threat-indicators/threat-intel-add-new-indicator.png#lightbox)
2. Choose the **Object type**, then fill in the form on the **New TI object** page. Required fields are marked with a red asterisk (\*).
3. Consider designating a sensitivity value, or **Traffic light protocol** (TLP) rating to the TI object. For more information on what sensitivity values and TLP ratings represent, see [Curate threat intelligence](understand-threat-intelligence#curate-threat-intelligence).
4. If you know how this object relates to another threat intelligence object, indicate that connection with the **Relationship type** and the **Target reference**.
5. Select **Add** for an individual object, or **Add and duplicate** if you want to create more items with the same metadata. When you select **Add and duplicate**, the common metadata section of each STIX object is copied to the new object.

![Screenshot showing new STIX object creation and the common metadata available to all objects.](media/work-with-threat-indicators/common-metadata-stix-object-reduced.png)

## Manage threat intelligence

Optimize threat intelligence from your sources with ingestion rules. Curate existing threat intelligence with the relationship builder, search and filter threat intelligence, and add tags to threat intelligence objects.

### Optimize threat intelligence feeds with ingestion rules

Reduce noise from your TI feeds, extend the validity of high value indicators, and add meaningful tags to incoming objects. These tasks are just some of the use cases for ingestion rules. Here are the steps for extending the `Valid until` date on high value indicators.

1. Select **Ingestion rules** to open a whole new page to view existing rules and construct new rule logic.

    ![Screenshot showing threat intelligence management menu hovering on ingestion rules.](media/work-with-threat-indicators/select-ingestion-rules.png)
2. Enter a descriptive name for your rule. The ingestion rules page has ample rule for the name, but it's the only text description available to differentiate your rules without editing them.
3. Select the **Object type**. The example of extending indicator validity is based on the `Valid from` property, which is only available for `Indicator` object types.
4. **Add condition** for `Source``Equals` and select your high value `Source`.
5. **Add condition** for `Confidence``Greater than or equal` and enter a `Confidence` score.
6. Select the **Action**. Since the rule should modify matching indicators, select `Edit`.
7. Select the **Add action** for `Valid until`, `Extend by`, and select a time span in days.
8. Consider adding a tag to indicate the high value placed on these indicators, like `Extended`. The object's `Modified` date field isn't updated by ingestion rules.
9. Select the **Order** you want the rule to run. Rules run from lowest order number to highest. Each rule evaluates every object ingested.
10. If the rule is ready to be enabled, toggle **Status** to on.
11. Select **Add** to create the ingestion rule.

![Screenshot showing new ingestion rule creation for extending valid until date.](media/work-with-threat-indicators/new-ingestion-rule.png)

For more information, see [Threat intelligence ingestion rules](understand-threat-intelligence#configure-ingestion-rules).

### Curate threat intelligence with the relationship builder

Connect threat intelligence objects with the relationship builder. There's a maximum of 20 relationships in the builder at once, but more connections can be created through multiple iterations and by adding relationship target references for new objects.

1. Select **Add new** &gt; **TI relationship**.
2. Start with an existing TI object like a threat actor or attack pattern where the single object connects to one or more existing objects, like indicators.
3. Add the relationship type according to the best practices outlined in the following table and in the [STIX 2.1 reference relationship summary table](https://docs.oasis-open.org/cti/stix/v2.1/os/stix-v2.1-os.html#_6n2czpjuie3v):

    | Relationship type | Description |
    | --- | --- |
    | **Duplicate of** **Derived from** **Related to** | Common relationships defined for any STIX domain object (SDO)For more information, see [STIX 2.1 reference on common relationships](https://docs.oasis-open.org/cti/stix/v2.1/os/stix-v2.1-os.html#_f3dx2rhc3vl) |
    | **Targets** | `Attack pattern` or `Threat actor` Targets `Identity` |
    | **Uses** | `Threat actor` Uses `Attack pattern` |
    | **Attributed to** | `Threat actor` Attributed to `Identity` |
    | **Indicates** | `Indicator` Indicates `Attack pattern` or `Threat actor` |
    | **Impersonates** | `Threat actor` Impersonates `Identity` |
4. As an example of a relationship-builder configuration, you can connect a threat actor to an attack pattern, indicator, and identity in the Defender portal.

    [![Screenshot showing the relationship builder.](media/work-with-threat-indicators/relationship-example-defender-portal.png)](media/work-with-threat-indicators/relationship-example-defender-portal.png#lightbox)
5. Complete the relationship by configuring **Common** properties.

### Search and filter threat intelligence

# [Defender portal](#tab/defender-portal)
Use **Intel explorer** to search and filter threat intelligence without writing a query. Intel explorer brings together threat intelligence objects and Threat analytics reports in a single experience.

1. In the [Microsoft Defender portal](https://security.microsoft.com/), select **Threat intelligence** &gt; **Intel explorer**.
2. Enter a keyword or value in the search box.
3. Select a threat intelligence type to narrow the results.
4. Use **Targeted industries** or **Source** to filter the results.
5. To filter by attributes for the selected threat intelligence type, select **Add filter**.
6. Select an available attribute.
7. Configure the filter.
8. Select an object to view its details.

Note

Changes to threat intelligence might take a few minutes to appear in Intel explorer. If you don't see a recent change, refresh the page after a few minutes.

# [Azure portal](#tab/azure-portal)
Use the threat intelligence management interface to sort, filter, and search your threat intelligence without writing a Log Analytics query.

1. Expand the **What would you like to search?** menu.
2. Select a STIX object type or leave the default **All object types**.
3. Select conditions using logical operators.
4. Select the object you want to view.

For example, you can search by multiple sources by placing them in an `OR` group, while grouping multiple conditions with the `AND` operator.

[![Screenshot showing an OR operator combined with multiple AND conditions to search threat intelligence.](media/work-with-threat-indicators/advanced-search.png)](media/work-with-threat-indicators/advanced-search.png#lightbox)

---

Microsoft Sentinel only displays the most current version of your threat intel in the management interface. For more information on how objects are updated, see [Threat intelligence lifecycle](understand-threat-intelligence#threat-intelligence-lifecycle).

IP and domain name indicators are enriched with extra `GeoLocation` and `WhoIs` data so you can provide more context for any investigations where the indicator is found.

Here's an example of an indicator enriched with `GeoLocation` and `WhoIs` data.

[![Screenshot that shows the Threat intelligence page with an indicator showing GeoLocation and WhoIs data.](media/work-with-threat-indicators/geolocation-whois-unified.png)](media/work-with-threat-indicators/geolocation-whois-unified.png#lightbox)

Important

`GeoLocation` and `WhoIs` enrichment is currently in preview. The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include more legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

### Tag and edit threat intelligence

Tagging threat intelligence is a quick way to group objects together to make them easier to find. Typically, you might apply tags related to a particular incident. But, if an object represents threats from a particular known actor or well-known attack campaign, consider creating a relationship instead of a tag.

1. Search and filter for the threat intelligence objects that you want to update.
2. After you find the objects you want to work with, multiselect them choosing one or more objects of the same type.
3. Select **Add tags** and tag them all at once with one or more tags.
4. Because tagging is free-form, we recommend that you create standard naming conventions for tags in your organization.

Edit threat intelligence one object at a time, whether created directly in Microsoft Sentinel or from partner sources, like TIP and TAXII servers. For threat intel created in the management interface, all fields are editable. For threat intel ingested from partner sources, only specific fields are editable, including tags, **Expiration date**, **Confidence**, and **Revoked**. Whether the threat intel was created in Microsoft Sentinel or ingested from a partner source, only the latest version of the object appears in the management interface.

For more information on how threat intel is updated, see [View your threat intelligence](understand-threat-intelligence#view-your-threat-intelligence).

### Find and view threat intelligence with queries

View your threat intelligence with queries, regardless of the source feed or method you used to ingest them.

Threat indicators are stored in the Microsoft Sentinel `ThreatIntelIndicators` table. The `ThreatIntelIndicators` table is the basis for threat intelligence queries performed by other Microsoft Sentinel features, such as **Analytics**, **Hunting**, and **Workbooks**.

# [Defender portal](#tab/defender-portal)
To view threat intelligence queries in the Defender portal, complete the following steps.

1. For Microsoft Sentinel in the [Defender portal](https://security.microsoft.com/), select **Investigation & response** &gt; **Hunting** &gt; **Advanced hunting**.
2. The `ThreatIntelIndicators` table is located under the **Microsoft Sentinel** group.

[![Screenshot of add watchlist option on watchlist page.](media/work-with-threat-indicators/table-results-advanced-hunting.png)](media/work-with-threat-indicators/table-results-advanced-hunting.png#lightbox)

# [Azure portal](#tab/azure-portal)
To view threat intelligence queries in the Azure portal, complete the following steps.

1. For Microsoft Sentinel in the [Azure portal](https://portal.azure.com), under **General**, select **Logs**.
2. Select the **Preview data** icon (the eye) next to the table name. Select **See in query editor** to run a query that shows records from the `ThreatIntelIndicators` table.

Your results should look similar to the sample `ThreatIntelligenceIndicator` table results with expanded details.

[![Screenshot that shows sample ThreatIntelIndicators table results with the details expanded.](media/work-with-threat-indicators/table-results.png)](media/work-with-threat-indicators/table-results.png#lightbox)

---

For more information, see [View your threat intelligence](understand-threat-intelligence#view-your-threat-intelligence).

### Visualize your threat intelligence with workbooks

Use a purpose-built Microsoft Sentinel workbook to visualize key information about your threat intelligence in Microsoft Sentinel, and customize the workbook according to your business needs.

To find the threat intelligence workbook in Microsoft Sentinel and customize it, complete the following steps.

1. From the [Azure portal](https://portal.azure.com/), go to **Microsoft Sentinel**.
2. Choose the workspace to which you imported threat indicators by using either threat intelligence data connector.
3. Under the **Threat management** section of the Microsoft Sentinel menu, select **Workbooks**.
4. Find the workbook titled **Threat Intelligence**. Verify that you have data in the `ThreatIntelIndicators` table.

    ![Screenshot that shows verifying that you have data.](media/work-with-threat-indicators/threat-intel-verify-data.png)
5. Select **Save**, and choose an Azure location in which to store the workbook. Saving the workbook is required if you intend to modify the workbook in any way and save your changes.
6. Now select **View saved workbook** to open the workbook for viewing and editing.
7. You should now see the default charts provided by the template. To modify a chart, select **Edit** at the top of the page to start the editing mode for the workbook.
8. Add a new chart of threat indicators by threat type. Scroll to the bottom of the page and select **Add Query**.
9. Add the following text to the **Log Analytics workspace Log Query** text box:

    ```kusto
    ThreatIntelligenceIndicator
    | summarize count() by ThreatType
    ```

    For more information about the `summarize` operator and the `count()` aggregation function used in this query, see the Kusto documentation:

    - [***summarize*** operator](/en-us/kusto/query/summarize-operator?view=microsoft-sentinel&amp;preserve-view=true)
    - [***count()*** aggregation function](/en-us/kusto/query/count-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true)
10. On the **Visualization** dropdown menu, select **Bar chart**.
11. Select **Done editing**, and view the new chart for your workbook.

    ![Screenshot that shows a bar chart for the workbook.](media/work-with-threat-indicators/threat-intel-bar-chart.png)

Workbooks provide powerful interactive dashboards that give you insights into all aspects of Microsoft Sentinel. You can do many tasks with workbooks, and the provided templates are a great starting point. Customize the templates or create new dashboards by combining many data sources so that you can visualize your data in unique ways.

Microsoft Sentinel workbooks are based on Azure Monitor workbooks, so extensive documentation and many more templates are available. For more information, see [Create interactive reports with Azure Monitor workbooks](/en-us/azure/azure-monitor/visualize/workbooks-overview).

There's also a rich resource for [Azure Monitor workbooks on GitHub](https://github.com/microsoft/Application-Insights-Workbooks), where you can download more templates and contribute your own templates.

## Export threat intelligence

Microsoft Sentinel lets you export threat intelligence to other destinations. For example, if you've ingested threat intelligence using the **Threat Intelligence - TAXII** data connector, you can export threat intelligence back to the source platform for bi-directional intelligence sharing. The Microsoft Sentinel threat intelligence export feature reduces the need for manual processes or custom playbooks to distribute threat intelligence.

Important

Carefully consider both the threat intelligence data you export and its destination, which might reside in a different geographic or regulatory region. Data export cannot be undone. Ensure you own the data or have proper authorization before exporting or sharing threat intelligence with third parties.

To export threat intelligence:

1. For Microsoft Sentinel in the [Defender portal](https://security.microsoft.com/), select **Threat intelligence** &gt; **Intel explorer**. For Microsoft Sentinel in the [Azure portal](https://portal.azure.com), select **Threat management** &gt; **Threat intelligence**.
2. Select one or more STIX objects, and then select **Export**![](media/work-with-threat-indicators/export-icon.png) in the toolbar at the top of the page. For example:

# [Defender portal](#tab/defender-portal)
[![Screenshot of the Export TI option in the Defender portal.](media/work-with-threat-indicators/export-defender.png)](media/work-with-threat-indicators/export-defender.png#lightbox)

# [Azure portal](#tab/azure-portal)
[![Screenshot of the Export TI option in the Defender portal.](media/work-with-threat-indicators/export-azure.png)](media/work-with-threat-indicators/export-azure.png#lightbox)

---
3. In the **Export** pane, from the **Export TI** dropdown, select the server you want to export your threat intelligence to.

    If there isn't a server listed, you need to configure a TAXII 2.1 server for export first, as described in [Enable the Threat intelligence - TAXII Export data connector](connect-threat-intelligence-taxii#enable-the-threat-intelligence---taxii-export-data-connector). Microsoft Sentinel currently supports exporting to TAXII 2.1-based platforms only.
4. Select **Export**.

    Important

    When you export threat intelligence objects, the system carries out a bulk operation. A known issue exists where this bulk operation sometimes fails. If the bulk export operation fails, you'll see a warning when you open the Export side panel, asking you to remove the failed action from the bulk operations history view. Microsoft Sentinel pauses subsequent export operations until you remove the failed operation.

**To access the export history**:

1. Navigate to the exported item in either **Intel explorer** (Defender portal) or the **Threat intelligence** page (Azure portal).
2. In the **Exports** column, select **View export history** to show the export history for that item.