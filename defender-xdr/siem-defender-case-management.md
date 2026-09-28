---
layout: Conceptual
title: Case management in the Microsoft Defender portal - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/siem-defender-case-management
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how case management in the Microsoft Defender portal helps security operations teams manage incident cases and generic cases with tasks, evidence, activity history, and workflow tracking.
ms.service: microsoft-defender
author: mberdugo
ms.author: monaberdugo
ms.date: 2026-08-19T00:00:00.0000000Z
ms.collection:
- M365-security-compliance
- tier1
- usx-security
ms.topic: concept-article
ms.custom: sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: 0261d659-21f7-231b-01e7-5d3b840a0f76
document_version_independent_id: 0261d659-21f7-231b-01e7-5d3b840a0f76
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/siem-defender-case-management.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: siem-defender-case-management
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/siem-defender-case-management.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: bfa3327f-94f2-7d1c-a84e-0f15cdb0dc91
---

# Case management in the Microsoft Defender portal - Microsoft Defender XDR | Microsoft Learn

Microsoft Defender case management helps security operations teams manage SecOps work natively in the Microsoft Defender portal. A case is a security operations work item that brings together investigation context, collaboration, tasks, evidence, activity history, and workflow tracking so teams can manage work without leaving the Defender portal.

Case management supports the following case types:

- **Incident cases (Preview)**: Cases created from correlated incident activity to help analysts investigate, manage, and resolve security incidents.
- **Generic cases**: Cases created manually to track SecOps work, collaboration, tasks, and follow-up outside the incident response workflow.

Note

Incident cases are in preview and are the recommended experience for managing incidents in the Microsoft Defender portal. The legacy incident experience remains available during this preview.

![Screenshot showing the Cases page in the Microsoft Defender portal.](media/siem-defender-case-management/case-management-cases-page.png)

## What is case management?

Case management enables you to create and manage SecOps cases in the Defender portal. Cases help security operations teams standardize work, improve collaboration, track ownership, and maintain a record of decisions and actions.

Use cases to manage work such as:

- Investigating and responding to security incidents.
- Tracking general SecOps work.
- Coordinating analyst tasks and ownership.
- Documenting investigation notes, decisions, attachments, and activity history.
- Auditing and reporting on case changes and operational outcomes.

## Case management capabilities

Case management capabilities vary by case type, license, onboarding state, and preview scope.

Case management includes capabilities such as:

- View and manage cases on the **Cases** page.
- Filter, sort, search, export, and customize columns in the cases list.
- Manage case details, including status, priority, assignee, tags, description, and SLA policy.
- Add tasks to track ownership, due dates, priority, status, descriptions, and closing notes.
- Use comments and activity history to document investigation notes and audit case changes.
- Upload and review attachments.
- Review linked objects associated with a case, when available.
- Configure custom fields and SLA policies with case templates.
- Audit, retain, and report on case activity in Log Analytics with the `SecurityCaseEvent` table.
- Manage access to cases using RBAC.

Incident cases also include incident investigation context, such as attack story, alerts, assets, investigations, evidence, activities, and response actions.

Incident cases can also include agentic sessions. Analysts can run supported agentic playbooks from an incident case, track agent session status, and review session outputs from the case experience.

## Requirements

To use case management, your tenant must be onboarded to the Microsoft Defender portal. Cases are available only in the Defender portal and aren't available in the Microsoft Sentinel experience in the Azure portal.

Case management is available to eligible Microsoft Defender and Microsoft Sentinel customers. Requirements depend on the case management scenario, case type, license, and tenant configuration.

### ISOC case management

For [Integrated Security Operations Center (ISOC)](isoc-overview) customers, incident cases and generic cases don't require an ISOC workspace or a connected Microsoft Sentinel workspace.

### Microsoft Sentinel workspace-based case management

A connected Microsoft Sentinel workspace is required for case management scenarios that depend on Microsoft Sentinel workspace data, Sentinel-ingested data, or other Microsoft Sentinel workspace capabilities.

For Microsoft Sentinel customers, see [Connect Microsoft Sentinel to the Defender portal](/en-us/azure/sentinel/microsoft-sentinel-onboard).

Use [Microsoft Defender unified role-based access control (RBAC)](/en-us/defender-xdr/manage-rbac) or Microsoft Sentinel roles to grant access to case management features.

Permissions differ by case type and tenant configuration.

### Incident case permissions

Incident cases use the same permissions model as incidents in Microsoft Defender.

To work with incident cases, users need one of the following Microsoft Defender unified RBAC permissions:

| Permission | Access |
| --- | --- |
| **Security Data Read** | View incident cases. |
| **Security Data Manage** | View and manage incident cases. |

Incident case permissions and scoping follow the same permissions model as the legacy incident experience.

For more information, see [Microsoft Defender unified role-based access control (RBAC)](/en-us/defender-xdr/manage-rbac).

### Generic case permissions

| Generic case feature | Microsoft Defender unified RBAC | Microsoft Sentinel role |
| --- | --- | --- |
| View generic cases, case details, tasks, comments, and case audits | Security operations &gt; Security data basics (read) | Microsoft Sentinel Reader |
| Create and manage generic cases and case tasks, assign cases, and update case properties | Security operations &gt; Alerts (manage) | Microsoft Sentinel Responder |
| Configure case templates, custom fields, SLA policies, and case workflow settings | Authorization and settings &gt; Core security settings (manage) | Microsoft Sentinel Contributor |

## Manage cases

Use the **Cases** page in the Defender portal to view and manage cases. From the cases list, analysts can filter, sort, search, export, customize columns, and open cases for investigation or response work.

Case management varies by case type:

- For incident response workflows, see [Manage incident cases in the Microsoft Defender portal](manage-incident-cases).
- For general SecOps case workflows, see [Manage generic cases in the Microsoft Defender portal](manage-cases).

## Configure case templates

Use case templates to configure case management settings for supported case types. Case templates let admins configure custom fields and SLA policies.

Template capabilities vary by case type. For step-by-step guidance, see [Configure case templates in the Microsoft Defender portal](manage-case-templates).