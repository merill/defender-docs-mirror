---
layout: Conceptual
title: Create and manage Microsoft Sentinel playbooks | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/automation/create-playbooks
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
description: Learn how to create and manage Microsoft Sentinel playbooks to automate your incident response and remediate security threats.
ms.author: monaberdugo
author: mberdugo
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 9444208d-51e4-9417-e502-aa81988ede89
document_version_independent_id: e6c30ed3-66db-7985-fcd8-c3326ab97172
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/automation/create-playbooks.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/automation/create-playbooks
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/automation/create-playbooks.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e60d1924-c4ad-4104-bd1b-973758bbac7a
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/91d5f984-ee3d-43c4-9daf-bb09a6bc4e1a
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 225f5a4c-5d77-cbb6-27bc-12e31fff8312
---

# Create and manage Microsoft Sentinel playbooks | Microsoft Learn

Playbooks are collections of procedures that can be run from Microsoft Sentinel in response to an entire incident, to an individual alert, or to a specific entity. A playbook can help automate and orchestrate your response and can be attached to an automation rule to run automatically when specific alerts are generated or when incidents are created or updated. Playbooks can also be run manually on-demand on specific incidents, alerts, or entities.

This article describes how to create and manage Microsoft Sentinel playbooks. Before you begin, make sure you meet the playbook prerequisites, including an Azure subscription and the required Logic App Azure roles. You can later attach these playbooks to analytics rules or automation rules, or run them manually on specific incidents, alerts, or entities.

Note

