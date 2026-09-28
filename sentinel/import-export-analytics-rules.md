---
layout: Conceptual
title: Import and export Microsoft Sentinel analytics rules | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/import-export-analytics-rules
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
description: Export Microsoft Sentinel analytics rules to ARM templates and import them into other workspaces or tenants to manage and control your deployments as code.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 72a4a22d-34ed-4f36-8b97-add0c11afec3
document_version_independent_id: 744345db-b085-2f9c-ec0c-2f0379b2416d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/import-export-analytics-rules.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/import-export-analytics-rules
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/import-export-analytics-rules.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/4e834929-0ce1-4c1d-9c81-fcb14721edfb
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/75670257-a3f0-4627-9981-8046f99219e6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: a1b26664-51f9-0475-4e27-727c65340fa6
---

# Import and export Microsoft Sentinel analytics rules | Microsoft Learn

Important

[**Custom detections**](/en-us/defender-xdr/custom-detections-overview?toc=/azure/sentinel/TOC.json&amp;bc=/azure/sentinel/breadcrumb/toc.json) is now the best way to create new rules across Microsoft Sentinel SIEM Microsoft Defender XDR. With custom detections, you can reduce ingestion costs, get unlimited real-time detections, and benefit from seamless integration with Defender XDR data, functions, and remediation actions with automatic entity mapping. For more information, read [Custom detections are now the unified experience for creating detections in Microsoft Defender XDR](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/custom-detections-are-now-the-unified-experience-for-creating-detections-in-micr/4463875).

Important

Exporting and importing rules is in **PREVIEW**. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

This article shows you how to export Microsoft Sentinel analytics rules to Azure Resource Manager (ARM) template JSON files and import rules from those files into other workspaces or tenants. Use this feature to manage your analytics rules as code, enabling version control and consistent deployment across environments.

## How ARM template export and import works for analytics rules

You can now export your analytics rules to Azure Resource Manager (ARM) template files, and import rules from these files, as part of managing and controlling your Microsoft Sentinel deployments as code. The export action will create a JSON file (named *Azure\_Sentinel\_analytic\_rule.json*) in your browser's downloads location, that you can then rename, move, and otherwise handle like any other file.

The exported JSON file is workspace-independent, so it can be imported to other workspaces and even other tenants. As code, it can also be version-controlled, updated, and deployed in a managed CI/CD framework.

The file includes all the parameters defined in the analytics rule, so for **Scheduled** rules it includes the underlying query and its accompanying scheduling settings, the severity, incident creation, event- and alert-grouping settings, assigned MITRE ATT&CK tactics, and more. Any type of analytics rule - not just **Scheduled** - can be exported to a JSON file.

## Export analytics rules to ARM templates

Perform the following steps to export an analytics rule to an ARM template file:

1. From the Microsoft Sentinel navigation menu, select **Analytics**.
2. Select the rule you want to export and click **Export** from the bar at the top of the screen.

    [![Export analytics rule](media/import-export-analytics-rules/export-analytics-rule.png)](media/import-export-analytics-rules/export-analytics-rule.png#lightbox)

    Note

    - You can select multiple analytics rules at once for export by marking the check boxes next to the rules and clicking **Export** at the end.
    - You can export all the rules on a single page of the display grid at once, by marking the check box in the header row (next to **SEVERITY**) before clicking **Export**. You can't export more than one page's worth of rules at a time, though.
    - Be aware that in this scenario, a single file (named *Azure\_Sentinel\_analytic\_**rules**.json*) will be created, and will contain JSON code for all the exported rules.

## Import analytics rules from ARM templates

Perform the following steps to import an analytics rule from an ARM template file:

1. Have an analytics rule ARM template JSON file ready.
2. From the Microsoft Sentinel navigation menu, select **Analytics**.
3. Click **Import** from the bar at the top of the screen. In the resulting dialog box, navigate to and select the JSON file representing the rule you want to import, and select **Open**.

    [![Import analytics rule](media/import-export-analytics-rules/import-analytics-rule.png)](media/import-export-analytics-rules/import-analytics-rule.png#lightbox)

    Note

    You can import **up to 50** analytics rules from a single ARM template file.