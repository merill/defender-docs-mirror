---
layout: Conceptual
title: Migrate Splunk SOAR Automation to Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/migration-splunk-automation
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
description: Learn how to identify SOAR use cases, and how to migrate your Splunk SOAR automation to Microsoft Sentinel.
ms.author: monaberdugo
author: mberdugo
ms.reviewer: sshuster
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 0e74dffa-bfa3-4a7e-b999-289b866fafb7
document_version_independent_id: 19f1cb27-7e50-d3da-8384-143ad05dd57f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/migration-splunk-automation.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/migration-splunk-automation
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/migration-splunk-automation.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 35244061-0f73-bfd3-601b-b34e0b3001fb
---

# Migrate Splunk SOAR Automation to Microsoft Sentinel | Microsoft Learn

Microsoft Sentinel provides Security Orchestration, Automation, and Response (SOAR) capabilities with automation rules and playbooks. Automation rules facilitate simple incident handling and response, while playbooks run more complex sequences of actions to respond and remediate threats. This article discusses how to identify SOAR use cases, and how to migrate your Splunk SOAR automation to Microsoft Sentinel automation rules and playbooks.

For more information about the differences between automation rules and playbooks, see the following articles:

- [Automate threat response with automation rules](automate-incident-handling-with-automation-rules)
- [Automate threat response with playbooks](automation/automate-responses-with-playbooks)

## Identify SOAR use cases

Here's what you need to think about when migrating SOAR use cases from Splunk.

- **Use case quality**: Choose automation use cases based on procedures that are clearly defined, with minimal variation, and a low false-positive rate.
- **Manual intervention**: Automated responses can have wide ranging effects. High impact automations should have human input to confirm high impact actions before they're taken.
- **Binary criteria**: To increase response success, decision points within an automated workflow should be as limited as possible, with binary criteria. When there are only two variables in the automated decision making, the need for human intervention is reduced and outcome predictability is enhanced.
- **Accurate alerts or data**: Response actions are dependent on the accuracy of signals such as alerts. Alerts and enrichment sources should be reliable. Microsoft Sentinel resources such as watchlists and threat intelligence with high confidence ratings enhance reliability.
- **Analyst role**: While automation is great, reserve the most complex tasks for analysts. Provide them with the opportunity for input into workflows that require validation. In short, response automation should augment and extend analyst capabilities.

## Migrate SOAR workflow

This section shows how key Splunk SOAR concepts translate to Microsoft Sentinel components, and provides general guidelines for how to migrate each step or component in the SOAR workflow.

