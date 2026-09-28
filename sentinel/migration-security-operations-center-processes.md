---
layout: Conceptual
title: 'Microsoft Sentinel Migration: Update SOC and Analyst Processes | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/migration-security-operations-center-processes
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
description: Learn how to update your SOC and analyst processes as part of your migration to Microsoft Sentinel.
author: EdB-MSFT
ms.author: edbaynash
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 4cfbfa49-6b39-1a71-82f7-5284b24c0b08
document_version_independent_id: ac7383b9-d873-d4c2-95b8-bb47af5acfd6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/migration-security-operations-center-processes.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/migration-security-operations-center-processes
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/migration-security-operations-center-processes.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 27937398-905f-e85c-1eb3-9cfba8a5e80b
---

# Microsoft Sentinel Migration: Update SOC and Analyst Processes | Microsoft Learn

A security operations center (SOC) is a centralized function within an organization that integrates people, processes, and technology. A SOC implements the organization's overall cybersecurity framework. The SOC collaborates the organizational efforts to monitor, alert, prevent, detect, analyze, and respond to cybersecurity incidents. SOC teams, led by a SOC manager, may include incident responders, SOC analysts at levels 1, 2, and 3, threat hunters, and incident response managers.

SOC teams use telemetry from across the organization's IT infrastructure, including networks, devices, applications, behaviors, appliances, and information stores. The teams then co-relate and analyze the data, to determine how to manage the data and which actions to take.

To successfully migrate to Microsoft Sentinel, you need to update not only the technology that the SOC uses, but also the SOC tasks and processes. This article describes how to update your SOC and analyst processes as part of your migration to Microsoft Sentinel.

## Update analyst workflow

Microsoft Sentinel offers a range of tools that map to a typical analyst workflow, from incident assignment to closure. Analysts can flexibly use some or all of the available tools to triage and investigate incidents. As your organization migrates to Microsoft Sentinel, your analysts need to adapt to these new toolsets, features, and workflows.

### Incidents in Microsoft Sentinel

In Microsoft Sentinel, an incident is a collection of alerts that Microsoft Sentinel determines have sufficient fidelity to trigger the incident. Hence, with Microsoft Sentinel, the analyst triages incidents in the **Incidents** page first, and then proceeds to analyze alerts, if a deeper dive is needed. Compare your security information and event management (SIEM) incident terminology and management areas with Microsoft Sentinel.

### Analyst workflow stages

This table describes the key stages in the analyst workflow, and highlights the specific tools relevant to each activity in the workflow.

| Assign | Triage | Investigate | Respond |
| --- | --- | --- | --- |
| **Assign incidents**:• Manually, in the **Incidents** page • Automatically, using playbooks or automation rules | **Triage incidents** using:• The incident details in the **Incident** page• Entity information in the **Incident page**, under the **Entities** tab• [Microsoft Sentinel notebooks](notebooks) | **Investigate incidents** using:• The investigation graph• Microsoft Sentinel Workbooks• The Log Analytics query window | **Respond to incidents** using:• Playbooks and automation rules• Microsoft Teams War Room |

The following workflow stages map analyst activities and SIEM terminology to specific Microsoft Sentinel features.

#### Assign incident ownership

Use the Microsoft Sentinel **Incidents** page to assign incidents. The **Incidents** page includes an incident preview, and a detailed view for single incidents.

