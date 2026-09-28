---
layout: Conceptual
title: Add Advanced Conditions to Microsoft Sentinel Automation Rules | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/add-advanced-conditions-to-automation-rules
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
description: This article explains how to add complex, advanced "Or" conditions to automation rules in Microsoft Sentinel, for more effective triage of incidents.
ms.topic: how-to
ms.author: monaberdugo
author: mberdugo
ms.reviewer: sshuster
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 5215e8d2-f547-5f0a-a6ba-8ff5036c8dc5
document_version_independent_id: 5a524863-092d-6b50-e29e-576b7d74b410
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/add-advanced-conditions-to-automation-rules.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/add-advanced-conditions-to-automation-rules
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/add-advanced-conditions-to-automation-rules.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: add6016e-62af-2394-ba3c-29f33bd59ac3
---

# Add Advanced Conditions to Microsoft Sentinel Automation Rules | Microsoft Learn

This article explains how to add advanced "Or" conditions to automation rules in Microsoft Sentinel, for more effective triage of incidents.

Add "Or" conditions in the form of *condition groups* in the Conditions section of your automation rule.

Condition groups can contain two levels of conditions:

- **Simple conditions**: At least two conditions, each separated by an `OR` operator:

    - **A `OR` B**
    - **A `OR` B `OR` C** (Example 1B: Add more OR conditions)
    - and so on.
- **Compound conditions**: More than two conditions, with at least two conditions on at least one side of an `OR` operator:

    - **(A `and` B) `OR` C**
    - **(A `and` B) `OR` (C `and` D)**
    - **(A `and` B) `OR` (C `and` D `and` E)**
    - **(A `and` B) `OR` (C `and` D) `OR` (E `and` F)**
    - and so on.

Using condition groups with OR logic affords you great power and flexibility in determining when rules will run. It can also greatly increase your efficiency by letting you combine many old automation rules into one new rule.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Add a condition group

Since condition groups offer a lot more power and flexibility in creating automation rules, the best way to explain how to add condition groups to automation rules is by presenting some examples.

Let's create a rule that will change the severity of an incoming incident from whatever it is to High, assuming it meets the conditions we'll set.

