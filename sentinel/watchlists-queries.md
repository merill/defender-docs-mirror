---
layout: Conceptual
title: Build queries or rules with watchlists - Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/watchlists-queries
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
description: Use watchlists in KQL search queries or detection rules with built-in functions for Microsoft Sentinel.
author: EdB-MSFT
ms.author: edbaynash
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: usx-security
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 583cf4bf-ba09-a0d9-46a0-5621539f9b64
document_version_independent_id: 6a79afcd-24e1-8366-92cb-01428925e285
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/watchlists-queries.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/watchlists-queries
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/watchlists-queries.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
platformId: cff98f68-fecc-5be9-bdc6-146392695c77
---

# Build queries or rules with watchlists - Microsoft Sentinel | Microsoft Learn

Correlate your watchlist data against any Microsoft Sentinel data with Kusto tabular operators such as `join` and `lookup`. When you create a watchlist, you define the *SearchKey*. The search key is the name of a column in your watchlist that you expect to use as a join with other data or as a frequent object of searches.

For optimal query performance, use **SearchKey** as the key for joins in your queries.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Build queries with watchlists

To use a watchlist in a search query, write a Kusto Query Language (KQL) query that uses the \_GetWatchlist('watchlist-name') function and uses **SearchKey** as the key for your join.

1. For Microsoft Sentinel in the [Defender portal](https://security.microsoft.com/), select **Microsoft Sentinel** &gt; **Configuration** &gt; **Watchlist**. For Microsoft Sentinel in the [Azure portal](https://portal.azure.com), under **Configuration**, select **Watchlist**.
2. Select the watchlist you want to use.
3. Select **View in Logs**.

    [![Screenshot that shows how to use watchlists in queries.](media/watchlists-queries/sentinel-watchlist-queries-list.png)](media/watchlists-queries/sentinel-watchlist-queries-list.png#lightbox)
4. Review the **Results** tab. The items in your watchlist are automatically extracted for your query.

    The example below shows the results of the extraction of the **Name** and **IP Address** fields. The **SearchKey** is shown as its own column.

    [![Screenshot that shows queries with watchlist fields.](media/watchlists-queries/sentinel-watchlist-queries-fields.png)](media/watchlists-queries/sentinel-watchlist-queries-fields.png#lightbox)

    The timestamp on your queries will be ignored in both the query UI and in scheduled alerts.
5. Write a query that uses the \_GetWatchlist('watchlist-name') function and uses **SearchKey** as the key for your join.

    For example, the following example query joins the `RemoteIPCountry` column in the `Heartbeat` table with the search key defined for the watchlist named `mywatchlist`.

    ```kusto
    Heartbeat
    | lookup kind=leftouter _GetWatchlist('mywatchlist') 
     on $left.RemoteIPCountry == $right.SearchKey
    ```

    The results of this example query appear in Log Analytics as shown in the following screenshot.

    [![Screenshot of queries against watchlist as lookup.](media/watchlists-queries/sentinel-watchlist-queries-join.png)](media/watchlists-queries/sentinel-watchlist-queries-join.png#lightbox)

## Create an analytics rule with a watchlist

The \_GetWatchlist('watchlist-name') function returns the contents of a specified watchlist so you can reference watchlist data directly in a query. To use watchlists in analytics rules, create a rule that includes this function in the rule query.

1. Under **Configuration**, select **Analytics**.
2. Select **Create** and the type of rule you want to create.
3. On the **General** tab, enter the appropriate information.
4. On the **Set rule logic** tab, under **Rule query** use the `_GetWatchlist('<watchlist>')` function in the query.

    For example, let's say you have a watchlist named `ipwatchlist` that you created from a CSV file with the following values:

    | `IPAddress,Location` |
    | --- |
    | `10.0.100.11,Home` |
    | `172.16.107.23,Work` |
    | `10.0.150.39,Home` |
    | `172.20.32.117,Work` |

    The CSV file looks something like the following image. ![Screenshot of four items in a CSV file that's used for the watchlist.](media/watchlists-queries/create-watchlist.png)

    To use the `_GetWatchlist` function for this example, your query would be `_GetWatchlist('ipwatchlist')`.

    ![Screenshot that shows the query returns the four items from the watchlist.](media/watchlists-queries/sentinel-watchlist-new-other.png)

    In this example, we only include events from IP addresses in the watchlist:

    ```kusto
    //Watchlist as a variable
    let watchlist = (_GetWatchlist('ipwatchlist') | project IPAddress);
    Heartbeat
    | where ComputerIP in (watchlist)
    ```

    The following example query uses the watchlist inline with the query and the search key defined for the watchlist.

    ```kusto
    //Watchlist inline with the query
    //Use SearchKey for the best performance
    Heartbeat
    | where ComputerIP in ( 
        (_GetWatchlist('ipwatchlist')
        | project SearchKey)
    )
    ```

    The following screenshot shows the inline `_GetWatchlist('ipwatchlist')` query used in the rule query.

    ![Screenshot that shows how to use watchlists in analytics rules.](media/watchlists-queries/sentinel-watchlist-analytics-rule.png)
5. Complete the rest of the tabs in the **Analytics rule wizard**.

Watchlists are refreshed in your workspace every 12 days, updating the `TimeGenerated` field. For information about creating custom analytics rules that use watchlists, see [Create custom analytics rules to detect threats](detect-threats-custom).

## View the list of watchlist aliases

A watchlist alias is the unique identifier used to reference a watchlist in queries and analytics rules. You might need to see a list of watchlist aliases to identify a watchlist to use in a query or analytics rule.

1. For Microsoft Sentinel in the [Azure portal](https://portal.azure.com), under **General**, select **Logs**. In the [Defender portal](https://security.microsoft.com/), select **Investigation & response** &gt; **Hunting** &gt; **Advanced hunting**.
2. On the **New Query** page, run the following query: `_GetWatchlistAlias`.
3. Review the list of aliases in the **Results** tab.

    [![Screenshot that shows a list of watchlists.](media/watchlists-queries/sentinel-watchlist-alias.png)](media/watchlists-queries/sentinel-watchlist-alias.png#lightbox)

For more information about the Kusto operators and statements used in the examples on this page, see the Kusto documentation:

- [***where*** operator](/en-us/kusto/query/where-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***project*** operator](/en-us/kusto/query/project-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***lookup*** operator](/en-us/kusto/query/lookup-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***in*** operator](/en-us/kusto/query/in-cs-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***let*** statement](/en-us/kusto/query/let-statement?view=microsoft-sentinel&amp;preserve-view=true)

For more information on KQL, see [Kusto Query Language (KQL) overview](/en-us/kusto/query/?view=microsoft-sentinel&amp;preserve-view=true).

Other resources:

- [KQL quick reference](/en-us/kusto/query/kql-quick-reference?view=microsoft-sentinel&amp;preserve-view=true)
- [Kusto Query Language learning resources](/en-us/kusto/query/kql-learning-resources?view=microsoft-sentinel&amp;preserve-view=true)