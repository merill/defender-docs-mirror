---
layout: Conceptual
title: Investigate incidents and alerts in Microsoft Defender for IoT in the Defender portal - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-iot/investigate-threats
breadcrumb_path: /defender-for-iot/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Investigate Defender for IoT incidents and related alerts in the Defender portal, analyze evidence, and remediate security issues detected in your OT environment.
ms.service: defender-for-iot
author: limwainstein
ms.author: lwainstein
ms.localizationpriority: medium
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: b7a90896-f276-8e0a-b633-29868de3e76c
document_version_independent_id: b7a90896-f276-8e0a-b633-29868de3e76c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot/investigate-threats.md
site_name: Docs
depot_name: Learn.defender-for-iot
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: investigate-threats
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot/investigate-threats.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 7bf309ad-f827-e006-bb6e-83f7b57cc7cf
---

# Investigate incidents and alerts in Microsoft Defender for IoT in the Defender portal - Microsoft Defender for IoT | Microsoft Learn

Microsoft Defender for IoT in the Microsoft Defender portal displays incidents and alerts, which enhance your network security and operations with real-time details about events logged in your operational technology (OT) network.

Alerts are the basis of all incidents and indicate the occurrence of malicious or suspicious events in your environment. Within an incident, you analyze the alerts that affect your network, understand what they mean, and collate the evidence so that you can devise an effective remediation plan.

Learn more about [alert investigation in Microsoft Defender XDR](/en-us/defender-xdr/investigate-alerts) and [incident investigation in Microsoft Defender XDR](/en-us/defender-xdr/investigate-incidents) in the Defender portal.

This section explains how to investigate a Microsoft Defender for IoT incident and its associated alerts, and how to remediate the security issues they raise.

Alerts in the **Incidents** page uniquely combine IT and OT environment signals to detect potential threats and data leaks. The **Incidents** page displays:

- A history of the alerts connected to the incident and an incident graph. The graph shows other devices connected to the affected OT device that might also be compromised.
- Alert descriptions, which explain the type of detected security issue.
- Remediation options to solve the security problem.

Note

Incident and alert data for Defender for IoT only appear once you have a site set up and your devices are sending data to the Defender portal. If you haven't configured a site yet, see [Set up a site for Defender for IoT](set-up-sites).

Important

This article discusses Microsoft Defender for IoT in the Defender portal (Preview).

Some features are not yet available in the Defender portal. If you're interested in these features, or you're an existing customer working on the Azure portal, see the [Defender for IoT on Azure documentation](/en-us/azure/defender-for-iot/organizations/overview).

Learn more about the [Defender for IoT management portals](/en-us/defender-for-iot/microsoft-defender-iot#what-are-the-different-management-portals-for-microsoft-defender-for-iot).

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Investigate alerts

To investigate an alert:

1. In the [Microsoft Defender portal](https://security.microsoft.com/machines) menu, select **Incidents & alerts &gt; Incidents**.
2. To display OT related incidents:

    1. Select **Add filter**.
    2. Select **Product name** and select **Add**.
    3. Select the **Product names** tab that appears and type: *Defender for IoT*.
    4. Select **Apply**.
3. Locate and select an incident.

    The specific incident page shows the attack story made up of the alert timeline, an incident graph and the incident details.
4. Select an alert from the alerts list.

    The incident graph and incident details display specific data for this alert.
5. In the **Incident** panel, review the information, read the **Alert description**, **Evidence** and **Impacted assetts** and follow the **Alert recommended actions** to remediate the issue.

## Review a Defender for IoT alert

Defender for IoT generates its own unique alert.

| Name | Description |
| --- | --- |
| **Possible operational impact due to a compromised device** | A compromised device communicated with an operational technology (OT) asset. An attacker might be attempting to control or disrupt physical operations. |

## Use advanced hunting to investigate IoT alerts

Advanced hunting is a query-based investigation feature in the Defender portal that lets you explore security data across your environment. Use the **Site** property listed in the **DeviceInfo** table to write queries for advanced hunting. Using the **Site** property allows you to filter devices according to a specific site, for example, all devices that communicated with malicious devices at a specific site.

The following query filters the **DeviceInfo** table to return all endpoint devices that match a specific public IP address at the San Francisco site.

```kusto
DeviceInfo
|where Site == "SanFrancisco" and PublicIP == "192.168.1.1" and DeviceCategory == "Endpoint"
```

Filtering devices by site in advanced hunting queries is relevant for both the device inventory and site security. For more information, see [Advanced hunting](/en-us/../defender-xdr/advanced-hunting-overview) and the [Advanced hunting DeviceInfo schema](/en-us/../defender-xdr/advanced-hunting-deviceinfo-table).