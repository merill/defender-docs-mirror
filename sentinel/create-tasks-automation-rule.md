---
layout: Conceptual
title: Create Incident Tasks in Microsoft Sentinel using Automation Rules | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/create-tasks-automation-rule
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
description: Use automation rules to automatically add incident task lists in Microsoft Sentinel and standardize analyst response workflows across incidents.
ms.topic: how-to
ms.author: monaberdugo
author: mberdugo
ms.reviewer: sshuster
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: a29055a4-686f-e269-a3fe-fed7f59bc99a
document_version_independent_id: 0f455a16-a2fc-9625-a26d-95a3853e3dc8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/create-tasks-automation-rule.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/create-tasks-automation-rule
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/create-tasks-automation-rule.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 8f732194-a7e2-5885-3920-1e411d43e7c4
---

# Create Incident Tasks in Microsoft Sentinel using Automation Rules | Microsoft Learn

This article explains how to use automation rules to create lists of incident tasks, in order to standardize analyst workflow processes in Microsoft Sentinel.

[Incident tasks](incident-tasks) can be created automatically not only by automation rules, but also by playbooks, and also manually, ad-hoc, from within an incident.

## Use cases for different roles

This article addresses the following scenarios that apply to SOC managers, senior analysts, and automation engineers:

- View automation rules with incident task actions
- Add tasks to incidents with automation rules

The scenario of adding tasks to incidents with playbooks is addressed in the following companion article:

- [Add tasks to incidents with playbooks](create-tasks-playbook)

The [Work with tasks](work-with-tasks) article addresses the following scenarios that apply more to SOC analysts:

- [View and follow incident tasks](work-with-tasks#view-and-follow-incident-tasks)
- [Manually add an ad-hoc task to an incident](work-with-tasks#manually-add-an-ad-hoc-task-to-an-incident)

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Prerequisites

The **Microsoft Sentinel Responder** role is required to create automation rules and to view and edit incidents, both of which are necessary to add, view, and edit tasks.

## View automation rules with incident task actions

In the **Automation** page, you can filter the view of automation rules to see only the ones that have **Add task** actions defined.

![Screenshot showing how to filter automation rules grid.](media/create-tasks-automation-rule/filter-grid-on-actions.png)

1. Select the **Actions** filter.
2. Unmark the **Select all** checkbox.
3. Scroll down and mark the **Add task** checkbox.
4. Select **OK** and see the results.

    ![Screenshot showing the results of the filter on the automation rules grid.](media/create-tasks-automation-rule/filtered-grid-on-actions.png)

    The filtered results are the automation rules that add tasks to incidents. The **Analytics rule names** column tells you which analytics rules these automation rules are conditioned on, so you'll have a general idea of which incidents are affected.

    Note

    To have exact knowledge of whether an automation rule will apply to a particular incident, you must open the rule to see if any additional conditions are defined, besides the analytics rule condition. If other conditions are defined, the scope of the affected incidents will be accordingly narrowed.

## Add tasks to incidents with automation rules

Perform the following steps to add tasks to incidents by using an automation rule:

1. In the **Automation** page, select **+ Create** and select **Automation rule**.
2. The **Create new automation rule** panel will open on the right side. Give your automation rule a name that describes what it does.
3. Select **When incident is created** as the trigger (you can also use **When incident is updated**).
4. Add **Conditions** to determine to which incidents new tasks will be added.

    For example, filter by **Analytics rule name**:

    - You might want to add tasks to incidents based on the types of threats detected by an analytics rule or a group of analytics rules that need to be handled according to a certain workflow. Search for and select the relevant analytics rules from the drop-down list.
    - Or, you might want to add tasks that are relevant for incidents across all types of threats (in this case, leave the default selection of **All** as is).

    Whether you select specific analytics rules or leave **All** selected, you can add more conditions to narrow the scope of incidents to which your automation rule will apply. Learn more about [adding advanced conditions to automation rules](add-advanced-conditions-to-automation-rules).

    One thing you'll need to consider is that the order in which tasks appear in your incident is determined by the tasks' creation time. You can set the order of automation rules so that rules that add tasks required for all incidents will run first, and only afterwards any rules that add tasks required for incidents generated by specific analytics rules.

    ![Screenshot of first part of automation rule wizard.](media/create-tasks-automation-rule/create-new-automation-rule.png)
5. Under **Actions**, select **Add task**.

    ![Screenshot of choosing the Add Task action in an automation rule.](media/create-tasks-automation-rule/add-task-action.png)
6. For each task, enter a title in the **Task title** field, and then (optionally) select **+ Add description** to open a description field. Only task titles appear by default in the incident's task list panel. A task's description appears only when the task item is expanded.

    ![Screenshot showing how to add a title and a description to a task.](media/create-tasks-automation-rule/add-title-description.png)
7. In the description field you can add a free-form description for the task, including images, links and rich-text formatting (see the hyperlinks, numbered lists, and code-block-formatted text in the examples below).

    ![Screenshot showing how to add a description to a task.](media/create-tasks-automation-rule/add-task-description.png)
8. Add more tasks to the same group of incidents by selecting **+ Add action** and repeating the last three steps.

    Tasks will be created and added to the incident according to the order of the **Add task** actions in your automation rule.

    ![Screenshot showing how to add more tasks to an automation rule.](media/create-tasks-automation-rule/create-more-tasks.png)
9. Finish creating the automation rule by completing the remaining steps, **Rule expiration** and **Order**, and selecting **Apply** at the end. See [Create and use Microsoft Sentinel automation rules to manage response](create-manage-use-automation-rules) for full details.

    Regarding the **Order** setting: The order in which tasks appear in your incidents depends on two things:

    1. The order of execution of the automation rules, as determined by the number in the **Order** setting, and...
    2. The order of the **Add task** actions defined within each automation rule.