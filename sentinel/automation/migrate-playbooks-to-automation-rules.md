---
layout: Conceptual
title: Migrate Microsoft Sentinel alert-trigger playbooks to automation rules | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/automation/migrate-playbooks-to-automation-rules
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
description: This article explains how (and why) to take your existing playbooks built on the alert trigger and migrate them from being invoked by analytics rules to being invoked by automation rules.
ms.topic: how-to
ms.author: monaberdugo
author: mberdugo
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 33aea305-b8ed-e1fa-ecf5-04e06aa128b9
document_version_independent_id: 79c1d3af-c1d6-6d99-096f-aa7f3b2d5f1e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/automation/migrate-playbooks-to-automation-rules.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/automation/migrate-playbooks-to-automation-rules
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/automation/migrate-playbooks-to-automation-rules.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 98885ae6-4469-561e-8c18-be67565005ed
---

# Migrate Microsoft Sentinel alert-trigger playbooks to automation rules | Microsoft Learn

We recommend that you migrate existing playbooks built on alert triggers and migrate them from being invoked by **analytics rules** to being invoked by **automation rules**. This article explains why we recommend migrating playbooks from analytics rules to automation rules, and how to do it. Before you begin, review the Prerequisites.

- If you're migrating a playbook that's used by only one analytics rule, follow the instructions under Create an automation rule from an analytics rule.
- If you're migrating a playbook that's used by multiple analytics rules, follow the instructions under Create a new automation rule from the Automation page.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](../overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](../move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Why migrate

Playbooks that are invoked by automation rules instead of analytics rules have the following advantages:

- Automation management from a single display, regardless of type (“single pane of glass”).
- Use a single automation rule triggering playbooks for multiple analytics rules, instead of configuring each analytics rule separately.
- Define the order in which alert playbooks are to be executed.
- Support for scenarios that set an expiration date for running a playbook.

Migrating your playbook trigger doesn't change the playbook at all, and only changes the mechanism that invokes the playbook to run changes.

The ability to invoke playbooks from analytics rules will be **deprecated effective March 2026**. Until then, playbooks already defined as from analytics rules will continue to run, but as of **June 2023** you can no longer add playbooks to the list of those invoked from analytics rules. The only remaining option is to invoke them from automation rules.

## Prerequisites

You need these roles:

- **Logic Apps Contributor** role to create and edit playbooks.
- **Microsoft Sentinel Contributor** role to attach a playbook to an automation rule.

To learn more, see [Microsoft Sentinel playbook prerequisites](automate-responses-with-playbooks#prerequisites).

## Create an automation rule from an analytics rule

Follow these steps to migrate a playbook that's used by only one analytics rule. If the playbook is used by multiple analytics rules, use Create a new automation rule from the Automation page.

1. For Microsoft Sentinel in the [Azure portal](https://portal.azure.com), select the **Configuration** &gt; **Analytics** page. For Microsoft Sentinel in the [Defender portal](https://security.microsoft.com/), select **Microsoft Sentinel** &gt; **Configuration** &gt; **Analytics**.
2. Under **Active rules**, find an analytics rule already configured to run a playbook, and select **Edit**.

    ![Screenshot of finding and selecting an analytics rule.](../media/migrate-playbooks-to-automation-rules/find-analytics-rule.png)
3. Select the **Automated response** tab. Playbooks directly configured to run from this analytics rule can be found under **Alert automation (classic)**. Notice the warning about deprecation.

    ![Screenshot of automation rules and playbooks screen.](../media/migrate-playbooks-to-automation-rules/see-playbooks.png)
4. In the upper half of the screen, select **+ Add new** under **Automation rules** to create a new automation rule.
5. In the **Create new automation rule** panel, under **Trigger**, select **When alert is created**.

    ![Screenshot of creating automation rule in analytics rule screen.](../media/migrate-playbooks-to-automation-rules/select-trigger.png)
6. Under **Actions**, see that the **Run playbook** action, being the only type of action available, is automatically selected and grayed out. Select your playbook from those available in the drop-down list in the line below.

    ![Screenshot of selecting playbook as action in automation rule wizard.](../media/migrate-playbooks-to-automation-rules/select-playbook.png)
7. Select **Apply**. The new rule shows in the automation rules grid.
8. Remove the playbook from the **Alert automation (classic)** section.
9. **Review and update** the analytics rule to save your changes.

## Create a new automation rule from the Automation page

Use this procedure if you're migrating a playbook that's used by multiple analytics rules. Otherwise, use Create an automation rule from an analytics rule

1. For Microsoft Sentinel in the [Azure portal](https://portal.azure.com), select the **Configuration** &gt; **Analytics** page. For Microsoft Sentinel in the [Defender portal](https://security.microsoft.com/), select **Microsoft Sentinel** &gt; **Configuration** &gt; **Analytics**.
2. From the top menu bar, select **Create -&gt; Automation rule**.
3. In the **Create new automation rule** panel, in the **Trigger** drop-down, select **When alert is created**.
4. Under **Conditions**, select the analytics rules you want to run a particular playbook or a set of playbooks on.
5. Under **Actions**, for each playbook you want this rule to invoke, select **+ Add action**. The **Run playbook** action is automatically selected and grayed out.
6. Select from the list of available playbooks in the drop-down list in the line below. Order the actions according to the order in which you want the playbooks to run by selecting the up/down arrows next to each action.
7. Select **Apply** to save the automation rule.
8. Edit the analytics rule or rules that invoked these playbooks (the rules you specified under **Conditions**), removing the playbook from the **Alert automation (classic)** section of the **Automated response** tab.