[![Diagram displaying the Splunk and Microsoft Sentinel SOAR workflows.](media/migration-splunk-automation/splunk-sentinel-soar-workflow-new.png)](media/migration-splunk-automation/splunk-sentinel-soar-workflow-new.png#lightbox)

| Step (in diagram) | Splunk | Microsoft Sentinel |
| --- | --- | --- |
| 1 | Ingest events into main index. | Ingest events into the Log Analytics workspace. |
| 2 | Create containers. | Tag incidents using the [custom details feature](surface-custom-details-in-alerts). |
| 3 | Create cases. | Microsoft Sentinel can automatically group incidents according to user-defined criteria, such as shared entities or severity. These alerts then generate incidents. |
| 4 | Create playbooks. | Azure Logic Apps uses several connectors to orchestrate activities across Microsoft Sentinel, Azure, third party and hybrid cloud environments. |
| 4 | Create workbooks. | Microsoft Sentinel executes playbooks either in isolation or as part of an ordered automation rule. You can also execute playbooks manually against alerts or incidents, according to a predefined Security Operations Center (SOC) procedure. |

## Map SOAR components

Review which Microsoft Sentinel or Azure Logic Apps features map to the main Splunk SOAR components.

| Splunk | Microsoft Sentinel/Azure Logic Apps |
| --- | --- |
| Playbook editor | [Logic App designer](/en-us/azure/logic-apps/logic-apps-overview) |
| Trigger | [Trigger](/en-us/azure/logic-apps/logic-apps-overview) |
| - Connectors- App- Automation broker | - [Connector](tutorial-respond-threats-playbook)- [Hybrid Runbook Worker](/en-us/azure/automation/automation-hybrid-runbook-worker) |
| Action blocks | [Action](/en-us/azure/logic-apps/logic-apps-overview) |
| Connectivity broker | [Hybrid Runbook Worker](/en-us/azure/automation/automation-hybrid-runbook-worker) |
| Community | - [Automation &gt; Templates tab](use-playbook-templates)- [Content hub catalog](sentinel-solutions-catalog)- [GitHub](https://github.com/Azure/Azure-Sentinel/tree/master/Playbooks/Block-OnPremADUser) |
| Decision | [Conditional control](/en-us/azure/logic-apps/logic-apps-control-flow-conditional-statement) |
| Code | [Azure Function connector](/en-us/azure/logic-apps/logic-apps-azure-functions) |
| Prompt | [Send approval email](/en-us/azure/logic-apps/tutorial-process-mailing-list-subscriptions-workflow) |
| Format | [Data operations](/en-us/azure/logic-apps/logic-apps-perform-data-operations) |
| Input playbooks | Obtain variable inputs from results of previously executed steps or explicitly declared [variables](/en-us/azure/logic-apps/logic-apps-create-variables-store-values) |
| Set parameters with Utility block API utility | Manage Incidents with the [Microsoft Sentinel Incidents REST API](/en-us/rest/api/securityinsights/stable/incidents/get) |

## Operationalize playbooks and automation rules in Microsoft Sentinel

Most of the playbooks that you use with Microsoft Sentinel are available in either the [Automation &gt; Templates tab](use-playbook-templates), the [Content hub catalog](sentinel-solutions-catalog), or [Microsoft Sentinel playbook samples on GitHub](https://github.com/Azure/Azure-Sentinel/tree/master/Playbooks/Block-OnPremADUser). In some cases, however, you might need to create playbooks from scratch or from existing templates.

You typically build your custom logic app using the Azure Logic App Designer feature. The logic apps code is based on [Azure Resource Manager (ARM) templates](/en-us/azure/azure-resource-manager/templates/overview), which facilitate development, deployment and portability of Azure Logic Apps across multiple environments. To convert your custom playbook into a portable ARM template, you can use the [ARM template generator](https://techcommunity.microsoft.com/t5/microsoft-sentinel-blog/export-microsoft-sentinel-playbooks-or-azure-logic-apps-with/ba-p/3275898).

Use the following articles and tutorials for cases where you need to build your own playbooks either from scratch or from existing templates:

- [Automate incident handling in Microsoft Sentinel](automate-incident-handling-with-automation-rules)
- [Automate threat response with playbooks in Microsoft Sentinel](automate-responses-with-playbooks)
- [Tutorial: Use playbooks with automation rules in Microsoft Sentinel](tutorial-respond-threats-playbook)
- [How to use Microsoft Sentinel for Incident Response, Orchestration and Automation](https://techcommunity.microsoft.com/t5/microsoft-sentinel-blog/how-to-use-azure-sentinel-for-incident-response-orchestration/ba-p/2242397)
- [Adaptive Cards to enhance incident response in Microsoft Sentinel](https://techcommunity.microsoft.com/t5/microsoft-sentinel-blog/using-microsoft-teams-adaptive-cards-to-enhance-incident/ba-p/3330941)

## SOAR post migration best practices

Here are best practices you should take into account after your SOAR migration:

- After you migrate your playbooks, test the playbooks extensively to ensure that the migrated actions work as expected.
- Periodically review your automations to explore ways to further simplify or enhance your SOAR. Microsoft Sentinel constantly adds new connectors and actions that can help you to further simplify or increase the effectiveness of your current response implementations.
- Monitor the performance of your playbooks using the [Playbooks health monitoring workbook](https://techcommunity.microsoft.com/t5/microsoft-sentinel-blog/what-s-new-monitoring-your-logic-apps-playbooks-in-azure/ba-p/1873211).
- Use managed identities and service principals: Authenticate against various Azure services within your Logic Apps, store the secrets in Azure Key Vault, and obscure the flow execution output. We also recommend that you [monitor the activities of these service principals](https://techcommunity.microsoft.com/t5/azure-sentinel/non-interactive-logins-minimizing-the-blind-spot/ba-p/2287932).