---
layout: Conceptual
title: Migrate ArcSight SOAR Automation to Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/migration-arcsight-automation
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
description: Learn how to identify SOAR use cases, and how to migrate your ArcSight SOAR automation to Microsoft Sentinel.
author: EdB-MSFT
ms.author: edbaynash
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: a9a10aa5-239f-99c2-52bf-eebb71dcdf77
document_version_independent_id: 3566f2ef-58a1-daf4-6a45-2dbea2cae408
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/migration-arcsight-automation.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/migration-arcsight-automation
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/migration-arcsight-automation.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 74f7d340-570b-c8f9-866c-a9ab34405ca4
---

# Migrate ArcSight SOAR Automation to Microsoft Sentinel | Microsoft Learn

Microsoft Sentinel provides Security Orchestration, Automation, and Response (SOAR) capabilities with [automation rules](automate-incident-handling-with-automation-rules) and [playbooks](tutorial-respond-threats-playbook). Automation rules automate incident handling and response, and playbooks run predetermined sequences of actions to response and remediate threats. This article discusses how to identify SOAR use cases, and how to migrate your ArcSight SOAR automation to Microsoft Sentinel.

Automation rules simplify complex workflows for your incident orchestration processes, and allow you to centrally manage your incident handling automation.

With automation rules, you can:

- Perform simple automation tasks without necessarily using playbooks. For example, you can assign, tag incidents, change status, and close incidents.
- Automate responses for multiple analytics rules at once.
- Control the order of actions that are executed.
- Run playbooks for those cases where more complex automation tasks are necessary.

## Identify SOAR use cases

Here’s what you need to think about when migrating SOAR use cases from ArcSight:

- **Use case quality**: Choose good use cases for automation. Use cases should be based on procedures that are clearly defined, with minimal variation and a low false-positive rate. Automation should work with efficient use cases.
- **Manual intervention**: Automated response can have wide ranging effects and high impact automations should have human input to confirm high impact actions before they’re taken.
- **Binary criteria**: To increase response success, decision points within an automated workflow should be as limited as possible, with binary criteria. Binary criteria reduces the need for human intervention and enhances outcome predictability.
- **Accurate alerts or data**: Response actions are dependent on the accuracy of signals such as alerts. Alerts and enrichment sources should be reliable. Microsoft Sentinel resources such as watchlists and reliable threat intelligence can enhance reliability.
- **Analyst role**: While automation where possible is great, reserve more complex tasks for analysts and provide them with the opportunity for input into workflows that require validation. In short, response automation should augment and extend analyst capabilities.

## Migrate SOAR workflows to Microsoft Sentinel playbooks

The following mapping shows how key SOAR concepts in ArcSight translate to Microsoft Sentinel components, and provides general guidelines for how to migrate each step or component in the SOAR workflow.

![Diagram displaying the ArcSight and Microsoft Sentinel SOAR workflows.](media/migration-arcsight-automation/arcsight-sentinel-soar-workflow.png)

