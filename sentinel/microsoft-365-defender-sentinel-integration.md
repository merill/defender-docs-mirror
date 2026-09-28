---
layout: Conceptual
title: Microsoft Defender XDR integration with Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/microsoft-365-defender-sentinel-integration
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
description: Learn how using Microsoft Defender XDR together with Microsoft Sentinel lets you use Microsoft Sentinel as your universal incidents queue.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: concept-article
ms.date: 2026-06-17T00:00:00.0000000Z
ms.collection: usx-security
locale: en-us
document_id: ba38fd25-1d28-82db-a103-cf361c25e5a6
document_version_independent_id: ff01c550-74b2-4bea-b0cd-fa4dbec06fb1
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/microsoft-365-defender-sentinel-integration.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/microsoft-365-defender-sentinel-integration
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/microsoft-365-defender-sentinel-integration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 202f4676-5ab0-123a-318e-17e91d67e151
---

# Microsoft Defender XDR integration with Microsoft Sentinel | Microsoft Learn

This article describes how Microsoft Defender XDR services integrate with Microsoft Sentinel, whether in the Microsoft Defender portal or in the Azure portal.

- If you first onboarded to Microsoft Sentinel after July 1, 2025 with permissions of a subscription [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) or a [User access administrator](/en-us/azure/role-based-access-control/built-in-roles#user-access-administrator), your workspace is [automatically onboarded to the Defender portal](quickstart-onboard). In such cases, you [use Microsoft Sentinel in the Defender portal only](microsoft-sentinel-defender-portal), where your data can integrate directly with Defender XDR service data for [unified security operations](/en-us/defender-xdr/isoc-overview).
- If you're otherwise using the Azure portal in addition to or instead of the Defender portal, integrate Microsoft Defender XDR with Microsoft Sentinel. Integrating the services streams all Defender XDR incidents and advanced hunting events into Microsoft Sentinel, and keeps the incidents and events synchronized between the Azure and Microsoft Defender portals.

Incidents from Defender XDR include all associated alerts, entities, and relevant information, providing you with enough context to perform triage and preliminary investigation in Microsoft Sentinel. Once in Microsoft Sentinel, incidents remain bi-directionally synced with Defender XDR, allowing you to take advantage of the benefits of both portals in your incident investigation.

## Microsoft Sentinel and Defender XDR

Use one of the following methods to integrate Microsoft Sentinel with Microsoft Defender XDR services:

- Ingest Microsoft Defender XDR service data into Microsoft Sentinel and view Microsoft Sentinel data in the Azure portal. Enable the Defender XDR connector in Microsoft Sentinel.
- Integrate Microsoft Sentinel and Defender XDR directly in the Microsoft Defender portal. In this case, view Microsoft Sentinel data directly with the rest of your Defender incidents, alerts, vulnerabilities, and other security data. To do this, you must onboard Microsoft Sentinel to the Defender portal.

Select the appropriate tab to see what the Microsoft Sentinel integration with Defender XDR looks like depending on which integration method you use.

# [Defender portal](#tab/defender-portal)
The following illustration shows how Microsoft's XDR solution seamlessly integrates with Microsoft Sentinel in the Microsoft Defender portal.

[![Diagram of a Microsoft Sentinel and Microsoft Defender XDR architecture in the Microsoft Defender portal.](media/microsoft-365-defender-sentinel-integration/sentinel-xdr-usx.svg)](media/microsoft-365-defender-sentinel-integration/sentinel-xdr-usx.svg#lightbox)

In this diagram:

- Insights from signals across your entire organization feed into Microsoft Defender XDR and Microsoft Defender for Cloud.
- Microsoft Sentinel provides support for multicloud environments and integrates with third-party apps and partners.
- Microsoft Sentinel data is ingested together with your organization's data into the Microsoft Defender portal.
- SecOps teams can then analyze and respond to threats identified by Microsoft Sentinel and Microsoft Defender XDR in the Microsoft Defender portal.

# [Azure portal](#tab/azure-portal)
The following illustration shows how Microsoft's XDR solution seamlessly integrates with Microsoft Sentinel.

[![Diagram of the integration of Microsoft Sentinel and Microsoft XDR.](media/microsoft-365-defender-sentinel-integration/sentinel-xdr.svg)](media/microsoft-365-defender-sentinel-integration/sentinel-xdr.svg#lightbox)

In this diagram:

- Insights from signals across your entire organization feed into Microsoft Defender XDR and Microsoft Defender for Cloud.
- Microsoft Defender XDR and Microsoft Defender for Cloud send SIEM log data through Microsoft Sentinel connectors.
- SecOps teams can then analyze and respond to threats identified in Microsoft Sentinel and Microsoft Defender XDR.
- Microsoft Sentinel provides support for multicloud environments and integrates with third-party apps and partners.

---

## Incident correlation and alerts

With the integration of Defender XDR with Microsoft Sentinel, Defender XDR incidents are visible and manageable from within Microsoft Sentinel. This gives you a primary incident queue across the entire organization. See and correlate Defender XDR incidents together with incidents from all of your other cloud and on-premises systems. At the same time, this integration allows you to take advantage of the unique strengths and capabilities of Defender XDR for in-depth investigations and a Defender-specific experience across the Microsoft 365 ecosystem.

Defender XDR enriches and groups alerts from multiple Microsoft Defender products, both reducing the size of the SOC’s incident queue and shortening the time to resolve. Alerts from the following Microsoft Defender products and services are also included in the integration of Defender XDR to Microsoft Sentinel:

- [Microsoft Defender for Endpoint](/en-us/defender-endpoint/microsoft-defender-endpoint)
- [Microsoft Defender for Identity](/en-us/defender-for-identity/what-is)
- [Microsoft Defender for Office 365](/en-us/defender-office-365/mdo-about)
- [Microsoft Defender for Cloud Apps](/en-us/defender-cloud-apps/what-is-defender-for-cloud-apps)

Other services whose alerts are collected by Defender XDR include:

- [Microsoft Purview Data Loss Prevention](/en-us/microsoft-365/security/defender/investigate-dlp)
- [Microsoft Entra ID Protection](/en-us/defender-cloud-apps/aadip-integration)
- [Microsoft Purview Insider Risk Management](/en-us/defender-xdr/irm-investigate-alerts-defender)

## Data ingestion limitations

While most Defender XDR data streams to Microsoft Sentinel, some advanced hunting tables aren't ingested. Notably, **Defender Vulnerability Management (TVM) tables** such as `DeviceTvmSoftwareInventory` and `DeviceTvmSoftwareVulnerabilities` appear in the Microsoft Sentinel schema, but TVM data isn't ingested into Microsoft Sentinel workspaces. This means queries using these tables return results in Defender XDR Advanced Hunting but return no results in Microsoft Sentinel.

For a complete list of unsupported tables and guidance on custom ingestion solutions, see [Which Defender XDR tables aren't supported in Microsoft Sentinel](connect-microsoft-365-defender#which-defender-xdr-tables-arent-supported-in-microsoft-sentinel).

The Defender XDR connector also brings incidents from Microsoft Defender for Cloud. To synchronize alerts and entities from these incidents as well, you must enable the Defender for Cloud connector in Microsoft Sentinel. Otherwise, your Defender for Cloud incidents appear empty. For more information, see [Ingest Microsoft Defender for Cloud incidents with Microsoft Defender XDR integration](ingest-defender-for-cloud-incidents).

In addition to collecting alerts from these components and other services, Defender XDR generates alerts of its own. It creates incidents from all of these alerts and sends them to Microsoft Sentinel.

## Common use cases and scenarios

Consider integrating Defender XDR with Microsoft Sentinel for the following use cases and scenarios:

- Onboard Microsoft Sentinel to the Microsoft Defender portal.
- Enable one-click connect of Defender XDR incidents, including all alerts and entities from Defender XDR components, into Microsoft Sentinel.
- Allow bi-directional sync between Microsoft Sentinel and Defender XDR incidents on status, owner, and closing reason.
- Apply Defender XDR alert grouping and enrichment capabilities in Microsoft Sentinel, thus reducing time to resolve.
- Facilitate investigations across both portals with in-context deep links between a Microsoft Sentinel incident and its parallel Defender XDR incident.

For more information, see [Microsoft Sentinel in the Microsoft Defender portal](microsoft-sentinel-defender-portal).

## Connecting to Microsoft Defender XDR

How you integrate Defender XDR depends on whether you plan to onboard Microsoft Sentinel to the Defender portal or continue to work in the Azure portal.

### Defender portal integration

If you onboard Microsoft Sentinel to the Defender portal and are licensed for Defender XDR, Microsoft Sentinel is automatically connected to Defender XDR. The data connector for Defender XDR is automatically set up for you. Any data connectors for the alert providers included in the Defender XDR connector are disconnected. This includes the following data connectors:

- Microsoft Defender for Cloud Apps (alerts)
- Microsoft Defender for Endpoint
- Microsoft Defender for Identity
- Microsoft Defender for Office 365
- Microsoft Entra ID Protection

### Azure portal integration

If you want to sync Defender XDR data to Microsoft Sentinel in the Azure portal, you must enable the Microsoft Defender XDR connector in Microsoft Sentinel. When you enable the connector, it sends all Defender XDR incidents and alerts information to Microsoft Sentinel and keep the incidents synchronized.

- First, install the **Microsoft Defender XDR** solution for Microsoft Sentinel from the **Content hub**. Then, enable the **Microsoft Defender XDR** data connector to collect incidents and alerts. For more information, see [Connect data from Microsoft Defender XDR to Microsoft Sentinel](connect-microsoft-365-defender).
- After you enable alert and incident collection in the Defender XDR data connector, Defender XDR incidents appear in the Microsoft Sentinel incidents queue shortly after they're generated in Defender XDR. Under normal operating conditions, incidents generated in Defender XDR typically appear in the Microsoft Sentinel UI and API within five minutes. Ingestion into the `securityIncident` table might take a few more minutes. In these incidents, the **Alert product name** field contains **Microsoft Defender XDR** or one of the component Defender services' names.

### Ingestion costs

Alerts and incidents from Defender XDR, including items that populate the *SecurityAlert* and *SecurityIncident* tables, are ingested into and synchronized with Microsoft Sentinel at no charge. For all other data types from individual Defender components such as the *Advanced hunting* tables *DeviceInfo*, *DeviceFileEvents*, *EmailEvents*, and so on, ingestion is charged.

For more information, see [Plan costs and understand Microsoft Sentinel pricing and billing](billing).

### Data ingestion behavior

Alerts created by Defender XDR-integrated products are sent to Defender XDR and grouped into incidents. Both the alerts and the incidents flow to Microsoft Sentinel through the Defender XDR connector.

For the available options and more information, see:

- [Microsoft Defender for Cloud in the Microsoft Defender portal](/en-us/microsoft-365/security/defender/microsoft-365-security-center-defender-cloud)
- [Ingest Microsoft Defender for Cloud incidents with Microsoft Defender XDR integration](ingest-defender-for-cloud-incidents)

### Microsoft incident creation rules

To avoid creating *duplicate incidents for the same alerts*, the **Microsoft incident creation rules** setting is turned off for Defender XDR-integrated products when connecting Defender XDR. Defender XDR-integrated products include Microsoft Defender for Identity, Microsoft Defender for Office 365, and more. Also, Microsoft incident creation rules aren't supported in the Defender portal because the Defender portal has its own incident creation engine. This change has the following potential impacts:

- **Alert filtering**. Microsoft Sentinel's incident creation rules allowed you to filter the alerts that would be used to create incidents. With these rules disabled, preserve the alert filtering capability by configuring [alert tuning in the Microsoft Defender portal](/en-us/microsoft-365/security/defender/investigate-alerts), or by using [automation rules](automate-incident-handling-with-automation-rules#incident-suppression) to suppress or close incidents you don't want.
- **Incident titles**. With the Defender XDR connector enabled, you can no longer predetermine the titles of incidents. The Defender XDR correlation engine presides over incident creation and automatically names the incidents it creates. This change is liable to affect any automation rules you created that use the incident name as a condition. To avoid this pitfall, use criteria other than the incident name as conditions for [triggering automation rules](automate-incident-handling-with-automation-rules#conditions). We recommend using *tags*.
- **Scheduled analytics rules**. If you use Microsoft Sentinel's incident creation rules for other Microsoft security solutions or products not integrated into Defender XDR, such as Microsoft Purview Insider Risk Management, and you plan to onboard to the Defender portal, replace your incident creation rules with [scheduled analytics rules](scheduled-rules-overview).

If you want to preserve Sentinel-style incident creation behavior for XDR alerts while using the Defender portal, you can [migrate Microsoft Sentinel incident creation rules to alert grouping in Microsoft Defender](/en-us/azure/sentinel/migrate-sentinel-incident-creation-rules-alert-grouping).

## Working with Microsoft Defender XDR incidents in Microsoft Sentinel and bi-directional sync

Defender XDR incidents appear in the Microsoft Sentinel incidents queue with the product name **Microsoft Defender XDR**, and with similar details and functionality to any other Microsoft Sentinel incidents. Each incident contains a link back to the parallel incident in the Microsoft Defender portal.

As the incident evolves in Defender XDR, and more alerts or entities are added to it, the Microsoft Sentinel incident gets updated accordingly.

Changes made to certain fields or attributes of a Defender XDR incident, in either Defender XDR or Microsoft Sentinel, likewise update accordingly in the other's incidents queue. The synchronization takes place in both portals immediately after the change to the incident is applied, with no delay. A refresh might be required to see the latest changes.

The following fields are synchronized "as is" between incidents in the Defender portal and in Microsoft Sentinel in the Azure portal:

- Title
- Description
- ProductName
- Severity
- Custom tags
- AdditionalData
- Comments (new only)
- LastModifiedBy

The following fields are transformed during synchronization so that their values comply with the schema of each platform:

| Field | Value in the Defender portal | Value in Microsoft Sentinel |
| --- | --- | --- |
| **Status** |  |  |
|  | Active | New |
| **Classification/*Classification reason*** |  |  |
|  | True Positive/*any* | True Positive/*Suspicious activity* |
|  | False Positive/*any* | False Positive/*Inaccurate data* |
|  | N/A | False Positive/*Inaccurate alert logic* |
|  | Benign Positive/*Informational expected activity* | Benign Positive/*Suspicious but expected* |
|  | Not set | Undetermined |

In Defender XDR, all alerts from one incident can be transferred to another, resulting in the incidents being merged. When this merge happens, the Microsoft Sentinel incidents reflect the changes. One incident contains all the alerts from both original incidents, and the other incident is automatically closed, with a tag of "redirected" added.

Note

Incidents in Microsoft Sentinel can contain a maximum of 150 alerts. Defender XDR incidents can have more than this. If a Defender XDR incident with more than 150 alerts is synchronized to Microsoft Sentinel, the Microsoft Sentinel incident shows as having “150+” alerts and provides a link to the parallel incident in Defender XDR where you see the full set of alerts.

## Advanced hunting event collection

The Defender XDR connector also lets you stream **advanced hunting** events—a type of raw event data—from Defender XDR and its component services into Microsoft Sentinel. Collect [advanced hunting](/en-us/microsoft-365/security/defender/advanced-hunting-overview) events from all Defender XDR components, and stream them straight into purpose-built tables in your Microsoft Sentinel workspace. These tables are built on the same schema that is used in the Defender portal giving you complete access to the full set of advanced hunting events, and allowing for the following tasks:

- Easily copy your existing Microsoft Defender for Endpoint/Office 365/Identity/Cloud Apps advanced hunting queries into Microsoft Sentinel.
- Use the raw event logs to provide further insights for your alerts, hunting, and investigation, and correlate these events with events from other data sources in Microsoft Sentinel.
- Store the logs with increased retention, beyond the Defender XDR default retention of 30 days. You can do so by configuring the retention of your workspace or by configuring per-table retention in Log Analytics.

## Custom detection rules creation

[Custom detections](/en-us/defender-xdr/custom-detections-overview?toc=/azure/sentinel/TOC.json&amp;bc=/azure/sentinel/breadcrumb/toc.json) in Microsoft Defender is now the best way to create new rules across Microsoft Sentinel Security Information and Event Management (SIEM) and Microsoft Defender XDR. It supports a unified security operations center (SOC) experience in the Defender portal and provides greater opportunity for enhancements.

With custom detections, you can reduce ingestion costs, get unlimited real-time detections, and benefit from seamless integration with Defender XDR data, functions, and remediation actions with automatic entity mapping. Microsoft Sentinel users can still use [analytics rules](threat-detection), but we encourage that they use custom detections to take advantage of the latest innovations.