[![Screenshot of Microsoft Sentinel Incidents page.](media/migration-soc-processes/analyst-workflow-incidents.png)](media/migration-soc-processes/analyst-workflow-incidents.png#lightbox)

To assign an incident:

- **Manually**: Set the **Owner** field to the relevant user name.
- **Automatically**: [Use a custom solution based on Microsoft Teams and Logic Apps](https://techcommunity.microsoft.com/t5/microsoft-sentinel-blog/automate-incident-assignment-with-shifts-for-teams/ba-p/2297549), or [create an automation rule](automate-incident-handling-with-automation-rules).

[![Screenshot of assigning an owner in the Incidents page.](media/migration-soc-processes/analyst-workflow-assign-incidents.png)](media/migration-soc-processes/analyst-workflow-assign-incidents.png#lightbox)

#### Triage security incidents

To conduct a triage exercise in Microsoft Sentinel, you can start with various Microsoft Sentinel features, depending on your level of expertise and the nature of the incident under investigation. As a typical starting point, select **View full details** in the **Incident** page. You can now examine the alerts that comprise the incident, review bookmarks, select entities to drill down further into specific entities, or add comments.

[![Screenshot of viewing incident details in the Incidents page.](media/migration-soc-processes/analyst-workflow-incident-details.png)](media/migration-soc-processes/analyst-workflow-incidents.png#lightbox)

Here are suggested actions to continue your incident review:

- Select **Investigation** for a visual representation of the relationships between the incidents and the relevant entities.
- Use a [Microsoft Sentinel notebook](notebooks) to perform an in-depth triage exercise for a particular entity. You can use the **Incident triage** notebook for in-depth triage of the selected entity.

[![Screenshot of Incident triage notebook, including detailed steps in TOC.](media/migration-soc-processes/analyst-workflow-incident-triage-notebook.png)](media/migration-soc-processes/analyst-workflow-incident-triage-notebook.png#lightbox)

##### Expedite triage

Use these features and capabilities to expedite triage:

- For quick filtering, in the **Incidents** page, [search for incidents](investigate-cases#search-for-incidents) associated to a specific entity. Filtering by entity in the **Incidents** page is faster than filtering by the entity column in legacy SIEM incident queues.
- For faster triage, use the **[Alert details](customize-alert-details)** screen to include key incident information in the incident name and description, such as the related user name, IP address, or host. For example, an incident could be dynamically renamed to `Ransomware activity detected in DC01`, where `DC01` is a critical asset, dynamically identified via the customizable alert properties.
- For deeper analysis, in the **Incidents** page, select an incident and select **Events** under **Evidence** to view specific events that triggered the incident. The event data is visible as the output of the query associated with the analytics rule, rather than the raw event. The rule migration engineer can use this output to ensure that the analyst gets the correct data.
- For detailed entity information, in the **Incidents** page, select an incident and select an entity name under **Entities** to view the entity's directory information, timeline, and insights. Learn how to [map entities](map-data-fields-to-entities).
- To link to relevant workbooks, select **Incident preview**. You can customize the workbook to display additional information about the incident, or associated entities and custom fields.

#### Investigate security incidents

Use the investigation graph to deeply investigate incidents. From the **Incidents** page, select an incident and select **Investigate** to view the [investigation graph](investigate-cases#use-the-investigation-graph-to-deep-dive).

[![Screenshot of the investigation graph.](media/migration-soc-processes/analyst-workflow-investigation-graph.png)](media/migration-soc-processes/analyst-workflow-investigation-graph.png#lightbox)

With the investigation graph, you can:

- Understand the scope and identify the root cause of potential security threats by correlating relevant data with any involved entity.
- Dive deeper into entities, and choose between different expansion options.
- Easily see connections across different data sources by viewing relationships extracted automatically from the raw data.
- Expand your investigation scope using built-in exploration queries to surface the full scope of a threat.
- Use predefined exploration options to help you ask the right questions while investigating a threat.

From the investigation graph, you can also open workbooks to further support your investigation efforts. Microsoft Sentinel includes several workbook templates that you can customize to suit your specific use case.

[![Screenshot of a workbook opened from the investigation graph.](media/migration-soc-processes/analyst-workflow-investigation-workbooks.png)](media/migration-soc-processes/analyst-workflow-investigation-workbooks.png#lightbox)

#### Respond to incidents

Use Microsoft Sentinel automated response capabilities to respond to complex threats and reduce alert fatigue. Microsoft Sentinel provides automated response using [Logic Apps playbooks and automation rules](automate-responses-with-playbooks).

[![Screenshot of Playbook templates tab in Automation blade.](media/migration-soc-processes/analyst-workflow-playbooks.png)](media/migration-soc-processes/analyst-workflow-playbooks.png#lightbox)

Use one of the following options to access playbooks:

- The [Automation &gt; Playbook templates tab](use-playbook-templates)
- The Microsoft Sentinel [Content hub](sentinel-solutions-deploy)
- The Microsoft Sentinel [playbooks GitHub repository](https://github.com/Azure/Azure-Sentinel/tree/master/Playbooks)

These sources include a wide range of security-oriented playbooks to cover a substantial portion of use cases of varying complexity. To streamline your work with playbooks, use the templates under **Automation &gt; Playbook templates**. Templates allow you to easily deploy playbooks into the Microsoft Sentinel instance, and then modify the playbooks to suit your organization's needs.

See the [SOC Process Framework](https://github.com/Azure/Azure-Sentinel/wiki/SOC-Process-Framework) to map your SOC process to Microsoft Sentinel capabilities.

## Compare SIEM concepts with Microsoft Sentinel

Use this table to compare the main concepts of your legacy SIEM to Microsoft Sentinel concepts.

| ArcSight | QRadar | Splunk | Microsoft Sentinel |
| --- | --- | --- | --- |
| Event | Event | Event | Event |
| Correlation Event | Correlation Event | Notable Event | Alert |
| Incident | Offense | Notable Event | Incident |
|  | List of offenses | Tags | Incidents page |
| Labels | Custom field in SOAR | Tags | Tags |
|  | Jupyter Notebooks | Jupyter Notebooks | Microsoft Sentinel notebooks |
| Dashboards | Dashboards | Dashboards | Workbooks |
| Correlation rules | Building blocks | Correlation rules | Analytics rules |
| Incident queue | Offenses tab | Incident review | **Incident** page |

## After migration

After migration, explore Microsoft's Microsoft Sentinel resources to expand your skills and get the most out of Microsoft Sentinel.

Also consider increasing your threat protection by using Microsoft Sentinel alongside [Microsoft Defender XDR](microsoft-365-defender-sentinel-integration) and [Microsoft Defender for Cloud](/en-us/azure/security-center/azure-defender) for [integrated threat protection](https://www.microsoft.com/security/business/threat-protection). Benefit from the breadth of visibility that Microsoft Sentinel delivers, while diving deeper into detailed threat analysis.