---
layout: Conceptual
title: Create basic automation rules with Simple Flows in the Microsoft Defender portal (preview) | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/automation/create-basic-automation-rules-simple-flows
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
description: Use Simple Flows in the Microsoft Defender portal to build case and alert automations directly in automation rules without Logic Apps or playbooks.
ms.author: monaberdugo
author: mberdugo
ms.topic: how-to
ms.date: 2026-05-20T00:00:00.0000000Z
ms.collection: usx-security
locale: en-us
document_id: e3aa68d0-c3f1-a3b8-bd4c-a1101ab929e8
document_version_independent_id: a8c8c94f-8790-785d-6531-1108883d76e1
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/automation/create-basic-automation-rules-simple-flows.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/automation/create-basic-automation-rules-simple-flows
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/automation/create-basic-automation-rules-simple-flows.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 55391a93-a9f4-dc8d-e064-63d06b505b86
---

# Create basic automation rules with Simple Flows in the Microsoft Defender portal (preview) | Microsoft Learn

Simple Flows is a collection of pre-built automation actions in the Microsoft Defender portal. With Simple Flows, you can build a working automation rule by choosing a trigger and adding a single, ready-made action: no playbook, no Logic App. Use Simple Flows to send email notifications, update case fields, add investigation tasks, and update alerts directly from the automation rule wizard.

This article explains how Simple Flows fits into the automation rules engine, describes the new triggers and actions, shows which actions are available for each trigger, and walks through end-to-end examples for common SOC scenarios.

Important

