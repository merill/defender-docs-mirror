---
layout: Conceptual
title: Conduct End-to-end Threat Hunting with Hunts - Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/hunts
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
description: Learn how to use hunts for conducting end-to-end proactive threat hunting. Seek out undetected threats based on hypothesis or start broadly and refine your searches with this hunting experience.
ms.author: monaberdugo
author: mberdugo
ms.reviewer: efratka
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: usx-security
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 362b66d3-a3b7-6c68-f7ae-6343240dde17
document_version_independent_id: 96aae90c-5e4a-5f6e-7315-eeb7d5e7b908
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/hunts.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/hunts
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/hunts.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 82242e42-3d6a-b8d1-ed55-42a640d278dd
---

# Conduct End-to-end Threat Hunting with Hunts - Microsoft Sentinel | Microsoft Learn

Proactive threat hunting is a process where security analysts seek out undetected threats and malicious behaviors. By creating a hypothesis, searching through data, and validating that hypothesis, they determine what to act on. Actions can include creating new detections, new threat intelligence, or spinning up a new incident.

Use the end to end hunting experience within Microsoft Sentinel to:

- Proactively hunt based on specific MITRE techniques, potentially malicious activity, recent threats, or your own custom hypothesis.
- Use security-researcher-generated hunting queries or custom hunting queries to investigate malicious behavior.
- Conduct your hunts using multiple persisted-query tabs that enable you to keep context over time.
- Collect evidence, investigate UEBA sources, and annotate your findings using hunt specific bookmarks.
- Collaborate and document your findings with comments.
- Act on results by creating new analytic rules, new incidents, new threat indicators, and running playbooks.
- Keep track of your new, active, and closed hunts in one place.
- View metrics based on validated hypotheses and tangible results.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Prerequisites

In order to use the hunts feature, you either need to be assigned a built-in Microsoft Sentinel role, or a custom Azure RBAC role. Here are your options:

