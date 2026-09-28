---
layout: Conceptual
title: Microsoft Defender for IoT solution versions in Microsoft Sentinel - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/release-notes-sentinel
breadcrumb_path: ../breadcrumb/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-iot-blog/bg-p/MicrosoftDefenderIoTBlog
feedback_help_link_type: ask-the-community
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
ms.service: defender-for-iot
author: limwainstein
manager: bagol
ms.author: lwainstein
description: Learn about the updates available in each version of the Microsoft Defender for IoT solution, available from the Microsoft Sentinel content hub.
ms.date: 2025-11-17T00:00:00.0000000Z
ms.topic: release-notes
ms.subservice: sentinel-integration
locale: en-us
document_id: 59061425-feef-e74a-c98a-1ec7005925a6
document_version_independent_id: 9b0a540f-6d17-8049-2156-94c12f2b7486
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/release-notes-sentinel.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/release-notes-sentinel
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/release-notes-sentinel.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 4fa81eb9-89c1-9a86-6c92-184a5899ec0b
---

# Microsoft Defender for IoT solution versions in Microsoft Sentinel - Microsoft Defender for IoT | Microsoft Learn

This article lists the updates to out-of-the-box security content available from each version of the **Microsoft Defender for IoT** solution. The **Microsoft Defender for IoT** solution is available from the Microsoft Sentinel content hub.

The **Microsoft Defender for IoT** solution enhances the integration between Defender for IoT and Microsoft Sentinel, helping to streamline SOC workflows to analyze, investigate, and respond efficiently to OT incidents.

For more information, see:

- [What's new in Microsoft Defender for IoT?](whats-new)
- [Tutorial: Integrate Microsoft Sentinel and Microsoft Defender for IoT](/en-us/azure/sentinel/iot-solution?bc=%2fazure%2fdefender-for-iot%2fbreadcrumb%2ftoc.json&amp;toc=%2fazure%2fdefender-for-iot%2forganizations%2ftoc.json)
- [Tutorial: Investigate and detect threats for IoT devices](/en-us/azure/sentinel/iot-advanced-threat-monitoring?bc=%2fazure%2fdefender-for-iot%2fbreadcrumb%2ftoc.json&amp;toc=%2fazure%2fdefender-for-iot%2forganizations%2ftoc.json).

## Version 3.0.02

**Released**: January 2025

Updates in this version include:

- Microsoft Defender for IoT analytic rule templates now use Microsoft Sentinel Entities for alert entity mapping. The mapping includes source and destination IP addresses, as well as other device entities such as host to attach devices to alerts.
- Device entities add richer alert context to incidents in Microsoft Sentinel and the Microsoft Defender portal.

## Version 2.0.2

**Released**: February 2023

New features in this version include:

- Improved analytics rules, with the new ability to have incidents created only when new alerts are triggered in Defender for IoT. When configuring your incident creation in Microsoft Sentinel, filter alerts by the **Is New** property.
- An enhanced incident details page that includes Defender for IoT data, including a deep link to the Defender for IoT alert details page, the product name, remediation steps, and MITRE tactics and techniques.
- Performance improvements for analytics rule queries.

## Version 2.0.1

**Released**: September 2022

New features in this version include:

- Solution name changed to **Microsoft Defender for IoT**
- Workbook improvements:

    - A new overview dashboard
    - A new vulnerability dashboard
    - Inventory dashboard improvements
- New SOC playbooks for automation with CVEs, triaging incidents that involve sensitive devices, and email notifications to device owners for new incidents.

For more information, see [Updates to the Microsoft Defender for IoT solution](whats-new-archive#updates-to-the-microsoft-defender-for-iot-solution-in-microsoft-sentinels-content-hub).

## Version 2.0.0

**Released**: September 2022

This version provides enhanced experiences for managing, installing, and updating the solution package in the Microsoft Sentinel content hub.

For more information, see [Centrally discover and deploy Microsoft Sentinel out-of-the-box content and solutions](/en-us/azure/sentinel/sentinel-solutions-deploy)

## Version 1.0.14

**Released**: July 2022

New features in this version include:

- [Microsoft Sentinel incident synch with Defender for IoT alerts](whats-new-archive#microsoft-sentinel-incident-synch-with-defender-for-iot-alerts)
- IoT device entities displayed in related Microsoft Sentinel incidents.

## Version 1.0.13

**Released**: March 2022

New features in this version include:

- A bug fix to prevent new incidents from being created in Microsoft Sentinel each time an alert in Defender for IoT is updated or deleted.
- A new analytics rule for the **No traffic on sensor detected** Defender for IoT alert.
- Updates in the **Unauthorized PLC changes** analytics rule to support the **Illegal Beckhoff AMS Command** Defender for IoT alert.
- A new, deep link to Defender for IoT alerts directly from related Microsoft Sentinel incidents.

## Earlier versions

For more information about earlier versions of the **Microsoft Defender for IoT** solution, contact us via the [Defender for IoT community](https://techcommunity.microsoft.com/t5/microsoft-defender-for-iot/bd-p/MicrosoftDefenderIoT).