---
layout: Conceptual
title: Extend governance to endpoint remediation - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/tutorial-flow
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
description: This tutorial describes the process to configure Microsoft Defender for Cloud Apps policy alerts to trigger Microsoft Power Automate workflows to run Microsoft Defender for Endpoint remediation actions.
ms.date: 2023-01-29T00:00:00.0000000Z
ms.topic: tutorial
ms.custom: sfi-image-nochange
locale: en-us
document_id: f912fadc-e3c0-f55a-46e1-df34dd70908e
document_version_independent_id: f912fadc-e3c0-f55a-46e1-df34dd70908e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/tutorial-flow.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: tutorial-flow
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/tutorial-flow.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 92c735af-442c-8f19-4eb1-08ee53c0980d
---

# Extend governance to endpoint remediation - Microsoft Defender for Cloud Apps | Microsoft Learn

Defender for Cloud Apps provides predefined governance options for policies, such as suspend a user or make a file private. Using the native integration with Microsoft Power Automate, you can use a large ecosystem of software as a service (SaaS) connectors to build workflows to automate processes including remediation.

For example, when detecting a possible malware threat, you can use workflows to start Microsoft Defender for Endpoint remediation actions such as running an antivirus scan or isolating an endpoint.

In this tutorial, you'll learn how to configure a policy governance action to use a workflow to run an antivirus scan on an endpoint where a user shows signs of suspicious behavior:

- 1: Generate a Defender for Cloud Apps API token
- 2: Create a flow to run an antivirus scan
- 3: Configure the flow
- 4: Configure a policy to run the flow

Note

These workflows are only relevant for policies that contains user activity. For example, you can't use these workflows with Discovery or OAuth policies.

If you don't have a Power Automate plan, [sign up for a free trial account](https://flow.microsoft.com/pricing/).

## Prerequisites

- You must have a valid [Microsoft Power Automate plan](https://flow.microsoft.com/pricing/)
- You must have a valid Microsoft Defender for Endpoint plan
- The Power Automate environment must be Microsoft Entra ID synced, Defender for Endpoint monitored, and domain-joined

## Phase 1: Generate a Defender for Cloud Apps API token

Note

If you have previously created a workflow using a Defender for Cloud Apps connector, Power Automate automatically reuses the token and you can skip this step.

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**.
2. Under **System**, choose **API tokens**.
3. Select **+Add token** to generate a new API token.
4. In the **Generate new token** pop-up, enter the token name (for example, "Flow-Token"), and then select **Generate**.

    ![Screenshot of the token window, showing the name entry and generate button.](media/tutorial-flow-token-generate.png)
5. Once the token is generated, select the copy icon to the right of the generated token, and then select **Close**. You'll need the token later.

    ![Screenshot of the token window, showing the token and the copy process.](media/tutorial-flow-token-copy.png)

## Phase 2: Create a flow to run an antivirus scan

Note

If you have previously created a flow using a Defender for Endpoint connector, Power Automate automatically reuses the connector and you can skip the **Sign in** step.

1. Go to the [Power Automate portal](https://flow.microsoft.com/) and select **Templates**.

    ![Screenshot of the main Power Automate page, showing the selection of templates.](media/tutorial-flow-templates.png)
2. Search for *Defender for Cloud Apps* and select **Run antivirus scan using Windows Defender on Defender for Cloud Apps alerts**.

    ![Screenshot of the templates Power Automate page, showing the search results.](media/tutorial-flow-templates-search.png)
3. In the list of apps, on the row in which **Microsoft Defender for Endpoint connector** appears, select **Sign in**.

    ![Screenshot of the templates Power Automate page, showing the sign-in process.](media/tutorial-flow-templates-signin.png)

## Phase 3: Configure the flow

Note

If you have previously created a flow using a Microsoft Entra connector, Power Automate automatically reuses the token and you can skip this step.

1. In the list of apps, on the row in which **Defender for Cloud Apps** appears, select **Create**.

    ![Screenshot of the templates Power Automate page, showing the Defender for Cloud Apps create button.](media/tutorial-flow-templates-create.png)
2. In the **Defender for Cloud Apps** pop-up, enter the connection name (for example, "Defender for Cloud Apps Token"), paste the API token you copied, and then select **Create**.

    ![Screenshot of the Defender for Cloud Apps window, showing the name and key entry and create button.](media/tutorial-flow-templates-create-window.png)
3. In the list of apps, on the row in which **HTTP with Azure AD** appears, select **Sign in**.
4. In the **HTTP with Azure AD** pop-up, for both the **Base Resource URL** and **Azure AD Resource URI** fields, enter `https://graph.microsoft.com`, and then select **Sign in** and enter the admin credentials you want to use with the HTTP with Azure AD connector.

    ![Screenshot of the HTTP with Azure AD window, showing the Resource fields and sign-in button.](media/tutorial-flow-templates-azure.png)
5. Select **Continue**.

    ![Screenshot of the templates Power Automate window, showing the completed actions and continue button.](media/tutorial-flow-templates-continue.png)
6. Once all the connecters are successfully connected, on the flow's page under **Apply to each device**, optionally modify the comment and scan type, and then select **Save**.

    ![Screenshot of the flow page, showing the scan setting section.](media/tutorial-flow-templates-scan.png)

## Phase 4: Configure a policy to run the flow

1. In the Microsoft Defender Portal, under **Cloud Apps**, go to **Policies** -&gt; **Policy management**.
2. In the list of policies, on the row where the relevant policy appears, choose the three dots at the end of the row, and then choose **Edit policy**.
3. Under **Alerts**, select **Send alerts to Power Automate**, and then select **Run antivirus scan using Windows Defender upon a Defender for Cloud Apps alert**.

    ![Screenshot of the policy page, showing the alerts settings section.](media/tutorial-flow-templates-alerts.png)

Now every alert raised for this policy will initiate the flow to run the antivirus scan.

You can use the steps in this tutorial to create a wide range of workflow-based actions to extend Defender for Cloud Apps remediation capabilities, including other Defender for Endpoint actions. To see a list of predefined Defender for Cloud Apps workflows, in Power Automate, [search for "Defender for Cloud Apps"](https://go.microsoft.com/fwlink/?linkid=2102574).