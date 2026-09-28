---
layout: Conceptual
title: Extract incident entities with non-native actions | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/tutorial-extract-incident-entities
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
description: In this tutorial, you extract entity types with action types that aren't native to Microsoft Sentinel, and save these actions in a playbook to use for SOC automation.
ms.topic: tutorial
ms.author: monaberdugo
author: mberdugo
ms.reviewer: efratka
ms.date: 2024-03-14T00:00:00.0000000Z
ms.collection: usx-security
ms.custom: sfi-image-nochange
locale: en-us
document_id: e8409b88-38e9-3f32-38f3-b6ef5e6f43eb
document_version_independent_id: f98d22ac-8eef-5585-e949-a4e2dfae9236
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/tutorial-extract-incident-entities.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/tutorial-extract-incident-entities
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/tutorial-extract-incident-entities.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: b94a7602-25ee-88ea-2d4f-1e798057d6f1
---

# Extract incident entities with non-native actions | Microsoft Learn

Entity mapping enriches alerts and incidents with information essential for any investigative processes and remedial actions that follow.

Microsoft Sentinel playbooks include these native actions to extract entity info:

- Accounts
- DNS
- File hashes
- Hosts
- IPs
- URLs

In addition to these actions, analytic rule entity mapping contains entity types that aren't native actions, like malware, process, registry key, mailbox, and more. In this tutorial, you learn how to work with non-native actions using different built-in actions to extract the relevant values.

In this tutorial, you learn how to:

- Create a playbook with an incident trigger and run it manually on the incident.
- Initialize an array variable.
- Filter the required entity type from other entity types.
- Parse the results in a JSON file.
- Create the values as dynamic content for future use.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Prerequisites

To complete this tutorial, make sure you have:

