---
layout: Conceptual
title: Create and use Microsoft Sentinel automation rules to manage response | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/create-manage-use-automation-rules
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
description: Create automation rules in Microsoft Sentinel to trigger actions on incidents based on defined conditions, and configure triggers, conditions, and response actions.
ms.topic: how-to
ms.author: monaberdugo
author: mberdugo
ms.reviewer: sshuster
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: usx-security
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: ea6edf1b-1679-5f72-8b64-2fd1c2a67427
document_version_independent_id: 84843641-de19-0fe3-f93a-88867dea330a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/create-manage-use-automation-rules.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/create-manage-use-automation-rules
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/create-manage-use-automation-rules.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 6b69cda4-8fed-f64c-d413-c910f1b3de65
---

# Create and use Microsoft Sentinel automation rules to manage response | Microsoft Learn

This article explains how to create and use automation rules in Microsoft Sentinel to manage and orchestrate threat response, in order to maximize your SOC's efficiency and effectiveness.

In this article you'll learn how to define the triggers and conditions that determine when your automation rule runs, the various actions that you can have the rule perform, and the remaining features and functionalities.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Design your automation rule

Before you create your automation rule, we recommend that you determine its scope and design, including the trigger, conditions, and actions that make up your rule.

### Determine the scope

The first step in designing and defining your automation rule is figuring out which incidents or alerts you want it to apply to. Deciding which incidents or alerts the rule applies to directly impacts how you create the rule.

You also want to determine your use case. What are you trying to accomplish with this automation? Consider the following options:

- Create tasks for your analysts to follow in triaging, investigating, and remediating incidents.
- Suppress noisy incidents. (Alternatively, use other methods to [handle false positives in Microsoft Sentinel](false-positives).)
- Triage new incidents by changing their status from New to Active and assigning an owner.
- Tag incidents to classify them.
- Escalate an incident by assigning a new owner.
- Close resolved incidents, specifying a reason and adding comments.
- Analyze the incident's contents (alerts, entities, and other properties) and take further action by calling a playbook.
- Handle or respond to an alert without an associated incident.

### Determine the trigger

Do you want this automation rule to be activated when new incidents or alerts are created? Or anytime an incident gets updated?

Automation rules are triggered **when an incident is created or updated** or **when an alert is created**. Recall that incidents include alerts, and that both alerts and incidents can be created by analytics rules, of which there are several types, as explained in [Threat detection in Microsoft Sentinel](threat-detection).

The following table shows the different possible scenarios that cause an automation rule to run.

| Trigger type | Events that cause the rule to run |
| --- | --- |
| **When incident is created** | **Microsoft Defender portal:**- A new incident is created in the Microsoft Defender portal.**Microsoft Sentinel not onboarded to the Defender portal:**- A new incident is created by an analytics rule.- An incident is ingested from Microsoft Defender XDR.- A new incident is created manually. |
| **When incident is updated** | - An incident's status is changed (closed/reopened/triaged).- An incident's owner is assigned or changed.- An incident's severity is raised or lowered.- Alerts are added to an incident.- Comments, tags, or tactics are added to an incident. |
| **When alert is created** | - An alert is created by a Microsoft Sentinel **Scheduled** or **NRT** analytics rule. |

Note

