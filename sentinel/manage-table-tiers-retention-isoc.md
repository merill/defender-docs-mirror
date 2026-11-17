---
layout: Conceptual
title: Manage tables, tiers, and retention in ISOC | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/manage-table-tiers-retention-isoc
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
description: Review ISOC data ingestion, retention, and billing, and configure table retention and data tier settings in the Microsoft Defender portal.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: how-to
ms.date: 2026-11-13T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 6fe7ce50-1d91-c3f4-a8bb-67653435110a
document_version_independent_id: 8de438ef-51c0-6790-3048-829ea80eb65b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/manage-table-tiers-retention-isoc.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/manage-table-tiers-retention-isoc
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/manage-table-tiers-retention-isoc.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 2228f8ba-fcec-a86e-fea2-54ab22708957
---

# Manage tables, tiers, and retention in ISOC | Microsoft Learn

Integrated Security Operations Center (ISOC) in Microsoft Defender supports Microsoft security data and additional Microsoft and non-Microsoft security data.

## How data is handled

Native Microsoft Defender data is available directly in the Microsoft Defender experience and doesn't need to be separately ingested into an ISOC workspace.

Other supported Microsoft and non-Microsoft data can be connected through an ISOC workspace by using [data connectors](/en-us/azure/sentinel/connect-data-sources?tabs=defender-portal).

## Microsoft security data

ISOC supports Microsoft security data from the following sources:

- Microsoft Defender for Endpoint
- Microsoft Defender for Office 365
- Microsoft Defender for Identity
- Microsoft Defender for Cloud Apps
- Microsoft Defender for Cloud
- Microsoft Entra
- Azure Activity through a connector
- Office 365 Activity through a connector

Eligible customers with Microsoft Defender Suite, Microsoft 365 E5, or Microsoft 365 E7 can use supported Microsoft Defender security data as part of the ISOC experience.

