---
layout: Conceptual
title: What is Microsoft Sentinel SIEM? | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/overview
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
description: Learn about Microsoft Sentinel, a scalable, cloud-native SIEM and SOAR that uses AI, analytics, and automation for threat detection, investigation, and response.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: overview
ms.date: 2026-01-28T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 97d99c58-f56b-e951-06d6-e6d358d89bc9
document_version_independent_id: 1a65d02b-b41f-34a0-8808-89fd9b9b8bd6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/overview.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 55389f42-3117-4ffc-0143-0934da118cf7
---

# What is Microsoft Sentinel SIEM? | Microsoft Learn

Microsoft Sentinel is a cloud-native SIEM solution that delivers scalable, cost-efficient security across multicloud and multiplatform environments. It combines AI, automation, and threat intelligence to support threat detection, investigation, response, and proactive hunting.

Microsoft Sentinel SIEM empowers analysts to anticipate and stop attacks across clouds and platforms, faster and with greater precision.

This article highlights the key capabilities in Microsoft Sentinel.

Microsoft Sentinel inherits the Azure Monitor [tamper-proofing and immutability](/en-us/azure/azure-monitor/logs/data-security#tamper-proofing-and-immutability) practices. While Azure Monitor is an append-only data platform, it includes provisions to delete data for compliance purposes.

This service supports [Azure Lighthouse](/en-us/azure/lighthouse/overview), which lets service providers sign in to their own tenant to manage subscriptions and resource groups that customers have delegated.

## Enable out of the box security content

Microsoft Sentinel provides security content packaged in SIEM solutions that enable you to ingest data, monitor, alert, hunt, investigate, respond, and connect with different products, platforms, and services.

# [Defender portal](#tab/defender-portal)
[![Screenshot of the Microsoft Sentinel content hub in the Defender portal that shows the security content available with a solution.](media/overview/content-hub-defender-portal.png)](media/overview/content-hub-defender-portal.png#lightbox)

# [Azure portal](#tab/azure-portal)
[![Screenshot of the Microsoft Sentinel content hub in the Azure portal that shows the security content available with a solution.](media/overview/content-hub-azure-portal.png)](media/overview/content-hub-azure-portal.png#lightbox)

---

For more information, see [About Microsoft Sentinel content and solutions](sentinel-solutions).

## Collect data at scale

Collect data across all users, devices, applications, and infrastructure, both on-premises and in multiple clouds.

# [Defender portal](#tab/defender-portal)
[![Screenshot of the Microsoft Sentinel data connectors page in the Defender portal that shows a list of available connectors.](media/overview/data-connector-list-defender.png)](media/overview/data-connector-list-defender.png#lightbox)

# [Azure portal](#tab/azure-portal)
[![Screenshot of the data connectors page in Microsoft Sentinel that shows a list of available connectors.](media/overview/data-connectors.png)](media/overview/data-connectors.png#lightbox)

---

This table highlights the key capabilities in Microsoft Sentinel for data collection.

| Capability | Description | Get started |
| --- | --- | --- |
| Out of the box data connectors | Many connectors are packaged with SIEM solutions for Microsoft Sentinel and provide real-time integration. These connectors include Microsoft sources and Azure sources like Microsoft Entra ID, Azure Activity, Azure Storage, and more. Out of the box connectors are also available for the broader security and applications ecosystems for non-Microsoft solutions. You can also use common event format, Syslog, or REST-API to connect your data sources with Microsoft Sentinel. | [Microsoft Sentinel data connectors](connect-data-sources) |
| Custom connectors | Microsoft Sentinel supports ingesting data from some sources without a dedicated connector. If you're unable to connect your data source to Microsoft Sentinel using an existing solution, create your own data source connector. | [Resources for creating Microsoft Sentinel custom connectors](create-custom-connector). |
| Data normalization | Microsoft Sentinel uses both query time and ingestion time normalization to translate various sources into a uniform, normalized view. | [Normalization and the Advanced Security Information Model (ASIM)](normalization) |

## Detect threats

Detect previously undetected threats and minimize false positives using Microsoft's analytics and unparalleled threat intelligence.

# [Defender portal](#tab/defender-portal)
[![Screenshot of the MITRE coverage page with both active and simulated indicators selected in Microsoft Defender.](media/overview/mitre-coverage-defender.png)](media/overview/mitre-coverage-defender.png#lightbox)

# [Azure portal](#tab/azure-portal)
[![Screenshot of the MITRE coverage page with both active and simulated indicators selected.](media/overview/mitre-coverage.png)](media/overview/mitre-coverage.png#lightbox)

---

This table highlights the key capabilities in Microsoft Sentinel for threat detection.

| Capacity | Description | Get started |
| --- | --- | --- |
| Analytics | Helps you reduce noise and minimize the number of alerts you have to review and investigate. Microsoft Sentinel uses analytics to group alerts into incidents. Use the out of the box analytic rules as-is, or as a starting point to build your own rules. Microsoft Sentinel also provides rules to map your network behavior and then look for anomalies across your resources. These analytics connect the dots, by combining low fidelity alerts about different entities into potential high-fidelity security incidents. | [Detect threats out-of-the-box](detect-threats-built-in) |
| MITRE ATT&CK coverage | Microsoft Sentinel analyzes ingested data, not only to detect threats and help you investigate, but also to visualize the nature and coverage of your organization's security status based on the tactics and techniques from the MITRE ATT&CK® framework. | [Understand security coverage by the MITRE ATT&CK® framework](mitre-coverage) |
| Threat intelligence | Integrate numerous sources of threat intelligence into Microsoft Sentinel to detect malicious activity in your environment and provide context to security investigators for informed response decisions. | [Threat intelligence in Microsoft Sentinel](understand-threat-intelligence) |
| Watchlists | Correlate data from a data source you provide, a watchlist, with the events in your Microsoft Sentinel environment. For example, you might create a watchlist with a list of high-value assets, terminated employees, or service accounts in your environment. Use watchlists in your search, detection rules, threat hunting, and response playbooks. | [Watchlists in Microsoft Sentinel](watchlists) |
| Workbooks | Create interactive visual reports by using workbooks. Microsoft Sentinel comes with built-in workbook templates that allow you to quickly gain insights across your data as soon as you connect a data source. Or, create your own custom workbooks. | [Visualize collected data](get-visibility). |

## Investigate threats

Investigate threats with artificial intelligence, and hunt for suspicious activities at scale, tapping into years of cyber security work at Microsoft.

[![Screenshot of an incident investigation that shows an entity and connected entities in an interactive graph.](media/overview/map-timeline.png)](media/overview/map-timeline.png#lightbox)

This table highlights the key capabilities in Microsoft Sentinel for threat investigation.

| Feature | Description | Get started |
| --- | --- | --- |
| Incidents | Microsoft Sentinel deep investigation tools help you to understand the scope and find the root cause of a potential security threat. You can choose an entity on the interactive graph to ask interesting questions for a specific entity, and drill down into that entity and its connections to get to the root cause of the threat. | [Navigate and investigate incidents in Microsoft Sentinel](investigate-incidents) |
| Hunts | Microsoft Sentinel's powerful hunting search-and-query tools, based on the MITRE framework, enable you to proactively hunt for security threats across your organization’s data sources, before an alert is triggered. Create custom detection rules based on your hunting query. Then, surface those insights as alerts to your security incident responders. | [Threat hunting in Microsoft Sentinel](hunting) |
| Notebooks | Microsoft Sentinel supports Jupyter notebooks in Azure Machine Learning workspaces, including full libraries for machine learning, visualization, and data analysis.Use notebooks in Microsoft Sentinel to extend the scope of what you can do with Microsoft Sentinel data. For example:- Perform analytics that aren't built in to Microsoft Sentinel, such as some Python machine learning features.- Create data visualizations that aren't built in to Microsoft Sentinel, such as custom timelines and process trees.- Integrate data sources outside of Microsoft Sentinel, such as an on-premises data set. | [Jupyter notebooks with Microsoft Sentinel hunting capabilities](notebooks) |

## Respond to incidents rapidly

Automate your common tasks and simplify security orchestration with playbooks that integrate with Azure services and your existing tools. Microsoft Sentinel's automation and orchestration provides a highly extensible architecture that enables scalable automation as new technologies and threats emerge.

Playbooks in Microsoft Sentinel are based on workflows built in Azure Logic Apps. For example, if you use the ServiceNow ticketing system, use Azure Logic Apps to automate your workflows and open a ticket in ServiceNow each time a particular alert or incident is generated.

[![Screenshot of example automated workflow in Azure Logic Apps where an incident can trigger different actions.](media/overview/logic-app.png)](media/overview/logic-app.png#lightbox)

This table highlights the key capabilities in Microsoft Sentinel for threat response.

| Feature | Description | Get started |
| --- | --- | --- |
| Automation rules | Centrally manage the automation of incident handling in Microsoft Sentinel by defining and coordinating a small set of rules that cover different scenarios. | [Automate threat response in Microsoft Sentinel with automation rules](automate-incident-handling-with-automation-rules) |
| Playbooks | Automate and orchestrate your threat response by using playbooks, which are a collection of remediation actions. Run a playbook on-demand or automatically in response to specific alerts or incidents, when triggered by an automation rule.  To build playbooks with Azure Logic Apps, choose from a constantly expanding gallery of connectors for various services and systems like ServiceNow, Jira, and more. These connectors allow you to apply any custom logic in your workflow. | [Automate threat response with playbooks in Microsoft Sentinel](automate-responses-with-playbooks)[List of all Logic App connectors](/en-us/connectors/connector-reference/connector-reference-logicapps-connectors) |

## Microsoft Sentinel in the Azure portal retirement timeline

Microsoft Sentinel is [generally available in the Microsoft Defender portal](microsoft-sentinel-defender-portal), including for customers without Microsoft Defender XDR or an E5 license. This means that you can use Microsoft Sentinel in the Defender portal even if you aren't using other Microsoft Defender services.

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal.

If you're currently using Microsoft Sentinel in the Azure portal, we recommend that you start planning your transition to the Defender portal now to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

For more information, see:

- [Microsoft Sentinel in the Microsoft Defender portal](microsoft-sentinel-defender-portal)
- [Transition your Microsoft Sentinel environment to the Defender portal](move-to-defender)
- [Planning your move to Microsoft Defender portal for all Microsoft Sentinel customers](https://techcommunity.microsoft.com/blog/microsoft-security-blog/planning-your-move-to-microsoft-defender-portal-for-all-microsoft-sentinel-custo/4428613) (blog)

### Changes for new customers starting July 2025

For the sake of the changes described in this section, new Microsoft Sentinel customers are customers who are [onboarding the first workspace in their tenant to Microsoft Sentinel](quickstart-onboard).

Starting **July 2025**, such new customers who also have the permissions of a subscription [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) or a [User access administrator](/en-us/azure/role-based-access-control/built-in-roles#user-access-administrator), and are not Azure Lighthouse-delegated users, have their workspaces automatically onboarded to the Defender portal together with onboarding to Microsoft Sentinel.

Users of such workspaces, who also aren't Azure Lighthouse-delegated users, see links in Microsoft Sentinel in the Azure portal that redirect them to the Defender portal.

For example:

![Screenshot of a redirect link from the Azure portal to the Defender portal.](media/overview/redirect-no-defender.png)

Such users use Microsoft Sentinel in the Defender portal only.

New customers who don't have relevant permissions aren't automatically onboarded to the Defender portal, but they do still see redirection links in the Azure portal, together with prompts to have a user with relevant permissions manually onboard the workspace to the Defender portal.

This table summarizes these experiences:

| Customer type | Experience |
| --- | --- |
| **Existing customers** creating new workspaces in a tenant where there is already a workspace enabled for Microsoft Sentinel | Workspaces are not automatically onboarded, and users don't see redirection links |
| **Azure Lighthouse-delegated users** creating new workspaces in any tenant | Workspaces are not automatically onboarded, and users don't see redirection links |
| **New customers** onboarding the first workspace in their tenant to Microsoft Sentinel | - **Users who have the required permissions** have their workspace automatically onboarded. Other users of such workspaces see redirection links in the Azure portal. - **Users who don't have the required permissions** don't have their workspace automatically onboarded. All users of such workspaces see redirection links in the Azure portal, and a user with the required permissions must onboard the workspace to the Defender portal. |