---
layout: Conceptual
title: Azure Logic Apps for Microsoft Sentinel playbooks | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/automation/logic-apps-playbooks
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
ms.reviewer: sshuster
description: Learn about Azure Logic Apps concepts and how they work with Microsoft Sentinel playbooks.
ms.author: monaberdugo
author: mberdugo
ms.topic: concept-article
ms.date: 2024-04-18T00:00:00.0000000Z
ms.collection: usx-security
locale: en-us
document_id: f7218205-6938-89aa-ab6a-3b8e8fa9194e
document_version_independent_id: 78022a37-f501-7339-de19-dd1e805f1703
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/automation/logic-apps-playbooks.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/automation/logic-apps-playbooks
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/automation/logic-apps-playbooks.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e60d1924-c4ad-4104-bd1b-973758bbac7a
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/91d5f984-ee3d-43c4-9daf-bb09a6bc4e1a
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: ae4f591b-c5e7-4001-33c4-fafbe495c6e3
---

# Azure Logic Apps for Microsoft Sentinel playbooks | Microsoft Learn

Microsoft Sentinel playbooks are based on workflows built in [Azure Logic Apps](/en-us/azure/logic-apps/logic-apps-overview), a cloud service that helps you schedule, automate, and orchestrate tasks and workflows across systems throughout the enterprise. Microsoft Sentinel playbooks can take advantage of all the power and capabilities of the built-in templates in Azure Logic Apps.

Azure Logic Apps communicates with other systems and services using various types of [connectors](/en-us/connectors/). Use the [Microsoft Sentinel connector](/en-us/connectors/azuresentinel/) to create playbooks that interact with Microsoft Sentinel.

Note

Azure Logic Apps creates separate resources, so additional charges might apply. For more information, visit the [Azure Logic Apps pricing page](https://azure.microsoft.com/pricing/details/logic-apps/).

## Microsoft Sentinel connector components

Within the Microsoft Sentinel connector, use triggers, actions, and dynamic fields to define your playbook's workflow:

| Component | Description |
| --- | --- |
| **Trigger** | A trigger is the connector component that starts a workflow, in this case, a playbook. A Microsoft Sentinel trigger defines the schema that the playbook expects to receive when triggered. The Microsoft Sentinel connector supports the following types of triggers: - [Alert trigger](/en-us/connectors/azuresentinel/#triggers): The playbook receives an alert as input. - [Entity trigger](/en-us/connectors/azuresentinel/#triggers): The playbook receives an entity as input. - [Incident trigger](/en-us/connectors/azuresentinel/#triggers): The playbook receives an incident as input, along with all the included alerts and entities. |
| **Actions** | Actions are all the steps that happen after the trigger. Actions can be arranged sequentially, in parallel, or in a matrix of complex conditions. |
| **Dynamic fields** | Dynamic fields are temporary fields that can be used in the actions that follow your trigger. Dynamic fields are determined by the output schema of triggers and actions, and are populated by their actual output. |

Azure Logic Apps also supports other types of connectors, such as managed connectors, which wrap around API calls, or custom connectors. For more information, see [Azure Logic Apps connectors and their documentation](/en-us/connectors/connector-reference/connector-reference-logicapps-connectors) and [Create your own custom Azure Logic Apps connectors](/en-us/connectors/custom-connectors/create-logic-apps-connector).

## Supported logic app types

Microsoft Sentinel supports both Consumption and Standard logic apps:

- **Consumption**: Runs in multitenant Azure Logic Apps, and uses the classic, original Azure Logic Apps engine.
- **Standard**: Runs in single-tenant Azure Logic Apps, and uses a more recently designed Azure Logic Apps engine.

    Standard resources offer higher performance, fixed pricing, multiple workflow capability, easier API connections management, built-in network capabilities and CI/CD features, and more. However, the following playbook functionality differs for Standard logic apps in Microsoft Sentinel:

    | Feature | Description |
    | --- | --- |
    | **Creating playbooks** | Playbook templates aren't currently supported for Standard workflows, which means that you can't use a template to create your playbook directly in Microsoft Sentinel. Instead, create your workflow manually in Azure Logic Apps to use it as a playbook in Microsoft Sentinel. |
    | **Private endpoints** | If you're using Standard workflows with private endpoints, Microsoft Sentinel requires you to [define an access restriction policy in Logic apps](../define-playbook-access-restrictions) to support those private endpoints in any playbooks based on Standard workflows. Without an access restriction policy, workflows with private endpoints might still be visible and selectable in Microsoft Sentinel, but running them will fail. |
    | **Stateless workflows** | While Standard workflows support both *stateful* and *stateless* in Azure Logic Apps, Microsoft Sentinel doesn't support stateless workflows. For more information, see [Stateful and stateless workflows](/en-us/azure/logic-apps/single-tenant-overview-compare#stateful-and-stateless-workflows). |

## Playbook authentications to Microsoft Sentinel

Azure Logic Apps must connect separately and authenticate independently to each resource, of each type, that it interacts with, including to Microsoft Sentinel itself. Azure Logic Apps uses [specialized connectors](/en-us/connectors/connector-reference/) for this purpose, with each resource type having its own connector.

For more information, see [Authenticate playbooks to Microsoft Sentinel](../authenticate-playbooks-to-sentinel).