1. For Microsoft Sentinel in the [Azure portal](https://portal.azure.com), select the **Configuration** &gt; **Automation** page. For Microsoft Sentinel in the [Defender portal](https://security.microsoft.com/), select **Microsoft Sentinel** &gt; **Configuration** &gt; **Automation**.
2. From the **Automation** page, select **Create &gt; Automation rule** from the button bar at the top.

    See the [general instructions for creating an automation rule](create-manage-use-automation-rules) for details.
3. Name the rule *Triage: Change Severity to High*.
4. Select the trigger **When incident is created**.
5. Under **Conditions**, if you see the **Incident provider** and **Analytics rule name** conditions, leave them as they are. The **Incident provider** and **Analytics rule name** conditions aren't available if your workspace is onboarded to the Microsoft Defender portal. In either case, you add more conditions in the following examples.
6. Under **Actions**, select **Change severity** from the drop-down list.
7. Select **High** from the drop-down list that appears below **Change severity**.

For example, the **Onboarded workspaces** and **Workspaces that aren't onboarded** tabs show samples from a workspace that's onboarded to the Defender portal, in either the Azure or Defender portals, and a workspace that isn't onboarded:

# [Add a condition group for onboarded workspaces](#tab/after-onboarding)
The following example shows the automation rule creation experience for workspaces onboarded to the Defender portal.

![Screenshot of creating new automation rule without adding conditions.](media/add-advanced-conditions-to-automation-rules/create-automation-rule-no-conditions-onboarded.png)

# [Add a condition group for workspaces that aren't onboarded](#tab/before-onboarding)
The following example shows the automation rule creation experience for workspaces that aren't onboarded to the Defender portal.

![Screenshot of creating new automation rule without adding conditions.](media/add-advanced-conditions-to-automation-rules/create-automation-rule-no-conditions.png)

---

## Example 1: simple conditions

In this first example, we'll create a simple condition group: If either condition A **or** condition B is true, the rule will run and the incident's severity will be set to *High*.

1. Select the **+ Add** expander and choose **Condition group (Or)** from the drop-down list.

    ![Screenshot of adding a condition group to an automation rule's condition set.](media/add-advanced-conditions-to-automation-rules/add-condition-group.png)
2. See that two sets of condition fields are displayed, separated by an `OR` operator. The two sets of condition fields are conditions A and B, representing the two sides of a simple OR condition group: If A or B is true, the rule will run. (Don't be confused by all the different **Add** links—each one is explained in the following steps.)

    ![Screenshot of empty condition group fields.](media/add-advanced-conditions-to-automation-rules/empty-condition-group.png)
3. Decide what these conditions will be. That is, what two *different* conditions will cause the incident severity to be changed to *High*? We suggest the following:

    - If the incident's associated MITRE ATT&CK **Tactics** include any of the four we've selected from the drop-down (see the image below), the severity should be raised to High.
    - If the incident contains a **Host name** entity named "SUPER\_SECURE\_STATION", the severity should be raised to High.

    ![Screenshot of adding simple OR conditions to an automation rule.](media/add-advanced-conditions-to-automation-rules/add-simple-or-condition.png)

    As long as at least ONE of these conditions is true, the actions we define in the rule will run, changing the severity of the incident to High.

### Example 1A: Add an OR value within a single condition

Let's say we have not one, but two super-sensitive workstations whose incidents we want to make high-severity. To add another value to an entity-property condition, select the dice icon to the right of the current condition value, and then enter an additional value below it.

![Screenshot of adding more values to a single condition.](media/add-advanced-conditions-to-automation-rules/add-value-to-condition.png)

### Example 1B: Add more OR conditions

Let's say we want to have this rule run if one of THREE (or more) conditions is true. If A *or* B *or* C is true, the rule will run.

1. Remember all those **Add** links? To add another OR condition, select the **+ Add** connected by a line to the `OR` operator.

    ![Screenshot of adding another OR condition to an automation rule.](media/add-advanced-conditions-to-automation-rules/add-another-or-condition.png)
2. Now, select the field, operator, and value for the new condition by choosing a property from the drop-down list, selecting a comparison operator, and entering the target value.

    ![Screenshot of another OR condition added to an automation rule.](media/add-advanced-conditions-to-automation-rules/added-another-or-condition.png)

## Example 2: Add compound conditions

In this example, we add multiple conditions to each side of an OR condition group, creating compound logic. The goal is for the rule to run if A *and* B are true, *OR* if C *and* D are true.

1. To add a condition to one side of an OR condition group, select the **+ Add** link immediately below the existing condition, on the same side of the `OR` operator (in the same blue-shaded area) to which you want to add the new condition.

    ![Screenshot of adding a compound condition to an automation rule.](media/add-advanced-conditions-to-automation-rules/add-a-compound-condition.png)

    You'll see a new row added under the existing condition (in the same blue-shaded area), linked to it by an `AND` operator.

    ![Screenshot of empty new condition row in automation rules.](media/add-advanced-conditions-to-automation-rules/empty-new-condition.png)
2. Fill in the parameters and values for the new condition row by selecting a property, operator, and value from the drop-down lists, using the same method you used for the earlier conditions in this condition group.

    ![Screenshot of new condition fields to fill in to add to automation rules.](media/add-advanced-conditions-to-automation-rules/fill-in-new-condition.png)
3. On either side of the OR condition group, select the **+ Add** link below an existing condition to add a new row, and then enter the new condition's parameters and values.

    ![Screenshot of adding multiple compound conditions to an automation rule.](media/add-advanced-conditions-to-automation-rules/add-compound-conditions.png)

That's it! You can use what you've learned here to add more conditions and condition groups, using different combinations of `AND` and `OR` operators, to create powerful, flexible, and efficient automation rules to really help your SOC run smoothly and lower your response and resolution times.