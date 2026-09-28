---
layout: Conceptual
title: Discover and deploy Microsoft Sentinel out-of-the-box content from Content hub | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/sentinel-solutions-deploy
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
description: Learn how to find and deploy Sentinel packaged solutions containing data connectors, analytics rules, hunting queries, workbooks, and other content.
ms.author: edbaynash
author: EdB-MSFT
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 4df7b51c-ac81-11ba-9f41-fa179e7a387c
document_version_independent_id: 81b59166-acb5-ae82-3247-51b5203973c0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/sentinel-solutions-deploy.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/sentinel-solutions-deploy
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/sentinel-solutions-deploy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: ebe9f3f9-3827-bab3-292f-b3249674d800
---

# Discover and deploy Microsoft Sentinel out-of-the-box content from Content hub | Microsoft Learn

The Microsoft Sentinel Content hub is your centralized location to discover and manage out-of-the-box (built-in) content. In the Content hub, you find packaged solutions for end-to-end products by domain or industry. You have access to the vast number of standalone contributions hosted in our GitHub repository and feature blades.

- Discover solutions and standalone content with a consistent set of filtering capabilities based on status, content type, support, provider, and category.
- Install content in your workspace all at once or individually.
- View content in list view and quickly see which solutions have updates. Update solutions all at once while standalone content updates automatically.
- Manage a solution to install its content types and get the latest changes.
- Configure standalone content to create new active items based on the most up-to-date template.

If you're a partner who wants to create your own solution, see the [Microsoft Sentinel Solutions Build Guide](https://aka.ms/sentinelsolutionsbuildguide) for solution authoring and publishing.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Prerequisites

To install, update, or delete standalone content or solutions in content hub, you need the **Microsoft Sentinel Contributor** role at the resource group level.

For more information about other roles and permissions supported for Microsoft Sentinel, see [Permissions in Microsoft Sentinel](roles).

## Discover content

The content hub offers the best way to find new content or manage the solutions you already installed.

