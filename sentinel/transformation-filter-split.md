---
layout: Conceptual
title: Transform data using filter and split in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/transformation-filter-split
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
ms.subservice: sentinel-platform
search.appverid: met150
description: Learn how to use filter and split data transformations to streamline ingestion, reduce costs, and route data between Analytics and Data lake tiers in Microsoft Sentinel.
author: EdB-MSFT
ms.author: edbaynash
ms.topic: how-to
ms.date: 2026-07-20T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 2878ff12-c7bd-4011-9681-0ba1775f147e
document_version_independent_id: 957d4eb5-70b5-6035-48ca-b4103955f15b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/transformation-filter-split.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/transformation-filter-split
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/transformation-filter-split.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
platformId: 3b92c366-4012-5b12-2a9e-a2bc75f763a3
---

# Transform data using filter and split in Microsoft Sentinel | Microsoft Learn

As security data volumes continue to grow, organizations face the challenge of balancing cost-effective retention of telemetry used for AI, compliance, and investigations while ensuring that only necessary data is retained in high-performance storage tiers. Use filter and split data transformations in Microsoft Sentinel to address this challenge by modifying data at ingestion time to optimize your data retention strategy.

This article describes how to configure filter and split data transformations without the need to manually create custom Data Collection Rule (DCR) configurations. When you tailor data ingestion by using filter and split data transformations, you can improve performance and reduce noise.

By using data transformations, you can optimize your security data pipeline by controlling what data is stored and in which tier. Using filter and split transformations provides the following benefits:

- **Cost optimization**: Reduce storage and processing costs by filtering out low-value data that doesn't contribute to threat detection. Route less frequently accessed data to cost-effective Data lake storage while keeping high-priority data in the Analytics tier.
- **Improved SOC efficiency**: Focus your security operations center (SOC) on actionable, high-value events. By removing noise at ingestion time, analysts spend less time sifting through irrelevant logs and more time investigating real threats.
- **Faster query performance**: Smaller datasets in the Analytics tier result in faster query execution times, making your threat hunting, incident investigations, and analytics rules more responsive.
- **Compliance and retention flexibility**: Maintain comprehensive data retention for regulatory audits and forensic analysis in the Data lake tier while optimizing the Analytics tier for operational workloads. Maintaining comprehensive retention in the Data lake tier while optimizing the Analytics tier satisfies compliance requirements without sacrificing performance.
- **Scalable data management**: As your organization's data volumes grow, transformations help you maintain control over costs and performance. Apply consistent policies across tables to ensure predictable data management.

Filter and split transformations are the first steps in a larger transformation framework that empowers you to evolve your data to fit your needs. For more information about data transformation concepts, see [Custom data ingestion and transformation in Microsoft Sentinel](data-transformation).

## Prerequisites

Before you configure filter or split transformation rules, verify the following requirements:

- Your Microsoft Sentinel workspace must be onboarded to the Defender portal. For more information, see [Connect Microsoft Sentinel to the Microsoft Defender portal](/en-us/azure/sentinel/microsoft-sentinel-onboard).
- In the Microsoft Defender portal with unified role-based access control (RBAC), **Data (manage)** permissions under the **Data operations** permissions group.
- For the Microsoft Sentinel workspace, you need the **Log Analytics Contributor** role, which provides:

    - **Microsoft.OperationalInsights/workspaces/write**
    - **Microsoft.OperationalInsights/workspaces/tables/write** permissions to the Log Analytics workspace.
- To configure a split transformation:

    - [Onboard the workspace to the Microsoft Sentinel data lake](datalake/sentinel-lake-onboarding).
    - Ensure that the table is currently in the Analytics tier.

### Supported tables

Filter and split transformations have different table support requirements. Data Collection Rules (DCRs) determine how data is collected and transformed during ingestion.

- **Filtering**: Supported on any table that supports DCRs.
- **Splitting**: Supported on any table that supports Analytics only ingestion, Data lake only ingestion, and Data Collection Rules (DCRs).

To verify whether a connector's tables support DCRs, see [Find your Microsoft Sentinel data connector](data-connectors-reference).

## Filter transformations

Filter transformations enable you to reduce noise by discarding data during ingestion that isn't useful for investigations. Use a filter transformation rule to specify a KQL condition that determines which data to filter out, with the remaining data sent to the Analytics tier.

Use filter transformations when you need to:

- **Reduce noise**: Focus your SOC on actionable events by filtering out routine, low-severity logs such as "allow" events from firewall logs.
- **Optimize costs**: Lower storage and processing costs by discarding data that doesn't contribute to threat detection.
- **Improve performance**: Speed up queries and streamline analytics by reducing the volume of stored data.

Consider the following example of a filter transformation:

Your enterprise relies on firewall logs to identify anomalies. Most firewall logs are routine "allow" events with low severity that don't contribute to threat detection. To retain only critical events such as blocked traffic or high severity and filter out low-value logs, create a filter transformation rule with a KQL condition to send only medium or high severity data that isn't "allow" events to the Analytics tier.

## Split transformations

Split transformations enable you to route data between the Analytics tier and the Data lake tier based on specified conditions. Use a split transformation rule to define a KQL expression that determines which data lands in Analytics. Data that doesn't match the expression is routed to the Data lake tier only.

Note

