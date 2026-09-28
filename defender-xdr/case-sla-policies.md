---
layout: Conceptual
title: SLA policies for cases in the Microsoft Defender portal - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/case-sla-policies
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how SLA policies work for cases in the Microsoft Defender portal.
ms.service: microsoft-defender
ms.subservice: unified-security-operations
author: guywi-ms
ms.author: guywild
ms.date: 2026-07-28T00:00:00.0000000Z
ms.collection:
- M365-security-compliance
- tier1
- usx-security
ms.topic: concept-article
ms.custom: sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: ffb3ecdd-f0c5-fb8f-1939-6750acfdc7a4
document_version_independent_id: ffb3ecdd-f0c5-fb8f-1939-6750acfdc7a4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/case-sla-policies.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: case-sla-policies
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/case-sla-policies.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: a300033c-b74f-5454-5e9a-473984139a29
---

# SLA policies for cases in the Microsoft Defender portal - Microsoft Defender XDR | Microsoft Learn

Service-level agreement (SLA) policies help security operations teams define and track response-time expectations for cases in the Microsoft Defender portal.

Use SLA policies to monitor whether cases are handled within your organization's required timeframes. SLA policies can help teams identify cases that are approaching a breach, cases that have breached, and trends in SLA performance over time.

SLA policies apply to supported case types, including incident cases, generic cases, and exposure cases.

Note

During this preview, SLA policies are supported only in the single-tenant Microsoft Defender portal. They aren't supported in multitenant organization environments.

For information about configuring SLA policies, see [Configure case templates in the Microsoft Defender portal](manage-case-templates).

## How SLA policies work

SLA policies define when a timer starts, when the end criteria are met, when the timer pauses, and how much time is allowed before the SLA is breached.

Organizations commonly use SLA policies for workflows such as:

- Time to acknowledge
- Time to escalate
- Time to resolve

Each SLA policy can be configured with criteria and timers that match your organization's case lifecycle.

## SLA policy criteria

An SLA policy uses criteria to determine when the SLA applies and how the SLA timer behaves.

| Criteria | Description |
| --- | --- |
| **Set criteria** | Defines when the SLA timer starts. For example, when a case status, owner, severity, source, or other supported field changes. |
| **End criteria** | Defines when the SLA is fulfilled and the timer stops. For example, when a case moves to a specific status. |
| **Pause criteria** | Defines when the SLA timer pauses. When the pause criteria no longer apply, the timer resumes. |

For example, a time-to-resolve SLA might start when a case is created, pause when the case is pending, and complete when the case is closed.

## SLA timers

SLA timers define how much time is allowed before the SLA is breached.

A single SLA policy can include different timer durations for different case conditions. For example, your organization might configure a shorter timer for high-severity cases and a longer timer for low-severity cases.

Timer duration can be based on supported case properties, such as:

- Severity
- Source
- Owner or group
- Case type
- Other supported case fields or custom fields

## SLA timer states

An SLA timer can have the following states:

| State | Description |
| --- | --- |
| **Active** | The SLA timer is running and the end criteria haven't been met. |
| **At Risk** | The timer is approaching the breach threshold. This state is available only when an at-risk threshold is configured for the SLA policy. |
| **Breached** | The SLA target was exceeded, but the timer is still running because the end criteria haven't been met. |
| **Paused** | The timer is temporarily stopped because the pause criteria are met. |
| **Completed (Met)** | The end criteria were met before the SLA target was exceeded. |
| **Completed (Breached)** | The end criteria were met after the SLA target was exceeded. |

## SLA timer recalculation

SLA timer recalculation controls what happens when an active case no longer matches its current timer criteria and matches a different timer in the same SLA policy.

For example, a case might start with a high-severity timer and later change to medium severity. If the new severity matches a different timer in the same SLA policy, the SLA can recalculate the remaining time.

When timer recalculation is enabled, the SLA policy can use one of the following behaviors:

| Behavior | Description |
| --- | --- |
| **Carry on** | Keeps the elapsed time and updates the remaining time based on the newly matched timer. |
| **Reset** | Restarts the SLA timer using the full duration of the newly matched timer. |

For example, if a case has a 10-minute timer for high severity and changes to medium severity after five minutes, **Reset** starts the timer again using the full medium-severity timer. **Carry on** keeps the elapsed five minutes and recalculates the remaining time from the medium-severity timer.

## SLA notifications

You can configure email notifications when an SLA timer changes state, including when the timer becomes **Active**, **At Risk**, **Breached**, **Paused**, **Completed (Met)**, or **Completed (Breached)**.

To send SLA notification emails, create an automation rule that uses the **Case updated** trigger. Under **SLA Policies**, select the **Status changed to** or **Status changed from** operator, and then select one or more SLA timer states.

If the case is assigned, the case assignee is always notified in addition to any other recipients selected in the automation rule.

## SLA indicators in the case queue and case details

Cases that match an SLA policy can show SLA information in the case queue and case details.

SLA information can include:

- SLA policy name
- Expiration time
- Remaining time
- SLA timer state

While an SLA timer is running, a positive timer value means that time remains. A negative timer value means that the SLA target was exceeded.

After the end criteria are met, the timer shows **Completed (Met)** if the SLA was completed before the target or **Completed (Breached)** if it was completed after the target.

Use SLA indicators to quickly identify cases that need attention and review the final outcome of completed SLA timers.

## Sort and filter cases by SLA state

You can sort and filter cases by SLA state to find cases that need attention or review completed SLA outcomes.

For example, you can filter the case queue to show:

- Active cases
- Cases that are at risk
- Cases that are breached
- Cases with paused SLA timers
- Cases completed before the SLA target
- Cases completed after the SLA target
- Cases related to a specific SLA policy

Sorting and filtering by SLA state helps analysts prioritize active work and helps managers review completed and breached cases.

## Report on SLA performance

You can use the `SecurityCase` table to create custom reports for SLA performance.

Custom reports can use the SLA information available in the table to review breached cases and analyze SLA performance.

## SLA activity history

Changes to a case's SLA timer appear in the case activity history.

The activity history can include the following SLA events:

| Event | Description |
| --- | --- |
| **Policy applied** | An SLA policy was applied to the case. The event includes the SLA timer and its due date. |
| **Status changed** | The SLA timer changed from one state to another. The event includes the previous and new states. |
| **Timer recalculated** | The SLA timer was recalculated. The event includes the previous and new due dates. |
| **Breached** | The SLA timer exceeded its target. |
| **Completed (Met)** | The end criteria were met before the SLA target was exceeded. |
| **Completed (Breached)** | The end criteria were met after the SLA target was exceeded. |

Use the activity history to review how the SLA state changed during the case lifecycle and to support audit or post-case review.

## Configure SLA policies

SLA policies are configured in case templates.

To configure SLA policies, go to **Case templates** and define the SLA policies that apply to the supported case type.

For more information, see [Configure case templates in the Microsoft Defender portal](manage-case-templates).