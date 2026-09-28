---
layout: Conceptual
title: Automate and run Microsoft Sentinel playbooks | Microsoft Learn
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
description: Learn how to automate incident response with Microsoft Sentinel playbooks, or run playbooks manually to remediate immediate security threats.
ms.author: monaberdugo
author: mberdugo
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
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
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
platformId: 5b1e0c92-618f-a617-919a-2dea7d0396cc
---

# Automate and run Microsoft Sentinel playbooks | Microsoft Learn

Playbooks are collections of procedures that can be run from Microsoft Sentinel in response to an entire incident, to an individual alert, or to a specific entity. A playbook can help automate and orchestrate your response and can be set to run automatically when specific alerts are generated or when incidents are created or updated, by being attached to an automation rule. It can also be run manually on-demand on specific incidents, alerts, or entities.

This article describes how to attach playbooks to analytics rules or automation rules, or run playbooks manually on specific incidents, alerts, or entities. Before you begin, make sure you meet the prerequisites, including required Azure roles and playbook permissions.

Note

Playbooks in Microsoft Sentinel are based on workflows built in [Azure Logic Apps](/en-us/azure/logic-apps/logic-apps-overview), which means that you get all the power, customizability, and built-in templates of Logic Apps. Additional charges might apply. Visit the [Azure Logic Apps](https://azure.microsoft.com/pricing/details/logic-apps/) pricing page for more details.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](../overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](../move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Prerequisites

Before you start, make sure that you have a playbook available to automate or run, with a trigger, conditions, and actions defined. For more information, see [Create and manage Microsoft Sentinel playbooks](create-playbooks).

### Required Azure roles to run playbooks

To run playbooks, you need the following Azure roles:

| Role | Description |
| --- | --- |
| **Owner** | Lets you grant access to playbooks in the resource group. |
| **Microsoft Sentinel Contributor** | Attach a playbook to an analytics rule or automation rule |
| **Microsoft Sentinel Responder** | Access an incident in order to run a playbook manually. To actually run the playbook, you also need the following roles: - **Microsoft Sentinel Playbook Operator**, to run a playbook manually - **Microsoft Sentinel Automation Contributor** role, to allow automation rules to run playbooks. |

For more information about required roles and permissions, see [playbook prerequisites](automate-responses-with-playbooks#prerequisites).

### Extra permissions required to run playbooks on incidents

Microsoft Sentinel uses a service account to run playbooks on incidents, to add security and enable the automation rules API to support CI/CD use cases. This service account is used for incident-triggered playbooks, or when you run a playbook manually on a specific incident.

In addition to your own roles and permissions, this Microsoft Sentinel service account must have its own set of permissions on the resource group where the playbook resides, in the form of the **Microsoft Sentinel Automation Contributor** role. Once Microsoft Sentinel has this role, it can run any playbook in the relevant resource group, manually or from an automation rule.

To grant Microsoft Sentinel with the required permissions, you must have an **Owner** or **User access administrator** role. To run the playbooks, you'll also need the **Logic App Contributor** role on the resource group that contains the playbooks you want to run.

### Configure playbook permissions for incidents in a multitenant deployment

In a multitenant deployment, if the playbook you want to run is in a different tenant, you must grant the Microsoft Sentinel service account with permission to run the playbook in the playbook's tenant.

1. From the Microsoft Sentinel navigation menu in the playbooks' tenant, select **Settings**.
2. In the **Settings** page, select the **Settings** tab, then the **Playbook permissions** expander.
3. Select the **Configure permissions** button to open the **Manage permissions** panel.
4. Mark the check boxes of the resource groups containing the playbooks you want to run, and select **Apply**. For example:

    ![Screenshot that shows the actions section with run playbook selected.](../media/run-playbooks/manage-permissions.png)

You yourself must have **Owner** permissions on any resource group to which you want to grant Microsoft Sentinel permissions, and you must have the **Microsoft Sentinel Playbook Operator** role on any resource group containing playbooks you want to run.

If, in an MSSP scenario, you want to [run a playbook in a customer tenant](../automate-incident-handling-with-automation-rules#permissions-in-a-multitenant-architecture) from an automation rule created while signed into the service provider tenant, you must grant Microsoft Sentinel permission to run the playbook in both tenants:

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

## Automate responses to incidents and alerts

To respond automatically to entire incidents or individual alerts with a playbook, create an automation rule that runs when the incident is created or updated, or when the alert is generated. This automation rule includes a step that calls the playbook you want to use.

**To create an automation rule**:

1. From the **Automation** page in the Microsoft Sentinel navigation menu, select **Create** from the top menu and then **Automation rule**. For example:

    ![Screenshot showing how to add a new automation rule.](../media/run-playbooks/add-new-rule.png)
2. The **Create new automation rule** panel opens. Enter a name for your rule. Your options differ depending on whether your workspace is onboarded to the Microsoft Defender portal. For example:

# [Onboarded workspaces](#tab/after-onboarding)
![Screenshot showing the automation rule creation wizard.](../media/run-playbooks/create-automation-rule-onboarded.png)

# [Workspaces that aren't onboarded](#tab/before-onboarding)
![Screenshot showing the automation rule creation wizard.](../media/run-playbooks/create-automation-rule.png)

---
3. **Trigger:** Select the appropriate trigger according to the circumstance for which you're creating the automation rule — **When incident is created**, **When incident is updated**, or **When alert is created**.
4. **Conditions:**

    1. If your workspace isn't yet onboarded to the Defender portal, incidents can have two possible sources:

        - Incidents can be created inside Microsoft Sentinel
        - Incidents can be [imported from — and synchronized with — Microsoft Defender XDR](../microsoft-365-defender-sentinel-integration).

        If you selected one of the incident triggers and you want the automation rule to take effect only on incidents sourced in Microsoft Sentinel, or alternatively in Microsoft Defender XDR, specify the source in the **If Incident provider equals** condition.

        This condition is displayed only if an incident trigger is selected and your workspace isn't onboarded to the Defender portal.
    2. For all trigger types, if you want the automation rule to take effect only on certain analytics rules, specify which ones by modifying the **If Analytics rule name contains** condition.
    3. Add any other conditions you want to determine whether this automation rule runs. Select **+ Add** and select [conditions or condition groups](../add-advanced-conditions-to-automation-rules) from the drop-down list. The list of conditions is populated by alert detail and entity identifier fields.
5. **Actions:**

    1. Since you're using this automation rule to run a playbook, select the **Run playbook** action from the drop-down list. You'll then be prompted to select from a second drop-down list that shows the available playbooks. An automation rule can run only those playbooks that start with the same trigger (incident or alert) as the trigger defined in the rule, so only those playbooks appear in the list.

        If a playbook appears grayed out in the drop-down list, it means that Microsoft Sentinel doesn't have permission to that playbook's resource group. Select the **Manage playbook permissions** link to assign permissions.

        In the **Manage permissions** panel that opens up, mark the check boxes of the resource groups containing the playbooks you want to run, and select **Apply**. For example:

        ![Screenshot that shows the actions section with run playbook selected.](../media/run-playbooks/manage-permissions.png)

        You yourself must have **Owner** permissions on any resource group to which you want to grant Microsoft Sentinel permissions, and you must have the **Microsoft Sentinel Playbook Operator** role on any resource group containing playbooks you want to run.

        For more information, see Extra permissions required to run playbooks on incidents.
    2. Add any other actions you want for this rule. You can change the order of execution of actions by selecting the up or down arrows to the right of any action.
6. Set an expiration date for your automation rule if you want it to have one.
7. Enter a number under **Order** to determine where in the sequence of automation rules this rule runs.
8. Select **Apply** to complete your automation.

For more information, see [Create and manage Microsoft Sentinel playbooks](create-playbooks).

### Respond to alerts—legacy method

Another way to run playbooks automatically in response to **alerts** is to call them from an **analytics rule**. When the rule generates an alert, the playbook runs.

**Calling playbooks from analytics rules will be deprecated as of March 2026.**

Beginning **June 2023**, you can no longer add playbooks directly from an analytics rule. However, you can still see the existing playbooks called from analytics rules, and these playbooks will still run until March 2026. We strongly encourage you to [create automation rules to call these playbooks instead](migrate-playbooks-to-automation-rules) before then.

## Run a playbook manually, on demand

You can also manually run a playbook on demand, whether in response to alerts, incidents, or entities. This can be useful in situations where you want more human input into and control over orchestration and response processes.

### Run a playbook manually on an alert

Running a playbook manually on an alert isn't supported in the Defender portal.

In the Azure portal, select one of the following tabs as needed for your environment:

# [Run a playbook from the incident details page](#tab/incidents)
To run a playbook on an alert from the incident details page, perform the following steps:

1. In the **Incidents** page, select an incident, and then select **View full details** to open the incident details page.
2. In the incident details page, in the **Incident timeline** widget, select the alert you want to run the playbook on. Select the three dots at the end of the alert's line and select **Run playbook** from the pop-up menu.

    ![Screenshot of running a playbook on an alert on-demand.](../media/investigate-incidents/remove-alert.png)
3. The **Alert playbooks** pane opens. You see a list of all playbooks configured with the **Microsoft Sentinel Alert** Logic Apps trigger that you have access to.
4. Select **Run** on the line of a specific playbook to run it immediately.

# [Run a playbook from the investigation graph](#tab/cases)
To run a playbook on an alert from the investigation graph, follow these steps:

1. In the **Incidents** page, select an incident, and then select **View full details** to open the incident details page.
2. In the incident details page, select the **Alerts** tab, select the alert you want to run the playbook on, and select the **View playbooks** link at the end of the line of that alert.
3. The **Alert playbooks** pane opens. You see a list of all playbooks configured with the **Microsoft Sentinel Alert** Logic Apps trigger that you have access to.
4. Select **Run** on the line of a specific playbook to run it immediately.

---

You can see the run history for playbooks on an alert by selecting the **Runs** tab on the **Alert playbooks** pane. It might take a few seconds for any just-completed run to appear in the list. Selecting a specific run opens the full run log in Logic Apps.

### Run a playbook manually on an incident

The procedure for manually running a playbook on an incident differs, depending on whether you're working in the Azure portal or in the Defender portal. Select the relevant tab for your environment:

# [Run a playbook on an incident in the Azure portal](#tab/azure)
In the Azure portal, use the following steps to run a playbook on an incident:

1. In the **Incidents** page, select an incident.
2. From the incident details pane that appears on the side, select **Actions &gt; Run playbook**.

    Selecting the three dots at the end of the incident's line on the grid or right-clicking the incident displays the same list as the **Action** button.
3. The **Run playbook on incident** panel opens on the side. You see a list of all playbooks configured with the **Microsoft Sentinel Incident** Logic Apps trigger that you have access to.

    If you don't see the playbook you want to run in the list, it means Microsoft Sentinel doesn't have permissions to run playbooks in that resource group.

    To grant those permissions, select **Settings** &gt; **Settings** &gt; **Playbook permissions** &gt; **Configure permissions**. In the **Manage permissions** panel that opens up, mark the check boxes of the resource groups containing the playbooks you want to run, and select **Apply**.

    For information, see Extra permissions required to run playbooks on incidents.
4. Select **Run** on the line of a specific playbook to run it immediately.

    You must have the **Microsoft Sentinel playbook operator** role on any resource group containing playbooks you want to run. If you're unable to run the playbook due to missing permissions, we recommend you contact an admin to grant you with the relevant permissions. For more information, see [Microsoft Sentinel playbook prerequisites](automate-responses-with-playbooks#prerequisites).

# [Run a playbook on an incident in the Microsoft Defender portal](#tab/microsoft-defender)
In the Microsoft Defender portal, follow these steps to run a playbook on an incident:

1. In the **Incidents** page, select an incident.
2. From the incident details pane that appears on the side, select **Run Playbook**.
3. The **Run playbook on incident** panel opens on the side, with all related playbooks for the selected incident. In the **Action** column, select **Run playbook** for the playbook you want to run immediately.

The **Actions** column might also show one of the following statuses:

| Status | Description and action required |
| --- | --- |
| **Missing permissions** | You must have the **Microsoft Sentinel Playbook Operator** role on any resource group containing playbooks you want to run. If you're missing permissions, we recommend you contact an admin to grant you with the relevant permissions. For more information, see [Microsoft Sentinel playbook prerequisites](automate-responses-with-playbooks#prerequisites). |
| **Grant permission** | Microsoft Sentinel is missing the **Microsoft Sentinel Automation Contributor** role, which is required to run playbooks on incidents. In such cases, select **Grant permission** to open the **Manage permissions** pane. The **Manage permissions** pane is filtered by default to the selected playbook's resource group. Select the resource group and then select **Apply** to grant the required permissions. You must be an **Owner** or a **User access administrator** on the resource group to which you want to grant Microsoft Sentinel permissions. If you're missing permissions, the resource group is greyed out and you can't select it. In such cases, we recommend you contact an admin to grant you with the relevant permissions. For more information, see Extra permissions required to run playbooks on incidents. |

---

View the run history for playbooks on an incident by selecting the **Runs** tab on the **Run playbook on incident** panel. It might take a few seconds for any just-completed run to appear in the list. Selecting a specific run opens the full run log in Logic Apps.

### Run a playbook manually on an entity

Select an entity in one of the following ways, depending on your originating context:

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