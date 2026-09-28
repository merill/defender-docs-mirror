---
layout: Conceptual
title: Check the device health at Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/check-sensor-status
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Check the sensor health on devices to identify which ones are misconfigured, inactive, or aren't reporting sensor data.
ms.service: defender-endpoint
ms.subservice: onboard
ms.author: lwainstein
author: limwainstein
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.topic: concept-article
ms.date: 2025-03-26T00:00:00.0000000Z
locale: en-us
document_id: 48f2fdd4-377e-40b3-7ee6-117e51220bfe
document_version_independent_id: 48f2fdd4-377e-40b3-7ee6-117e51220bfe
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/check-sensor-status.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: check-sensor-status
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/check-sensor-status.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 4261e770-9b38-ce27-c693-380d0ee9c2ac
---

# Check the device health at Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

The **Device health** tile provides information on the individual device's ability to provide sensor data and communicate with the Defender for Endpoint service. It reports how many devices require attention and helps you identify problematic devices and take action to correct known issues.

There are two status indicators on the tile that provide information on the number of devices that aren't reporting properly to the service:

- **Misconfigured** - These devices might partially be reporting sensor data to the Defender for Endpoint service and might have configuration errors that need to be corrected.
- **Inactive** - Devices that have stopped reporting to the Defender for Endpoint service for more than seven days in the past month.

Clicking any of the groups directs you to **Device inventory**, filtered according to your choice.

On **Device inventory**, you can filter the health state list by the following status:

- **Active** - Devices that are actively reporting to the Defender for Endpoint service.
- **Misconfigured**- These devices might partially be reporting sensor data to the Defender for Endpoint service but have configuration errors that need to be corrected. Misconfigured devices can have either one or a combination of the following issues:
    - **No sensor data** - Devices has stopped sending sensor data. Limited alerts can be triggered from the device.
    - **Impaired communications** - Ability to communicate with device is impaired. Sending files for deep analysis, blocking files, isolating device from network and other actions that require communication with the device may not work.
- **Inactive** - Devices that have stopped reporting to the Defender for Endpoint service.

You can also download the entire list in CSV format using the **Export** feature. For more information on filters, see [View and organize the Devices list](machines-view-overview).

Note

Export the list in CSV format to display the unfiltered data. The CSV file will include all devices in the organization, regardless of any filtering applied in the view itself and can take a significant amount of time to download, depending on how large your organization is.

You can view the device details when you click on a misconfigured or inactive device.