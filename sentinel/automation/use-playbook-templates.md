---
layout: Conceptual
title: Create and customize Microsoft Sentinel playbooks from templates | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/automation/use-playbook-templates
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
description: This article shows how to create playbooks from and work with playbook templates, to customize them to fit your needs.
ms.topic: how-to
ms.author: monaberdugo
author: mberdugo
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: usx-security
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: a7e84283-e6a3-c9ef-9f1a-e0f2293e5332
document_version_independent_id: 8234e847-1078-6b77-d440-eb1f78afa56a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/automation/use-playbook-templates.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/automation/use-playbook-templates
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/automation/use-playbook-templates.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/e60d1924-c4ad-4104-bd1b-973758bbac7a
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/91d5f984-ee3d-43c4-9daf-bb09a6bc4e1a
platformId: 77e09a5b-4120-cbc9-0fe5-ac12bae84a94
---

# Create and customize Microsoft Sentinel playbooks from templates | Microsoft Learn

A playbook template is a prebuilt, tested, and ready-to-use automation workflow for Microsoft Sentinel that can be customized to meet your needs. Templates can also serve as a reference for best practices when developing playbooks from scratch, or as inspiration for new automation scenarios.

Playbook templates aren't active playbooks themselves, and you must create an editable copy for your needs.

Many playbook templates are developed by the Microsoft Sentinel community, independent software vendors (ISVs), and Microsoft's own experts, based on popular automation scenarios used by security operations centers around the world.

Important

