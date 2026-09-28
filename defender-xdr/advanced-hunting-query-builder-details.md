---
layout: Conceptual
title: Supported data types and filters in guided mode for hunting in Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-query-builder-details
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Refine your query by using the different guided mode capabilities in advanced hunting in Microsoft Defender XDR.
ms.service: defender-xdr
ms.subservice: adv-hunting
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- m365initiative-m365-defender
- tier2
ms.custom:
- msecd-doc-authoring-1014
- cx-ti
- cx-ah
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: fb65fa86-42e3-a2d5-6951-450fe8915fb2
document_version_independent_id: fb65fa86-42e3-a2d5-6951-450fe8915fb2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-query-builder-details.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-query-builder-details
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-query-builder-details.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: 3b6a888a-301b-e7e6-a4da-d8e8d5176d71
---

# Supported data types and filters in guided mode for hunting in Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn

Important

Some information relates to prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

This article explains how to refine your advanced hunting queries in guided mode in Microsoft Defender XDR. Learn how to use supported data types, subgroups, smart auto-complete, event type filters, sample sizes, and how to switch from guided mode to advanced (KQL) mode.

## Use different data types

Advanced hunting in guided mode supports several data types that you can use to fine-tune your query.

- Numbers![Screenshot of the query builder with a numeric field added as a condition](media/advanced-hunting-query-builder-details/21-numbers.png)
- Strings![Screenshot of the query builder with a string field configured as a condition](media/advanced-hunting-query-builder-details/21-string.png)

    In the free text box, type the value and press **Enter** to add it. Note that the delimiter between values is **Enter**.

    ![Screenshot of the query builder showing multiple string values entered as filter conditions](media/advanced-hunting-query-builder-details/23-string2.png)
- Boolean![Screenshot of the query builder with a Boolean field used as a condition](media/advanced-hunting-query-builder-details/24-boolean.png)
- Datetime![Screenshot of the query builder with a datetime field configured as a condition](media/advanced-hunting-query-builder-details/25-datetime.png)
- Closed list - You don't need to remember the exact value you're looking for. You can easily choose from a suggested closed list that supports multi-selection.![Screenshot of the query builder with a predefined list of values available for multi-selection as a condition](media/advanced-hunting-query-builder-details/26-closed.png)

## Use subgroups

You can create groups of conditions by clicking **Add subgroup**:

![Screenshot highlighting Add subgroup button](media/advanced-hunting-query-builder-details/27-subgroup1.png)

![Screenshot showing use of subgroups in query builder conditions](media/advanced-hunting-query-builder-details/28-subgroup2.png)

## Use smart auto-complete for search

Smart auto-complete for searching devices and user accounts is supported. You don't need to remember the device ID, full device name, or user account name. You can start typing the first few characters of the device or user you're looking for and a suggested list appears from which you can choose what you need:

![Screenshot showing smart auto-complete support](media/advanced-hunting-query-builder-details/29-smart-auto.png)

## Use `EventType`

You can even look for specific event types like all failed logons, file modification events, or successful network connections by using the **EventType** filter in any section where the **EventType** filter is available.

For instance, if you want to add a condition that looks for registry value deletions, you can go to the **Registry Events** section and select **EventType**.

![Screenshot of the Registry Events EventType list showing available registry event values](media/advanced-hunting-query-builder-details/30-eventtype1.png)

Selecting EventType under Registry Events allows you to choose from different registry events, including the one you're hunting for, **RegistryValueDeleted**.

![Screenshot of the Registry Events filter with EventType set to RegistryValueDeleted](media/advanced-hunting-query-builder-details/31-eventtype2.png)

Note

`EventType` is the equivalent of `ActionType` in the data schema, which users of advanced mode might be more familiar with.

## Test your query with a smaller sample size

If you're still working on your query and would like to see its performance and some sample results quickly, adjust the number of records to return by picking a smaller set through the **Sample size** dropdown menu.

![Screenshot of the Sample size dropdown used to limit returned records while testing a query](media/advanced-hunting-query-builder-details/32-sample-size.png)

The sample size is set to 10,000 results by default, which is the maximum number of records that can be returned in hunting. However, we highly recommend lowering the sample size to 10 or 100 to quickly test your query, as doing so consumes less resources while you're still working on improving the query.

Then, once you finalize your query and are ready to use it to get all the relevant results for your hunting activity, make sure that the sample size is set to 10k, the maximum.

## Switch to advanced mode after building a query

You can click on **Edit in KQL** to view the KQL query generated by your selected conditions. Editing in KQL opens a new tab in advanced mode, with the corresponding KQL query:

![Screenshot of guided mode showing the Edit in KQL control used to open the generated query in advanced mode](media/advanced-hunting-query-builder-details/33-edit-kql.png)

![Screenshot of the generated KQL query in advanced mode for a guided query searching file name and SHA256 across all relevant tables](media/advanced-hunting-query-builder-details/33-edit-kql-2.png)

In the file-name and SHA256 query example shown in the previous screenshot, the selected view is All, so the KQL query searches all tables that have file properties of name and SHA256, and in all the relevant columns covering these properties.

If you change the view to **Emails & collaboration**, the KQL query generated for the file-name and SHA256 example is narrowed down to:

![Screenshot of the generated KQL query in advanced mode narrowed to Emails &amp; collaboration tables for the file-name and SHA256 example](media/advanced-hunting-query-builder-details/34-edit-kql-3.png)