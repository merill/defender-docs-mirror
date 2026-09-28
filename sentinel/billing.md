---
layout: Conceptual
title: Plan costs and understand pricing and billing - Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/billing
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
description: Learn how to plan your Microsoft Sentinel costs, and understand pricing and billing using the pricing calculator and other methods.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: daniha
ms.topic: concept-article
ms.date: 2026-04-01T00:00:00.0000000Z
ms.collection: usx-security
ms.custom:
- subject-cost-optimization
- sfi-image-nochange
locale: en-us
document_id: 65112a4d-379a-80c5-d13d-7eb5929c98ca
document_version_independent_id: ff75da1d-b798-c06b-c17d-1e031a2b18be
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/billing.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/billing
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/billing.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 8867cd5c-9fca-8523-20e6-9cc30a8e885b
---

# Plan costs and understand pricing and billing - Microsoft Sentinel | Microsoft Learn

To estimate your expected Microsoft Sentinel costs, use the [Microsoft Sentinel cost estimator tool,](https://microsoft.com/en-us/security/pricing/microsoft-sentinel/cost-estimator) and [work directly with a Security sales specialist](https://aka.ms/contactsecuritysaleslink) for a custom quote or additional guidance.

Costs for Microsoft Sentinel are only a portion of the monthly costs in your Azure bill. Although this article explains how to plan costs and understand the billing for Microsoft Sentinel, you're billed for all Azure services and resources your Azure subscription uses, including Partner services.

This article is part of the [Deployment guide for Microsoft Sentinel](deploy-overview).

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Free trial

Enable Microsoft Sentinel on an Azure Monitor Log Analytics workspace and the first 10 GB/day ingested using the Analytics logs plan is free for 31 days. The cost for both Log Analytics data ingestion and Microsoft Sentinel analysis charges up to the 10 GB/day limit, are waived during the 31-day trial period. This free trial is subject to a 20 workspace limit per Azure tenant.

See the [Microsoft Sentinel pricing](https://azure.microsoft.com/pricing/details/azure-sentinel) page for information on how usage beyond these limits is charged. Charges related to extra capabilities for [automation](automation) and [bring your own machine learning](bring-your-own-ml) are still applicable during the free trial, and any Microsoft Sentinel data lake related charges.

During your free trial, find resources for cost management, training, and more on the [**News & guides &gt; Free trial**](https://portal.azure.com/#view/Microsoft_Azure_Security_Insights/MainMenuBlade/%7E/NewsAndGuides) tab in Microsoft Sentinel on the Azure portal. This tab also displays details about the dates of your free trial, and how many days left until the trial expires.

## Understand the full billing model for Microsoft Sentinel

Microsoft Sentinel offers a flexible and predictable pricing model. For more information, see the [Microsoft Sentinel pricing page](https://azure.microsoft.com/pricing/details/azure-sentinel/). Workspaces older than July 2023 might have Log Analytics workspace charges separate from Microsoft Sentinel in a classic pricing tier. For the related Log Analytics charges, see [Azure Monitor Log Analytics pricing](https://azure.microsoft.com/pricing/details/log-analytics/).

Microsoft Sentinel runs on Azure infrastructure that accrues costs when you deploy new resources. It's important to understand that there could be other, extra infrastructure costs that might accrue.

### How you're charged for Microsoft Sentinel

Pricing is based on the tier that the data is ingested into. For more information on tiers and plans, see [Data tiers in Microsoft Sentinel](log-plans).

#### Analytics tier

There are two ways to pay for the analytics tier: **pay-as-you-go** and **commitment tiers**.

- **Pay-as-you-go** is the default model, based on the actual data volume stored and optionally for data retention beyond 90 days. Data volume is measured in GB (10^9^ bytes).
- Log Analytics and Microsoft Sentinel have **commitment tier** pricing, formerly called Capacity Reservations. These pricing tiers are combined into simplified pricing tiers that are more predictable and offer substantial savings compared to **pay-as-you-go** pricing.

    **Commitment tier** pricing starts at 100 GB per day. Any usage above the commitment level is billed at the Commitment tier rate you selected. For example, a Commitment tier of **100 GB per day** bills you for the committed 100-GB data volume, plus any extra GB/day at the discounted effective rate for that tier. The **Effective Per GB Price** is simply the **Microsoft Sentinel Price** divided by the **Tier** GB per day quantity. For more information, see [Microsoft Sentinel pricing](https://azure.microsoft.com/pricing/details/microsoft-sentinel/).

    Increase your Commitment tier anytime to optimize costs as your data volume increases. Lowering the Commitment tier is only allowed every 31 days. To see your current Microsoft Sentinel pricing tier, select **Settings** in Microsoft Sentinel, and then select the **Pricing** tab. Your current pricing tier is marked as **Current tier**.

    To set and change your Commitment tier, see [Set or change pricing tier](billing-reduce-costs#set-or-change-pricing-tier). Switch any workspaces older than July 2023 to the simplified pricing tiers experience to unify billing meters. Or, continue to use the classic pricing tiers that separate out the Log Analytics pricing from the classic Microsoft Sentinel classic pricing.

#### Data lake tier

To learn more about the Microsoft Sentinel data lake, see [Microsoft Sentinel data lake](datalake/sentinel-lake-overview).

The data lake tier incurs charges based on usage of various data lake capabilities.

- **Data lake ingestion** is charged per GB for all data ingested into tables with retention set to data lake tier only. Data lake ingestion charges don't apply when data is ingested into tables with retention set to include both analytic and data lake tiers.
- **Data processing** is charged per GB for data ingested into tables with retention set to data lake tier only. It supports transformations like redaction, splitting, filtering, and normalization. Data processing charges don't apply when data is ingested into tables with retention set to include both analytic and data lake tiers.
- **Data lake storage** charges are applied per GB per month for any data that remains in the data lake tier after the analytic tier retention period ends. Charges are based on a simple and uniform data compression rate of 6:1. For example, if you retain 600 GB of raw data, it's billed as 100 GB of compressed data.
- **Data lake query** charges apply per GB of uncompressed data scanned using Kusto Query Language (KQL) queries or KQL jobs.
- **Advanced data insights** charges apply per compute hour used when using within notebook sessions, running notebook jobs, or building nodes and edges for custom graphs. Compute hours are calculated by multiplying the number of cores in the pool selected for the notebook with the amount of time a session was active or a job was running. Data lake notebook sessions and jobs are available in pools of 12, 32, and 80 vCores.

Once onboarded, usage from Microsoft Sentinel workspaces begins to be billed through the previously described meters rather than existing long-term retention (formerly known as Archive), search, or auxiliary logs ingestion meters.

### Microsoft Sentinel graph

#### Embedded graphs in Defender and Purview portals

Hunting graph and blast radius visualizations in the Microsoft Defender portal, along with Insider Risk Management and Data Security Investigations in the Microsoft Purview portal, don't incur any billing or consumption charges. To learn more about the Microsoft Purview and Defender graphs powered by Sentinel, see [Microsoft Sentinel graph](/en-us/azure/sentinel/datalake/sentinel-graph-overview?tabs=defender).

Accessing Defender and Purview graphs through the MCP graph tool collection results in additional charges.

#### Custom graphs

Sentinel custom graph billing is consumption based, with graph operations charged per compute hour. To learn more about the Microsoft Sentinel custom graphs, see [Custom graphs](/en-us/azure/sentinel/datalake/custom-graphs-overview).

The following custom graph operations are billed per compute hour under the graph meter:

- Creating a graph using notebooks in Visual Studio Code.
- Querying a graph using notebooks in Visual Studio Code.
- Querying a graph using Sentinel graphs experiences via Defender portal.
- Querying a graph using Graph Query APIs.
- Querying a graph using Sentinel MCP graph tool collection.

#### Graph charges

Graph charges are calculated as core hours times execution time multiplied by the number of vCores in the selected SKU times the Sentinel graph meter price. There's a single graph SKU option, which uses 49 vCores for graph build operations and 6 vCores for graph queries, with a minimum query execution time of one minute.

For example, when you run a Notebook job for one hour and use graph APIs to build a graph that takes five minutes, the graph cost is calculated as:

`cost = 49 × (Price per vCore hour) × (5/60)`

Similarly, if your graph queries take one minute to complete, the cost is determined as:

`cost = 6 × (Price per vCore hour) × (1/60)`

Any notebook/Spark compute and Data lake storage consumed for data transformations to build node and edges for the graph is billed independently per existing Sentinel data lake meters (Data lake storage and Advanced Data Insights).

You can monitor usage for custom graphs by using [Microsoft Sentinel cost management in the Microsoft Defender portal](billing-monitor-costs#microsoft-sentinel-cost-management-in-the-microsoft-defender-portal).

#### Sentinel Model Context Protocol (MCP) server

Sentinel MCP server is an interface layer that exposes Sentinel platform capabilities to AI agents. There's no extra cost for using the MCP server itself. MCP tools use underlying Sentinel platform services, such as data lake queries or graph operations, which are billed based on their respective meters. In addition, certain tools, such as entity analyzer, may consume [Security Compute Units (SCUs)](/en-us/copilot/security/manage-usage) when AI reasoning execution is required. Customers are charged only for the underlying platform services and compute they consume.

##### Microsoft Sentinel MCP data lake tools

To learn more about data lake tools, see [Data exploration tool collection in Microsoft Sentinel MCP server](/en-us/azure/sentinel/datalake/sentinel-mcp-data-exploration-tool#execute-kql-kusto-query-language-query-on-microsoft-sentinel-data-lake-query_lake).

Installing and configuring the Microsoft Sentinel's unified MCP server carries no cost. However, using the tools to search and retrieve data by using Kusto Query Language (KQL) queries from Microsoft Sentinel data lake invokes the data lake query meter. To learn more, see [Microsoft Sentinel data lake’s pricing](/en-us/azure/sentinel/billing?tabs=simplified%2Ccommitment-tiers).

##### Microsoft Sentinel MCP entity analyzer

To learn more about the entity analyzer, see [Entity analyzer](/en-us/azure/sentinel/datalake/sentinel-mcp-data-exploration-tool#entity-analyzer).

Customers are charged for the Security Compute Units (SCUs) used for AI reasoning that generates the entity risk analysis, which is based on prevalence, threat intelligence, and relationships.

Existing Security Copilot entitlements apply. Any usage that exceeds your Microsoft 365 E5 entitlement incurs additional charges. SCU overages are billed only when usage exceeds your provisioned amount, and customers are charged only for the SCUs consumed. For more information, see [Sentinel MCP billing](/en-us/azure/sentinel/datalake/sentinel-mcp-billing) and [Get started with Microsoft Security Copilot](/en-us/copilot/security/get-started-security-copilot) for SCUs information.

In addition, when using entity analyzer, customers are charged for the KQL queries executed against the Microsoft Sentinel data lake.

##### Microsoft Sentinel MCP triage tool

To learn more about the triage tool, see [Triage tool collection](/en-us/azure/sentinel/datalake/sentinel-mcp-triage-tool).

Installing, configuring, and using the triage tool carries no cost, provided you're onboarded to the required products and services. You can get access to triage at no additional charge when Microsoft Defender, Microsoft Defender for Endpoint, or Microsoft Sentinel is set up in the Microsoft Defender portal.

##### Microsoft Sentinel MCP graph tool

To learn more about the graph tool, see [Graph tools](/en-us/azure/sentinel/datalake/sentinel-mcp-data-exploration-tool#graph-tools-preview).

Installing and configuring the Microsoft Sentinel MCP graph tools doesn't incur any cost. Charges apply only when the tools are used to query the graph, which triggers the graph meter.

### Understand your Microsoft Sentinel bill

Billable meters are the individual components of your service that appear on your bill and are shown in Microsoft Cost Management. At the end of your billing cycle, the charges for each meter are summed. Your bill or invoice shows a section for all Microsoft Sentinel costs. There's a separate line item for each meter.

To see your Azure bill, select **Cost Analysis** in the left navigation of **Cost Management**. On the **Cost analysis** screen, find and select the **Invoice details** from **All views**. To understand the access level required to view billing information, see [Manage access to billing information for Azure](/en-us/azure/cost-management-billing/manage/manage-billing-access).

The costs shown in the following image are for example purposes only. They're not intended to reflect actual costs. Starting July 1, 2023, legacy pricing tiers are prefixed with **Classic**.

[![Screenshot showing the Microsoft Sentinel section of a sample Azure bill, to help you estimate costs.](media/billing/sample-bill-classic.png)](media/billing/sample-bill-classic.png#lightbox)

Microsoft Sentinel and Log Analytics charges might appear on your Azure bill as separate line items based on your selected pricing plan. Simplified pricing tiers are represented as a single `sentinel` line item for the pricing tier. Ingestion and analysis are billed on a daily basis. If your workspace exceeds its Commitment tier usage allocation in any given day, the Azure bill shows one line item for the Commitment tier with its associated fixed cost, and a separate line item for the cost beyond the Commitment tier, billed at the same effective Commitment tier rate.

# [Simplified](#tab/simplified)
The following tabs show how Microsoft Sentinel costs appear in the **Service name** and **Meter** columns of your Azure bill depending on your simplified pricing tier.

# [Classic](#tab/classic)
The following tabs show how Microsoft Sentinel and Log Analytics costs appear in the **Service name** and **Meter** columns of your Azure bill depending on your classic pricing tier.

---

# [Commitment tiers](#tab/commitment-tiers/simplified)
If you're billed at the simplified Commitment tier rate, this table shows how Microsoft Sentinel costs appear in the **Service name** and **Meter** columns of your Azure bill.

| Cost description | Service name | Meter |
| --- | --- | --- |
| Microsoft Sentinel Commitment tier | `Sentinel` | **`n` GB commitment tier** |
| Microsoft Sentinel Commitment tier overage | `Sentinel` | **Analysis** |

# [Commitment tiers](#tab/commitment-tiers/classic)
If you're billed at the classic Commitment tier rate, this table shows how Microsoft Sentinel and Log Analytics costs appear in the **Service name** and **Meter** columns of your Azure bill.

| Cost description | Service name | Meter |
| --- | --- | --- |
| Microsoft Sentinel Commitment tier | `Sentinel` | **Classic `n` GB commitment tier** |
| Log Analytics Commitment tier | `Azure Monitor` | **`n` GB commitment tier** |
| Microsoft Sentinel Commitment tier overage | `Sentinel` | **Classic Analysis** |
| Log Analytics over the Commitment tier | `Log Analytics` | **Data Ingestion** |

# [Pay-as-you-go](#tab/pay-as-you-go/simplified)
If you're billed at the simplified pay-as-you-go rate, this table shows how Microsoft Sentinel costs appear in the **Service name** and **Meter** columns of your Azure bill.

| Cost description | Service name | Meter |
| --- | --- | --- |
| Pay-as-you-go | `Sentinel` | **Pay-as-you-go Analysis** |
| Basic logs data analysis | `Sentinel` | **Basic Logs Analysis** |
| Auxiliary logs data analysis | `Sentinel` | **Auxiliary Logs Analysis** |

# [Pay-as-you-go](#tab/pay-as-you-go/classic)
If you're billed at classic pay-as-you-go rate, this table shows how Microsoft Sentinel and Log Analytics costs appear in the **Service name** and **Meter** columns of your Azure bill.

| Cost description | Service name | Meter |
| --- | --- | --- |
| Pay-as-you-go | `Sentinel` | **Classic Pay-as-you-go Analysis** |
| Pay-as-you-go | `Log Analytics` | **Pay-as-you-go Data Ingestion** |
| Basic logs data analysis | `Sentinel` | **Classic Basic Logs Analysis** |
| Basic logs data ingestion | `Azure Monitor` | **Basic Logs Data Ingestion** |
| Auxiliary logs data analysis | `Sentinel` | **Classic Auxiliary Logs Analysis** |
| Auxiliary logs data ingestion | `Azure Monitor` | **Basic Auxiliary Data Ingestion** |

# [Free data meters](#tab/free-data-meters/simplified)
This table shows how Microsoft Sentinel and Log Analytics no charge costs appear in the **Service name** and **Meter** columns of your Azure bill for free data services when billing is at a simplified pricing tier. For more information, see [View Data Allocation Benefits](/en-us/azure/azure-monitor/cost-usage#view-data-allocation-benefits).

| Cost description | Service name | Meter |
| --- | --- | --- |
| Microsoft Sentinel Free Trial – Sentinel Analysis | `Sentinel` | **Free trial Analysis** |
| Microsoft Defender XDR Benefit – Data Analysis | `Sentinel` | **Free Benefit - M365 Defender Analysis** |

# [Free data meters](#tab/free-data-meters/classic)
This table shows how Microsoft Sentinel and Log Analytics no charge costs appear in the **Service name** and **Meter** columns of your Azure bill for free data services when billing is at a classic pricing tier. For more information, see [View Data Allocation Benefits](/en-us/azure/azure-monitor/cost-usage#view-data-allocation-benefits).

| Cost description | Service name | Meter |
| --- | --- | --- |
| Microsoft Sentinel Free Trial – Log Analytics data ingestion | `Azure Monitor` | **Free Benefit - Az Sentinel Trial Data Ingestion** |
| Microsoft Sentinel Free Trial – Sentinel Analysis | `Sentinel` | **Free trial Analysis** |
| Microsoft Defender XDR Benefit – Data Ingestion | `Azure Monitor` | **Free Benefit - M365 Defender Data Ingestion** |
| Microsoft Defender XDR Benefit – Data Analysis | `Sentinel` | **Free Benefit - M365 Defender Analysis** |

---

Learn how to [view and download your Azure bill](/en-us/azure/cost-management-billing/understand/download-azure-daily-usage).

## Costs and pricing for other services

Microsoft Sentinel integrates with many other Azure services, including Azure Logic Apps, Azure Notebooks, and bring your own machine learning (BYOML) models. Some of these services might have extra charges. Some of Microsoft Sentinel's data connectors and solutions use Azure Functions for data ingestion, which also has a separate associated cost.

Learn about pricing for these services:

- [Automation-Logic Apps pricing](https://azure.microsoft.com/pricing/details/logic-apps/)
- [Notebooks pricing](https://azure.microsoft.com/pricing/details/machine-learning/)
- [BYOML pricing](https://azure.microsoft.com/pricing/details/machine-learning-studio/)
- [Azure Functions pricing](https://azure.microsoft.com/pricing/details/functions/)

Any other services you use might have associated costs.

## Interactive and total data retention costs

After you enable Microsoft Sentinel on a Log Analytics workspace, consider these configuration options:

- Retain all data ingested into the workspace at no charge for the first 90 days. Retention beyond 90 days is charged per the standard [Log Analytics retention prices](https://azure.microsoft.com/pricing/details/monitor/).
- Specify different retention settings for individual data types. Learn about [retention by data type](/en-us/azure/azure-monitor/logs/data-retention-configure#configure-table-level-retention).
- Extend retention of data with total retention so you have access to historical logs. The Microsoft Sentinel data lake is a low-cost retention state for the preservation of data for such things as regulatory compliance. It's charged based on the volume of data stored and scanned. Use **Data management &gt; Tables** to adjust the Analytics and Total retention period and learn more in [What is Microsoft Sentinel data lake?](datalake/sentinel-lake-overview)
- Switch tables that contain secondary security data to **Lake tier**. This enables you to store high-volume, low-value logs at a low price, with querying capabilities built in. Use **Data management &gt; Tables** to switch tables from **Analytics** to **Lake** tier.

## Other CEF ingestion costs

CEF is a supported Syslog events format in Microsoft Sentinel. Use CEF to bring in valuable security information from various sources to your Microsoft Sentinel workspace. CEF logs land in the CommonSecurityLog table in Microsoft Sentinel, which includes all the standard up-to-date CEF fields.

Many devices and data sources support logging fields beyond the standard CEF schema. These extra fields land in the AdditionalExtensions table. These fields could have higher ingestion volumes than the standard CEF fields, because the event content within these fields can be variable.

## Costs that might accrue after resource deletion

Removing Microsoft Sentinel doesn't remove the Log Analytics workspace Microsoft Sentinel was deployed on, or any separate charges that workspace might be incurring.

## Free data sources

The following data sources are free with Microsoft Sentinel:

- Azure Activity Logs
- Microsoft Sentinel Health
- Office 365 Audit Logs, including all SharePoint activity, Exchange admin activity, and Teams
- Security alerts, including alerts from the following sources:
    - Microsoft Defender XDR
    - Microsoft Defender for Cloud
    - Microsoft Defender for Office 365
    - Microsoft Defender for Identity
    - Microsoft Defender for Cloud Apps
    - Microsoft Defender for Endpoint
- Alerts from the following sources:
    - Microsoft Defender for Cloud
    - Microsoft Defender for Cloud Apps

Although alerts are free, the raw logs for some Microsoft Defender XDR, Defender for Endpoint/Identity/Office 365/Cloud Apps, Microsoft Entra ID, and Azure Information Protection (AIP) data types are paid.

The following table lists the data sources in Microsoft Sentinel and Log Analytics that aren't charged. For more information, see [excluded tables](/en-us/azure/azure-monitor/logs/cost-logs#excluded-tables).

| Microsoft Sentinel data connector | Free data type |
| --- | --- |
| **Azure Activity** | AzureActivity |
| **Health monitoring for Microsoft Sentinel**^1^ | SentinelHealth |
| **Microsoft Entra ID Protection** | SecurityAlert (IPC) |
| **Microsoft 365** | OfficeActivity (SharePoint) |
|  | OfficeActivity (Exchange) |
|  | OfficeActivity (Teams) |
| **Microsoft Defender for Cloud** | SecurityAlert (Azure Security Center) |
| **Microsoft Defender for IoT** | SecurityAlert (Azure Security Center for IoT) |
| **Microsoft Defender XDR** | SecurityIncident |
|  | SecurityAlert |
| **Microsoft Defender for Endpoint** | SecurityAlert (MDATP) |
| **Microsoft Defender for Identity** | SecurityAlert (AATP) |
| **Microsoft Defender for Cloud Apps** | SecurityAlert (MCAS) |
| **Microsoft Defender for Office 365 (Preview)** | SecurityAlert (OATP) |

*^1^**For more information, see [Auditing and health monitoring for Microsoft Sentinel](health-audit).*

For data connectors that include both free and paid data types, select which data types you want to enable.

[![Screenshot of the connector page for Defender for Cloud Apps, with the free security alerts selected and paid MCAS Shadow IT Reporting not enabled.](media/billing/data-types.png)](media/billing/data-types.png#lightbox)

Learn more about how to [connect data sources](connect-data-sources), including free and paid data sources.

## Learn more

- [Monitor costs for Microsoft Sentinel](billing-monitor-costs)
- [Reduce costs for Microsoft Sentinel](billing-reduce-costs)
- Learn [how to optimize your cloud investment with Microsoft Cost Management](/en-us/azure/cost-management-billing/costs/cost-mgt-best-practices?WT.mc_id=costmanagementcontent_docsacmhorizontal_-inproduct-learn).
- Learn more about managing costs with [cost analysis](/en-us/azure/cost-management-billing/costs/quick-acm-cost-analysis?WT.mc_id=costmanagementcontent_docsacmhorizontal_-inproduct-learn).
- Learn about how to [prevent unexpected costs](/en-us/azure/cost-management-billing/understand/analyze-unexpected-charges?WT.mc_id=costmanagementcontent_docsacmhorizontal_-inproduct-learn).
- Take the [Cost Management](/en-us/training/paths/control-spending-manage-bills?WT.mc_id=costmanagementcontent_docsacmhorizontal_-inproduct-learn) guided learning course.
- For more tips on reducing Log Analytics data volume, see [Azure Monitor best practices - Cost management](/en-us/azure/azure-monitor/best-practices-cost).