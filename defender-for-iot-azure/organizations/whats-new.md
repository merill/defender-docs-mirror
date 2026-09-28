---
layout: Conceptual
title: What's New in Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/whats-new
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
description: This article describes new features available in Microsoft Defender for IoT, including both OT and Enterprise IoT networks, and both on-premises and in the Azure portal.
ms.topic: whats-new
ms.date: 2026-05-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom:
- enterprise-iot
- sfi-image-nochange
locale: en-us
document_id: f88a9981-2016-4df0-0415-85e28818c19a
document_version_independent_id: b97b7268-951e-b5ab-65d8-517fab87a7d4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/whats-new.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/whats-new
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/whats-new.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 524f3ded-26aa-9d38-a10d-b5eee4658ab0
---

# What's New in Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn

This article describes features available in Microsoft Defender for IoT, across both OT and Enterprise IoT networks, both on-premises and in the Azure portal, and for versions released in the last nine months.

Features released earlier than nine months ago are described in the [What's new archive for Microsoft Defender for IoT for organizations](whats-new-archive). For more information specific to OT monitoring software versions, see [OT monitoring software release notes](release-notes).

Note

Noted features listed below are in PREVIEW. bThe [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include other legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

Note

This article discusses Microsoft Defender for IoT in the Azure portal.

If you're a Microsoft Defender customer looking for a unified IT/OT experience, see the documentation for [Microsoft Defender for IoT in the Microsoft Defender portal (Preview) documentation](/en-us/defender-for-iot/).

Learn more about the [Defender for IoT management portals](/en-us/defender-for-iot/microsoft-defender-iot#what-are-the-different-management-portals-for-microsoft-defender-for-iot).

## June 2026

| Service area | Updates |
| --- | --- |
| **OT networks** | Sensor version 26.1.1 is now available. This release includes CVE updates and bug fixes for stability improvements. See [release details and updates](release-notes#version-2611). |

## April 2026

| Service area | Updates |
| --- | --- |
| **OT networks** | Sensor version 26.1.0 is now available. This release includes CVE updates and an OT sensor operating system upgrade to Debian 12. See [release details and updates](release-notes#version-2610). |

## February 2026

| Service area | Updates |
| --- | --- |
| **OT networks** | [New sensor health message - NTP server not configured](sensor-health-messages) |
| **OT networks** | Sensor version 25.2.2 is now available. See [release details and updates](release-notes#version-2522) |

## December 2025

| Service area | Updates |
| --- | --- |
| **OT networks** | Sensor version 25.2.1 is now available. See [release details and updates](release-notes#version-2521). |
| **OT networks** | [New sensor health message - No connection to NTP](sensor-health-messages) |

## September 2025

| Service area | Updates |
| --- | --- |
| **OT networks** | Sensor version 25.2.0 is now available. See [release details and updates](release-notes#version-2520). |
| **OT networks** | New sensor health messages |

### New sensor health messages

We've added the following sensor health messages to improve visibility into sensor connectivity issues:

- **Traffic bandwidth is close to its limit**
- **Traffic bandwidth exceeded its limit**
- **Number of monitored devices is close to its limit**
- **Number of monitored devices exceeded its limit**
- **Disk is almost full**

For more information, see [Sensor health message reference](sensor-health-messages).

## June 2025

| Service area | Updates |
| --- | --- |
| **OT networks** | Sensor version 25.1.2 is now available. See [release details and updates](release-notes#version-2512). |

## April 2025

| Service area | Updates |
| --- | --- |
| **OT networks** | Sensor version 25.1.1 is now available. See [release details and updates](release-notes#version-2511). |

## March 2025

| Service area | Updates |
| --- | --- |
| **OT networks** | The following sensor versions are now available:- 24.1.9: See [release details and updates](release-notes#2419).- 25.1.0: See [release details and updates](release-notes#version-2510). |
| **OT networks** | - "Unauthorized Internet Connectivity Detected" alert now includes URL information- Improved RDP Brute Force Detection |

### "Unauthorized Internet Connectivity Detected" alert now includes URL information

The "Unauthorized Internet Connectivity Detected" alert details now includes the URL from which the suspicious connection initiated, helping SOC analysts assess and respond to incidents more effectively.

The URL information applies only to HTTP-based connections and doesn’t appear for other protocols or for encrypted traffic such as HTTPS. You can view the URL details both on the sensor and in the Azure portal.

[![Screenshot of URL information in alert details.](media/whats-new/url-parameters.png)](media/whats-new/url-parameters.png#lightbox)

### Improved RDP brute force detection

The “Excessive Number of Sessions” alert now includes support by default to a remote desktop protocol (RDP) port, enhancing visibility into potential brute-force attacks and unauthorized access attempts.

## January 2025

| Service area | Updates |
| --- | --- |
| **OT networks** | - Aggregating multiple alerts violations with the same parameters |
| **OT networks** | - On-premises management console retirement |

### Aggregating multiple alerts violations with the same parameters

To reduce alert fatigue, multiple versions of the same alert violation and with the same parameters are grouped together and listed in the alerts table as one item. The alert details pane lists each of the identical alert violations in the **Violations** tab and the appropriate remediation actions are listed in the **Take action** tab. For more information, see [aggregating alerts with the same parameters](alerts#aggregating-alert-violations).

## On-premises management console retirement

The legacy on-premises management console isn't available for download after **January 1st, 2025**. We recommend transitioning to the new architecture using the full spectrum of on-premises and cloud APIs before this date. For more information, see [on-premises management console retirement](ot-deploy/on-premises-management-console-retirement).