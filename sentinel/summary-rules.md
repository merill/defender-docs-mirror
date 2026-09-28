---
layout: Conceptual
title: Aggregate Microsoft Sentinel data with summary rules | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/summary-rules
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
description: Learn how to aggregate large sets of Microsoft Sentinel data across log tiers with summary rules.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 3a1d6ed1-9043-c0e1-adca-b90bb408289e
document_version_independent_id: a114bb1d-c214-9a56-b484-0d484465f647
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/summary-rules.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/summary-rules
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/summary-rules.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 8fceff5b-c730-099f-ec6b-2f21fff2d8e8
---

# Aggregate Microsoft Sentinel data with summary rules | Microsoft Learn

Use [summary rules](/en-us/azure/azure-monitor/logs/summary-rules) in Microsoft Sentinel to aggregate large sets of data in the background for a smoother security operations experience across all log tiers. Summary data is precompiled in custom log tables and provide fast query performance, including queries run on data derived from [low-cost log tiers](billing#data-lake-tier). Summary rules can help optimize your data for:

- **Analysis and reports**, especially over large data sets and time ranges, as required for security and incident analysis, month-over-month or annual business reports, and so on.
- **Cost savings** on verbose logs, which you can retain for as little or as long as you need in a less expensive log tier, and send as summarized data only to an Analytics table for analysis and reports.
- **Security and data privacy**, by removing or obfuscating privacy details in summarized shareable data and limiting access to tables with raw data.

Microsoft Sentinel stores summary rule results in custom tables with the **Analytics** data plan. For more information on data plans and storage costs, see [Log table plans](/en-us/azure/azure-monitor/logs/basic-logs-configure).

This article explains how to create summary rules, deploy pre-built templates, and review common usage scenarios in Microsoft Sentinel.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline). Starting in **July 2025**, many new customers are [automatically onboarded and redirected to the Defender portal](overview#changes-for-new-customers-starting-july-2025).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview). For more information, see [It’s Time to Move: Retiring Microsoft Sentinel’s Azure portal for greater security](https://techcommunity.microsoft.com/blog/microsoft-security-blog/planning-your-move-to-microsoft-defender-portal-for-all-microsoft-sentinel-custo/4428613).

## Prerequisites

To create summary rules in Microsoft Sentinel:

- Microsoft Sentinel must be enabled in at least one workspace, and actively consume logs.
- You must be able to access Microsoft Sentinel with [**Microsoft Sentinel Contributor**](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-contributor) permissions. For more information, see [Roles and permissions in Microsoft Sentinel](roles).
- To create summary rules in the Microsoft Defender portal, you must first onboard your workspace to the Defender portal. For more information, see [Connect Microsoft Sentinel to the Microsoft Defender portal](/en-us/azure/sentinel/microsoft-sentinel-onboard).

We recommend that you experiment with your summary rule query on the [Hunts](hunts) page before creating your rule. Verify that the query doesn't reach or near the [summary rules restrictions and limitations](/en-us/azure/azure-monitor/logs/summary-rules#restrictions-and-limitations), and check that the query produces the intended schema and expected results. If the query is close to the query limits, consider using a smaller `binSize` to process less data per bin. You can also modify the query to return fewer records or remove fields with higher volume.

## Create a new summary rule

Create a new summary rule to aggregate a specific large set of data into a dynamic table. Configure your rule frequency to determine how often your aggregated data set is updated from the raw data.

1. Open the Summary rule wizard:

    - In the Defender portal, select **Microsoft Sentinel &gt; Configuration &gt; Summary rules**.
    - In the Azure portal, from the Microsoft Sentinel navigation menu, under **Configuration**, select **Summary rules**. For example:

        [![Screenshot of the Summary rules page in the Azure portal.](media/summary-rules/summary-rules-azure.png)](media/summary-rules/summary-rules-azure.png#lightbox)
2. Select **+ Create** and enter the following details:

    - **Name**. Enter a meaningful name for your rule.
    - **Description**. Enter an optional description.
    - **Destination table**. Define the custom log table where your data is aggregated:

        - If you select **Existing custom log table**, select the table you want to use.
        - If you select **New custom log table**, enter a meaningful name for your table. Your full table name uses the following syntax: `<tableName>_CL`.
3. We recommend that you enable **SummaryLogs** diagnostic settings on your workspace to get visibility for historical runes and failures. If **SummaryLogs** diagnostic settings aren't enabled, you're prompted to enable them in the **Diagnostic settings** area.

    If **SummaryLogs** diagnostic settings are already enabled, but you want to modify the settings, select **Configure advanced diagnostic settings**. When you come back to the **Summary rule wizard** page, make sure to select **Refresh** to refresh your setting details.

    Important

    The **SummaryLogs** diagnostic setting has additional costs. For more information, see [Diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/diagnostic-settings?WT.mc_id=Portal-Microsoft_Azure_Monitoring).
4. Select **Next: Set summary logic &gt;** to continue.
5. On the **Set summary logic** page, enter your summary query. For example, to summarize data from Google Cloud Platform, you might want to enter:

    ```kusto
    GCPAuditLogs
    | where ServiceName == 'pubsub.googleapis.com'
    | summarize count() by Severity
    ```

    For for more information, see Sample summary rule scenarios and [Kusto Query Language (KQL) in Azure Monitor](/en-us/azure/azure-monitor/log-query/log-query-overview).
6. Select **Preview results** to show an example of the data you'd collect with the configured query.
7. In the **Query scheduling** area, define the following details:

    - How often you want the rule to run
    - Whether you want the rule to run with any sort of delay, in minutes
    - When you want the rule to start running

    Times defined in the scheduling are based on the `timegenerated` column in your data
8. Select **Next: Review + create &gt;** &gt; **Save** to complete the summary rule.

Existing summary rules are listed on the **Summary rules** page, where you can review your rule status. For each rule, select the options menu at the end of the row to take any of the following actions:

- View the rule's current data in the **Logs** page, as if you were to run the query immediately
- View the run history for the selected rule
- Disable or enable the rule.
- Edit the rule configuration

Warning

Deleting a summary rule is irreversible.

To delete a rule, select the rule row and then select **Delete** in the toolbar at the top of the page.

Note

Azure Monitor also supports creating summary rules via API or an Azure Resource Monitor (ARM) template. For more information, see [Create or update a summary rule](/en-us/azure/azure-monitor/logs/summary-rules?tabs=api).

## Deploy pre-built summary rule templates

Summary rule templates are pre-built summary rules that you can deploy as-is or customize to your needs.

To deploy a summary rule template:

1. Open the **Content hub** and filter **Content type** by **Summary rules** to view the available summary rule templates.

    [![Screenshot of the Content Hub page in Microsoft Sentinel showing summary rule templates.](media/summary-rules/summary-rule-templates-content-hub.png)](media/summary-rules/summary-rule-templates-content-hub.png#lightbox)
2. Select a summary rule template.

    A panel with information about the summary rule template opens, displaying fields such as description, summary query, and destination table.

    [![Screenshot showing the details panel of a summary rule template in Microsoft Sentinel, including fields like description, summary query, and destination table.](media/summary-rules/summary-rule-template-details.png)](media/summary-rules/summary-rule-template-details.png#lightbox)
3. Select **Install** to install the template.
4. Select the **Templates** tab on the **Summary rules** page, and select the summary rule you installed.

    [![A screenshot of the Templates tab of the Summary rules page.](media/summary-rules/summary-rule-template-create.png)](media/summary-rules/summary-rule-template-create.png#lightbox)
5. Select **Create** to open the Summary rule wizard, where all of the fields are prepopulated.
6. Go through the Summary rule wizard and select **Save** to deploy the summary rule.

    For more information about the Summary rule wizard, see Create a new summary rule.

## Sample summary rule scenarios in Microsoft Sentinel

This section reviews common scenarios for creating summary rules in Microsoft Sentinel, and our recommendations for how to configure each rule. For more information and examples, see [Summarize insights from raw data in an Auxiliary table to an Analytics table in Microsoft Sentinel](summary-rules-tutorial) and [Log sources to use for Auxiliary Logs ingestion](basic-logs-use-cases).

### Quickly find a malicious IP address in your network traffic

**Scenario**: You're a threat hunter, and one of your team's goals is to identify all instances of when a malicious IP address interacted in the network traffic logs from an active incident, in the last 90 days.

**Challenge**: Microsoft Sentinel currently ingests multiple terabytes of network logs a day. You need to move through them quickly to find matches for the malicious IP address.

**Solution**: We recommend using summary rules to do the following:

1. **Create a summary data set** for each IP address related to the incident, including the `SourceIP`, `DestinationIP`, `MaliciousIP`, `RemoteIP`, each listing important attributes, such as `IPType`, `FirstTimeSeen`, and `LastTimeSeen`.

    The summary dataset enables you to quickly search for a specific IP address and narrow down the time range where the IP address is found. You can do this even when the searched events happened more than 90 days ago, which is beyond their workspace retention period.

    In this example, configure the summary to run daily, so that the query adds new summary records every day until it expires.
2. **Create an analytics rule** that runs for less than two minutes against the summary dataset, quickly drilling into the specific time range when the malicious IP address interacted with the company network.

    Make sure to configure run intervals of up to five minutes at a minimum, to accommodate different summary payload sizes. This ensures that there's no loss even when there's an event ingestion delay.

    For example:

    ```kusto
    let csl_columnmatch=(column_name: string) {
    summarized_CommonSecurityLog
    | where isnotempty(column_name)
    | extend
        Date = format_datetime(TimeGenerated, "yyyy-MM-dd"),
        IPaddress = column_ifexists(column_name, ""),
        FieldName = column_name
    | extend IPType = iff(ipv4_is_private(IPaddress) == true, "Private", "Public")
    | where isnotempty(IPaddress)
    | project Date, TimeGenerated, IPaddress, FieldName, IPType, DeviceVendor
    | summarize count(), FirstTimeSeen = min(TimeGenerated), LastTimeSeen = min(TimeGenerated) by Date, IPaddress, FieldName, IPType, DeviceVendor
    };
    union csl_columnmatch("SourceIP")
        , csl_columnmatch("DestinationIP") 
        , csl_columnmatch("MaliciousIP")
        , csl_columnmatch("RemoteIP")
    // Further summarization can be done per IPaddress to remove duplicates per day on larger timeframe for the first run
    | summarize make_set(FieldName), make_set(DeviceVendor) by IPType, IPaddress
    ```
3. **Run a subsequent search or correlation with other data** to complete the attack story.

### Generate alerts on threat intelligence matches against network data

Generate alerts on threat intelligence matches against noisy, high volume, and low-security value network data.

**Scenario**: You need to build an analytics rule for firewall logs to match domain names in the system that have been visited against a threat intelligence domain name list.

Most of the data sources are raw logs that are noisy and have high volume, but have lower security value, including IP addresses, Azure Firewall traffic, Fortigate traffic, and so on. There's a total volume of about 1 TB per day.

**Challenge**: Creating separate rules requires multiple logic apps, requiring extra setup and maintenance overhead and costs.

**Solution**: We recommend using summary rules to do the following:

1. **Create a summary rule**:

    1. Extend your query to extract key fields, such as the source address, destination address, and destination port from the **CommonSecurityLog\_CL** table, which is the **CommonSecurityLog** with the Auxiliary plan.
    2. Perform an inner lookup against the active Threat Intelligence Indicators to identify any matches with our source address. This allows you to cross-reference your data with known threats.
    3. Project relevant information, including the time generated, activity type, and any malicious source IPs, along with the destination details. Set the frequency you want the query to run, and the destination table, such as **MaliciousIPDetection** . The results in this table are in the analytic tier and are charged accordingly.
2. **Create an alert**:

    Creating an analytics rule in Microsoft Sentinel that alerts based on results from the **MaliciousIPDetection** table. Creating an analytics rule is crucial for proactive threat detection and incident response.

**Sample summary rule**:

```kusto
CommonSecurityLog_CL​
| extend sourceAddress = tostring(parse_json(Message).sourceAddress), destinationAddress = tostring(parse_json(Message).destinationAddress), destinationPort = tostring(parse_json(Message).destinationPort)​
| lookup kind=inner (ThreatIntelligenceIndicator | where Active == true ) on $left.sourceAddress == $right.NetworkIP​
| project TimeGenerated, Activity, Message, DeviceVendor, DeviceProduct, sourceMaliciousIP =sourceAddress, destinationAddress, destinationPort
```