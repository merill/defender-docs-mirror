---
layout: Conceptual
title: Microsoft Defender XDR in the Microsoft Defender portal - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/microsoft-365-defender-portal
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about Microsoft Defender XDR and how other services complement in the Microsoft Defender portal.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
- essentials-manage
- usx-security
ms.custom:
- admindeeplinkDEFENDER
- intro-overview
ms.topic: article
ms.date: 2025-10-31T00:00:00.0000000Z
locale: en-us
document_id: f6421ed5-4817-6795-43f6-04ad4c6f8ab2
document_version_independent_id: f6421ed5-4817-6795-43f6-04ad4c6f8ab2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/microsoft-365-defender-portal.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: microsoft-365-defender-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/microsoft-365-defender-portal.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 1b22076d-8446-99e0-2810-86e51bc4e443
---

# Microsoft Defender XDR in the Microsoft Defender portal - Microsoft Defender XDR | Microsoft Learn

The Microsoft Defender portal at https://security.microsoft.com combines protection, detection, investigation, and response to threats across your entire organization and all its components, in a central place. The Defender portal emphasizes quick access to information, simpler layouts, and bringing related information together for easier use. It includes Microsoft Defender XDR and features and capabilities of other Microsoft security solutions that you have provisioned access to.

To learn more about the services that are part of the Microsoft Defender portal, see the following resources:

- **[Microsoft Defender for Endpoint in the Microsoft Defender portal](microsoft-365-security-center-mde)**
- **[Microsoft Defender for Office 365 in the Microsoft Defender portal](microsoft-365-security-center-mdo)**
- **[Microsoft Defender for Identity in the Microsoft Defender portal](/en-us/defender-for-identity/microsoft-365-security-center-mdi)**
- **[Microsoft Defender for Cloud Apps in the Microsoft Defender portal](/en-us/defender-cloud-apps/microsoft-365-security-center-defender-cloud-apps)**
- **[Microsoft Defender for Cloud integration with Microsoft Defender](/en-us/azure/defender-for-cloud/concept-integration-365)**
- **[Microsoft Purview Data Loss Prevention alerts in the Microsoft Defender portal](dlp-investigate-alerts-defender)**
- **[Microsoft Defender Vulnerability Management in the Microsoft Defender portal](/en-us/defender-vulnerability-management/defender-vulnerability-management)**
- **[Microsoft Security Copilot embedded experience in the Microsoft Defender portal](security-copilot-in-microsoft-365-defender)**
- **[Microsoft Defender for IoT enterprise monitoring in the Microsoft Defender portal](/en-us/azure/defender-for-iot/organizations/eiot-defender-for-endpoint)**
- **[Microsoft Sentinel in the Microsoft Defender portal](/en-us/azure/sentinel/microsoft-sentinel-defender-portal)**
- **[Microsoft Purview Insider Risk Management alerts in the Microsoft Defender portal](irm-investigate-alerts-defender)**

Important

Microsoft Sentinel is generally available in the Microsoft Defender portal, with or without Microsoft Defender XDR or an E5 license. For more information, see [Microsoft Sentinel in the Microsoft Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2263690).

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal.

If you're currently using Microsoft Sentinel in the Azure portal, we recommend that you start planning your transition to the Defender portal now to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview). For more information, see [Transition your Microsoft Sentinel environment to the Defender portal](/en-us/azure/sentinel/move-to-defender) and [Planning your move to Microsoft Defender portal for all Microsoft Sentinel customers](https://techcommunity.microsoft.com/blog/microsoft-security-blog/planning-your-move-to-microsoft-defender-portal-for-all-microsoft-sentinel-custo/4428613) (blog).

Watch this short video to learn about the Defender portal.

## What to expect

Microsoft Defender correlates signals from various Microsoft security solutions in the Microsoft Defender portal to help security teams investigate and respond to attacks into a set of unified experiences for:

- Incidents & alerts
- Hunting
- Actions & submissions
- Threat analytics

The Microsoft Defender portal emphasizes *unity, clarity, and common goals*. Searching for entities and notifications are also unified in the portal.

Note

In the Microsoft Defender portal, customers see only the security features their subscription includes. For example, if you have Defender for Office 365 but not Defender for Endpoint, you see features and capabilities for Defender for Office 365, but not for device protection.

## Incident and alert investigations

Microsoft Defender [correlates alerts and events](alerts-incidents-correlation) from all Microsoft security solutions across all assets in your entire organization into incidents. **Incidents** are a collection of alerts that are related to a single threat or attack. Incidents are prioritized based on the severity of the threat and the potential impact on your organization.

