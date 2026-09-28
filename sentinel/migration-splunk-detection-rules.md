---
layout: Conceptual
title: Migrate Splunk detection rules to Microsoft Sentinel - Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/migration-splunk-detection-rules
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
description: Learn how to identify, compare, and migrate Splunk detection rules to Microsoft Sentinel analytics rules, including use of the SIEM migration experience to find out-of-the-box matches.
ms.author: guywild
author: guywi-ms
ms.reviewer: soulisabag
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: f2733f7f-99f2-d380-87ee-bdee41de0a58
document_version_independent_id: b5f4bfc6-2f57-4213-e034-f2679e618772
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/migration-splunk-detection-rules.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/migration-splunk-detection-rules
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/migration-splunk-detection-rules.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 3d2f747a-54a2-5311-389f-fa610ea81787
---

# Migrate Splunk detection rules to Microsoft Sentinel - Microsoft Sentinel | Microsoft Learn

Splunk detection rules are security information and event management (SIEM) components that compare to analytics rules in Microsoft Sentinel. This article describes the concepts used to identify, compare, and migrate Splunk detection rules to Microsoft Sentinel. The best way to migrate Splunk detection rules to Microsoft Sentinel is to start with the [SIEM migration experience](siem-migration), which identifies out-of-the-box (OOTB) analytics rules for automatic translation.

If you want to migrate your Splunk Observability deployment, learn more about how to [migrate from Splunk to Azure Monitor Logs](/en-us/azure/azure-monitor/logs/migrate-splunk-to-azure-monitor-logs).

## Audit rules

Microsoft Sentinel uses machine learning analytics to create high-fidelity and actionable incidents. Some of your existing Splunk detections may be redundant in Microsoft Sentinel, so don't migrate all Splunk detections blindly. Review the following rule-auditing considerations as you identify your existing detection rules.

- Make sure to select use cases that justify rule migration, considering business priority and efficiency.
- Check that you [understand Microsoft Sentinel rule types](detect-threats-built-in).
- Check that you understand the rule terminology.
- Review outdated rules that don't have alerts for the past 6-12 months, and determine whether they're still relevant.
- Eliminate low-level threats or alerts that you routinely ignore.
- Microsoft Sentinel Analytics require that the data type is present in the Log Analytics workspace before a rule is enabled. Confirm that your required data sources are connected and review your data connection methods. Revisit data collection conversations to ensure data depth and breadth across the use cases you plan to detect. Then use the [SIEM migration experience](siem-migration) to ensure the data sources are mapped appropriately.

## Migrate rules

After you identify the Splunk detections to migrate, review the following migration-process considerations:

