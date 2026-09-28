---
layout: Conceptual
title: Migrate QRadar Detection Rules to Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/migration-qradar-detection-rules
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
description: Learn how to inventory QRadar detection rules, map them to Microsoft Sentinel analytics rule types, and plan your migration using built-in detections or custom KQL queries.
author: EdB-MSFT
ms.author: edbaynash
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 57024277-5dcc-2d5c-34f9-fc33013d68a0
document_version_independent_id: 58705781-0da1-624b-58ef-bda908b7d3be
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/migration-qradar-detection-rules.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/migration-qradar-detection-rules
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/migration-qradar-detection-rules.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: d9a44f28-087a-0eca-6393-207060ed9d6a
---

# Migrate QRadar Detection Rules to Microsoft Sentinel | Microsoft Learn

This article describes how to identify, compare, and migrate your QRadar detection rules to Microsoft Sentinel built-in rules. It walks you through inventorying your existing detections, comparing rule terminology between QRadar and Microsoft Sentinel, and choosing the right migration path—whether that's adopting built-in analytics templates from the Content Hub, converting queries with an online tool, or writing custom Kusto Query Language (KQL) queries. By the end, you'll have a structured approach for migrating your detection rules while taking advantage of Microsoft Sentinel's machine learning analytics.

## Identify and migrate rules

Microsoft Sentinel uses machine learning analytics to create high-fidelity and actionable incidents, and some of your existing detections may be redundant in Microsoft Sentinel. Therefore, don't migrate all of your detection and analytics rules blindly. Review these considerations as you identify your existing detection rules.