- Assign the built-in [Microsoft Sentinel Contributor role assignment](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-contributor). To learn more about roles in Microsoft Sentinel, see [Roles and permissions in Microsoft Sentinel](roles).
- Assign a custom Azure RBAC role with the appropriate permissions under [*Microsoft.SecurityInsights/hunts*](/en-us/azure/role-based-access-control/resource-provider-operations#microsoftsecurityinsights).

For more information, see [Roles and permissions in the Microsoft Sentinel platform](roles).

## Define your hypothesis

Defining a hypothesis is an open ended, flexible process and can include any idea you want to validate. Common hypotheses include:

- Suspicious behavior - Investigate potentially malicious activity that's visible in your environment to determine if an attack is occurring.
- New threat campaign - Look for types of malicious activity based on newly discovered threat actors, techniques, or vulnerabilities. This might be something you heard about in a security news article.
- Detection gaps - Increase your detection coverage using the MITRE ATT&CK map to identify gaps.

Microsoft Sentinel gives you flexibility as you zero in on the right set of hunting queries to investigate your hypothesis. When you create a hunt, initiate it with preselected hunting queries or add queries as you progress. Here are recommendations for preselected queries based on these common hypotheses: suspicious behavior, new threat campaigns, and detection gaps.

### Hypothesis - Suspicious behavior

1. For Microsoft Sentinel in the [Azure portal](https://portal.azure.com), under **Threat management**, select **Hunting**. For Microsoft Sentinel in the [Defender portal](https://security.microsoft.com/), select **Microsoft Sentinel** &gt; **Threat management** &gt; **Hunting**.
2. Select the **Queries** tab. To identify potentially malicious behaviors, run all the queries.
3. Select **Run All queries** &gt; wait for the queries to execute. Running all queries might take a while.
4. Select **Add filter** &gt; **Results** &gt; unselect the checkboxes "!", "N/A", "-", and "0" values &gt; **Apply**![Screenshot shows the filter described in step 3.](media/hunts/all-queries-with-results.png)
5. Sort the filtered query results by the **Results Delta** column to see what changed most recently. The filtered query results provide initial guidance on the hunt.

### Hypothesis - New threat campaign

The content hub offers threat campaign and domain-based solutions to hunt for specific attacks. In the following steps, you install a threat campaign or domain-based solution.

1. Go to the **Content Hub**.
2. Install a threat campaign or domain-based solution like the **Log4J Vulnerability Detection** or **Apache Tomcat**.

    [![Screenshot shows the content hub in grid view with the Log4J and Apache solutions selected.](media/hunts/content-hub-solutions.png)](media/hunts/content-hub-solutions.png#lightbox)
3. After your selected solution is installed, in Microsoft Sentinel, go to **Hunting**.
4. Select the **Queries** tab.
5. Search by solution name, or filtering by **Source Name** of the solution.
6. Select the query and **Run query**.

### Hypothesis - Detection gaps

The MITRE ATT&CK map helps you identify specific gaps in your detection coverage. Use predefined hunting queries for specific MITRE ATT&CK techniques as a starting point to develop new detection logic.

1. Navigate to the **MITRE ATT&CK (Preview)** page.
2. Unselect items in the Active drop-down menu.
3. Select **Hunting queries** in the **Simulated** filter to see which techniques have hunting queries associated with them.

    [![Screenshot shows the MITRE ATT&amp;CK page with the option for simulated Hunting queries selected.](media/hunts/mitre-hunting-queries.png)](media/hunts/mitre-hunting-queries.png#lightbox)
4. Select the card with your desired technique.
5. Select the **View** link next to **Hunting queries** at the bottom of the details pane. The **View** link opens a filtered view of the **Queries** tab on the **Hunting** page for the selected technique.

    ![Screenshot shows the MITRE ATT&amp;CK card view with the Hunting queries view link.](media/hunts/mitre-card-view.png)
6. Select all the queries for that technique.

## Create a Hunt

There are two primary ways to create a hunt.

1. If you started with a hypothesis where you selected queries, select the **Hunt actions** drop down menu &gt; **Create new hunt**. All the queries you selected are cloned for this new hunt.

    ![Screenshot shows queries selected and the create new hunt menu option selected.](media/hunts/create-new-hunt.png)
2. If you haven't decided on queries yet, select the **Hunts (Preview)** tab &gt; **New Hunt** to create a blank hunt.

    ![Screenshot shows the menu to create a blank hunt with no preselected queries.](media/hunts/create-blank-hunt.png)
3. Fill out the hunt name and optional fields. The description is a good place to verbalize your hypothesis. The **Hypothesis** pull down menu is where you set the status of your working hypothesis.
4. Select **Create** to get started.

    ![Screenshot shows the hunt creation page with Hunt name, description, owner, status, and hypothesis state.](media/hunts/create-hunt-description.png)

## View hunt details

After you create a hunt, open its details page to review queries, bookmarks, and entities.

1. Select the **Hunts (Preview)** tab to view your new hunt.
2. Select the hunt link by name to view the details and take actions.

    [![Screenshot showing new hunt in Hunting tab.](media/hunts/view-hunt.png)](media/hunts/view-hunt.png#lightbox)
3. View the details pane with the **Hunt name**, **Description**, **Content**, **Last update time**, and **Creation time**.
4. Note the tabs for **Queries**, **Bookmarks**, and **Entities**.

    [![Screenshot showing the hunt details.](media/hunts/view-hunt-details.png)](media/hunts/view-hunt-details.png#lightbox)

### Queries tab

The **Queries** tab contains hunting queries specific to this hunt. These queries are clones of the originals, independent from all others in the workspace. Update or delete them without impacting your overall set of hunting queries or queries in other hunts.

#### Add a query to the hunt

To add existing hunting queries to the current hunt, complete the following steps.

1. Select **Query Actions** &gt; **add queries to hunt**
2. Select the queries you want to add. [![Screenshot shows query actions menu in the queries tab page.](media/hunts/add-queries-to-hunt.png)](media/hunts/add-queries-to-hunt.png#lightbox)

#### Run queries

Run the queries in your hunt to generate and review current results.

1. Select ![](media/hunts/run.png)**Run all queries** or choose specific queries and select ![](media/hunts/run.png)**Run selected queries**.
2. Select ![](media/hunts/cancel.png)**Cancel** to cancel query execution at any time.

#### Manage queries

You can manage individual hunt queries from the context menu in the **Queries** tab.

1. Right-click a query and select one of the following from the context menu:

    - **Run**
    - **Edit**
    - **Clone**
    - **Delete**
    - **Create analytics rule**

    ![Screenshot shows right-click context menu options in the Queries tab of a hunt.](media/hunts/queries-tab.png)

    The context-menu options behave just like the options in the existing queries table on the **Hunting** page, except the actions only apply within this hunt. When you choose to create an analytics rule, the name, description, and KQL query is prepopulated in the new rule creation. A link is created to view the new analytics rule found under **Related analytics rules**.

    ![Screenshot showing hunt details with related analytics rule.](media/hunts/analytics-rule-from-query-tab.png)

#### View results

The **View results** feature allows you to see hunting query results in the Log Analytics search experience. From here, analyze your results, refine your queries, and add a bookmark to record information and further investigate individual row results.

1. Select the **View results** button.
2. If you pivot to another part of the Microsoft Sentinel portal, then browse back to the LA log search experience from the hunt page, all your LA query tabs remain.
3. These LA query tabs are lost if you close the browser tab. If you want to persist the queries long term, you need to save the query, create a new hunting query, or add a comment for later use within the hunt.

## Add a bookmark

When you find interesting results or important rows of data, add those results to the hunt by creating a bookmark. For more information, see [Use hunting bookmarks for data investigations](bookmarks).

1. Select the desired row or rows.
2. Above the results table, select **Add bookmark**. [![Screenshot showing add bookmark pane with optional fields filled in.](media/hunts/add-bookmark.png)](media/hunts/add-bookmark.png#lightbox)
3. Name the bookmark.
4. Set the event time column.
5. Map entity identifiers.
6. Set MITRE tactics and techniques.
7. Add tags, and add notes.

    The bookmarks preserve the specific row results, KQL query, and time range that generated the result.
8. Select **Create** to add the bookmark to the hunt.

## View bookmarks

Use the **Bookmarks** tab to review saved findings and take follow-up actions.

1. Navigate to the hunt's bookmark tab to view your bookmarks.

    [![Screenshot showing a bookmark with all its details and the hunts action menu open.](media/hunts/view-bookmark.png)](media/hunts/view-bookmark.png#lightbox)
2. Select a desired bookmark and perform the following actions:

    - Select entity links to view the corresponding UEBA entity page.
    - View raw results, tags, and notes.
    - Select **View source query** to see the source query in Log Analytics.
    - Select **View bookmark logs** to see the bookmark contents in the Log Analytics hunting bookmark table.
    - Select **Investigate** button to view the bookmark and related entities in the investigation graph.
    - Select the **Edit** button to update the tags, MITRE tactics and techniques, and notes.

## Interact with entities

Use the **Entities** tab to investigate the entities collected from bookmarks in the hunt.

1. Navigate to your hunt's **Entities** tab to view, search, and filter the entities contained in your hunt. This list is generated from the list of entities in the bookmarks. The Entities tab automatically resolves duplicated entries.
2. Select entity names to visit the corresponding User and Entity Behavior Analytics (UEBA) entity page.
3. Right-click on the entity to take actions appropriate to the entity types, such as adding an IP address to Threat Intelligence (TI) or running an entity type specific playbook.

    ![Screenshot showing context menu for entities.](media/hunts/entities-add-ti.png)

## Add comments

Comments are an excellent place to collaborate with colleagues, preserve notes, and document findings.

1. Select ![](media/hunts/comments-icon.png)
2. Type and format your comment in the edit box.
3. Add a query result as a link for collaborators to quickly understand the context.
4. Select the **Comment** button to apply your comments.

    ![Screenshot showing comment edit box with LA query as a link.](media/hunts/add-comment.png)

## Create incidents

There are two choices for incident creation while hunting.

### Option 1: Use bookmarks

1. Select a bookmark or bookmarks.
2. Select the Incident actions button.
3. Select Create new incident or Add to existing incident

    ![Screenshot showing incident actions menu from the bookmarks window.](media/hunts/create-incident.png)

    - For **Create new incident**, follow the guided steps. The bookmarks tab is prepopulated with your selected bookmarks.
    - For **Add to existing incident**, select the incident and select the **Accept** button.

### Option 2: Use the hunts Actions

1. Select the hunts **Actions** menu &gt; **Create incident**, and follow the guided steps.

    ![Screenshot showing hunts actions menu from the bookmarks window.](media/hunts/create-incident-actions-menu.png)
2. During the **Add bookmarks** step, use the **Add bookmark** action to choose bookmarks from the hunt to add to the incident. You're limited to bookmarks that aren't assigned to an incident.
3. After the incident is created, it will be linked under the **Related incidents** list for that hunt.

## Update status

As your investigation progresses, update the hypothesis and hunt statuses to reflect the current state.

1. When you captured enough evidence to validate or invalidate your hypothesis, update your hypothesis state.

    ![Screenshot shows hypothesis state menu selection.](media/hunts/set-hypothesis.png)
2. When all the actions associated with the hunt are complete, such as creating analytics rules, incidents, or adding indicators of compromise (IOCs) to TI, close out the hunt.

    ![Screenshot shows Hunt state menu selection.](media/hunts/set-status.png)

The hypothesis state and hunt status are visible on the main Hunting page and contribute to the hunting metrics shown in the **Hunts** tab.

## Track metrics

Use the metrics bar at the top of the **Hunts** tab to track tangible results from hunting activity. Metrics show the number of validated hypotheses, new incidents created, and new analytic rules created. Use the hunting metrics to set goals or celebrate milestones of your hunting program.

![Screenshot shows hunting metrics.](media/hunts/track-metrics.png)