- Compare the existing functionality of Microsoft Sentinel's OOTB analytics rules with your current use cases. Use the [SIEM migration experience](siem-migration) to see which Splunk detections are automatically converted to OOTB templates.
- Translate detections that don't align to OOTB analytics rules. The best way to translate Splunk detections automatically is with the [SIEM migration experience](siem-migration).
- Discover more algorithms for your use cases by exploring community resources such as the [SOC Prime Threat Detection Marketplace](https://my.socprime.com/platform-overview/).
- Manually translate detections if built-in rules aren't available or aren't automatically translated. Create the new KQL queries and review the rules mapping.

For more information, see [best practices for migrating detection rules](https://techcommunity.microsoft.com/t5/microsoft-sentinel-blog/best-practices-for-migrating-detection-rules-from-arcsight/ba-p/2216417).

### Rule migration steps

Follow these steps to validate, translate, and test each Splunk detection rule during migration to Microsoft Sentinel.

1. Verify that you have a testing system in place for each rule you want to migrate.

    1. **Prepare a validation process** for your migrated rules, including full test scenarios and scripts.
    2. **Ensure that your team has useful resources** to test your migrated rules.
    3. **Confirm that you have the required data sources connected,** and review your data connection methods.
2. Verify whether your detections are available as OOTB templates in Microsoft Sentinel:

    - **Use the SIEM migration experience** to automate translation and installation of the OOTB templates.

        For more information, see [Use the SIEM migration experience](siem-migration).
    - **If you have use cases not reflected in the detections**, create rules for your own workspace with OOTB rule templates.

        In Microsoft Sentinel, go to the **Content hub**.

        Filter **Content type** for **Analytics rule** templates.

        Find and **Install/Update** each corresponding Content hub solution or standalone analytics rule template.

        For more information, see [Detect threats out-of-the-box](detect-threats-built-in).
    - **If you have detections that aren't covered by Microsoft Sentinel's OOTB rules**, first try the [SIEM migration experience](siem-migration) for automatic translation.
    - **If neither the OOTB rules nor the SIEM migration completely translate the detection**, create the rule manually. Use the following steps to create your rule:

        1. **Identify the data sources you want to use in your rule**. Identify the Microsoft Sentinel tables you want to query by creating a mapping table between data sources and data tables.
        2. **Identify any attributes, fields, or entities** in your data that you want to use in your rules.
        3. **Identify your rule criteria and logic**. When identifying your rule criteria and logic, consider using rule templates as samples for how to construct your KQL queries.

            Consider filters, correlation rules, active lists, reference sets, watchlists, detection anomalies, aggregations, and so on. You might use references provided by your legacy SIEM to understand how to best map your query syntax.
        4. **Identify the trigger condition and rule action, and then construct and review your KQL query**. When reviewing your query, consider KQL optimization guidance resources.
3. Test the rule with each of your relevant use cases. If it doesn't provide expected results, review and edit the KQL and test it again.
4. When you're satisfied, consider the rule migrated. Create a playbook for your rule action as needed. For more information, see [Automate threat response with playbooks in Microsoft Sentinel](automate-responses-with-playbooks).

Learn more about analytics rules:

- [**Create custom analytics rules to detect threats**](detect-threats-custom). Use [alert grouping](detect-threats-custom#alert-grouping) to reduce alert fatigue by grouping alerts that occur within a given timeframe.
- [**Map data fields to entities in Microsoft Sentinel**](map-data-fields-to-entities) to enable SOC engineers to define entities as part of the evidence to track during an investigation. Entity mapping also makes it possible for SOC analysts to take advantage of an intuitive [investigation graph] (investigate-cases.md#use-the-investigation-graph-to-deep-dive) that can help reduce time and effort.
- [**Investigate incidents with UEBA data**](investigate-with-ueba), as an example of how to use evidence to surface events, alerts, and any bookmarks associated with a particular incident in the incident preview pane.
- [**Kusto Query Language (KQL)**](/en-us/kusto/query/?view=microsoft-sentinel&amp;preserve-view=true), which you can use to send read-only requests to your [Log Analytics](/en-us/azure/azure-monitor/logs/log-analytics-tutorial) database to process data and return results. KQL is also used across other Microsoft services, such as [Microsoft Defender for Endpoint](https://www.microsoft.com/microsoft-365/security/endpoint-defender) and [Application Insights](/en-us/azure/azure-monitor/app/app-insights-overview).

## Compare rule terminology

The following comparison table clarifies how a KQL-based rule in Microsoft Sentinel corresponds to an SPL-based detection in Splunk.

| - | Splunk | Microsoft Sentinel |
| --- | --- | --- |
| **Rule type** | • Scheduled• Real-time | • Scheduled query• Fusion• Microsoft Security• Machine Learning (ML) Behavior Analytics |
| **Criteria** | Define in SPL | Define in KQL |
| **Trigger condition** | • Number of results• Number of hosts• Number of sources• Custom | Threshold: Number of query results |
| **Action** | • Add to triggered alerts• Log Event• Output results to look up• And more | • Create alert or incident• Integrates with Logic Apps |

## Map and compare rule samples

Use the SPL-to-KQL sample tables and examples in this section to compare and map rules from Splunk to Microsoft Sentinel in various scenarios.

### Compare common Splunk search commands with KQL examples

This table maps common SPL search commands to their KQL equivalents in Microsoft Sentinel.

| SPL command | Description | KQL operator | KQL example |
| --- | --- | --- | --- |
| `chart/ timechart` | Returns results in a tabular output for time-series charting. | [render operator](/en-us/kusto/query/render-operator?view=microsoft-sentinel&amp;preserve-view=true) | `… | render timechart` |
| `dedup` | Removes subsequent results that match a specified criterion. | • [distinct](/en-us/kusto/query/distinct-operator?view=microsoft-sentinel&amp;preserve-view=true)• [summarize](/en-us/kusto/query/summarize-operator?view=microsoft-sentinel&amp;preserve-view=true) | `… | summarize by Computer, EventID` |
| `eval` | Calculates an expression. Learn about [common `eval` commands](https://github.com/Azure/Azure-Sentinel/blob/master/Tools/RuleMigration/SPL%20to%20KQL.md#common-eval-commands). | [extend](/en-us/kusto/query/extend-operator?view=microsoft-sentinel&amp;preserve-view=true) | `T | extend duration = endTime - startTime` |
| `fields` | Removes fields from search results. | • [project](/en-us/kusto/query/project-operator?view=microsoft-sentinel&amp;preserve-view=true)• [project-away](/en-us/kusto/query/project-away-operator?view=microsoft-sentinel&amp;preserve-view=true) | `T | project cost=price*quantity, price` |
| `head/tail` | Returns the first or last N results. | [top](/en-us/kusto/query/top-operator?view=microsoft-sentinel&amp;preserve-view=true) | `T | top 5 by Name desc nulls last` |
| `lookup` | Adds field values from an external source. | • [externaldata](/en-us/kusto/query/externaldata-operator?view=microsoft-sentinel&amp;preserve-view=true)• [lookup](/en-us/kusto/query/lookup-operator?view=microsoft-sentinel&amp;preserve-view=true) | Lookup command KQL example |
| `rename` | Renames a field. Use wildcards to specify multiple fields. | [project-rename](/en-us/kusto/query/project-rename-operator?view=microsoft-sentinel&amp;preserve-view=true) | `T | project-rename new_column_name = column_name` |
| `rex` | Specifies group names using regular expressions to extract fields. | [matches regex](/en-us/kusto/query/regex?view=microsoft-sentinel&amp;preserve-view=true) | `… | where field matches regex "^addr.*"` |
| `search` | Filters results to results that match the search expression. | [search](/en-us/kusto/query/search-operator?view=microsoft-sentinel&amp;preserve-view=true) | `search "X"` |
| `sort` | Sorts the search results by the specified fields. | [sort](/en-us/kusto/query/sort-operator?view=microsoft-sentinel&amp;preserve-view=true) | `T | sort by strlen(country) asc, price desc` |
| `stats` | Provides statistics, optionally grouped by fields. Learn more about [common stats commands](https://github.com/Azure/Azure-Sentinel/blob/master/Tools/RuleMigration/SPL%20to%20KQL.md#common-stats-commands). | [summarize](/en-us/kusto/query/summarize-operator?view=microsoft-sentinel&amp;preserve-view=true) | Stats command KQL example |
| `mstats` | Similar to stats, used on metrics instead of events. | [summarize](/en-us/kusto/query/summarize-operator?view=microsoft-sentinel&amp;preserve-view=true) | Mstats command KQL example |
| `table` | Specifies which fields to keep in the result set, and retains data in tabular format. | [project](/en-us/kusto/query/project-operator?view=microsoft-sentinel&amp;preserve-view=true) | `T | project columnA, columnB` |
| `top/rare` | Displays the most or least common values of a field. | [top](/en-us/kusto/query/top-operator?view=microsoft-sentinel&amp;preserve-view=true) | `T | top 5 by Name desc nulls last` |
| `transaction` | Groups search results into transactions.Transaction command SPL example | Example: [row_window_session](/en-us/kusto/query/row-window-session-function?view=microsoft-sentinel&amp;preserve-view=true) | Transaction command KQL example |
| `eventstats` | Generates summary statistics from fields in your events and saves those statistics in a new field.SPL example | Examples:• [join](/en-us/kusto/query/join-operator?view=microsoft-sentinel&amp;preserve-view=true)• [make_list](/en-us/kusto/query/make-list-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true)• [mv-expand](/en-us/kusto/query/mv-expand-operator?view=microsoft-sentinel&amp;preserve-view=true) | KQL example |
| `streamstats` | Find the cumulative sum of a field.SPL example:`... | streamstats sum(bytes) as bytes _ total \| timechart` | [row_cumsum](/en-us/kusto/query/row-cumsum-function?view=microsoft-sentinel&amp;preserve-view=true) | `...\| serialize cs=row_cumsum(bytes)` |
| `anomalydetection` | Find anomalies in the specified field.SPL example | [series_decompose_anomalies()](/en-us/kusto/query/series-decompose-anomalies-function?view=microsoft-sentinel&amp;preserve-view=true) | KQL example |
| `where` | Filters search results using `eval` expressions. Used to compare two different fields. | [where](/en-us/kusto/query/where-operator?view=microsoft-sentinel&amp;preserve-view=true) | `T | where fruit=="apple"` |

#### `lookup` command: KQL example

This KQL example uses `externaldata` to replicate the SPL `lookup` pattern by filtering users against an external data source.

```kusto
Users 
| where UserID in ((externaldata (UserID:string) [
@"https://storageaccount.blob.core.windows.net/storagecontainer/users.txt" 
h@"?...SAS..." // Secret token to access the blob 
])) | ... 
```

#### `stats` command: KQL example

This KQL example uses `summarize` to count transactions and sum totals, grouped by fruit and month.

```kusto
Sales 
| summarize NumTransactions=count(), 
Total=sum(UnitPrice * NumUnits) by Fruit, 
StartOfMonth=startofmonth(SellDateTime) 
```

#### `mstats` command: KQL example

This KQL example bins metric values into price ranges and counts the records in each range.

```kusto
T | summarize count() by price_range=bin(price, 10.0) 
```

#### `transaction` command: SPL example

This SPL example groups related start and stop events into a single transaction by activity ID.

```spl
sourcetype=MyLogTable type=Event
| transaction ActivityId startswith="Start" endswith="Stop"
| Rename timestamp as StartTime
| Table City, ActivityId, StartTime, Duration
```

#### `transaction` command: KQL example

This KQL example replicates SPL transaction grouping by joining start and stop events on a shared activity ID and calculating the duration.

```kusto
let Events = MyLogTable | where type=="Event";
Events
| where Name == "Start"
| project Name, City, ActivityId, StartTime=timestamp
| join (Events
| where Name == "Stop"
| project StopTime=timestamp, ActivityId)
on ActivityId
| project City, ActivityId, StartTime, 
Duration = StopTime – StartTime
```

Use `row_window_session()` to calculate session start values for a column in a serialized row set.

```kusto
...| extend SessionStarted = row_window_session(
Timestamp, 1h, 5m, ID != prev(ID))
```

#### `eventstats` command: SPL example

This SPL example calculates per-category event counts in one-minute bins and then appends a per-time-bin total using `eventstats`.

```spl
… | bin span=1m _time
|stats count AS count_i by _time, category
| eventstats sum(count_i) as count_total by _time
```

#### `eventstats` command: KQL example

Here's an example with the `join` statement:

```kusto
let binSize = 1h;
let detail = SecurityEvent 
| summarize detail_count = count() by EventID,
tbin = bin(TimeGenerated, binSize);
let summary = SecurityEvent
| summarize sum_count = count() by 
tbin = bin(TimeGenerated, binSize);
detail 
| join kind=leftouter (summary) on tbin 
| project-away tbin1
```

Here's an example with the `make_list` statement:

```kusto
let binSize = 1m;
SecurityEvent
| where TimeGenerated >= ago(24h)
| summarize TotalEvents = count() by EventID, 
groupBin =bin(TimeGenerated, binSize)
|summarize make_list(EventID), make_list(TotalEvents), 
sum(TotalEvents) by groupBin
| mvexpand list_EventID, list_TotalEvents
```

#### `anomalydetection` command: SPL example

This SPL example detects anomalies in historical closing price data over a 10-year period.

```spl
sourcetype=nasdaq earliest=-10y
| anomalydetection Close _ Price
```

#### `anomalydetection` command: KQL example

This KQL example uses time-series analysis functions to detect anomalies in disabled-account sign-in trends over a seven-day lookback period.

```kusto
let LookBackPeriod= 7d;
let disableAccountLogon=SignIn
| where ResultType == "50057"
| where ResultDescription has "account is disabled";
disableAccountLogon
| make-series Trend=count() default=0 on TimeGenerated 
in range(startofday(ago(LookBackPeriod)), now(), 1d)
| extend (RSquare,Slope,Variance,RVariance,Interception,
LineFit)=series_fit_line(Trend)
| extend (anomalies,score) = 
series_decompose_anomalies(Trend)
```

### Compare common Splunk `eval` commands with KQL equivalents

This table maps common SPL `eval` functions to their KQL equivalents in Microsoft Sentinel.

| SPL command | Description | SPL example | KQL command | KQL example |
| --- | --- | --- | --- | --- |
| `abs(X)` | Returns the absolute value of X. | `abs(number)` | [`abs()`](/en-us/kusto/query/abs-function?view=microsoft-sentinel&amp;preserve-view=true) | `abs(X)` |
| `case(X,"Y",…)` | Takes pairs of `X` and `Y` arguments, where the `X` arguments are boolean expressions. When evaluated to `TRUE`, the arguments return the corresponding `Y` argument. | SPL example | [`case`](/en-us/kusto/query/case-function?view=microsoft-sentinel&amp;preserve-view=true) | KQL example |
| `ceil(X)` | Ceiling of a number X. | `ceil(1.9)` | [`ceiling()`](/en-us/kusto/query/ceiling-function?view=microsoft-sentinel&amp;preserve-view=true) | `ceiling(1.9)` |
| `cidrmatch("X",Y)` | Identifies IP addresses that belong to a particular subnet. | `cidrmatch``("123.132.32.0/25",ip)` | • [`ipv4_is_match()`](/en-us/kusto/query/ipv4-is-match-function?view=microsoft-sentinel&amp;preserve-view=true)• [ipv6_is_match()](/en-us/kusto/query/ipv6-is-match-function?view=microsoft-sentinel&amp;preserve-view=true) | `ipv4_is_match('192.168.1.1', '192.168.1.255')``== false` |
| `coalesce(X,…)` | Returns the first value that isn't null. | `coalesce(null(), "Returned val", null())` | [`coalesce()`](/en-us/kusto/query/coalesce-function?view=microsoft-sentinel&amp;preserve-view=true) | `coalesce(tolong("not a number"),``tolong("42"), 33) == 42` |
| `cos(X)` | Calculates the cosine of X. | `n=cos(0)` | [cos()](/en-us/kusto/query/cos-function?view=microsoft-sentinel&amp;preserve-view=true) | `cos(X)` |
| `exact(X)` | Evaluates an expression X using double precision floating point arithmetic. | `exact(3.14*num)` | [`todecimal()`](/en-us/kusto/query/todecimal-function?view=microsoft-sentinel&amp;preserve-view=true) | `todecimal(3.14*2)` |
| `exp(X)` | Returns eX. | `exp(3)` | [exp()](/en-us/kusto/query/exp-function?view=microsoft-sentinel&amp;preserve-view=true) | `exp(3)` |
| `if(X,Y,Z)` | If `X` evaluates to `TRUE`, the result is the second argument `Y`. If `X` evaluates to `FALSE`, the result evaluates to the third argument `Z`. | `if(error==200,``"OK", "Error")` | [`iff()`](/en-us/kusto/query/iff-function?view=microsoft-sentinel&amp;preserve-view=true) | KQL example |
| `isbool(X)` | Returns `TRUE` if `X` is boolean. | `isbool(field)` | • [`iff()`](/en-us/kusto/query/iff-function?view=microsoft-sentinel&amp;preserve-view=true)• [`gettype`](/en-us/kusto/query/gettype-function?view=microsoft-sentinel&amp;preserve-view=true) | `iff(gettype(X) =="bool","TRUE","FALSE")` |
| `isint(X)` | Returns `TRUE` if `X` is an integer. | `isint(field)` | • [`iff()`](/en-us/kusto/query/iff-function?view=microsoft-sentinel&amp;preserve-view=true)• [`gettype`](/en-us/kusto/query/gettype-function?view=microsoft-sentinel&amp;preserve-view=true) | KQL example |
| `isnull(X)` | Returns `TRUE` if `X` is null. | `isnull(field)` | [`isnull()`](/en-us/kusto/query/isnull-function?view=microsoft-sentinel&amp;preserve-view=true) | `isnull(field)` |
| `isstr(X)` | Returns `TRUE` if `X` is a string. | `isstr(field)` | • [`iff()`](/en-us/kusto/query/iff-function?view=microsoft-sentinel&amp;preserve-view=true)• [`gettype`](/en-us/kusto/query/gettype-function?view=microsoft-sentinel&amp;preserve-view=true) | KQL example |
| `len(X)` | This function returns the character length of a string `X`. | `len(field)` | [`strlen()`](/en-us/kusto/query/strlen-function?view=microsoft-sentinel&amp;preserve-view=true) | `strlen(field)` |
| `like(X,"y")` | Returns `TRUE` if and only if `X` is like the SQLite pattern in `Y`. | `like(field, "addr%")` | • [`has`](/en-us/kusto/query/has-any-operator?view=microsoft-sentinel&amp;preserve-view=true)• [`contains`](/en-us/kusto/query/datatypes-string-operators?view=microsoft-sentinel&amp;preserve-view=true)• [`startswith`](/en-us/kusto/query/datatypes-string-operators?view=microsoft-sentinel&amp;preserve-view=true)• [matches regex](/en-us/kusto/query/regex?view=microsoft-sentinel&amp;preserve-view=true) | KQL example |
| `log(X,Y)` | Returns the log of the first argument `X` using the second argument `Y` as the base. The default value of `Y` is `10`. | `log(number,2)` | • [`log`](/en-us/kusto/query/log-function?view=microsoft-sentinel&amp;preserve-view=true)• [`log2`](/en-us/kusto/query/log2-function?view=microsoft-sentinel&amp;preserve-view=true)• [`log10`](/en-us/kusto/query/log10-function?view=microsoft-sentinel&amp;preserve-view=true) | `log(X)``log2(X)``log10(X)` |
| `lower(X)` | Returns the lowercase value of `X`. | `lower(username)` | [tolower](/en-us/kusto/query/tolower-function?view=microsoft-sentinel&amp;preserve-view=true) | `tolower(username)` |
| `ltrim(X,Y)` | Returns `X` with the characters in parameter `Y` trimmed from the left side. The default output of `Y` is spaces and tabs. | `ltrim(" ZZZabcZZ ", " Z")` | [`trim_start()`](/en-us/kusto/query/trim-start-function?view=microsoft-sentinel&amp;preserve-view=true) | `trim_start(“ ZZZabcZZ”,” ZZZ”)` |
| `match(X,Y)` | Returns if X matches the regex pattern Y. | `match(field, "^\d{1,3}.\d$")` | [`matches regex`](/en-us/kusto/query/regex?view=microsoft-sentinel&amp;preserve-view=true) | `… | where field matches regex @"^\d{1,3}.\d$")` |
| `max(X,…)` | Returns the maximum value in a column. | `max(delay, mydelay)` | • [`max()`](/en-us/kusto/query/max-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true)• [`arg_max()`](/en-us/kusto/query/arg-max-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true) | `… | summarize max(field)` |
| `md5(X)` | Returns the MD5 hash of a string value `X`. | `md5(field)` | [`hash_md5`](/en-us/kusto/query/hash-md5-function?view=microsoft-sentinel&amp;preserve-view=true) | `hash_md5("X")` |
| `min(X,…)` | Returns the minimum value in a column. | `min(delay, mydelay)` | • [`min_of()`](/en-us/kusto/query/min-of-function?view=microsoft-sentinel&amp;preserve-view=true)• [min()](/en-us/kusto/query/min-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true)• [arg_min](/en-us/kusto/query/arg-min-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true) | KQL example |
| `mvcount(X)` | Returns the number (total) of `X` values. | `mvcount(multifield)` | [`dcount`](/en-us/kusto/query/dcount-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true) | `…| summarize dcount(X) by Y` |
| `mvfilter(X)` | Filters a multi-valued field based on the boolean `X` expression. | `mvfilter(match(email, "net$"))` | [`mv-apply`](/en-us/kusto/query/mv-apply-operator?view=microsoft-sentinel&amp;preserve-view=true) | KQL example |
| `mvindex(X,Y,Z)` | Returns a subset of the multi-valued `X` argument from a start position (zero-based) `Y` to `Z` (optional). | `mvindex( multifield, 2)` | [`array_slice`](/en-us/kusto/query/array-slice-function?view=microsoft-sentinel&amp;preserve-view=true) | `array_slice(arr, 1, 2)` |
| `mvjoin(X,Y)` | Given a multi-valued field `X` and string delimiter `Y`, and joins the individual values of `X` using `Y`. | `mvjoin(address, ";")` | [`strcat_array`](/en-us/kusto/query/strcat-array-function?view=microsoft-sentinel&amp;preserve-view=true) | KQL example |
| `now()` | Returns the current time, represented in Unix time. | `now()` | [`now()`](/en-us/kusto/query/now-function?view=microsoft-sentinel&amp;preserve-view=true) | `now()``now(-2d)` |
| `null()` | Doesn't accept arguments and returns `NULL`. | `null()` | [null](/en-us/kusto/query/scalar-data-types/null-values) | `null` |
| `nullif(X,Y)` | Includes two arguments, `X` and `Y`, and returns `X` if the arguments are different. Otherwise, returns `NULL`. | `nullif(fieldA, fieldB)` | [`iff`](/en-us/kusto/query/iff-function?view=microsoft-sentinel&amp;preserve-view=true) | `iff(fieldA==fieldB, null, fieldA)` |
| `random()` | Returns a pseudo-random number between `0` to `2147483647`. | `random()` | [`rand()`](/en-us/kusto/query/rand-function?view=microsoft-sentinel&amp;preserve-view=true) | `rand()` |
| `relative_ time(X,Y)` | Given an epoch time `X` and relative time specifier `Y`, returns the epoch time value of `Y` applied to `X`. | `relative_time(now(),"-1d@d")` | [unix time](/en-us/kusto/query/datetime-timespan-arithmetic?view=microsoft-sentinel&amp;preserve-view=true#example-unix-time) | KQL example |
| `replace(X,Y,Z)` | Returns a string formed by substituting string `Z` for every occurrence of regular expression string `Y` in string `X`. | Returns date with the month and day numbers switched.For example, for the `4/30/2015` input, the output is `30/4/2009`:`replace(date, "^(\d{1,2})/ (\d{1,2})/", "\2/\1/")` | [`replace()`](/en-us/kusto/query/replace-string-function?view=microsoft-sentinel&amp;preserve-view=true) | KQL example |
| `round(X,Y)` | Returns `X` rounded to the number of decimal places specified by `Y`. The default is to round to an integer. | `round(3.5)` | [`round`](/en-us/kusto/query/round-function?view=microsoft-sentinel&amp;preserve-view=true) | `round(3.5)` |
| `rtrim(X,Y)` | Returns `X` with the characters of `Y` trimmed from the right side. If `Y` isn't specified, spaces and tabs are trimmed. | `rtrim(" ZZZZabcZZ ", " Z")` | [`trim_end()`](/en-us/kusto/query/trim-end-function?view=microsoft-sentinel&amp;preserve-view=true) | `trim_end(@"[ Z]+",A)` |
| `searchmatch(X)` | Returns `TRUE` if the event matches the search string `X`. | `searchmatch("foo AND bar")` | [iff()](/en-us/kusto/query/iff-function?view=microsoft-sentinel&amp;preserve-view=true) | `iff(field has "X","Yes","No")` |
| `split(X,"Y")` | Returns `X` as a multi-valued field, split by delimiter `Y`. | `split(address, ";")` | [`split()`](/en-us/kusto/query/split-function?view=microsoft-sentinel&amp;preserve-view=true) | `split(address, ";")` |
| `sqrt(X)` | Returns the square root of `X`. | `sqrt(9)` | [`sqrt()`](/en-us/kusto/query/sqrt-function?view=microsoft-sentinel&amp;preserve-view=true) | `sqrt(9)` |
| `strftime(X,Y)` | Returns the epoch time value `X` rendered using the format specified by `Y`. | `strftime(_time, "%H:%M")` | [`format_datetime()`](/en-us/kusto/query/format-datetime-function?view=microsoft-sentinel&amp;preserve-view=true) | `format_datetime(time,'HH:mm')` |
| `strptime(X,Y)` | Given a time represented by a string `X`, returns value parsed from format `Y`. | `strptime(timeStr, "%H:%M")` | [format_datetime()](/en-us/kusto/query/format-datetime-function?view=microsoft-sentinel&amp;preserve-view=true) | KQL example |
| `substr(X,Y,Z)` | Returns a substring field `X` from start position (one-based) `Y` for `Z` (optional) characters. | `substr("string", 1, 3)` | [`substring()`](/en-us/kusto/query/substring-function?view=microsoft-sentinel&amp;preserve-view=true) | `substring("string", 0, 3)` |
| `time()` | Returns the wall-clock time with microsecond resolution. | `time()` | [`format_datetime()`](/en-us/kusto/query/format-datetime-function?view=microsoft-sentinel&amp;preserve-view=true) | KQL example |
| `tonumber(X,Y)` | Converts input string `X` to a number, where `Y` (optional, default value is `10`) defines the base of the number to convert to. | `tonumber("0A4",16)` | [`toint()`](/en-us/kusto/query/toint-function?view=microsoft-sentinel&amp;preserve-view=true) | `toint("123")` |
| `tostring(X,Y)` | Description | SPL example | [`tostring()`](/en-us/kusto/query/tostring-function?view=microsoft-sentinel&amp;preserve-view=true) | `tostring(123)` |
| `typeof(X)` | Returns a string representation of the field type. | `typeof(12)` | [`gettype()`](/en-us/kusto/query/gettype-function?view=microsoft-sentinel&amp;preserve-view=true) | `gettype(12)` |
| `urldecode(X)` | Returns the URL `X` decoded. | SPL example | [`url_decode`](/en-us/kusto/query/url-decode-function?view=microsoft-sentinel&amp;preserve-view=true) | KQL example |

#### `case(X,"Y",…)` SPL example

This SPL example returns a different message string based on the HTTP error code.

```SPL
case(error == 404, "Not found",
error == 500,"Internal Server Error",
error == 200, "OK")
```

#### `case(X,"Y",…)` KQL example

This KQL example uses `case()` to assign a message based on the error code value.

```kusto
T
| extend Message = case(error == 404, "Not found", 
error == 500,"Internal Server Error", "OK") 
```

#### `if(X,Y,Z)` KQL example

This KQL example uses `iif()` to label whether a timestamp falls on the current day.

```kusto
iif(floor(Timestamp, 1d)==floor(now(), 1d), 
"today", "anotherday")
```

#### `isint(X)` KQL example

This KQL example checks whether `X` has an integer-compatible type by using `gettype` and `iif`.

```kusto
iif(gettype(X) =="long","TRUE","FALSE")
```

#### `isstr(X)` KQL example

This KQL example checks whether `X` is a string value by using `gettype` and `iif`.

```kusto
iif(gettype(X) =="string","TRUE","FALSE")
```

#### `like(X,"y")` example

These KQL examples show several string-matching operators you can use to replicate SPL `like` pattern matching.

```kusto
… | where field has "addr"

… | where field contains "addr"

… | where field startswith "addr"

… | where field matches regex "^addr.*"
```

#### `min(X,…)` KQL example

These KQL examples show different ways to compute minimum values using `min_of`, `min`, and `arg_min`.

```kusto
min_of (expr_1, expr_2 ...)

…|summarize min(expr)

…| summarize arg_min(Price,*) by Product
```

#### `mvfilter(X)` KQL example

This KQL example uses `mv-apply` to filter and reduce multi-valued content, similar to the SPL `mvfilter` function.

```kusto
T | mv-apply Metric to typeof(real) on 
(
 top 2 by Metric desc
)
```

#### `mvjoin(X,Y)` KQL example

This KQL example uses `strcat_array` to join array elements into a single string with a custom separator.

```kusto
strcat_array(dynamic([1, 2, 3]), "->")
```

#### `relative time(X,Y)` KQL example

This KQL example converts a datetime value to Unix epoch time for relative-time calculations.

```kusto
let toUnixTime = (dt:datetime)
{
(dt - datetime(1970-01-01))/1s 
};
```

#### `replace(X,Y,Z)` KQL example

This KQL example uses `replace()` with a regex pattern to swap the month and day parts of a date string.

```kusto
replace( @'^(\d{1,2})/(\d{1,2})/', @'\2/\1/',date)
```

#### `strptime(X,Y)` KQL example

This KQL example uses `format_datetime` to display only the hours and minutes from a datetime value.

```kusto
format_datetime(datetime('2017-08-16 11:25:10'),
'HH:mm')
```

#### `time()` KQL example

This KQL example formats a datetime value as a time string showing hours, minutes, and seconds.

```kusto
format_datetime(datetime(2015-12-14 02:03:04),
'h:m:s')
```

#### `tostring(X,Y)` description

The SPL `tostring(X,Y)` function converts values to strings and supports several formatting options. It returns a field value of `X` as a string.

- If the value of `X` is a number, `X` is reformatted to a string value.
- If `X` is a boolean value, `X` is reformatted to `TRUE` or `FALSE`.
- If `X` is a number, the second argument `Y` is optional and can either be `hex` (converts `X` to a hexadecimal), `commas` (formats `X` with commas and two decimal places), or `duration` (converts `X` from a time format in seconds to a readable time format: `HH:MM:SS`).

##### `tostring(X,Y)` SPL example

This `tostring` SPL example returns:

```SPL
foo=615 and foo2=00:10:15:

… | eval foo=615 | eval foo2 = tostring(
foo, "duration")
```

#### `urldecode(X)` SPL example

This SPL example decodes a URL-encoded string back to its original form.

```SPL
urldecode("http%3A%2F%2Fwww.splunk.com%2Fdownload%3Fr%3Dheader")
```

### Compare common Splunk `stats` commands with KQL equivalents

This table maps common SPL `stats` aggregation functions to their KQL equivalents in Microsoft Sentinel.

| SPL command | Description | KQL command | KQL example |
| --- | --- | --- | --- |
| `avg(X)` | Returns the average of the values of field `X`. | [avg()](/en-us/kusto/query/avg-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true) | `avg(X)` |
| `count(X)` | Returns the number of occurrences of the field `X`. To indicate a specific field value to match, format `X` as `eval(field="value")`. | [count()](/en-us/kusto/query/count-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true) | `summarize count()` |
| `dc(X)` | Returns the count of distinct values of the field `X`. | [dcount()](/en-us/kusto/query/dcount-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true) | `…\| summarize countries=dcount(country) by continent` |
| `earliest(X)` | Returns the chronologically earliest seen value of `X`. | [arg_min()](/en-us/kusto/query/arg-min-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true) | `… \| summarize arg_min(TimeGenerated, *) by X` |
| `latest(X)` | Returns the chronologically latest seen value of `X`. | [arg_max()](/en-us/kusto/query/arg-max-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true) | `… \| summarize arg_max(TimeGenerated, *) by X` |
| `max(X)` | Returns the maximum value of the field `X`. If the values of `X` are non-numeric, the maximum value is found via alphabetical ordering. | [max()](/en-us/kusto/query/max-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true) | `…\| summarize max(X)` |
| `median(X)` | Returns the middle-most value of the field `X`. | [percentile()](/en-us/kusto/query/percentiles-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true) | `…\| summarize percentile(X, 50)` |
| `min(X)` | Returns the minimum value of the field `X`. If the values of `X` are non-numeric, the minimum value is found via alphabetical ordering. | [min()](/en-us/kusto/query/min-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true) | `…\| summarize min(X)` |
| `mode(X)` | Returns the most frequent value of the field `X`. | [top-hitters()](/en-us/kusto/query/top-hitters-operator?view=microsoft-sentinel&amp;preserve-view=true) | `…\| top-hitters 1 of Y by X` |
| `perc(Y)` | Returns the percentile `X` value of the field `Y`. For example, `perc5(total)` returns the fifth percentile value of a field `total`. | [percentile()](/en-us/kusto/query/percentiles-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true) | `…\| summarize percentile(Y, 5)` |
| `range(X)` | Returns the difference between the maximum and minimum values of the field `X`. | [range()](/en-us/kusto/query/range-function?view=microsoft-sentinel&amp;preserve-view=true) | `range(1, 3)` |
| `stdev(X)` | Returns the sample standard deviation of the field `X`. | [stdev](/en-us/kusto/query/stdev-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true) | `stdev()` |
| `stdevp(X)` | Returns the population standard deviation of the field `X`. | [stdevp()](/en-us/kusto/query/stdevp-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true) | `stdevp()` |
| `sum(X)` | Returns the sum of the values of the field `X`. | [sum()](/en-us/kusto/query/sum-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true) | `sum(X)` |
| `sumsq(X)` | Returns the sum of the squares of the values of the field `X`. |  |  |
| `values(X)` | Returns the list of all distinct values of the field `X` as a multi-value entry. The order of the values is alphabetical. | [make_set()](/en-us/kusto/query/make-set-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true) | `…\| summarize r = make_set(X)` |
| `var(X)` | Returns the sample variance of the field `X`. | [variance](/en-us/kusto/query/variance-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true) | `variance(X)` |