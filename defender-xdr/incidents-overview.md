---
layout: Conceptual
title: Incidents and alerts in the Microsoft Defender portal - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/incidents-overview
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: An introduction to incidents and alerts, and the differences between them, in the Microsoft Defender portal.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
- usx-security
- sentinel-only
ms.custom: admindeeplinkDEFENDER
ms.topic: concept-article
ms.date: 2025-12-22T00:00:00.0000000Z
locale: en-us
document_id: 8717e531-fa99-f7ab-3907-06c528edf3f3
document_version_independent_id: 8717e531-fa99-f7ab-3907-06c528edf3f3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/incidents-overview.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: incidents-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/incidents-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: f84f5d7f-7be0-19ee-38bb-7c1dcc56e758
---

# Incidents and alerts in the Microsoft Defender portal - Microsoft Defender XDR | Microsoft Learn

The Microsoft Defender portal brings together a unified set of security services to reduce your exposure to security threats, improve your organizational security posture, detect security threats, and investigate and respond to breaches. These services collect and produce signals that are displayed in the portal. The two main kinds of signals are:

**Alerts**: Signals that result from various threat detection activities. These signals indicate the occurrence of malicious or suspicious events in your environment.

**Incidents**: Containers that include collections of related alerts and tell the full story of an attack. The alerts in a single incident might come from all Microsoft security and compliance solutions, as well as from vast numbers of external solutions collected through Microsoft Sentinel and Microsoft Defender for Cloud.

Note

Incident cases are in preview and are the recommended experience for managing incidents. The legacy incident experience remains available during this preview. For the recommended experience, see [Manage incident cases in the Microsoft Defender portal](manage-incident-cases).

## Incidents for correlation and investigation

While you can investigate and mitigate the threats that individual alerts bring to your attention, by themselves these threats are isolated occurrences that don't tell you anything about a broader, complex attack story. You could search for, research, investigate, and correlate groups of alerts that belong together in a single attack story, but that will cost you lots of time, effort, and energy.

Instead, the correlation engines and algorithms in the Microsoft Defender portal automatically aggregate and correlate related alerts together to form incidents that represent these larger attack stories. Defender identifies multiple signals as belonging to the same attack story, using AI to continually monitor its telemetry sources and add more evidence to already open incidents. Incidents contain all the alerts deemed to be related to each other and to the overall attack story, and present the story in various forms:

- Timelines of alerts and the raw events on which they're based
- A list of the tactics that were used
- Lists of all the involved and impacted users, devices, and other resources
- A visual representation of how all the players in the story interact
- Logs of automatic investigation and response processes that Defender initiated and completed
- Collections of evidence supporting the attack story: bad actors' user accounts and device information and address, malicious files and processes, relevant threat intelligence, and so on
- A textual summary of the attack story

Incidents also provide you with a framework for managing and documenting your investigations and threat response. For the recommended experience, see [Manage incident cases in the Microsoft Defender portal](manage-incident-cases). For the legacy incident experience, see [Manage incidents in Microsoft Defender](manage-incidents).

## Alert sources and threat detection

Alerts in the Microsoft Defender portal come from many sources. These sources include the many services that are part of Microsoft Defender, as well as other services with varying degrees of integration with the Microsoft Defender portal.

For example, when Microsoft Sentinel is [onboarded](/en-us/azure/sentinel/microsoft-sentinel-onboard) to the Microsoft Defender portal, the correlation engine in the Defender portal has access to all the raw data ingested by Microsoft Sentinel, which you can find in Defender's **Advanced hunting** tables.

- Microsoft Sentinel customers using the Defender portal, or who are using the Azure portal with the [Microsoft Sentinel Defender XDR data connector](/en-us/azure/sentinel/connect-microsoft-365-defender), also benefit from Microsoft Threat Intelligence alerts that highlight activity from nation state actors, such as ransomware campaigns and fraudulent operations. For customers without E5 licenses or Microsoft Sentinel, these alerts are available only in the Microsoft 365 Admin Center (MAC).
- Microsoft Defender XDR itself also creates alerts. Defender XDR's unique correlation capabilities provide another layer of data analysis and threat detection for all the non-Microsoft solutions in your digital estate. These detections produce Defender XDR alerts, in addition to the alerts already provided by Microsoft Sentinel's analytics rules.

Within each of these sources, there are one or more threat detection mechanisms that produce alerts based on the rules defined in each mechanism. For example, Microsoft Sentinel has at least four different engines that produce different types of alerts, each with its own rules.

## Tools and methods for investigation and response

The Microsoft Defender portal includes tools and methods to automate or otherwise assist in the triage, investigation, and resolution of incidents. These tools are presented in the following table:

| Tool/Method | Description |
| --- | --- |
| **[Manage](manage-incident-cases) and [investigate](investigate-incident-cases) incident cases** | Prioritize incident cases according to severity, and then investigate them to understand and respond to the associated threats. For the legacy incident experience, see [Manage incidents](manage-incidents) and [Investigate incidents](investigate-incidents). |
| **[Manage incident case tasks](manage-incident-case-tasks)** | Use tasks in the Microsoft Defender portal to investigate and resolve incident cases collaboratively across your operations teams. Managing incident cases with tasks helps improve efficiency in incident response and ensure accountability for investigation outcomes. For the legacy incident experience, see [Use tasks to handle incident workflow](split-incidents-into-tasks). |
| **[Automatically investigate and resolve alerts](/en-us/defender-xdr/m365d-autoir)** | If enabled to do so, Microsoft Defender can automatically investigate and resolve alerts from Microsoft 365 and Entra ID sources through automation and artificial intelligence. |
| **[Configure automatic attack disruption actions](automatic-attack-disruption)** | Use high-confidence signals collected from Microsoft Defender XDR and Microsoft Sentinel to automatically disrupt active attacks at machine speed, containing the threat and limiting the impact. |
| **[Configure Microsoft Sentinel automation rules](/en-us/azure/sentinel/automate-incident-handling-with-automation-rules)** | Use automation rules to automate triage, assignment, and management of incidents, regardless of their source. Help your team's efficiency even more by configuring your rules to apply tags to incidents based on their content, suppress noisy (false positive) incidents, and close resolved incidents that meet the appropriate criteria, specifying a reason and adding comments. |
| **[Proactively hunt with advanced hunting](advanced-hunting-overview)** | Use Kusto Query Language (KQL) to proactively inspect events in your network by querying the logs collected in the Defender portal. Advanced hunting supports a guided mode for users looking for the convenience of a query builder. |
| **[Harness AI with Microsoft Security Copilot](/en-us/defender-xdr/security-copilot-in-microsoft-365-defender)** | Add AI to support analysts with complex and time-consuming daily workflows. For example, Microsoft Security Copilot can help with end-to-end incident investigation and response by providing clearly described attack stories, step-by-step actionable remediation guidance and incident activity summarized reports, natural language KQL hunting, and expert code analysis—optimizing on SOC efficiency across data from all sources. This capability is in addition to the other AI-based functionality that Microsoft Sentinel brings to the unified platform, in the areas of user and entity behavior analytics, anomaly detection, multi-stage threat detection, and more. |

Tip

**Defender Boxed**, a series of cards showcasing your organization's security successes, improvements, and response actions in the past six months/year, appears for a limited time during January and July of each year. Learn how you can share your [Defender Boxed](incident-queue#defender-boxed) highlights.

## Related items

- [Manage incident cases in the Microsoft Defender portal](manage-incident-cases)
- [Alerts, incidents, and correlation in Microsoft Defender](alerts-incidents-correlation).
- [Manage incidents in Microsoft Defender (legacy)](manage-incidents).