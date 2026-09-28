---
layout: Conceptual
title: ASIM-based domain solutions - Essentials for Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/domain-based-essential-solutions
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
description: Learn about the Microsoft essential solutions for Microsoft Sentinel that span across different ASIM schemas like networks, DNS, and web sessions.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: krishsa
ms.topic: concept-article
ms.date: 2026-08-07T00:00:00.0000000Z
ms.collection: usx-security
locale: en-us
document_id: 4a0bfa27-6b69-b8da-8f34-21c6f5c1fecf
document_version_independent_id: 49556174-00e2-41a8-b149-b1266e4e51bb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/domain-based-essential-solutions.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/domain-based-essential-solutions
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/domain-based-essential-solutions.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: ec1a820a-8399-eb2a-d3e9-0368ec82b5e1
---

# ASIM-based domain solutions - Essentials for Microsoft Sentinel | Microsoft Learn

Microsoft essential solutions are domain solutions published by Microsoft for Microsoft Sentinel. These solutions have out-of-the-box content that can operate across multiple products for specific categories like networking. Some of these essential solutions use the normalization technique Advanced Security Information Model (ASIM) to normalize the data at query time or ingestion time.

Important

Microsoft essential solutions and the Network Session Essentials solution are currently in PREVIEW. The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

## Why use ASIM-based Microsoft essential solutions?

When multiple solutions in a domain category share similar detection patterns, it makes sense to have the data captured under a normalized schema like ASIM. Essential solutions make use of this ASIM schema to detect threats at scale.

In the content hub, there are multiple product solutions for different domain categories like "Security - Network". For example, Azure Firewall, Palo Alto Firewall, and Corelight have product solutions for the "Security - Network" domain category.

- These solutions have differing data ingest components by design. But there’s a certain pattern to the analytics, hunting, workbooks, and other content within the same domain category.
- Most of the major network products have a common basic set of firewall alerts that includes malicious threats coming from unusual IP addresses. The analytic rule template is, in general, duplicated for each of the "Security - Network" category of product solutions. If you're running multiple network products, you need to check and configure multiple analytic rules individually, which is inefficient. You'd also get alerts for each rule configured and might end up with alert fatigue.
- If you have duplicative hunting queries, you might have less performant hunting experiences with the run-all mode of hunting. These duplicative hunting queries also introduce inefficiencies for threat hunters to select and run similar queries.

You might consider Microsoft essential solutions for the following reasons:

- A normalized schema makes it easier for you to query incident details. You don't have to remember different vendor syntax for similar log attributes.
- If you don't have to manage content for multiple solutions, use case deployment and incident handling is easier.
- A consolidated workbook view gives you better environment visibility and possible query time parsing with high performing ASIM parsers.

## ASIM schemas supported

The essential solutions currently use the following ASIM schemas:

- Audit event
- Authentication event
- DNS activity
- File activity
- Network session
- Process event
- Web session

For more information, see [Advanced Security Information Model (ASIM) schemas](/en-us/azure/sentinel/normalization-about-schemas).

## Ingestion time normalization

The ingestion time normalization results can be ingested into following normalized table:

- [ASimDnsActivityLogs](/en-us/azure/azure-monitor/reference/tables/asimdnsactivitylogs) for the DNS schema.
- [ASimNetworkSessionLogs](/en-us/azure/azure-monitor/reference/tables/asimnetworksessionlogs) for the Network Session schema

For more information, see [Ingest time normalization](/en-us/azure/sentinel/normalization-ingest-time).

## Content available with ASIM-based domain essential solutions

The following table describes the type of content available with each essential solution. For some specific use cases, you might want to also use the content available with the Microsoft Sentinel product solution.

| Content type | description |
| --- | --- |
| Analytical Rule | The analytical rules available in the ASIM-based essential solutions are generic and a good fit for any of the dependent Microsoft Sentinel product solutions for that domain. The Microsoft Sentinel product solution might have a source specific use case covered as part of the analytical rule. Enable Microsoft Sentinel product solution rules as needed for your environment. |
| Hunting query | The hunting queries available in the ASIM-based essential solutions are generic and a good fit to hunt for threats from any of the dependent Microsoft Sentinel product solutions for that domain. The Microsoft Sentinel product solution might have a source specific hunting query available out-of-the-box. Use the hunting queries from the Microsoft Sentinel product solution as needed for your environment. |
| Playbook | The ASIM-based essential solutions are expected to handle data with high events per seconds. When you have content that's using that volume of data, you might experience some performance impact that can cause slow loading of workbooks or query results. To solve this problem, the summarization playbook summarizes the source logs and stores the information into a predefined table. Enable the summarization playbook to allow the essential solutions to query this table. Because playbooks in Microsoft Sentinel are based on workflows built in Azure Logic Apps that create separate resources, other charges might apply. For more information, see the [Azure Logic Apps pricing page](https://azure.microsoft.com/pricing/details/logic-apps/). Other charges might also apply for storage of the summarized data. |
| Watchlist | The ASIM-based essential solutions use a watchlist that includes multiple sets of conditions for analytic rule detection and hunting queries. The watchlist allows you to do the following tasks:- Do focused monitoring with data filtration. - Switch between hunting and detection for each list item. - Keep **Threshold type** set to **Static** to leverage threshold-based alerting while anomaly-based alerts would learn from the last few days of data (maximum 14 days). - Modify **Alert Name**, **Description**, **Tactic**, and **Severity** by using this watchlist for individual list items.- Disable detection by setting **Severity** as **Disabled**. |
| Workbook | The workbook available with the ASIM-based essential solutions gives a consolidated view of different events and activity happening in the dependent domain. Because this workbook fetches results from a very high volume of data, there might be some performance lag. If you experience performance issues, use the summarization playbook. |

These essential solutions like other Microsoft Sentinel domain solutions don't have a connector of their own. They depend on the source specific connectors in Microsoft Sentinel product solutions to pull in the logs. To understand the products the domain solution supports, refer to the prerequisite list of product solutions each of the ASIM domain essentials solutions lists. Install one or more of the product solutions. Configure the data connectors to meet the underlying product dependency needs and to enable better usage of this domain solution content.