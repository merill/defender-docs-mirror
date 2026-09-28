---
layout: Conceptual
title: Manage Security Incidents - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/incidents
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Triage and investigate security incidents with correlated alerts and analytics in Microsoft Defender for Cloud to understand attack campaigns and affected resources.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 57ccb4d2-0b8f-c862-b637-77539fe6e094
document_version_independent_id: 0cc09c1e-9f28-1948-c137-9732c70501e3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/incidents.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/incidents
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/incidents.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 374f46ce-1c06-d784-d198-a9434e96a86e
---

# Manage Security Incidents - Microsoft Defender for Cloud | Microsoft Learn

Triaging and investigating security alerts can take a lot of time, even for skilled security analysts. For many people, it can be hard to know where to start.

Defender for Cloud uses analytics to connect information between distinct security alerts. By using connections between related security alerts, Defender for Cloud provides a single view of an attack campaign and its related alerts. This view helps you understand attacker actions and affected resources. For more information, see [Security alerts in Defender for Cloud](alerts-overview) and [Manage and respond to security alerts](manage-respond-alerts).

This article provides an overview of incidents in Defender for Cloud.

## What is a security incident?

In Defender for Cloud, a security incident is an aggregation of all alerts for a resource that align with kill chain patterns. Incidents appear on the Security alerts page. Select an incident to view related alerts and get more information. For details about tactics, see [MITRE ATT&CK tactics](alerts-reference#mitre-attck-tactics).

## Manage security incidents

Perform the following steps to find and manage security incidents in Defender for Cloud:

1. On the Defender for Cloud security alerts page, use **Add filter** to filter by alert name for the alert name **Security incident detected on multiple resources**.

    ![Locating the incidents on the security alerts page in Microsoft Defender for Cloud.](media/incidents/locating-incidents.png)

    The list is now filtered to show only incidents. Security incidents have a different icon from security alerts.

    ![List of incidents on the security alerts page in Microsoft Defender for Cloud.](media/incidents/incidents-list.png)
2. To view details of an incident, select one from the list. A pane appears with more details about the incident.

    ![Screenshot of the side pane showing incident details such as severity, status, and related alerts in Microsoft Defender for Cloud.](media/incidents/incident-quick-peek.png)
3. To view more details, select **View full details**.

    [![Screenshot showing a security incident full details in Microsoft Defender for Cloud.](media/incidents/incident-details.png)](media/incidents/incident-details.png#lightbox)

    The left pane of the security incident page shows high-level information about the security incident, including title, severity, status, activity time, description, and the affected resource. Next to the affected resource, you can see the relevant Azure tags. Use the Azure tags shown next to the affected resource to infer the organizational context of the resource when investigating the alert.

    The right pane includes the **Alerts** tab with the security alerts that were correlated as part of this incident.

    Tip

    For more information about a specific alert, select it.

    [![Screenshot showing the take action tab for a security incident in Microsoft Defender for Cloud.](media/incidents/incident-take-action-tab.png)](media/incidents/incident-take-action-tab.png#lightbox)
4. To switch to the **Take action** tab, select the tab or select the **Take action** button at the bottom of the right pane. Use this tab to take further actions such as:

    - Mitigate the threat: provides manual remediation steps for this security incident.
    - Prevent future attacks: provides security recommendations to help reduce the attack surface, increase security posture, and prevent future attacks.
    - Trigger automated response: provides the option to trigger a Logic App as a response to this security incident.
    - Suppress similar alerts: provides the option to suppress future alerts with similar characteristics if the alert isn't relevant for your organization.

    Note

    A security alert can appear both as part of an incident and as a standalone alert.
5. To remediate the threats in the incident, follow the remediation steps provided with each alert.