For Microsoft 365 E5 plan details and pricing, see [Microsoft 365 E5 for Enterprise](https://www.microsoft.com/microsoft-365/enterprise/e5#Pricing).

To compare the security capabilities included with Microsoft 365 enterprise plans, see [Microsoft 365 Security Enterprise Plans](https://www.microsoft.com/security/pricing/enterprise-plans).

### 90-day retention

Starting November 15, 2026, eligible customers receive up to 90 days of included retention for supported Microsoft Defender data, Azure Activity data, and Office 365 Activity data at no additional charge.

The retention benefit applies at the workload level, except for the tables listed in Retention exceptions. As additional supported tables become available for an included workload, they're also included in the retention benefit unless otherwise noted.

The following tables and data sources are currently included:

- **Alerts**

    - `AlertEvidence`
    - `AlertInfo`
- **Azure Activity**
- **Behaviors**

    - `BehaviorEntities`
    - `BehaviorInfo`
- **Microsoft Defender for Cloud**

    - `BehaviorInfo`
    - `BehaviorEntities`
    - `CloudStorageEvents`
    - `CloudStorageAggregatedEventsV2`
    - `CloudPolicyEnforcementEvents`
    - `CloudKeyVaultEvents`
    - `CloudKeyVaultRawEvents`
    - `CloudHttpIncomingEvents`
    - `CloudProcessEvents`
    - `CloudStorageAggregatedEvents`
    - `CloudAuditEvents`
    - `CloudDnsEvents`
- **Microsoft Defender for Cloud Apps**

    - `CloudAppEvents`
    - `OAuthAppInfo`
- **Microsoft Defender for Endpoint**

    - `DeviceEvents`
    - `DeviceFileCertificateInfo`
    - `DeviceFileEvents`
    - `DeviceImageLoadEvents`
    - `DeviceInfo`
    - `DeviceLogonEvents`
    - `DeviceNetworkEvents`
    - `DeviceNetworkInfo`
    - `DeviceProcessEvents`
    - `DeviceRegistryEvents`
    - `DisruptionAndResponseEvents`
- **Microsoft Defender for Identity**

    - `IdentityDirectoryEvents`
    - `IdentityEvents`
    - `IdentityLogonEvents`
    - `IdentityQueryEvents`
- **Microsoft Defender for Office 365**

    - `CallActivityEvents`
    - `CampaignInfo`
    - `EmailAttachmentInfo`
    - `EmailEvents`
    - `EmailPostDeliveryEvents`
    - `EmailUrlInfo`
    - `FileMaliciousContentInfo`
    - `MessageEvents`
    - `MessagePostDeliveryEvents`
    - `MessageUrlInfo`
    - `UrlClickEvents`
- **Microsoft Entra**

    - `EntraIdDirectoryAuditEvents`
    - `EntraIdSignInEvents`
    - `EntraIdSpnSignInEvents`
    - `GraphAPIAuditEvents`
- **Office 365 Activity**

### Extend Microsoft Defender data retention

When you enable streaming for supported Microsoft Defender data, the retention period starts at 180 days.

Extended retention applies to new data after you enable it. Data that was collected before you enabled extended retention isn't backfilled.

Additional charges apply when you extend retention beyond the retention included with ISOC.

### Retention exceptions

The following tables don't receive the 90-day included retention benefit. They're stored in XDR for 30 days. As with other supported tables, extended retention starts at 180 days.

| Table | Retention in XDR | Extended retention starts at |
| --- | --- | --- |
| `AgentsInfo` | 30 days. | 180 days. |
| `IdentityAccountInfo` | 30 days. | 180 days. |

## Additional Microsoft and non-Microsoft security data

An ISOC workspace is required to ingest additional Microsoft and non-Microsoft security data through [more than 500 data connectors](/en-us/azure/sentinel/data-connectors-reference).

Additional Microsoft and non-Microsoft security data is billed separately from the Microsoft security data included with the ISOC benefit. Ingested data can be retained for up to 90 days as part of the ISOC ingestion experience.

Additional ingestion and retention charges might apply depending on the data you ingest and how long you retain it.

## How data tiers and retention work

You can retain data in one of two tiers:

- **Analytics tier**: This tier makes data available for alerting, hunting, workbooks, and more. It retains data in two states:

    - **Analytics retention**: In this "hot" state, data is fully available for real-time analytics, including high-performance queries, analytics rules, and threat hunting. By default, supported Microsoft Defender XDR tables retain data in this tier for 90 days, except for the tables listed in Retention exceptions. You can extend the retention period of supported tables at a prorated monthly long-term retention charge.
    - **Total retention**: By default, all data in the analytics tier is mirrored to the data lake for the same retention period. You can extend the retention of your data in the lake beyond the analytics retention, for up to 12 years of total retention at a low cost.
- **Data Lake tier**: In this low-cost "cold" tier, ISOC retains your data in the data lake only. Data in the Data Lake tier isn't available for real-time analytics features and threat hunting. However, you can access data in the lake whenever you need it through [KQL jobs](datalake/kql-jobs), analyze trends over time by running scheduled KQL or Spark jobs, and aggregate insights from incoming data at a regular cadence by using summary rules.
- **XDR data**: Except for the tables listed in Retention exceptions, supported Microsoft Defender XDR threat hunting data is available in the Analytics tier for 90 days by default. Extending retention beyond 90 days in the Analytics tier incurs ingestion and storage costs. You can also ingest exclusively into the Data Lake tier, but supported data remains available in the Analytics tier for its included retention period. Ingesting XDR data directly into the Data Lake tier is more cost-effective, but it involves ingestion, storage, and processing costs.

For more information about the differences between the Analytics tier and the Data Lake tier, see Compare the analytics and data lake tiers.

For more information about the Microsoft Sentinel data lake, see [What is Microsoft Sentinel data lake](datalake/sentinel-lake-overview).

## Compare the analytics and data lake tiers

This table compares the Analytics and Data Lake tiers and their key characteristics:

| Comparison | Analytics tier | Data Lake tier |
| --- | --- | --- |
| Key characteristics | High-performance querying and indexing for logs (also known as hot, or interactive retention). | Cost-effective long-term retention of large data volumes (also known as cold storage). |
| Best for | Real-time analytics rules, alerting, hunting, workbooks, and all Microsoft Sentinel features. | - Compliance and regulatory logging.- Historical trend analysis and forensics.- Low-touch data that's not needed for real-time alerts. |
| Ingestion cost | Standard | Minimal |
| Query price included | ✅ | ❌ |
| Optimized query performance | ✅ | ❌ Slower queries.Good for auditing. Not optimized for real-time analysis. |
| Query capabilities | [Full query capabilities](/en-us/azure/azure-monitor/logs/get-started-queries) in the Microsoft Defender portal, the Azure portal, and by using APIs. | - [Full query capabilities](/en-us/azure/azure-monitor/logs/get-started-queries), including unions and joins.- Run scheduled KQL or Spark jobs.- Use notebooks. |
| Full set of real-time analytics features | ✅ | ❌ Limitations on some features, including analytics rules, hunting queries, parsers, watchlists, workbooks, and playbooks. |
| [Search jobs](investigate-large-datasets) | ✅ | ✅ |
| [Summary rules](summary-rules) | ✅ | ✅ [Full KQL on a single table](/en-us/azure/azure-monitor/logs/basic-logs-query), which you can extend with data from an analytics table using [lookup](/en-us/azure/data-explorer/kusto/query/lookup-operator) |
| [Restore](restore) | ✅ | ❌ KQL and Notebook jobs can promote data to the analytics tier. |
| [Data export](/en-us/azure/azure-monitor/logs/logs-data-export) | ✅ | ❌ |
| Retention period | 90 days for Microsoft Sentinel and supported Microsoft Defender XDR tables, subject to Retention exceptions.You can extend retention for supported tables at a prorated monthly long-term retention charge. | Same as analytics retention, by default. Can be extended to up to 12 years. |

## What happens when you modify table settings

You can switch a table's tier and retention settings at any time.

When you change a table's tier from Analytics to Data Lake, all real-time analytics and hunting queries stop working.

When you shorten a table's total retention, Microsoft waits 30 days before removing the data, so you can revert the change and avoid data loss if you made a configuration error.

When you increase total retention, the new retention period applies to all data that was already ingested into the table and wasn't yet removed.

When you change the analytics retention settings of a table with existing data, the change takes effect immediately.

***Example***:

- You have a table in the Analytics tier with 180 days of analytics retention. By default, total retention is also set to 180 days.
- You change analytics retention to 90 days without changing total retention, which remains 180 days.
- ISOC automatically removes the last 90 days of data from analytics retention, but continues to store data that's 90-180 days old in the Data Lake tier.

## Manage table settings

To configure table retention and tier settings in the Microsoft Defender portal, follow these steps:

1. Select **Setup & Configuration** &gt; **Data management** &gt; **Data & connectors** from the left navigation pane.

    The **Tables** page lists all the tables you can manage in the Microsoft Defender portal and each table's current settings.
2. Select a table on the **Tables** screen.

    Selecting a table opens the table details side panel with more information about the table, including data sources, table description, tier, and retention details.

    [![Screenshot that shows the table details side panel for the CommonSecurityLog table, including data sources, on the Table Management screen in the Defender portal.](media/manage-data-overview/table-management-microsoft-defender-portal.png)](media/manage-data-overview/table-management-microsoft-defender-portal.png#lightbox)
3. Select **Manage table**.

    The **Manage table** screen lets you modify retention settings in the current tier and change the storage tier, if necessary.

    Available settings depend on the table. Review the options and warnings shown for the selected table rather than assuming that every table supports the full ranges listed here.

    [![Screenshot that shows the Manage table screen for the CommonSecurityLog table in the Defender portal.](media/manage-data-overview/manage-table-settings-microsoft-defender-portal.png)](media/manage-data-overview/manage-table-settings-microsoft-defender-portal.png#lightbox)

    - **Analytics tier retention settings**:

        - **Analytics retention**: Select a retention period from the available values for the table.
        - **Total retention**: Set a value up to 12 years of long-term storage in the Data Lake.
    - **Data Lake tier**: Set **Retention** to a value between 30 days and 12 years. Selecting **Data Lake tier** stores data exclusively in the Data Lake.
    - **Tier changes**: If necessary, you can change tiers at any time based on your cost management and data usage needs.

        Important

        Tier changes aren't available for all tables. For example, some tables must remain in the Analytics tier because Microsoft security services require the data in these tables for near-real-time analytics.

    For more information about retention and tier settings, see How data tiers and retention work.
4. Review warnings and messages. These messages help you understand important implications of changing table settings.

    Examples include:

    - Increased retention is likely to increase data cost.
    - Changing from the Analytics tier to the Data Lake tier causes features that rely on Analytics data to stop functioning, such as:
        - Alerting
        - Advanced hunting
        - Analytics rules
        - Custom detection rules
5. Select **Save** to apply the new settings.

## Retention pricing

When you change a table's retention settings in **Manage table**, you might see an estimated retention price. This price shows the cost of retaining 1 GB of ingested data for the full selected retention period.

The estimate includes the components described below, not your total data cost.

The components depend on the tier you ingest data into and the type of data, as described in the following sections. The examples use illustrative rates in US dollars (USD).

Data Lake storage is charged per GB per month, based on a uniform data compression rate of 6:1. For example, 600 GB of raw data is billed as 100 GB of compressed data. For each 1 GB of ingested data, storage charges therefore apply to 1/6 GB.

### Analytics tier

The estimate can include two components:

- **Extended analytics retention**: A charge for extending analytics retention, based on the type of data.
- **Data Lake storage**: A charge for keeping data in the data lake after its analytics retention period ends.

For example, 180 days of analytics retention and 270 days of total retention adds 90 days, or three months, of Data Lake storage charges. There's no separate Data Lake ingestion or processing charge.

#### Microsoft Defender XDR data

For supported Microsoft Defender XDR tables with 90 days of included retention, the minimum extended analytics retention period is 180 days. A per-GB charge covers the first 180 days. Analytics retention beyond 180 days is charged per GB per month.

**Example:** You retain data for 180 days in the Analytics tier and 270 days in total.

Assume an analytics retention charge of $1.20 per GB and a Data Lake storage rate of $0.026 per GB per month.

- Analytics retention for the first 180 days: $1.20 per GB.
- Data Lake storage for the remaining 90 days: 3 × 1/6 × $0.026 = $0.013 per GB.

The estimated retention price is $1.20 + $0.013 = **$1.213 per GB**.

**Example:** You retain data for 270 days in the Analytics tier, with the same total retention period.

Assume a charge of $1.20 per GB for the first 180 days and an analytics retention rate of $0.10 per GB per month beyond 180 days.

The additional 90 days cost 3 × $0.10 = $0.30 per GB. The estimated retention price is $1.20 + $0.30 = **$1.50 per GB**. There's no additional Data Lake storage charge because total retention equals analytics retention.

#### Additional Microsoft and non-Microsoft security data

Analytics retention beyond the included 90 days is charged per GB per month. The estimate shows the added retention cost. Existing Analytics tier ingestion charges are separate and aren't included.

**Example:** You retain data for 180 days in the Analytics tier and 270 days in total.

Assume an analytics retention rate of $0.10 per GB per month and a Data Lake storage rate of $0.026 per GB per month.

- Analytics retention beyond the included 90 days: 3 × $0.10 = $0.30 per GB.
- Data Lake storage for the remaining 90 days: 3 × 1/6 × $0.026 = $0.013 per GB.

The estimated added retention price is $0.30 + $0.013 = **$0.313 per GB**.

### Data Lake tier

When you ingest Microsoft Defender XDR data or additional Microsoft and non-Microsoft security data directly into the Data Lake tier, the estimate combines three components:

- **Ingestion**: A per-GB charge for ingesting the data.
- **Processing**: A per-GB charge for processing the ingested data.
- **Data Lake storage**: A charge per GB per month for the selected retention period.

**Example:** You ingest data directly into the Data Lake tier and retain it for 180 days, or six months.

Assume rates of $0.05 per GB for ingestion, $0.10 per GB for processing, and $0.026 per GB per month for storage.

- Ingestion: $0.05 per GB.
- Processing: $0.10 per GB.
- Data Lake storage for six months: 6 × 1/6 × $0.026 = $0.026 per GB.

The estimated retention price is $0.05 + $0.10 + $0.026 = **$0.176 per GB**.