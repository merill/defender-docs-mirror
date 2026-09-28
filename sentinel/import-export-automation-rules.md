---
layout: Conceptual
title: Import and export Microsoft Sentinel automation rules | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/import-export-automation-rules
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
description: Export and import automation rules to and from ARM templates to aid deployment
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.collection: usx-security
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: f86d0ea8-2636-1eff-0f2d-4d25d5249fdc
document_version_independent_id: 9c15840a-0282-a8fb-54c0-8c0886f83757
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/import-export-automation-rules.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/import-export-automation-rules
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/import-export-automation-rules.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/4e834929-0ce1-4c1d-9c81-fcb14721edfb
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/75670257-a3f0-4627-9981-8046f99219e6
platformId: a67a3056-9ed5-e553-c06c-7c34313ac598
---

# Import and export Microsoft Sentinel automation rules | Microsoft Learn

Manage your Microsoft Sentinel automation rules as code! You can now export your automation rules to Azure Resource Manager (ARM) template files, and import rules from these files, as part of your program to manage and control your Microsoft Sentinel deployments as code. The export action creates a JSON file in your browser's downloads location. You can then rename, move, and otherwise handle the file like any other file.

The exported JSON file is workspace-independent, so it can be imported to other workspaces and even other tenants. As code, it can also be version-controlled, updated, and deployed in a managed CI/CD framework.

The exported JSON file includes all the parameters defined in the automation rule. Rules of any trigger type can be exported to a JSON file.

This section explains how to export and import Microsoft Sentinel automation rules.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Export automation rules to ARM templates

To export one or more automation rules to a JSON file, perform the following steps:

1. From the Microsoft Sentinel navigation menu, select **Automation**.
2. Select the rule (or rules—see note) you want to export, and select **Export** from the bar at the top of the screen.

    [![Screenshot showing how to export an automation rule.](media/import-export-automation-rules/export-automation-rule.png)](media/import-export-automation-rules/export-automation-rule.png#lightbox)

    Find the exported file in your Downloads folder. It has the same name as the automation rule, with a .json extension.

    Note

    - You can select multiple automation rules at once for export by marking the check boxes next to the rules and selecting **Export** at the end.
    - You can export all the rules on a single page of the display grid at once, by marking the check box in the header row before clicking **Export**. You can't export more than one page's worth of rules at a time, though.
    - When you export multiple rules at once, a single file (named *Azure\_Sentinel\_automation\_rules.json*) is created, and contains JSON code for all the exported rules.

## Import automation rules from ARM templates

To import automation rules from an ARM template JSON file, perform the following steps:

1. Have an automation rule ARM template JSON file ready.
2. From the Microsoft Sentinel navigation menu, select **Automation**.
3. Select **Import** from the bar at the top of the screen. In the resulting dialog box, navigate to and select the JSON file representing the rule you want to import, and select **Open**.

    [![Screenshot showing how to import an automation rule.](media/import-export-automation-rules/import-automation-rule.png)](media/import-export-automation-rules/import-automation-rule.png#lightbox)

    Note

    You can import **up to 50** automation rules from a single ARM template file.

## Troubleshooting

If you have any issues importing an exported automation rule, consult the troubleshooting table in this section.

| Behavior (with*error*) | Reason | Suggested action |
| --- | --- | --- |
| **Imported automation rule is disabled**-*and*-**The rule's *analytics rule* condition displays "Unknown rule"** | The rule contains a condition that refers to an analytics rule that doesn't exist in the target workspace. | 1. Export the referenced analytics rule from the original workspace and import it to the target one.<br>2. Edit the automation rule in the target workspace, choosing the now-present analytics rule from the drop-down.<br>3. Enable the automation rule. |
| **Imported automation rule is disabled**-*and*-**The rule's *custom details key* condition displays "Unknown custom details key"** | The rule contains a condition that refers to a [custom details key](surface-custom-details-in-alerts) that isn't defined in any analytics rules in the target workspace. | 1. Export the referenced analytics rule from the original workspace and import it to the target one.<br>2. Edit the automation rule in the target workspace, choosing the now-present analytics rule from the drop-down.<br>3. Enable the automation rule. |
| **Deployment failed in target workspace, with error message: "*Automation rules failed to deploy.*"**Deployment details contain the reasons listed in the **Reason** column for failure. | The playbook was moved.-*or*-The playbook was deleted.-*or*-The target workspace doesn't have access to the playbook. | Make sure the playbook exists, and that the target workspace has the right access to the resource group that contains the playbook. |
| **Deployment failed in target workspace, with error message: "*Automation rules failed to deploy.*"**Deployment details contain the reasons listed in the **Reason** column for failure. | The automation rule was past its defined expiration date when you imported it. | **If you want the rule to remain expired in its original workspace:**<br>1. Edit the JSON file that represents the exported automation rule.<br>2. Find the expiration date (that appears immediately after the string `"expirationTimeUtc":`) and replace it with a new expiration date (in the future).<br>3. Save the file and re-import it into the target workspace.<br><br>**If you want the rule to return to active status in its original workspace:**<br>1. Edit the automation rule in the original workspace and change its expiration date to a date in the future.<br>2. Export the rule again from the original workspace.<br>3. Import the newly exported version into the target workspace. |
| **Deployment failed in target workspace, with error message:"*The JSON file you attempted to import has an invalid format. Please check the file and try again.*"** | The imported file isn't a valid JSON file. | Check the file for problems and try again. For best results, export the original rule again to a new file, then try the import again. |
| **Deployment failed in target workspace, with error message:"*No resources found in the file. Please ensure the file contains deployment resources and try again.*"** | The list of resources under the "resources" key in the JSON file is empty. | Check the file for problems and try again. For best results, export the original rule again to a new file, then try the import again. |