- Make sure to select use cases that justify rule migration, considering business priority and efficiency.
- Check that you [understand Microsoft Sentinel rule types](threat-detection).
- Check that you understand the rule terminology.
- Review any rules that haven't triggered any alerts in the past 6-12 months, and determine whether they're still relevant.
- Eliminate low-level threats or alerts that you routinely ignore.
- Use existing functionality and check whether Microsoft Sentinel’s [built-in analytics rules](https://github.com/Azure/Azure-Sentinel/tree/master/Detections) might address your current use cases. Because Microsoft Sentinel uses machine learning analytics to produce high-fidelity and actionable incidents, it’s likely that some of your existing detections won’t be required anymore.
- Confirm connected data sources and review your data connection methods. Revisit data collection conversations to ensure data depth and breadth across the use cases you plan to detect.
- Explore community resources such as the [SOC Prime Threat Detection Marketplace](https://my.socprime.com/platform-overview/) to check whether your rules are available.
- Consider whether an online query converter such as Uncoder.io might work for your rules.
- If rules aren't available or can't be converted, they need to be created manually, using a KQL query. Review the rules mapping to create new queries.

Learn more about [best practices for migrating detection rules](https://techcommunity.microsoft.com/t5/microsoft-sentinel-blog/best-practices-for-migrating-detection-rules-from-arcsight/ba-p/2216417).

**To migrate your analytics rules to Microsoft Sentinel**:

1. Verify that you have a testing system in place for each rule you want to migrate.

    1. **Prepare a validation process** for your migrated rules, including full test scenarios and scripts.
    2. **Ensure that your team has useful resources** to test your migrated rules.
    3. **Confirm that you have any required data sources connected,** and review your data connection methods.
2. Verify whether your detections are available as built in templates in the Content Hub:

    - **If the built in rules are sufficient**, install the relevant solutions and use the templates to create rules for your workspace.

        1. In Microsoft Sentinel, go to **Content management &gt; Content hub**.
        2. Search for and install the relevant analytics rule.

        For more information, see [Discover and manage Microsoft Sentinel out-of-the-box content](sentinel-solutions-deploy) and [Create scheduled analytics rules from templates](create-analytics-rule-from-template).
    - **If you have detections that aren't covered by the built in rules available in theContent Hub**, try an online query converter, such as [Uncoder.io](https://uncoder.io/) to convert your queries to KQL.

        Identify the trigger condition and rule action, and then construct and review your KQL query.
    - **If neither Content Hub solutions nor an online rule converter is sufficient**, you'll need to create the rule manually. In such cases, use the following steps to start creating your rule:

        1. **Identify the data sources you want to use in your rule**. You'll want to create a mapping table between data sources and data tables in Microsoft Sentinel to identify the tables you want to query.
        2. **Identify any attributes, fields, or entities** in your data that you want to use in your rules.
        3. **Identify your rule criteria and logic**. At this stage, you may want to use rule templates as samples for how to construct your KQL queries as samples for how to construct your KQL queries.

            Consider filters, correlation rules, active lists, reference sets, watchlists, detection anomalies, aggregations, and so on. You might use references provided by your legacy SIEM to understand how to best map your query syntax.
        4. **Identify the trigger condition and rule action, and then construct and review your KQL query**. When reviewing your query, consider KQL optimization guidance resources.
3. Test the rule with each of your relevant use cases. If it doesn't provide expected results, you may want to review the KQL and test it again.
4. When you're satisfied, you can consider the rule migrated. Create a playbook for your rule action as needed. For more information, see [Automate threat response with playbooks in Microsoft Sentinel](automate-responses-with-playbooks).

For more information about Microsoft Sentinel analytics rules and KQL, see the following resources:

- [**Scheduled analytics rules in Microsoft Sentinel**](scheduled-rules-overview): Use [alert grouping](scheduled-rules-overview#alert-grouping) to reduce alert fatigue by grouping alerts that occur within a given timeframe.
- [**Map data fields to entities in Microsoft Sentinel**](map-data-fields-to-entities): To enable SOC engineers to define entities as part of the evidence to track during an investigation. Entity mapping also makes it possible for SOC analysts to take advantage of an intuitive [investigation graph](investigate-cases#use-the-investigation-graph-to-deep-dive) that can help reduce time and effort.
- [**Investigate incidents with UEBA data**](investigate-with-ueba): As an example of how to use evidence to surface events, alerts, and any bookmarks associated with a particular incident in the incident preview pane.
- [**Kusto Query Language (KQL)**](/en-us/kusto/query/?view=microsoft-sentinel&amp;preserve-view=true): Which you can use to send read-only requests to your [Log Analytics](/en-us/azure/azure-monitor/logs/log-analytics-tutorial) database to process data and return results. KQL is also used across other Microsoft services, such as [Microsoft Defender for Endpoint](https://www.microsoft.com/microsoft-365/security/endpoint-defender) and [Application Insights](/en-us/azure/azure-monitor/app/app-insights-overview).

## Compare rule terminology

This table helps you to clarify the concept of a rule in Microsoft Sentinel compared to QRadar. Microsoft Sentinel rule types include scheduled queries, Fusion (which automatically correlates alerts from multiple data sources into incidents using machine learning), Microsoft Security, and Machine Learning (ML) Behavior Analytics.

| - | QRadar | Microsoft Sentinel |
| --- | --- | --- |
| **Rule type** | - Events- Flow- Common- Offense- Anomaly detection rules | - Scheduled query- Fusion- Microsoft Security- Machine Learning (ML) Behavior Analytics |
| **Criteria** | Define in test condition | Define in KQL |
| **Trigger condition** | Define in rule | Threshold: Number of query results |
| **Action** | - Create offense- Dispatch new event- Add to reference set or data- And more | - Create alert or incident- Integrates with Logic Apps |

## Map and compare rule samples

Use these samples to compare and map rules from QRadar to Microsoft Sentinel in various scenarios. The sample queries are written in Kusto Query Language (KQL), the query language used by Microsoft Sentinel.

| Rule | Syntax | Sample detection rule (QRadar) | Sample KQL query | Resources |
| --- | --- | --- | --- | --- |
| Common property tests | QRadar syntax | - Regular expression example- AQL filter query example- equals/not equals example | - Regular expression example- AQL filter query example- equals/not equals example | - Regular expression: [matches regex](/en-us/kusto/query/regex?view=microsoft-sentinel&amp;preserve-view=true)- AQL filter query: [string operators](/en-us/kusto/query/datatypes-string-operators?view=microsoft-sentinel&amp;preserve-view=true#operators-on-strings)- equals/not equals: [String operators](/en-us/kusto/query/datatypes-string-operators?view=microsoft-sentinel&amp;preserve-view=true#operators-on-strings) |
| Date/time tests | QRadar syntax | - Selected day of the month example- Selected day of the week example- after/before/at example | - Selected day of the month example- Selected day of the week example- after/before/at example | - [Date and time operators](/en-us/kusto/query/datetime-timespan-arithmetic?view=microsoft-sentinel&amp;preserve-view=true)- Selected day of the month: [dayofmonth()](/en-us/kusto/query/day-of-month-function?view=microsoft-sentinel&amp;preserve-view=true)- Selected day of the week: [dayofweek()](/en-us/kusto/query/day-of-week-function?view=microsoft-sentinel&amp;preserve-view=true)- after/before/at: [format_datetime()](/en-us/kusto/query/format-datetime-function?view=microsoft-sentinel&amp;preserve-view=true) |
| Event property tests | QRadar syntax | - IP protocol example- Event Payload string example | - IP protocol example- Event Payload string example | - IP protocol: [String operators](/en-us/kusto/query/datatypes-string-operators?view=microsoft-sentinel&amp;preserve-view=true#operators-on-strings)- Event Payload string: [has](/en-us/kusto/query/has-operator?view=microsoft-sentinel&amp;preserve-view=true) |
| Functions: counters | QRadar syntax | Event property and time example | Event property and time example | [summarize](/en-us/kusto/query/summarize-operator?view=microsoft-sentinel&amp;preserve-view=true) |
| Functions: negative conditions | QRadar syntax | Negative conditions example | Negative conditions example | - [join()](/en-us/kusto/query/join-operator?view=microsoft-sentinel&amp;preserve-view=true)- [String operators](/en-us/kusto/query/datatypes-string-operators?view=microsoft-sentinel&amp;preserve-view=true#operators-on-strings)- [Numerical operators](/en-us/kusto/query/numerical-operators?view=microsoft-sentinel&amp;preserve-view=true) |
| Functions: simple | QRadar syntax | Simple conditions example | Simple conditions example | [or](/en-us/kusto/query/logical-operators?view=microsoft-sentinel&amp;preserve-view=true) |
| IP/port tests | QRadar syntax | - Source port example- Source IP example | - Source port example- Source IP example |  |
| Log source tests | QRadar syntax | Log source example | Log source example |  |

### Common property tests syntax

Here's the QRadar syntax for a common property tests rule.

![Diagram illustrating a common property test rule syntax.](media/migration-qradar-detection-rules/rule-1-syntax.png)

### Common property tests: Regular expression example (QRadar)

Here's the syntax for a sample QRadar common property tests rule that uses a regular expression:

```
when any of <these properties> match <this regular expression>
```

Here's the sample rule in QRadar:

![Diagram illustrating a common property test rule that uses a regular expression.](media/migration-qradar-detection-rules/rule-1-sample.png)

### Common property tests: Regular expression example (KQL)

Here's the common property tests rule with a regular expression in KQL.

```kusto
CommonSecurityLog
| where tostring(SourcePort) matches regex @"\d{1,5}" or tostring(DestinationPort) matches regex @"\d{1,5}"
```

### Common property tests: AQL filter query example (QRadar)

Here's the syntax for a sample QRadar common property tests rule that uses an AQL filter query:

```
when the event matches <this> AQL filter query
```

Here's the sample rule in QRadar:

![Diagram illustrating a common property test rule that uses an A Q L filter query.](media/migration-qradar-detection-rules/rule-1-sample-aql.png)

### Common property tests: AQL filter query example (KQL)

Here's the common property tests rule with an AQL filter query in KQL:

```kusto
CommonSecurityLog
| where SourceIP == '10.1.1.10'
```

### Common property tests: equals/not equals example (QRadar)

Here's the syntax for a sample QRadar common property tests rule that uses the `equals` or `not equals` operator:

```
and when <this property> <equals/not equals> <this property>
```

Here's the sample rule in QRadar: ![Diagram illustrating a common property test rule that uses equals/not equals.](media/migration-qradar-detection-rules/rule-1-sample-equals.png)

### Common property tests: equals/not equals example (KQL)

Here's the common property tests rule with the `equals` or `not equals` operator in KQL:

```kusto
CommonSecurityLog
| where SourceIP == DestinationIP
```

### Date/time tests syntax

Here's the QRadar syntax for a date/time tests rule:

![Diagram illustrating a date/time tests rule syntax.](media/migration-qradar-detection-rules/rule-2-syntax.png)

### Date/time tests: Selected day of the month example (QRadar)

Here's the syntax for a sample QRadar date/time tests rule that uses a selected day of the month:

```
and when the event(s) occur <on/after/before> the <selected> day of the month
```

Here's the sample rule in QRadar:

![Diagram illustrating a date/time tests rule that uses a selected day.](media/migration-qradar-detection-rules/rule-2-sample-selected-day.png)

### Date/time tests: Selected day of the month example (KQL)

Here's the date/time tests rule with a selected day of the month in KQL:

```kusto
SecurityEvent
 | where dayofmonth(TimeGenerated) < 4
```

### Date/time tests: Selected day of the week example (QRadar)

Here's the syntax for a sample QRadar date/time tests rule that uses a selected day of the week:

```
and when the event(s) occur on any of <these days of the week{Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday}>
```

Here's the sample rule in QRadar:

![Diagram illustrating a date/time tests rule that uses a selected day of the week.](media/migration-qradar-detection-rules/rule-2-sample-selected-day-week.png)

### Date/time tests: Selected day of the week example (KQL)

Here's the date/time tests rule with a selected day of the week in KQL:

```kusto
SecurityEvent
 | where dayofweek(TimeGenerated) between (3d .. 5d)
```

### Date/time tests: after/before/at example (QRadar)

Here's the syntax for a sample QRadar date/time tests rule that uses the `after`, `before`, or `at` operator:

```
and when the event(s) occur <after/before/at> <this time{12.00AM, 12.05AM, ...11.50PM, 11.55PM}>
```

Here's the sample rule in QRadar:

![Diagram illustrating a date/time tests rule that uses the after/before/at operator.](media/migration-qradar-detection-rules/rule-2-sample-after-before-at.png)

### Date/time tests: after/before/at example (KQL)

Here's the date/time tests rule that uses the `after`, `before`, or `at` operator in KQL:

```kusto
SecurityEvent
| where format_datetime(TimeGenerated,'HH:mm')=="23:55"
```

`TimeGenerated` is in UTC/GMT.

### Event property tests syntax

Here's the QRadar syntax for an event property tests rule:

![Diagram illustrating an event property tests rule syntax.](media/migration-qradar-detection-rules/rule-3-syntax.png)

### Event property tests: IP protocol example (QRadar)

Here's the syntax for a sample QRadar event property tests rule that uses an IP protocol:

```
and when the IP protocol is one of the following <protocols>
```

Here's the sample rule in QRadar:

![Diagram illustrating an event property tests rule that uses an I P protocol.](media/migration-qradar-detection-rules/rule-3-sample-protocol.png)

### Event property tests: IP protocol example (KQL)

Here's the event property tests rule with an IP protocol filter in KQL:

```kusto
CommonSecurityLog
| where Protocol in ("UDP","ICMP")
```

### Event property tests: Event Payload string example (QRadar)

Here's the syntax for a sample QRadar event property tests rule that uses an `Event Payload` string value:

```
and when the Event Payload contains <this string>
```

Here's the sample rule in QRadar:

![Diagram illustrating an event property tests rule that uses an Event Payload string.](media/migration-qradar-detection-rules/rule-3-sample-payload.png)

### Event property tests: Event Payload string example (KQL)

Here's the event property tests rule with an `Event Payload` string in KQL. To optimize performance, avoid using the `search` command if you already know the table name.

```kusto
CommonSecurityLog
| where DeviceVendor has "Palo Alto"

search "Palo Alto"
```

### Functions: counters syntax

Here's the QRadar syntax for a functions rule that uses counters:

![Diagram illustrating the syntax of a functions rule that uses counters.](media/migration-qradar-detection-rules/rule-4-syntax.png)

### Counters: Event property and time example (QRadar)

Here's the syntax for a sample QRadar functions rule that uses a defined number of event properties in a defined number of minutes"

```
and when at least <this many> events are seen with the same <event properties> in <this many> <minutes>
```

Here's the sample rule in QRadar:

![Diagram illustrating a functions rule that uses event properties.](media/migration-qradar-detection-rules/rule-4-sample-event-property.png)

### Counters: Event property and time example (KQL)

Here's the counters rule with event property and time conditions in KQL:

```kusto
CommonSecurityLog
| summarize Count = count() by SourceIP, DestinationIP
| where Count >= 5
```

### Functions: negative conditions syntax

Here's the QRadar syntax for a functions rule that uses negative conditions:

![Diagram illustrating the syntax of a functions rule that uses negative conditions.](media/migration-qradar-detection-rules/rule-5-syntax.png)

### Negative conditions example (QRadar)

Here's the syntax for a sample QRadar functions rule that uses negative conditions:

```
and when none of <these rules> match in <this many> <minutes> after <these rules> match with the same <event properties>
```

Here are two defined rules in QRadar. The negative conditions are based on these rules:

![Diagram illustrating an event property tests rule to be used for a negative conditions rule.](media/migration-qradar-detection-rules/rule-5-sample-1.png)

![Diagram illustrating a common property tests rule to be used for a negative conditions rule.](media/migration-qradar-detection-rules/rule-5-sample-2.png)

Here's a sample of the negative conditions rule based on the two previously defined QRadar rules (Test2 and Test6):

![Diagram illustrating a functions rule with negative conditions.](media/migration-qradar-detection-rules/rule-5-sample-3.png)

### Negative conditions example (KQL)

Here's the negative conditions rule with a `rightanti` join in KQL:

```kusto
let spanoftime = 10m;
let Test2 = (
CommonSecurityLog
| where Protocol !in ("UDP","ICMP")
| where TimeGenerated > ago(spanoftime)
);
let Test6 = (
CommonSecurityLog
| where SourceIP == DestinationIP
);
Test2
| join kind=rightanti Test6 on $left. SourceIP == $right. SourceIP and $left. Protocol ==$right. Protocol
```

### Functions: simple conditions syntax

Here's the QRadar syntax for a functions rule that uses simple conditions:

![Diagram illustrating the syntax of a functions rule that uses simple conditions.](media/migration-qradar-detection-rules/rule-6-syntax.png)

### Simple conditions example (QRadar)

Here's the syntax for a sample QRadar functions rule that uses simple conditions.:

```
and when an event matches <any|all> of the following <rules>
```

Here's the sample rule in QRadar:

![Diagram illustrating a functions rule with simple conditions.](media/migration-qradar-detection-rules/rule-6-sample-1.png)

### Simple conditions example (KQL)

Here's the simple conditions rule in KQL:

```kusto
CommonSecurityLog
| where Protocol !in ("UDP","ICMP") or SourceIP == DestinationIP
```

### IP/port tests syntax

Here's the QRadar syntax for an IP/port tests rule:

![Diagram illustrating the syntax of an IP/port tests rule.](media/migration-qradar-detection-rules/rule-7-syntax.png)

### IP/port tests: Source port example (QRadar)

Here's the syntax for a sample QRadar rule specifying a source port:

```
and when the source port is one of the following <ports>
```

Here's the sample rule in QRadar:

![Diagram illustrating a rule that specifies a source port.](media/migration-qradar-detection-rules/rule-7-sample-1-port.png)

### IP/port tests: Source port example (KQL)

Here's the IP/port tests rule with a source port filter in KQL:

```kusto
CommonSecurityLog
| where SourcePort == 20
```

### IP/port tests: Source IP example (QRadar)

Here's the syntax for a sample QRadar rule specifying a source IP:

```
and when the source IP is one of the following <IP addresses>
```

Here's the sample rule in QRadar:

![Diagram illustrating a rule that specifies a source IP address.](media/migration-qradar-detection-rules/rule-7-sample-2-ip.png)

### IP/port tests: Source IP example (KQL)

Here's the IP/port tests rule with a source IP filter in KQL:

```kusto
CommonSecurityLog
| where SourceIP in ("10.1.1.1","10.2.2.2")
```

### Log source tests syntax

Here's the QRadar syntax for a log source tests rule:

![Diagram illustrating the syntax of a log source tests rule.](media/migration-qradar-detection-rules/rule-8-syntax.png)

### Log source example (QRadar)

Here's the syntax for a sample QRadar rule specifying log sources:

```
and when the event(s) were detected by one or more of these <log source types>
```

Here's the sample rule in QRadar:

![Diagram illustrating a rule that specifies log sources.](media/migration-qradar-detection-rules/rule-8-sample-1.png)

### Log source example (KQL)

Here's the log source tests rule in KQL.

```kusto
OfficeActivity
| where OfficeWorkload == "Exchange"
```