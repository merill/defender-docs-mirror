---
layout: Conceptual
title: Investigate an IP address associated with an alert - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/investigate-ip
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use the investigation options to examine possible communication between devices and external IP addresses.
ms.service: defender-endpoint
ms.author: chrisda
author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
- mde-edr
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.subservice: edr
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 55b7569d-7008-7451-b319-b97b82b4db3f
document_version_independent_id: 55b7569d-7008-7451-b319-b97b82b4db3f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/investigate-ip.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: investigate-ip
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/investigate-ip.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: ac826c26-dd52-879a-e1e5-2333ab09281b
---

# Investigate an IP address associated with an alert - Microsoft Defender for Endpoint | Microsoft Learn

Examine possible communication between your devices and external internet protocol (IP) addresses.

Identifying all devices in the organization that communicated with a suspected or known malicious IP address, such as Command and Control (C2) servers, helps determine the potential scope of breach, associated files, and infected devices.

You can find information from the following sections in the IP address view:

- IP geo information
- Alerts related to this IP
- IP in organization observations
- Prevalence in organization

## IP geolocation information

In the IP address view, the left pane provides IP details (if available).

- Organization (ISP)
- ASN
- Country
- State
- City
- Carrier
- Latitude
- Longitude
- Postal code

## Related alerts

The **Related alerts** section provides a list of alerts that are associated with the IP.

## IP activity observed in the organization

The **IP activity observed in the organization** section provides a list of devices that have a connection with this IP and the last event details for each device (the list is limited to 100 devices).

## IP prevalence in the organization

The **IP prevalence in the organization** section displays how many devices have connected to this IP address, and when the IP was first and last seen. You can filter the results of this section by time period; the default period is 30 days.

**Investigate an external IP:**

1. Enter the IP address in the **Search** field.
2. Select the IP suggestion box and open the IP side panel.
3. Select **Enter**.

Details about the IP address are displayed, including: registration details (if available), prevalence of devices in the organization that communicated with this IP Address (during selectable time period), and the devices in the organization that were observed communicating with this IP address.

Note

Search results will only be returned for IP addresses observed in communication with devices in the organization.

Use the IP search filters at the top of the page to define the search criteria. You can also use the timeline search box to filter the displayed results of all devices in the organization observed communicating with the IP address, the file associated with the communication and the last date observed.

Clicking any of the device names will take you to that device's view, where you can continue to investigate reported alerts, behaviors, and events.