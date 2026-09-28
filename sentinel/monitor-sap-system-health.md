---
layout: Conceptual
title: Monitor the health of the connection between Microsoft Sentinel and your SAP system | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/monitor-sap-system-health
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
description: Use the SAP connector page and a dedicated alert rule template to keep track of your SAP systems' connectivity and performance.
ms.author: monaberdugo
author: mberdugo
ms.reviewer: mapankra
ms.topic: how-to
ms.date: 2026-08-04T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 7e21816f-6c23-5c40-70bd-0c0a2baf0619
document_version_independent_id: 5d2adeb4-8348-643f-99a7-c5d1e5fd3f13
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/monitor-sap-system-health.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/monitor-sap-system-health
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/monitor-sap-system-health.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
platformId: 5a7bf2c3-c907-28e0-2483-bbe3eb250f68
---

# Monitor the health of the connection between Microsoft Sentinel and your SAP system | Microsoft Learn

After you [deploy the SAP solution](sap/deployment-overview), you want to ensure proper functioning and performance of your SAP systems, and keep track of system role, connectivity, and log ingestion. This article describes how to look up system role and health from workspace tables and functions, and how to use a dedicated alert rule template to monitor the health of your SAP systems.

## Prerequisites

Before you can perform the procedures in this article, you need to have an SAP data connector connected to your SAP system. SAP logs aren't displayed in the Microsoft Sentinel **Logs** page until your SAP system is connected and data starts streaming into Microsoft Sentinel. For more information, see [Connect your SAP system to Microsoft Sentinel](sap/deploy-data-connector-agentless).

## Check your SAP data connector's health and connectivity

The agentless data connector page lists the SAP systems (SIDs) you configured, but system role and health are no longer surfaced there as a table. Query them from the workspace instead:

- **System role (production or nonproduction)**. Use the [SAPSystems](sap/sap-solution-function-reference#sapsystems) KQL function, which reads the *SAP - Systems* watchlist and returns the `SystemRole` value for each SID. Role also affects billing - see [Solution pricing](sap/sap-applications-overview#solution-pricing). Typical values include:

    | Value | Description |
    | --- | --- |
    | **Production** | The system is defined by the SAP admin as a production system. |
    | **Non-production** | Roles such as development, test, quality assurance, or training. |
    | *(empty or missing)* | The *SAP - Systems* watchlist isn't populated for the SID yet, or the ABAP user can't read the T000 table. Microsoft Sentinel treats an unknown SID as production for security and billing purposes. Populate the watchlist and validate the role permissions on `T000`. |
- **Health**. Query the **SentinelHealth** table for the SAP data connector, or turn on the *SAP - Data collection health check* alert rule template (see the next sections). Typical signals include:

    | Value | Description |
    | --- | --- |
    | **Success** | Microsoft Sentinel identified both logs and a heartbeat from the system. |
    | **Success with warnings** | Connection succeeded, but some log streams returned errors or the ABAP user is missing authorizations. Check the Microsoft Sentinel role definitions on the SAP system, including read access to `T000`. |
    | **Failure** | Microsoft Sentinel can't reach the SAP system or the credentials are invalid. Review the [troubleshooting steps](sap/sap-deploy-troubleshoot). |

## View SAP logs streaming into Microsoft Sentinel

The agentless data connector streams SAP logs into standard Log Analytics tables such as `ABAPAuditLog`, `ABAPAuthorizationDetails`, `ABAPChangeDocsLog`, and `ABAPUserDetails`. Query them from Microsoft Sentinel **Logs** (Azure portal) or from **Advanced hunting** (Defender portal). For example, run `ABAPAuditLog | take 50` to confirm that data is arriving.

For the full list of tables and the recommended KQL functions to query them, see [Log and table reference for the Microsoft Sentinel solution for SAP applications](sap-solution-log-reference).

## Check the SentinelHealth table for health indicators

The **SentinelHealth** table in Microsoft Sentinel contains health indicators for the SAP data connector, among others. You can query this table to get a summary of the health of your SAP systems.

For more information, see:

- [Auditing and health monitoring in Microsoft Sentinel](health-audit)
- [Turn on auditing and health monitoring for Microsoft Sentinel (preview)](enable-monitoring)
- [Monitor the health of your data connectors](monitor-data-connector-health)
- [Microsoft Sentinel health tables reference](health-table-reference)

## Use an alert rule template to monitor the health of your SAP systems

The Microsoft Sentinel for SAP solution includes an alert rule template designed to give you insight into the health of the SAP data collection.

The rule needs at least seven days of loading history to detect the different seasonality patterns. We recommend a value of 14 days for the alert rule **Look back** parameter to allow detection of weekly activity profiles.

Once the alert rule is activated, it judges the recent telemetry and log volume observed on the workspace according to the history learned. The rule then alerts on potential issues, dynamically assigning severities according to the scope of the problem.

To turn on the analytics rule in Microsoft Sentinel, select **Analytics &gt; Rule templates**, and locate the *SAP - Data collection health check* alert rule.

The analytics rule does the following:

- Evaluates the connector's health signals.
- Evaluates telemetry data.
- Evaluates alerts on log continuation and other system connectivity issues, if any are found.
- Learns the log ingestion history, and therefore works better with time.

The following screenshot shows an example of an alert generated by the *SAP - Data collection health check* alert rule:

![Screenshot of an alert triggered by the SAP - Data collection health check alert rule.](media/monitor-sap-system-health/alert-rule-example.png)