---
layout: Conceptual
title: Update workbooks to use Advanced Hunting data - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/update-workbooks-advanced-hunting-data
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
description: Learn how to update workbooks to query Microsoft Defender XDR data directly by using Advanced Hunting.
author: mberdugo
ms.author: monaberdugo
ms.topic: how-to
ms.date: 2026-09-08T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1032
locale: en-us
document_id: 5d9ee20c-ec3b-2aa4-b408-02371851ce0b
document_version_independent_id: f61b7f62-54c7-1fe9-1c72-5a5646a5de1f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/update-workbooks-advanced-hunting-data.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/update-workbooks-advanced-hunting-data
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/update-workbooks-advanced-hunting-data.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
platformId: 25ad1d4c-6d47-7a92-9915-b852bb1351c1
---

# Update workbooks to use Advanced Hunting data - Microsoft Defender XDR | Microsoft Learn

Workbooks can query Microsoft Defender XDR data directly by using Advanced Hunting, without requiring the same data to be ingested into a workspace.

You can update existing workbooks to use Advanced Hunting data or create new workbooks that query Microsoft Defender XDR data directly.

## Prerequisites

Before you begin, make sure you have:

- Your tenant is [eligible for ISOC](/en-us/defender-xdr/isoc-overview).
- To create and edit workbooks, either the **Workbooks** Unified RBAC permission with **Manage** access or the **Security Administrator** role.
- Access to the scopes and workloads used by the workbook queries.

Workbook permissions don't grant access to the underlying data. Data access and scoping are enforced when the query runs.

For example, a user can open a workbook that contains Defender for Endpoint data, but the workbook tile returns an error if the user doesn't have access to that data.

For more information, see [Update permissions and roles with Unified RBAC](transition-unified-rbac).

## Create a workbook using Advanced Hunting data

The **Workbooks** page includes example workbooks that use Microsoft Defender XDR data.

To create your own workbook:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
2. Select **Dashboards & reports** &gt; **Workbooks**.
3. Select **+ Add workbook**.
4. Select **Edit**.
5. In the query section, select **Advanced Hunting** as the data source.
6. Add or update the query for the workbook tile.
7. Save the workbook.

## Update an existing workbook

When you stop ingesting a supported Microsoft Defender XDR table into a workspace, update any workbooks that query that table.

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
2. Select **Dashboards & reports** &gt; **Workbooks** and open the workbook you want to update.
3. Select **Edit**.
4. Change the query data source to **Advanced Hunting**.
5. Review the query and confirm that the table names are available in Advanced Hunting. Most table names remain the same.
6. Update any table or column references that differ in the Advanced Hunting schema.
7. Validate the workbook tiles, filters, and parameters.

For information about schema and data-type differences, see [Update Microsoft Sentinel content to use Advanced Hunting tables](transition-advanced-hunting-tables).

## Work with workbooks across workspaces

When one or more workspaces are connected, the **Workbooks** page includes a **Workspace** column that shows where each workbook is saved.

- A workspace name indicates that the workbook is saved to that workspace.
- **None** indicates that the workbook is saved at the tenant level.

You can filter the workbook list by workspace directly from the **Workbooks** page.

When you save a workbook, choose whether to save it to a specific workspace or at the tenant level.