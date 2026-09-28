---
layout: Conceptual
title: Investigate insider risk threats in the Microsoft Defender portal with insights from Microsoft Purview Insider Risk Management - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/irm-investigate-alerts-defender
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Investigate insider risk threats in the Microsoft Defender portal with insights from Microsoft Purview Insider Risk Management.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.topic: article
ms.date: 2025-02-17T00:00:00.0000000Z
locale: en-us
document_id: a70d52aa-e499-a98c-0e22-4d856b7061b4
document_version_independent_id: a70d52aa-e499-a98c-0e22-4d856b7061b4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/irm-investigate-alerts-defender.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: irm-investigate-alerts-defender
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/irm-investigate-alerts-defender.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/57eae111-0f3b-497e-be07-450fd1409dea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac8bf8ab-8134-4c9a-9f2e-58b31575b492
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: dfa1e0ac-48b2-18d5-5c4f-ced970d4b508
---

# Investigate insider risk threats in the Microsoft Defender portal with insights from Microsoft Purview Insider Risk Management - Microsoft Defender XDR | Microsoft Learn

Important

Some information in this article relates to a prereleased product, which may be substantially modified before it's commercially released. Microsoft makes no warranties expressed or implied, with respect to the information provided here.

[Microsoft Purview Insider Risk Management alerts](/en-us/purview/insider-risk-management-activities#alert-dashboard) in the Microsoft Defender portal are vital for protecting an organization's sensitive information and maintaining security. These alerts and insights from Microsoft Purview Insider Risk Management help identify and mitigate internal threats like data leaks and intellectual property theft by employees or contractors. Monitoring these alerts allows organizations to address security incidents proactively, ensuring sensitive data remains protected and compliance requirements are met.

One key benefit of monitoring insider risk alerts is the unified view of all alerts related to a user, allowing security operations center (SOC) analysts to correlate alerts from [Microsoft Purview Insider Risk Management](/en-us/purview/insider-risk-management-solution-overview) with other Microsoft security solutions. Additionally, having these alerts in the Microsoft Defender portal enables seamless integration with advanced hunting capabilities, enhancing the ability to investigate and respond to incidents effectively.

Another advantage is the automatic synchronization of alert updates between [Microsoft Purview](/en-us/purview/purview-portal) and the Defender portals, ensuring real-time visibility and reducing the chances of oversight. This integration strengthens an organization's ability to detect, investigate, and respond to insider threats, thereby enhancing overall security posture.

You can manage insider risk management alerts in the Microsoft Defender portal by navigating to **Incidents & alerts**, where you can:

- View all insider risk alerts grouped under incidents in the Microsoft Defender portal [incident queue](incident-queue#incident-queue).
- View insider risk alerts correlated with other Microsoft solutions, like [Microsoft Purview Data Loss Prevention](/en-us/purview/dlp-learn-about-dlp) and [Microsoft Entra ID](/en-us/entra/fundamentals/whatis), under a single incident.
- View individual insider risk alerts in the [alert queue](investigate-alerts).
- Filter by service source on the incident and alert queues.
- Hunt for all activities and all alerts related to the user in the insider risk alert.
- View a user's insider risk activity summary and risk level in the user entity page.

## Know before you begin

If you're new to Microsoft Purview and insider risk management, consider reading the following articles:

- [Learn about Microsoft Purview](/en-us/purview/purview)
- [Learn about Microsoft Purview Insider Risk Management](/en-us/purview/insider-risk-management)
- [Microsoft Purview data security solutions](/en-us/purview/purview-security)

## Prerequisites

To investigate insider risk management alerts in the Microsoft Defender portal, you need to do the following:

- Confirm your Microsoft 365 subscription supports insider risk management access. Know more about [subscription and licensing](/en-us/purview/insider-risk-management-configure#subscriptions-and-licensing).
- Confirm your access to Microsoft Defender XDR. See [Microsoft Defender XDR licensing requirements](prerequisites#licensing-requirements).

Data sharing with other security solutions must be turned on in the **Data sharing** settings in Microsoft Purview Insider Risk Management. Turning on **Share user risk details with other security solutions** in the Microsoft Purview portal enables users with the correct permissions to review user risk details in the user entity pages in the Microsoft Defender portal.

See [Share alert severity levels with other Microsoft security solutions](/en-us/purview/insider-risk-management-settings-dlp-sync#share-alert-severity-levels-with-other-microsoft-security-solutions) for more information.

![Highlighting the setting in the Microsoft Purview portal required for insider risk alerts to show in Defender XDR.](media/irm-investigate-alerts-defender/irm-toggle-settings-small.png)

## Permissions and roles

### Microsoft Defender XDR roles

The following permissions are essential to access insider risk management alerts in the Microsoft Defender portal:

- Security Operator
- Security Reader

For more information about Microsoft Defender XDR roles, see [Manage access to Microsoft Defender XDR with Microsoft Entra global roles](m365d-permissions).

### Microsoft Purview Insider Risk Management roles

You must also be a member of one of the following insider risk management role groups to view and manage insider risk management alerts in the Microsoft Defender portal:

- Insider Risk Management
- Insider Risk Management Analysts
- Insider Risk Management Investigators

For more information on these role groups, see [Enable permissions for insider risk management](/en-us/purview/insider-risk-management-configure#step-1-required-enable-permissions-for-insider-risk-management).

### Microsoft Graph API roles

Customers integrating insider risk management alerts with other security information and events management (SIEM) tools using the Microsoft Graph security API must have the following permissions to successfully access the relevant Microsoft Defender data through APIs:

| App permissions | Incidents | Alerts | Behaviors & events | Advanced hunting |
| --- | --- | --- | --- | --- |
| SecurityIncident.Read.All | Read | Read | Read |  |
| SecurityIncident.ReadWrite.All | Read/Write | Read/Write | Read |  |
| SecurityIAlert.Read.All |  | Read | Read |  |
| SecurityAlert.ReadWrite.All |  | Read/Write | Read |  |
| SecurityEvents.Read.All |  |  | Read |  |
| SecurityEvents.ReadWrite.All |  |  | Read |  |
| ThreatHunting.Read.All |  |  |  | Read |

More information about integrating data using the Microsoft Graph security API in Integrate insider risk management data with Microsoft Graph security API.

## Investigation experience in the Microsoft Defender portal

### Incidents

Insider risk management alerts related to a user are correlated to a single incident to ensure a holistic approach to incident response. This correlation allows SOC analysts to have a unified view of all alerts about a user coming from Microsoft Purview Insider Risk Management and various Defender products. Unifying all alerts also allows SOC analysts to view the details of devices involved in the alerts.

[![Sample of an incident with insider risk alerts from Microsoft Purview Insider Risk Management.](media/irm-investigate-alerts-defender/xdr-irm-incident-small.png)](media/irm-investigate-alerts-defender/xdr-irm-incident.png#lightbox)

You can filter incidents by choosing Microsoft Purview Insider Risk Management under **Service source**.

### Alerts

All insider risk management alerts are also visible in the Microsoft Defender portal's alert queue. Filter these alerts by choosing Microsoft Purview Insider Risk Management under **Service source**.

Here's an example of an insider risk management alert in the Microsoft Defender portal:

[![Sample of an insider risk alerts from Microsoft Purview Insider Risk Management.](media/irm-investigate-alerts-defender/xdr-irm-alert-small.png)](media/irm-investigate-alerts-defender/xdr-irm-alert.png#lightbox)

Microsoft Defender XDR and Microsoft Purview Insider Risk Management follow different alert status and classification frameworks. The following alert mapping is used to sync alert statuses between the two solutions:

| Microsoft Defender alert status | Microsoft Purview Insider Risk Management alert status |
| --- | --- |
| New | Needs review |
| In progress | Needs review |
| Resolved | Classification dependent. If classification is not available, the alert status is set to *Dismissed* by default. |

The following alert classification mapping is used to sync the alert classification between the two solutions:

| Microsoft Defender alert classification | Microsoft Purview Insider Risk Management alert classification |
| --- | --- |
| True positive  Includes multi-staged attack, phishing, etc. | Confirmed |
| Information, expected activity (benign positive)  Includes security testing, confirmed activity, etc. | Dismissed |
| False positive  Includes not malicious, not enough data to validate, etc. | Dismissed |

For more information about alert statuses and classifications in Microsoft Defender XDR, see [Manage alerts in Microsoft Defender](investigate-alerts#manage-alerts).

Any updates made to an insider risk management alert in the Microsoft Purview or the Microsoft Defender portals are automatically reflected in both portals. These updates might include:

- Alert status
- Severity
- Activity that generated the alert
- Trigger information
- Classification

The updates are reflected in both portals within 30 minutes of the alert generation or update.

Note

Alerts created from custom detections or link query results to incidents are not available in the Microsoft Purview portal.

The following insider risk management data are not yet available in this integration:

- Exfiltration through email events
- Risky AI usage events
- Third-party cloud apps events
- Events that occurred before an alert was generated
- Exclusions to events defined by the administrator
- Insider risk management incidents don't contain alerts currently, impacting Microsoft Sentinel users. For more information, see Impact to Microsoft Sentinel users.

### Advanced hunting

Use advanced hunting to further investigate insider risk events and behaviors. Refer to the table below for a summary of insider risk management data available in advanced hunting.

| Table name | Description |
| --- | --- |
| [AlertInfo](advanced-hunting-alertinfo-table) | Insider risk management alerts are available as part the AlertInfo table, which contains information about alerts from various Microsoft security solutions. |
| [AlertEvidence](advanced-hunting-alertevidence-table) | Insider risk management alerts are available as part of the AlertEvidence table, which contains information about entities associated with alerts from various Microsoft security solutions. |
| [DataSecurityBehaviors](advanced-hunting-datasecuritybehaviors-table) | This table contains insights into potentially suspicious user behavior that violates the default or customer-defined policies in Microsoft Purview. |
| [DataSecurityEvents](advanced-hunting-datasecurityevents-table) | This table contains enriched events about user activities that violate the default or customer-defined policies in Microsoft Purview. |

In the example below, we use the **DataSecurityEvents** table to investigate potentially suspicious user behavior. In this case, the user uploaded a file to Google Drive, which can be viewed as suspicious behavior if a company doesn't support file uploads to Google Drive.

[![Advanced hunting page showing a query using the tables related to insider risk behaviors and events.](media/irm-investigate-alerts-defender/irm-adv-hunting-small.png)](media/irm-investigate-alerts-defender/irm-adv-hunting.png#lightbox)

To access insider risk data in advanced hunting, users must have the following Microsoft Purview Insider Risk Management roles:

- Insider Risk Management Analyst
- Insider Risk Management Investigator

## Integrate insider risk management data with Microsoft Graph security API

Use the [Microsoft Graph security API](/en-us/graph/api/resources/security-api-overview) to integrate insider risk management alerts, insights, and indicators with other SIEM tools like Microsoft Sentinel, ServiceNow, or Splunk. You can also use the security API to integrate insider risk management data to data lakes, ticketing systems, and the like.

To learn how to set up the Microsoft Graph API, see [Use the Microsoft Graph API](/en-us/graph/use-the-api).

Refer to the table below to find insider risk management data in specific APIs.

| Table name | Description | Mode |
| --- | --- | --- |
| [Incidents](/en-us/graph/api/resources/security-incident) | Includes all insider risk incidents in the Defender XDR unified incident queue | Read/Write |
| [Alerts](/en-us/graph/api/resources/security-alert) | Includes all insider risk alerts shared with Defender XDR unified alert queue | Read/Write |
| [Advanced hunting](/en-us/graph/api/security-security-runhuntingquery) | Includes all insider risk management data in advanced hunting including Alerts, Behaviors, and Events | Read |

The insider risk alert metadata is part of the alert resource type in Microsoft Graph security API. See the complete information in [alert resource type](/en-us/graph/api/resources/security-alert).

Note

Insider risk alert information can be accessed in both the Alerts and Advanced hunting graph namespace. The alerts namespace provides more metadata.

Insider risk behaviors and events in advanced hunting can be accessed in the Graph API by [passing KQL queries in the API](/en-us/graph/api/security-security-runhuntingquery). Use this method to pull supporting data for specific alerts or investigations.

For customers using [Office 365 Management Activity API](/en-us/office/office-365-management-api/office-365-management-activity-api-reference), we recommend migrating to Microsoft Security Graph API to ensure richer metadata and bi-directional support for IRM data.

## Impact to Microsoft Sentinel users

We recommend Microsoft Sentinel customers to use the [Microsoft Purview Insider Risk Management – Microsoft Sentinel data connector](/en-us/azure/sentinel/connect-services-api-based) to get insider risk management alerts in Microsoft Sentinel.

If you are using automation on Microsoft Sentinel incidents, note that automation risks failure due to insider risk management incidents having no alert content. To mitigate this, [turn off data sharing in insider risk management settings](/en-us/purview/insider-risk-management-settings-share-data#use-the-apis-to-review-insider-risk-alert-information).