1. For Microsoft Sentinel in the [Defender portal](https://security.microsoft.com/), select **Microsoft Sentinel** &gt; **Content management** &gt; **Content hub**. For Microsoft Sentinel in the [Azure portal](https://portal.azure.com), under **Content management**, select **Content hub**.

    The **Content hub** page displays a searchable grid or a list of solutions and standalone content.
2. Search for the solutions or standalone content items that you need. Either select specific values from the filters, or enter a search term into the **Search** box. Searches use AI to support fuzzy searches and approximate vocabulary.

    Press **ENTER** to start the search. Results are limited to 50 items, including solutions and content items within solutions. If you don't find what you need, refine your search or try different filters.

    For more information, see [Categories for Microsoft Sentinel out-of-the-box content and solutions](sentinel-solutions#categories-for-microsoft-sentinel-out-of-the-box-content-and-solutions).
3. In the list view (![](media/sentinel-solutions-deploy/list-view.png) ), select a solution from the list to view information about the solution as well as the types of content items it includes.

    Expand a solution in the search or filter results to view the list of content items it includes. The information pane on the side presents detailed information about the content item.

# [Defender portal](#tab/defender-portal)
![Screenshot of the Microsoft Sentinel content hub in the Defender portal.](media/sentinel-solutions-deploy/solutions-list-defender.png)

# [Azure portal](#tab/azure-portal)
![Screenshot of the Microsoft Sentinel content hub in the Azure portal.](media/sentinel-solutions-deploy/solutions-list.png)

---

    Alternately, select the card view (![](media/sentinel-solutions-deploy/card-view.png) ) to view solutions presented in a grid. Each card shows the solution name, description, and categories. Select a card to view more information about the solution on the side.

To use a content item that's part of a solution, you must install the entire solution. If you've selected a specific content item in the list view, select **Install solution** in the details pane on the side to install the relevant solution.

For more information, see [Categories for Microsoft Sentinel out-of-the-box content and solutions](sentinel-solutions#categories-for-microsoft-sentinel-out-of-the-box-content-and-solutions).

## Install or update content

Install standalone content and solutions individually or all together in bulk. For more information on bulk operations, see Bulk install and update content.

If a solution that you deployed has updates since you last deployed it, the list view shows **Update** in the status column. The solution is also included in the **Updates** count at the top of the page.

Here's an example showing the install of an individual solution.

1. In the **Content hub**, search for and select the solution.
2. On the solutions details pane, from the bottom right-hand side, select **View details**.
3. Select **Create** or **Update**.
4. On the **Basics** tab, enter the subscription, resource group, and workspace to deploy the solution. For example:

    ![Screenshot of a solution installation wizard, showing the Basics tab.](media/sentinel-solutions-deploy/wizard-basics.png)
5. Select **Next** to go through the remaining tabs to learn about, and in some cases configure, each of the content components.

    The tabs correspond with the content offered by the solution. Different solutions might have different types of content, so you might not see the same tabs in every solution.

    You might also be prompted to enter credentials to a non-Microsoft service so that Microsoft Sentinel can authenticate to your systems. For example, with playbooks, you might want to take response actions as prescribed in your system.
6. In the **Review + create** tab, wait for the `Validation Passed` message.
7. Select **Create** or **Update** to deploy the solution. You can also select the **Download a template for automation** link to deploy the solution as code.

### Install with dependencies

Some solutions have dependencies to install, including many [domain solutions](sentinel-solutions-catalog#domain-solutions) and solutions that use the unified Azure Monitor Agent (AMA) connectors for [CEF, Syslog](cef-syslog-ama-overview), or [custom logs](connect-custom-logs-ama).

If the solution has dependencies, select **Install with dependencies** to ensure that the required data connectors are also installed. In the dependency selection pane, select one or more of the dependencies to install them along with the original solution. The original solution you chose to install is always selected by default.

If one or more of the dependency solutions is already installed, but has updates, use the **Install/Update** button to both install and update all selected solutions in bulk. For example:

[![Screenshot of installing multiple solution dependencies in bulk.](media/sentinel-solutions-deploy/install-update-dependencies.png)](media/sentinel-solutions-deploy/install-update-dependencies.png#lightbox)

After you install a solution, each content type within the solution might require more steps to configure. For more information, see Enable content items in a solution.

## Bulk install and update content

Content hub supports a list view in addition to the default card view. Select the list view to install multiple solutions and standalone content all at once. Standalone content is kept up-to-date automatically. Any active or custom content created based on solutions or standalone content installed from content hub remains untouched.

1. To install or update items in bulk, change to the list view.
2. Search for or filter to find the content that you want to install or update in bulk.
3. Select the checkbox for each solution or standalone content that you want to install or update.
4. Select the **Install/Update** button. [![Screenshot of solutions list view with multiple solutions selected and in progress for installation.](media/sentinel-solutions-deploy/bulk-install-update.png)](media/sentinel-solutions-deploy/bulk-install-update.png#lightbox)

    If a solution or standalone content you selected was already installed or updated, no action is taken on that item. It doesn't interfere with the update and install of the other items.
5. Select **Manage** for each solution you installed. Content types within the solution might require more information for you to configure. For more information, see Enable content items in a solution.

## Install packages and templates using the API

If you're using the API to install solution packages or individual templates, follow these steps:

1. Retrieve the solution package or template:

    - To retrieve a package, use the [Get Product Package API](/en-us/rest/api/securityinsights/product-package/get).
    - To retrieve an individual template, use the [Get Product Template API](/en-us/rest/api/securityinsights/product-template/get).
2. In the API response, locate the `properties.mainTemplate` field. This field contains the Azure Resource Manager (ARM) template JSON that defines the solution or template resources.
3. Deploy the extracted `mainTemplate` using an [ARM template deployment](/en-us/azure/azure-resource-manager/templates/overview#template-deployment-process), either through the Rest API, Azure CLI, or PowerShell.

## Enable content items in a solution

Centrally manage content items for installed solutions from the content hub.

1. In the content hub, select an installed solution where the version is 2.0.0 or higher.
2. On the solutions details page, select **Manage**.

    [![Screenshot of manage button on details page of the Azure Activity content hub solution.](media/sentinel-solutions-deploy/content-hub-manage-option.png)](media/sentinel-solutions-deploy/content-hub-manage-option.png#lightbox)
3. Review the list of content items.

    [![Screenshot of solution description and list of content items for Azure Activity solution.](media/sentinel-solutions-deploy/manage-solution-azure-activity.png)](media/sentinel-solutions-deploy/manage-solution-azure-activity.png#lightbox)
4. Select a content item to get started.

### Manage each content type

The following sections describe how to work with data connectors, analytics rules, hunting queries, workbooks, parsers, and playbooks as you manage a solution.

#### Connect a data connector

To connect a data connector, complete the configuration steps.

1. Select **Open connector page**.
2. Complete the data connector configuration steps.

    ![Screenshot of data connector content item for Azure Activity solution where status is disconnected.](media/sentinel-solutions-deploy/manage-solution-data-connector-open-connector.png)

    After you configure the data connector and logs are detected, the status changes to **Connected**.

#### Enable an analytics rule

Create a rule from a template or edit an existing rule.

1. View the template in the analytics template gallery.
2. If the template isn't used yet, select **Open** &gt; **Create rule** and follow the steps to enable the analytics rule.

    After you create a rule, the number of active rules created from the template is shown in the **Created content** column.
3. Select the active rules link to edit the existing rule. For example, the active rule link in the following image is under **Content created** and shows **2 items**.

    [![Screenshot of analytics rule content item in solution for Azure Activity.](media/sentinel-solutions-deploy/manage-solution-analytics-rule.png)](media/sentinel-solutions-deploy/manage-solution-analytics-rule.png#lightbox)

#### Run or customize a hunting query

Run the provided hunting query or customize it.

1. To start searching right away, select **Run query** from the details page for quick results.

    [![Screenshot of cloned hunting query content item in solution for Azure Activity.](media/sentinel-solutions-deploy/manage-solution-hunting-query.png)](media/sentinel-solutions-deploy/manage-solution-hunting-query.png#lightbox)
2. To customize your hunting query, select the link in the **Content name** column.

    In the hunting gallery, select the ellipses menu to clone the read-only query template. Cloned queries appear in the content hub **Created content** column.

#### Create a workbook from a template

To customize a workbook, save a copy from the template.

1. Select **View template** to open the workbook and see the visualizations.
2. Select **Save** to create an instance of the workbook template.
3. View your saved customizable workbook by selecting **View saved workbook**.
4. From the content hub, select the **1 item** link in the **Created content** column to manage the workbook.

    [![Screenshot of saved workbook item in solution for Azure Activity.](media/sentinel-solutions-deploy/manage-solution-workbook.png)](media/sentinel-solutions-deploy/manage-solution-workbook.png#lightbox)

#### Use a parser

When a solution is installed, any parsers included are added as workspace functions in Log Analytics.

1. Select **Load the function code** to open Log Analytics and view or run the function code.
2. Select **Use in editor** to open Log Analytics with the parser name ready to add to your custom query.

    [![Screenshot of parser content type in a solution.](media/sentinel-solutions-deploy/manage-solution-parser.png)](media/sentinel-solutions-deploy/manage-solution-parser.png#lightbox)

#### Create a playbook from a template

Create a playbook from a template.

1. Select the **Content name** link of the playbook.
2. Choose the template and select **Create playbook**.
3. After the playbook is created, the active playbook is shown in the **Created content** column.
4. Select the active playbook **1 item** link to manage the playbook.

    [![Screenshot of playbook type content type in a solution.](media/sentinel-solutions-deploy/manage-solution-playbook.png)](media/sentinel-solutions-deploy/manage-solution-playbook.png#lightbox)

## Find the support model for your content

Each solution and standalone content item shows its support model in the **Support** box on its details pane. The box lists either **Microsoft** or a partner name. For example:

[![Screenshot of where you can find your support model for your solution.](media/sentinel-solutions-deploy/find-support-details.png)](media/sentinel-solutions-deploy/find-support-details.png#lightbox)

When you contact support, you might need the publisher, provider, or plan ID for your solution. Find these details on the **Usage information & support** tab of the details page.

![Screenshot of usage and support details for a solution.](media/sentinel-solutions-deploy/usage-support.png)