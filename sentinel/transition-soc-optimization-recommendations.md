---
layout: Conceptual
title: Review Microsoft Sentinel recommendations for ISOC (Preview) | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/transition-soc-optimization-recommendations
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
description: Review SOC optimization recommendations and use the preview migration tool to convert eligible Microsoft Sentinel analytics rules to custom detections.
author: mberdugo
ms.author: monaberdugo
ms.localizationpriority: high
ms.collection:
- m365-security
- tier1
- usx-security
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1032
ms.date: 2026-11-15T00:00:00.0000000Z
locale: en-us
document_id: f0fba616-f658-fe93-3175-418d441b449e
document_version_independent_id: 490ec67e-9ff6-e671-eb97-4a81d543d7f9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/transition-soc-optimization-recommendations.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/transition-soc-optimization-recommendations
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/transition-soc-optimization-recommendations.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: e95703b8-292f-a625-de23-6156559de8c7
---

# Review Microsoft Sentinel recommendations for ISOC (Preview) | Microsoft Learn

When you transition an existing Microsoft Sentinel deployment to Integrated Security Operations Center (ISOC), you can use supported Microsoft Defender XDR data directly in the Microsoft Defender portal instead of relying on the same data being ingested into Microsoft Sentinel.

SOC optimization recommendations help you identify Microsoft Defender XDR data to review and the Microsoft Sentinel content that might need to be updated before ingestion changes.

Use the preview migration tool in a recommendation to convert eligible analytics rules to custom detections. Validate them while the original rules remain enabled, and complete migration when you're ready.

Note

The migration tool and the migration, validation, completion, and alert compatibility behavior documented here are in **PREVIEW**. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

Important

Update and validate dependent content table by table, including queries, detections, permissions, workbooks, automation, and data collection rules (DCRs). You can't stop ingestion for a single table. After all tables are done, **Configure workspace** stops ingestion for the supported Defender XDR tables in the workspace at the same time, except tables with analytics retention set to 180 days or more, which stay ingested. If ingestion stops before content is updated, existing content can stop receiving data, which creates coverage gaps.

## Prerequisites

Before you review SOC optimization recommendations:

- Connect all Microsoft Sentinel workspaces in your deployment to the Microsoft Defender portal. For more information, see [Transition an existing Microsoft Sentinel deployment to ISOC](transition-existing-sentinel-deployment).
- Make sure you have access to SOC optimization and the permissions required to review and update the Microsoft Sentinel and Microsoft Defender content in your environment.
- Review the [ISOC eligibility and workspace requirements](/en-us/defender-xdr/isoc-overview).

Before you use the preview migration tool:

