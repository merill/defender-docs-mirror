---
layout: Conceptual
title: Manage your SOC Better with Incident Metrics in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/manage-soc-with-incident-metrics
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
description: Use information from the Microsoft Sentinel incident metrics screen and workbook to help you manage your Security Operations Center (SOC).
ms.author: guywild
author: guywi-ms
ms.reviewer: idpelleg
ms.topic: how-to
ms.custom: mvc, msecd-doc-authoring-1016
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 4de1ab73-9148-617a-33fc-045c21172e03
document_version_independent_id: 7cdf56cf-8c48-4e58-bdd9-d57e5c19d8af
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/manage-soc-with-incident-metrics.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/manage-soc-with-incident-metrics
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/manage-soc-with-incident-metrics.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 861cdf95-a383-0fbd-a9ff-0b145394326f
---

# Manage your SOC Better with Incident Metrics in Microsoft Sentinel | Microsoft Learn

Note

For information about feature availability in US Government clouds, see the Microsoft Sentinel tables in [Cloud feature availability for US Government customers](/en-us/azure/security/fundamentals/feature-availability).

As a Security Operations Center (SOC) manager, you need to have overall efficiency metrics and measures at your fingertips to gauge the performance of your team. You'll want to see incident operations over time by many different criteria, like severity, MITRE tactics, mean time to triage, mean time to resolve, and more. Microsoft Sentinel now makes this data available to you with the new **SecurityIncident** table and schema in Log Analytics and the accompanying **Security operations efficiency** workbook. You'll be able to visualize your team's performance over time and use these incident metrics to improve efficiency. You can also write and use your own KQL queries against the incident table to create customized workbooks that fit your specific auditing needs and KPIs.

## Use the security incidents table

The **SecurityIncident** table is built into Microsoft Sentinel. You'll find it with the other tables in the **SecurityInsights** collection under **Logs**. You can query it like any other table in Log Analytics.

![Security incidents table](media/manage-soc-with-incident-metrics/security-incident-table.png)

Every time you create or update an incident, a new log entry will be added to the table. This allows you to track the changes made to incidents, and allows for even more powerful SOC metrics, but you need to be mindful that each incident update creates a new log entry when constructing queries for this table, as you may need to remove duplicate entries for an incident (dependent on the exact query you are running).

For example, if you wanted to return a list of all incidents sorted by their incident number but only wanted to return the most recent log per incident, you could retrieve the most recent log per incident by using the KQL [***summarize*** operator](/en-us/kusto/query/summarize-operator?view=microsoft-sentinel&amp;preserve-view=true) with the [***arg\_max()*** aggregation function](/en-us/kusto/query/arg-max-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true):

```Kusto
SecurityIncident
| summarize arg_max(LastModifiedTime, *) by IncidentNumber
```

### Sample KQL queries for incident metrics

The following examples show common KQL queries you can use with the **SecurityIncident** table.

Incident state - all incidents by status and severity in a given time frame:

```Kusto
let startTime = ago(14d);
let endTime = now();
SecurityIncident
| where TimeGenerated >= startTime
| summarize arg_max(TimeGenerated, *) by IncidentNumber
| where LastModifiedTime  between (startTime .. endTime)
| where Status in  ('New', 'Active', 'Closed')
| where Severity in ('High','Medium','Low', 'Informational')
```

Closure time by percentile:

```Kusto
SecurityIncident
| summarize arg_max(TimeGenerated,*) by IncidentNumber 
| extend TimeToClosure =  (ClosedTime - CreatedTime)/1h
| summarize 5th_Percentile=percentile(TimeToClosure, 5),50th_Percentile=percentile(TimeToClosure, 50), 
  90th_Percentile=percentile(TimeToClosure, 90),99th_Percentile=percentile(TimeToClosure, 99)
```

Triage time by percentile:

```Kusto
SecurityIncident
| summarize arg_max(TimeGenerated,*) by IncidentNumber 
| extend TimeToTriage =  (FirstModifiedTime - CreatedTime)/1h
| summarize 5th_Percentile=max_of(percentile(TimeToTriage, 5),0),50th_Percentile=percentile(TimeToTriage, 50), 
  90th_Percentile=percentile(TimeToTriage, 90),99th_Percentile=percentile(TimeToTriage, 99) 
```

## Security operations efficiency workbook

To complement the **SecurityIncidents** table, we’ve provided you with an out-of-the-box **security operations efficiency** workbook template that you can use to monitor your SOC operations. The workbook contains the following metrics:

- Incident created over time
- Incidents created by closing classification, severity, owner, and status
- Mean time to triage
- Mean time to closure
- Incidents created by severity, owner, status, product, and tactics over time
- Time to triage percentiles
- Time to closure percentiles
- Mean time to triage per owner
- Recent activities
- Recent closing classifications

You can find this new workbook template by choosing **Workbooks** from the Microsoft Sentinel navigation menu and selecting the **Templates** tab. Choose **Security operations efficiency** from the gallery and click one of the **View saved workbook** and **View template** buttons.

![Security incidents workbook gallery](media/manage-soc-with-incident-metrics/security-incidents-workbooks-gallery.png)

![Security incidents workbook complete](media/manage-soc-with-incident-metrics/security-operations-workbook-1.png)

You can use the template to create your own custom workbooks tailored to your specific needs.

## Review the SecurityIncidents schema

The following schema reference describes the fields available in the **SecurityIncident** table.

### The data model of the schema

| Field | Data type | Description |
| --- | --- | --- |
| **AdditionalData** | dynamic | Alerts count, bookmarks count, comments count, alert products names and tactics |
| **AlertIds** | dynamic | Alerts from which incident was created |
| **BookmarkIds** | dynamic | Bookmarked entities |
| **Classification** | string | Incident closing classification |
| **ClassificationComment** | string | Incident closing classification comment |
| **ClassificationReason** | string | Incident closing classification reason |
| **ClosedTime** | datetime | Timestamp (UTC) of when the incident was last closed |
| **Comments** | dynamic | Incident comments |
| **CreatedTime** | datetime | Timestamp (UTC) of when the incident was created |
| **Description** | string | Incident description |
| **FirstActivityTime** | datetime | First event time |
| **FirstModifiedTime** | datetime | Timestamp (UTC) of when the incident was first modified |
| **IncidentName** | string | Internal GUID |
| **IncidentNumber** | int |  |
| **IncidentUrl** | string | Link to incident |
| **Labels** | dynamic | Tags |
| **LastActivityTime** | datetime | Last event time |
| **LastModifiedTime** | datetime | Timestamp (UTC) of when the incident was last modified (the modification described by the current record) |
| **ModifiedBy** | string | User or system that modified the incident |
| **Owner** | dynamic |  |
| **RelatedAnalyticRuleIds** | dynamic | Rules from which the incident's alerts were triggered |
| **Severity** | string | Severity of the incident (High/Medium/Low/Informational) |
| **SourceSystem** | string | Constant ('Azure') |
| **Status** | string |  |
| **TenantId** | string |  |
| **TimeGenerated** | datetime | Timestamp (UTC) of when the current record was created (upon modification of the incident) |
| **Title** | string |  |
| **Type** | string | Constant ('SecurityIncident') |
|  |  |  |