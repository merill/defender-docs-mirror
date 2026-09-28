---
layout: Conceptual
title: Hunt with bookmarks in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/bookmarks
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
description: This article describes how to use the Microsoft Sentinel hunting bookmarks to keep track of data.
ms.author: monaberdugo
author: mberdugo
ms.reviewer: efratka
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 02ce3538-bc10-700d-85fb-8150b3a44eae
document_version_independent_id: 1c756eaf-200f-9391-d129-a30d5d76b391
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/bookmarks.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/bookmarks
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/bookmarks.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: fd2f5032-0b7f-da36-bb8b-1aa4051b947a
---

# Hunt with bookmarks in Microsoft Sentinel | Microsoft Learn

Hunting bookmarks in Microsoft Sentinel helps you preserve the queries and query results that you deem relevant. You can also record your contextual observations and reference your findings by adding notes and tags. Bookmarked data is visible to you and your teammates for easy collaboration. For more information, see [Bookmarks](hunting#bookmarks-to-keep-track-of-data).

This article explains how to create, view, and manage hunting bookmarks in Microsoft Sentinel and how to use them during investigations.

Note

**Microsoft Sentinel hunting bookmarks**: You can only create bookmarks in the Azure portal, under **Microsoft Sentinel** &gt; **Threat management** &gt; **Hunting**. In the Microsoft Defender portal, you can view bookmarks that were already created, but you can't add new ones.

**Advanced hunting bookmarks**: Bookmarks aren't available in Advanced hunting, which provides a unified query experience across Microsoft Defender and Microsoft Sentinel data. However, bookmarks are still available in **Microsoft Sentinel** &gt; **Threat management** &gt; **Hunting**, which provides the Microsoft Sentinel-specific hunting experience. You can also use alternatives such as incident tags, saved queries, or custom hunting tables to preserve and track investigation context.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Add a bookmark (Azure portal only)

Create a bookmark to preserve the queries, results, your observations, and findings.

1. Under **Threat management**, select **Hunting**.
2. From the **Queries** tab, select one or more of the hunting queries.
3. From the top command bar, select **Run selected queries**.
4. Select **View query results**. For example:

    ![Screenshot of viewing query results from Microsoft Sentinel hunting.](media/bookmarks/new-processes-observed-example.png)

    Selecting **View query results** opens the query results in the **Logs** pane.
5. From the log query results list, use the checkboxes to select one or more rows that contain the information you find interesting.
6. In Azure portal, select **Add bookmark**:

    [![Screenshot of adding hunting bookmark to query.](media/bookmarks/add-hunting-bookmark.png)](media/bookmarks/add-hunting-bookmark.png#lightbox)
7. On the right, in the **Add bookmark** pane, optionally, update the bookmark name, add tags, and notes to help you identify what was interesting about the item.
8. You can optionally map bookmarks to MITRE ATT&CK techniques or sub-techniques. MITRE ATT&CK mappings are inherited from mapped values in hunting queries, but you can also create them manually. Select the MITRE ATT&CK tactic associated with the desired technique from the drop-down menu in the **Tactics & Techniques** section of the **Add bookmark** pane. The menu expands to show all the MITRE ATT&CK techniques, and you can select multiple techniques and sub-techniques in this menu.

    ![Screenshot of how to map Mitre Attack tactics and techniques to bookmarks.](media/bookmarks/mitre-attack-mapping.png)
9. Now an expanded set of entities can be extracted from bookmarked query results for further investigation. In the **Entity mapping** section, use the drop-downs to select [entity types and identifiers](entities-reference). Then map the column in the query results containing the corresponding identifier. For example:

    ![Screenshot to map entity types for hunting bookmarks.](media/bookmarks/map-entity-types-bookmark.png)

    To view the bookmark in the investigation graph, you must map at least one entity. Entity mappings to account, host, IP, and URL entity types you created are supported, preserving backwards compatibility.
10. Select **Create** to commit your changes and add the bookmark. All bookmarked data is shared with other analysts, and is a first step toward a collaborative investigation experience.

The log query results support bookmarks whenever the **Logs** pane is opened from Microsoft Sentinel. For example, if you select **General** &gt; **Logs** from the navigation bar, select event links in the investigations graph, or select an alert ID from the full details of an incident. You can't create bookmarks when the **Logs** pane is opened from another location, such as directly from Azure Monitor.

## View and update bookmarks

Find and update a bookmark from the **Bookmarks** tab.

1. For Microsoft Sentinel in the [Azure portal](https://portal.azure.com), under **Threat management** select **Hunting**. For Microsoft Sentinel in the [Defender portal](https://security.microsoft.com/), select **Microsoft Sentinel** &gt; **Threat management** &gt; **Hunting**.
2. Select the **Bookmarks** tab to view the list of bookmarks.
3. Search or filter to find a specific bookmark or bookmarks.
4. Select individual bookmarks to view the bookmark details in the right-hand pane.
5. Make your changes as needed. Your changes are automatically saved.

Note

You can only view up to 1,000 bookmarks in the **Bookmarks** tab. You can view the rest of your bookmarked data in your logs. View bookmarked data in logs

## Exploring bookmarks in the investigation graph

Visualize your bookmarked data by launching the investigation experience in which you can view, investigate, and visually communicate your findings by using an interactive entity-graph diagram and timeline.

Important

Each bookmark you want to investigate must have at least one mapped entity. If a bookmark doesn't have a mapped entity, update the bookmark to add one before you begin.

1. From the **Bookmarks** tab, select the bookmark or bookmarks you want to investigate.
2. Select **Investigate** to view the bookmark in the investigation graph.

For instructions to use the investigation graph, see [Use the investigation graph to deep dive](investigate-cases#use-the-investigation-graph-to-deep-dive).

## Add bookmarks to a new or existing incident (Azure portal only)

Add bookmarks to an incident from the bookmarks tab on the **Hunting** page.

1. From the **Bookmarks** tab, select the bookmark or bookmarks you want to add to an incident.
2. Select **Incident actions** from the command bar:

    ![Screenshot of adding bookmarks to incident.](media/bookmarks/incident-actions.png)
3. Select either **Create new incident** or **Add to existing incident**, as appropriate. Then:

    - For a new incident: Optionally update the details for the incident, and then select **Create**.
    - For adding a bookmark to an existing incident: Select one incident, and then select **Add**.
4. To view the bookmark within the incident:

    1. Go to **Microsoft Sentinel** &gt; **Threat management** &gt; **Incidents**.
    2. Select the incident with your bookmark and **View full details**.
    3. On the incident page, in the left pane, select the **Bookmarks**.

## View bookmarked data in logs

View bookmarked queries, results, or their history.

1. From the **Hunting** &gt; **Bookmarks** tab, select the bookmark.
2. From the details pane, select the following links:

    - **View source query** to view the source query in the **Logs** pane.
    - **View bookmark logs** to see all bookmark metadata, which includes who made the update, the updated values, and the time the update occurred.
3. From the command bar on the **Hunting** &gt; **Bookmarks** tab, select **Bookmark Logs** to view the raw bookmark data for all bookmarks.

    ![Screenshot of bookmark logs command.](media/bookmarks/bookmark-logs.png)

The **Bookmark Logs** view shows all your bookmarks with associated metadata. You can use [Kusto Query Language (KQL)](/en-us/kusto/query/kql-quick-reference?view=microsoft-sentinel&amp;preserve-view=true) queries to filter down to the latest version of the specific bookmark you're looking for.

There can be a significant delay (measured in minutes) between the time you create a bookmark and when it's displayed in the **Bookmarks** tab.

## Delete a bookmark

Deleting the bookmark removes the bookmark from the list in the **Bookmarks** tab. The **HuntingBookmark** table for your Log Analytics workspace continues to contain previous bookmark entries, but the latest entry changes the **SoftDelete** value to **true**, which marks the bookmark as deleted so you can filter out old bookmarks. Deleting a bookmark doesn't remove any entities from the investigation experience that are associated with other bookmarks or alerts.

To delete a bookmark, complete the following steps.

1. From the **Hunting** &gt; **Bookmarks** tab, select the bookmark or bookmarks you want to delete.
2. Right-click, and select the option to delete the bookmarks selected.