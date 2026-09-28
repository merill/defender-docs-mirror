---
layout: Conceptual
title: Threat detection in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/threat-detection
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
description: Understand how threat detection works in Microsoft Sentinel. Learn about different types of analytics rules and templates, and the generation of alerts and incidents.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: concept-article
ms.custom: devx-track-arm-template
ms.date: 2024-10-16T00:00:00.0000000Z
ms.collection: usx-security
locale: en-us
document_id: b1e5a527-d4ce-7419-1aa8-f8cd82654088
document_version_independent_id: 671a2924-c21d-b7c7-31e0-587ca5aec785
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/threat-detection.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/threat-detection
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/threat-detection.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 87b4a10e-3293-4c49-8a8b-214749f53e08
---

# Threat detection in Microsoft Sentinel | Microsoft Learn

Important

[**Custom detections**](/en-us/defender-xdr/custom-detections-overview?toc=/azure/sentinel/TOC.json&amp;bc=/azure/sentinel/breadcrumb/toc.json) is now the best way to create new rules across Microsoft Sentinel SIEM Microsoft Defender XDR. With custom detections, you can reduce ingestion costs, get unlimited real-time detections, and benefit from seamless integration with Defender XDR data, functions, and remediation actions with automatic entity mapping. For more information, read [this blog](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/custom-detections-are-now-the-unified-experience-for-creating-detections-in-micr/4463875).

After [setting up Microsoft Sentinel to collect data from all over your organization](connect-data-sources), you need to constantly dig through all that data to detect security threats to your environment. To accomplish this task, Microsoft Sentinel provides threat detection rules that run regularly, querying the collected data and analyzing it to discover threats. These rules come in a few different flavors and are collectively known as **analytics rules**.

These rules generate ***alerts*** when they find what they’re looking for. Alerts contain information about the events detected, such as the [entities](entities) (users, devices, addresses, and other items) involved. Alerts are aggregated and correlated into ***incidents***—case files—that you can [assign and investigate](incident-investigation) to learn the full extent of the detected threat and respond accordingly. You can also build predetermined, automated responses into the rules' own configuration.

You can create these rules from scratch, using the [built-in analytics rule wizard](scheduled-rules-overview). However, Microsoft strongly encourages you to make use of the vast array of [**analytics rule templates**](create-analytics-rule-from-template) available to you through the many [solutions for Microsoft Sentinel](sentinel-solutions) provided in the content hub. These templates are pre-built rule prototypes, designed by teams of security experts and analysts based on their knowledge of known threats, common attack vectors, and suspicious activity escalation chains. You activate rules from these templates to automatically search across your environment for any activity that looks suspicious. Many of the templates can be customized to search for specific types of events, or filter them out, according to your needs.

This article helps you understand how Microsoft Sentinel detects threats, and what happens next.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Types of analytics rules

You can view the analytics rules and templates available for you to use on the **Analytics** page of the **Configuration** menu in Microsoft Sentinel. The currently **active rules** are visible in one tab, and **templates** to create new rules in another tab. A third tab displays **Anomalies**, a special rule type described later in this article.

To find more rule templates than are currently displayed, go to the **Content hub** in Microsoft Sentinel to install the related product solutions or standalone content. Analytics rule templates are available with nearly every product solution in the content hub.

The following types of analytics rules and rule templates are available in Microsoft Sentinel:

- Scheduled rules
- Near-real-time (NRT) rules
- Anomaly rules
- Microsoft security rules

Besides the preceding rule types, there are some other specialized template types that can each create one instance of a rule, with limited configuration options:

- Threat intelligence
- Advanced multistage attack detection ("Fusion")
- Machine learning (ML) behavior analytics

### Scheduled rules

By far the most common type of analytics rule, **Scheduled** rules are based on [Kusto queries](/en-us/kusto/query/?toc=/azure/sentinel/TOC.json&amp;bc=/azure/sentinel/breadcrumb/toc.json) that are configured to run at regular intervals and examine raw data from a defined "lookback" period. If the number of results captured by the query passes the threshold configured in the rule, the rule produces an alert.

The queries in [scheduled rule templates](create-analytics-rule-from-template) were written by security and data science experts, either from Microsoft or from the vendor of the solution providing the template. Queries can perform complex statistical operations on their target data, revealing baselines and outliers in groups of events.

The query logic is displayed in the rule configuration. You can use the query logic and the scheduling and lookback settings as defined in the template, or customize them to create new rules. Alternatively, you can create [entirely new rules from scratch](create-analytics-rules).

Learn more about [Scheduled analytics rules in Microsoft Sentinel](scheduled-rules-overview).

### Near-real-time (NRT) rules

NRT rules are a limited subset of scheduled rules. They are designed to run once every minute, in order to supply you with information as up-to-the-minute as possible.

They function mostly like scheduled rules and are configured similarly, with some limitations.

Learn more about [Quick threat detection with near-real-time (NRT) analytics rules in Microsoft Sentinel](near-real-time-rules).

### Anomaly rules

Anomaly rules use machine learning to observe specific types of behaviors over a period of time to determine a baseline. Each rule has its own unique parameters and thresholds, appropriate to the behavior being analyzed. After the observation period is completed, the baseline is set. When the rule observes behaviors that exceed the boundaries set in the baseline, it flags those occurrences as anomalous.

