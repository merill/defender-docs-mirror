---
layout: Conceptual
title: Automate Threat Response with Playbooks in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/automation/automate-responses-with-playbooks
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
description: Learn how to automate threat response in Microsoft Sentinel using playbooks to efficiently manage security alerts and incidents.
ms.topic: how-to
ms.author: monaberdugo
author: mberdugo
ms.date: 2026-06-12T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1014
locale: en-us
document_id: 7b0f01f1-d9b1-af3b-9900-3dd68afddc98
document_version_independent_id: 0bcb222a-f2b9-340e-11d2-d99be6453a9d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/automation/automate-responses-with-playbooks.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/automation/automate-responses-with-playbooks
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/automation/automate-responses-with-playbooks.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/e60d1924-c4ad-4104-bd1b-973758bbac7a
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/91d5f984-ee3d-43c4-9daf-bb09a6bc4e1a
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
platformId: 0440610e-0429-b5cf-e1ce-3e3a85208654
---

# Automate Threat Response with Playbooks in Microsoft Sentinel | Microsoft Learn

Security operations centers (SOCs) face a constant stream of security alerts and incidents. Managing these efficiently is critical to keeping your organization’s security strong. Microsoft Sentinel playbooks are automated workflows that help you respond to threats quickly and consistently. This article shows how to use playbooks in Microsoft Sentinel to automate threat response, cut manual effort, and let your team focus on deeper investigations.

Use Microsoft Sentinel playbooks to run preconfigured sets of remediation actions and [automate and orchestrate your threat response](tutorial-respond-threats-playbook). Run playbooks automatically in response to specific alerts and incidents that trigger a configured [automation rule](../automate-incident-handling-with-automation-rules), or run them manually for a particular entity or alert.

For example, if an account and machine are compromised, a playbook can automatically isolate the machine from the network and block the account before the SOC team gets notified of the incident.

Note

