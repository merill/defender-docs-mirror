---
layout: Conceptual
title: Advanced hunting overview in Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-overview
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about advanced hunting queries in Microsoft Defender and how to use them to proactively find threats and weaknesses in your network.
ms.service: defender-xdr
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- m365initiative-m365-defender
- tier1
ms.custom:
- cx-ti
- cx-ah
- seo-marvel-apr2020
- msecd-doc-authoring-1015
ms.topic: overview
ms.date: 2026-08-07T00:00:00.0000000Z
locale: en-us
document_id: 24fc4809-527a-f593-b08e-7e5c3ce3a137
document_version_independent_id: 24fc4809-527a-f593-b08e-7e5c3ce3a137
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-overview.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 7b9bc1d5-b45e-e7a1-b631-ac2cbe525251
---

# Advanced hunting overview in Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn

Advanced hunting is a query-based threat hunting tool that you use to explore up to 30 days of raw Defender XDR data. When you onboard a Microsoft Sentinel workspace, you can also query analytics-tier data according to the retention configured for the workspace. You can proactively inspect events in your network to locate threat indicators and entities. The flexible access to data enables unconstrained hunting for both known and potential threats.

Advanced hunting supports two modes: guided and advanced. Use [guided mode](advanced-hunting-query-builder) if you're not yet familiar with Kusto Query Language (KQL) or if you prefer the convenience of a query builder. Use [advanced mode](advanced-hunting-query-language) if you're comfortable using KQL to create queries from scratch.

**To start hunting, see [Choose between guided and advanced modes to hunt in the Microsoft Defender portal](advanced-hunting-modes).**

You can use the same threat hunting queries to build custom detection rules. These rules run automatically to check for and then respond to suspected breach activity, misconfigured machines, and other findings.

Advanced hunting supports queries that check a broader data set coming from:

- Microsoft Defender for Endpoint
- Microsoft Defender for Office 365
- Microsoft Defender for Cloud Apps
- Microsoft Defender for Identity
- Microsoft Sentinel

To use advanced hunting, [turn on Microsoft Defender XDR](m365d-enable). To use advanced hunting with Microsoft Sentinel, [connect Microsoft Sentinel to the Defender portal](/en-us/azure/sentinel/microsoft-sentinel-onboard).

