---
layout: Conceptual
title: Optimize Microsoft Defender XDR data ingestion | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/transition-optimize-xdr-ingestion
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
ms.service: microsoft-defender
ms.subservice: unified-security-operations
search.appverid: met150
description: Learn how to stop duplicate Microsoft Defender XDR data ingestion in Microsoft Sentinel after updating your security operations content to use Advanced Hunting data.
author: guywi-ms
ms.author: guywild
ms.date: 2026-11-15T00:00:00.0000000Z
ms.collection:
- M365-security-compliance
- tier1
- usx-security
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1032
locale: en-us
document_id: a19938b1-fce4-691f-4b56-8e1d6291a7c1
document_version_independent_id: cfe9a0de-6e68-12b4-627f-d5299fad4a12
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/transition-optimize-xdr-ingestion.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/transition-optimize-xdr-ingestion
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/transition-optimize-xdr-ingestion.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
platformId: 7bc486fd-750a-cfad-9da1-8f0b611373ea
---

# Optimize Microsoft Defender XDR data ingestion | Microsoft Learn

When Microsoft Defender XDR data is available directly in Advanced Hunting, you can update Microsoft Sentinel content to use the corresponding Advanced Hunting tables and then stop duplicate ingestion of that data into Microsoft Sentinel.

Update your content one table at a time. When the content for all tables is updated and validated, stop ingestion for the supported Microsoft Defender XDR tables in the workspace at the same time.

Important

You can't stop ingestion for a single table. **Configure workspace** stops ingesting data into Log Analytics for the supported Defender XDR tables in the workspace at the same time, except tables with analytics retention set to 180 days or more, which stay ingested. Don't select it until you've updated and validated all content that depends on any of these tables. Otherwise, detections, workbooks, queries, and automation can stop receiving the data they require.

## Prerequisites

Before you begin, make sure that:

- Your tenant is [eligible for ISOC](/en-us/defender-xdr/isoc-overview).
- You have an existing Microsoft Sentinel workspace that ingests Microsoft Defender XDR data that is also available through Advanced Hunting.
- You have access to the [Microsoft Defender portal](https://security.microsoft.com) and Advanced Hunting.
- You have permissions to review and update the Microsoft Sentinel and Microsoft Defender content that depends on the tables you're optimizing.
- You have identified the queries, analytics rules, workbooks, Logic App playbooks, reports, and other content that depend on each table you plan to transition.

For information about updating access when moving from workspace-based data to Microsoft Defender XDR data, see [Update permissions and roles with Unified RBAC](transition-unified-rbac).

## Prepare dependent content

Before you stop ingestion, update content that currently queries the Microsoft Sentinel table so that it can use the corresponding Advanced Hunting data.

Use the following sequence:

| Area | Action |
| --- | --- |
| Queries and other KQL content | Update queries to use the corresponding Advanced Hunting tables and schema. |
| Permissions and roles | Make sure users and automation identities have access to the required Microsoft Defender workloads. |
| Analytics rules | Recreate applicable Microsoft Sentinel analytics rules as Microsoft Defender custom detections. |
| Workbooks | Update workbook queries to use the Advanced Hunting data source. |
| Logic App playbooks | Replace Log Analytics query actions with queries to the Microsoft Graph Advanced Hunting API where applicable. |
| Ingestion | Stop ingestion for the supported Defender XDR tables only after the content for all tables is updated and validated. |

For detailed migration guidance, see:

- [Update Microsoft Sentinel content to use Advanced Hunting tables](transition-advanced-hunting-tables)
- [Update permissions and roles with Unified RBAC](transition-unified-rbac)
- [Convert Microsoft Sentinel analytics rules to custom detections](transition-custom-detections)
- [Update workbooks to use Advanced Hunting data](update-workbooks-advanced-hunting-data)
- [Update Logic App playbook automation to use Advanced Hunting](transition-logic-app-playbooks)

## Validate content before you stop ingestion

For each table, validate all dependent content before you stop ingestion.

Make sure that:

- **Detections**: Every analytics rule that queries the table has an equivalent custom detection running against Advanced Hunting data.
- **Workbooks**: Every workbook that uses the table has been updated to use the Advanced Hunting data source and renders correctly for its intended users.
- **Automation**: Every Logic App playbook that queries the table has been updated to use the Microsoft Graph Advanced Hunting API where required and has passed an end-to-end test.
- **Access**: Users, groups, and automation identities that require the data have access to the corresponding Microsoft Defender workload.
- **Queries and reports**: Queries, saved hunts, scheduled reports, and other content that previously referenced the Microsoft Sentinel table return the expected results against Advanced Hunting.
- **Deployment**: If you use CI/CD or repeatable deployment definitions, make sure they deploy the updated custom detections and Advanced Hunting-based content.

Validate dependencies before you stop ingestion. In particular, validate detections, workbooks, automation, and access for every table.

## Stop ingestion for the supported Defender XDR tables

If you use data collection rules (DCRs) on these tables, check them first. To keep a DCR working on a table, set that table's retention to 180 days or more before you select **Configure workspace**. For more information, see [Check data collection rules and transformations before you stop ingestion](transition-soc-optimization-recommendations#dcr-xdr-tables).

After you complete all **Lower Defender data costs** recommendations and validate all dependent content:

1. In the Microsoft Defender portal, go to **Setup & configuration** &gt; **Data management** &gt; **Data & connectors**.
2. Select the **Tables** tab.
3. Select **Configure workspace**.

This stops ingesting Defender XDR data into Log Analytics for the supported Defender XDR tables in the workspace. This is what lowers your costs.

## Validate after you stop ingestion

After you stop ingestion, confirm that ingestion changed as expected and that your security operations content continues to work.

Monitor the updated configuration over several detection and automation runs.

Verify that:

- Custom detections continue to return the expected results from Advanced Hunting data.
- Hunting queries and other KQL content return the expected results.
- Workbook tiles render correctly for their intended users.
- Logic App playbooks continue to trigger and complete successfully.
- Users and automation identities retain access to the required data.

If content doesn't behave as expected, review its Advanced Hunting table mapping, schema, permissions, and query configuration.

## Update content table by table

You don't need to update the content for every Microsoft Defender XDR table at the same time. For each table:

1. Identify the content that depends on the table.
2. Update the dependent content to use Advanced Hunting.
3. Validate queries, detections, workbooks, automation, and access.
4. Set the recommendation status to **Completed**.
5. Continue with the next table.

After all tables are complete, stop ingestion for the supported Defender XDR tables.