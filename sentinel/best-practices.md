---
layout: Conceptual
title: Best practices for Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/best-practices
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
description: Learn about best practices to employ when managing your Log Analytics workspace for Microsoft Sentinel.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: abhiag
ms.topic: best-practice
ms.date: 2025-07-16T00:00:00.0000000Z
locale: en-us
document_id: e4c560cc-6996-366b-3dc3-3a5e860fe821
document_version_independent_id: 8004ed5f-86cc-50fc-58c0-cc44562cfcb0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/best-practices.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/best-practices
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/best-practices.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 46b5e0af-571c-4c8c-4918-89633387bb4d
---

# Best practices for Microsoft Sentinel | Microsoft Learn

Best practice guidance is provided throughout the technical documentation for Microsoft Sentinel. This article highlights some key guidance to use when deploying, managing, and using Microsoft Sentinel.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

To get started with Microsoft Sentinel, see the [deployment guide](deploy-overview), which covers the high level steps to plan, deploy, and fine-tune your Microsoft Sentinel deployment. From that guide, select the provided links to find detailed guidance for each stage in your deployment.

## Adopt a single-platform architecture

Microsoft Sentinel is integrated with a modern data lake that offers affordable, long-term storage enabling teams to simplify data management, optimize costs, and accelerate the adoption of AI. The Microsoft Sentinel data lake enables a single-platform architecture for security data and empowers analysts with a unified query experience while leveraging Microsoft Sentinel’s rich connector ecosystem. For more information, see [Microsoft Sentinel data lake](datalake/sentinel-lake-overview).

## Onboard Microsoft Sentinel to the Microsoft Defender portal and integrate with Microsoft Defender XDR

Consider onboarding Microsoft Sentinel to the Microsoft Defender portal to unify capabilities with Microsoft Defender XDR like incident management and advanced hunting.

If you don't onboard Microsoft Sentinel to the Microsoft Defender portal, note that:

- By July 2026, all Microsoft Sentinel customers using the Azure portal will be redirected to the Defender portal.
- Until then, you can use the [Defender XDR data connector](connect-microsoft-365-defender) to integrate Microsoft Defender service data with Microsoft Sentinel in the Azure portal.

The following illustration shows how Microsoft's XDR solution seamlessly integrates with Microsoft Sentinel.