- An Azure subscription. Create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) if you don't already have one.
- An Azure user with the following roles assigned on the following resources:

    - [**Microsoft Sentinel Contributor**](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-contributor) on the Log Analytics workspace where Microsoft Sentinel is deployed.
    - [**Logic App Contributor**](/en-us/azure/role-based-access-control/built-in-roles#logic-app-contributor), and **Owner** or equivalent, on whichever resource group will contain the playbook created in this tutorial.
- A (free) [VirusTotal account](https://www.virustotal.com/gui/my-apikey) will suffice for this tutorial. A production implementation requires a VirusTotal Premium account.

## Create a playbook with an incident trigger

1. For Microsoft Sentinel in the [Defender portal](https://security.microsoft.com/), select **Microsoft Sentinel** &gt; **Configuration** &gt; **Automation**. For Microsoft Sentinel in the [Azure portal](https://portal.azure.com), select the **Configuration** &gt; **Automation** page.
2. On the **Automation** page, select **Create** &gt; **Playbook with incident trigger**.
3. In the **Create playbook** wizard, under **Basics**, select the subscription and resource group, and give the playbook a name.
4. Select **Next: Connections &gt;**.

    Under **Connections**, the **Microsoft Sentinel - Connect with managed identity** connection should be visible. For example:

    ![Screenshot of creating a new playbook with an incident trigger.](media/tutorial-extract-incident-entities/create-playbook.png)
5. Select **Next: Review and create &gt;**.
6. Under **Review and create**, select **Create and continue to designer**.

    The Logic app designer opens a logic app with the name of your playbook.

    ![Screenshot of viewing the playbook in the Logic app designer.](media/tutorial-extract-incident-entities/logic-app-designer.png)

## Initialize an Array variable

1. In the Logic app designer, under the step where you want to add a variable, select **New step**.
2. Under **Choose an operation**, in the search box, type *variables* as your filter. From the actions list, select **Initialize variable**.
3. Provide this information about your variable:

    1. For the variable name, use *Entities*.
    2. For the type, select **Array**.
    3. For the value, hover over the **Value** field, and select **fx** in the blue icon group on the left.

        ![Screenshot of initializing a variable in the Logic app designer.](media/tutorial-extract-incident-entities/initialize-variable-fx.png)
    4. In the dialog box that opens, select the **Dynamic content** tab, and in the search box, type *entities*.
    5. Select **Entities** from the list and select **Add**.

        ![Screenshot of selecting the Entities value in the Logic app designer.](media/tutorial-extract-incident-entities/initialize-variable-select-entities.png)

## Select an existing incident

1. In Microsoft Sentinel, navigate to **Incidents** and select an incident on which you want to run the playbook.
2. In the incident page on the right, select **Actions &gt; Run playbook (Preview**).
3. Under **Playbooks**, next to the playbook you created, select **Run**.

    When the playbook is triggered, a **Playbook is triggered successfully** message is visible on the top right.
4. Select **Runs**, and next to your playbook, select **View Run**.

    The **Logic app run** page is visible.
5. Under **Initialize variable**, the sample payload is visible under **Value**. Note the sample payload for later use.

    [![Screenshot of viewing the sample payload under the Value field.](media/tutorial-extract-incident-entities/sample-payload-new.png)](media/tutorial-extract-incident-entities/sample-payload-new.png#lightbox)

## Filter the required entity type from other entity types

1. Navigate back to the **Automation** page and select your playbook.
2. Under the step where you want to add a variable, select **New step**.
3. Under **Choose an action**, in the search box, enter *filter array* as your filter. From the actions list, select **Data operations**.

    [![Screenshot of filtering an array and selecting data operations.](media/tutorial-extract-incident-entities/filter-array-data-operations.png)](media/tutorial-extract-incident-entities/filter-array-data-operations.png#lightbox)
4. Provide this information about your filter array:

    1. Under **From** &gt; **Dynamic content**, select the **Entities** variable you initialized previously.
    2. Select the first **Choose a value** field (on the left), and select **Expression**.
    3. Paste the value *item()?['kind']*, and select **OK**.

        [![Screenshot of filling in the filter array expression.](media/tutorial-extract-incident-entities/filter-array-information.png)](media/tutorial-extract-incident-entities/filter-array-information.png#lightbox)
    4. Leave the **is equal to** value (do not modify it).
    5. In the second **Choose a value** field (on the right), type *Process*. This needs to be an exact match to the value in the system.

        Note

        This query is case-sensitive. Ensure that the `kind` value matches the value in the sample payload. See the sample payload from when you create a playbook.

        ![Screenshot of filling in the filter array information.](media/tutorial-extract-incident-entities/filter-array-information-full.png)

## Parse the results to a JSON file

1. In your logic app, under the step where you want to add a variable, select **New step**.
2. Select **Data operations** &gt; **Parse JSON**.

    ![Screenshot of selecting the Parse JSON option under Data Operations.](media/tutorial-extract-incident-entities/parse-json.png)
3. Provide this information about your operation:

    1. Select **Content**, and under **Dynamic content** &gt; **Filter array**, select **Body**.

        ![Screenshot of selecting Dynamic content under Content.](media/tutorial-extract-incident-entities/dynamic-content-new.png)
    2. Under **Schema**, paste a JSON schema so that you can extract values from an array. Copy the sample payload you generated when you created the playbook.

        [![Screenshot of copying the sample payload.](media/tutorial-extract-incident-entities/copy-sample-payload-new.png)](media/tutorial-extract-incident-entities/copy-sample-payload-new.png#lightbox)
    3. Return to the playbook, and select **Use sample payload to generate schema**.

        ![Screenshot of selecting Use sample payload to generate schema.](media/tutorial-extract-incident-entities/use-sample-payload.png)
    4. Paste the payload. Add an opening square bracket (`[`) at the beginning of the schema and close them at the end of the schema `]`.

        ![Screenshot of pasting the sample payload.](media/tutorial-extract-incident-entities/paste-sample-payload-first.png)

        ![Screenshot of the second part of the pasted sample payload.](media/tutorial-extract-incident-entities/paste-sample-payload-second.png)
    5. Select **Done**.

## Use the new values as dynamic content for future use

You can now use the values you created as dynamic content for further actions. For example, if you want to send an email with process data, you can find the **Parse JSON** action under **Dynamic content**, if you didn't change the action name.

![Screenshot of sending an email with process data.](media/tutorial-extract-incident-entities/utilize-dynamic-content-new.png)

## Ensure that your playbook is saved

Ensure that the playbook is saved, and you can now use your playbook for SOC operations.