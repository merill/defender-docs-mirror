---
layout: Conceptual
title: Endpoint Attack Notifications - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/endpoint-attack-notifications
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
ms.reviewer: 
description: Endpoint Attack Notifications provides proactive hunting for the most important threats to your network.
ms.service: defender-endpoint
ms.author: chrisda
author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.topic: article
ms.custom:
- cx-ti
- cx-ean
ms.subservice: edr
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: 20836e67-b909-b02c-1780-11a465b2c8a4
document_version_independent_id: 20836e67-b909-b02c-1780-11a465b2c8a4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/endpoint-attack-notifications.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: endpoint-attack-notifications
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/endpoint-attack-notifications.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 550d45b9-c370-2adb-5daa-1e1dddc6fc02
---

# Endpoint Attack Notifications - Microsoft Defender for Endpoint | Microsoft Learn

Note

This covers threat hunting on your Microsoft Defender for Endpoint service. However, if you're interested to explore the service beyond your current license, and proactively hunt threats not just on endpoints but also across Office 365, cloud applications, and identity, refer to [Microsoft Defender Experts for Hunting](/en-us/defender-xdr/defender-experts-for-hunting).

Note

The intake of new customers to the Endpoint Attack Notifications service is currently on pause. For customers interested in a managed service, sign up the [Defender Experts service request form](https://aka.ms/IWantDefenderExperts).

Endpoint Attack Notifications (previously referred to as Microsoft Threat Experts - Targeted Attack Notification) provides proactive hunting for the most important threats to your network, including human adversary intrusions, hands-on-keyboard attacks, or advanced attacks like cyber-espionage. These notifications show up as a new alert. The managed hunting service includes:

- Threat monitoring and analysis, reducing dwell time and risk to the business
- Hunter-trained artificial intelligence to discover and prioritize both known and unknown attacks
- Identifying the most important risks, helping SOCs maximize time and energy
- Scope of compromise and as much context as can be quickly delivered to enable fast SOC response

![Screenshot of the Endpoint Attack Notifications alert](/en-us/defender/media/defender-endpoint/endpoint-attack-notification-alert.png)

## Apply for Endpoint Attack Notifications

If you're a Microsoft Defender for Endpoint customer, you can apply for Endpoint Attack Notifications. Go to **Settings** &gt; **Endpoints** &gt; **General** &gt; **Advanced features** &gt; **Endpoint Attack Notifications** to apply. Once accepted, you get the benefits of Endpoint Attack Notifications.

![How to enable Endpoint Attack Notifications in 365 Defender Portal](/en-us/defender/media/defender-endpoint/enable-endpoint-attack-notifications.png)

## Receive Endpoint Attack notifications

Endpoint Attack Notifications are alerts that are hand crafted by Microsoft's managed hunting service based on suspicious activity in your environment. They can be viewed through several mediums:

- The alerts queue in the Microsoft Defender portal
- Using the [API](api/get-alerts)
- [DeviceAlertEvents](/en-us/defender-xdr/advanced-hunting-migrate-from-mde#map-devicealertevents-table) table in Advanced hunting
- Your email if you [configure an email notifications](configure-vulnerability-email-notifications) rule

Endpoint Attack Notifications are identified by:

- Have a tag named **Endpoint Attack Notification**
- Have a service source of **Microsoft Defender for Endpoint** &gt; **Microsoft Defender Experts**

Note

If you enrolled for Endpoint Attack Notifications but are not seeing any alerts from the service, it indicates that you have a strong security posture and are less prone to attacks.

## Create an email notification rule

You can create rules to send email notifications for notification recipients. See [Configure alert notifications](/en-us/defender-xdr/configure-email-notifications) to create, edit, delete, or troubleshoot email notification, for details.