---
layout: Conceptual
title: Work with STIX objects and indicators to enhance threat intelligence and threat hunting in Microsoft Sentinel (Preview) - Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/work-with-stix-objects-indicators
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
description: Learn how to use STIX objects and indicators in Microsoft Sentinel queries for threat hunting, and how to migrate to the new ThreatIntelIndicators and ThreatIntelObjects table schemas.
ms.author: guywild
author: guywi-ms
ms.reviewer: yoninave
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: bbc94c09-0fc6-e375-b31f-e5ac5ecdcd5e
document_version_independent_id: 15cae4c5-d7c9-e5af-5718-eaae57219176
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/work-with-stix-objects-indicators.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/work-with-stix-objects-indicators
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/work-with-stix-objects-indicators.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: a46ab334-7da7-a53f-3ec8-63e42126337d
---

# Work with STIX objects and indicators to enhance threat intelligence and threat hunting in Microsoft Sentinel (Preview) - Microsoft Sentinel | Microsoft Learn

On April 3, 2025, we publicly previewed two new tables to support STIX (Structured Threat Information eXpression) indicator and object schemas: `ThreatIntelIndicators` and `ThreatIntelObjects`. This article provides examples of how to incorporate STIX objects into queries to enhance threat hunting, and how to migrate to the new `ThreatIntelIndicators` table schema.

For more information about threat intelligence in Microsoft Sentinel, see [Threat intelligence in Microsoft Sentinel](understand-threat-intelligence).

Important

Microsoft Sentinel will ingest all threat intelligence into the new `ThreatIntelIndicators` and `ThreatIntelObjects` tables, while continuing to ingest the same data into the legacy `ThreatIntelligenceIndicator` table until July 31, 2025. **Be sure to update your custom queries, analytics and detection rules, workbooks, and automation to use the new tables by July 31, 2025.** After July 31, 2025, Microsoft Sentinel will stop ingesting data to the legacy `ThreatIntelligenceIndicator` table. We're updating all out-of-the-box threat intelligence solutions in Content hub to leverage the new tables. We introduced important updates to the data republishing processes.

1. Previously, data was divided and republished to Log Analytics over a **12-day period**. Now, **all data** is republished every **7-10 days**. You can identify this data in the `ThreatIntelIndicators` and `ThreatIntelObjects` tables by checking if `LastUpdateMethod` equals `LogARepublisher`.
2. The new tables now support more columns, including the `Data` column, which contains the full data object (except for attributes that already exist in other columns) used in advanced hunting scenarios. If the `Data` column or other added columns don't align with your scenario, learn more about filtering out columns and filtering out rows before ingestion to Log Analytics.
3. To optimize ingestion to Log Analytics, key-value pairs with no data are excluded. Additionally, some fields within the `Data` column—such as `description` and `pattern`—are truncated if they exceed 1,000 characters. For more information on the updated schema and how it might affect your usage, see [ThreatIntelIndicators](/en-us/azure/azure-monitor/reference/tables/threatintelindicators) and [ThreatIntelObjects](/en-us/azure/azure-monitor/reference/tables/threatintelobjects).

## Identify threat actors associated with specific threat indicators

This query is an example of how to correlate threat indicators, such as IP addresses, with threat actors:

```Kusto
 let IndicatorsWithThatIP = (ThreatIntelIndicators
| extend tlId = tostring(Data.id)
| summarize arg_max(TimeGenerated,*) by Id
|  where IsDeleted == false);
let ThreatActors = (ThreatIntelObjects
| where StixType == 'threat-actor'
| extend tlId = tostring(Data.id)
| extend ThreatActorName = Data.name
| extend ThreatActorSource = base64_decode_tostring(tostring(split(Id, '---')[0]))
| summarize arg_max(TimeGenerated,*) by Id
|  where IsDeleted == false);
let AllRelationships = (ThreatIntelObjects
| where StixType == 'relationship'
| extend tlSourceRef = tostring(Data.source_ref)
| extend tlTargetRef = tostring(Data.target_ref)
| extend tlId = tostring(Data.id)
| summarize arg_max(TimeGenerated,*) by Id
|  where IsDeleted == false);
let IndicatorAsSource = (IndicatorsWithThatIP
| join AllRelationships on $left.tlId == $right.tlSourceRef
| join ThreatActors on $left.tlTargetRef == $right.tlId);
let IndicatorAsTarget = (IndicatorsWithThatIP
| join AllRelationships on $left.tlId == $right.tlTargetRef
| join ThreatActors on $left.tlSourceRef == $right.tlId);
IndicatorAsSource
| union IndicatorAsTarget
| project ObservableValue, ThreatActorName
```

## List threat intelligence data related to a specific threat actor

This query provides insights into the tactics, techniques, and procedures (TTPs) of the threat actor (replace `Sangria Tempest` with the name of the threat actor you want to investigate):

