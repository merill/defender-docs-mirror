---
layout: Conceptual
title: Automate and Run Microsoft Sentinel Playbooks | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/automation/run-playbooks
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
description: Learn how to run Microsoft Sentinel and Microsoft Defender playbooks, configure permissions, and review results for security investigations.
ms.author: guyshmeltzer
author: guyshmeltzer
ms.topic: how-to
ms.date: 2026-11-01T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1032
locale: en-us
document_id: a37eabcb-35e3-d257-8b1a-9ed19319b488
document_version_independent_id: 3508a767-2ee2-16ba-e489-d2ccba7b64d6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/automation/run-playbooks.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/automation/run-playbooks
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/automation/run-playbooks.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/e60d1924-c4ad-4104-bd1b-973758bbac7a
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/91d5f984-ee3d-43c4-9daf-bb09a6bc4e1a
platformId: 5b1e0c92-618f-a617-919a-2dea7d0396cc
---

# Automate and Run Microsoft Sentinel Playbooks | Microsoft Learn

Use automation rules to run playbooks automatically when a case, incident, or alert matches the rule's trigger and conditions. You can also run playbooks manually on demand in response to cases, incidents, alerts, or entities, without an automation rule.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](../overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](../move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

Note

Azure Logic App playbooks are built on [Azure Logic Apps](/en-us/azure/logic-apps/logic-apps-overview). These playbooks use either the Microsoft Sentinel connector or the Microsoft Defender SOC connector for their triggers and input data. You can customize these workflows and use built-in Logic Apps templates. Additional charges might apply. See the [Azure Logic Apps pricing page](https://azure.microsoft.com/pricing/details/logic-apps/) for details.

The Defender portal also supports [generated playbooks](/en-us/defender-xdr/siem-defender-generate-playbooks), which are code-based workflows, not Logic Apps. For details about the new Logic App connector, see the [Microsoft Defender SOC connector reference](/en-us/connectors/defendersoc/). For manual execution instructions for all three families, see Run a playbook manually, on demand.

## Prerequisites

The permissions you need depend on the playbook family and your task. For manual runs, you also need access to the investigation page.

### Microsoft Defender unified RBAC permissions

For generated playbooks and Microsoft Defender SOC Logic Apps, your Microsoft Defender unified role-based access control (RBAC) role needs the [Automation permission](/en-us/defender-xdr/custom-permissions-details#security-operations--security-data) that matches your task:

| Task | Permission |
| --- | --- |
| Create, manage, and run playbooks | **Playbooks** with **Manage** access |
| Run existing playbooks without authoring access | **Execute hard actions** |
| Create an automation rule | **Automation rules** with **Manage** access |

For execution, either playbook permission is sufficient; you don't need both.

### Azure RBAC permissions

Azure role-based access control (RBAC) permissions are required for Microsoft Defender SOC Logic Apps and Microsoft Sentinel connector Logic Apps. Generated playbooks aren't Logic Apps and don't require these Azure roles.

For Microsoft Defender SOC Logic Apps, you need the appropriate Azure user roles for the Logic App in addition to Defender unified RBAC execution permission. See [Azure Logic Apps access permissions](/en-us/azure/logic-apps/set-up-security-permissions#secure-access-to-logic-app-operations-with-azure-rbac).

#### Required Azure roles to run playbooks

For Microsoft Sentinel connector Logic Apps, the following Azure roles apply:

| Role | Description |
| --- | --- |
| **Owner** or **User Access Administrator** | Grant Microsoft Sentinel access to playbooks in the resource group. Elevate only while assigning these service permissions. |
| **Microsoft Sentinel Contributor** | Attach a playbook to an automation rule |
| **Microsoft Sentinel Responder** | Access an incident in order to run a playbook manually. To actually run the playbook, you also need the following roles: - **Microsoft Sentinel Playbook Operator**, to run a playbook manually - **Microsoft Sentinel Automation Contributor** role, to allow automation rules to run playbooks. |

For more information about required roles and permissions, see [playbook prerequisites](automate-responses-with-playbooks#prerequisites).

#### Extra permissions required to run Logic Apps

For Microsoft Sentinel connector Logic Apps, the following service permissions are required to run playbooks on a case or an incident:

Microsoft Sentinel uses a service account to run playbooks on incidents, to add security and enable the automation rules API to support CI/CD use cases. This service account is used for incident-triggered playbooks, or when you run a playbook manually on a specific incident.

In addition to your own roles and permissions, this Microsoft Sentinel service account must have its own set of permissions on the resource group where the playbook resides, in the form of the **Microsoft Sentinel Automation Contributor** role. Once Microsoft Sentinel has this role, it can run any playbook in the relevant resource group, manually or from an automation rule.

To grant Microsoft Sentinel with the required permissions, you must have an **Owner** or **User access administrator** role. To run the playbooks, you'll also need the **Logic App Contributor** role on the resource group that contains the playbooks you want to run.

For Microsoft Defender SOC Logic Apps on cases or alerts, grant service permissions from the **Run playbook** panel or from **Settings**. See Grant permissions for Microsoft Defender SOC Logic Apps.

#### Configure playbook permissions for cases or incidents in a multitenant deployment

In a multitenant deployment, if the Microsoft Sentinel connector playbook you want to run on a case or incident is in a different tenant, grant the Microsoft Sentinel service account permission to run it in the playbook's tenant.

##### Microsoft Defender portal

In the Defender portal, configure permissions in the playbook's tenant:

1. From the navigation bar, select **Settings** &gt; **Sentinel**.
2. Select the workspace, and then select **Playbook permissions**.
3. Select **Configure permissions** to open the **Manage permissions** panel.
4. Select the resource groups containing the playbooks you want to run, and select **Apply**.

##### Azure portal

In the Azure portal, configure permissions in the playbook's tenant:

1. From the Microsoft Sentinel navigation menu in the playbooks' tenant, select **Settings**.
2. In the **Settings** page, select the **Settings** tab, then the **Playbook permissions** expander.
3. Select the **Configure permissions** button to open the **Manage permissions** panel.
4. Mark the check boxes of the resource groups containing the playbooks you want to run, and select **Apply**. For example:

    ![Screenshot that shows the actions section with run playbook selected.](../media/run-playbooks/manage-permissions.png)

For setup and execution roles, see Required Azure roles to run playbooks.

If, in a managed security service provider (MSSP) scenario, you want to [run a playbook in a customer tenant](../automate-incident-handling-with-automation-rules#permissions-in-a-multitenant-architecture) from an automation rule created while signed into the service provider tenant, you must grant Microsoft Sentinel permission to run the playbook in both tenants:

- **In the customer tenant**, follow the standard instructions for the multitenant deployment.
- **In the service provider tenant**, add the Azure Security Insights app in your Azure Lighthouse onboarding template as follows:

    1. From the Azure portal go to Microsoft Entra ID and select **Enterprise applications**.
    2. Select **Application type** and filter on **Microsoft Applications**.
    3. In the search box, enter **Azure Security Insights**.
    4. Copy the **Object ID** field. You need to add this extra authorization to your existing Azure Lighthouse delegation.

The **Microsoft Sentinel Automation Contributor** role has a fixed GUID of `f4c81013-99ee-4d62-a7ee-b3f1f648599a`. To assign the Azure Security Insights app this role in your Azure Lighthouse delegation, add the following authorization entry to your parameters template. Replace the `principalId` value with the Object ID you copied in the previous step:

```json
{
"principalId": "<Enter the Azure Security Insights app Object ID>", 
"roleDefinitionId": "f4c81013-99ee-4d62-a7ee-b3f1f648599a",
"principalIdDisplayName": "Microsoft Sentinel Automation Contributors" 
}
```

## Run a playbook manually, on demand

Note

Manual execution of Microsoft Defender SOC Logic Apps and generated playbooks on alerts and cases is in public preview. Existing Microsoft Sentinel connector playbook support isn't part of this preview. The case procedures apply to cases of type **Incident**.

Manually run playbooks on cases, incidents, alerts, or entities. In the Defender portal, use **Run playbook** to start a compatible playbook and the **Runs** tab to review execution results. No automation rule is required.

The Defender portal supports three playbook families:

- **Microsoft Defender SOC Logic Apps:** Azure Logic Apps using the **Microsoft Defender SOC alert** or **Microsoft Defender SOC case** trigger.
- **Generated playbooks:** Code-based workflows created with Playbook Generator, using alert or case input. Generated playbooks aren't Logic Apps.
- **Microsoft Sentinel connector Logic Apps:** Existing playbooks remain supported on cases and incidents as the incident experience transitions to cases.

Microsoft Defender SOC Logic Apps and generated playbooks don't require a Microsoft Sentinel or Integrated Security Operations Center (ISOC) workspace for manual runs. Execution requires the appropriate entitlement and compatible input. Logic App hosting charges still apply, and third-party data ingested through Log Analytics still requires a workspace.

For generated playbooks, configure the integration profiles and API permissions required by their actions; see [Configure integration profiles](/en-us/defender-xdr/siem-defender-automation-integrations).

### Run a playbook manually on a case

Cases support all three types of playbooks. Run a compatible playbook from the case you're investigating in the Defender portal:

1. Go to **Cases**, select **Incident**, and open the case.
2. Open the three-dot menu. Under **Actions**, select **Run playbook**.

    ![Screenshot of Run playbook under Actions in the case menu.](../media/run-playbooks/defender-case-entry.png)
3. In the **Playbooks** tab, select a playbook. The list is filtered to playbooks compatible with the case.

    Microsoft Defender SOC Logic Apps in this list use the **Microsoft Defender SOC case** trigger, not the alert trigger.

    [![Screenshot of the case playbook picker showing compatible playbooks, their families, and availability states.](../media/run-playbooks/defender-case-playbooks.png)](../media/run-playbooks/defender-case-playbooks.png#lightbox)
4. If the playbook is inactive, activate it on the **Automation** page under the **Playbooks** tab. For a Microsoft Defender SOC Logic App with **Missing permissions**, follow Grant permissions for SOC Logic Apps.

    For existing Microsoft Sentinel connector playbooks, see Extra permissions required to run Logic Apps.
5. Select **Run playbook** for the playbook.
6. Review the execution result.

An alert-input playbook isn't automatically compatible with case input. Running a playbook on a case doesn't imply iteration over the case's child alerts.

### Run a playbook manually on an incident

The incident experience is being upgraded to the full case experience, retaining all incident features and adding new capabilities. Use the case experience to continue running the same Microsoft Sentinel connector playbooks.

The procedure for manually running a playbook on an incident differs, depending on whether you're working in the Azure portal or in the Defender portal. Select the relevant tab for your environment:

# [Run a playbook on an incident in the Microsoft Defender portal](#tab/microsoft-defender)
In the Microsoft Defender portal, follow these steps to run a playbook on an incident:

1. In the **Incidents** page, select an incident.
2. From the incident details pane that appears on the side, select **Run Playbook**.
3. The **Run playbook on incident** panel opens on the side, with all related playbooks for the selected incident. In the **Action** column, select **Run playbook** for the playbook you want to run immediately.

The **Actions** column might also show one of the following statuses:

| Status | Description and action required |
| --- | --- |
| **Missing permissions** | You must have the **Microsoft Sentinel Playbook Operator** role on any resource group containing playbooks you want to run. If you're missing permissions, we recommend you contact an admin to grant you with the relevant permissions. For more information, see [Microsoft Sentinel playbook prerequisites](automate-responses-with-playbooks#prerequisites). |
| **Grant permission** | Microsoft Sentinel is missing the **Microsoft Sentinel Automation Contributor** role, which is required to run playbooks on incidents. In such cases, select **Grant permission** to open the **Manage permissions** pane. The **Manage permissions** pane is filtered by default to the selected playbook's resource group. Select the resource group and then select **Apply** to grant the required permissions. You must be an **Owner** or a **User Access Administrator** on the resource group to which you want to grant Microsoft Sentinel permissions. If you're missing permissions, the resource group is greyed out and you can't select it. In such cases, we recommend you contact an admin to grant you with the relevant permissions. For more information, see Extra permissions required to run Logic Apps. |

# [Run a playbook on an incident in the Azure portal](#tab/azure)
In the Azure portal, use the following steps to run a playbook on an incident:

1. In the **Incidents** page, select an incident.
2. From the incident details pane that appears on the side, select **Actions &gt; Run playbook**.

    Selecting the three dots at the end of the incident's line on the grid or right-clicking the incident displays the same list as the **Action** button.
3. The **Run playbook on incident** panel opens on the side. You see a list of all playbooks configured with the **Microsoft Sentinel Incident** Logic Apps trigger that you have access to.

    If you don't see the playbook you want to run in the list, it means Microsoft Sentinel doesn't have permissions to run playbooks in that resource group.

    To grant those permissions, select **Settings** &gt; **Settings** &gt; **Playbook permissions** &gt; **Configure permissions**. In the **Manage permissions** panel that opens up, mark the check boxes of the resource groups containing the playbooks you want to run, and select **Apply**.

    For information, see Extra permissions required to run Logic Apps.
4. Select **Run** on the line of a specific playbook to run it immediately.

    You must have the **Microsoft Sentinel playbook operator** role on any resource group containing playbooks you want to run. If you're unable to run the playbook due to missing permissions, we recommend you contact an admin to grant you with the relevant permissions. For more information, see [Microsoft Sentinel playbook prerequisites](automate-responses-with-playbooks#prerequisites).

---

View the run history for playbooks on an incident by selecting the **Runs** tab on the **Run playbook on incident** panel. It might take a few seconds for any just-completed run to appear in the list. Selecting a specific run opens the full run log in Logic Apps.

### Run a playbook manually on an alert

Select the portal where you want to run the playbook:

# [Microsoft Defender portal](#tab/alert-defender)
Run Microsoft Defender SOC Logic Apps or generated playbooks on alerts in the Defender portal. The **Microsoft Defender SOC alert** trigger supports both Microsoft Defender and Microsoft Sentinel alerts.

In the Defender portal, perform the following steps:

1. On the alert page, in the right side panel, select **Run playbook**.
2. In the **Playbooks** tab, select a playbook. The list shows only alert-trigger Microsoft Defender SOC Logic Apps and generated playbooks with **Alert** input.

    ![Screenshot of SOC Logic Apps in the alert picker with active, inactive, and missing-permissions states.](../media/run-playbooks/defender-alert-run-playbook-list-statuses.png)
3. If the playbook is inactive, activate it on the **Automation** page under the **Playbooks** tab. For a Microsoft Defender SOC Logic App with **Missing permissions**, follow Grant permissions for SOC Logic Apps.
4. Select **Run playbook** on the line of a specific playbook to run it.
5. Review the execution result. A request-accepted acknowledgment doesn't establish that execution completed successfully.

# [Azure portal](#tab/alert-azure)
The following legacy procedures apply only to the Azure portal and run Microsoft Sentinel connector playbooks on alerts. For the Defender portal, select the **Microsoft Defender portal** tab.

##### Run a playbook from the incident details page (legacy, Azure portal)

To run a playbook on an alert from the incident details page, perform the following steps:

1. In the **Incidents** page, select an incident, and then select **View full details** to open the incident details page.
2. In the incident details page, in the **Incident timeline** widget, select the alert you want to run the playbook on. Select the three dots at the end of the alert's line and select **Run playbook** from the pop-up menu.

    ![Screenshot of running a playbook on an alert on-demand.](../media/investigate-incidents/remove-alert.png)
3. The **Alert playbooks** pane opens. You see a list of all playbooks configured with the **Microsoft Sentinel Alert** Logic Apps trigger that you have access to.
4. Select **Run** on the line of a specific playbook to run it immediately.

##### Run a playbook from the investigation graph (legacy, Azure portal)

To run a playbook on an alert from the investigation graph, follow these steps:

1. In the **Incidents** page, select an incident, and then select **View full details** to open the incident details page.
2. In the incident details page, select the **Alerts** tab, select the alert you want to run the playbook on, and select the **View playbooks** link at the end of the line of that alert.
3. The **Alert playbooks** pane opens. You see a list of all playbooks configured with the **Microsoft Sentinel Alert** Logic Apps trigger that you have access to.
4. Select **Run** on the line of a specific playbook to run it immediately.

You can see the run history for playbooks on an alert by selecting the **Runs** tab on the **Alert playbooks** pane. It might take a few seconds for any just-completed run to appear in the list. Selecting a specific run opens the full run log in Logic Apps.

---

### Review Defender playbook execution results

Use the **Runs** tab in the **Run playbook** panel to review execution results in one place. A request-accepted acknowledgment doesn't establish that execution completed successfully.

To review a run:

1. In the alert or case's **Run playbook** panel, select **Runs** and find the execution. Check whether it is running, completed, or failed.
2. For a Logic App execution, select **View run** to open the Azure Logic App execution details. Review individual actions and errors to determine the downstream outcome.
3. Review execution results in the related case or incident:

    - For a case, open **Artifacts** &gt; **Activities**.
    - For an incident, select **Activity**.

    For an alert run, use the parent case or incident, not an Alert-local Activity tab. Generated playbooks aren't Logic Apps; review their results in the related case or incident activity, not Azure Logic App execution details.

### Grant permissions for Microsoft Defender SOC Logic Apps

Use this flow when a Microsoft Defender SOC Logic App shows **Missing permissions** in an alert or case's **Run playbook** panel. A user who can run a playbook might need an authorized administrator or author to resolve missing permissions.

If the **Missing permissions** status is shown, select it, browse resource groups, select the relevant resource group, and grant Microsoft Sentinel permissions to run playbooks in that resource group. You can also update permissions from **Settings** &gt; **Sentinel** (select the workspace) &gt; **Playbook permissions** (select **Configure permissions**).

![Screenshot of the Logic Apps permission dialog for selecting resource groups and granting service permissions.](../media/run-playbooks/defender-alert-grant-playbook-permissions.png)

This Logic App permission flow doesn't configure generated-playbook integrations. For generated playbooks, see [Configure integration profiles](/en-us/defender-xdr/siem-defender-automation-integrations).

### Run a playbook manually on an entity

**Legacy Azure portal procedures.** The following procedures describe Microsoft Sentinel entity-trigger playbooks in the Azure portal, not entry points on the Defender case page. "New" and "legacy" incident details pages in these tabs refer to versions of the Azure portal experience.

In the Azure portal, select an entity in one of the following ways, depending on your originating context:

# [Run a playbook on an entity from the new incident details page](#tab/incident-details-new)
**If you're in an incident's details page (new version):**

In the **Entities** widget in the **Overview** tab, locate your entity, and do one of the following:

- Don't select the entity. Instead, select the three dots to the right of the entity, and then select **Run playbook**. Locate the playbook you want to run, and select **Run** in that playbook's row.
- Select the entity to open the **Entities tab** of the incident details page. Locate your entity on the list, and select the three dots to the right. Locate the playbook you want to run, and select **Run** in that playbook's row.
- Select an entity and drill down to the entity details page. Then, select the **Run playbook** button in the left-hand panel. Locate the playbook you want to run, and select **Run** in that playbook's row.

# [Run a playbook on an entity from the legacy incident details page](#tab/incident-details-legacy)
**If you're in an incident's details page (legacy version):**

1. Select the incident's **Entities** tab and locate your entity on the list.
2. Do one of the following:

    - Select the **Run playbook** link at the end of the entity line in the list.
    - Select the entity to drill down to the entity details page and select the **Run playbook** button in the left-hand panel.
3. Locate the playbook you want to run, and select **Run** in that playbook's row.

# [Run a playbook on an entity from the investigation graph](#tab/investigation-graph)
**If you're in the Investigation graph:**

1. Select an entity in the graph and then select the **Run playbook** button in the entity side panel.

    For some entity types, you might have to select the **Entity actions** button and from the resulting menu select **Run playbook**.
2. Locate the playbook you want to run, and select **Run** in that playbook's row.

# [Run a playbook on an entity from proactive hunting](#tab/hunting)
**If you're proactively hunting for threats:**

1. From the **Entity behavior** screen, select an entity from the lists on the page, or search for and select another entity.
2. In the [entity page](../entity-pages), select the **Run playbook** button in the left-hand panel.
3. Locate the playbook you want to run, and select **Run** in that playbook's row.

---

Regardless of the context you came from, the last step in this procedure is from the **Run playbook on *&lt;entity type&gt;*** panel. This panel shows list of all playbooks that you have access to that were configured with the **Microsoft Sentinel Entity** Logic Apps trigger for the selected entity type.

On the **Run playbook on \*&lt;entity type&gt;** pane, select the **Runs** tab to see the playbook run history for a given entity. It might take a few seconds for any just-completed run to appear in the list. Selecting a specific run opens the full run log in Logic Apps.

### Optional: Create a playbook from an alert or case

If you need a new playbook while investigating an alert or case, you can start creating one from the **Run playbook** panel. This is an optional authoring shortcut, separate from running playbooks and reviewing results.

To start creating a playbook:

1. Open **Run playbook** from the alert or case.
2. Select **Create**, and choose the playbook family:

    | Option | Authoring guidance |
    | --- | --- |
    | **Create generated playbook** | Create a code-based workflow with the required alert or case input. See [Generate a playbook](/en-us/defender-xdr/siem-defender-generate-playbooks#generate-a-playbook). |
    | **Create Logic App** | Create a workflow using the [Microsoft Defender SOC connector](/en-us/connectors/defendersoc/). |

    The available Logic App options depend on the investigation:

    | Investigation | Logic App options |
    | --- | --- |
    | Alert | **Playbook with alert trigger**, **Blank playbook**. |
    | Case | **Playbook with case trigger**, **Blank playbook**. |
3. Follow the authoring guidance for the chosen family. Review and test the workflow before use. Saving a generated playbook leaves it disabled; [activate the generated playbook](/en-us/defender-xdr/siem-defender-generate-playbooks#activate-a-generated-playbook) before running it.

The contextual menu doesn't offer creation of existing Microsoft Sentinel connector playbooks. For authoring permissions, see Prerequisites.

## Automate responses to cases, incidents, and alerts

Use an automation rule to run a playbook automatically when a case, incident, or alert matches the rule's trigger and conditions. For setup instructions, see:

- [Create Microsoft Sentinel automation rules](../create-manage-use-automation-rules#create-your-automation-rule), including the [Run playbook action](../create-manage-use-automation-rules#add-actions).
- [Run a generated playbook when a case is created or updated](/en-us/defender-xdr/siem-defender-generate-playbooks#run-a-generated-playbook-when-an-incident-case-is-created-or-updated).