Simple Flows is currently in **public preview**. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](../overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](../move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## What is Simple Flows?

Automation rules in the Microsoft Defender portal follow a three-part model:

**Trigger** &gt; **Conditions** &gt; **Action**

A trigger is the event that starts the rule (for example, a case is created). Conditions filter which events the rule applies to (for example, only high-severity cases). Actions are the operations the rule performs when the conditions are met.

Simple Flows extends this model with new triggers and actions that target the **case** experience in the Defender portal, plus an alert-update action that works with the existing **Alert created** trigger. Each action is a single, configurable building block. You don't need to write code, build a Logic App, or generate a playbook.

Simple Flows is built for security operations center (SOC) teams who need quick, repeatable automation. Common audiences include:

- **SOC analysts** who want to automate routine case and alert handling without leaving the automation rules wizard.
- **Security administrators** who define automation policies across the SOC.
- **Security engineers** who extend incident response automation as part of a larger security orchestration, automation, and response (SOAR) strategy.

For a full overview of automation rules, see [Automate threat response in Microsoft Sentinel with automation rules](../automate-incident-handling-with-automation-rules).

## Prerequisites

Before you create automation rules with Simple Flows, make sure you have:

- Access to cases in the Microsoft Defender portal. Simple Flows is available to:
    - Microsoft Defender XDR customers. See [Microsoft Defender XDR prerequisites](/en-us/defender-xdr/prerequisites) for licensing requirements.
    - Microsoft Sentinel customers with a workspace [onboarded to the unified security operations platform](/en-us/azure/sentinel/microsoft-sentinel-onboard).
- One of the following roles, or an equivalent custom role with permission to manage automation rules and cases:
    - **Microsoft Sentinel Contributor** (to create and edit automation rules).
    - **Security Operator** or **Security Administrator** in Microsoft Defender XDR (to manage cases and alerts).
- For the **Update Alert** action: your account must have permission to update alerts in the source product, and (for Microsoft Sentinel alerts) the data connectors that produce the alerts must be enabled.

For a complete description of permission requirements for automation rules, see [Automate threat response in Microsoft Sentinel with automation rules](../automate-incident-handling-with-automation-rules).

## New triggers

Simple Flows adds two new triggers to the automation rules engine. The pre-existing **Alert created** trigger isn't part of Simple Flows but is listed here because the new **Update Alert** action uses it.

| Trigger | Fires when | Available context | Status |
| --- | --- | --- | --- |
| **Case created** | A new case is created manually, automatically from XDR correlation, through the API, or by another automation rule. | Case ID, Title, Severity, Status, Owner, Description, Tags, Source, Creation time, plus any case custom fields defined in your tenant. | Public preview |
| **Case updated** | An existing case is changed: status, severity, owner, tags, tasks, or other case fields. | Case ID, Title, Severity (old and new), Status (old and new), Owner, Tags, Update time, plus any case custom fields defined in your tenant. | Public preview |
| **Alert created***(existing)* | A new alert is created in Microsoft Sentinel or Microsoft Defender XDR. | Alert ID, Title, Severity, Status, Provider, Tactics, Entities. | Generally available |

### Trigger behaviors to know

- **Loop prevention.** The engine deduplicates events so that the same rule doesn't re-fire on the same case within a single evaluation cycle. This protects you from infinite loops where an automation update re-triggers the rule that produced it.
- **One fire per save.** When you save several changes to a case at once (for example, change severity and owner together), the **Case updated** trigger fires once and evaluates all conditions against the final state, not once per field.
- **Old and new values.** The **Case updated** trigger exposes both the previous and new values of changed fields, so you can write precise conditions like *"Severity changed from Medium to High."*
- **Rule priority.** If multiple rules match the same event, they run in the priority order you configure on the **Automation** page.

## Actions reference

Simple Flows introduces six actions across two categories: case actions (driven by Case Management) and an alert action (driven by the Alerts API). All actions execute through the Unified Actions platform, which routes each action to the correct downstream service.

| Action | Compatible triggers | Configurable fields | Behavior and limits |
| --- | --- | --- | --- |
| **Send Case Created Email** | Case created | Recipient email addresses (one or more). | Sends an email notification when a new case is created. Uses a fixed Microsoft-managed email template with case context (case ID, title, severity, status, owner, and case link). The sender is **Microsoft Security**. |
| **Send Case Updated Email** | Case updated | Recipient email addresses. | Sends an email notification when a case is updated. Uses a fixed template with case context and old/new values of changed fields. Fires once per save. |
| **Update Case** | Case created, Case updated | Standard fields: Name, Description, Assign To, Priority, Status, Due Date, Closing Notes, Email recipients, Grace period. Plus any case custom fields defined in your tenant. | Modifies one or more case fields in a single action. Set only the fields you want to change; other fields stay unchanged. Multiple field updates in one **Update Case** action count as one save and produce a single **Case updated** event downstream. |
| **Add Task** | Case created, Case updated | Per task: Name *(required)*, Status, Priority, Assign To, Due Date, Description, Closing Notes. | Adds one or more investigation tasks to a case, in listed order. Limit: up to **10 tasks per rule**. The action doesn't deduplicate, so repeated rule runs add tasks again. Use **Case updated** conditions to avoid unwanted re-firing. |
| **Update Alert** | Alert created | Status, Classification, Determination, Assigned To. | Modifies fields on a Microsoft Sentinel or Microsoft Defender XDR alert. Executes through the Alerts API and is reflected on the alert immediately. Useful for auto-triaging high-volume, low-fidelity alerts. |

Note

The three email actions share the following constraints in this release: emails use a fixed, Microsoft-managed template (no customization), the sender is always **Microsoft Security**, CC and BCC recipients aren't supported, and email runs aren't written to the case audit log, so you can't verify from the case timeline that a notification was sent.

## Trigger and action compatibility

Not every action works with every trigger. The matrix below shows the supported combinations in this release.

| Action | Case created | Case updated | Alert created |
| --- | --- | --- | --- |
| Send Case Created Email | ✅ |  |  |
| Send Case Updated Email |  | ✅ |  |
| Update Case | ✅ | ✅ |  |
| Add Task | ✅ | ✅ |  |
| Update Alert |  |  | ✅ |

## End-to-end walkthroughs

The following examples show how to combine Simple Flows triggers, conditions, and actions to deliver common SOC workflows.

### Example 1: Auto-triage low-fidelity alerts by classification

Automatically resolve informational alerts from a specific provider as benign positives so the queue stays focused on real threats.

1. In the Microsoft Defender portal, go to **Microsoft Sentinel** &gt; **Automation** and select **+ Create** &gt; **Automation rule**.
2. Under **Trigger**, select **When an alert is created**.
3. Under **Conditions**, add:
    - **Provider***Equals***Microsoft Defender for Endpoint**
    - **Severity***Equals***Informational**
4. Under **Actions**, add **Update Alert**with:
    - **Classification:** Benign positive
    - **Status:** Resolved
5. Save the rule.

### Example 2: Promote tasks when a case moves to Investigating

Add a stage-appropriate checklist the moment an analyst starts investigating.

1. From **Microsoft Sentinel** &gt; **Automation**, create a new automation rule.
2. Under **Trigger**, select **When a case is updated**.
3. Under **Conditions**, add: **Status***Changed to***Investigating**.
4. Under **Actions**, add **Add Task** with the tasks you want the analyst to follow during the investigation phase.
5. Save the rule.

Tip

Combine the **Case updated** trigger's old and new values with rule priority to layer rules without conflicts. A generic rule that runs on every case can be paired with a higher-priority rule that adds extra actions only when severity changes to High or Critical.