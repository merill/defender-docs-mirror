---
layout: Conceptual
title: Manually create an incident or alert in the Microsoft Defender portal (Legacy) - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/manually-create-incident
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
ms.reviewer: isco
description: Learn how to manually create incidents and alerts on demand in the Microsoft Defender portal for investigation and operational workflows.
ms.author: monaberdugo
author: mberdugo
ms.service: defender-xdr
f1.keywords:
- NOCSH
ms.collection:
- m365-security
- usx-security
- tier1
ms.topic: how-to
ai-usage: ai-assisted
ms.date: 2026-07-02T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 249e41b3-61e4-a8b0-cc74-afec78120c86
document_version_independent_id: 249e41b3-61e4-a8b0-cc74-afec78120c86
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/manually-create-incident.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: manually-create-incident
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/manually-create-incident.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: fd147b9b-15ee-5182-180b-1e99cdef38e4
---

# Manually create an incident or alert in the Microsoft Defender portal (Legacy) - Microsoft Defender XDR | Microsoft Learn

Important

This feature is in preview. Preview features aren't meant for production use and might have restricted functionality. These features are available before an official release so that customers can get early access and provide feedback.

Note

This article describes the legacy incident experience in the Microsoft Defender portal. Incident cases are in preview and are the recommended experience for managing incidents. The legacy incident experience remains available during this preview. To learn about the recommended incident case experience, see [Manage incident cases in the Microsoft Defender portal](manage-incident-cases).