```Kusto
let THREAT_ACTOR_NAME = 'Sangria Tempest';
let ThreatIntelObjectsPlus = (ThreatIntelObjects
| union (ThreatIntelIndicators
| extend StixType = 'indicator')
| extend tlId = tostring(Data.id)
| extend PlusStixTypes = StixType
| extend importantfield = case(StixType == "indicator", Data.pattern,
                            StixType == "attack-pattern", Data.name,
                            "Unkown")
| extend feedSource = base64_decode_tostring(tostring(split(Id, '---')[0]))
| summarize arg_max(TimeGenerated,*) by Id
|  where IsDeleted == false);
let ThreatActorsWithThatName = (ThreatIntelObjects
| where StixType == 'threat-actor'
| where Data.name == THREAT_ACTOR_NAME
| extend tlId = tostring(Data.id)
| extend ActorName = tostring(Data.name)
| summarize arg_max(TimeGenerated,*) by Id
|  where IsDeleted == false);
let AllRelationships = (ThreatIntelObjects
| where StixType == 'relationship'
| extend tlSourceRef = tostring(Data.source_ref)
| extend tlTargetRef = tostring(Data.target_ref)
| extend tlId = tostring(Data.id)
| summarize arg_max(TimeGenerated,*) by Id
|  where IsDeleted == false);
let SourceRelationships = (ThreatActorsWithThatName
| join AllRelationships on $left.tlId == $right.tlSourceRef
| join ThreatIntelObjectsPlus on $left.tlTargetRef == $right.tlId);
let TargetRelationships = (ThreatActorsWithThatName
| join AllRelationships on $left.tlId == $right.tlTargetRef
| join ThreatIntelObjectsPlus on $left.tlSourceRef == $right.tlId);
SourceRelationships
| union TargetRelationships
| project ActorName, PlusStixTypes, ObservableValue, importantfield, Tags, feedSource
```

## Migrate existing queries to the new ThreatIntelIndicators schema

This example shows how to migrate existing queries from the legacy `ThreatIntelligenceIndicator` table to the new `ThreatIntelIndicators` schema. The query uses the `extend` operator to recreate legacy columns based on the `ObservableKey` and `ObservableValue` columns in the new table.

```Kusto
ThreatIntelIndicators
| extend NetworkIP = iff(ObservableKey == 'ipv4-addr:value', ObservableValue, ''),
        NetworkSourceIP = iff(ObservableKey == 'network-traffic:src_ref.value', ObservableValue, ''),
        NetworkDestinationIP = iff(ObservableKey == 'network-traffic:dst_ref.value', ObservableValue, ''),
        DomainName = iff(ObservableKey == 'domain-name:value', ObservableValue, ''),
        EmailAddress = iff(ObservableKey == 'email-addr:value', ObservableValue, ''),
        FileHashType = case(ObservableKey has 'MD5', 'MD5',
                                ObservableKey has 'SHA-1', 'SHA-1',
                                ObservableKey has 'SHA-256', 'SHA-256',
                                ''),
        FileHashValue = iff(ObservableKey has 'file:hashes', ObservableValue, ''),
        Url = iff(ObservableKey == 'url:value', ObservableValue, ''),
        x509Certificate = iff(ObservableKey has 'x509-certificate:hashes.', ObservableValue, ''),
        x509Issuer = iff(ObservableKey has 'x509-certificate:issuer', ObservableValue, ''),
        x509CertificateNumber = iff(ObservableKey == 'x509-certificate:serial_number', ObservableValue, ''),        
        Description = tostring(Data.description),
        CreatedByRef = Data.created_by_ref,
        Extensions = Data.extensions,
        ExternalReferences = Data.references,
        GranularMarkings = Data.granular_markings,
        IndicatorId = tostring(Data.id),
        ThreatType = tostring(Data.indicator_types[0]),
        KillChainPhases = Data.kill_chain_phases,
        Labels = Data.labels,
        Lang = Data.lang,
        Name = Data.name,
        ObjectMarkingRefs = Data.object_marking_refs,
        PatternType = Data.pattern_type,
        PatternVersion = Data.pattern_version,
        Revoked = Data.revoked,
        SpecVersion = Data.spec_version
| project-reorder TimeGenerated, WorkspaceId, AzureTenantId, ThreatType, ObservableKey, ObservableValue, Confidence, Name, Description, LastUpdateMethod, SourceSystem, Created, Modified, ValidFrom, ValidUntil, IsDeleted, Tags, AdditionalFields, CreatedByRef, Extensions, ExternalReferences, GranularMarkings, IndicatorId, KillChainPhases, Labels, Lang, ObjectMarkingRefs, Pattern, PatternType, PatternVersion, Revoked, SpecVersion, NetworkIP, NetworkDestinationIP, NetworkSourceIP, DomainName, EmailAddress, FileHashType, FileHashValue, Url, x509Certificate, x509Issuer, x509CertificateNumber, Data
```

## Filter data before sending it to Log Analytics

[Transformations in Azure Monitor](/en-us/azure/azure-monitor/data-collection/data-collection-transformations) allow you to filter or modify incoming data before it's stored in a Log Analytics workspace. They're implemented as a Kusto Query Language (KQL) statement in a [data collection rule (DCR)](/en-us/azure/azure-monitor/data-collection/data-collection-rule-overview). Learn more about how to [create workspace transformations](/en-us/azure/azure-monitor/data-collection/data-collection-transformations-create?tabs=portal#create-workspace-transformation-dcr) and the [cost for transformations](/en-us/azure/azure-monitor/data-collection/data-collection-transformations#cost-for-transformations).

### Exclude columns before sending data to Log Analytics

The `ThreatIntelIndicators` and `ThreatIntelObjects` tables include a `Data` column that contains the full original STIX object. If this column isn't relevant to your use case, you can filter it out before ingestion using the following KQL statement:

```Kusto
source
| project-away Data
```

### Exclude rows before sending data to Log Analytics

The `ThreatIntelIndicators` table always receives at least one row for each unexpired indicator. In some cases, the STIX pattern can't be parsed into key/value pairs. When this happens, the indicator is still sent to Log Analytics, but only the raw, unparsed pattern is included—allowing users to build custom analytics if needed. If these rows aren't useful for your scenario, you can filter them out before ingestion using the following KQL statement:

```Kusto
source
| where (ObservableKey != "" and isnotempty(ObservableKey)) 
    or (ObservableValue != "" and isnotempty(ObservableValue))
```