**In the Defender portal:** Alert triggers work only on Microsoft Sentinel alerts. To automate responses to alerts across Microsoft Sentinel, Microsoft Defender, and XDR platforms, use the **[Enhanced Alert Trigger](automation/generate-playbook#enhanced-alert-trigger)**.

## Create your automation rule

The following steps apply to most automation rule creation scenarios.

If you're looking to suppress noisy incidents and are working in the Azure portal, try [handling false positives](false-positives#add-exceptions-with-automation-rules-azure-portal-only).

If you want to create an automation rule to apply to a specific analytics rule, see [Set automated responses and create the rule](detect-threats-custom#set-automated-responses-and-create-the-rule).

To create your automation rule:

1. For Microsoft Sentinel in the [Azure portal](https://portal.azure.com), select the **Configuration** &gt; **Automation** page. For Microsoft Sentinel in the [Defender portal](https://security.microsoft.com/), select **Microsoft Sentinel** &gt; **Configuration** &gt; **Automation**.
2. From the **Automation** page in the Microsoft Sentinel navigation menu, select **Create** from the top menu and choose **Automation rule**.

# [Defender portal](#tab/defender-portal)
[![Screenshot of creating a new automation rule in the Automation page.](media/create-manage-use-automation-rules/add-rule-automation-defender.png)](media/create-manage-use-automation-rules/add-rule-automation-defender.png#lightbox)

# [Azure portal](#tab/azure-portal)
[![Screenshot of creating a new automation rule in the Automation page.](media/create-manage-use-automation-rules/add-rule-automation.png)](media/create-manage-use-automation-rules/add-rule-automation.png#lightbox)

---
3. The **Create new automation rule** panel opens. In the **Automation rule name** field, enter a name for your rule.

### Choose your trigger

From the **Trigger** drop-down, select the trigger that matches when you want the automation rule to run—**When incident is created**, **When incident is updated**, or **When alert is created**.

Note

If your workspace is onboarded to the Microsoft Defender portal, the trigger drop-down also includes the **Case created** and **Case updated** triggers from [Simple Flows](automation/create-basic-automation-rules-simple-flows) (preview).

![Screenshot of selecting the incident create or incident update trigger.](media/create-manage-use-automation-rules/select-trigger.png)

### Define conditions

Use the options in the **Conditions** area to define conditions for your automation rule. All conditions are case insensitive.

- Rules you create for when an alert is created support only the **If Analytic rule name** property in your condition. Select whether you want the rule to be inclusive (**Contains**) or exclusive (**Does not contain**), and then select the analytic rule name from the drop-down list.

    Analytic rule name values include only analytics rules, and don't include other types of rules, such as threat intelligence or anomaly rules.
- Rules you create for when an incident is created or updated support a large variety of conditions, depending on your environment. The available condition options depend on whether you've onboarded Microsoft Sentinel to the Defender portal:

# [Onboarded to the Defender portal](#tab/onboarded)
If your workspace is onboarded to the Defender portal, start by selecting one of the following operators, in either the Azure or the Defender portal:

    - **AND**: individual conditions that are evaluated as a group. The rule executes if *all* the conditions of this type are met.

        To work with the **AND** operator, select the **+ Add** expander and choose **Condition (And)** from the drop-down list. The list of conditions is populated by incident property and [entity property](entities-reference) fields.
    - **OR** (also known as *condition groups*): groups of conditions, each of which are evaluated independently. The rule executes if one or more groups of conditions are true. To learn how to work with these complex types of conditions, see [Add advanced conditions to automation rules](add-advanced-conditions-to-automation-rules).

For example:

![Screenshot of automation rule conditions when your workspace is onboarded to the Defender portal.](media/create-manage-use-automation-rules/conditions-onboarded.png)

# [Not onboarded to the Defender portal](#tab/not-onboarded)
If your workspace isn't onboarded to the Defender portal, start by defining the following condition properties:

    - **Incident provider**: Incidents can have two possible sources: they can be created inside Microsoft Sentinel, and they can also be [imported from—and synchronized with—Microsoft Defender XDR](microsoft-365-defender-sentinel-integration).

        If you selected one of the incident triggers and you want the automation rule to take effect only on incidents created in Microsoft Sentinel, or alternatively, only on those imported from Microsoft Defender XDR, specify the source in the **If Incident provider equals** condition. (This condition is displayed only if an incident trigger is selected.)
    - **Analytic rule name**: For all trigger types, if you want the automation rule to take effect only on certain analytics rules, specify which ones by modifying the **If Analytics rule name contains** condition. (This condition isn't displayed if Microsoft XDR is selected as the incident provider.)

Then, continue by selecting one of the following operators:

    - **AND**: individual conditions that are evaluated as a group. The rule executes if *all* the conditions of this type are met.

        To work with the **AND** operator, select the **+ Add** expander and choose **Condition (And)** from the drop-down list. The list of conditions is populated by incident property and [entity property](entities-reference) fields.
    - **OR** (also known as *condition groups*): groups of conditions, each of which are evaluated independently. The rule executes if one or more groups of conditions are true. To learn how to work with these complex types of conditions, see [Add advanced conditions to automation rules](add-advanced-conditions-to-automation-rules).

For example:

![Screenshot of automation rule conditions when the workspace isn't onboarded to the Defender portal.](media/create-manage-use-automation-rules/conditions-not-onboarded.png)

---

    If you selected **When an incident is updated** as the trigger, start by defining your conditions, and then adding extra operators and values as needed.

To define your conditions:

1. Select a property from the first drop-down box on the left. You can begin typing any part of a property name in the search box to dynamically filter the list, so you can find what you're looking for quickly.

    ![Screenshot of typing in a search box to filter the list of choices.](media/create-manage-use-automation-rules/filter-list.png)
2. Select an operator from the next drop-down box to the right. ![Screenshot of selecting a condition operator for automation rules.](media/create-manage-use-automation-rules/select-operator.png)

    The list of operators you can choose from varies according to the selected trigger and property. When working in the Defender portal, we recommend that you use the **Analytic rule name** condition instead of an incident title.

#### Conditions available with the create trigger

    | Property | Operator set |
    | --- | --- |
    | - Title- Description- All listed entity properties (see [supported entity properties](automation-rule-reference)) | - Equals/Does not equal- Contains/Does not contain- Starts with/Does not start with- Ends with/Does not end with |
    | - Tag (See [individual vs. collection](automate-incident-handling-with-automation-rules#tag-property-individual-vs-collection)) | Any individual tag:- Equals/Does not equal- Contains/Does not contain- Starts with/Does not start with- Ends with/Does not end withCollection of all tags:- Contains/Does not contain |
    | - Severity- Status- Custom details key | - Equals/Does not equal |
    | - Tactics- Alert product names- Custom details value- Analytic rule name | - Contains/Does not contain |

#### Conditions available with the update trigger

    | Property | Operator set |
    | --- | --- |
    | - Title- Description- All listed entity properties (see [supported entity properties](automation-rule-reference)) | - Equals/Does not equal- Contains/Does not contain- Starts with/Does not start with- Ends with/Does not end with |
    | - Tag (See [individual vs. collection](automate-incident-handling-with-automation-rules#tag-property-individual-vs-collection)) | Any individual tag:- Equals/Does not equal- Contains/Does not contain- Starts with/Does not start with- Ends with/Does not end withCollection of all tags:- Contains/Does not contain |
    | - Tag (in addition to above)- Alerts- Comments | - Added |
    | - Severity- Status | - Equals/Does not equal- Changed- Changed from- Changed to |
    | - Owner | - Changed. If an incident's owner is updated via API, you must include the [*userPrincipalName* or *ObjectID*](/en-us/rest/api/securityinsights/automation-rules/get#incidentownerinfo) for the change to be detected by automation rules. |
    | - Updated by- Custom details key | - Equals/Does not equal |
    | - Tactics | - Contains/Does not contain- Added |
    | - Alert product names- Custom details value- Analytic rule name | - Contains/Does not contain |

#### Conditions available with the alert trigger

    The only condition that can be evaluated by rules based on the alert creation trigger is which Microsoft Sentinel analytics rule created the alert.

    Automation rules that are based on the alert trigger only run on alerts created by Microsoft Sentinel.
3. Enter a value in the field on the right. Depending on the property you chose, this might be either a text box or a drop-down in which you select from a closed list of values. You might also be able to add several values by selecting the dice icon to the right of the text box.

    ![Screenshot of adding values to your condition in automation rules.](media/create-manage-use-automation-rules/add-values-to-condition.png)

For information about setting complex **Or** conditions with different fields, see [Add advanced conditions to automation rules](add-advanced-conditions-to-automation-rules).

#### Conditions based on tags

You can create two kinds of conditions based on tags:

- Conditions with **Any individual tag** operators evaluate the specified value against every tag in the collection. The evaluation is *true* when *at least one tag* satisfies the condition.
- Conditions with **Collection of all tags** operators evaluate the specified value against the collection of tags as a single unit. The evaluation is *true* only if *the collection as a whole* satisfies the condition.

To add one of these conditions based on an incident's tags, take the following steps:

1. Create a new automation rule as described above.
2. Add a condition or a condition group.
3. Select **Tag** from the properties drop-down list.
4. Select the operators drop-down list to reveal the available operators to choose from.

# [Onboarded workspaces](#tab/onboarded)
[![Screenshot of list of operators for tag condition in create trigger rule--for onboarded workspaces.](media/create-manage-use-automation-rules/tag-create-condition-defender.png)](media/create-manage-use-automation-rules/tag-create-condition-defender.png#lightbox)

# [Workspaces not onboarded](#tab/not-onboarded)
[![Screenshot of list of operators for tag condition in create trigger rule--for non-onboarded workspaces.](media/create-manage-use-automation-rules/tag-create-condition-azure.png)](media/create-manage-use-automation-rules/tag-create-condition-azure.png#lightbox)

---

    The operators are divided into two categories: **Any individual tag** and **Collection of all tags**. Choose your operator carefully based on how you want the tags to be evaluated.

    For more information, see [*Tag* property: individual vs. collection](automate-incident-handling-with-automation-rules#tag-property-individual-vs-collection).

#### Conditions based on custom details

You can set the value of a [custom detail surfaced in an incident](surface-custom-details-in-alerts) as a condition of an automation rule. Recall that custom details are data points in raw event log records that can be surfaced and displayed in alerts and the incidents generated from them. Use custom details to get to the actual relevant content in your alerts without having to dig through query results.

**Known limitation**: When using custom detail values, the **Does not contain** operator might fail to evaluate correctly when multiple (two or more) distinct values are present.

To add a condition based on a custom detail:

1. Create a new automation rule as described in Create your automation rule.
2. Add a condition or a condition group.
3. Select **Custom details key** from the properties drop-down list. Select **Equals** or **Does not equal** from the operators drop-down list.

    For the custom details condition, the values in the last drop-down list come from the custom details that were surfaced in all the analytics rules listed in the first condition. Select the custom detail you want to use as a condition.

    ![Screenshot of adding a custom detail key as a condition.](media/create-manage-use-automation-rules/custom-detail-key-condition.png)
4. You chose the field you want to evaluate for this condition. Now specify the value appearing in that field that makes this condition evaluate to *true*. Select **+ Add item condition**.

    ![Screenshot of selecting add item condition for automation rules.](media/create-manage-use-automation-rules/add-item-condition.png)

    The value condition line appears below.

    ![Screenshot of the custom detail value field appearing.](media/create-manage-use-automation-rules/custom-details-value.png)
5. Select **Contains** or **Does not contain** from the operators drop-down list. In the text box to the right, enter the value for which you want the condition to evaluate to *true*.

    ![Screenshot of the custom detail value field filled in.](media/create-manage-use-automation-rules/custom-details-value-filled.png)

In this example, if the incident has the custom detail *DestinationEmail*, and if the value of that detail is `pwned@bad-botnet.com`, the actions defined in the automation rule will run.

### Add actions

Choose the actions you want this automation rule to take. Available actions include **Assign owner**, **Change status**, **Change severity**, **Add tags**, and **Run playbook**. You can add as many actions as you like.

If your workspace is onboarded to the Microsoft Defender portal, [Simple Flows](automation/create-basic-automation-rules-simple-flows) (preview) adds more pre-built case and alert actions to this list that don't require a playbook: **Send Case Created/Updated/SLA Exceeded Email**, **Update Case**, **Add Task**, and **Update Alert**.

Note

Only the **Run playbook** action is available in automation rules using the **alert trigger**.

![Screenshot of list of actions to select in automation rule.](media/create-manage-use-automation-rules/select-action.png)

For whichever action you choose, fill out the fields that appear for that action according to what you want done.

If you add a **Run playbook** action, you're prompted to choose from the drop-down list of available playbooks.

- Only playbooks that start with the **incident trigger** can be run from automation rules using one of the incident triggers, so only they appear in the list. Likewise, only playbooks that start with the **alert trigger** are available in automation rules using the alert trigger.
- Microsoft Sentinel must be granted explicit permissions in order to run playbooks. If a playbook appears unavailable in the drop-down list, it means that Sentinel doesn't have permissions to access that playbook's resource group. To assign permissions, select the **Manage playbook permissions** link.

    In the **Manage permissions** panel that opens up, mark the check boxes of the resource groups containing the playbooks you want to run, and select **Apply**.

    ![Manage permissions](media/create-manage-use-automation-rules/manage-permissions.png)

    You yourself must have **owner** permissions on any resource group to which you want to grant Microsoft Sentinel permissions, and you must have the **Microsoft Sentinel Automation Contributor** role on any resource group containing playbooks you want to run.
- If you don't yet have a playbook that takes the action that you want, [create a new playbook](tutorial-respond-threats-playbook). You have to exit the automation rule creation process and restart it after you create your playbook.

#### Move actions around

You can change the order of actions in your rule even after you've added them. Select the blue up or down arrows next to each action to move it up or down one step.

![Screenshot showing how to move actions up or down.](media/create-manage-use-automation-rules/change-actions-order.png)

### Finish creating your rule

Complete the remaining settings to finalize your automation rule:

1. Under **Rule expiration**, if you want your automation rule to expire, set an expiration date, and optionally, a time. Otherwise, leave it as *Indefinite*.
2. The **Order** field is prepopulated with the next available number for your rule's trigger type. This number determines where in the sequence of automation rules (of the same trigger type) that this rule runs. You can change the number if you want this rule to run before an existing rule.

    For more information, see [Notes on execution order and priority](automate-incident-handling-with-automation-rules#notes-on-execution-order-and-priority).
3. Select **Apply**. You're done!

![Screenshot of final steps of creating automation rule.](media/create-manage-use-automation-rules/finish-creating-rule.png)

## Audit automation rule activity

Find out what automation rules might have done to a given incident. You have a full record of incident chronicles available to you in the *SecurityIncident* table in the **Logs** page in the Azure portal, or the **Advanced hunting** page in the Defender portal. The following Kusto query retrieves all incidents that were modified by an automation rule, so you can review which actions were taken automatically:

```kusto
SecurityIncident
| where ModifiedBy contains "Automation"
```

## Automation rules execution

Automation rules run sequentially, according to the order that you determine. Each automation rule executes after the previous one finishes its run. Within an automation rule, all actions run sequentially in the order that they're defined. See [Notes on execution order and priority](automate-incident-handling-with-automation-rules#notes-on-execution-order-and-priority) for more information.

Playbook actions within an automation rule might be treated differently under some circumstances, according to the following criteria:

| Playbook run time | Automation rule advances to the next action... |
| --- | --- |
| Less than a second | Immediately after playbook is completed |
| Less than two minutes | Up to two minutes after playbook began running,but no more than 10 seconds after the playbook is completed |
| More than two minutes | Two minutes after playbook began running,regardless of whether or not it was completed |