**Playbook templates** are currently in **PREVIEW**. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](../overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline). Starting in **July 2025**, many new customers are [automatically onboarded and redirected to the Defender portal](../overview#changes-for-new-customers-starting-july-2025).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](../move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview). For more information, see [It’s Time to Move: Retiring Microsoft Sentinel’s Azure portal for greater security](https://techcommunity.microsoft.com/blog/microsoft-security-blog/planning-your-move-to-microsoft-defender-portal-for-all-microsoft-sentinel-custo/4428613).

## Prerequisites

To create and manage playbooks, you need access to Microsoft Sentinel with one of the following Azure roles:

- **Logic App Contributor**, to edit and manage logic apps
- **Logic App operator**, to read, enable, and disable logic apps

For more information, see [Microsoft Sentinel playbook prerequisites](automate-responses-with-playbooks#prerequisites).

We recommend that you read [Azure Logic Apps for Microsoft Sentinel playbooks](logic-apps-playbooks) before creating your playbook.

## Access playbook templates

Access playbook templates from the following sources:

| Location | Description |
| --- | --- |
| **Microsoft Sentinel Automation page** | The **Playbook templates** tab lists all installed playbooks. Create one or more active playbooks using the same template. When we publish a new version of a template, any active playbooks created from that template have an extra label added in the **Active playbooks** tab to indicate that an update is available. |
| **Microsoft Sentinel Content hub page** | Playbook templates are available as part of product solutions or standalone content installed from the **Content hub**. For more information, see: [About Microsoft Sentinel content and solutions](../sentinel-solutions)[Discover and manage Microsoft Sentinel out-of-the-box content](../sentinel-solutions-deploy) |
| **GitHub** | The [Microsoft Sentinel GitHub repository](https://github.com/Azure/Azure-Sentinel/tree/master/Playbooks) contains many other playbook templates. Select **Deploy to Azure** to deploy a template to your Azure subscription. |

Technically, a playbook template is an [Azure Resource Manager (ARM) template](/en-us/azure/azure-resource-manager/templates/), which consists of several resources: an Azure Logic Apps workflow and API connections for each connection involved.

The following procedure focuses on deploying a playbook template from the **Playbook templates** tab under **Automation**.

## Explore playbook templates

For Microsoft Sentinel in the [Azure portal](https://portal.azure.com), select the **Content management** &gt; **Content hub** page. For Microsoft Sentinel in the [Defender portal](https://security.microsoft.com/), select **Microsoft Sentinel** &gt; **Content management** &gt; **Content hub**.

On the **Content hub** page, select **Content type** to filter for **Playbook**. The filtered **Content hub** page lists all the solutions and standalone content that include one or more playbook templates. Install the solution or standalone content to get the template.

To view the installed templates, select **Configuration** &gt; **Automation** &gt; **Playbook templates** tab. For example:

[![Screenshot of the playbook templates gallery.](../media/use-playbook-templates/gallery.png)](../media/use-playbook-templates/gallery.png#lightbox)

To find a playbook template that fits your requirements, filter the list by the following criteria:

| Filter | Description |
| --- | --- |
| **Trigger** | Filter by how the playbook is triggered, including incidents, alerts, or entities. For more information, see [Supported Microsoft Sentinel triggers](playbook-triggers-actions#supported-microsoft-sentinel-triggers). |
| **Logic Apps connectors** | Filter by the external services the playbooks interact with. During the deployment process, each connector needs to assume an identity to authenticate to the external service. |
| **Entities** | Filter by the entity types that the playbook expects to find in the incident. For example, a playbook that tells a firewall to block an IP address expects to to find IP addresses in the incident. Such incidents might be created by a Brute Force attack analytics rule. |
| **Tags** | Filter by the labels applied to the playbook, relating the playbook to a specific scenario, or indicating special characteristic. For example: - **Enrichment** - Playbooks that fetch information from another service to add context to an incident. This information is typically added as a comment to the incident or sent to the SOC. - **Remediation** - Playbooks that take an action on the affected entities to eliminate a potential threat. - **Sync** - Playbook that help to keep an external service, such as an incident management service, updated with the incident's properties. - **Notification** - Playbooks that send an email or message. - **Response from Teams** - Playbooks that allow analysts to take a manual action from Teams using interactive cards. |

For example:

![Screenshot of how to filter the list of playbook templates.](../media/use-playbook-templates/filters.png)

## Customize a playbook from a template

The following steps describe how to deploy playbook templates and can be repeated to create multiple playbooks from the same template.

While most playbook templates can be used as they are, we recommend that you adjust them as needed to fit your playbook to your SOC needs.

1. On the **Playbook templates** tab, select a playbook to start from.
2. If the playbook has any prerequisites, make sure to follow the instructions. For example:

    - Some playbooks call other playbooks as actions. The called playbook is referred to as a **nested playbook**. In such a case, one of the prerequisites is to first deploy the nested playbook.
    - Some playbooks require deploying a custom Logic Apps connector or an Azure Function. In such cases, there's a **Deploy to Azure** link that takes you to the general ARM template deployment process.
3. Select **Create playbook** to open the playbook creation wizard based on the selected template. The wizard has four tabs:

    - **Basics:** Locate your new playbook, which is a Logic Apps resource, and give it a name. You can use the default. For example:

        ![Screenshot of the Playbook creation wizard, basics tab.](../media/use-playbook-templates/basics.png)
    - **Parameters:** Enter customer-specific values that the playbook uses. For example, if the playbook sends an email to the SOC, define the recipient address. If the playbook has a custom connector in use, it must be deployed in the same resource group, and you're prompted to enter its name in the **Parameters** tab.

        The **Parameters** tab shows only if the playbook has parameters. For example:

        ![Screenshot of the Playbook creation wizard, parameters tab.](../media/use-playbook-templates/parameters.png)
    - **Connections:** Expand each action to see the existing connections you created for previous playbooks. You can choose to use existing connections, or create a new one. For example:

        ![Screenshot of the Playbook creation wizard, connections tab.](../media/use-playbook-templates/connections.png)

        - To create a new connection, select **Create new connection after deployment**. The **Create new connection after deployment** option takes you to the Logic Apps designer after the deployment process is completed.
        - Custom connectors are listed by the custom connector name entered in the **Parameters** tab.
        - For connectors that support [connecting with managed identity](authenticate-playbooks-to-sentinel#authenticate-with-a-managed-identity), such as **Microsoft Sentinel**, managed identity is the default connection method.

        For more information, see [Authenticate playbooks to Microsoft Sentinel](authenticate-playbooks-to-sentinel).
    - **Review and Create:** View a summary of the process and await validation of your input before creating the playbook.
4. After following the steps in the playbook creation wizard to the end, you're taken to the new playbook's workflow design in the Logic Apps designer. For example:

    [![Screenshot of the playbook in Logic Apps designer.](../media/use-playbook-templates/designer.png)](../media/use-playbook-templates/designer.png#lightbox)
5. For each connector for which you selected **Create new connection after deployment**, create the connection:

    1. From the navigation menu, select **API connections** and then select the connection name. For example:

        ![Screenshot showing how to view A P I connections.](../media/use-playbook-templates/view-api-connections.png)
    2. Select **Edit API connection** from the navigation menu.
    3. Fill in the required parameters and select **Save**. For example:

        ![Screenshot showing how to edit A P I connections.](../media/use-playbook-templates/edit-api-connection.png)

    Alternatively, create a new connection from within the relevant steps in the Logic Apps designer:

    1. For each step that appears with an error sign, select it to expand and then select **Add new**.
    2. Authenticate according to the relevant instructions. For more information, see [Authenticate playbooks to Microsoft Sentinel](authenticate-playbooks-to-sentinel).
    3. If there are other steps using this same connector, expand their boxes. From the list of connections that appears, select the connection you just created.
6. If you have chosen to use a managed identity connection for Microsoft Sentinel, or for other supported connections, make sure to grant permissions to the new playbook on the Microsoft Sentinel workspace or on the relevant target resources for other connectors.
7. Save the playbook. The playbook appears in the **Active Playbooks** tab.

To run your playbook, set an automated response or run it manually. For more information, see [Respond to threats with Microsoft Sentinel playbooks](run-playbooks).

## Report an issue in a playbook template

To report a bug or request an improvement for a playbook, select the **Supported by** link in the playbook's details pane. If the playbook is community-supported, the link takes you to open a GitHub issue. Otherwise, you're directed to the supporter's page, with information about how to send your feedback.