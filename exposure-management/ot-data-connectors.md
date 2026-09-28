---
layout: Conceptual
title: OT data connectors in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/ot-data-connectors
author: limwainstein
ms.author: lwainstein
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Learn how OT data connectors enrich Microsoft Security Exposure Management with third-party operational technology asset and vulnerability data.
ms.topic: overview
ms.date: 2026-07-07T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: 317034af-009d-5fcd-6ac9-273b4223e17c
document_version_independent_id: 317034af-009d-5fcd-6ac9-273b4223e17c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/ot-data-connectors.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: ot-data-connectors
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/ot-data-connectors.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 49e49c68-7822-7adf-ee4e-5355a3c33d97
---

# OT data connectors in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn

Operational technology (OT) data connectors let you bring OT asset and vulnerability data from supported third-party OT platforms into [Microsoft Security Exposure Management](microsoft-security-exposure-management).

After an OT connector is configured, Exposure Management uses the ingested data to enrich device inventory, improve asset context, and help security teams investigate exposure across IT and OT environments.

## Supported OT data connectors

Microsoft Security Exposure Management supports the following OT data connectors:

- [Armis](armis-data-connector)
- [Dragos](dragos-data-connector)
- [Forescout](forescout-data-connector)

## OT data in Exposure Management

OT data connectors bring OT device, asset, and vulnerability data from supported third-party OT platforms into the Defender portal. This data helps security teams view OT assets alongside other devices and investigate OT exposure without switching between separate tools.

OT connectors can provide data such as:

- OT device and asset information
- Device identifiers, such as hostnames, IP addresses, MAC addresses, and serial numbers
- Device type, subtype, vendor, model, firmware, and operating system details
- Location, zone, site, sensor, or network association information
- Asset criticality or device importance values from the connected OT platform
- Vulnerability findings associated with OT devices

The exact properties depend on the OT platform and connector.

## OT device visibility

OT data connectors enrich device inventory with OT device details from supported third-party OT platforms. This helps security teams view IT, IoT, and OT devices in a single inventory experience.

In device inventory, OT data can help you:

- Identify OT devices discovered by third-party OT platforms.
- View OT-specific device details, such as device type, vendor, model, firmware, and site.
- Filter devices by OT-related properties, such as discovery source, firmware version, and site.
- Open a device page to review available OT context for a specific asset.

[![Screenshot of OT devices in device inventory.](media/ot-data-connectors/ot-device-inventory.png)](media/ot-data-connectors/ot-device-inventory.png#lightbox)

## OT vulnerability visibility

OT data connectors can also bring vulnerability findings associated with OT devices into Defender portal vulnerability experiences.

This helps security teams:

- View OT vulnerabilities together with other vulnerability data.
- Search for CVEs and review affected OT devices.
- Open a device page to review vulnerabilities discovered for that device.
- Understand vulnerability impact across IT and OT environments.

[![Screenshot of OT vulnerabilities in the Defender portal.](media/ot-data-connectors/ot-vulnerabilities.png)](media/ot-data-connectors/ot-vulnerabilities.png#lightbox)