Manual incident and alert creation lets your security operations center (SOC) team create incidents and alerts as needed in the [Microsoft Defender portal](https://security.microsoft.com). Use it to track investigations, tips from other teams, or operational work in the unified incident queue, even if no automatic detection has triggered.

This article describes how to manually create an incident or alert from the Defender portal. After you create an incident, [manage the incident](manage-incidents) like any other incident in the queue.

## What you can do with manual creation

Manual creation supports the following capabilities:

- Create a new incident with an initial alert, or attach an alert to an existing incident.
- Provide full incident metadata, including title, description, severity, category, MITRE ATT&CK techniques, impacted assets, and evidence.
- Decide whether the incident participates in correlation, or keep it standalone.
- Send incident and alert data through the same portal pages, advanced hunting tables, and APIs as automatically generated incidents, so your existing IT service management (ITSM) and reporting integrations can use it.

## Prerequisites

Before you can create an incident or alert manually, make sure that:

- Your tenant is onboarded to Microsoft Defender.
- You have one of the following Microsoft Defender unified role-based access control (RBAC) roles or equivalent permissions:
    - [**Detection tuning – Manage**](custom-permissions-details#authorization-and-settings)
    - [**Microsoft Sentinel Responder**](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-responder) (for Microsoft Sentinel customers)
    - [**Microsoft Sentinel Contributor**](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-contributor) (for Microsoft Sentinel customers)
- You can only create alerts for assets that are in your assigned RBAC scope. Assets outside of your scope aren't available in the impacted assets picker.

For more information about roles, see [Microsoft Defender Unified role-based access control (RBAC)](manage-rbac).

## Create an incident or alert from the portal

Manually create an incident or alert from the **Incidents** queue in the [Microsoft Defender portal](https://security.microsoft.com).

### Step 1: Create the incident or alert

1. In the Microsoft Defender portal, go to **Investigation & response** &gt; **Incidents & alerts**.
2. Select the **Incidents** tab or **Alerts** tab, depending on what you want to create.
3. On the queue toolbar, select **Create**.

    [![Screenshot of the Create button on the Incidents queue toolbar in the Microsoft Defender portal.](media/manually-create-incident/incidents-queue-create-button.png)](media/manually-create-incident/incidents-queue-create-button.png#lightbox)

    The **Create new** wizard opens.

### Step 2: Select workspace (Microsoft Sentinel only)

In the **Preparation** step, Microsoft Sentinel customers select the workspace scope for this incident. If you don't see the workspace you want, you can add it by selecting **Add workspace**.

[![Screenshot of the Preparation step of the Create new wizard in the Microsoft Defender portal, showing the workspace selection dropdown.](media/manually-create-incident/preparation.png)](media/manually-create-incident/preparation.png#lightbox)

### Step 3: Provide alert details

On the **Alert details** step, choose whether to create a new incident or to attach the alert to an existing one, set the correlation behavior, and enter the alert metadata.

[![Screenshot of the Alert details step of the Create new wizard in the Microsoft Defender portal.](media/manually-create-incident/alert-details-step.png)](media/manually-create-incident/alert-details-step.png#lightbox)

| Field | Required | Notes |
| --- | --- | --- |
| Create a new incident or correlate alert with an existing incident | Yes | Select **Create a new incident** to open a new incident. Select **Correlate alert with an existing incident** and provide the incident ID to attach the alert to that incident. |
| Enable incident correlation for this alert | No | When selected, the incident participates in standard Defender correlation logic and might merge with related incidents. Clear the checkbox to keep the incident standalone. |
| Alert title | Yes | Short, descriptive name for the alert. |
| Severity | Yes | High, medium, low, or informational. |
| Category | Yes | Maps to the Defender alert category taxonomy. |
| MITRE ATT&CK techniques | No | One or more technique IDs that describe the activity. |
| Description | Yes | Explanation of what the alert represents. For new incidents, the description of the first attached alert becomes the default incident description. |
| Recommended actions | No | Free-text guidance for responders. |
| Sentinel workspace | Yes (Microsoft Sentinel customers only) | The Microsoft Sentinel workspace that receives the alert and incident. |

Note

Manually created alerts are tagged with **Service source: Microsoft Defender XDR**, **Detection source: Manual**, and **Product name: Microsoft Defender XDR**, so you can filter for them in the alert queue and in advanced hunting.

Select **Next** to continue.

### Step 4: Select entities

On the **Select entities** step, attach the assets and evidence the alert applies to.

[![Screenshot of the Select entities step of the Create new wizard, with the impacted assets picker open.](media/manually-create-incident/select-entities-step.png)](media/manually-create-incident/select-entities-step.png#lightbox)

- **Impacted assets** (required): Add at least one asset. Use search and autocomplete to find devices, identities, mailboxes, IP addresses, or other supported entity types by name or unique identifier. Impacted assets are prioritized for incident context.
- **Related evidence** (optional): Add files, processes, URLs, IP addresses, or other supporting evidence.

You can only add assets that are within your RBAC scope.

Select **Next** to continue.

### Step 5: Link the alert to a related incident

On the **Related incident** step, select whether to create a new incident or correlate the alert with an existing incident. If you choose to correlate with an existing incident, provide the incident ID.

[![Screenshot of the Related incident step of the Create new wizard, showing the option to correlate with an existing incident and the incident ID input field.](media/manually-create-incident/related-incident.png)](media/manually-create-incident/related-incident.png#lightbox)

Select **Next** to continue.

### Step 6: Review and create

On the **Review and create** step, review the alert and incident details, and then select **Create**.

After you create the incident, the wizard confirms creation and provides links to the new incident and alert.

After the incident is created, you can set the owner and tag fields from the [Manage incident](manage-incidents) pane.

## Where manually created incidents and alerts appear

After creation, manually generated content flows through the same surfaces as automatically generated content:

- **Incident and alert queues** in the Microsoft Defender portal, including incident details, the alert page, and the activity log.
- **Entity pages** for the impacted assets and any related evidence.
- **Advanced hunting** tables, including [`AlertInfo`](advanced-hunting-alertinfo-table), [`AlertEvidence`](advanced-hunting-alertevidence-table), `SecurityAlert`, and `SecurityIncident`.
- **APIs**, including the Microsoft Graph security incidents and alerts APIs and Azure Resource Manager (ARM) APIs that your ITSM and reporting integrations use.

All create and update actions on a manually generated incident appear in the incident **Activity log**, the alert comments and history, and the Microsoft 365 audit log, so you can audit who did what and when.