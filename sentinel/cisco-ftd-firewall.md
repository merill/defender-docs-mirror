---
layout: Conceptual
title: Collect data from Cisco Secure Firewall devices with ASA or FTD connectors | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/cisco-ftd-firewall
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
description: Learn when to use the Microsoft Sentinel connectors for Cisco Secure Firewall devices running ASA or FTD, with links to the appropriate installation steps.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ms.collection: sentinel-data-connector
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: e5a2ce48-5c7c-66e0-351a-9a15033b5ccf
document_version_independent_id: 4b00a79f-90cf-853f-7f35-3f0c7a7a85f3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/cisco-ftd-firewall.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/cisco-ftd-firewall
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/cisco-ftd-firewall.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/440fefb2-823b-44b8-a593-35604cde23b7
- https://authoring-docs-microsoft.poolparty.biz/devrel/9f747546-6aa0-47b1-90d7-ee9646fdb207
- https://authoring-docs-microsoft.poolparty.biz/devrel/bad69977-db6a-44f3-b752-d2bee7de49ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1b2df129-9f07-41b8-9038-0761a41d8a21
- https://authoring-docs-microsoft.poolparty.biz/devrel/c49cc9cb-c0e4-4c7c-8e26-9ab61f52e8b0
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31d7aff-61be-45e2-a324-a578cf0c3360
platformId: 7122da49-17f3-f017-3d24-9ff908d6fec9
---

# Collect data from Cisco Secure Firewall devices with ASA or FTD connectors | Microsoft Learn

Microsoft Sentinel provides two connectors that collect logs from Cisco Secure Firewall devices, depending on whether the devices run the Firewall Threat Defense (FTD) or Adaptive Security Appliance (ASA) software. This article explains when to use each connector and provides links to installation instructions.

## Collect Syslog from a Cisco FTD or ASA device

To collect syslog from FTD or ASA devices, use the [Cisco ASA/FTD via AMA connector](data-connectors-reference#cisco-asaftd-via-ama). For information on syslog configuration guidance for Cisco FTD, see the Cisco documentation [External Logging Configuration](https://secure.cisco.com/secure-firewall/docs/external-logging-configuration).

## Collect CEF logs from a Cisco FTD device

To collect CEF logs from a Cisco FTD device:

Warning

The eNcore client is no longer being updated, and Cisco recommends the syslog format for new deployments. Use the following steps only if you specifically need the CEF path.

1. Install and configure the eNcore eStreamer client, which collects logs from FTD devices (via the Firewall Management Center) and converts them to Common Event Format (CEF). For more information, see the full [Cisco eStreamer eNcore installation guide](https://www.cisco.com/c/en/us/td/docs/security/firepower/670/api/eStreamer_enCore/eStreamereNcoreSentinelOperationsGuide_409.html).
2. Install [CEF via AMA connector](connect-cef-syslog-ama).