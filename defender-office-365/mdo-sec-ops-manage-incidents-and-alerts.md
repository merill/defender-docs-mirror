---
layout: Conceptual
title: Manage incidents and alerts from Defender for Office 365 in Microsoft Defender XDR - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/mdo-sec-ops-manage-incidents-and-alerts
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: concept-article
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.custom:
- sfi-image-nochange
description: SecOps personnel can learn how to use the Incidents queue in Microsoft Defender XDR to manage incidents in Microsoft Defender for Office 365.
ms.service: defender-office-365
ms.date: 2025-12-23T00:00:00.0000000Z
locale: en-us
document_id: 0fb0cf7d-c6d5-65d8-eef4-fea8d8fc3480
document_version_independent_id: 0fb0cf7d-c6d5-65d8-eef4-fea8d8fc3480
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/mdo-sec-ops-manage-incidents-and-alerts.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdo-sec-ops-manage-incidents-and-alerts
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/mdo-sec-ops-manage-incidents-and-alerts.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 0b25b936-876e-276a-8d25-ab355e1a985d
---

# Manage incidents and alerts from Defender for Office 365 in Microsoft Defender XDR - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

An [incident](/en-us/defender-xdr/incidents-overview) in the Microsoft Defender portal is a collection of correlated alerts and associated data that define the complete story of an attack. Defender for Office 365 [alerts](/en-us/defender-xdr/alert-policies#default-alert-policies), [automated investigation and response (AIR)](air-about#the-overall-flow-of-air), and the outcome of the investigations are natively integrated and correlated on the **Incidents** page in the Microsoft Defender portal at https://security.microsoft.com/incidents. We refer to this page as the *Incidents* queue.

Alerts are created when malicious or suspicious activity affects an entity (for example, email, users, or mailboxes). Alerts provide valuable insights about in-progress or completed attacks. However, an ongoing attack can affect multiple entities, which results in multiple alerts from different sources. Some built-in alerts automatically trigger AIR playbooks. These playbooks do a series of investigation steps to look for other impacted entities or suspicious activity.

Watch this short video on how to manage Microsoft Defender for Office 365 alerts in the Microsoft Defender portal.

Defender for Office 365 alerts, investigations, and their data are automatically correlated. When a relationship is determined, the system creates an incident to give security teams visibility for the entire attack. Incidents represent more than just static events; they represent attack stories that happen over time. As the attack progresses, new Defender for Office 365 alerts, AIR investigations, and their data are continuously added to the existing incident.

We strongly recommend that SecOps teams manage incidents and alerts from Defender for Office 365 in the Incidents queue at https://security.microsoft.com/incidents. This approach has the following benefits:

- Multiple options for [management](/en-us/defender-xdr/manage-incidents):

    - Prioritization
    - Filtering
    - Classification
    - Tag management

    You can take incidents directly from the queue or assign them to someone. Comments and comment history can help track progress.
- If the attack impacts other workloads that are protected by Microsoft Defender^\*^, the related alerts, investigations, and their data are also correlated to the same incident.

    ^\*^Microsoft Defender for Endpoint, Microsoft Defender for Identity, and Microsoft Defender for Cloud Apps.
- Complex correlation logic isn't required, because the logic is provided by the system.
- If the correlation logic doesn't fully meet your needs, you can add alerts to existing incidents or create new incidents.
- Related Defender for Office 365 alerts, AIR investigations, and pending actions from investigations are automatically added to incidents.
- If the AIR investigation finds no threat, the system automatically resolves the related alerts If all alerts within an incident are resolved, the incident status also changes to **Resolved**.
- Related evidence and response actions are automatically aggregated on the **Evidence and response** tab of the incident.
- Security team members can take response actions directly from the incidents. For example, they can soft-delete email in mailboxes or remove suspicious Inbox rules from mailboxes.
- Recommended email actions are created only when the latest delivery location of a malicious email is a cloud mailbox.
- Pending email actions are updated based on the latest delivery location. If the email was already remediated by a manual action, the status reflects that.
- Recommended actions are created only for email and email clusters that are determined to be the most critical threats:

    - Malware
    - High confidence phishing
    - Malicious URLs
    - Malicious files

Note

The Defender portal shows a single evidence cluster for Defender for Office 365 instead of listing individual evidence items.

Manage incidents on the **Incidents** page in the Microsoft Defender portal at https://security.microsoft.com/incidents:

[![Incidents page in the Microsoft Defender portal.](media/mdo-sec-ops-incidents.png)](media/mdo-sec-ops-incidents.png#lightbox)

[![Details flyout on the Incidents page in the Microsoft Defender portal.](media/mdo-sec-ops-incident-details.png)](media/mdo-sec-ops-incident-details.png#lightbox)

[![Filter flyout on the Incidents page in the Microsoft Defender portal.](media/mdo-sec-ops-incident-filters.png)](media/mdo-sec-ops-incident-filters.png#lightbox)

[![Summary tab of the incident details in the Microsoft Defender portal.](media/mdo-sec-ops-incident-summary-tab.png)](media/mdo-sec-ops-incident-summary-tab.png#lightbox)

[![Evidence and alerts tab of the incident details in the Microsoft Defender portal.](media/mdo-sec-ops-incident-evidence-and-response-tab.png)](media/mdo-sec-ops-incident-evidence-and-response-tab.png#lightbox)

Manage incidents on the **Incidents** page in Microsoft Sentinel at https://portal.azure.com/#blade/HubsExtension/BrowseResource/resourceType/microsoft.securityinsightsarg%2Fsentinel:

[![Incidents page in Microsoft Sentinel.](media/microsoft-sentinel-incidents.png)](media/microsoft-sentinel-incidents.png#lightbox)

[![Incident details page in Microsoft Sentinel.](media/mdo-sec-ops-microsoft-sentinel-incident-details.png)](media/mdo-sec-ops-microsoft-sentinel-incident-details.png#lightbox)

## Response actions to take

Security teams can take wide variety of response actions on email using Defender for Office 365 tools:

- You can delete messages, but you can also take the following actions on email:

    - Move to Inbox
    - Move to Junk
    - Move to Deleted Items
    - Soft delete
    - Hard delete.

    You can take these actions from the following locations:

    - The **Evidence and response** tab from the details of the incident on the **Incidents** page at https://security.microsoft.com/incidents (recommended).
    - **Threat Explorer** at https://security.microsoft.com/threatexplorer.
    - The unified **Action center** at https://security.microsoft.com/action-center/pending.
- You can start an AIR playbook manually on any email message using the **Trigger investigation** action in Threat Explorer.
- You can report false positive or false negative detections directly to Microsoft using [Threat Explorer](threat-explorer-real-time-detections-about) or [admin submissions](submissions-admin).
- You can block undetected malicious files, URLs, or senders using the [Tenant Allow/Block List](tenant-allow-block-list-about).

Actions in Defender for Office 365 are seamlessly integrated into hunting experiences and the history of actions are visible on the **History** tab in the unified **Action center** at https://security.microsoft.com/action-center/history.

The most effective way to take action is to use the built-in integration with Incidents in Microsoft Defender XDR. You can approve the actions that were recommended by AIR in Defender for Office 365 on the [Evidence and response](/en-us/defender-xdr/investigate-incidents#evidence-and-response) tab of an incident in Microsoft Defender XDR. This method of tacking action is recommended for the following reasons:

- You investigate the complete attack story.
- You benefit from the built-in correlation with other workloads: Microsoft Defender for Endpoint, Microsoft Defender for Identity, and Microsoft Defender for Cloud Apps.
- You take actions on email from a single place.

You take action on email based on the result of a manual investigation or hunting activity. [Threat Explorer](threat-explorer-real-time-detections-about) allows security team members to take action on any email messages that might still exist in cloud mailboxes. They can take action on intra-org messages that were sent between users in your organization. Threat Explorer data is available for the last 30 days.

Watch this short video to learn how the Microsoft Defender portal combines alerts from various detection sources, like Defender for Office 365, into incidents.