For more information on advanced hunting in Microsoft Defender for Cloud Apps data, see [Advanced hunting in Defender for Cloud Apps (video)](https://learn-video.azurefd.net/vod/player?id=ffdedc73-6edf-45a9-8c90-566296e8d4ec).

## Get access

You need to be assigned permissions before you can run advanced hunting queries. You have the following options:

- [Microsoft Defender XDR Unified role based access control (URBAC)](manage-rbac):

    - **Advanced Hunting access (Email & Collaboration tables)**: Membership assigned with the **Security operations** &gt; **Raw data** &gt; **Email & collaboration metadata (read)**URBAC permission. This permission provides access to:
        - **EmailEvents**
        - **EmailUrlInfo**
        - **EmailAttachmentInfo**
        - **EmailPostDeliveryEvents**
        - **CampaignInfo**
        - **FileMaliciousContentInfo**
        - **MessageEvents**
        - **MessagePostDeliveryEvents**
        - **MessageUrlInfo**
        - **UrlClickEvents**
        - **Email entity metadata**
    - **Advanced Hunting access (Alerts & behaviors tables)**: Membership assigned with the **Security operations** &gt; **Security data** &gt; **Security data basics (read)** URBAC permission. This permission provides access to the *Alerts & behaviors* schema, but not the *Email & collaboration* schema.
- [Email & collaboration permissions in the Microsoft Defender portal](/en-us/defender-office-365/mdo-portal-permissions): Membership in one of the following Email & Collaboration role groups provides access to email data tables in advanced hunting:

    - **Security Administrator**
    - **Security Operator**
    - **Security Reader**
- [Exchange Online permissions](/en-us/exchange/permissions-exo/permissions-exo): To access Exchange Online data surfaced in advanced hunting, users must be members of one of the following Exchange Online role groups:

    - **View-Only Organization Management**
    - **View-Only Configuration**
    - **Security Reader**
    - **Global Reader**
- [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): Membership in one of the following Microsoft Entra roles grants full read access to all advanced hunting data:

    - **Global Administrator**
    - **Security Administrator**
    - **Security Reader**
    - **Global Reader**

    Your access to endpoint data is determined by role-based access control (RBAC) settings in Microsoft Defender for Endpoint. For more information, see [Manage access to Microsoft Defender with Microsoft Entra global roles](m365d-permissions).

## Data freshness and update frequency

Advanced hunting data falls into two distinct types, each with a different consolidation process.

### Event or activity data

Event or activity data populates tables about alerts, security events, system events, and routine assessments. Advanced hunting receives this data almost immediately after the sensors that collect them successfully transmit it to the corresponding cloud services. For example, you can query event data from healthy sensors on workstations or domain controllers almost immediately after they're available on Microsoft Defender for Endpoint and Microsoft Defender for Identity.

To collect even more event properties, you can turn on [aggregated reporting](/en-us/defender-endpoint/aggregated-reporting).

### Entity data

Entity data populates tables with information about users and devices. Entity data comes from relatively static sources like Active Directory entries and dynamic sources like event logs. To provide fresh data, tables are updated every hour with a record that contains the latest, most comprehensive data set about each entity, including health status and tags.

## Quotas and usage parameters

To keep the service performant and responsive, advanced hunting sets various quotas and usage parameters (also known as "service limits"). These quotas and parameters apply separately to queries run manually and to queries run using [custom detection rules](custom-detection-rules). Be mindful of these limits if you regularly run multiple queries. [Apply optimization best practices](advanced-hunting-best-practices) to minimize disruptions.

The following table describes the available quotas and usage parameters.

| Quota or parameter | Size | Refresh cycle | Description |
| --- | --- | --- | --- |
| Date range | 30 days for native Defender XDR data. Microsoft Sentinel table retention depends on the configured analytics-tier retention. | Every query | Each query can look up native Defender XDR data from up to the past 30 days. When you onboard a Microsoft Sentinel workspace, the available date range for its tables depends on the configured analytics-tier retention. |
| Result set | 100,000 rows | Every query | Each query can return up to 100,000 records. |
| Timeout | 10 minutes | Every query | Each query can run for up to 10 minutes. If it doesn't complete within 10 minutes, the service displays an error. |
| CPU resources | Based on tenant size | Every 15 minutes | The portal displays a warning whenever a query runs and the tenant consumes over 10% of allocated resources. [Queries are blocked](advanced-hunting-errors) if the tenant reaches 100% until after the next 15-minute cycle. |
| Results size limit | 64 MB | Every query | The limit for overall size of the results data, which doesn't just refer to the number of records. Factors such as the number of columns, data types, and field lengths also contribute to the result size.If the query result exceeds the 64-MB size limit, the portal returns the maximum number of records it can within this limit and displays a message indicating that the displayed results are partial due to size constraints. |

In the unified Microsoft Defender portal, you can run queries over Microsoft Sentinel tables by onboarding a workspace. [Log Analytics workspace limits](/en-us/azure/azure-monitor/service-limits#log-analytics-workspaces) and the configured analytics-tier retention therefore also apply. Data stored exclusively in the Microsoft Sentinel data lake isn't available in advanced hunting. Use [data lake exploration](/en-us/azure/sentinel/datalake/sentinel-mcp-data-exploration-tool) to query that data.

For advanced hunting in multitenant organizations, see [Quotas in advanced hunting in multitenant management](/en-us/defender-xdr/mto-advanced-hunting#quotas).

Note

A separate set of quotas and parameters apply to advanced hunting queries performed through the API. [Read about advanced hunting APIs](api-advanced-hunting).

## Time zone

### Queries

Advanced hunting uses UTC (Coordinated Universal Time) for all data.

![Screenshot of the custom time range option in advanced hunting query settings.](media/advanced-hunting-overview/custom-time-range.png)

Write queries in UTC.

### Results

Microsoft Defender converts advanced hunting results to the [timezone](m365d-time-zone) you set.

## Extend data retention

To retain supported Defender XDR hunting tables for more than 30 days, onboard a Microsoft Sentinel workspace and configure the tables' analytics-tier retention. For more information, see [Configure table settings in Microsoft Sentinel](/en-us/azure/sentinel/manage-table-tiers-retention).

You can also stream Defender XDR data to external services for longer retention. For more information, see:

- Microsoft Defender [Streaming API](/en-us/defender-xdr/streaming-api)
- Microsoft Defender for Endpoint [Raw Data Streaming API](/en-us/defender-endpoint/api/raw-data-export)

Note

Data retention starts from the first day that you implement and enable the streaming API.