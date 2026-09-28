---
layout: Conceptual
title: Audit and retain case data in Log Analytics - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/audit-retain-case-data
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how case management activity is automatically synced to Log Analytics for auditing, retention, investigation, and reporting.
author: guywi-ms
ms.author: guywild
ms.service: defender-xdr
ms.topic: how-to
ms.date: 2026-07-05T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: dc1ff136-cd3d-a64c-cf62-1793d8489129
document_version_independent_id: dc1ff136-cd3d-a64c-cf62-1793d8489129
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/audit-retain-case-data.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: audit-retain-case-data
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/audit-retain-case-data.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: b5b89530-7b8a-0360-2d26-42f0def4e14f
---

# Audit and retain case data in Log Analytics - Microsoft Defender XDR | Microsoft Learn

Case management activity from the Microsoft Defender portal is automatically synced to the `SecurityCaseEvent` table in Log Analytics when your tenant has a connected primary Microsoft Sentinel workspace. You can use KQL to review case activity, investigate changes, create visualizations and dashboards, and retain case history beyond the default 180-day retention period in Defender.

Case audit and retention supports incident cases and all other supported case types. It syncs case activity and changes to related case items, including:

- Cases
- Case tasks
- Case comments
- Case attachments
- Case relations

Note

For attachments, only attachment metadata is exported. Attachment contents aren't exported.

Each change is recorded as an event in the `SecurityCaseEvent` table. Events can include create, update, delete, link, and unlink operations.

## Prerequisites

To access case audit and retention data, you need read access to the Log Analytics workspace to query case data.

For more information, see [Manage access to Log Analytics workspaces](/en-us/azure/azure-monitor/logs/manage-access).

## How case data is synced

Case data is automatically synced to the `SecurityCaseEvent` table in your current primary Microsoft Sentinel workspace. You don't need to enable case sync in Defender settings, and case sync can't be turned off.

If you change the primary Microsoft Sentinel workspace, case activity automatically begins flowing to the new primary workspace. The change can take up to 15 minutes to take effect.

## Query case activity

You can query case activity by using the `SecurityCaseEvent` table in Advanced hunting in the Microsoft Defender portal, Microsoft Sentinel, or Log Analytics. Use KQL to review case changes, investigate activity, create visualizations, and build dashboards.

For the full table schema, see [SecurityCaseEvent](/en-us/azure/azure-monitor/reference/tables/securitycaseevent).

If you're new to querying data in Log Analytics, see [Log Analytics tutorial](/en-us/azure/azure-monitor/logs/log-analytics-tutorial).

### Audit cases using example queries in the Azure portal

Example queries are available for case audit and retention. You can run the queries as-is, or modify them for your investigation, reporting, auditing, or dashboard needs.

Example queries include:

- Recent changes on a case
- Cases by status
- Cases with most open tasks
- Inactive cases
- Urgent open cases
- Cases with overdue tasks
- Case tasks created daily
- All case management activity by a specific user
- Cases and tasks assigned to a specific user
- Users with most open case tasks
- Full cases snapshot
- Single case snapshot
- Point-in-time single case snapshot
- Cases by SLA status

To use an example query:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Open your Microsoft Sentinel workspace.
3. Select **Logs**.
4. Select **Queries hub**.
5. Select **Add filter**.
6. Filter by **Resource type: Case Management**.

    [![Screenshot of the Queries hub filtered by Case Management resource type and Audit category.](media/audit-retain-case-data/queries-hub-case-management.png)](media/audit-retain-case-data/queries-hub-case-management.png#lightbox)
7. Hover over an example query.
8. Select **Run** to run the query as-is, or select **Load to editor** to customize the query before selecting **Run**.

    Note

    Some queries include placeholders, such as a case ID, user, or status value. To update placeholder values before running the query, select **Load to editor**.

    Tip

    To edit a query after results appear, select **User Query** to return to the query editor.

### Audit cases using example queries in the Microsoft Defender portal

The same example queries available for case audit and retention in the Azure portal are also available in Advanced hunting in the Microsoft Defender portal.

To access the example queries:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Investigation & response** &gt; **Hunting** &gt; **Advanced hunting**.
3. Select **Queries** from the dropdown.
4. Expand **Community queries** &gt; **Microsoft Sentinel**. The case management example queries are listed there.

    [![Screenshot of Advanced hunting in the Microsoft Defender portal showing case management example queries under Community queries and Microsoft Sentinel.](media/audit-retain-case-data/advanced-hunting-case-management-queries.png)](media/audit-retain-case-data/advanced-hunting-case-management-queries.png#lightbox)

## Manage retention

After case data is synced to Log Analytics, retention is controlled by the retention settings for the `SecurityCaseEvent` table and its Log Analytics workspace.

You can manage table retention directly in the Microsoft Defender portal:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Go to **Microsoft Sentinel** &gt; **Configuration** &gt; **Tables**.
3. If needed, select the Microsoft Sentinel workspace that contains the `SecurityCaseEvent` table.
4. Select the `SecurityCaseEvent` table.
5. Select **Manage table**.
6. Configure the analytics and total retention settings.
7. Review any warnings or messages about the effects of the changes.
8. Select **Save**.

The **Tables** page also provides Table insights to help you review ingestion volume, when data was last received, estimated daily ingestion costs, and unusual changes in ingestion before you modify table retention or tier settings.

For more information, see:

- [Configure table settings in Microsoft Sentinel](/en-us/azure/sentinel/manage-table-tiers-retention)
- [Manage data tiers and retention in Microsoft Sentinel](/en-us/azure/sentinel/manage-data-overview#how-data-tiers-and-retention-work)
- [Plan costs and understand pricing and billing for Microsoft Sentinel](/en-us/azure/sentinel/billing?tabs=simplified%2Ccommitment-tiers)