---
layout: Conceptual
title: Integrate the Forescout OT data connector in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/forescout-data-connector
author: DebLanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Learn how to set up the Forescout OT data connector in Microsoft Security Exposure Management.
ms.topic: how-to
ms.date: 2026-07-07T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: 6db88fec-0ceb-5e21-13dc-7f65fb85862a
document_version_independent_id: 6db88fec-0ceb-5e21-13dc-7f65fb85862a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/forescout-data-connector.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: forescout-data-connector
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/forescout-data-connector.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/5287f575-02f0-405f-92b7-800456526b0c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/06e86142-34c2-4b94-ab9c-9477c21f7152
platformId: 8736546e-9b48-af46-d028-fbff03f3ec1c
---

# Integrate the Forescout OT data connector in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn

The Forescout operational technology (OT) data connector lets you bring OT asset and vulnerability data from Forescout into Microsoft Security Exposure Management.

## Prerequisites

Before you configure the Forescout OT data connector, make sure you have:

- [Access to the Microsoft Defender portal](prerequisites).
- [Permissions to manage data connectors](configure-data-connectors#roles--permissions).
- Your Forescout **Endpoint** and **API Key**.

## Data retrieved by the connector

The Forescout OT data connector retrieves the following asset and device properties:

- Device name (hostname)
- MAC addresses
- IP addresses
- Operating system details
- Vendor
- Model
- Firmware version
- Device category or type
- Serial number
- Device criticality
- Associated edge collectors
- Last seen

## Connect the Forescout OT data connector

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
2. Go to **System** &gt; **Data management** &gt; **Data connectors**.
3. In **Unified connectors**, select **Catalog**.
4. Select **Forescout**.
5. Select **Add new instance**.
6. In **Connector name**, enter a name for the connector instance.
7. In **Endpoint**, enter your Forescout endpoint without the `http://` or `https://` prefix.
8. In **API Key**, enter the API key from Forescout.
9. Select **Next**.
10. Confirm that **MSEM (Microsoft Security Exposure Management)** is selected.
11. Select **Next**.
12. Review the connector details.
13. Select **Connect**.

## Verify the connection

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
2. Go to **System** &gt; **Data management** &gt; **Data connectors**.
3. In **Unified connectors**, select **My connectors**.
4. Confirm that the Forescout connector instance appears with a connected status.