Playbooks in Microsoft Sentinel are based on workflows built in [Azure Logic Apps overview](/en-us/azure/logic-apps/logic-apps-overview), which means that you get all the power, customizability, and built-in templates of logic apps. Additional charges may apply. For pricing information, visit the [Azure Logic Apps pricing page](https://azure.microsoft.com/pricing/details/logic-apps/).

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](../overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](../move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Prerequisites

Before you create or manage playbooks, make sure you meet the following prerequisites:

- An Azure account and subscription. If you don't have a subscription, [create a free Azure account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- To create and manage playbooks, you need access to Microsoft Sentinel with one of the following Azure roles:

    | Logic app | Azure roles | Description |
    | --- | --- | --- |
    | Consumption | **Logic App Contributor** | Edit and manage logic apps. |
    | Consumption | **Logic App Operator** | Read, enable, and disable logic apps. |
    | Standard | **Logic Apps Standard Operator** | Enable, resubmit, and disable workflows. |
    | Standard | **Logic Apps Standard Developer** | Create and edit workflows. |
    | Standard | **Logic Apps Standard Contributor** | Manage all aspects of a workflow. |

    For more information, see the following documentation:

    - [Secure access to logic app operations in Azure Logic Apps](/en-us/azure/logic-apps/logic-apps-securing-a-logic-app#access-to-logic-app-operations)
    - [Microsoft Sentinel playbook prerequisites](automate-responses-with-playbooks#prerequisites).
- Before you create your playbook, we recommend that you read [Azure Logic Apps for Microsoft Sentinel playbooks](logic-apps-playbooks).

## Create a playbook

Follow these steps to create a new playbook in Microsoft Sentinel:

1. In the [Defender portal](https://security.microsoft.com/) or in the [Azure portal](https://portal.azure.com), go to your Microsoft Sentinel workspace. On the workspace menu, under **Configuration**, select **Automation**.

# [Defender portal](#tab/defender-portal)
[![Screenshot shows Defender portal and Microsoft Sentinel Automation page with Create selected.](../media/create-playbooks/add-new-playbook-defender.png)](../media/create-playbooks/add-new-playbook-defender.png#lightbox)

# [Azure portal](#tab/azure-portal)
[![Screenshot shows Azure portal and Microsoft Sentinel Automation page with Create selected.](../media/create-playbooks/add-new-playbook.png)](../media/create-playbooks/add-new-playbook.png#lightbox)

---
2. From the top menu, select **Create**, and then select one of the following options:

    - If you're creating a **Consumption** playbook, select one of the following options, depending on the trigger you want to use, and then follow the steps to [prepare a **Consumption** logic app playbook](create-playbooks?tabs=consumption#prepare-playbook-logic-app):

        - **Playbook with incident trigger**
        - **Playbook with alert trigger**
        - **Playbook with entity trigger**

        In this example, select **Playbook with entity trigger**.
    - If you're creating a **Standard** playbook, select **Blank playbook** and then [prepare a **Standard** logic app playbook](create-playbooks?tabs=standard#prepare-playbook-logic-app).

    For more information, see [Supported logic app types](logic-apps-playbooks#supported-logic-app-types) and [Supported triggers and actions in Microsoft Sentinel playbooks](playbook-triggers-actions).

## Prepare your playbook's logic app

Select one of the following tabs for details about how to create a logic app for your playbook, depending on whether you're using a Consumption or Standard logic app. For more information, see [Supported logic app types](logic-apps-playbooks#supported-logic-app-types).

Tip

If your playbooks need access to protected resources that are inside or connected to an Azure virtual network, [create a Standard logic app workflow](/en-us/azure/logic-apps/create-single-tenant-workflows-azure-portal).

Standard workflows run in single-tenant Azure Logic Apps and support using private endpoints for inbound traffic so that your workflows can communicate privately and securely with virtual networks. Standard workflows also support virtual network integration for outbound traffic. For more information, see [Secure traffic between virtual networks and single-tenant Azure Logic Apps using private endpoints](/en-us/azure/logic-apps/secure-single-tenant-workflow-virtual-network-private-endpoint).

# [Consumption](#tab/consumption)
After you select the trigger, which includes an incident, alert, or entity trigger, the **Create playbook** wizard appears, for example:

[![Screenshot shows Create playbook wizard and Basics tab for a Consumption workflow-based playbook.](../media/create-playbooks/create-playbook-basics-consumption.png)](../media/create-playbooks/create-playbook-basics-consumption.png#lightbox)

Follow these steps to create your playbook:

1. On the **Basics** tab, provide the following information:

    1. For **Subscription** and **Resource group**, select the values you want from their respective lists.

        The **Region** value is set to the same region as the associated Log Analytics workspace.
    2. For **Playbook name**, enter a name for your playbook.
    3. To monitor this playbook's activity for diagnostic purposes, select **Enable diagnostics logs in Log Analytics**, and then select a **Log Analytics workspace** unless you already selected a workspace.
2. Select **Next : Connections &gt;**.
3. On the **Connections** tab, we recommend leaving the default values, which configure a logic app to connect to Microsoft Sentinel with a managed identity.

    For more information, see [Authenticate playbooks to Microsoft Sentinel](authenticate-playbooks-to-sentinel).
4. To continue, select **Next : Review and create &gt;**.
5. On the **Review and create** tab, review your configuration choices, and select **Create playbook**.

    Azure takes a few minutes to create and deploy your playbook. After deployment completes, your playbook opens in the Consumption workflow designer for [Azure Logic Apps](/en-us/azure/logic-apps/logic-apps-overview). The trigger that you selected earlier automatically appears as the first step in your workflow, so now you can continue building the workflow from here.

    [![Screenshot shows Consumption workflow designer with selected trigger.](../media/create-playbooks/designer-consumption.png)](../media/create-playbooks/designer-consumption.png#lightbox)
6. On the designer, select the Microsoft Sentinel trigger, if not already selected.
7. On the **Create connection** pane, follow these steps to provide the required information to connect to Microsoft Sentinel.

    1. For **Authentication**, select from the following methods, which affect subsequent connection parameters:

        | Method | Description |
        | --- | --- |
        | **OAuth** | Open Authorization (OAuth) is a technology standard that lets you authorize an app or service to sign in to another without exposing private information, such as passwords. OAuth 2.0 is the industry protocol for authorization and grants limited access to protected resources. For more information, see the following resources: - [What is OAuth](https://www.microsoft.com/security/business/security-101/what-is-oauth)? - [OAuth 2.0 authorization with Microsoft Entra ID](/en-us/entra/architecture/auth-oauth2) |
        | **Service principal** | A service principal represents an entity that requires access to resources that are secured by a Microsoft Entra tenant. For more information, see [Service principal object](/en-us/entra/identity-platform/app-objects-and-service-principals). |
        | **Managed identity** | An identity that is automatically managed in Microsoft Entra ID. Apps can use this identity to access resources that support Microsoft Entra authentication and to obtain Microsoft Entra tokens without having to manage any credentials. For optimal security, Microsoft recommends using a managed identity for authentication when possible. This option provides superior security and helps keep authentication information secure so that you don't have to manage this sensitive information. For more information, see the following resources: - [What are managed identities for Azure resources](/en-us/entra/identity/managed-identities-azure-resources/overview)? - [Authenticate access and connections to Azure resources with managed identities in Azure Logic Apps](/en-us/azure/logic-apps/authenticate-with-managed-identity). |

        For more information about authentication options and prompts, see Authenticate connections for your playbook actions.
    2. Based on your selected authentication option, provide the necessary parameter values for the corresponding option.

        For more information about these parameters, see [Microsoft Sentinel connector reference](/en-us/connectors/azuresentinel/).
    3. For **Tenant ID**, select your [Microsoft Entra tenant ID](/en-us/entra/fundamentals/how-to-find-tenant).
    4. When you finish, select **Sign in**.
8. If you previously chose **Playbook with entity trigger**, select the type of entity you want this playbook to receive as an input.

    [![Screenshot shows Consumption workflow playbook with entity trigger, and available entity types to select for setting the playbook schema.](../media/create-playbooks/entity-trigger-types.png)](../media/create-playbooks/entity-trigger-types.png#lightbox)

# [Standard](#tab/standard)
Playbooks based on a Standard workflow don't support playbook templates, so you need to first create a Standard logic app, then create your playbook, and finally choose the trigger for your playbook.

After you select **Blank playbook**, a new browser tab opens, and **Create Logic App** wizard appears. The wizard shows the available hosting options where **Standard - Workflow Service Plan** is already selected, for example:

[![Screenshot shows hosting options page for creating a logic app.](../media/create-playbooks/logic-apps-hosting-options.png)](../media/create-playbooks/logic-apps-hosting-options.png#lightbox)

Follow these steps to create your Standard logic app:

#### Create Standard logic app

To create and configure your Standard logic app resource, follow these steps:

1. On the **Create Logic App** page, confirm your hosting plan selection, and then select **Select**.
2. On the **Basics** tab, provide the following information:

    1. For **Subscription** and **Resource Group**, select the values you want from their respective lists.
    2. For **Logic App name**, enter a name for your logic app.
    3. For **Region**, select the Azure region for your logic app.
    4. For **Windows Plan (*selected-region*)**, create or select an existing plan.
    5. For **Pricing plan**, select the compute resources and their pricing for your logic app.
    6. Under **Zone redundancy**, you can enable this capability if you selected an Azure region that supports availability zone redundancy.

        For this example, leave the option disabled. For more information, see [Protect logic apps from region failures with zone redundancy and availability zones](/en-us/azure/logic-apps/set-up-zone-redundancy-availability-zones).
    7. Select **Next : Storage &gt;**.

    [![Screenshot shows Create Logic App wizard and Basics tab for a Standard logic app.](../media/create-playbooks/create-logic-app-basics-standard.png)](../media/create-playbooks/create-logic-app-basics-standard.png#lightbox)
3. On the **Storage** tab, provide the following information:

    1. For **Storage type**, select **Azure Storage**, and create or select a storage account.
    2. For **Blob service diagnostic settings**, leave the default setting.
4. On the **Networking** tab, you can leave the default options for this example.

    For your specific, real-world, production scenarios, make sure to review and select the appropriate options. You can also change this configuration after you deploy your logic app resource. For more information, see the following documentation:

    - [Create example Standard workflow - Azure portal](/en-us/azure/logic-apps/create-single-tenant-workflows-azure-portal)
    - [Secure traffic between Standard logic apps and Azure virtual networks using private endpoints](/en-us/azure/logic-apps/secure-single-tenant-workflow-virtual-network-private-endpoint).
5. On the **Monitoring** tab, follow these steps:

    1. Under **Application Insights**, set **Enable Application Insights** to **No**.

        This setting disables or enables performance monitoring with Application Insights in Azure Monitor. However, for Microsoft Sentinel, this capability isn't required and costs extra.
    2. To apply tags to this logic app for resource categorization and billing purposes, select **Next : Tags &gt;**. Otherwise, select **Review + create**.
6. On the **Review + create** tab, review your configuration choices, and select **Create**.

    Azure takes a few minutes to create and deploy your logic app.
7. After deployment completes, select **Go to resource**, which opens your logic app resource.

    Unlike with classic Consumption playbooks, you're not done yet. Now you must create a workflow.

#### Create a workflow for your playbook

After your Standard logic app is deployed, create a workflow to define your playbook's logic:

1. On your logic app menu, under **Workflows**, select **Workflows**.
2. On the **Workflows** page toolbar, select **Add**.
3. In the **New workflow** pane, provide the following information:

    | Property | Description |
    | --- | --- |
    | **Workflow Name** | A meaningful name for your workflow. |
    | **State type** | Select **Stateful**. Microsoft Sentinel doesn't support the use of stateless workflows as playbooks. |
4. When you finish, select **Create**.

    After Azure saves your workflow, the **Workflows** page shows your workflow.
5. Select the workflow to open the workflow **Overview** page.

    This page shows all the information about your workflow, including the history of all the times that the workflow runs.
6. On the workflow menu, under **Developer**, select **Designer**.

    The workflow designer opens for you to start building your workflow by adding a trigger.

#### Add the workflow trigger

To add a Microsoft Sentinel trigger to your workflow, follow these steps:

1. On the designer, select **Add a trigger** to open the **Add a trigger** pane, for example:

    [![Screenshot shows designer in Standard logic app workflow.](../media/create-playbooks/designer-standard.png)](../media/create-playbooks/designer-standard.png#lightbox)
2. [Find the **Microsoft Sentinel** triggers in the workflow designer](/en-us/azure/logic-apps/create-workflow-with-trigger-or-action?tabs=standard#add-trigger). The available triggers include:

    - **Microsoft Sentinel entity**
    - **Microsoft Sentinel alert**
    - **Microsoft Sentinel incident**

    [![Screenshot shows how to select a trigger for your playbook.](../media/create-playbooks/sentinel-triggers.png)](../media/create-playbooks/sentinel-triggers.png#lightbox)
3. Select the trigger that you want to use for your playbook.

    This example continues with the **Microsoft Sentinel entity** trigger.
4. On the designer, select the trigger, if not already selected.
5. On the **Create connection** pane, provide the required information to connect to Microsoft Sentinel.

    1. For **Authentication**, select from the following methods, which affect subsequent connection parameters:

        | Method | Description |
        | --- | --- |
        | **OAuth** | Open Authorization (OAuth) is a technology standard that lets you authorize an app or service to sign in to another without exposing private information, such as passwords. OAuth 2.0 is the industry protocol for authorization and grants limited access to protected resources. For more information, see the following resources: - [What is OAuth](https://www.microsoft.com/security/business/security-101/what-is-oauth)? - [OAuth 2.0 authorization with Microsoft Entra ID](/en-us/entra/architecture/auth-oauth2) |
        | **Service principal** | A service principal represents an entity that requires access to resources that are secured by a Microsoft Entra tenant. For more information, see [Service principal object](/en-us/entra/identity-platform/app-objects-and-service-principals). |
        | **Managed identity** | An identity that is automatically managed in Microsoft Entra ID. Apps can use this identity to access resources that support Microsoft Entra authentication and to obtain Microsoft Entra tokens without having to manage any credentials. For optimal security, Microsoft recommends using a managed identity for authentication when possible. This option provides superior security and helps keep authentication information secure so that you don't have to manage this sensitive information. For more information, see the following resources: - [What are managed identities for Azure resources](/en-us/entra/identity/managed-identities-azure-resources/overview)? - [Authenticate access and connections to Azure resources with managed identities in Azure Logic Apps](/en-us/azure/logic-apps/authenticate-with-managed-identity). |

        For more information about the authentication types and prompts shown by the Microsoft Sentinel connector, see Authenticate connections for your playbook actions.
    2. Based on your selected authentication option, provide the necessary parameter values for the corresponding option.

        For more information about these parameters, see [Microsoft Sentinel connector reference](/en-us/connectors/azuresentinel/).
    3. For **Tenant ID**, select your [Microsoft Entra tenant ID](/en-us/entra/fundamentals/how-to-find-tenant).
    4. When you finish, select **Sign in**.
6. If you chose **Playbook with entity trigger**, select the type of entity you want this playbook to receive as an input.

    [![Screenshot shows Standard workflow playbook with entity trigger, and available entity types to select for setting the playbook schema.](../media/create-playbooks/entity-trigger-types.png)](../media/create-playbooks/entity-trigger-types.png#lightbox)

For more information, see [Supported triggers and actions in Microsoft Sentinel playbooks](playbook-triggers-actions).

---

### Authenticate connections for your playbook actions

When you add a trigger or subsequent action that requires authentication, you might be prompted to choose from the available authentication types supported by the corresponding resource provider. In this example, a Microsoft Sentinel trigger is the first operation that you add to your workflow. So, the resource provider is Microsoft Sentinel, which supports several authentication options. For more information, see the following documentation:

- [**Authenticate playbooks to Microsoft Sentinel**](authenticate-playbooks-to-sentinel)
- [**Supported triggers and actions in Microsoft Sentinel playbooks**](playbook-triggers-actions)

### Add actions to your playbook

Now that you have a workflow for your playbook, define what happens when you call the playbook. Add actions, logical conditions, loops, or switch case conditions, all by selecting the plus sign (**+**) on the designer. For more information, see [Create a workflow with a trigger or action](/en-us/azure/logic-apps/create-workflow-with-trigger-or-action).

This selection opens the **Add an action** pane where you can browse or search for services, applications, systems, control flow actions, and more. After you enter your search terms or select the resource that you want, the results list shows you the available actions.

In each action, when you select inside a field, you get the following options:

- **Dynamic content** (lightning icon): Choose from a list of available outputs from the preceding actions in the workflow, including the Microsoft Sentinel trigger. For example, these outputs can include the attributes of an alert or incident that was passed to the playbook, including the values and attributes of all the [map data fields to entities](../map-data-fields-to-entities) and [surface custom details in alerts](../surface-custom-details-in-alerts) in the alert or incident. You can add references to the current action by selecting these outputs.

    For examples that show using dynamic content, see Use entity playbooks with no incident ID and Work with custom details.
- **Expression editor** (function icon): Choose from a large library of functions to add more logic to your workflow.

For more information, see [Supported triggers and actions in Microsoft Sentinel playbooks](playbook-triggers-actions).

### Dynamic content: Entity playbooks with no incident ID

Playbooks created with the **Microsoft Sentinel entity** trigger often use the **Incident ARM ID** field, which contains the Azure Resource Manager identifier for the associated incident. This field is used, for example, to update an incident after taking action on the entity. If such a playbook is triggered in a scenario that's unconnected to an incident, such as when threat hunting, there's no incident ID to populate this field. Instead, the field is populated with a null value. As a result, the playbook might fail to run to completion.

To prevent this failure, we recommend that you create a condition that checks for a value in the incident ID field before the workflow takes any other actions. You can prescribe a different set of actions to take if the field has a null value, due to the playbook not being run from an incident.

1. In your workflow, preceding the first action that refers to the **Incident ARM ID** field, [add a **Condition** action in the workflow designer](/en-us/azure/logic-apps/create-workflow-with-trigger-or-action).
2. In the **Condition** pane, on the condition row, select the left **Choose a value** field, and then select the dynamic content option (lightning icon).
3. From the dynamic content list, under **Microsoft Sentinel incident**, use the search box to find and select **Incident ARM ID**.

    Tip

    If the output doesn't appear in the list, next to the trigger name, select **See more**.
4. In the middle field, from the operator list, select **is not equal to**.
5. In the right **Choose a value** field, and select the expression editor option (function icon).
6. In the editor, enter **null**, and select **Add**.

When you finish, your condition looks similar to the following example:

[![Screenshot shows extra condition to add before the Incident ARM ID field.](../media/create-playbooks/no-incident-id.png)](../media/create-playbooks/no-incident-id.png#lightbox)

### Dynamic content: Work with custom details

In the **Microsoft Sentinel incident** trigger, the **Alert custom details** output is an array of JSON objects where each represents a custom detail, as described in [Surface custom details in alerts](../surface-custom-details-in-alerts). Custom details are key-value pairs that let you surface information from events in the alert so they can be represented, tracked, and analyzed as part of the incident.

This field in the alert is customizable, so its schema depends on the type of event that is surfaced. To generate the schema that determines how to parse the custom details output, provide the data from an instance of this event:

1. On the Microsoft Sentinel workspace menu, under **Configuration**, select **Analytics**.
2. Follow the steps to create or open an existing [create a scheduled analytics rule](../create-analytics-rules?tabs=azure-portal) or [create an NRT analytics rule](../create-nrt-rules?tabs=azure-portal).
3. On the **Set rule logic** tab, [expand the **Custom details** section](../surface-custom-details-in-alerts?tabs=azure), for example:

    [![Screenshot shows custom details defined in an analytics rule.](../media/create-playbooks/custom-details-values.png)](../media/create-playbooks/custom-details-values.png#lightbox)

    The following table provides more information about these key-value pairs:

    | Item | Location | Description |
    | --- | --- | --- |
    | **Key** | Left column | Represents the custom fields that you create. |
    | **Value** | Right column | Represents the fields from the event data that populate the custom fields. |
4. To generate the schema, provide the following example JSON code:

    ```json
    { "FirstCustomField": [ "1", "2" ], "SecondCustomField": [ "a", "b" ] }
    ```

    The code shows the key names as arrays, and the values as items in the arrays. Values are shown as the actual values, not the column that contains the values.

To use custom fields for incident triggers, follow these steps for your workflow:

1. In the workflow designer, under the **Microsoft Sentinel incident** trigger, add the built-in action named **Parse JSON**.
2. Select inside the action's **Content** parameter, and select the dynamic content list option (lightning icon).
3. From the list, in the incident trigger section, find and select **Alert Custom Details**, for example:

    [![Screenshot shows selected Alert Custom Details in dynamic content list.](../media/create-playbooks/custom-details-dynamic-field.png)](../media/create-playbooks/custom-details-dynamic-field.png#lightbox)

    This selection automatically adds a **For each** loop around **Parse JSON** because an incident contains an array of alerts.
4. In the **Parse JSON** information pane, select **Use sample payload to generate schema**, for example:

    [![Screenshot shows selection for Use sample payload to generate schema link.](../media/create-playbooks/generate-schema-link.png)](../media/create-playbooks/generate-schema-link.png#lightbox)
5. In the **Enter or paste a sample JSON payload** box, provide a sample payload, and select **Done**.

    For example, you can find a sample payload by looking in Log Analytics for another instance of this alert, and then copying the custom details object, which you can find under **Extended Properties**. To access Log Analytics data, go either to the **Logs** page in the Azure portal or the **Advanced hunting** page in the Defender portal.

    The following example shows the sample custom-details JSON payload from step 4 in the schema generation procedure:

    [![Screenshot shows sample JSON payload.](../media/create-playbooks/sample-payload.png)](../media/create-playbooks/sample-payload.png#lightbox)

    When you finish, the **Schema** box now contains the generated schema based on the sample that you provided. The **Parse JSON** action creates custom fields that you can now use as dynamic fields with **Array** type in your workflow's subsequent actions.

    The following example shows an array and its items, both in the schema and in the dynamic content list for a subsequent action named **Compose**:

    [![Screenshot shows ready to use dynamic fields from the schema.](../media/create-playbooks/custom-fields-ready-to-use.png)](../media/create-playbooks/custom-fields-ready-to-use.png#lightbox)

## Manage your playbooks

Select the **Automation &gt; Active playbooks** tab to view all the playbooks you have access to, filtered by your subscription view.

After you onboard to the Microsoft Defender portal, by default the **Active playbooks** tab shows a predefined filter with onboarded workspace's subscription. **In the Azure portal**, edit the subscriptions you're showing from the **Directory + subscription** menu in the global Azure page header.

While the **Active playbooks** tab displays all the active playbooks available across any selected subscriptions, by default a playbook can be used only within the subscription to which it belongs, unless you specifically grant Microsoft Sentinel permissions to the playbook's resource group.

The **Active playbooks** tab shows your playbooks with the following details:

| Column name | Description |
| --- | --- |
| **Status** | Indicates if the playbook is enabled or disabled. |
| **Plan** | Indicates whether the playbook uses the *Standard* or *Consumption* Azure Logic Apps resource type. Playbooks of the *Standard* type use the `LogicApp/Workflow` naming convention, which reflects how a Standard playbook represents a workflow that exists alongside other workflows in a single logic app. For more information, see [Azure Logic Apps for Microsoft Sentinel playbooks](logic-apps-playbooks). |
| **Trigger kind** | Indicates the trigger in Azure Logic Apps that starts this playbook: - **Microsoft Sentinel Incident/Alert/Entity**: The playbook is started with one of the Sentinel triggers, including incident, alert, or entity - **Using Microsoft Sentinel Action**: The playbook is started with a non-Microsoft Sentinel trigger but uses a Microsoft Sentinel action - **Other**: The playbook doesn't include any Microsoft Sentinel components - **Not initialized**: The playbook was created, but contains no components, neither triggers no actions. |

Select a playbook to open its Azure Logic Apps page, which shows more details about the playbook. On the Azure Logic Apps page:

- View a log of all times the playbook ran
- View run results, including successes and failures and other details
- If you have the relevant permissions, open the workflow designer in Azure Logic Apps to edit the playbook directly