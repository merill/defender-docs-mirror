---
layout: Conceptual
title: Integrate with Microsoft Power Automate for custom alert automation - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/flow-integration
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: Integrate Defender for Cloud Apps with Microsoft Power Automate to trigger custom alert automation and orchestration playbooks, such as ticket creation or approval workflows.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: bfd1a649-7ffe-bbab-da99-14526df94721
document_version_independent_id: bfd1a649-7ffe-bbab-da99-14526df94721
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/flow-integration.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: flow-integration
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/flow-integration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: b6f49711-197d-e453-d117-d2d0c705782c
---

# Integrate with Microsoft Power Automate for custom alert automation - Microsoft Defender for Cloud Apps | Microsoft Learn

Defender for Cloud Apps integrates with [Microsoft Power Automate](/en-us/power-automate/getting-started) to provide custom alert automation and orchestration playbooks. By using the [Power Automate connectors](/en-us/connectors/) available in Power Automate, you can automate the triggering of playbooks when Defender for Cloud Apps generates alerts. For example, automatically create an issue in ticketing systems using [ServiceNow connector](/en-us/connectors/service-now/) or send an approval email to execute a custom governance action when an alert is triggered in Defender for Cloud Apps. Before you begin, make sure you meet the prerequisites.

## Prerequisites

Before you create playbooks, make sure you meet the following prerequisites:

- You must have a valid [Microsoft Power Automate plan](https://flow.microsoft.com/pricing/)
- [Create an API token](api-tokens-legacy) in Defender for Cloud Apps.

## How it works

On its own, Defender for Cloud Apps provides predefined governance options such as suspend a user or make a file private when defining policies. By creating a playbook in Power Automate using a Defender for Cloud Apps connector, you can create workflows to enable customized governance options for your policies. After the playbook is created in Power Automate, it will be automatically synchronized to Defender for Cloud Apps. Then associate the playbook with a policy in Defender for Cloud Apps to send alerts to Power Automate. Microsoft Power Automate offers several connectors and conditions to create a customized workflow for your organization.

The [Defender for Cloud Apps connector](/en-us/connectors/cloudappsecurity/) in Power Automate supports automated triggers and actions. Power Automate is triggered automatically when Defender for Cloud Apps generates an alert. Actions include changing the alert status in Defender for Cloud Apps.

## Create Power Automate playbooks for Defender for Cloud Apps

Perform the following steps to create a Power Automate playbook for Defender for Cloud Apps:

1. [Create an API token](api-tokens-legacy) in Defender for Cloud Apps.
2. Navigate to the [Power Automate portal](https://flow.microsoft.com/), select **My flows**, select **New flow**, and in the drop-down, under **Build your own from blank**, select **Automated cloud flow**.

    ![Screenshot of the Power Automate portal showing the create new flow option.](media/flow-create-new.png)
3. Provide a name for the flow, and in **Choose your flow's trigger**, type *Defender for Cloud Apps* and select **When an alert is generated**.

    ![Screenshot of the Power Automate trigger configuration selecting When an alert is generated for Defender for Cloud Apps.](media/flow-when-alert.png)
4. Under **Authentication settings**, paste the Defender for Cloud Apps API token you created in step 1. Give your connection a name and select **Create**.

    ![Screenshot of the Power Automate authentication settings where the API token is pasted to create a connection.](media/add-token.png)
5. Now create the playbook according to your requirements. Select **+New step** to define the workflow that should be triggered when a policy in Defender for Cloud Apps generates an alert. You can add an action, logical condition, switch case conditions, or loops and save the playbook. In this example, we'll be adding a [ServiceNow connector](/en-us/connectors/service-now/).

    ![Screenshot of the Power Automate workflow showing the alert trigger and configured ServiceNow connector action.](media/flow-workflow.png)
6. Continue to configure your playbook. The playbook will be automatically synchronized with Defender for Cloud Apps. For more information about creating cloud flows in Power Automate, see [Create a cloud flow in Power Automate](/en-us/power-automate/get-started-logic-flow).
7. In the Microsoft Defender Portal, under **Cloud Apps**, go to **Policies** -&gt; **Policy management**. In the row of the policy whose alerts you want to forward to Power Automate, select the three dots and then select **Edit Policy**.
8. Under **Alerts**, select **Send Alerts to Power Automate** and choose the name of your Power Automate playbook from the drop-down menu.

    ![Screenshot of policy Alerts settings with Send Alerts to Power Automate enabled and a playbook selected.](media/flow-alerts-config.png)
9. Defender for Cloud Apps playbooks that you've authored or are granted access to can be seen by in the Microsoft Defender Portal, by going to **Settings**, then choosing **Cloud Apps**, and under **System** selecting **Playbooks**.

    ![Screenshot of the Microsoft Defender Portal Settings, Cloud Apps, System, Playbooks page listing available playbooks.](media/flow-extensions.png)

Note

The maximum supported number of Power Platform environments is 80, but there is no limit to the number of playbooks that can be used within each environment.