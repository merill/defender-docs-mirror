---
layout: Conceptual
title: Migrate IBM Security QRadar SOAR Automation to Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/migration-qradar-automation
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
description: Learn how to identify SOAR use cases, and how to migrate your QRadar SOAR automation to Microsoft Sentinel.
author: EdB-MSFT
ms.author: edbaynash
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 534f7115-426a-1b29-e7ed-7d5cfa792d19
document_version_independent_id: bec70864-098f-9cd1-828d-83f03873517f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/migration-qradar-automation.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/migration-qradar-automation
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/migration-qradar-automation.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: b5653bc7-60cc-2613-d71b-54f672b96575
---

# Migrate IBM Security QRadar SOAR Automation to Microsoft Sentinel | Microsoft Learn

Microsoft Sentinel provides Security Orchestration, Automation, and Response (SOAR) capabilities with [automation rules](automate-incident-handling-with-automation-rules) and [playbooks](tutorial-respond-threats-playbook). Automation rules automate incident handling and response, and playbooks run predetermined sequences of actions to response and remediate threats. This article discusses how to identify SOAR use cases, and how to migrate your IBM Security QRadar SOAR automation to Microsoft Sentinel.

Automation rules simplify complex workflows for your incident orchestration processes, and allow you to centrally manage your incident handling automation.

With automation rules, you can:

- Perform simple automation tasks without necessarily using playbooks. For example, you can assign, tag incidents, change status, and close incidents.
- Automate responses for multiple analytics rules at once.
- Control the order of actions that are executed.
- Run playbooks for those cases where more complex automation tasks are necessary.

## Identify SOAR use cases

Here’s what you need to think about when migrating SOAR use cases from IBM Security QRadar SOAR.

- **Use case quality**: Choose good use cases for automation. Use cases should be based on procedures that are clearly defined, with minimal variation, and a low false-positive rate. Automation should work with efficient use cases.
- **Manual intervention**: Automated response can have wide ranging effects and high impact automations should have human input to confirm high impact actions before they’re taken.
- **Binary criteria**: To increase response success, decision points within an automated workflow should be as limited as possible, with binary criteria. Binary criteria reduces the need for human intervention, and enhances outcome predictability.
- **Accurate alerts or data**: Response actions are dependent on the accuracy of signals such as alerts. Alerts and enrichment sources should be reliable. Microsoft Sentinel resources such as watchlists and reliable threat intelligence can enhance reliability.
- **Analyst role**: While automation where possible is great, reserve more complex tasks for analysts, and provide them with the opportunity for input into workflows that require validation. In short, response automation should augment and extend analyst capabilities.

## Migrate SOAR workflows to Microsoft Sentinel

This section shows how key SOAR concepts in IBM Security QRadar SOAR translate to Microsoft Sentinel components. This section also provides general guidelines for how to migrate each step or component in the SOAR workflow.

The following diagram labels four numbered workflow stages. The table after the diagram maps each numbered stage from QRadar SOAR to its Microsoft Sentinel equivalent.

[![Diagram displaying the QRadar and Microsoft Sentinel SOAR workflows.](media/migration-qradar-automation/qradar-sentinel-soar-workflow.png)](media/migration-qradar-automation/qradar-sentinel-soar-workflow.png#lightbox)

| Step (in diagram) | IBM Security QRadar SOAR | Microsoft Sentinel |
| --- | --- | --- |
| 1 | Define rules and conditions. | Define automation rules. |
| 2 | Execute ordered activities. | Execute automation rules containing multiple playbooks. |
| 3 | Execute selected workflows. | Execute other playbooks according to tags applied by playbooks that were executed previously. |
| 4 | Post data to message destinations. | Execute code snippets using inline actions in Logic Apps. |

## Map QRadar SOAR components to Microsoft Sentinel capabilities

Review which Microsoft Sentinel or Azure Logic Apps features map to the main QRadar SOAR components.

| QRadar | Microsoft Sentinel/Azure Logic Apps |
| --- | --- |
| Rules | [Analytics rules](detect-threats-built-in) attached to playbooks or automation rules |
| Gateway | [Condition control](/en-us/azure/logic-apps/logic-apps-control-flow-conditional-statement) |
| Scripts | [Inline code](/en-us/azure/logic-apps/logic-apps-add-run-inline-code) |
| Custom action processors | [Custom API calls](/en-us/azure/logic-apps/logic-apps-create-api-app) in Azure Logic Apps or third party connectors |
| Functions | [Azure Function connector](/en-us/azure/logic-apps/logic-apps-azure-functions) |
| Message destinations | [Azure Logic Apps with Azure Service Bus](/en-us/azure/connectors/connectors-create-api-servicebus) |
| IBM X-Force Exchange | • [Automation &gt; Templates tab](use-playbook-templates)• [Content hub catalog](sentinel-solutions-catalog)• [Microsoft Sentinel playbooks on GitHub](https://github.com/Azure/Azure-Sentinel/tree/master/Playbooks/Block-OnPremADUser) |

## Operationalize playbooks and automation rules in Microsoft Sentinel

Most of the playbooks that you use with Microsoft Sentinel are available in either the [Automation &gt; Templates tab](use-playbook-templates), the [Content hub catalog](sentinel-solutions-catalog), or [Microsoft Sentinel playbooks on GitHub](https://github.com/Azure/Azure-Sentinel/tree/master/Playbooks/Block-OnPremADUser). In some cases, however, you might need to create playbooks from scratch or from existing templates.

You typically build your custom logic app using the Azure Logic App Designer feature. The logic apps code is based on [Azure Resource Manager (ARM) templates](/en-us/azure/azure-resource-manager/templates/overview). ARM templates are deployment files that package and move Azure resources across multiple environments. To convert your custom playbook into a portable ARM template, you can use the [ARM template generator](https://techcommunity.microsoft.com/t5/microsoft-sentinel-blog/export-microsoft-sentinel-playbooks-or-azure-logic-apps-with/ba-p/3275898).

Use these articles and blog posts for cases where you need to build your own playbooks either from scratch or from existing templates.

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
- Use managed identities and service principals: Authenticate against various Azure services within your Logic Apps, store the secrets in Azure Key Vault, and obscure the output of the flow execution. We also recommend that you [monitor the activities of the service principals used by your Logic Apps](https://techcommunity.microsoft.com/t5/azure-sentinel/non-interactive-logins-minimizing-the-blind-spot/ba-p/2287932).