---
layout: Conceptual
title: Learn the advanced hunting query language in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-query-language
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Create your first threat hunting query and learn about common operators and other aspects of the advanced hunting query language
ms.service: defender-xdr
ms.subservice: adv-hunting
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- m365initiative-m365-defender
- tier1
ms.custom:
- msecd-doc-authoring-1014
- cx-ti
- cx-ah
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: effc9f1b-280e-3b4f-0247-39c2d5f46778
document_version_independent_id: effc9f1b-280e-3b4f-0247-39c2d5f46778
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-query-language.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-query-language
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-query-language.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c6f99e62-1cf6-4b71-af9b-649b05f80cce
- https://authoring-docs-microsoft.poolparty.biz/devrel/26e1a60c-4ce1-41de-b2d1-e5f3b7e68e6e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3f56b378-07a9-4fa1-afe8-9889fdc77628
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad3bd485-5ca9-4865-afde-baec02586899
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: d8f98474-9009-c350-a384-52f25fcb24fa
---

# Learn the advanced hunting query language in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn

Advanced hunting is based on the [Kusto query language](/en-us/azure/kusto/query/). You can use Kusto operators and statements to construct queries that locate information in a specialized [advanced hunting schema](advanced-hunting-schema-tables).

Watch this short video to learn some handy Kusto query language basics.

To understand Kusto query language basics in advanced hunting, run your first query.

## Try your first query

In the Microsoft Defender portal, go to **Hunting** to run your first query. Use the following example:

```kusto
// Finds PowerShell execution events that could involve a download
union DeviceProcessEvents, DeviceNetworkEvents
| where Timestamp > ago(7d)
// Pivoting on PowerShell processes
| where FileName in~ ("powershell.exe", "powershell_ise.exe")
// Suspicious commands
| where ProcessCommandLine has_any("WebClient",
 "DownloadFile",
 "DownloadData",
 "DownloadString",
"WebRequest",
"Shellcode",
"http",
"https")
| project Timestamp, DeviceName, InitiatingProcessFileName, InitiatingProcessCommandLine,
FileName, ProcessCommandLine, RemoteIP, RemoteUrl, RemotePort, RemoteIPType
| top 100 by Timestamp
```

