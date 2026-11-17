---
layout: Conceptual
title: Troubleshoot Microsoft Sentinel analytics rule migration blockers | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/transition-custom-detections-migration-blockers
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
description: Resolve blockers when migrating Microsoft Sentinel analytics rules to Microsoft Defender custom detections. Review report codes and validate changes safely.
author: omerbinyamin
ms.author: omerbinyamin
ms.localizationpriority: high
ms.collection: ms-security
ms.topic: troubleshooting-general
ai-usage: ai-generated
ms.custom: msecd-doc-authoring-1032
ms.date: 2026-11-15T00:00:00.0000000Z
locale: en-us
document_id: 308b2aea-43e9-b58c-16e6-8dd901269fdf
document_version_independent_id: c83b4f13-2661-d487-0223-e3ccd4c799dd
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/transition-custom-detections-migration-blockers.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/transition-custom-detections-migration-blockers
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/transition-custom-detections-migration-blockers.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7e593268-8d01-46ef-aa78-9d1388e6a294
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/264d03ab-bab8-454b-a56c-0fedead7f602
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
platformId: 426920cf-39c8-6adc-c26c-1b1255fe75b5
---

# Troubleshoot Microsoft Sentinel analytics rule migration blockers | Microsoft Learn

When an analytics rule shows **Migration isn't available**, use its migration report to identify the blocker. Match the report code to the guidance, decide whether a change is safe, and validate the rule before reassessing eligibility.

Before editing a rule, review the access, backup, and validation prerequisites.

## Prerequisites

- Permissions to edit analytics rules and manage custom detections.
- An exported or copied rule configuration that you can restore.
- A representative validation period and expected test events.
- A list of automation rules, playbooks, workbooks, and integrations that depend on the current alerts.

Important

Rule changes can affect alert volume, timing, entities, incidents, and automation. Don't change a rule only to get migration eligibility. Keep the original analytics rule enabled until migration is explicitly completed. Validate every change, and retain the original behavior when the operational risk is greater than the benefit of migrating now.

## Troubleshooting checklist

Identify the reported blocker and the safest next action before editing.

### Download and match the report

Use the latest report to identify the blocker and assess a safe resolution.

1. In the SOC optimization recommendation, select **Download report** for rules marked **Migration isn't available**.
2. Match the error code or message to the blocker index.
3. Record the current rule configuration and expected behavior.
4. Decide whether to edit the rule, evaluate a separate redesign, or retain it until a supported migration path is available.

### Validate source-rule changes

Test the edited analytics rule before requesting reassessment.

1. Change one blocker at a time when practical.
2. Save the edited analytics rule and validate that it still detects the intended activity.
3. Compare alert volume, timing, entities, incident behavior, and dependent automation.
4. Reassess eligibility only after the changes preserve detection intent.

## Causes and solutions

Use the exact report code to find the relevant category. Match the report wording below to the message in your downloaded report. Values in braces are placeholders. A rule can have more than one blocker.

| Blocker | Report code |
| --- | --- |
| Dynamic alert properties | `UnsupportedAlertDetailsOverride`, `UnsupportedAlertProperty`, `InvalidDynamicProperties` |
| Unsupported entity type | `UnsupportedEntityType` |
| Unsupported Sentinel entities mapping | `UnsupportedSentinelEntitiesMapping` |
| Alerts without incidents | `UnsupportedIncidentConfiguration` |
| Secondary workspace | `NonPrimaryLogAnalyticsWorkspace` |
| Cross-workspace query | `CrossWorkspaceCustomDetectionNotSupported` |
| NRT watchlist | `NrtFunctionsNotSupported` |
| NRT multiple tables | `NrtMultipleTablesNotSupported` |
| NRT workspace operator | `NrtCrossWorkspaceNotSupported` |
| Other streaming failure | `NrtStreamingIncompatible`, `NrtStreamingCompatibilityUnknown` |
| NRT externaldata | `NrtExternalDataNotSupported` |
| NRT event grouping | `UnsupportedNrtSingleAlertGrouping` |
| ASIM, custom, or nested functions | `UnsupportedLogAnalyticsCustomFunction`, `NrtFunctionsNotSupported`, `HuntingRuleWithPrivateFunction`, `HuntingRuleQuerySyntaxErrors` |
| Suppression | `UnsupportedSuppression` |
| Non-default threshold | `UnsupportedThreshold` |

