---
layout: Conceptual
title: Migrate ArcSight Detection Rules to Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/migration-arcsight-detection-rules
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
description: Identify, compare, and migrate your ArcSight detection rules to Microsoft Sentinel analytics rules.
author: EdB-MSFT
ms.author: edbaynash
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 619f0d63-5380-95d7-5c0b-66ecac7670a8
document_version_independent_id: 53819ff3-5bf7-3b0c-b4b4-90e6da0d9955
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/migration-arcsight-detection-rules.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/migration-arcsight-detection-rules
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/migration-arcsight-detection-rules.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: b42978ee-f47e-2e66-a5a2-8365ea790e81
---

# Migrate ArcSight Detection Rules to Microsoft Sentinel | Microsoft Learn

This article describes how to identify, compare, and migrate your ArcSight detection rules to Microsoft Sentinel analytics rules.

## Identify and migrate rules

Microsoft Sentinel uses machine learning analytics to create high-fidelity and actionable incidents, and some of your existing detections may be redundant in Microsoft Sentinel. Therefore, don't migrate all of your detection and analytics rules blindly. Review the following considerations as you identify your existing detection rules.

- Make sure to select use cases that justify rule migration, considering business priority and efficiency.
- Check that you [understand Microsoft Sentinel rule types](threat-detection).
- Check that you understand the rule terminology.
- Review any rules that haven't triggered any alerts in the past six to 12 months, and determine whether they're still relevant.
- Eliminate low-level threats or alerts that you routinely ignore.
- Use existing functionality, and check whether Microsoft Sentinel’s [built-in analytics rules](https://github.com/Azure/Azure-Sentinel/tree/master/Detections) might address your current use cases. Because Microsoft Sentinel uses machine learning analytics to produce high-fidelity and actionable incidents, it’s likely that some of your existing detections won’t be required anymore.
- Confirm connected data sources and review your data connection methods. Revisit data collection conversations to ensure data depth and breadth across the use cases you plan to detect.
- Explore community resources such as the [SOC Prime Threat Detection Marketplace](https://my.socprime.com/platform-overview/) to check whether your rules are available.
- Consider whether an online query converter such as Uncoder.io might work for your rules.
- If rules aren’t available or can’t be converted, they need to be created manually, using a KQL query. Review the rules mapping to create new queries.

Learn more about [best practices for migrating detection rules](https://techcommunity.microsoft.com/t5/microsoft-sentinel-blog/best-practices-for-migrating-detection-rules-from-arcsight/ba-p/2216417).

**To migrate your analytics rules to Microsoft Sentinel**:

1. Verify that you have a testing system in place for each rule you want to migrate.

    1. **Prepare a validation process** for your migrated rules, including full test scenarios and scripts.
    2. **Ensure that your team has useful resources** to test your migrated rules.
    3. **Confirm that you have any required data sources connected,** and review your data connection methods.
2. Verify whether your detections are available as built-in templates in Microsoft Sentinel:

    - **If the built-in rules are sufficient**, use built-in rule templates to create rules for your own workspace.

        In Microsoft Sentinel, go to the **Configuration &gt; Analytics &gt; Rule templates** tab, and create and update each relevant analytics rule.

        To learn how to create rules from built-in templates, see [Create scheduled analytics rules from templates](create-analytics-rule-from-template).
    - **If you have detections that aren't covered by Microsoft Sentinel's built-in rules**, try an online query converter, such as [Uncoder.io](https://uncoder.io/) to convert your queries to KQL.

        Identify the trigger condition and rule action, and then construct and review your KQL query.
    - **If neither the built-in rules nor an online rule converter is sufficient**, you'll need to create the rule manually. In such cases, use the following steps to start creating your rule:

        1. **Identify the data sources you want to use in your rule**. You'll want to create a mapping table between data sources and data tables in Microsoft Sentinel to identify the tables you want to query.
        2. **Identify any attributes, fields, or entities** in your data that you want to use in your rules.
        3. **Identify your rule criteria and logic**. At this stage, you may want to use rule templates as samples for how to construct your KQL queries.

            Consider filters, correlation rules, active lists, reference sets, watchlists, detection anomalies, aggregations, and so on. You might use references provided by your legacy SIEM to map ArcSight query syntax to KQL.
        4. **Identify the trigger condition and rule action, and then construct and review your KQL query**. When reviewing your query, consider KQL optimization guidance resources.
3. Test the rule with each of your relevant use cases. If it doesn't provide expected results, you may want to review the KQL and test it again.
4. When you're satisfied, you can consider the rule migrated. Create a playbook for your rule action as needed. To create and use playbooks for rule actions, see [Automate threat response with playbooks in Microsoft Sentinel](automate-responses-with-playbooks).

Learn more about analytics rules:

- [**Scheduled analytics rules in Microsoft Sentinel**](scheduled-rules-overview): Use [alert grouping](scheduled-rules-overview#alert-grouping) to reduce alert fatigue by grouping alerts that occur within a given timeframe.
- [**Map data fields to entities in Microsoft Sentinel**](map-data-fields-to-entities): To enable SOC engineers to define entities as part of the evidence to track during an investigation. Entity mapping also makes it possible for SOC analysts to take advantage of an intuitive [investigation graph](investigate-cases#use-the-investigation-graph-to-deep-dive) that can help reduce time and effort.
- [**Investigate incidents with UEBA data**](investigate-with-ueba): As an example of how to use evidence to surface events, alerts, and any bookmarks associated with a particular incident in the incident preview pane.
- [**Kusto Query Language (KQL)**](/en-us/kusto/query/?view=microsoft-sentinel&amp;preserve-view=true): You can use KQL to send read-only requests to your [Log Analytics](/en-us/azure/azure-monitor/logs/log-analytics-tutorial) database to process data and return results. KQL is also used across other Microsoft services, such as [Microsoft Defender for Endpoint](https://www.microsoft.com/microsoft-365/security/endpoint-defender) and [Application Insights](/en-us/azure/azure-monitor/app/app-insights-overview).

## Compare rule terminology

This table helps you to clarify the concept of a rule in Microsoft Sentinel compared to ArcSight.

| - | ArcSight | Microsoft Sentinel |
| --- | --- | --- |
| **Rule type** | - Filter rule- Join rule- Active list rule- And more | - Scheduled query- Fusion- Microsoft Security- Machine Learning (ML) Behavior Analytics |
| **Criteria** | Define in rule conditions | Define in KQL |
| **Trigger condition** | - Define in action- Define in aggregation (for event aggregation) | Threshold: Number of query results |
| **Action** | - Set event field- Send notification- Create new case- Add to active list- And more | - Create alert or incident- Integrates with Logic Apps |

## Map and compare rule samples

Use the following samples to compare ArcSight detection rules with equivalent Microsoft Sentinel queries written in Kusto Query Language (KQL).

| Rule | Description | Sample detection rule (ArcSight) | Sample KQL query | Resources |
| --- | --- | --- | --- | --- |
| Filter (`AND`) | A sample rule with `AND` conditions. The event must match all conditions. | Filter (AND) example | Filter (AND) example | String filter:- [String operators](/en-us/kusto/query/datatypes-string-operators?view=microsoft-sentinel&amp;preserve-view=true#operators-on-strings)Numerical filter:- [Numerical operators](/en-us/kusto/query/numerical-operators?view=microsoft-sentinel&amp;preserve-view=true)Datetime filter:- [ago](/en-us/kusto/query/ago-function?view=microsoft-sentinel&amp;preserve-view=true)- [Datetime](/en-us/kusto/query/datetime-timespan-arithmetic?view=microsoft-sentinel&amp;preserve-view=true)- [between](/en-us/kusto/query/between-operator?view=microsoft-sentinel&amp;preserve-view=true)- [now](/en-us/kusto/query/now-function?view=microsoft-sentinel&amp;preserve-view=true)Parsing:- [parse](/en-us/kusto/query/parse-operator?view=microsoft-sentinel&amp;preserve-view=true)- [extract](/en-us/kusto/query/extract-function?view=microsoft-sentinel&amp;preserve-view=true)- [parse_json](/en-us/kusto/query/parse-json-function?view=microsoft-sentinel&amp;preserve-view=true)- [parse_csv](/en-us/kusto/query/parse-csv-function?view=microsoft-sentinel&amp;preserve-view=true)- [parse_path](/en-us/kusto/query/parse-path-function?view=microsoft-sentinel&amp;preserve-view=true)- [parse_url](/en-us/kusto/query/parse-url-function?view=microsoft-sentinel&amp;preserve-view=true) |
| Filter (`OR`) | A sample rule with `OR` conditions. The event can match any of the conditions. | Filter (OR) example | Filter (OR) example | - [String operators](/en-us/kusto/query/datatypes-string-operators?view=microsoft-sentinel&amp;preserve-view=true#operators-on-strings)- [in](/en-us/kusto/query/in-operator?view=microsoft-sentinel&amp;preserve-view=true) |
| Nested filter | A sample rule with nested filtering conditions. The rule includes the `MatchesFilter` statement, which also includes filtering conditions. | Nested filter example | Nested filter example | - [Use KQL functions to speed up analysis](https://techcommunity.microsoft.com/t5/azure-sentinel/using-kql-functions-to-speed-up-analysis-in-azure-sentinel/ba-p/712381)- [Enrich Windows security events with a parameterized function](https://techcommunity.microsoft.com/t5/microsoft-sentinel-blog/enriching-windows-security-events-with-parameterized-function/ba-p/1712564)- [join](/en-us/kusto/query/join-operator?view=microsoft-sentinel&amp;preserve-view=true)- [where](/en-us/kusto/query/where-operator?view=microsoft-sentinel&amp;preserve-view=true) |
| Active list (lookup) | A sample lookup rule that uses the `InActiveList` statement. | Active list (lookup) example | Active list (lookup) example | - A watchlist is the equivalent of the active list feature. Learn more about [watchlists](watchlists).- [Other ways to implement lookups](https://techcommunity.microsoft.com/t5/azure-sentinel/implementing-lookups-in-azure-sentinel/ba-p/1091306) |
| Correlation (matching) | A sample rule that defines a condition against a set of base events, using the `Matching Event` statement. | Correlation (matching) example | Correlation (matching) example | join operator:- [join](/en-us/kusto/query/join-operator?view=microsoft-sentinel&amp;preserve-view=true)- [join with time window](/en-us/kusto/query/join-time-window?view=microsoft-sentinel&amp;preserve-view=true)- [shuffle](/en-us/kusto/query/shuffle-query?view=microsoft-sentinel&amp;preserve-view=true)- [Broadcast](/en-us/kusto/query/broadcast-join?view=microsoft-sentinel&amp;preserve-view=true)- [Union](/en-us/kusto/query/union-operator?view=microsoft-sentinel&amp;preserve-view=true)define statement:- [let](/en-us/kusto/query/let-statement?view=microsoft-sentinel&amp;preserve-view=true)Aggregation:- [make_set](/en-us/kusto/query/make-set-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true)- [make_list](/en-us/kusto/query/make-list-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true)- [make_bag](/en-us/kusto/query/make-bag-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true)- [bag_pack](/en-us/kusto/query/pack-function?view=microsoft-sentinel&amp;preserve-view=true) |
| Correlation (time window) | A sample rule that defines a condition against a set of base events, using the `Matching Event` statement, and uses the `Wait time` filter condition. | Correlation (time window) example | Correlation (time window) example | - [join](/en-us/kusto/query/join-operator?view=microsoft-sentinel&amp;preserve-view=true)- [Microsoft Sentinel rules and join statement](https://techcommunity.microsoft.com/t5/azure-sentinel/azure-sentinel-correlation-rules-the-join-kql-operator/ba-p/1041500) |

### Filter (AND) example: ArcSight

Here's a sample filter rule with `AND` conditions in ArcSight.

[![Diagram illustrating a sample filter rule.](media/migration-arcsight-detection-rules/rule-1-sample.png)](media/migration-arcsight-detection-rules/rule-1-sample.png#lightbox)

### Filter (AND) example: KQL

Here's the filter rule with `AND` conditions in KQL.

```kusto
SecurityEvent
| where EventID == 4728
| where SubjectUserName =~ "AutoMatedService"
| where isnotempty(SubjectDomainName)
```

This rule assumes that the Azure Monitoring Agent (AMA) collects the Windows Security Events. Therefore, the rule uses the Microsoft Sentinel [SecurityEvent](/en-us/azure/azure-monitor/reference/tables/securityevent) table.

Consider these best practices:

- To optimize your queries, avoid case-insensitive operators when possible: `=~`.
- Use `==` if the value isn't case-sensitive.
- Order the filters by starting with the `where` statement, which filters out the most data.

### Filter (OR) example: ArcSight

Here's a sample filter rule with `OR` conditions in ArcSight.

![Diagram illustrating a sample filter rule (or).](media/migration-arcsight-detection-rules/rule-2-sample.png)

### Filter (OR) example: KQL

Here are a few ways to write the filter rule with `OR` conditions in KQL.

As a first option, use the `in` statement:

```kusto
SecurityEvent
| where SubjectUserName in
 ("Adm1","ServiceAccount1","AutomationServices")
```

As a second option, use the `or` statement:

```kusto
SecurityEvent
| where SubjectUserName == "Adm1" or 
SubjectUserName == "ServiceAccount1" or 
SubjectUserName == "AutomationServices"
```

While both options are identical in performance, we recommend the first option, which is easier to read.

### Nested filter example: ArcSight

Here's a sample nested filter rule in ArcSight.

![Diagram illustrating a sample nested filter rule.](media/migration-arcsight-detection-rules/rule-3-sample-1.png)

Here's a rule for the `/All Filters/Soc Filters/Exclude Valid Users` filter.

![Diagram illustrating an Exclude Valid Users filter.](media/migration-arcsight-detection-rules/rule-3-sample-2.png)

### Nested filter example: KQL

Here are a few ways to write the filter rule with `OR` conditions in KQL.

As a first option, use a direct filter with a `where` statement:

```kusto
SecurityEvent
| where EventID == 4728 
| where isnotempty(SubjectDomainName) or 
isnotempty(TargetDomainName) 
| where SubjectUserName !~ "AutoMatedService"
```

As a second option, use a KQL function:

1. Save the following query as a KQL function with the `ExcludeValidUsers` alias.

    ```kusto
        SecurityEvent
        | where EventID == 4728
        | where isnotempty(SubjectDomainName)
        | where SubjectUserName =~ "AutoMatedService"
        | project SubjectUserName
    ```
2. Use the following query to filter the `ExcludeValidUsers` alias.

    ```kusto
        SecurityEvent    
        | where EventID == 4728
        | where isnotempty(SubjectDomainName) or 
        isnotempty(TargetDomainName)
        | where SubjectUserName !in (ExcludeValidUsers)
    ```

As a third option, use a parameter function:

1. Create a parameter function with `ExcludeValidUsers` as the name and alias.
2. Define the parameters of the function. For example:

    ```kusto
        Tbl: (TimeGenerated:datetime, Computer:string, 
        EventID:string, SubjectDomainName:string, 
        TargetDomainName:string, SubjectUserName:string)
    ```
3. The `parameter` function has the following query:

    ```kusto
        Tbl
        | where SubjectUserName !~ "AutoMatedService"
    ```
4. Run the following query to invoke the parameter function:

    ```kusto
        let Events = (
        SecurityEvent 
        | where EventID == 4728
        );
        ExcludeValidUsers(Events)
    ```

As a fourth option, use the `join` function:

```kusto
let events = (
SecurityEvent
| where EventID == 4728
| where isnotempty(SubjectDomainName) 
or isnotempty(TargetDomainName)
);
let ExcludeValidUsers = (
SecurityEvent
| where EventID == 4728
| where isnotempty(SubjectDomainName)
| where SubjectUserName =~ "AutoMatedService"
);
events
| join kind=leftanti ExcludeValidUsers on 
$left.SubjectUserName == $right.SubjectUserName
```

#### Considerations

- We recommend that you use a direct filter with a `where` statement (first option) due to its simplicity. For optimized performance, avoid using `join` (fourth option).
- To optimize your queries, avoid the `=~` and `!~` case-insensitive operators when possible. Use the `==` and `!=` operators if the value isn't case-sensitive.

### Active list (lookup) example: ArcSight

Here's an active list (lookup) rule in ArcSight.

![Diagram illustrating a sample active list rule (lookup).](media/migration-arcsight-detection-rules/rule-4-sample.png)

### Active list (lookup) example: KQL

Important

Before you run this query, create the **Cyber-Ark Exception Accounts** watchlist in Microsoft Sentinel and include an **Account** field.

The following KQL query uses the Cyber-Ark Exception Accounts watchlist to filter lookup results.

```kusto
let Activelist=(
_GetWatchlist('Cyber-Ark Exception Accounts')
| project Account );
CommonSecurityLog
| where DestinationUserName in (Activelist)
| where DeviceVendor == "Cyber-Ark"
| where DeviceAction == "Get File Request"
| where DeviceCustomNumber1 != ""
| project DeviceAction, DestinationUserName, 
TimeGenerated,SourceHostName, 
SourceUserName, DeviceEventClassID
```

Order the filters by starting with the `where` statement that filters out the most data.

### Correlation (matching) example: ArcSight

Here's a sample ArcSight rule that defines a condition against a set of base events, using the `Matching Event` statement.

![Diagram illustrating a sample correlation rule (matching).](media/migration-arcsight-detection-rules/rule-5-sample.png)

### Correlation (matching) example: KQL

The following KQL example shows how to implement the ArcSight matching correlation rule in Microsoft Sentinel.

```kusto
let event1 =(
SecurityEvent
| where EventID == 4728
);
let event2 =(
SecurityEvent
| where EventID == 4729
);
event1
| join kind=inner event2 
on $left.TargetUserName==$right.TargetUserName
```

#### Best practices

- To optimize your query, ensure that the smaller table is on the left side of the `join` function.
- If the left side of the table is relatively small (up to 100 K records), add `hint.strategy=broadcast` for better performance.

### Correlation (time window) example: ArcSight

Here's a sample ArcSight rule that defines a condition against a set of base events, using the `Matching Event` statement, and uses the `Wait time` filter condition.

![Diagram illustrating a sample correlation rule (time window).](media/migration-arcsight-detection-rules/rule-6-sample.png)

### Correlation (time window) example: KQL

The following KQL example implements a correlation rule with a time window equivalent to the ArcSight example.

```kusto
let waittime = 10m;
let lookback = 1d;
let event1 = (
SecurityEvent
| where TimeGenerated > ago(waittime+lookback)
| where EventID == 4728
| project event1_time = TimeGenerated, 
event1_ID = EventID, event1_Activity= Activity, 
event1_Host = Computer, TargetUserName, 
event1_UPN=UserPrincipalName, 
AccountUsedToAdd = SubjectUserName 
);
let event2 = (
SecurityEvent
| where TimeGenerated > ago(waittime)
| where EventID == 4729
| project event2_time = TimeGenerated, 
event2_ID = EventID, event2_Activity= Activity, 
event2_Host= Computer, TargetUserName, 
event2_UPN=UserPrincipalName,
 AccountUsedToRemove = SubjectUserName 
);
 event1
| join kind=inner event2 on TargetUserName
| where event2_time - event1_time < lookback
| where tolong(event2_time - event1_time ) >=0
| project delta_time = event2_time - event1_time,
 event1_time, event2_time,
 event1_ID,event2_ID,event1_Activity,
 event2_Activity, TargetUserName, AccountUsedToAdd,
 AccountUsedToRemove,event1_Host,event2_Host, 
 event1_UPN,event2_UPN
```

### Aggregation example: ArcSight

Here's a sample ArcSight rule with aggregation settings: three matches within 10 minutes.

![Diagram illustrating a sample aggregation rule.](media/migration-arcsight-detection-rules/rule-7-sample.png)

### Aggregation example: KQL

The following KQL query shows how to detect three or more matches using aggregation.

```kusto
SecurityEvent
| summarize Count = count() by SubjectUserName, 
SubjectDomainName
| where Count >3
```