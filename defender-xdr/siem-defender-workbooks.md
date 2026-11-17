---
layout: Conceptual
title: Update workbooks to use Advanced Hunting data - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/siem-defender-workbooks
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to update workbooks to query Microsoft Defender XDR data directly by using Advanced Hunting.
author: mberdugo
ms.author: monaberdugo
ms.service: microsoft-sentinel
ms.topic: how-to
ms.date: 2026-09-08T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1030
locale: en-us
document_id: a2fbabf2-da1c-78e4-6126-b51afa4ed232
document_version_independent_id: a2fbabf2-da1c-78e4-6126-b51afa4ed232
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/siem-defender-workbooks.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: siem-defender-workbooks
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/siem-defender-workbooks.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 62774c8e-09e9-be22-b031-fd92b5439832
---

# Update workbooks to use Advanced Hunting data - Microsoft Defender XDR | Microsoft Learn

Workbooks can query Microsoft Defender XDR data directly by using Advanced Hunting, without requiring the same data to be ingested into a workspace.

You can update existing workbooks to use Advanced Hunting data or create new workbooks that query Microsoft Defender XDR data directly.

## Prerequisites

Before you begin, make sure you have:

- Your tenant is [eligible for ISOC](isoc-overview).
- To create and edit workbooks, either the **Workbooks** Unified RBAC permission with **Manage** access or the **Security Administrator** role.
- Access to the scopes and workloads used by the workbook queries.

Workbook permissions don't grant access to the underlying data. Data access and scoping are enforced when the query runs.

For example, a user can open a workbook that contains Defender for Endpoint data, but the workbook tile returns an error if the user doesn't have access to that data.

For more information, see [Update permissions and roles with Unified RBAC](/en-us/azure/sentinel/transition-unified-rbac).

## Create a workbook using Advanced Hunting data

The **Workbooks** page includes example workbooks that use Microsoft Defender XDR data.

To create your own workbook:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
2. Go to **Workbooks**.
3. Select **+ Add workbook**.
4. Select **Edit**.
5. In the query section, select **Advanced Hunting** as the data source.
6. Add or update the query for the workbook tile.
7. Save the workbook.

## Update an existing workbook

When you stop ingesting a supported Microsoft Defender XDR table into a workspace, update any workbooks that query that table.

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
2. Go to **Workbooks** and open the workbook you want to update.
3. Select **Edit**.
4. Change the query data source to **Advanced Hunting**.
5. Review the query and confirm that the table names are available in Advanced Hunting. Most table names remain the same.
6. Update any table or column references that differ in the Advanced Hunting schema.
7. Validate the workbook tiles, filters, and parameters.

For information about schema and data-type differences, see [Update Microsoft Sentinel content to use Advanced Hunting tables](/en-us/azure/sentinel/transition-advanced-hunting-tables).

## Work with workbooks across workspaces

When one or more workspaces are connected, the **Workbooks** page includes a **Workspace** column that shows where each workbook is saved.

- A workspace name indicates that the workbook is saved to that workspace.
- **None** indicates that the workbook is saved at the tenant level.

You can filter the workbook list by workspace directly from the **Workbooks** page.

When you save a workbook, choose whether to save it to a specific workspace or at the tenant level.