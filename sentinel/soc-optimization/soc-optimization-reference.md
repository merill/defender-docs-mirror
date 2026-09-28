---
layout: Conceptual
title: SOC optimization reference | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/soc-optimization/soc-optimization-reference
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
ms.reviewer: yohasson
description: Learn about the Microsoft Sentinel SOC optimization recommendations available to help you optimize your security operations.
ms.author: monaberdugo
author: mberdugo
ms.collection:
- usx-security
ms.topic: reference
ms.date: 2025-05-06T00:00:00.0000000Z
locale: en-us
document_id: 39ba3288-2fe1-0fa1-df7a-6db393f7f00d
document_version_independent_id: de93cae5-1680-6b42-d068-a2dc601bccbe
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/soc-optimization/soc-optimization-reference.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/soc-optimization/soc-optimization-reference
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/soc-optimization/soc-optimization-reference.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: d703e32a-4344-7c72-bda1-a921bf3cc55a
---

# SOC optimization reference | Microsoft Learn

Use SOC optimization recommendations to help you close coverage gaps against specific threats and tighten your ingestion rates against data that doesn't provide security value. SOC optimizations help you optimize your Microsoft Sentinel workspace, without having your SOC teams spend time on manual analysis and research.

Microsoft Sentinel SOC optimizations include the following types of recommendations:

- **Data value recommendations** suggest ways to improve your data use, such as a better data plan for your organization.
- **Coverage based recommendations** suggest adding controls to prevent coverage gaps that can lead to vulnerability to attacks or scenarios that can lead to financial loss. Coverage recommendations include:

    - **Threat-based recommendations**: Recommends adding security controls that help you detect coverage gaps to prevent attacks and vulnerabilities.
    - **AI MITRE ATT&CK tagging recommendations (Preview)**: Uses artificial intelligence to suggest tagging security detections with MITRE ATT&CK tactics and techniques.
    - **Risk-based recommendations (Preview)**: Recommends implementing controls to address coverage gaps linked to use cases that may result in business risks or financial losses, including operational, financial, reputational, compliance, and legal risks.
- **Similar organizations recommendations** suggest ingesting data from the types of sources used by organizations which have similar ingestion trends and industry profiles to yours.