### Dynamic alert properties and alert-details overrides

**Report codes:**`UnsupportedAlertDetailsOverride`, `UnsupportedAlertProperty`, `InvalidDynamicProperties`.

**Report wording:** The Analytics Rule overrides dynamic alert details; Custom Detections have no equivalent override.

**Resolution:** Remove the dynamic alert-details overrides, retaining values analysts need as custom details. If several static values are required, splitting the rule is a redesign to validate before adoption. Apply changes only when they preserve detection intent.

### Unsupported entity type

**Report code:**`UnsupportedEntityType`.

**Report wording:** The rule contains an entity type that is not supported by custom detections. Unsupported AnalyticsEntityType: {value}

**Resolution:** Replace the unsupported mapping with a supported entity type that carries the same information. Remove the mapping only if investigation and automation don't need it.

### Unsupported Sentinel entities mapping

**Report code:**`UnsupportedSentinelEntitiesMapping`.

**Report wording:** The rule uses Sentinel prebuilt entity mappings that are not supported by custom detection alert creation.

**Resolution:** Replace the prebuilt mapping with explicit, supported entity mappings taken from the query results.

### Alerts without incidents

**Report code:**`UnsupportedIncidentConfiguration`.

**Report wording:** The Analytics Rule has custom incident configuration; Custom Detections have no incident configuration equivalent.

**Resolution:** If the behavior change is acceptable, enable incident creation with the default settings. Use Defender alert tuning or automation rules if incidents should be auto-resolved or hidden. Validate the changed incident behavior and dependent automation before migration.

### Rule runs on a secondary workspace

**Report code:**`NonPrimaryLogAnalyticsWorkspace`.

**Report wording:** Custom Detections that query Log Analytics tables can only be created on the tenant's primary workspace.

**Resolution:** Recreate the rule against equivalent data in the primary workspace. Keep the original enabled until the replacement is validated. If equivalent data isn't available locally, retain the rule in Sentinel.

### Cross-workspace query using workspace()

**Report code:**`CrossWorkspaceCustomDetectionNotSupported`.

**Report wording:** This Analytics Rule references multiple workspaces ({WorkspaceIds}). Custom Detections require a single workspace. Rewrite the query to use one workspace and try again.

**Resolution:** Replace every `workspace()` call with equivalent local tables, or split the rule and retain the remote-data logic in Sentinel.

### NRT rule uses a watchlist

**Report code:**`NrtFunctionsNotSupported`.

**Report wording:** This NRT Analytics Rule references query functions ({FunctionNames}). Streaming Custom Detections do not support function references. Rewrite the query using supported KQL without functions and try again.

**Resolution:** Remove the watchlist lookup only if detection intent is preserved. If the lookup is essential, change the rule to a scheduled analytics rule before migration.

### NRT rule queries multiple tables

**Report code:**`NrtMultipleTablesNotSupported`.

**Report wording:** This NRT Analytics Rule references multiple tables ({DistinctTableNames}); streaming Custom Detections require a single table. Rewrite the query to use one table and try again.

**Resolution:** Rewrite the query to use one table, or split it into single-table detections. If the cross-table logic is essential, use a scheduled analytics rule.

### NRT rule uses the workspace operator

**Report code:**`NrtCrossWorkspaceNotSupported`.

**Report wording:** This NRT Analytics Rule references multiple workspaces ({WorkspaceIds}). Streaming Custom Detections require a single workspace. Rewrite the query to use one workspace and try again.

**Resolution:** Replace each `workspace()` call with the equivalent local table, or retain the remote-data logic in a separate Sentinel rule.

### Other streaming failure

