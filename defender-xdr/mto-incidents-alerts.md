---
layout: Conceptual
title: View and manage incidents and alerts in Microsoft Defender multitenant management - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/mto-incidents-alerts
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: View, triage, and manage incidents and alerts across multiple tenants and Microsoft Sentinel workspaces in Microsoft Defender multitenant management.
ms.service: defender-xdr
author: guywi-ms
ms.author: guywild
ms.collection:
- m365-security
- highpri
- tier1
- usx-security
ms.topic: how-to
ms.date: 2026-08-04T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 8ac65841-1728-83fb-dc10-7ee713eb773c
document_version_independent_id: 8ac65841-1728-83fb-dc10-7ee713eb773c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/mto-incidents-alerts.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mto-incidents-alerts
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/mto-incidents-alerts.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: babe725f-7852-4e99-8525-c96024cd7998
---

# View and manage incidents and alerts in Microsoft Defender multitenant management - Microsoft Defender XDR | Microsoft Learn

Multitenant management in the Defender portal brings together data from multiple tenants and Microsoft Sentinel workspaces in one place. Security operations center (SOC) analysts can use it to quickly find and respond to threats across Microsoft Defender XDR and Microsoft Sentinel. You can triage incidents and alerts that span SIEM and XDR data for any tenant with a Microsoft Sentinel workspace onboarded to the Defender platform.

Note

The incident-management guidance in this article describes the legacy incident experience in Microsoft Defender multitenant management. Incident cases are in preview and are the recommended experience for managing incidents. The legacy incident experience remains available during preview. To view and manage incident cases and generic cases across tenants, see [View and manage cases across multiple tenants in the Microsoft Defender multitenant portal](mto-manage-cases).

This article shows you how to view, investigate, and manage incidents and alerts from multiple tenants and workspaces by using the **Incidents & alerts** pages.

## View and investigate incidents (legacy)

To view or investigate an incident:

1. Go to the [Incidents page](https://mto.security.microsoft.com/incidents) in Microsoft Defender multitenant management. The **Tenant name** and **Workspaces** columns show which tenant the incident originates from:

    [![Screenshot of the Microsoft Defender multitenant incidents page.](media/mto-incidents-alerts/mto-incidents.png)](media/mto-incidents-alerts/mto-incidents.png#lightbox)
2. Select the incident you want to view. A flyout opens with the incident details pane, where you can:

    - Select **Open incident page** to open the incident in a new tab for that tenant in the [Microsoft Defender portal](https://security.microsoft.com).
    - Select **Manage incident** to assign, tag, classify, or change the status of the incident.

To learn more, see [Investigate incidents in the Microsoft Defender portal (legacy)](/en-us/defender-xdr/investigate-incidents).

## Manage multiple incidents (legacy)

Note

Currently, you can only assign multiple incidents from same tenant.

To manage incidents across multiple tenants and workspaces:

1. Go to the [Incidents page](https://mto.security.microsoft.com/incidents) in Microsoft Defender multitenant management.
2. Choose the incidents you want to manage from the incidents list and select **Manage incidents**.

    [![Screenshot that highlights the manage incidents option on the incidents page in Microsoft Defender multitenant management.](media/mto-incidents-alerts/mto-manage-incidents.png)](media/mto-incidents-alerts/mto-manage-incidents.png#lightbox)

On the flyout pane, you can assign, tag, classify, or change the status of incidents across multiple tenants at once.

To learn more about incidents in the Microsoft Defender portal, see [Manage incidents](/en-us/defender-endpoint/manage-incidents).

## View and investigate alerts

To view or investigate an alert:

1. Go to the [Alerts page](https://mto.security.microsoft.com/alerts) in multitenant management and select the alert you want to view. A flyout panel opens with the alert details page:

    [![Screenshot of alert details page for an alert in Microsoft Defender multitenant management.](media/mto-incidents-alerts/mto-alerts-details.png)](media/mto-incidents-alerts/mto-alerts-details.png#lightbox)
2. From the alert details pane you can:

    - Select **Open alerts page**, **Move alert to another incident**, or **Tune alert** to open the alert in a new tab for that tenant in the [Microsoft Defender portal](https://security.microsoft.com).
    - Select **Manage alert** to assign, classify, or change the status of the alert.

To learn more, see [Investigate alerts](/en-us/defender-endpoint/investigate-alerts).

## Manage multiple alerts

To manage alerts across multiple tenants and workspaces:

1. Go to the [Alerts page](https://mto.security.microsoft.com/alerts) in Microsoft Defender multitenant management.
2. Choose the alerts you want to manage from the alerts list and select **Manage alerts**.

    [![Screenshot that highlights the manage alerts option for selected alerts in Microsoft Defender multitenant management.](media/mto-incidents-alerts/mto-manage-alerts.png)](media/mto-incidents-alerts/mto-manage-alerts.png#lightbox)

Use the **Manage alerts** pane to set the status, assign, classify, and add comments for multiple alerts at once. You can set status, classifications, and comments across tenants. However, you can only assign alerts from the same tenant.

For more information, see [Manage alerts](/en-us/defender-xdr/investigate-alerts#manage-alerts).

## Move alerts (legacy)

Move an alert to a different incident to help you better organize and correlate related security events. For example, you might find that multiple alerts are part of the same security breach, and want to include them all in the same incident. Grouping related alerts into the same incident ensures that all relevant information is grouped together, enabling more efficient investigation and response.

To move one or more alerts:

- On the **Alerts** page, select one or more alerts and then select **Move alerts**
- On an alert details pane or alert details page, select **Move alert to another incident**

In the **Move alert to another incident** pane, define whether you want to create a new incident, or use an existing incident. If you choose to use an existing incident, search for the incident by name or ID and add a reason for the change. In all cases, add a comment describing your change before you select **Save**.

For detailed guidance, see [Move alerts from one incident to another in the Microsoft Defender portal (legacy)](/en-us/defender-xdr/move-alert-to-another-incident).