When you configure a split transformation, data designated for the Analytics tier is also mirrored to the Data lake tier. Data that doesn't match the Analytics criteria goes to the Data lake tier only. Mirroring Analytics-tier data to the Data lake while sending nonmatching data only to the Data lake ensures that all your data remains available in the Data lake for long-term retention and compliance purposes.

Use split transformations when you need to balance cost and performance by routing data to the appropriate storage tier:

- **Optimize storage costs**: Route older or less frequently accessed logs to the Data lake tier for cost-effective long-term storage.
- **Maintain performance**: Keep recent logs in the Analytics tier for faster queries during active threat hunting.
- **Meet compliance requirements**: Retain historical logs for regulatory audits and forensic analysis without sacrificing operational agility.

Consider the following example of a split transformation:

Your enterprise ingests millions of firewall log entries daily for threat detection and compliance. Your SOC team needs real-time access to recent logs for active investigations, but must also retain historical logs for regulatory audits. Create a split transformation rule to route real-time data to the Analytics tier and historical data to the Data lake tier.

Important

Transformations you create in Microsoft Sentinel may conflict with transformations created in Azure Monitor by using DCRs. For example, if a DCR is already applied to a table to ingest only data from Region A, and a filter transformation excludes Region A, no data is ingested. Ensure you understand and check the combined effects of having a DCR and a transformation applied to a table.

## Configure filter transformation rules

Follow these steps to create a filter transformation rule:

1. In the Microsoft Defender portal, go to **Microsoft Sentinel** &gt; **Configuration** &gt; **Tables**.
2. Select a table. In the side panel, select **Filter rule**.

    [![Screenshot showing the table properties in Microsoft Sentinel.](media/transformation-filter-split/table-properties-filter.png)](media/transformation-filter-split/table-properties-filter.png#lightbox)
3. In the side panel, enter a **Rule name**.
4. In the **Condition** field, enter a KQL expression that designates which data to filter out. The KQL expression should evaluate to true for data you don't want to ingest.
5. Set the **rule status** switch to **On** to enable the filter.

    Important

    Filters filter data out. Data matching the filter condition is discarded and isn't ingested to either Analytics or Data lake tiers. Ensure your KQL expression accurately captures the data you want to exclude.
6. To add another condition, select **Add condition** and enter a new KQL expression to filter out data. Multiple conditions are combined with a logical OR, so data matching any of the conditions is filtered out.
7. Select **Save** to apply the rule.
8. Verify that the filter rule is applied by checking the **Transformation Rules** column for the table. The column displays **Filter** when a filter rule is active.

    [![Screenshot showing the filter rule applied in the table list in Microsoft Sentinel.](media/transformation-filter-split/filter-rule.png)](media/transformation-filter-split/filter-rule.png#lightbox)

## Configure a split transformation rule

Follow these steps to create a split transformation rule:

1. In the Defender portal, go to **Microsoft Sentinel** &gt; **Configuration** &gt; **Tables**.
2. Select a table and then select **Split rule**.
3. In the side panel, enter a **Rule name**.
4. In the **KQL expression** field, enter the KQL expression that defines which data to ingest to the Analytics tier. Data that doesn't match this expression is ingested to the Data lake tier.
5. Select **Save** to apply the rule.
6. Verify that the split rule is applied by checking the **Transformation Rules** column for the table. The column displays **Split** when a split rule is active.

Note

The split data ingested into the Data lake tier goes into a separate table with the same name as the original table but with an "\_SPLT" suffix. For example, if you apply a split rule to the "FirewallLogs" table, the data routed to the Data lake tier is ingested into a separate "FirewallLogs\_SPLT" table. Using a separate \_SPLT table for Data lake data lets you manage retention and access policies separately for Analytics and Data lake tiers.

[![Screenshot showing the split rule applied in the table list in Microsoft Sentinel.](media/transformation-filter-split/split-rule.png)](media/transformation-filter-split/split-rule.png#lightbox)

### Configure retention for split tables

After creating a split rule, configure retention settings for each tier:

1. Under the original table, view the resulting **Analytics** and **Data lake** split tables.
2. To configure retention, select the Analytics or Data lake table.
3. Select **Data retention settings**.
4. Configure the retention period and save.

Alternatively, select the original table and configure both Analytics and Data lake retention from the combined **Data retention settings** dialog.

[![Screenshot showing the retention settings for split tables in Microsoft Sentinel.](media/transformation-filter-split/split-table-retention-settings.png)](media/transformation-filter-split/split-table-retention-settings.png#lightbox)

### Manage rules

To manage existing rules, select the table and then select either **Split rule** or **Filter rule** depending on the rule type you want to manage.

- To disable a rule, select the **Rule status** switch to turn off the rule, and then select **Save**.
- To delete a rule, note that deleting a transformation rule immediately stops data processing for that rule and can affect active ingestion. To proceed, select **Delete**.

Verify rules by running KQL queries to confirm that data is ingested correctly and routed to the correct tier.

## Known limitations

Be aware of the following limitations when using filter and split transformations:

- **XDR table visibility**: Split and filter transformations applied to XDR tables don't appear in Advanced Hunting for the first 30 days of data. The transformations are applied, and once data ages beyond the first 30 days, it behaves normally in Advanced Hunting. Data queried from Log Analytics or Microsoft Sentinel reflects the cost savings immediately.
- **Propagation delay**: Transformations can take up to one hour to take effect.
- **Table support**: Only tables that support Data Collection Rules (DCRs) support split and filter transformations.