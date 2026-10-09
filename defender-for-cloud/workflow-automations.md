---
layout: Conceptual
title: Workflow Automation in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/workflow-automations
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Automate security response in Microsoft Defender for Cloud using Azure Logic Apps. Explore triggers, manual runs, and DeployIfNotExist policies.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 8ad0685e-db59-8555-2f20-795750244d13
document_version_independent_id: ff8d8137-d562-429b-2327-ac5478438ded
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/workflow-automations.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/workflow-automations
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/workflow-automations.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e60d1924-c4ad-4104-bd1b-973758bbac7a
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/91d5f984-ee3d-43c4-9daf-bb09a6bc4e1a
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: da5d9b4f-46c9-a468-c41e-76d453fbb111
---

# Workflow Automation in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

Every security program includes multiple workflows for incident response. These processes might include notifying relevant stakeholders, starting a change management process, and applying specific remediation steps.

Security experts recommend that you automate as many steps of security procedures as you can. Automation reduces overhead. It can also improve your security by ensuring process steps are done quickly, consistently, and according to your predefined requirements.

This article describes the workflow automation feature of Microsoft Defender for Cloud. The workflow automation feature can trigger consumption logic apps on security alerts, recommendations, and changes to regulatory compliance. For example, you might want Defender for Cloud to email a specific user when an alert occurs. You also learn how to create logic apps by using [Azure Logic Apps](/en-us/azure/logic-apps/logic-apps-overview).

## Prerequisites