While the configurations of out-of-the-box rules can't be changed or fine-tuned, you can duplicate a rule, and then change and fine-tune the duplicate. In such cases, run the duplicate in **Flighting** mode and the original concurrently in **Production** mode. Then compare results, and switch the duplicate to **Production** if and when its fine-tuning is to your liking.

Anomalies don't necessarily indicate malicious or even suspicious behavior by themselves. Therefore, anomaly rules don't generate their own alerts. Rather, they record the results of their analysis—the detected anomalies—in the *Anomalies* table. You can query this table to provide context that improves your detections, investigations, and threat hunting.

For more information, see [Use customizable anomalies to detect threats in Microsoft Sentinel](soc-ml-anomalies) and [Work with anomaly detection analytics rules in Microsoft Sentinel](work-with-anomaly-rules).

### Microsoft security rules

While scheduled and NRT rules automatically create incidents for the alerts they generate, alerts generated in external services and ingested to Microsoft Sentinel don't create their own incidents. Microsoft security rules automatically create Microsoft Sentinel incidents from the alerts generated in other Microsoft security solutions, in real time. You can use Microsoft security templates to create new rules with similar logic.

Important

Microsoft security rules are **not available** if you have:

- Enabled [**Microsoft Defender XDR incident integration**](microsoft-365-defender-sentinel-integration), or
- Onboarded Microsoft Sentinel to the [**Defender portal**](microsoft-sentinel-defender-portal).

In these scenarios, Microsoft Defender XDR creates the incidents instead.

Any such rules you had defined beforehand are automatically disabled.

For more information about *Microsoft security* incident creation rules, see [Automatically create incidents from Microsoft security alerts](create-incidents-from-alerts).

### Threat intelligence

Take advantage of threat intelligence produced by Microsoft to generate high fidelity alerts and incidents with the **Microsoft Threat Intelligence Analytics** rule. This unique rule isn't customizable, but when enabled, automatically matches Common Event Format (CEF) logs, Syslog data or Windows DNS events with domain, IP and URL threat indicators from Microsoft Threat Intelligence. Certain indicators contain more context information through MDTI (**Microsoft Defender Threat Intelligence**).

For more information on how to enable this rule, see [Use matching analytics to detect threats](use-matching-analytics-to-detect-threats).For more information on MDTI, see [What is Microsoft Defender Threat Intelligence](/en-us/defender-xdr/defender-threat-intelligence).

### Advanced multistage attack detection (Fusion)

Microsoft Sentinel uses the [Fusion correlation engine](fusion), with its scalable machine learning algorithms, to detect advanced multistage attacks by correlating many low-fidelity alerts and events across multiple products into high-fidelity and actionable incidents. The **Advanced multistage attack detection** rule is enabled by default. Because the logic is hidden and therefore not customizable, there can be only one rule with this template.

The Fusion engine can also correlate alerts produced by scheduled analytics rules with alerts from other systems, producing high-fidelity incidents as a result.

Important

The *Advanced multistage attack detection* rule type is **not available** if you have:

- Enabled [**Microsoft Defender XDR incident integration**](microsoft-365-defender-sentinel-integration), or
- Onboarded Microsoft Sentinel to the [**Defender portal**](microsoft-sentinel-defender-portal).

In these scenarios, Microsoft Defender XDR creates the incidents instead.

Also, some of the **Fusion** detection templates are currently in **PREVIEW** (see [Advanced multistage attack detection in Microsoft Sentinel](fusion) to see which ones). See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

### Machine learning (ML) behavior analytics

Take advantage of Microsoft's proprietary machine learning algorithms to generate high fidelity alerts and incidents with the **ML Behavior Analytics** rules. These unique rules (currently in **Preview**) aren't customizable, but when enabled, detect specific anomalous SSH and RDP login behaviors based on IP and geolocation and user history information.

## Access permissions for analytics rules

When you create an analytics rule, an access permissions token is applied to the rule and saved along with it. This token ensures that the rule can access the workspace that contains the data queried by the rule, and that this access is maintained even if the rule's creator loses access to that workspace.

There is one exception to this access, however: when a rule is created to access workspaces in other subscriptions or tenants, such as what happens in the case of an MSSP, Microsoft Sentinel takes extra security measures to prevent unauthorized access to customer data. For these kinds of rules, the credentials of the user that created the rule are applied to the rule instead of an independent access token, so that when the user no longer has access to the other subscription or tenant, the rule stops working.

If you operate Microsoft Sentinel in a cross-subscription or cross-tenant scenario, when one of your analysts or engineers loses access to a particular workspace, any rules created by that user stops working. In this situation, you get a health monitoring message regarding "insufficient access to resource", and the rule is [auto-disabled](troubleshoot-analytics-rules#issue-a-scheduled-rule-failed-to-execute-or-appears-with-auto-disabled-added-to-the-name) after having failed a certain number of times.

## Export rules to an ARM template

You can easily [export your rule to an Azure Resource Manager (ARM) template](import-export-analytics-rules) if you want to manage and deploy your rules as code. You can also import rules from template files in order to view and edit them in the user interface.