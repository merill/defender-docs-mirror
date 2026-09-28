---
layout: Conceptual
title: Use Microsoft Sentinel situational awareness workbooks in multitenant management - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/mto-workbooks
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Access and use the out-of-the-box Situational Awareness workbook across multiple tenants in the Microsoft Defender portal. Monitor tenant health, trends, and metrics from a single multitenant view.
ms.service: defender-xdr
author: mberdugo
ms.author: monaberdugo
ms.reviewer: tbeerthuis
ms.collection:
- m365-security
- highpri
- tier1
- usx-security
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: fbda474c-9f81-92e8-90e4-560ef38cb189
document_version_independent_id: fbda474c-9f81-92e8-90e4-560ef38cb189
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/mto-workbooks.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mto-workbooks
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/mto-workbooks.md
platformId: b4adb025-8f12-c723-8279-fc73b765914d
---

# Use Microsoft Sentinel situational awareness workbooks in multitenant management - Microsoft Defender XDR | Microsoft Learn

Microsoft Sentinel lets you manage and view workbooks across multiple tenants from one page. You can use the built-in Situational Awareness workbook to track tenant health, trends, and key metrics. This article shows how to access and use workbooks in multitenant management. Before you begin, make sure you meet the prerequisites for using workbooks in multitenant management.

## Prerequisites

Before using Workbooks in multitenant management, ensure you have the following prerequisites:

- Access to Microsoft Sentinel on the Defender portal. ​
- Access to more than one tenant using B2B/GDAP.
- For the workbook aggregated view, at least one workbook must be available on one or more target tenants.
- For the Situational Awareness workbook, your home tenant (primary workspace) must have threat intelligence data. ​

## Access a workbook​

Follow these steps to open the Workbooks page in the multitenant portal.

1. In the left-hand navigation pane, select **Microsoft Sentinel** &gt; **Workbooks**. This page shows a combined list of all workbooks across your tenants.

    ![Screenshot of Workbooks homepage.](media/mto-workbooks/access-workbook.png)
2. Use the search bar to find specific workbooks. Filter or browse through multiple pages of workbooks as needed.
3. Select the desired workbook from the list.
4. Select **View saved workbook** to open it in the Defender portal for the corresponding tenant.

    ![Screenshot of View saved workbook option.](media/mto-workbooks/view-workbook.png)

## Open the situational awareness workbook

The Situational Awareness workbook shows health status, trends, and metrics across your tenants. It supports multiple tenants, so you can pick which ones to include.

1. In the multitenant management portal, select the button on the Situational Awareness card.

    ![Screenshot of Situational Awareness button.](media/mto-workbooks/situational-awareness-card.png)
2. Use the tenant selector in the top-right corner to pick which tenants to include. To pick specific workspaces, select **Edit selection**. Make sure your home tenant is in scope and has threat intelligence data. Then select **Apply**.

    ![Screenshot of tenant selector.](media/mto-workbooks/tenant-scope.png)

## Explore the situational awareness workbook

Use the following workbook features to analyze data across tenants:

- Use the global filters at the top of the workbook to refine the data displayed. ​
- Navigate through the subtabs to explore different categories of insights (for example, health status or threat insights).
- Review the charts and metrics provided to monitor trends and identify areas for investigation. ​

## Workbook limitations in multitenant management

Note the following limits for Workbooks in multitenant management:

- The Situational Awareness workbook only uses threat data from the home tenant. You can't change this setting.
- You can't edit or create workbooks from the Workbooks page. ​
- Workbook templates don't appear in the combined view.