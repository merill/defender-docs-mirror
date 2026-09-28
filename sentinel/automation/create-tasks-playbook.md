---
layout: Conceptual
title: Create and perform incident tasks in Microsoft Sentinel using playbooks | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/automation/create-tasks-playbook
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
description: Use the Microsoft Sentinel connector's Add task action in playbooks to create or complete incident tasks automatically, with support for Standard and Consumption Logic Apps workflows.
ms.topic: how-to
ms.author: monaberdugo
author: mberdugo
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: usx-security
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 8e6514d5-6fc6-7990-d459-9c87680eae0f
document_version_independent_id: 2e2a4369-cf6f-1eb6-bf45-5c06a4f0f07b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/automation/create-tasks-playbook.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/automation/create-tasks-playbook
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/automation/create-tasks-playbook.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
platformId: b00dcaeb-0cec-87c2-e56a-9bb26cd25ba8
---

# Create and perform incident tasks in Microsoft Sentinel using playbooks | Microsoft Learn

This article explains how to use playbooks to create, and optionally perform, incident tasks to manage complex analyst workflow processes in Microsoft Sentinel.

Use the **Add task** action in a playbook, in the Microsoft Sentinel connector, to automatically add a task to the incident that triggered the playbook. Both Standard and Consumption workflows are supported. Before you begin, make sure you meet the prerequisites, including required role assignments.

Tip

Incident tasks can be created automatically not only by playbooks, but also by automation rules, and also manually, ad-hoc, from within an incident.

For more information, see [Use tasks to manage incidents in Microsoft Sentinel](../incident-tasks).

## Prerequisites

Before you begin, make sure you have the following roles and permissions:

- The **Microsoft Sentinel Responder** role is required to view and edit incidents, which is necessary to add, view, and edit tasks.
- The **Logic Apps Contributor** role is required to create and edit playbooks.

For more information, see [Microsoft Sentinel playbook prerequisites](automate-responses-with-playbooks#prerequisites).

## Use a playbook to add a task and perform it

The following sample procedure shows how to add playbook actions that reset a compromised user's password:

- Adds a task to the incident, resetting a compromised user's password
- Adds another playbook action to send a signal to Microsoft Entra ID Protection (AADIP) to actually reset the password
- Adds a final playbook action to mark the task in the incident complete.

To add and configure the task-creation, password-reset, and task-completion actions, take the following steps:

1. From the **Microsoft Sentinel** connector, add the **Add task to incident** action and then:

    1. Select the **Incident ARM ID** dynamic content item for the **Incident ARM id** field.
    2. Enter **Reset user password** as the **Title**.
    3. Add an optional description.

    For example:

    ![Screenshot shows playbook actions to add a task to reset a user's password.](../media/create-tasks-playbook/add-task-reset-password.png)
2. Add the **Entities - Get Accounts (Preview)** action. Add the **Entities** dynamic content item (from the Microsoft Sentinel incident schema) to the **Entities list** field. For example:

    ![Screenshot shows playbook actions to get the account entities in the incident.](../media/create-tasks-playbook/get-entities-accounts.png)
3. Add a **For each** loop from the **Control** actions library. Add the **Accounts** dynamic content item from the **Entities - Get Accounts** output to the **Select an output from previous steps** field. For example:

    ![Screenshot shows how to add a for-each loop action to a playbook in order to perform an action on each discovered account.](../media/create-tasks-playbook/for-each-accounts.png)
4. Inside the **For each** loop, select **Add an action**. Then:

    1. Search for and select the **Microsoft Entra ID Protection** connector
    2. Select the **Confirm a risky user as compromised (Preview)** action.
    3. Add the **Accounts Microsoft Entra user ID** dynamic content item to the **userIds Item - 1** field.

    The **Confirm a risky user as compromised** action sets in motion processes inside Microsoft Entra ID Protection to reset the user's password.

    ![Screenshot shows sending entities to AADIP to confirm compromise.](../media/create-tasks-playbook/confirm-compromised.png)

    Note

    The **Accounts Microsoft Entra user ID** field is one way to identify a user in AADIP. It might not necessarily be the best way in every scenario, but is brought here just as an example.

    For assistance, consult other playbooks that handle compromised users, or the [Microsoft Entra ID Protection documentation](/en-us/azure/active-directory/identity-protection/overview-identity-protection).
5. Add the **Mark a task as completed** action from the Microsoft Sentinel connector and add the **Incident task ID** dynamic content item to the **Task ARM id** field. For example:

    ![Screenshot shows how to add a playbook action to mark an incident task complete.](../media/create-tasks-playbook/mark-complete.png)

## Use a playbook to add a task conditionally

The following sample procedure shows how to add a playbook action that researches an IP address appearing in an incident.

- If the results of this research are that the IP address is malicious, the playbook creates a task for the analyst to disable the user associated with the researched IP address.
- If the IP address isn't a known malicious address, the playbook creates a different task, for the analyst to contact the user to verify the activity.

To add and configure the IP-research condition and conditional task-creation actions, take the following steps:

1. From the Microsoft Sentinel connector, add the **Entities - Get IPs** action. Add the **Entities** dynamic content item (from the Microsoft Sentinel incident schema) to the **Entities list** field. For example:

    ![Screenshot shows playbook actions to get the IP address entities in the incident.](../media/create-tasks-playbook/get-entities-ips.png)
2. Add a **For each** loop from the **Control** actions library. Add the **IPs** dynamic content item from the **Entities - Get IPs** output to the **Select an output from previous steps** field. For example:

    ![Screenshot shows how to add a for-each loop action to a playbook in order to perform an action on each discovered IP address.](../media/create-tasks-playbook/for-each-ips.png)
3. Inside the **For each** loop, select **Add an action**, and then:

    1. Search for and select the **Virus Total** connector.
    2. Select the **Get an IP report (Preview)** action.
    3. Add the **IPs Address** dynamic content item from the **Entities - Get IPs** output to the **IP Address** field.

    For example:

    ![Screenshot shows sending request to Virus Total for IP address report.](../media/create-tasks-playbook/get-virus-total-report.png)
4. Inside the **For each** loop, select **Add an action**, and then:

    1. Add a **Condition** from the **Control** actions library.
    2. Add the **Last analysis statistics Malicious** dynamic content item from the **Get an IP report** output. You might have to select **See more** to find it.
    3. Select the **is greater than** operator and enter `0` as the value.

    The **Last analysis statistics Malicious is greater than 0** condition checks whether the Virus Total IP report returned any malicious results. For example:

    ![Screenshot shows how to set a true-false condition in a playbook.](../media/create-tasks-playbook/set-condition.png)
5. Inside the **True** option, select **Add an action**, and then:

    1. Select the **Add task to incident** action from the **Microsoft Sentinel** connector.
    2. Select the **Incident ARM ID** dynamic content item for the **Incident ARM id** field.
    3. Enter **Mark user as compromised** as the **Title**.
    4. Add an optional description.

    For example:

    ![Screenshot shows playbook actions to add a task to mark a user as compromised.](../media/create-tasks-playbook/condition-true.png)
6. Inside the **False** option, select **Add an action**, and then:

    1. Select the **Add task to incident** action from the **Microsoft Sentinel** connector.
    2. Select the **Incident ARM ID** dynamic content item for the **Incident ARM id** field.
    3. Enter **Reach out to the user to confirm the activity** as the **Title**.
    4. Add an optional description.

    For example:

    ![Screenshot shows playbook actions to add a task to have user confirm activity.](../media/create-tasks-playbook/condition-false.png)