Because playbooks use Azure Logic Apps, additional charges can apply. Go to the [Azure Logic Apps](https://azure.microsoft.com/pricing/details/logic-apps/) pricing page for more details.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](../overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](../move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Recommended use cases

The following table lists common use cases where Microsoft Sentinel playbooks help automate threat response:

| Use case | Description |
| --- | --- |
| **Enrichment** | Collect data and attach it to an incident so your team can make better decisions. |
| **Bi-directional sync** | Sync Microsoft Sentinel incidents with other ticketing systems. For example, create an automation rule for all new incidents, and attach a playbook that opens a ticket in ServiceNow. |
| **Orchestration** | Use the SOC team's chat platform to manage the incident queue. For example, send a message to your security operations channel in Microsoft Teams or Slack so your security analysts know about the incident. |
| **Response** | Respond to threats right away with minimal human involvement, such as when a compromised user or machine is detected. Or, manually trigger automated steps during an investigation or while hunting. |

For more information, see [Recommended playbook use cases, templates, and examples](playbook-recommendations).

## Prerequisites

You need the following roles to use Azure Logic Apps to create and run playbooks in Microsoft Sentinel.

| Role | Description |
| --- | --- |
| **Owner** | Lets you grant access to playbooks in the resource group. |
| **Microsoft Sentinel Contributor** | Lets you attach a playbook to an analytics or automation rule. |
| **Microsoft Sentinel Responder** | Lets you access an incident in order to run a playbook manually, but doesn't allow you to run the playbook. |
| **Microsoft Sentinel Playbook Operator** | Lets you run a playbook manually. |
| **Microsoft Sentinel Automation Contributor** | Allows automation rules to run playbooks. This role isn't used for any other purpose. |

The following table describes required roles based on whether you select a Consumption or Standard logic app to create your playbook:

| Logic app | Azure roles | Description |
| --- | --- | --- |
| Consumption | **Logic App Contributor** | Edit and manage logic apps. Run playbooks. Doesn't allow you to grant access to playbooks. |
| Consumption | **Logic App Operator** | Read, enable, and disable logic apps. Doesn't allow you to edit or update logic apps. |
| Standard | **Logic Apps Standard Operator** | Enable, resubmit, and disable workflows in a logic app. |
| Standard | **Logic Apps Standard Developer** | Create and edit logic apps. |
| Standard | **Logic Apps Standard Contributor** | Manage all aspects of a logic app. |

The **Active playbooks** tab on the **Automation** page displays all active playbooks available across any selected subscriptions. By default, a playbook can be used only within the subscription to which it belongs, unless you specifically grant Microsoft Sentinel permissions to the playbook's resource group.

### Extra permissions required for Microsoft Sentinel to run playbooks

Microsoft Sentinel also needs additional permissions to run playbooks on your behalf.

Microsoft Sentinel uses a service account to run playbooks on incidents, to add security and enable the automation rules API to support CI/CD use cases. This service account is used for incident-triggered playbooks, or when you run a playbook manually on a specific incident.

In addition to your own roles and permissions, this Microsoft Sentinel service account must have its own set of permissions on the resource group where the playbook resides, in the form of the **Microsoft Sentinel Automation Contributor** role. Once Microsoft Sentinel has this role, it can run any playbook in the relevant resource group, manually or from an automation rule.

To grant Microsoft Sentinel with the required permissions, you must have an **Owner** or **User access administrator** role. To run the playbooks, you'll also need the **Logic App Contributor** role on the resource group that contains the playbooks you want to run.

## Playbook templates (preview)

Important

Playbook templates are currently in PREVIEW. See the **[Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)** for additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

Playbook templates are prebuilt, tested, and ready-to-use workflows that aren't usable as playbooks themselves, but are ready for you to customize to meet your needs. We also recommend that you use playbook templates as a reference of best practices when developing playbooks from scratch, or as inspiration for new automation scenarios.

Get playbook templates from these sources:

| Location | Description |
| --- | --- |
| **Microsoft Sentinel Automation page** | The **Playbook templates** tab shows all installed playbooks. Create one or more active playbooks using the same template. When a new version of a template is published, any active playbooks created from that template get an extra label in the **Active playbooks** tab to show that an update is available. |
| **Microsoft Sentinel Content hub page** | Playbook templates are part of product solutions or standalone content you install from the **Content hub**. For more information, see: [About Microsoft Sentinel content and solutions](../sentinel-solutions)[Discover and manage Microsoft Sentinel out-of-the-box content](../sentinel-solutions-deploy) |
| **GitHub** | The [Microsoft Sentinel GitHub repository](https://github.com/Azure/Azure-Sentinel/tree/master/Playbooks) has many other playbook templates. Select **Deploy to Azure** to deploy a template to your Azure subscription. |

A playbook template is an [Azure Resource Manager (ARM) template](/en-us/azure/azure-resource-manager/templates/) that includes several resources: an Azure Logic Apps workflow and API connections for each connection involved.

For more information, see:

- [Create and customize Microsoft Sentinel playbooks from content templates](use-playbook-templates)
- [Recommended playbook templates](playbook-recommendations#recommended-playbook-templates)
- [Azure Logic Apps for Microsoft Sentinel playbooks](logic-apps-playbooks)

## Playbook creation and usage workflow

Follow these steps to create and run Microsoft Sentinel playbooks:

1. Define your automation scenario. Review [recommended playbooks use cases](playbook-recommendations#recommended-playbook-use-cases) and [playbook templates](playbook-recommendations#recommended-playbook-templates) to get started.
2. If you're not using a template, create your playbook and build your logic app. For more information, see [Create and manage Microsoft Sentinel playbooks](create-playbooks).

    Test your logic app by running it manually. For more information, see [Run a playbook manually, on demand](run-playbooks#run-a-playbook-manually-on-demand).
3. Set up your playbook to run automatically when a new alert or incident is created, or run it manually as needed for your process. For more information, see [Respond to threats with Microsoft Sentinel playbooks](run-playbooks).