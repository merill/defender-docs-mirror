---
layout: Conceptual
title: Tutorial - Automatically check and record IP address reputation in incident in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/tutorial-enrich-ip-information
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
description: In this tutorial, learn how to use Microsoft Sentinel automation rules and playbooks to automatically check IP addresses in your incidents against a threat intelligence source and record each result in its relevant incident.
ms.topic: tutorial
ms.author: monaberdugo
author: mberdugo
ms.reviewer: sshuster
ms.date: 2024-03-14T00:00:00.0000000Z
ms.collection: usx-security
ms.custom: sfi-image-nochange
locale: en-us
document_id: d52f56c9-b7be-4a2b-2802-4ad100c6b760
document_version_independent_id: 9ac19667-73cd-beb9-9fcc-2a9d73f4460a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/tutorial-enrich-ip-information.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/tutorial-enrich-ip-information
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/tutorial-enrich-ip-information.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: f18be932-27cc-c2ea-0165-2d26029a95c9
---

# Tutorial - Automatically check and record IP address reputation in incident in Microsoft Sentinel | Microsoft Learn

One quick and easy way to assess the severity of an incident is to see if any IP addresses in it are known to be sources of malicious activity. Having a way to do this automatically can save you a lot of time and effort.

In this tutorial, you'll learn how to use Microsoft Sentinel automation rules and playbooks to automatically check IP addresses in your incidents against a threat intelligence source and record each result in its relevant incident.

When you complete this tutorial, you'll be able to:

- Create a playbook from a template
- Configure and authorize the playbook's connections to other resources
- Create an automation rule to invoke the playbook
- See the results of your automated process

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Prerequisites

To complete this tutorial, make sure you have:

