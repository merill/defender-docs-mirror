---
layout: Conceptual
title: View MITRE ATT&CK Coverage in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/mitre-coverage
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
description: View your organization's MITRE ATT&CK coverage in Microsoft Sentinel. Identify active detections and available rules to strengthen security.
author: mberdugo
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.author: monaberdugo
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: cefd128c-7dd1-47c5-f15a-8957c2474b45
document_version_independent_id: c3e60370-41e3-38cf-f53e-9b0d4a8e7fd9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/mitre-coverage.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/mitre-coverage
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/mitre-coverage.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 056666f8-6c4e-9ae6-71f5-a91e8a5ba651
---

# View MITRE ATT&CK Coverage in Microsoft Sentinel | Microsoft Learn

[MITRE ATT&CK](https://attack.mitre.org/#) is a publicly accessible knowledge base of tactics and techniques commonly used by attackers. It's created and maintained based on real-world observations. Many organizations use the MITRE ATT&CK knowledge base to develop specific threat models and methodologies to verify security status in their environments.

Microsoft Sentinel analyzes ingested data, not only to [detect threats with built-in analytics](detect-threats-built-in) and help you [investigate incidents](investigate-cases), but also to visualize the nature and coverage of your organization's security status.

This article describes how to use the **MITRE** page in Microsoft Sentinel to view the analytics rules (detections) already active in your workspace and the detections available for you to configure. Use this page to understand your organization's security coverage based on the tactics and techniques from the MITRE ATT&CK framework.

Important

The MITRE page in Microsoft Sentinel is currently in *preview*. The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

## Prerequisites

Before you view the MITRE coverage for your organization in Microsoft Sentinel, ensure you have the following prerequisites:

- An active Microsoft Sentinel instance.
- Necessary permissions to view content in Microsoft Sentinel. For more information, see [Roles and permissions in Microsoft Sentinel](roles).
- Data connectors configured to ingest relevant security data into Microsoft Sentinel. For more information, see [Microsoft Sentinel data connectors](connect-data-sources).
- Active scheduled query rules and near real-time (NRT) rules set up in Microsoft Sentinel. For more information, see [Threat detection in Microsoft Sentinel](threat-detection).
- Familiarity with the MITRE ATT&CK framework and its tactics and techniques.

## MITRE ATT&CK framework version

Microsoft Sentinel is currently aligned to The MITRE ATT&CK framework, version 18.

## View current MITRE coverage

By default, both currently active scheduled query and near real-time (NRT) rules are indicated in the coverage matrix.

To view the current MITRE coverage for your organization:

1. Do one of the following, depending on the portal you're using:

# [Defender portal](#tab/defender-portal)
In the Defender portal, select **Microsoft Sentinel &gt; Threat management &gt; MITRE ATT&CK**.

[![Screenshot of the MITRE ATT&amp;CK page in the Defender portal.](media/mitre-coverage/mitre-coverage-defender.png)](media/mitre-coverage/mitre-coverage-defender.png#lightbox)

To filter the page by a specific threat scenario, toggle the **View MITRE by threat scenario** option on, and then select a threat scenario from the drop-down menu. The page updates to show MITRE coverage for the selected threat scenario. For example:

![Screenshot of the MITRE ATT&amp;CK page filtered by a specific threat scenario.](media/mitre-coverage/mitre-by-threat-scenario.png)

# [Azure portal](#tab/azure-portal)
In the Azure portal, under **Threat management**, select **MITRE ATT&CK (Preview)**.

[![Screenshot of the MITRE ATT&amp;CK coverage matrix in the Azure portal showing technique coverage levels.](media/mitre-coverage/mitre-coverage.png)](media/mitre-coverage/mitre-coverage.png#lightbox)

---
2. Use any of the following methods:

    - **Use the legend** to understand how many detections are currently active in your workspace for a specific technique.
    - **Use the search bar** to search for a specific technique in the matrix, using the technique name or ID, to view your organization's security status for the selected technique.
    - **Select a specific technique** in the matrix to view more details in the details pane. In the details pane, use the links to jump to any of the following locations:

        - In the **Description** area, select **View full technique details ...** for more information about the selected technique in the MITRE ATT&CK framework knowledge base.
        - Scroll down in the pane and select links to any of the active items to jump to the relevant area in Microsoft Sentinel.

        For example, select **Hunting queries** to jump to the **Hunting** page. On the **Hunting** page, you see a filtered list of the hunting queries that are associated with the selected technique, and available for you to configure in your workspace.

    On the Defender portal, the details pane also shows recommended coverage details, including the ratio of active detections and security services (products) out of all recommended detections and services for the selected technique.

## Simulate possible coverage with available detections

In the MITRE coverage matrix, *simulated* coverage refers to detections that are available but not currently configured in your Microsoft Sentinel workspace. View your simulated coverage to understand your organization's possible security status if you configured all available detections.

1. In Microsoft Sentinel, under **Threat management**, select **MITRE ATT&CK (Preview)**, and then select items in the **Simulated rules** menu to simulate your organization's possible security status.
2. Use the legend, search bar, and technique selection described in View current MITRE coverage to view the simulated coverage for a specific technique.

## Use the MITRE ATT&CK framework in analytics rules and incidents

Scheduled rules with MITRE techniques applied that run regularly in your Microsoft Sentinel workspace improve your organization's security status in the MITRE coverage matrix.

- **Analytics rules**:

    - When configuring analytics rules, select specific MITRE techniques to apply to your rule.
    - When searching for analytics rules, filter the rules displayed by technique to find your rules quicker.

        For more information, see [Detect threats out-of-the-box](detect-threats-built-in) and [Create custom analytics rules to detect threats](detect-threats-custom).
- **Incidents**:

    When incidents are created for alerts that are surfaced by rules with MITRE techniques configured, the techniques are also added to the incidents.

    For more information, see [Investigate incidents with Microsoft Sentinel](investigate-cases). If Microsoft Sentinel is onboarded to the Defender portal, then [investigate incidents in the Microsoft Defender portal](/en-us/defender-xdr/investigate-incidents) instead.
- **Threat hunting**:

    - When you're creating a new hunting query, select the specific tactics and techniques to apply to your query.
    - When searching for active hunting queries, filter the queries displayed by tactics by selecting an item from the list above the grid. Select a query to see tactic and technique details in the details pane on the side.
    - When you're creating bookmarks, either use the technique mapping inherited from the hunting query, or create your own mapping.

        For more information, see [Hunt for threats with Microsoft Sentinel](hunting) and [Keep track of data during hunting with Microsoft Sentinel](bookmarks).