| Step (in diagram) | ArcSight | Microsoft Sentinel |
| --- | --- | --- |
| 1 | Ingest events into Enterprise Security Manager (ESM) and trigger correlation events. | Ingest events into the Log Analytics workspace. |
| 2 | Automatically filter alerts for case creation. | Use [analytics rules](detect-threats-built-in) to trigger alerts. Enrich alerts using the [custom details feature](surface-custom-details-in-alerts) to create dynamic incident names. |
| 3 | Classify cases. | Use [automation rules](automate-incident-handling-with-automation-rules). With automation rules, Microsoft Sentinel treats incidents according to the analytics rule that triggered the incident, and the incident properties that match defined criteria. |
| 4 | Consolidate cases. | You can consolidate several alerts to a single incident according to properties such as matching entities, alert details, or creation timeframe by using the alert grouping feature. |
| 5 | Dispatch cases. | Assign incidents to specific analysts using [automated incident assignment with Shifts for Teams](https://techcommunity.microsoft.com/t5/microsoft-sentinel-blog/automate-incident-assignment-with-shifts-for-teams/ba-p/2297549) between Microsoft Teams, Azure Logic Apps, and Microsoft Sentinel automation rules. |

## Map ArcSight SOAR components to Microsoft Sentinel capabilities

Review which Microsoft Sentinel or Azure Logic Apps features map to the main ArcSight SOAR components. In ArcSight, a *trigger* initiates a workflow based on an event or condition, an *action* performs a specific task in response, and *playbooks* define the orchestrated sequence of actions. The following table maps these components to their Microsoft Sentinel equivalents.

| ArcSight | Microsoft Sentinel/Azure Logic Apps |
| --- | --- |
| Trigger | [Logic Apps triggers overview](/en-us/azure/logic-apps/logic-apps-overview) |
| Automation bit | [Azure Function connector](/en-us/azure/logic-apps/logic-apps-azure-functions) |
| Action | [Logic Apps actions overview](/en-us/azure/logic-apps/logic-apps-overview) |
| Scheduled playbooks | Playbooks initiated by the [recurrence trigger](/en-us/azure/connectors/connectors-native-recurrence) |
| Workflow playbooks | Playbooks automatically initiated by Microsoft Sentinel [alert or incident triggers](playbook-triggers-actions) |
| Marketplace | • [Automation &gt; Templates tab](use-playbook-templates)• [Content hub catalog](sentinel-solutions-catalog)• [Microsoft Sentinel playbooks on GitHub](https://github.com/Azure/Azure-Sentinel/tree/master/Playbooks/Block-OnPremADUser) |

## Operationalize playbooks and automation rules in Microsoft Sentinel

Most of the playbooks that you use with Microsoft Sentinel are available in either the [Automation &gt; Templates tab](use-playbook-templates), the [Content hub catalog](sentinel-solutions-catalog), or [Microsoft Sentinel playbooks on GitHub](https://github.com/Azure/Azure-Sentinel/tree/master/Playbooks/Block-OnPremADUser). In some cases, however, you might need to create playbooks from scratch or from existing templates.

You typically build your custom logic app using the Azure Logic App Designer feature. The logic apps code is based on [Azure Resource Manager (ARM) templates](/en-us/azure/azure-resource-manager/templates/overview), which facilitate development, deployment and portability of Azure Logic Apps across multiple environments. To convert your custom playbook into a portable ARM template, you can use the [ARM template generator](https://techcommunity.microsoft.com/t5/microsoft-sentinel-blog/export-microsoft-sentinel-playbooks-or-azure-logic-apps-with/ba-p/3275898).

Use the following Microsoft Sentinel automation and playbook resources for cases where you need to build your own playbooks either from scratch or from existing templates.

- [Automate incident handling in Microsoft Sentinel](automate-incident-handling-with-automation-rules)
- [Automate threat response with playbooks in Microsoft Sentinel](automate-responses-with-playbooks)
- [Tutorial: Use playbooks with automation rules in Microsoft Sentinel](tutorial-respond-threats-playbook)
- [How to use Microsoft Sentinel for Incident Response, Orchestration and Automation](https://techcommunity.microsoft.com/t5/microsoft-sentinel-blog/how-to-use-azure-sentinel-for-incident-response-orchestration/ba-p/2242397)
- [Adaptive Cards to enhance incident response in Microsoft Sentinel](https://techcommunity.microsoft.com/t5/microsoft-sentinel-blog/using-microsoft-teams-adaptive-cards-to-enhance-incident/ba-p/3330941)

## Post-migration best practices for SOAR in Microsoft Sentinel

Here are best practices you should take into account after your SOAR migration:

- After you migrate your playbooks, test the playbooks extensively to ensure that the migrated actions work as expected.
- Periodically review your automations to explore ways to further simplify or enhance your SOAR. Microsoft Sentinel constantly adds new connectors and actions that can help you to further simplify or increase the effectiveness of your current response implementations.
- Monitor the performance of your playbooks using the [Playbooks health monitoring workbook](https://techcommunity.microsoft.com/t5/microsoft-sentinel-blog/what-s-new-monitoring-your-logic-apps-playbooks-in-azure/ba-p/1873211).
- Use managed identities and service principals: Authenticate against various Azure services within your Logic Apps, store the secrets in Azure Key Vault, and obscure the output of the flow execution. We also recommend that you [monitor non-interactive service principal logins in Microsoft Sentinel](https://techcommunity.microsoft.com/t5/azure-sentinel/non-interactive-logins-minimizing-the-blind-spot/ba-p/2287932).