- An Azure subscription. Create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) if you don't already have one.
- A Log Analytics workspace with the Microsoft Sentinel solution deployed on it and data being ingested into it.
- An Azure user with the following roles assigned on the following resources:

    - [**Microsoft Sentinel Contributor**](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-contributor) on the Log Analytics workspace where Microsoft Sentinel is deployed.
    - [**Logic App Contributor**](/en-us/azure/role-based-access-control/built-in-roles#logic-app-contributor), and **Owner** or equivalent, on whichever resource group will contain the playbook created in this tutorial.
- Installed [VirusTotal Solution from the Content Hub](https://azuremarketplace.microsoft.com/en-gb/marketplace/apps/azuresentinel.azure-sentinel-solution-virustotal?tab=Overview)
- A (free) [VirusTotal account](https://www.virustotal.com/gui/my-apikey) will suffice for this tutorial. A production implementation requires a VirusTotal Premium account.
- An Azure Monitor Agent installed on at least one machine in your environment, so that incidents are generated and sent to Microsoft Sentinel.

## Create a playbook from a template

Microsoft Sentinel includes ready-made, out-of-the-box playbook templates that you can customize and use to automate a large number of basic SecOps objectives and scenarios. Let's find one to enrich the IP address information in our incidents.

1. In Microsoft Sentinel, select **Configuration** &gt; **Automation**.
2. From the **Automation** page, select the **Playbook templates (Preview)** tab.
3. Locate and select one of the **IP Enrichment - Virus Total report** templates, for either entity, incident, or alert triggers. If needed, filter the list by the **Enrichment** tag to find your templates.
4. Select **Create playbook** from the details pane. For example:

    ![Screenshot of the IP Enrichment - Virus Total Report - Entity Trigger template selected.](media/restore/select-virus-total.png)
5. The **Create playbook** wizard will open. In the **Basics** tab:

    1. Select your **Subscription**, **Resource group**, and **Region** from their respective drop-down lists.
    2. Edit the **Playbook name** by adding to the end of the suggested name "*Get-VirusTotalIPReport*". This way you'll be able to tell which original template this playbook came from, while still ensuring that it has a unique name in case you want to create another playbook from this same template. Let's call it "*Get-VirusTotalIPReport-Tutorial-1*".
    3. Leave the **Enable diagnostics logs in Log Analytics** option unchecked.
    4. Select **Next : Connections &gt;**.
6. In the **Connections** tab, you'll see all the connections that this playbook needs to make to other services, and the authentication method that will be used if the connection has already been made in an existing Logic App workflow in the same resource group.

    1. Leave the **Microsoft Sentinel** connection as is (it should say "*Connect with managed identity*").
    2. If any connections say "*New connection will be configured*," you're prompted to do so at the next stage of the tutorial. Or, if you already have connections to these resources, select the expander arrow to the left of the connection and choose an existing connection from the expanded list. For this exercise, we'll leave it as is.

        ![Screenshot of the Connections tab of the playbook creation wizard.](media/tutorial-enrich-ip-information/4-playbook-connections-tab.png)
    3. Select **Next : Review and create &gt;**.
7. In the **Review and create** tab, review all the information you've entered as it's displayed here, and select **Create playbook**.

    ![Screenshot of the Review and create tab from the playbook creation wizard.](media/tutorial-enrich-ip-information/5-playbook-review-tab.png)

    As the playbook is deployed, you'll see a quick series of notifications of its progress. Then the **Logic app designer** will open with your playbook displayed. We still need to authorize the logic app's connections to the resources it interacts with so that the playbook can run. Then we'll review each of the actions in the playbook to make sure they're suitable for our environment, making changes if necessary.

    [![Screenshot of playbook open in logic app designer window.](media/tutorial-enrich-ip-information/6-playbook-logic-app-designer.png)](media/tutorial-enrich-ip-information/6-playbook-logic-app-designer.png#lightbox)

## Authorize logic app connections

Recall that when we created the playbook from the template, we were told that the Azure Log Analytics Data Collector and Virus Total connections would be configured later.

![Screenshot of review information from playbook creation wizard.](media/tutorial-enrich-ip-information/7-authorize-connectors.png)

Here's where we do that.

### Authorize Virus Total connection

1. Select the **For each** action to expand it and review its contents, which include the actions that will be performed for each IP address. For example:

    ![Screenshot of for-each loop statement action in logic app designer.](media/tutorial-enrich-ip-information/8-for-each-loop.png)
2. The first action item you see is labeled **Connections** and has an orange warning triangle.

    If instead, that first action is labeled **Get an IP report (Preview)**, that means you already have an existing connection to Virus Total and you can go to the next step.

    1. Select the **Connections** action to open it.
    2. Select the icon in the **Invalid** column for the displayed connection.

        ![Screenshot of invalid Virus Total connection configuration.](media/tutorial-enrich-ip-information/9-virus-total-invalid.png)

        You'll be prompted for connection information.

        ![Screenshot shows how to enter API key and other connection details for Virus Total.](media/tutorial-enrich-ip-information/10-virus-total-connection.png)
    3. Enter "*Virus Total*" as the **Connection name**.
    4. For **x-api\_key**, copy and paste the API key from your Virus Total account.
    5. Select **Update**.
    6. Now you'll see the **Get an IP report (Preview)** action properly. (If you already had a Virus Total account, you'll already be at this stage.)

        ![Screenshot shows the action to submit an IP address to Virus Total to receive a report about it.](media/tutorial-enrich-ip-information/11-get-ip-report-action.png)

### Authorize Log Analytics connection

The next action is a **Condition** that determines the rest of the for-each loop's actions based on the outcome of the IP address report. It analyzes the **Reputation** score given to the IP address in the report. A score higher than **0** indicates the address is harmless; a score lower than **0** indicates it's malicious.

![Screenshot of condition action in logic app designer.](media/tutorial-enrich-ip-information/12-reputation-condition.png)

Whether the condition is true or false, we want to send the data in the report to a table in Log Analytics so it can be queried and analyzed, and add a comment to the incident.

But as you'll see, we have more invalid connections we need to authorize.

[![Screenshot showing true and false scenarios for defined condition.](media/tutorial-enrich-ip-information/13-condition-true-false-actions.png)](media/tutorial-enrich-ip-information/13-condition-true-false-actions.png#lightbox)

1. Select the **Connections** action in the **True** frame.
2. Select the icon in the **Invalid** column for the displayed connection.

    ![Screenshot of invalid Log Analytics connection configuration.](media/tutorial-enrich-ip-information/14-log-analytics-invalid.png)

    You'll be prompted for connection information.

    ![Screenshot shows how to enter Workspace ID and key and other connection details for Log Analytics.](media/tutorial-enrich-ip-information/15-log-analytics-connection.png)
3. Enter "*Log Analytics*" as the **Connection name**.
4. For **Workspace ID**, copy and paste the ID from the **Overview** page of the Log Analytics workspace settings.
5. Select **Update**.
6. Now you'll see the **Send data** action properly. (If you already had a Log Analytics connection from Logic Apps, you'll already be at this stage.)

    ![Screenshot shows the action to send a Virus Total report record to a table in Log Analytics.](media/tutorial-enrich-ip-information/16-send-data.png)
7. Now select the **Connections** action in the **False** frame. This action uses the same connection as the one in the True frame.
8. Verify the connection called **Log Analytics** is marked, and select **Cancel**. This ensures that the action will now be displayed properly in the playbook.

    ![Screenshot of second invalid Log Analytics connection configuration.](media/tutorial-enrich-ip-information/17-log-analytics-invalid-2.png)

    Now you'll see your entire playbook, properly configured.
9. **Very important!** Don't forget to select **Save** at the top of the **Logic app designer** window. After you see notification messages that your playbook was saved successfully, you'll see your playbook listed in the *Active playbooks*\* tab in the **Automation** page.

## Create an automation rule

Now, to actually run this playbook, you'll need to create an automation rule that will run when incidents are created and invoke the playbook.

1. From the **Automation** page, select **+ Create** from the top banner. From the drop-down menu, select **Automation rule**.

    ![Screenshot of creating an automation rule from the Automation page.](media/tutorial-enrich-ip-information/19-add-automation-rule.png)
2. In the **Create new automation rule** panel, name the rule "*Tutorial: Enrich IP info*".

    ![Screenshot of creating an automation rule, naming it, and adding a condition.](media/tutorial-enrich-ip-information/20-create-automation-rule-name.png)
3. Under **Conditions**, select **+ Add** and **Condition (And)**.

    ![Screenshot of adding a condition to an automation rule.](media/tutorial-enrich-ip-information/21-automation-rule-add-condition.png)
4. Select **IP Address** from the property drop-down on the left. Select **Contains** from the operator drop-down, and leave the value field blank. This effectively means that the rule will apply to incidents that have an IP address field that contains anything.

    We don't want to stop any analytics rules from being covered by this automation, but we don't want the automation to be triggered unnecessarily either, so we're going to limit the coverage to incidents that contain IP address entities.

    ![Screenshot of defining a condition to add to an automation rule.](media/tutorial-enrich-ip-information/22-automation-rule-condition.png)
5. Under **Actions**, select **Run playbook** from the drop-down.
6. Select the new drop-down that appears.

    ![Screenshot showing how to select your playbook from the list of playbooks - part 1.](media/tutorial-enrich-ip-information/23-add-run-playbook-action.png)

    You'll see a list of all the playbooks in your subscription. The grayed-out ones are those you don't have access to. In the **Search playbooks** text box, begin typing the name - or any part of the name - of the playbook we created above. The list of playbooks will be dynamically filtered with each letter you type.

    ![Screenshot showing how to select your playbook from the list of playbooks - part 2.](media/tutorial-enrich-ip-information/24-search-playbooks.png)

    When you see your playbook in the list, select it.

    ![Screenshot showing how to select your playbook from the list of playbooks - part 3.](media/tutorial-enrich-ip-information/25-select-playbook.png)

    If the playbook is grayed out, select the **Manage playbook permissions** link (in the fine-print paragraph below where you selected a playbook - see the screenshot above). In the panel that opens up, select the resource group containing the playbook from the list of available resource groups, then select **Apply**.
7. Select **+ Add action** again. Now, from the new action drop-down that appears, select **Add tags.**
8. Select **+ Add tag**. Enter "*Tutorial-Enriched IP addresses*" as the tag text and select **OK**.

    ![Screenshot showing how to add a tag to an automation rule.](media/tutorial-enrich-ip-information/26-automation-rule-tags.png)
9. Leave the remaining settings as they are, and select **Apply**.

## Verify successful automation

1. In the **Incidents** page, enter the tag text *Tutorial-Enriched IP addresses* into the **Search** bar and hit the Enter key to filter the list for incidents with that tag applied. These are the incidents that our automation rule ran on.
2. Open any one or more of these incidents and see if there are comments about the IP addresses there. The presence of these comments indicates that the playbook ran on the incident.

## Clean up resources

If you're not going to continue to use this automation scenario, delete the playbook and automation rule you created with the following steps:

1. In the **Automation** page, select the **Active playbooks** tab.
2. Enter the name (or part of the name) of the playbook you created in the **Search** bar. (If it doesn't show up, make sure any filters are set to **Select all**.)
3. Mark the check box next to your playbook in the list, and select **Delete** from the top banner. (If you don't want to delete it, you can select **Disable** instead.)
4. Select the **Automation rules** tab.
5. Enter the name (or part of the name) of the automation rule you created in the **Search** bar. (If it doesn't show up, make sure any filters are set to **Select all**.)
6. Mark the check box next to your automation rule in the list, and select **Delete** from the top banner. (If you don't want to delete it, you can select **Disable** instead.)