This article provides a detailed reference of the types of SOC optimization recommendations available.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](../overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](../move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Data value optimization recommendations

To optimize your cost/security value ratio, SOC optimization surfaces hardly used data connectors or tables. SOC optimization suggests ways to either reduce the cost of a table or improve its value, depending on your coverage. This type of optimization is also called *data value optimization*.

Data value optimizations only look at billable tables that ingested data in the past 30 days.

The following table lists the available types of data value SOC optimization recommendations:

| Type of observation | Action |
| --- | --- |
| The table wasn't used by analytics rules or detections in the last 30 days but was used by other sources, such as workbooks, log queries, hunting queries. | Turn on analytics rule templates ORMove the table to a [basic logs plan](../billing#data-lake-tier) if the table is eligible. |
| The table wasn’t used at all in the last 30 days. | Turn on analytics rule templates OR Stop data ingestion and remove the table or move the table to long term retention. |
| The table was only used by Azure Monitor. | Turn on any relevant analytics rule templates for tables with security value ORMove to a nonsecurity Log Analytics workspace. |

If a table is chosen for [UEBA](/en-us/azure/sentinel/enable-entity-behavior-analytics) or a [threat intelligence matching analytics rule](/en-us/azure/sentinel/use-matching-analytics-to-detect-threats), SOC optimization doesn't recommend any changes in ingestion.

### Unused columns (Preview)

SOC optimization also surfaces unused columns in your tables. The following table lists the available types of columns available for SOC optimization recommendations:

| Type of observation | Action |
| --- | --- |
| The **ConditionalAccessPolicies** column in the **SignInLogs** table or the **AADNonInteractiveUserSignInLogs** table isn't in use. | Stop data ingestion for the column. |

Important

When making changes to ingestion plans, we recommend always ensuring that the limits of your ingestion plans are clear, and that the affected tables aren't ingested for compliance or other similar reasons.

## Coverage-based optimization recommendations

Coverage-based optimization recommendations help you close coverage gaps against specific threats or to scenarios that can lead to business risks and financial loss.

### Threat-based optimization recommendations

To optimize data value, SOC optimization recommends adding security controls to your environment in the form of extra detections and data sources, using a threat-based approach. This optimization type is also known as *coverage optimization*, and is based on Microsoft's security research.

SOC optimization provides threat-based recommendations by analyzing your ingested logs and enabled analytics rules, then comparing them to the logs and detections needed to address specific types of attacks.

Threat-based optimizations consider both predefined and user-defined detections.

The following table lists the available types of threat-based SOC optimization recommendations:

| Type of observation | Action |
| --- | --- |
| There are data sources, but detections are missing. | Turn on analytics rule templates based on the threat: Create a rule using an analytics rule template, and adjust the name, description, and query logic to suit your environment. For more information, see [Threat detection in Microsoft Sentinel](../threat-detection). |
| Templates are turned on, but data sources are missing. | Connect new data sources. |
| There are no existing detections or data sources. | Connect detections and data sources or install a solution. |

### AI MITRE ATT&CK tagging recommendations (Preview)

The AI MITRE ATT&CK Tagging feature uses artificial intelligence to automatically tag security detections. The AI model runs on the customer's workspace to create tagging recommendations for untagged detections with relevant MITRE ATT&CK tactic and techniques.

Customers can apply these recommendations to ensure their security coverage is thorough and precise. This ensures complete and accurate security coverage, enhancing threat detection and response capabilities.

These are 3 ways to apply the AI MITRE ATT&CK tagging recommendations:

- Apply the recommendation to a specific analytics rule.
- Apply the recommendation to all analytics rules in the workspace.
- Don't apply the recommendation to any analytics rules.

### Risk-based optimization recommendations (Preview)

Risk-based optimizations consider real world security scenarios with a set of business risks associated with it, including Operational, Financial, Reputational, Compliance, and Legal risks. The recommendations are based on the Microsoft Sentinel risk-based approach to security.

To provide risk-based recommendations, SOC optimization looks at your ingested logs and analytics rules, and compares them to the logs and detections that are required to protect, detect, and respond to specific types of attacks that may cause business risks. Risk-based recommendations optimizations consider both predefined and user-defined detections.

The following table lists the available types of risk-based SOC optimization recommendations:

| Type of observation | Action |
| --- | --- |
| There are data sources, but detections are missing. | Turn on analytics rule templates based on the business risks: Create a rule using an analytics rule template, and adjust the name, description, and query logic to suit your environment. |
| Templates are turned on, but data sources are missing. | Connect new data sources. |
| There are no existing detections or data sources. | Connect detections and data sources or install a solution. |

## Similar organizations recommendations

SOC optimization uses advanced machine learning to identify tables that are missing from your workspace, but are used by organizations with similar ingestion trends and industry profiles. It shows how other organizations use these tables and recommends the relevant data sources, along with related rules, to improve your security coverage.

| Type of observation | Action |
| --- | --- |
| Log sources ingested by similar customers are missing | Connect the suggested data sources. This recommendation doesn't include: <br>- Custom connectors<br>- Custom tables<br>- Tables ingested by fewer than 10 workspaces<br>- Tables that contain multiple log sources, like the `Syslog` or `CommonSecurityLog` tables |

### Considerations

- A workspace only receives similar organization recommendations if the machine learning model identifies significant similarities with other organizations and discovers tables that they have but you don't. SOCs in their early or onboarding stages are more likely to receive these recommendations than SOCs with a higher level of maturity. Not all workspaces get similar organizations recommendations.
- The machine learning models never access or analyze the content of customer logs or ingest them at any point. No customer data, content, or personal data (EUII) is exposed to the analysis. Recommendations are based on machine learning models that rely solely on Organizational Identifiable Information (OII) and system metadata.