- You need to have **Security admin role** or **Owner** on the resource group.
- You must have write permissions for the target resource.
- To work with Azure Logic Apps workflows, you must have the following Logic Apps roles or permissions:

    - [Logic App Operator](/en-us/azure/role-based-access-control/built-in-roles#logic-app-operator) permissions are required or Logic App read or trigger access. Users with this role can't create or edit logic apps. They can only *run* existing ones.
    - [Logic App Contributor](/en-us/azure/role-based-access-control/built-in-roles#logic-app-contributor) permissions are required for logic app creation and modification.
- If you want to use Logic Apps connectors, you might need other credentials to sign in to their respective services, for example, your Outlook, Teams, or Slack instances.

## Create a logic app and define when it should automatically run

Follow these steps:

1. On the Defender for Cloud sidebar, select **Workflow automation**.

    [![Screenshot that shows the workflow automation pane with the list of defined automations.](media/workflow-automation/list-of-workflow-automations.png)](media/workflow-automation/list-of-workflow-automations.png#lightbox)

    On this page, you can create new automation rules or enable, disable, or delete existing ones. A *scope* refers to the subscription where the workflow automation is deployed.
2. To define a new workflow, select **Add workflow automation**. The options pane for your new automation opens.

    [![Screenshot that shows the Workflow automation pane.](media/workflow-automation/add-workflow.png)](media/workflow-automation/add-workflow.png#lightbox)
3. Enter the following:

    - A name and description for the automation.
    - The triggers that initiate this automatic workflow. For example, you might want your logic app to run when a security alert generates that contains the phrase *SQL*.
4. Specify the consumption logic app that runs when your trigger conditions are met.
5. On the **Actions** section, select **visit the Logic Apps page** to begin the process to create a logic app.

    ![Screenshot that shows the Actions section of the Add workflow automation screen and the link to go to Azure Logic Apps.](media/workflow-automation/visit-logic.png)

    Selecting **visit the Logic Apps page** opens Azure Logic Apps.
6. Select **(+) Add**.
7. Fill out all required fields, and then select **Review + Create**.

    [![Screenshot that shows where to create a logic app.](media/workflow-automation/logic-apps-create-new.png)](media/workflow-automation/logic-apps-create-new.png#lightbox)

    The message **Deployment is in progress** appears. Wait for the **Deployment complete** notification to appear, and then select **Go to resource**.
8. Review the information you entered, and then select **Create**.

    In your new logic app, you can choose from built-in, predefined templates from the security category. Or you can define a custom flow of events that occur when the workflow automation runs.

    Tip

    Sometimes, parameters are included in a logic app in the connector as part of a string and not in their own field. For an example of how to extract parameters, see step 14 of [Working with logic app parameters while building Microsoft Defender for Cloud workflow automations](https://techcommunity.microsoft.com/t5/azure-security-center/working-with-logic-app-parameters-while-building-azure-security/ba-p/1342121).

## Supported triggers

The logic app designer supports the following Defender for Cloud triggers:

- **When a Microsoft Defender for Cloud recommendation is created or triggered**: If your logic app relies on a recommendation that gets deprecated or replaced, your automation stops working and you need to update the trigger. To track changes to recommendations, see [the release notes](release-notes).
- **When a Defender for Cloud Alert is created or triggered**: You can customize the trigger so that it relates only to alerts with the severity levels that interest you.
- **When a Defender for Cloud regulatory compliance assessment is created or triggered**: You want to trigger automations based on updates to regulatory compliance assessments.

Note

If you use the legacy trigger **When a response to a Microsoft Defender for Cloud alert is triggered**, the Workflow Automation feature doesn't open your logic apps. Instead, use the **When a Microsoft Defender for Cloud recommendation is created or triggered** trigger or the **When a Defender for Cloud Alert is created or triggered** trigger.

1. After you define your logic app, return to the **Add workflow automation** pane.
2. Select **Refresh** to ensure your new logic app is available for selection.
3. Select your logic app, and then save the automation. The dropdown menu shows only logic apps that have supporting Defender for Cloud connectors.

## Manually trigger a logic app

You can also manually run logic apps when you view any security alert or recommendation.

To manually run a logic app, open an alert or a recommendation, and then select **Trigger logic app**.

[![Screenshot of the recommendation page with the Trigger logic app option.](media/workflow-automation/manually-trigger-logic-app.png)](media/workflow-automation/manually-trigger-logic-app.png#lightbox)

## Configure workflow automation at scale

When you automate your organization's monitoring and incident response processes, the time it takes to investigate and mitigate security incidents can greatly improve.

To deploy your automation configurations across your organization, use the supplied Azure Policy `DeployIfNotExist` policies described in the following table. The `DeployIfNotExist` policy effect automatically deploys required resources when they don't already exist, allowing you to create and configure workflow automation procedures at scale.

Get started with [workflow automation templates](https://github.com/Azure/Azure-Security-Center/tree/master/Workflow%20automation).

To implement these policies:

1. In the following table, select the policy that you want to apply:

    | Goal | Policy | Policy ID |
    | --- | --- | --- |
    | Workflow automation for security alerts | [Deploy Workflow Automation for Microsoft Defender for Cloud alerts](https://portal.azure.com/#view/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ff1525828-9a90-4fcf-be48-268cdd02361e) | f1525828-9a90-4fcf-be48-268cdd02361e |
    | Workflow automation for security recommendations | [Deploy Workflow Automation for Microsoft Defender for Cloud recommendations](https://portal.azure.com/#view/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F73d6ab6c-2475-4850-afd6-43795f3492ef) | 73d6ab6c-2475-4850-afd6-43795f3492ef |
    | Workflow automation for regulatory compliance changes | [Deploy Workflow Automation for Microsoft Defender for Cloud regulatory compliance](https://portal.azure.com/#view/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F509122b9-ddd9-47ba-a5f1-d0dac20be63c) | 509122b9-ddd9-47ba-a5f1-d0dac20be63c |

    You can also find policies by searching Azure Policy. In Azure Policy, select **Definitions**, and then search for the policies by name.
2. On the relevant Azure Policy page, select **Assign**.

    ![Screenshot of the Azure Policy page with the Assign option highlighted.](media/workflow-automation/export-policy-assign.png)
3. On the **Basics** tab, set the scope for the policy. To use centralized management, assign the policy to the **Management Group** that contains the subscriptions that use the workflow automation configuration.
4. On the **Parameters** tab, enter the required information.

    ![Screenshot that shows the Parameters tab.](media/workflow-automation/parameters-tab.png)
5. (Optional) Apply this assignment to an existing subscription on the **Remediation** tab, and then select the option to create a remediation task.
6. Review the summary page, and then select **Create**.

### Data type schemas for workflow automation

To view the raw event schemas of the security alerts or recommendations events that are passed to the logic app, go to the [data types schemas for workflow automation](https://aka.ms/ASCAutomationSchemas). Viewing the raw event schemas can be useful when you aren't using the built-in Defender for Cloud Logic Apps connectors and are instead using the generic HTTP connector. You can use the event JSON schema to manually parse it as you see fit.