- Confirm that you can migrate analytics rules, manage custom detections, and update dependent automation. Review [Microsoft Sentinel roles and permissions](roles) and [permissions for managing custom detections](/en-us/defender-xdr/custom-detection-rules#required-permissions-for-managing-custom-detections).
- Plan how to compare alerts, entities, severity, scheduling, and downstream automation during validation.
- During preview, configure an alert tuning rule to automatically resolve alerts associated with custom detections under validation. Both the original analytics rule and the custom detection generate alerts during this stage.
- During preview, re-create applicable health monitors as custom detection rules so that you can validate them during migration.

SOC optimization recommendations can take up to 48 hours to appear after workspace onboarding or changes to table retention.

For more information about SOC optimization, see [Optimize your security operations](soc-optimization/soc-optimization-access).

## Review SOC optimization recommendations

Review SOC optimization recommendations to identify Microsoft Defender XDR tables that might be affected by changes to Microsoft Sentinel ingestion.

1. [Sign in to the Microsoft Defender portal](https://security.microsoft.com/).
2. In the left menu, select **SOC optimization**.
3. Review the **Lower Defender data costs** recommendations. Each recommendation covers one table in one workspace.
4. Note the table and the workspace for each recommendation.
5. For each table, identify all content and integrations that depend on the corresponding Microsoft Sentinel data.

The recommendation details pane and the **Update your content to use Defender data** side panel include a **Before stopping ingestion** section. It explains how data collection rules (DCRs) and user and entity behavior analytics (UEBA) are affected when you stop ingestion. For what this means and what to do, see Check data collection rules and transformations before you stop ingestion.

Don't stop ingestion until you've reviewed and validated the dependencies for all affected tables.

## Track your progress

The **SOC optimization** page shows this banner: **Lower Defender data costs: Review the SOC optimization recommendations and update your content to lower your costs.**

![Screenshot of the Lower Defender data costs banner on the SOC optimization page, with the See what you need to do button.](media/transition-soc-optimization-recommendations/soc-optimization-banner.png)

To see what to do and track your progress, select **See what you need to do** on the banner. After you start working on recommendations, the button changes to **View progress**. The **Lower Defender data costs** section header on the page has the same link. It also shows **View all** when there are more recommendations than fit in one row.

The **Update your content to use Defender data** side panel opens. The panel shows:

- **Content counts**: the number of analytics rules, workbooks, and playbooks that use the tables.
- **Lower Defender data costs recommendations**: a progress bar for **Resolved recommendations** (for example, 3/10), and the number of recommendations in each status: **Not started**, **In progress**, **Completed**, and **Dismissed**.
- **What you gain**: the value of moving your content to Defender data.
- **What to do**: the steps to follow. These match the steps in Work through Lower Defender data costs recommendations.
- **Before stopping ingestion**: how data collection rules (DCRs) and UEBA are affected when you stop ingestion.
- **Required permissions**: the roles you need.
- A note that only tables with 90 days of retention or less are included.

[![Screenshot of the Update your content to use Defender data side panel, showing content counts and recommendation progress.](media/transition-soc-optimization-recommendations/soc-optimization-progress-panel.png)](media/transition-soc-optimization-recommendations/soc-optimization-progress-panel.png#lightbox)

A recommendation is resolved when its status is set to **Completed** or **Dismissed**. When all **Lower Defender data costs** recommendations are **Completed** or **Dismissed**, the banner and the section header link no longer appear. After you've updated and validated all dependent content, stop ingestion as described in Work through Lower Defender data costs recommendations.

## Review a Lower Defender data costs recommendation

Each recommendation covers one table in one workspace. Select a recommendation to open its details pane. The pane includes these sections:

| Section | What it shows |
| --- | --- |
| **Why we recommend this** | Why SOC optimization recommends this change for the table. |
| **Monthly estimated data volume** | The estimated monthly data volume for the table. |
| **What we've found** | The number of analytics rules, workbooks, and playbooks that use the table. |
| **What to do** | The steps to update your content. |
| **Before stopping ingestion** | How data collection rules (DCRs) and, for some tables, UEBA are affected when you stop ingestion. |
| **Table details** | Details about the table. The pane shows: "Data is calculated and refreshed every 24 hours." |

In the pane, you can select **Change status**, **Provide feedback**, or **View full details**.

[![Screenshot of a Lower Defender data costs recommendation details pane with Why we recommend this, What we've found, and What to do sections.](media/transition-soc-optimization-recommendations/soc-optimization-recommendation-pane.png)](media/transition-soc-optimization-recommendations/soc-optimization-recommendation-pane.png#lightbox)

Select **View full details** to open the recommendation page. The **Analytic rules**, **Playbooks**, and **Workbooks** tabs list the content that uses the table. To migrate analytics rules, use the **Analytic rules** tab. For more information, see Migrate analytics rules with the migration tool.

[![Screenshot of a Lower Defender data costs recommendation page with the Analytic rules, Playbooks, and Workbooks tabs.](media/transition-soc-optimization-recommendations/soc-optimization-recommendation-page.png)](media/transition-soc-optimization-recommendations/soc-optimization-recommendation-page.png#lightbox)

Note

- The **Analytic rules**, **Playbooks**, and **Workbooks** tabs list content that queried the table in the last 90 days. The lists refresh every 24 hours, so recent changes might not show yet, and deleted content might still be listed. A list can also include content that uses the table through a parser or function, or that only mentions the table in a comment. For analytics rules, this includes detections that use Advanced Security Information Model (ASIM) normalization. Review each item before you change it.
- The list shows only analytics rules, workbooks, and playbooks. If it's empty, still check for other content that uses the table, such as hunting queries, summary rules, DCRs, and external tools, before you set the status to **Completed**.

## Work through Lower Defender data costs recommendations

Do steps 1–5 for each recommendation. Do step 6 once, after all recommendations are complete.

1. Update Defender role-based access control (RBAC). Make sure that the users, groups, and automation identities that use the data have the required permissions in Microsoft Defender. For more information, see Update permissions and roles.
2. Open each **Lower Defender data costs** recommendation, and review the content that uses the table.
3. Update the content to query Defender data with Advanced Hunting. To migrate analytics rules, see Migrate analytics rules with the migration tool. For other content, see Update dependent content.
4. Test the updated content. For more information, see Validate your updated content.
5. Set the status of the recommendation manually. When you start, select **Change status** &gt; **In progress**. When you finish, set the status to **Completed**. If you don't plan to act on the recommendation, set the status to **Dismissed**.
6. After you complete all **Lower Defender data costs** recommendations, stop ingesting Defender XDR data into Log Analytics for the supported Defender XDR tables in the workspace. In the Defender portal, go to **Setup & configuration** &gt; **Data management** &gt; **Data & connectors**, select the **Tables** tab, and then select **Configure workspace**. Stopping this ingestion lowers your costs.

Note

- **Lower Defender data costs** recommendations don't complete automatically. Set the status yourself.
- Completing a rule migration sets the rule status to **Completed**. It doesn't change the status of the recommendation.

## Identify dependent content

For each table that you plan to transition, identify all content that queries, processes, or depends on that data.

Review dependencies including:

- Hunting and saved queries.
- Analytics rules.
- Custom detections.
- Workbooks.
- Logic App playbooks.
- Continuous integration and continuous delivery (CI/CD) deployments and repositories.
- Reports and API integrations.
- User, group, and automation permissions.
- Data collection rules (DCRs) and transformations on the table, including filter and split rules from the **Tables** page.

Search your queries and content repositories for references to the affected Microsoft Sentinel tables so that you can identify dependencies that aren't surfaced directly by a SOC optimization recommendation.

## Update dependent content

The changes required depend on how each table is used in your environment.

| Area | What to review and update |
| --- | --- |
| Queries and content | Update Kusto Query Language (KQL) queries to use the corresponding Advanced Hunting tables and schemas. |
| Permissions and roles | Make sure users and groups have access to the corresponding Microsoft Defender workloads through Microsoft Defender unified role-based access control (RBAC). |
| Analytics rules | Convert applicable Microsoft Sentinel analytics rules to Microsoft Defender custom detections and validate detection behavior. |
| Workbooks | Update workbook queries to use Advanced Hunting data and validate tiles, filters, and parameters. |
| Logic App playbooks | Replace Log Analytics or Azure Monitor Logs query actions with Microsoft Graph Advanced Hunting API calls where required. |
| CI/CD | Review deployed content and repositories for references to Microsoft Sentinel tables or other workspace-specific dependencies. |
| DCRs and transformations | Keep the table at 180 days or more to keep the DCR working, or move its logic into queries in Defender. See Check data collection rules and transformations. |
| Ingestion | Change ingestion only after all affected content has been updated and validated. |

### Update queries to use Advanced Hunting tables

Update queries that use Microsoft Sentinel workspace tables so that they use the corresponding Microsoft Defender XDR Advanced Hunting tables.

Depending on the table, changes can include:

- Replacing Microsoft Sentinel table names with their Advanced Hunting equivalents.
- Keeping or replacing `TimeGenerated`. When your Microsoft Sentinel workspace is connected to the Defender portal, `TimeGenerated` works in Advanced Hunting. For new queries, and for custom detections that run in near real time (**Continuous (NRT)** frequency), use `Timestamp`. `CallActivityEvents` doesn't have a `Timestamp` column. For that table, use `ActivityTimestamp`. For more information, see [Changes that apply to all tables](transition-advanced-hunting-tables#changes-that-apply-to-all-tables).
- Updating field names and data types.
- Removing dependencies on Sentinel-specific metadata fields that aren't available in Advanced Hunting.

Validate each updated query in Advanced Hunting before using it in production content.

For more information, see [Update content to use Advanced Hunting tables](transition-advanced-hunting-tables).

### Update permissions and roles

Access to Microsoft Sentinel workspace data doesn't automatically provide access to the corresponding Microsoft Defender workload data.

Make sure affected users and groups have the required Microsoft Defender permissions before changing ingestion.

For more information, see [Update permissions and roles with Unified RBAC](transition-unified-rbac).

### Update analytics rules and custom detections

Review Microsoft Sentinel analytics rules that depend on affected tables.

For eligible rules, use the preview migration tool. Validate differences in scheduling, entity mappings, alert configuration, automation, and other rule behavior before completing migration.

For rules that the tool can't convert, see [Manually convert analytics rules to custom detections](transition-custom-detections).

### Update workbooks

Review workbook queries that depend on affected Microsoft Sentinel tables.

Update applicable workbook queries to use Advanced Hunting data, and validate:

- Queries.
- Tiles and visualizations.
- Filters.
- Parameters.
- User access to the underlying data.

For more information, see [Update workbooks to use Advanced Hunting data](update-workbooks-advanced-hunting-data).

### Update Logic App playbooks

Review Logic App playbooks that query Log Analytics, Azure Monitor Logs, or workspace-based Microsoft Sentinel data.

Where required, update the playbook to use the Microsoft Graph Advanced Hunting API and validate authentication, query results, response parsing, and downstream actions.

For more information, see [Update Logic App playbook automation](transition-logic-app-playbooks).

### Review CI/CD deployments

Review CI/CD repositories and deployments for content that references affected Microsoft Sentinel tables or workspace-specific resources.

Update and validate affected deployments before changing ingestion.

For more information, see [Deploy content as code with CI/CD in ISOC](/en-us/defender-xdr/deploy-content-integrated-security-operations).

## Migrate analytics rules with the migration tool (Preview)

Use the preview migration tool to migrate one rule or all eligible rules in a recommendation. Each rule moves through migration, validation, and completion independently.

Important

The original analytics rule remains enabled while the custom detection is created and validated. Only **Complete migration** disables the original rule. Don't stop ingestion until you've validated all dependent content for all Defender XDR tables.

### Review rule eligibility

Open the recommendation for the table that you plan to transition and check each rule's status.

1. In the [Microsoft Defender portal](https://security.microsoft.com/), open **SOC optimization**.
2. Select the **Lower Defender data costs** recommendation for the affected table.
3. Select the **Analytic rules** tab and review the migration summary and per-rule statuses.

    [![Screenshot of the preview migration status summary and analytics rules with Ready to migrate and Migration unavailable statuses.](media/transition-soc-optimization-recommendations/migration-rule-statuses.png)](media/transition-soc-optimization-recommendations/migration-rule-statuses.png#lightbox)
4. For a rule marked **Migration unavailable**, select **Open migration tool**, and on the **Get started** tab select **Download CSV** to review the blocker. Modify the rule where appropriate or follow the [manual conversion guidance](transition-custom-detections). Keep the original rule enabled until you've validated its replacement.

Eligibility and migration are separate. Being listed in a recommendation doesn't mean a rule is ready to migrate.

| Status | Meaning | Next action |
| --- | --- | --- |
| **Ready to migrate** | The rule is eligible for conversion by the migration tool. | Start migration for the rule. |
| **Migration unavailable** | The current migration flow can't convert the rule. | Download the CSV report and review the reason. |
| **Validation required** | The custom detection was created and generates tagged alerts while the original analytics rule remains enabled. | Compare behavior and dependent automation before completing migration. |
| **Completed** | The custom detection is enabled and editable, and the original analytics rule is disabled. | Confirm the final state and review other dependencies. |

### Start migration

Choose the scope carefully. Starting migration creates custom detections for validation; it doesn't disable the original analytics rules.

To migrate one rule:

1. On the **Analytic rules** tab, select a rule marked **Ready to migrate** to open its side panel.
2. Select **Migrate rule**.
3. Wait for the migration to finish. The rule then shows **Validation required**.

To migrate all eligible rules in the recommendation:

1. Select **Open migration tool**.
2. On the **Get started** tab, review the **Migration**, **Validation**, and **Completion** stages.
3. Select **Migrate now**.

    Important

    **Migrate now** starts migration for all rules marked **Ready to migrate** in the recommendation. Filtering the recommendation's rule list doesn't narrow the migration scope. Rules for which migration isn't available aren't included.

Rules are processed independently. In a bulk migration, a rule that fails or remains unavailable doesn't prevent successfully created rules from moving to validation.

### Validate the custom detections

During preview validation, both the custom detection and its original analytics rule generate alerts. The custom detection's alerts are tagged for validation. Use the alert tuning rule you configured to reduce duplicate alert noise; don't assume those alerts are automatically resolved without it.

1. Open the migration tool and select **Rules being validated**. On the **Detection rules** page, you can also select **Review rules under validation** to filter the list to rules in validation.
2. Review each custom detection over a representative period.
3. Compare alert volume, timing, severity, title, entities, and scheduling with the original analytics rule.
4. Verify that downstream automation works with the custom detection's alerts. Review the preview alert compatibility differences when comparing results.

    [![Screenshot of the preview migration validation panel with Complete migration and Cancel and delete actions.](media/transition-soc-optimization-recommendations/migration-validation-panel.png)](media/transition-soc-optimization-recommendations/migration-validation-panel.png#lightbox)

During validation, you can edit migrated custom detections, except the alert title. If a rule needs more validation, leave it in validation. You don't have to complete every rule in a bulk migration at the same time.

### Complete or cancel migration

Complete migration only for rules whose detection results and dependent automation you've validated. Completion is the point at which the original analytics rule is disabled.

Important

In the preview migration flow, the disabled original analytics rule is automatically deleted after 90 days. Validate the replacement and its dependent automation before completing migration.

1. In the validation panel, select the rules that passed validation.
2. Select **Complete migration**. The custom detections are enabled and editable, and the corresponding analytics rules are disabled. You can also complete migration from the custom detection page.
3. Return to the recommendation and confirm that those rules show **Completed**.

    [![Screenshot of preview rule statuses showing one rule with Migration unavailable and two completed migrations.](media/transition-soc-optimization-recommendations/migration-completed-rules.png)](media/transition-soc-optimization-recommendations/migration-completed-rules.png#lightbox)
4. Update and validate all remaining rules and other dependencies for the table. Then set the recommendation status to **Completed**. Recommendations don't complete automatically.

To abandon a migration before completion, select the rule in the validation panel and choose **Cancel and delete**. The new custom detection is deleted, and the original analytics rule remains enabled.

### Review alert compatibility differences (Preview)

Alerts from migrated custom detections preserve selected analytics-rule properties to support existing Microsoft Sentinel flows. They don't have exactly the same properties as alerts from other custom detections. Validate your integrations rather than assuming every existing flow is compatible.

The following values describe the **Microsoft Sentinel view** of alerts in workspaces onboarded to the Defender portal. Optional properties depend on the information available for each alert.

| Property | Value for a migrated rule in Microsoft Sentinel | Validation consideration |
| --- | --- | --- |
| `ProviderName` | `Microsoft Sentinel` | Other custom detections use `MicrosoftThreatProtection` or `MDATP`. |
| `ProductComponentName` | `ASI Scheduled Alerts` or `ASI NRT Alerts` | Identifies the rule type. |
| `ProductName` | `Azure Sentinel` | The migrated rule's product name is also `Azure Sentinel` in Defender. |
| `AlertType` | `<sourceWorkspaceId>_<sourceAnalyticRuleId>` | Defender keeps the custom detection detector ID instead of this Sentinel compatibility value. |
| `ExtendedProperties["Analytic Rule Ids"]` | Same value as in the source analytics rule. | Identifies the original analytics rule, not the custom detection. |
| `ExtendedProperties["Analytic Rule Name"]` | Same value as in the source analytics rule. | Separate from the generated alert title. |
| `ExtendedProperties["MigratedAnalyticRule"]` | `"true"` | Identifies alerts from migrated rules. |
| `ExtendedProperties["Correlation Id"]` | The rule execution ID. | Identifies an execution, not an individual alert. |
| `ExtendedProperties["Query Start Time UTC"]` and `ExtendedProperties["Query End Time UTC"]` | Same values as in the source analytics rule. | Different from the alert's activity start and end times. |
| `ExtendedProperties["Query Period"]` | Same value as in the source analytics rule. | Review integrations that use the query period. |
| `ExtendedProperties["Trigger Operator"]` and `ExtendedProperties["Trigger Threshold"]` | Same values as in the source analytics rule. | Review integrations that use the trigger configuration. |
| `ExtendedProperties["Event Grouping"]` | Same value as in the source analytics rule. | Describes alert generation, not incident grouping. |
| `ExtendedProperties["Search Query Results Overall Count"]` | Same value as in the source analytics rule, when available. | Don't assume a total result count is available for grouped alerts. |
| `ExtendedProperties["Data Sources"]` | Same value as in the source analytics rule. | Review integrations that use data-source metadata. |
| `ExtendedProperties["Query"]` and `ExtendedProperties["OriginalQuery"]` | Not available in this preview. | Integrations that depend on these fields need review before completion. |

### Review known issues and troubleshoot migration (Preview)

Review these preview limitations before completing migration:

- For rules configured to group all events into one alert, two duplicate alerts can occasionally reach the `SecurityAlert` table and downstream automation instead of one.
- `ExtendedProperties["Query"]` and `ExtendedProperties["OriginalQuery"]` aren't available on alerts from migrated custom detections.

Use the per-rule status and surfaced errors to decide what to do next.

| Symptom | Action |
| --- | --- |
| **Migrate now** is unavailable. | No rules are marked **Ready to migrate**. If evaluation hasn't finished, wait and select **Refresh**. |
| A rule shows **Migration unavailable**. | Download the CSV report, review the per-rule reason, and use the manual conversion guidance where needed. |
| Validation needs more time or exposes a problem. | Leave the rule in validation, or use **Cancel and delete** before completion. The original analytics rule remains enabled. |

## Validate your updated content

Before you stop ingestion, validate the affected content end to end.

Make sure that:

- Updated KQL queries return the expected data in Advanced Hunting.
- Analysts and other users can access the required Microsoft Defender data.
- Custom detections generate the expected alerts.
- Workbooks return the expected results.
- Logic App playbooks run successfully with the updated data source.
- CI/CD deployments don't reintroduce outdated table references or configurations.
- Reports, APIs, and other integrations continue to return the expected data.
- You've reviewed any DCR or transformation on the table and chosen an option for it.

Complete validation for one table before continuing to the next table.

## Check data collection rules and transformations before you stop ingestion

Some organizations use a [data collection rule (DCR)](/en-us/azure/azure-monitor/data-collection/data-collection-rule-overview) to change Microsoft Defender XDR data before it's stored in their Microsoft Sentinel workspace. For example, they filter rows, send part of the data to the data lake, hide fields, or add new fields. This is also called a [workspace transformation, or a workspace transformation DCR](/en-us/azure/azure-monitor/data-collection/data-collection-transformations). [Filter and split rules](transformation-filter-split) that you create on the **Tables** page in the Defender portal also use a DCR.

This section applies to you if a DCR changes a Microsoft Defender XDR table (XDR table). Most of it matters when you stop ingestion with **Configure workspace**. The user and entity behavior analytics (UEBA) part applies if UEBA uses the DeviceLogonEvents table. If you don't use DCRs on XDR tables, you can skip this section.

### What happens when you stop ingestion

A DCR runs only on data that's ingested into your Microsoft Sentinel workspace. When you select **Configure workspace** on the **Tables** tab of **Data & connectors**, Defender XDR tables are no longer ingested into the workspace, so the DCR no longer applies to them. Tables with analytics retention set to 180 days or more stay ingested, and their DCR keeps working. The original, unchanged data stays available in Defender for 90 days, and you can query it in [Advanced Hunting](/en-us/defender-xdr/advanced-hunting-overview).

You might already see unfiltered data in Advanced Hunting today. [Filter and split rules on XDR tables don't show in Advanced Hunting for the first 30 days of data](transformation-filter-split#known-limitations).

The following table describes the effect for common DCR uses:

| What you use the DCR for | What changes when you stop ingestion | What you can do |
| --- | --- | --- |
| Filter rows or remove columns to lower cost | The filter no longer applies. Microsoft Sentinel charges for ingesting this table stop. | No action needed for cost. Queries and rules that you move to Defender see the unfiltered data, so check their results. |
| Send part of the data to the data lake only ([split rule](transformation-filter-split) on the Tables page) | The `_SPLT` table and the data lake copy of this table stop receiving new data, because the [data lake mirrors the data that's ingested into the workspace](manage-data-overview). Defender keeps the data for 90 days. | If you need the data for longer than 90 days, keep the table at 180 days or more, or use [streaming export from Defender](/en-us/defender-xdr/streaming-api) to your own storage. |
| Add or calculate fields ([columns that end in `_CF`](/en-us/azure/azure-monitor/logs/tutorial-workspace-transformations-portal)) | These fields don't exist in the Defender table. Queries and rules that use them fail. | [Calculate the field in the query](transition-advanced-hunting-tables), or keep the table at 180 days or more. |
| Copy data to a custom table | The custom table stops receiving new data. | Keep the table at 180 days or more, or use [streaming export from Defender](/en-us/defender-xdr/streaming-api). |
| Hide or mask fields | Defender data isn't masked. | Review who can access raw data in Defender. Use [Defender RBAC](transition-unified-rbac), [device groups](/en-us/defender-endpoint/machine-groups), and [Defender for Identity scoped access](/en-us/defender-for-identity/configure-scoped-access). |
| Filter out known-benign events | You might see more alerts. | Add exclusions to your [custom detection queries](/en-us/defender-xdr/custom-detection-rules), or create an [alert tuning rule](/en-us/defender-xdr/investigate-alerts#tune-an-alert) in Defender. |
| [Data export rules](/en-us/azure/azure-monitor/logs/logs-data-export) | They stop exporting new data. [Streaming export from Defender](/en-us/defender-xdr/streaming-api) exports the original data, not the transformed data, so the volume and content at the destination can change. | Use streaming export from Defender. |
| [Summary rules](summary-rules), search jobs, and other jobs that read the table | They stop getting new data, and so do the tables they fill. | Keep the table at 180 days or more. These jobs need the data in the workspace. |

### Check whether you're affected

To check whether a DCR changes an XDR table:

1. In the Defender portal, go to **Setup & configuration** &gt; **Data management** &gt; **Data & connectors**, and select the **Tables** tab. Check the **Transformation Rules** column for the XDR table. It shows **Filter** or **Split** when a [filter or split rule](transformation-filter-split) is active. A split rule also creates a table with an `_SPLT` suffix, for example `DeviceProcessEvents_SPLT`.
2. Check the table schema for [custom columns that end in `_CF`](/en-us/azure/azure-monitor/logs/tutorial-workspace-transformations-portal).
3. Check your [data export rules](/en-us/azure/azure-monitor/logs/logs-data-export) and [summary rules](summary-rules) for the table.
4. If you have more than one workspace, check each one. Each workspace has its own DCR and its own recommendations.
5. To list workspace DCRs that change XDR tables, run this query in [Azure Resource Graph Explorer](/en-us/azure/governance/resource-graph/first-query-portal). You need Reader access to the subscriptions that hold your workspaces; otherwise the results are incomplete.

```kusto
resources
| where type =~ "microsoft.operationalinsights/workspaces"
| extend DcrId = tolower(tostring(properties.defaultDataCollectionRuleResourceId))
| where isnotempty(DcrId)
| project WorkspaceName = name, subscriptionId, DcrId
| join kind=inner (
    resources
    | where type =~ "microsoft.insights/datacollectionrules" and kind =~ "WorkspaceTransforms"
    | extend DcrId = tolower(id)
    | mv-expand flow = properties.dataFlows
    | mv-expand stream = flow.streams
    | extend TableName = replace_string(tostring(stream), "Microsoft-Table-", ""),
             Transformation = tostring(flow.transformKql)
    | where Transformation !~ "source"
    | project DcrId, DcrName = name, TableName, Transformation
) on DcrId
| project WorkspaceName, subscriptionId, DcrName, TableName, Transformation
```

The query lists only the DCR that's linked to each workspace, and skips DCRs that pass the data through unchanged. Check the results for the tables that appear in your **Lower Defender data costs** recommendations.

### Choose an option for each table

**Option 1: Keep your DCR working**

Keep the table ingested in your Microsoft Sentinel workspace. The DCR stays in place and keeps running.

1. In the Defender portal, go to **Setup & configuration** &gt; **Data management** &gt; **Data & connectors**, and select the **Tables** tab.
2. Select the table, then select **Manage table**. For details, see [Configure table settings in Microsoft Sentinel](manage-table-tiers-retention).
3. Set the analytics retention to **180 days or more**, and save.

Do this before you select **Configure workspace**. Data that was already deleted before you change the setting isn't restored.

Additional charges apply when you extend retention beyond the 90 days included with ISOC. For details and pricing, see [Data ingestion, retention, and billing for ISOC in Microsoft Defender](/en-us/defender-xdr/integrated-security-operations-data-billing-retention).

**Option 2: Use the data in Defender**

Keep the table's analytics retention under 180 days. When you select **Configure workspace**, ingestion stops for the table, and you use the original data in Defender, which is kept for 90 days:

- **Added fields (`_CF`):** calculate them in the query. The source data is in the Defender table. See [Update Microsoft Sentinel content to use Advanced Hunting tables](transition-advanced-hunting-tables).
- **Exports:** use [streaming export from Defender](/en-us/defender-xdr/streaming-api).
- **Alert noise:** add exclusions to your [custom detection queries](/en-us/defender-xdr/custom-detection-rules), or create an [alert tuning rule](/en-us/defender-xdr/investigate-alerts#tune-an-alert).
- **Access:** set [device groups](/en-us/defender-endpoint/machine-groups) and [Defender for Identity scope](/en-us/defender-for-identity/configure-scoped-access), and review [imported roles](transition-unified-rbac).

Changes to table retention can take up to 48 hours to appear in SOC optimization.

### UEBA and DeviceLogonEvents

This applies to you if UEBA is turned on and a data collection rule (DCR) changes the **DeviceLogonEvents** table in your Microsoft Sentinel workspace.

UEBA processes the logon data that comes from Defender XDR only when no DCR applies to the DeviceLogonEvents table in your workspace. This keeps the data that UEBA processes in line with your DCR.

- To let UEBA process this data, stop the DCR on the DeviceLogonEvents table. Before you stop it, check what the DCR does. If it hides or masks sensitive fields, review who can access the raw data in Defender.
- If you keep the DCR, UEBA doesn't process the Defender XDR logon data.

For more information, see [Update UEBA to use Microsoft Defender XDR data](transition-ueba-to-xdr-data).

## Review retention and ingestion

Before making ingestion changes, review the retention available for the Microsoft Defender data that you're transitioning.

Eligible ISOC customers receive 90 days of included retention for supported Microsoft Defender data, Azure Activity data, and Office 365 Activity data.

If you need to keep a DCR working on a table, set that table's retention to 180 days or more before you select **Configure workspace**. See Check data collection rules and transformations.

For information about supported data, retention, and billing, see [Data ingestion, retention, and billing for ISOC in Microsoft Defender](/en-us/defender-xdr/integrated-security-operations-data-billing-retention).

After you complete all **Lower Defender data costs** recommendations, stop ingesting Defender XDR data into Log Analytics for the supported Defender XDR tables in the workspace. In the Defender portal, go to **Setup & configuration** &gt; **Data management** &gt; **Data & connectors**, select the **Tables** tab, and then select **Configure workspace**. Stopping this ingestion lowers your costs.

For more information, see [Optimize Microsoft Defender XDR data ingestion](transition-optimize-xdr-ingestion).