[![The Incidents page in the Microsoft Defender portal.](media/incidents-ss-incidents.png)](media/incidents-ss-incidents.png#lightbox)

Selecting an incident name displays a page that demonstrates the value of centralizing security information as you get better insights into the full extend of a threat, from email, to identity, to endpoints.

[![Screenshot that shows the attack story page for an incident in the Microsoft Defender portal.](media/microsoft-365-defender-portal/incidents-ss-incident-summary.png)](media/microsoft-365-defender-portal/incidents-ss-incident-summary.png#lightbox)

Take the time to review the incidents in your environment, drill down into each alert, and practice building an understanding of how to access the information and determine next steps in your analysis.

For more information, see [Incidents in the Microsoft Defender portal](incidents-overview).

## Hunting

You can build custom detection rules and hunt for specific threats in your environment. **Hunting** uses a query-based threat hunting tool that lets you proactively inspect events in your organization to locate threat indicators and entities. These rules run automatically to check for, and then respond to, suspected breach activity, misconfigured machines, and other findings.

For more information, see [Proactively hunt for threats with advanced hunting in Microsoft Defender](advanced-hunting-overview).

## Actions and submissions

**Actions** are tasks performed on entities in the Microsoft Defender portal. Actions can be performed on an asset like a device or user, can be performed on a single entity or on multiple entities at once, and be performed manually or automatically.

Automated actions are capabilities within Microsoft Defender that help you address alerts and incidents automatically and speedily respond to attacks. Automated actions include:

- [Automated investigation and response](m365d-autoir)
- [Attack disruption](automatic-attack-disruption)

These actions can be reviewed and managed in the [**Action Center**](m365d-action-center) page in the Microsoft Defender portal.

You can submit files, email and email attachments, URLs, or Teams messages in the **Submissions** page to Microsoft for further analysis. For more information, see the [Submission guide](/en-us/defender-xdr/submission-guide).

## Threat analytics

[**Threat analytics**](threat-analytics) is the Microsoft Defender threat intelligence solution from expert Microsoft security researchers. It's designed to assist security teams to be as efficient as possible while facing emerging threats like:

- Active threat actors and their campaigns
- Popular and new attack techniques
- Critical vulnerabilities
- Common attack surfaces
- Prevalent malware

## Microsoft Defender settings

You can manage settings for Microsoft Defender in the **Settings &gt; Microsoft Defender XDR** page in the Microsoft Defender portal. The settings page is where you can configure the following:

- Email notifications for [incidents](m365d-notifications-incidents), [response actions](m365d-response-actions-notifications), and [threat analytics reports](m365d-threat-analytics-notifications).
- [Permissions and roles](m365d-permissions)
- [Streaming API](streaming-api)
- [Asset rule management](configure-asset-rules)
- [Alert tuning](investigate-alerts#tune-an-alert)
- Critical asset management

## Unified search and notifications

### Global search

The Microsoft Defender portal's search function is located at the top of the page. As you type, suggestions are provided so that it's easier to find entities. The enhanced search results page centralizes the results from all entities.

[![Screenshot of the search bar in the Microsoft Defender portal.](/en-us/defender-xdr/media/microsoft-365-defender-portal/search-panel.png)](/en-us/defender-xdr/media/microsoft-365-defender-portal/search-panel.png#lightbox)

Search results are categorized by sections related to your search terms. You can search across the following entities in the Microsoft Defender portal:

- **Devices** - supported for Defender for Endpoint, Defender for Identity, Defender for Cloud, and Microsoft Sentinel.
- **Users** - supported for Defender for Endpoint, Defender for Identity, Defender for Cloud Apps, and Microsoft Sentinel.
- **Files, IPs, and URLs** - same capabilities as in Defender for Endpoint. 
    Note

    IP and URL searches are based on exact match and don't appear in the search results page – they lead directly to the entity page.
- **Microsoft Defender Vulnerability Management** - same capabilities as in Defender for Endpoint (vulnerabilities, software, and recommendations).

Search also provides results from relevant links in the Microsoft Tech Community portal, relevant documentation in Microsoft Learn, navigation items within the portal, and a link where you can provide feedback. Search history is stored in your browser and is accessible for the next 30 days.

### Notifications

Notifications are messages that inform you about important events or updates in the Defender portal. They help you stay on top of your security tasks and alerts.

[![Screenshot of the notifications icon in the Microsoft Defender portal.](/en-us/defender-xdr/media/microsoft-365-defender-portal/notifications-panel.png)](/en-us/defender-xdr/media/microsoft-365-defender-portal/notifications-panel.png#lightbox)

Notifications are in the top bar of the portal's user interface. You can access them by clicking on the notification icon, which looks like a bell. A number on the icon indicates that you have that number of unread notifications.

Notifications can tell you about various types of events or updates:

- Success: when an action or task has been completed successfully like scanning a device or applying a policy.
- Ongoing: when an action is in progress.
- Information: when there is some information that you might find useful.
- Warning: when there is a potential issue or risk that you should be aware of like a device that is out of compliance or a policy that needs to be updated.
- Error: when there is an error or failure that requires your attention like an incident is deleted or merged, a scan that failed, or a policy that could not be applied.

Each notification has a title and content that provides relevant information about the event or update. Each notification also has a timestamp that shows when the notification was generated.

You can hide notifications from your view. You can dismiss a single notification by clicking on the *x* icon on the right side of the notification. You can also dismiss all notifications in the list with a single click by using *dismiss all* at the top of the notification panel.

Dismissing a notification does not delete it from the portal. You can always view your dismissed notifications by selecting *show dismissed* at the bottom of the notification panel.

Notifications are sorted by their generated time in the notification panel, with the most recent ones displayed first. You can scroll through the list of notifications to see older ones.

## Training for security analysts

With this learning path from Microsoft Learn, you can understand Microsoft Defender and how it can help identify, control, and remediate security threats.

| Training: | Mitigate threats using Microsoft Defender XDR |
| --- | --- |
| ![Microsoft Defender XDR training icon.](media/microsoft-365-defender-portal/m365-defender-secure-organization.png) | Analyze threat data across domains and rapidly remediate threats with built-in orchestration and automation in Microsoft Defender XDR. This learning path aligns with exam SC-200: Microsoft Security Operations Analyst.<br> 9 hr 31 min - Learning Path - 11 Modules |