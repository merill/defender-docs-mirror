---
layout: Conceptual
title: Automation with ISOC in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/siem-defender-automation
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about automation rules, playbooks, Playbook Generator, integration profiles, and enhanced alert triggers with ISOC in Microsoft Defender.
ms.service: microsoft-defender
author: guywi-ms
ms.author: guywild
ms.date: 2026-07-15T00:00:00.0000000Z
ms.collection:
- M365-security-compliance
- tier1
- usx-security
ms.topic: concept-article
ms.custom: sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: a7b1d576-e978-38e3-2f56-eb6e47fe87c8
document_version_independent_id: a7b1d576-e978-38e3-2f56-eb6e47fe87c8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/siem-defender-automation.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: siem-defender-automation
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/siem-defender-automation.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
platformId: 6d148d3d-78df-ce60-c1be-e78a8e612d5a
---

# Automation with ISOC in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn

Use automation with Integrated Security Operations Center (ISOC) in Microsoft Defender to streamline security operations workflows and automate response actions.

Automation includes automation rules, Logic Apps-based playbooks, Playbook Generator, integration profiles, and enhanced alert trigger support.

This article describes the automation capabilities available with [ISOC](isoc-overview), the requirements that apply, and the current limitations.

Note

This feature is in preview. Capabilities and availability might change during the preview period.

[![Screenshot showing the Automation page with integration profiles, automation rules, playbooks, and the AI-generated playbooks banner.](media/siem-defender-automation/automation-ai-generated-playbooks.png)](media/siem-defender-automation/automation-ai-generated-playbooks.png#lightbox)

## Automation capabilities

Automation with ISOC helps security teams reduce repetitive work, standardize response actions, and automate supported alert and incident workflows.

| Capability | Description |
| --- | --- |
| Automation rules | Trigger automated actions for supported alert and incident workflows. |
| Logic Apps-based playbooks | Run response workflows built with Azure Logic Apps. |
| Playbook Generator | Create generated playbooks from natural language in the Defender portal. |
| Integration profiles | Configure Microsoft and third-party API connections used by generated playbooks. |
| Enhanced alert trigger | Trigger generated playbooks from supported alert conditions across the Defender portal experience. |

## Automation rules

Automation rules define when automation runs and which actions are taken. Use automation rules to run playbooks, update alert or incident properties, or apply standardized response logic.

## Playbooks and Playbook Generator

Playbooks automate response actions. Automation supports Logic Apps-based playbooks and generated playbooks in the Defender portal.

Playbook Generator creates playbooks from natural language. Describe the automation workflow you want, and the experience generates a code-based playbook that you can review, test, save, and activate.

Generated playbooks can use integration profiles to connect to Microsoft and third-party APIs. Configure the required integration profiles before you create or run playbooks that call external services.

## Workspace requirements

Workspace requirements depend on the automation scenario.

| Scenario | Workspace requirement |
| --- | --- |
| Automation on Microsoft data | A Microsoft Sentinel workspace isn't required. |
| Automation on third-party data ingested through Log Analytics | A [Microsoft Sentinel workspace](/en-us/azure/sentinel/quickstart-onboard) is required. |

## Roles and permissions

Automation in the Defender portal uses Unified RBAC.

The following permissions are available for automation:

| Permission | Access levels |
| --- | --- |
| **Automation Admin** | **Execution Low** / **Medium** / **High** |
| **Automation Rules** | **Read** / **Write** |
| **Automation Integration** | **Read** / **Write** |
| **Automation Playbooks** | **Read** / **Write** |

Make sure users have the permissions required for the automation actions they need to perform.

## Limitations

The following limitations apply to generated playbooks and enhanced alert trigger automation.

### Playbook limitations

Generated playbooks have the following limitations:

- Only Python is supported for playbook authoring.
- Generated playbooks currently support alerts and incident cases as input.
- A single user can edit only one playbook at a time.
- External libraries aren't currently supported.
- Users must manually review and validate generated code.
- You can create up to 100 playbooks per tenant.
- Each playbook can have up to 5,000 lines.
- Maximum runtime per playbook execution is 10 minutes.
- Maximum of 8M AI interaction tokens per day per tenant.
- Playbook nesting isn't supported. A playbook can't invoke another playbook.

### Integration profile limitations

Integration profiles have the following limitations:

- Microsoft Graph and Azure Resource Manager integration profiles must be configured before generated playbooks can use them.
- Custom integration profiles support OAuth2 Client Credentials, API Key, AWS Auth, User and Password, Bearer/JWT Authentication, and Hawk.
- The API URL and authentication method of a custom integration profile can't be changed after creation.
- You can configure up to 500 integration profiles per tenant.

### Enhanced alert trigger limitations

Enhanced alert trigger rules have the following limitations:

- Enhanced alert trigger rules don't support priority ordering.
- The available actions are limited to running generated playbooks and updating alerts.
- For automation on third-party data, you can select only Microsoft Sentinel workspaces where you have the required permissions.
- You can create up to 500 active automation rules per tenant.
- You can execute one action per rule.