[![Diagram of a Microsoft Sentinel and Microsoft Defender XDR architecture in the Microsoft Defender portal.](media/microsoft-365-defender-sentinel-integration/sentinel-xdr-usx.svg)](media/microsoft-365-defender-sentinel-integration/sentinel-xdr-usx.svg#lightbox)

For more information, see the following articles:

- [Microsoft Defender XDR integration with Microsoft Sentinel](microsoft-365-defender-sentinel-integration)
- [Connect Microsoft Sentinel to Microsoft Defender XDR](/en-us/azure/sentinel/microsoft-sentinel-onboard)
- [Microsoft Sentinel in the Microsoft Defender portal](microsoft-sentinel-defender-portal)

## Integrate Microsoft security services

Microsoft Sentinel is empowered by the components that send data to your workspace, and is made stronger through integrations with other Microsoft services. Any logs ingested into products, such as Microsoft Defender for Cloud Apps, Microsoft Defender for Endpoint, and Microsoft Defender for Identity, allow these services to create detections, and in turn provide those detections to Microsoft Sentinel. Logs can also be ingested directly into Microsoft Sentinel to provide a fuller picture for events and incidents.

More than ingesting alerts and logs from other sources, Microsoft Sentinel also provides:

| Capability | Description |
| --- | --- |
| **Threat detection** | [Threat detection capabilities](overview#detect-threats) with artificial intelligence, allowing you to build and present interactive visuals via workbooks, run playbooks to automatically act on alerts, integrate [machine learning models](bring-your-own-ml) to enhance your security operations, and ingest and fetch enrichment feeds from threat intelligence platforms. |
| **Threat investigation** | [Threat investigation capabilities](overview#respond-to-incidents-rapidly) allowing you to visualize and explore alerts and entities, detect anomalies in user and entity behavior, and monitor real-time events during an investigation. |
| **Data collection** | [Collect data](overview#collect-data-at-scale) across all users, devices, applications, and infrastructure, both on-premises and in multiple clouds. |
| **Threat response** | [Threat response capabilities](overview#respond-to-incidents-rapidly), such as playbooks that integrate with Azure services and your existing tools. |
| **Partner integrations** | Integrates with partner platforms using [Microsoft Sentinel data connectors](connect-data-sources), providing essential services for SOC teams. |

## Create custom integration solutions (partners)

For partners who want to create custom solutions that integrate with Microsoft Sentinel, see [Build and publish Microsoft Sentinel SIEM solutions](isv/sentinel-integration-guide).

## Plan incident management and response process

The following image shows recommended steps in an incident management and response process.

![Diagram showing incident management process: Triage. Preparation. Remediation. Eradication. Post incident activities.](media/best-practices/incident-handling.png)

The following table provides high-level incident management and response tasks and related best practices. For more information, see [Microsoft Sentinel incident investigation in the Azure portal](investigate-incidents) or [Incidents and alerts in the Microsoft Defender portal](/en-us/defender-xdr/incidents-overview).

| Task | Best practice |
| --- | --- |
| **Review Incidents page** | Review an incident on the **Incidents** page, which lists the title, severity, and related alerts, logs, and any entities of interest. You can also jump from incidents into collected logs and any tools related to the incident. |
| **Use Incident graph** | Review the **Incident graph** for an incident to see the full scope of an attack. You can then construct a timeline of events and discover the extent of a threat chain. |
| **Review incidents for false positives** | Use data about key entities, such as accounts, URLs, IP address, host names, activities, timeline to understand whether you have a [false positive](false-positives) on hand, in which case you can close the incident directly.If you discover that the incident is a true positive, take action directly from the **Incidents** page to investigate logs, entities, and explore the threat chain. After you identified the threat and created a plan of action, use other tools in Microsoft Sentinel and other Microsoft security services to continue investigating. |
| **Visualize information** | Take a look at the Microsoft Sentinel overview dashboard to get an idea of the security posture of your organization. For more information, see [Visualize collected data](get-visibility). In addition to information and trends on the Microsoft Sentinel overview page, workbooks are valuable investigative tools. For example, use the [Investigation Insights](top-workbooks#investigation-insights) workbook to investigate specific incidents together with any associated entities and alerts. This workbook enables you to dive deeper into entities by showing related logs, actions, and alerts. |
| **Hunt for threats** | While investigating and searching for root causes, run built-in threat hunting queries and check results for any indicators of compromise. For more information, see [Threat hunting in Microsoft Sentinel](hunting). |
| **Entity behavior** | Entity behavior in Microsoft Sentinel allows users to review and investigate actions and alerts for specific entities, such as investigating accounts and host names. For more information, see:- [Enable User and Entity Behavior Analytics (UEBA) in Microsoft Sentinel](enable-entity-behavior-analytics)- [Investigate incidents with UEBA data](investigate-with-ueba)- [Microsoft Sentinel UEBA enrichments reference](ueba-reference) |
| **Watchlists** | Use a watchlist that combines data from ingested data and external sources, such as enrichment data. For example, create lists of IP address ranges used by your organization or recently terminated employees. Use watchlists with playbooks to gather enrichment data, such as adding malicious IP addresses to watchlists to use during detection, threat hunting, and investigations. During an incident, use watchlists to contain investigation data, and then delete them when your investigation is done to ensure that sensitive data doesn't remain in view.  For more information, see [Watchlists in Microsoft Sentinel](watchlists). |

## Optimize data collection and ingestion

Review the Microsoft Sentinel [data collection best practices](best-practices-data), which include prioritizing data connectors, filtering logs, and optimizing data ingestion.

## Make your Kusto Query Language queries faster

Review the [Kusto Query Language best practices](/en-us/kusto/query/best-practices) to make queries faster.