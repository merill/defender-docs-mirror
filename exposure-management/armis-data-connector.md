---
layout: Conceptual
title: Integrate the Armis OT data connector in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/armis-data-connector
author: limwainstein
ms.author: lwainstein
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Learn how to set up the Armis OT data connector in Microsoft Security Exposure Management.
ms.topic: how-to
ms.date: 2026-07-07T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: 668cfe1b-4027-35f7-9ac0-ed24a1f9a003
document_version_independent_id: 668cfe1b-4027-35f7-9ac0-ed24a1f9a003
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/armis-data-connector.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: armis-data-connector
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/armis-data-connector.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 3e2df2d2-2228-0925-d789-d13b2eff142e
---

# Integrate the Armis OT data connector in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn

The Armis OT data connector lets you bring OT data from Armis into Microsoft Security Exposure Management.

## Prerequisites

Before you configure the Armis OT data connector, make sure you have:

- [Access to the Microsoft Defender portal](prerequisites).
- [Permissions to manage data connectors](configure-data-connectors#roles--permissions).
- Your Armis **Tenant Hostname**, **Client ID**, and **Client Secret**.

## Data retrieved by the connector

The Armis OT data connector retrieves the following asset and device properties:

- Device ID
- Device name
- Device category
- Device type
- Brand or vendor
- Model
- Operating system details, including OS name and OS version
- Firmware version
- Serial numbers
- Site or location
- Network interfaces
- Visibility information
- First seen
- Last seen

## Connect the Armis OT data connector

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
2. Go to **System** &gt; **Data management** &gt; **Data connectors**.
3. In **Unified connectors**, select **Catalog**.
4. Select **Armis**.
5. Select **Add new instance**.
6. In **Connector name**, enter a name for the connector instance.
7. In **Tenant Hostname**, enter your Armis tenant hostname without the `http://` or `https://` prefix.
8. In **Client ID**, enter the client ID from Armis.
9. In **Client Secret**, enter the client secret from Armis.
10. Select **Next**.
11. Confirm that **MSEM (Microsoft Security Exposure Management)** is selected.
12. Select **Next**.
13. Review the connector details.
14. Select **Connect**.

## Verify the connection

1. In the Microsoft Defender portal, go to **System** &gt; **Data management** &gt; **Data connectors**.
2. In **Unified connectors**, select **My connectors**.
3. Confirm that the Armis connector instance appears with a connected status.