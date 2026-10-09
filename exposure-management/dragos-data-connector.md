---
layout: Conceptual
title: Integrate the Dragos OT data connector in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/dragos-data-connector
author: DebLanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Learn how to set up the Dragos OT data connector in Microsoft Security Exposure Management.
ms.topic: how-to
ms.date: 2026-07-07T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: e684b181-09cd-58f1-55cd-045df7f3092e
document_version_independent_id: e684b181-09cd-58f1-55cd-045df7f3092e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/dragos-data-connector.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: dragos-data-connector
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/dragos-data-connector.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: ca7d08d0-b8ca-cedf-01a1-391024df58f5
---

# Integrate the Dragos OT data connector in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn

The Dragos OT data connector lets you bring OT data from Dragos into Microsoft Security Exposure Management.

## Prerequisites

Before you configure the Dragos OT data connector, make sure you have:

- [Access to the Microsoft Defender portal](prerequisites).
- [Permissions to manage data connectors](configure-data-connectors#roles--permissions).
- Your Dragos **Hostname**, **API Key**, and **API Secret**.

## Data retrieved by the connector

The Dragos OT data connector retrieves the following asset and device properties:

- Device name (hostname)
- IP address
- MAC address
- Domain
- Operating system details, including OS platform, OS platform friendly name, and kernel version
- Vendor
- Model
- Firmware version
- Serial number
- Device type
- Device subtype
- Sensor associations
- Zone
- Dragos criticality

## Connect the Dragos OT data connector

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
2. Go to **System** &gt; **Data management** &gt; **Data connectors**.
3. In **Unified connectors**, select **Catalog**.
4. Select **Dragos**.
5. Select **Add new instance**.
6. In **Connector name**, enter a name for the connector instance.
7. In **Hostname**, enter your Dragos hostname without the `http://` or `https://` prefix.
8. In **API Key**, enter the API key from Dragos.
9. In **API Secret**, enter the API secret from Dragos.
10. Select **Next**.
11. Confirm that **MSEM (Microsoft Security Exposure Management)** is selected.
12. Select **Next**.
13. Review the connector details.
14. Select **Connect**.

## Verify the connection

1. In the Microsoft Defender portal, go to **System** &gt; **Data management** &gt; **Data connectors**.
2. In **Unified connectors**, select **My connectors**.
3. Confirm that the Dragos connector instance appears with a connected status.