**[Run the suspicious PowerShell download commands query in advanced hunting](https://security.microsoft.com/hunting?query=H4sIAAAAAAAEAI2TW0sCURSF93PQfxh8Moisp956yYIgQtLoMaYczJpbzkkTpN_et_dcdPQkcpjbmrXXWftyetKTQG5lKqmMpeB9IJksJJKZDOWdZ8wKeP5wvcm3OLgZbMXmXCmIxjnYIfcAVgYvRi8w3TnfsXEDGAG47pCCZXyP5ViO4KeNbt-Up-hEuJmB6lvButnY8XSL-cDl0M2I-GwxVX8Fe2H5zMzHiKjEVB0eEsnBrszfBIWuXOLrxCJ7VqEBfM3DWUYTkNKrv1p5y3X0jwetemzOQ_NSVuuXZ1c6aNTKRaN8VvWhY9n7OS-o6J5r7mYeQypdEKc1m1qfiqpjCSuspsDntt2J61bEvTlXls5AgQfFl5bHM_gr_BhO2RF1rztoBv2tWahrso_TtzkL93KGMGZVr2pe7eWR-xeZl91f_113UOsx3nDR4Y9j5R6kaCq8ajr_YWfFeedsd27L7it-Z6dAZyxsJq1d9-2ZOSzK3y2NVd8-zUPjtZaJnYsIH4Md7AmdeAcd2Cl1XoURc5PzXlfU8U9P54WcswL6t_TW9Q__qX-xygQAAA&amp;runQuery=true&amp;timeRangeId=week)**

### Describe the query and specify the tables to search

A short comment has been added to the beginning of the query to describe the query's purpose. This comment helps if you later decide to save the query and share it with others in your organization.

```kusto
// Finds PowerShell execution events that could involve a download
```

The query itself will typically start with a table name followed by several elements that start with a pipe (`|`). In this example, we start by creating a union of two tables, `DeviceProcessEvents` and `DeviceNetworkEvents`, and add piped elements as needed.

```kusto
union DeviceProcessEvents, DeviceNetworkEvents
```

### Set the time range

The first piped element is a time filter scoped to the previous seven days. Limiting the time range helps ensure that queries perform well, return manageable results, and don't time out.

```kusto
| where Timestamp > ago(7d)
```

Note

Kusto time filters are in UTC regardless of the timezone you specified in your [time zone settings](m365d-time-zone).

### Check specific processes

The time range is immediately followed by a search for process file names representing the PowerShell application.

```kusto
// Pivoting on PowerShell processes
| where FileName in~ ("powershell.exe", "powershell_ise.exe")
```

### Search for specific command strings

Afterwards, the query looks for strings in command lines that are typically used to download files using PowerShell.

```kusto
// Suspicious commands
| where ProcessCommandLine has_any("WebClient",
    "DownloadFile",
    "DownloadData",
    "DownloadString",
    "WebRequest",
    "Shellcode",
    "http",
    "https")
```

### Customize result columns and length

Now that your query clearly identifies the data you want to locate, you can define what the results look like. `project` returns specific columns, and `top` limits the number of results. These operators help ensure the results are well-formatted and reasonably large and easy to process.

```kusto
| project Timestamp, DeviceName, InitiatingProcessFileName, InitiatingProcessCommandLine,
FileName, ProcessCommandLine, RemoteIP, RemoteUrl, RemotePort, RemoteIPType
| top 100 by Timestamp
```

Select **Run query** to see the results.

Tip

You can view query results as charts and quickly adjust filters. For guidance, see [Work with query results](advanced-hunting-query-results)

## Learn common query operators

You've just run your first query and have a general idea of its components. It's time to backtrack slightly and learn some basics. The Kusto query language used by advanced hunting supports a range of operators, including the following common ones.

| Operator | Description and usage |
| --- | --- |
| `where` | Filter a table to the subset of rows that satisfy a predicate. |
| `summarize` | Produce a table that aggregates the content of the input table. |
| `join` | Merge the rows of two tables to form a new table by matching values of the specified column(s) from each table. Watch [Joining tables in KQL](https://www.youtube.com/watch?v=8qZx7Pp5XgM) to learn how. |
| `count` | Return the number of records in the input record set. |
| `top` | Return the first N records sorted by the specified columns. |
| `limit` | Return up to the specified number of rows. |
| `project` | Select the columns to include, rename or drop, and insert new computed columns. |
| `extend` | Create calculated columns and append them to the result set. |
| `makeset` | Return a dynamic (JSON) array of the set of distinct values that Expr takes in the group. |
| `find` | Find rows that match a predicate across a set of tables. |

To see a live example of these operators, run them from the **Get started** pane on the **Advanced hunting** page in the Microsoft Defender portal.

## Understand data types

Advanced hunting supports Kusto data types, including the following common types:

| Data type | Description and query implications |
| --- | --- |
| `datetime` | Data and time information typically representing event timestamps. [Supported datetime formats](/en-us/azure/data-explorer/kusto/query/scalar-data-types/datetime) |
| `string` | Character string in UTF-8 enclosed in single quotes (`'`) or double quotes (`"`). [String data type](/en-us/azure/data-explorer/kusto/query/scalar-data-types/string) |
| `bool` | This data type supports `true` or `false` states. [Supported Boolean literals and operators](/en-us/azure/data-explorer/kusto/query/scalar-data-types/bool) |
| `int` | 32-bit integer |
| `long` | 64-bit integer |

To learn more about Kusto scalar data types, see [Kusto scalar data types](/en-us/azure/data-explorer/kusto/query/scalar-data-types/).

## Get help as you write queries

Take advantage of the following functionality to write queries faster:

- **Autosuggest** - as you write queries, advanced hunting provides suggestions from IntelliSense.
- **Schema tree** - a schema representation that includes the list of tables and their columns is provided next to your working area. For more information, hover over an item. Double-click an item to insert it to the query editor.
- **[Schema reference](advanced-hunting-schema-tables#get-schema-information-in-the-security-center)** - in-portal reference with table and column descriptions as well as supported event types (`ActionType` values) and sample queries

## Work with multiple queries in the editor

You can use the query editor to experiment with multiple queries. To use multiple queries:

- Separate each query with an empty line.
- Place the cursor on any part of a query to select that query before running it. This will run only the selected query. To run another query, move the cursor accordingly and select **Run query**.

    [![An example of multiple queries execution in the **New query** page in the Microsoft Defender portal](media/advanced-hunting-query-language/multiple-queries.png)](media/advanced-hunting-query-language/multiple-queries.png#lightbox)

    For a more efficient workspace, you can also use multiple tabs in the same hunting page. Select **New query** to open a tab for your new query.

    [![Opening a new tab by selecting Create new in advanced hunting in the Microsoft Defender portal](media/advanced-hunting-query-language/multitab.png)](media/advanced-hunting-query-language/multitab.png#lightbox)

    You can then run different queries without ever opening a new browser tab.

    [![Run different queries without ever leaving the advanced hunting page in the Microsoft Defender portal](media/advanced-hunting-query-language/multitab-examples.png)](media/advanced-hunting-query-language/multitab-examples.png#lightbox)

Note

Using multiple browser tabs with advanced hunting might cause you to lose your unsaved queries. To prevent this from happening, use the tab feature within advanced hunting instead of separate browser tabs.

## Use sample queries

The **Get started** section provides a few simple queries using commonly used operators. Try running the sample queries in the **Get started** section and making small modifications to them.

[![The **Getting started** section in the **Advanced hunting** page in the Microsoft Defender portal](media/advanced-hunting-query-language/get-started-section.png)](media/advanced-hunting-query-language/get-started-section.png#lightbox)

Note

Apart from the basic query samples, you can also access [shared queries](advanced-hunting-shared-queries) for specific threat hunting scenarios. Explore the shared queries on the left side of the page or the [GitHub query repository](https://aka.ms/hunting-queries).

## Access query language documentation

For more information on Kusto query language and supported operators, see [Kusto query language documentation](/en-us/azure/kusto/query/).

Note

Some tables in this article might not be available in Microsoft Defender for Endpoint. [Turn on Microsoft Defender](m365d-enable) to hunt for threats using more data sources. You can move your advanced hunting workflows from Microsoft Defender for Endpoint to Microsoft Defender by following the steps in [Migrate advanced hunting queries from Microsoft Defender for Endpoint](advanced-hunting-migrate-from-mde).