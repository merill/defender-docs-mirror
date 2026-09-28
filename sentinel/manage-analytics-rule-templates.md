---
layout: Conceptual
title: Manage Template Versions for your Scheduled Analytics Rules in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/manage-analytics-rule-templates
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
description: Learn how to manage the relationship between your scheduled analytics rule templates and the rules created from those templates. Merge updates to the templates into your rules, and revert changes in your rules back to the original template.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: d6ae3cad-4025-c5f6-4ffd-f5aba8a35a8e
document_version_independent_id: 65da8afc-a09d-7248-9281-db8f98b6ce63
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/manage-analytics-rule-templates.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/manage-analytics-rule-templates
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/manage-analytics-rule-templates.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: dbfdec16-1073-d92e-39fd-44970f815fac
---

# Manage Template Versions for your Scheduled Analytics Rules in Microsoft Sentinel | Microsoft Learn

Important

[**Custom detections**](/en-us/defender-xdr/custom-detections-overview?toc=/azure/sentinel/TOC.json&amp;bc=/azure/sentinel/breadcrumb/toc.json) is now the best way to create new rules across Microsoft Sentinel SIEM Microsoft Defender XDR. With custom detections, you can reduce ingestion costs, get unlimited real-time detections, and benefit from seamless integration with Defender XDR data, functions, and remediation actions with automatic entity mapping. For more information, read [Custom detections are now the unified experience for creating detections in Microsoft Defender XDR](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/custom-detections-are-now-the-unified-experience-for-creating-detections-in-micr/4463875).

This article explains how to track template version changes for your scheduled analytics rules in Microsoft Sentinel, update your rules to match new template versions, and revert rules back to their original templates.

Important

Managing analytics rule template versions is in **PREVIEW**. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

## How template version management works

Microsoft Sentinel contains [analytics rule templates](threat-detection) that you turn into active rules by effectively creating a copy of them – that’s what happens when you create a rule from a template. At that point, however, the active rule is no longer connected to the template. If changes are made to a rule template, by Microsoft engineers or anyone else, any rules created from that template beforehand are ***not*** dynamically updated to match the new template.

However, rules created from templates ***do*** remember which templates they came from, which allows you two advantages:

- If you made changes to a rule when creating it from a template, or at any time afterward, you can always revert the rule back to its original version.
- You get notified when a template is updated. You can either update your rules to the new version of their templates, or leave them as they are.

This article shows you how to manage these tasks, and what to keep in mind. The procedures discussed in the article apply to any **[Scheduled](scheduled-rules-overview)** analytics rules created from templates.

## Discover your rule's template version number

With the implementation of template version control, you can see and track the versions of your rule templates and the rules created from them. Rules with updated templates display an "*Update*" badge next to the rule name.

1. On the **Analytics** page, select the **Active rules** tab.
2. Select any rule of type **Scheduled**.

    - If the rule displays the "*Update*" badge, its details pane will have a **Review and update** button next to the **Edit** button (see image 1 in the next step).
    - If the rule was created from a template but doesn't have the "*Update*" badge, its details pane will have a **Compare with template** button next to the **Edit** button (see images 2 and 3 in the next step).
    - If there's only an **Edit** button, the rule was created from scratch, not from a template.

        [![Screenshot of active rules list, with badge indicating a template update is available.](media/manage-analytics-rule-templates/see-rules-with-updated-template.png)](media/manage-analytics-rule-templates/see-rules-with-updated-template.png#lightbox)
3. Scroll down to the bottom of the details pane, where you see two version numbers: the version of the template from which the rule was created, and the latest available version of the template.

    ![Screenshot of details pane. Scroll down to see template version numbers.](media/manage-analytics-rule-templates/see-template-versions.png)

    Each version number is in a "1.0.0" format – major version, minor version, and build.

    - A difference in the *major version* number indicates that something essential in the template was changed, that could affect how the rule detects threats or even its ability to function altogether. You want to include this change in your rules.
    - A difference in the *minor version* number indicates a minor improvement in the template – a cosmetic change or something similar – that would be "nice to have" but is not critical to maintaining the rule’s functionality, efficacy, or performance. You could just as easily take this change or leave it.

    Note

    Images 2 and 3 show two examples of rules created from templates, where the template has not been updated.

    - Image 2 shows a rule that has a version number for its current template. This signals that the rule was created after Microsoft Sentinel's initial implementation of template version control in October 2021.
    - Image 3 shows a rule that doesn't have a current template version. This shows that the rule had been created before October 2021. If there is a latest template version available, it's likely a newer version of the template than the one used to create the rule.

## Compare your active rule with its template

Choose either the **Update template** tab or the **Revert to template** tab for the relevant instructions:

# [Update template](#tab/update)
Note

Updating this rule will overwrite your existing rule with the latest version of the template.

Any automation step or logic that refers to the existing rule should be verified, in case the referenced names changed. Also, any customizations you made in creating the original rule—changes to the query, scheduling, grouping, or other settings—might be overwritten.

Having selected a rule and determined that you want to consider updating it, select **Review and update** in the rule details pane. You see that the **Analytics rule wizard** now has a **Compare to latest version** tab.

On the **Compare to latest version** tab, you see a side-by-side comparison between the YAML representations of the existing rule and the latest version of the template.

![Screenshot of 'Compare to latest version' tab in Analytics rule wizard.](media/manage-analytics-rule-templates/compare-template-versions.png)

### Update your rule with the new template version

Choose one of the following actions to apply, customize, or cancel the template update:

- If the changes made to the new version of the template are acceptable to you, and nothing else in your original rule is affected, select **Review and update** to validate and apply the changes.
- If you want to further customize the rule or reapply any changes that might otherwise be overwritten, select **Next : Custom changes**. Cycle through the remaining tabs of the [Analytics rule wizard](create-analytics-rules) to make those changes, then validate and apply the changes on the **Review and update** tab.
- If you don't want to make any changes to your existing rule, but rather to keep the existing template version, simply exit the wizard by selecting the X in the upper right corner.

# [Revert to template](#tab/revert)
Note

Updating this rule overwrites your existing rule with the latest version of the template.

Any automation step or logic that refers to the existing rule should be verified, in case the referenced names changed. Also, any customizations you made in creating the original rule, including changes to the query, scheduling, grouping, or other settings, might be overwritten.

Having selected a rule and determined that you want to revert to its original version, select **Compare with template** in the rule details pane. You see that the **Analytics rule wizard** now has a **Compare to latest version** tab.

On the **Compare to latest version** tab, you see a side-by-side comparison between the YAML representations of the existing rule and the latest version of the template. These two version numbers might be the same, but the right side shows the original, unchanged template, and the left side shows the active rule, including any changes from the original template.

![Screenshot of 'Compare to latest version' tab in Analytics rule wizard.](media/manage-analytics-rule-templates/compare-template-versions-2.png)

### Revert your rule to its original template version

Use one of the following options to revert the rule, make additional changes, or cancel the operation:

- If you want to revert completely to the original version of this rule—a clean copy of the template—select **Review and update** to validate and apply the changes.
- If you want to customize the rule differently or reapply any changes that might otherwise be overwritten, select **Next : Custom changes**. Cycle through the remaining tabs of the [Analytics rule wizard](create-analytics-rules) to make those changes, then validate and apply the changes on the **Review and update** tab.
- If you don't want to make any changes to your existing rule, simply exit the wizard by selecting the X in the upper right corner.

---