**Report codes:**`NrtStreamingIncompatible`, `NrtStreamingCompatibilityUnknown`.

**Report wording for NrtStreamingIncompatible:** The NRT Analytics Rule could not be validated as compatible with streaming Custom Detections. {StreamingCompatibilityReason}

**Report wording for NrtStreamingCompatibilityUnknown:** Streaming compatibility could not be determined for this NRT Analytics Rule; migration requires a confirmed compatible query.

**Resolution:** Simplify the query to single-table streaming KQL without functions, joins, unions, or external references. If the required logic can't be preserved, use a scheduled analytics rule.

### NRT query uses externaldata

**Report code:**`NrtExternalDataNotSupported`.

**Report wording:** This NRT Analytics Rule uses the externaldata operator, which is not supported in streaming Custom Detections. Remove the externaldata reference and try again.

**Resolution:** Write the external data values directly into the query filter, or use a scheduled analytics rule if the external data is essential.

### NRT rule uses event grouping

**Report code:**`UnsupportedNrtSingleAlertGrouping`.

**Report wording:** NRT Custom Detections don't support grouping all query results into a single alert.

**Resolution:** Switch the rule to one alert per event only when that behavior is acceptable. If events need to be grouped into a single alert, use a scheduled analytics rule.

### ASIM, custom, or nested functions

**Report codes:**`UnsupportedLogAnalyticsCustomFunction`, `NrtFunctionsNotSupported`, `HuntingRuleWithPrivateFunction`, `HuntingRuleQuerySyntaxErrors`.

**Report wording:** This Analytics Rule uses the Log Analytics custom function '{FunctionName}'. Custom functions aren't currently supported for migration to Custom Detections. Inline the function logic in the rule query and try again.

**Resolution:** Inline the logic of every custom, ASIM, or nested function so that the rule query no longer calls saved functions. Validate that the rewritten query preserves the intended behavior.

### Suppression is enabled

**Report code:**`UnsupportedSuppression`.

**Report wording:** The Analytics Rule uses alert suppression; Custom Detections have no suppression equivalent.

**Resolution:** Turn off **Stop running query after alert is generated** only when the change is acceptable. Handle noise with KQL aggregation, alert tuning, or automation, and validate the resulting alert volume.

### Non-default trigger threshold

**Report code:**`UnsupportedThreshold`.

**Report wording:** The Analytics Rule only alerts after {N} matches ({Operator}); Custom Detections have no threshold equivalent. A structural conversion can instead return: Unsupported AlertTriggerOperator: {value}.

**Resolution:** Move the threshold into the query by aggregating and filtering. Then set the alert threshold to **greater than 0** and validate the results.

## Reassess eligibility

Eligibility refresh isn't instant. After saving and validating changes:

1. Return to the SOC optimization recommendation and open **Analytic rules**.
2. Select **Refresh** and wait while the rule shows **Under evaluation**.
3. If the rule becomes **Ready to migrate**, select it and follow the [single-rule or bulk migration flow](transition-custom-detections-automatic#migrate-analytics-rules).
4. If **Migration isn't available** remains, download a new report and resolve the next blocker.
5. Repeat the edit, validation, and reassessment cycle until the rule is ready or you choose to retain it in Sentinel.

## Review unresolved issues

Use the following checks if eligibility or detection behavior doesn't match expectations.

| Issue | Next action |
| --- | --- |
| The rule is still unavailable. | Download a new report because another blocker might remain. |
| The rule stays **Under evaluation**. | Wait, select **Refresh**, and confirm that the saved rule and workspace match the recommendation. |
| Alert volume increased after editing. | Restore the original configuration or tune the query before migration. |
| Entity or incident quality degraded. | Restore the stronger mapping or incident behavior and retain the rule until support is available. |
| The rewritten query produces different results. | Compare parameters, functions, time filters, joins, projected columns, and result schema. |
| Required data isn't available locally. | Retain the rule in Sentinel. A rule edit doesn't resolve the data-availability constraint. |