---
layout: Conceptual
title: Collect SAP HANA audit logs in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/sap/collect-sap-hana-audit-logs
breadcrumb_path: ../breadcrumb/toc.json
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
ms.reviewer: mapankra
description: Learn how to ingest SAP HANA audit logs into Microsoft Sentinel for customer-managed environments, with guidance relevant to security, infrastructure, and SAP BASIS teams.
ms.author: monaberdugo
author: mberdugo
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: bdb82d26-8c09-004e-316b-0f5624803962
document_version_independent_id: 1036d0bb-0a72-aabc-c4b5-3897f634c4b0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/sap/collect-sap-hana-audit-logs.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/sap/collect-sap-hana-audit-logs
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/sap/collect-sap-hana-audit-logs.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 85ad90f6-d6e4-7cc8-b39d-361cef01ba74
---

# Collect SAP HANA audit logs in Microsoft Sentinel | Microsoft Learn

This article explains how to collect audit logs from your SAP HANA database in customer managed environments.

Content in this article is intended for your **security**, **infrastructure**, and **SAP BASIS** teams.

Important

Microsoft Sentinel SAP HANA support is currently in PREVIEW. The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

Important

For environments managed by SAP such as SAP RISE (S/4HANA Cloud, private edition), SAP HANA database audit logs are collected by SAP using the service **SAP LogServ** only. It integrates with Microsoft Sentinel for SAP applications natively re-using the built-in analytic rules. Learn more from the [Blog Series: SAP LogServ Integration with Microsoft Sentinel](https://community.sap.com/t5/enterprise-resource-planning-blog-posts-by-members/ultimate-blog-series-sap-logserv-integration-with-microsoft-sentinel/ba-p/14126401)

## Prerequisites

SAP HANA logs are sent over Syslog. Make sure that your Azure Monitor Agent is configured to collect Syslog files. For more information, see [Ingest syslog and CEF messages to Microsoft Sentinel with the Azure Monitor Agent](../connect-cef-syslog-ama).

## Collect SAP HANA audit logs

Perform the following steps to configure SAP HANA audit log collection.

1. Make sure that the SAP HANA audit log trail is configured to use Syslog, as described in *SAP Note 0002624117*, which is accessible from the [SAP Launchpad support site](https://launchpad.support.sap.com/#/notes/0002624117). For more information, see:

    - [SAP HANA Audit Trail - Best Practice](https://help.sap.com/docs/SAP_HANA_PLATFORM/b3ee5778bc2e4a089d3299b82ec762a7/35eb4e567d53456088755b8131b7ed1d.html)
    - [Recommendations for Auditing](https://help.sap.com/docs/SAP_HANA_PLATFORM/742945a940f240f4a2a0e39f93d3e2d4/5c34ecd355e44aa9af3b3e6de4bbf5c1.html)
    - [Actions Audited by Default Audit Policy](https://help.sap.com/docs/SAP_HANA_PLATFORM/b3ee5778bc2e4a089d3299b82ec762a7/4f7cde1125084ea3b8206038530e96ce.html)
2. Check your operating system Syslog files for any relevant HANA database events.
3. Sign into your HANA database operating system as a user with sudo privileges.
4. Install an agent on your machine and confirm that your machine is connected. For more information, see [Install and manage Azure Monitor Agent](/en-us/azure/azure-monitor/agents/azure-monitor-agent-manage?tabs=azure-portal).
5. Configure your agent to collect Syslog data. For more information, see [Collect Syslog events with Azure Monitor Agent](/en-us/azure/azure-monitor/agents/data-collection-syslog).

    Tip

    Because the facilities where HANA database events are saved can change between different distributions, we recommend that you add all facilities. Check them against your Syslog logs, and then remove any that aren't relevant.

## Verify your configuration

Use the following steps in both Microsoft Sentinel and your SAP HANA database to verify that your system is configured as expected.

### Verify the configuration in Microsoft Sentinel

In Microsoft Sentinel's **Logs** page, check to confirm that HANA database events are now shown in the ingested logs. For example, run the following query. This Kusto function template defines the schema and union logic for querying a custom Syslog table:

```Kusto
//generated function structure for custom log Syslog
// generated on 2024-05-07
let D_Syslog = datatable(TimeGenerated:datetime
,EventTime:datetime
,Facility:string
,HostName:string
,SeverityLevel:string
,ProcessID:int
,HostIP:string
,ProcessName:string
,Type:string
)['1000-01-01T00:00:00Z', '1000-01-01T00:00:00Z', 'initialString', 'initialString', 'initialString', 'initialString',1,'initialString', 'initialString', 'initialString'];

let T_Syslog = (Syslog | project
TimeGenerated = column_ifexists('TimeGenerated', '1000-01-01T00:00:00Z')
,EventTime = column_ifexists('EventTime', '1000-01-01T00:00:00Z')
,Facility = column_ifexists('Facility', 'initialString')
,HostName = column_ifexists('HostName', 'initialString')
,SeverityLevel = column_ifexists('SeverityLevel', 'initialString')
,ProcessID = column_ifexists('ProcessID', 1)
,HostIP = column_ifexists('HostIP', 'initialString')
,ProcessName = column_ifexists('ProcessName', 'initialString')
,Type = column_ifexists('Type', 'initialString')
);
T_Syslog | union isfuzzy= true (D_Syslog | where TimeGenerated != '1000-01-01T00:00:00Z')
```

See more information on the Kusto operators and functions used in the sample query, in the Kusto documentation:

- [***let*** statement](/en-us/kusto/query/let-statement?view=microsoft-sentinel&amp;preserve-view=true)
- [***datatable*** operator](/en-us/kusto/query/datatable-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***where*** operator](/en-us/kusto/query/where-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***project*** operator](/en-us/kusto/query/project-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***union*** operator](/en-us/kusto/query/union-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***column\_ifexists()*** function](/en-us/kusto/query/column-ifexists-function?view=microsoft-sentinel&amp;preserve-view=true)

For more information on KQL, see [Kusto Query Language (KQL) overview](/en-us/kusto/query/?view=microsoft-sentinel&amp;preserve-view=true).

Other resources:

- [KQL quick reference](/en-us/kusto/query/kql-quick-reference?view=microsoft-sentinel&amp;preserve-view=true)
- [Kusto Query Language learning resources](/en-us/kusto/query/kql-learning-resources?view=microsoft-sentinel&amp;preserve-view=true)

### Verify the configuration in SAP HANA

In your SAP HANA database, check your configured audit policies. For more information on the required SQL statements, see [SAP Note 3016478](https://me.sap.com/notes/3016478/E).

## Add analytics rules for SAP HANA in Microsoft Sentinel

Use the following built-in analytics rules to have Microsoft Sentinel start triggering alerts on related SAP HANA activity:

- **SAP - (PREVIEW) HANA DB -Assign Admin Authorizations**
- **SAP - (PREVIEW) HANA DB -Audit Trail Policy Changes**
- **SAP - (PREVIEW) HANA DB -Deactivation of Audit Trail**
- **SAP - (PREVIEW) HANA DB -User Admin actions**

For more information, see [Microsoft Sentinel solution for SAP applications: security content reference](sap-solution-security-content).