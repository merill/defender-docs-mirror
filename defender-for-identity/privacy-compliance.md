---
layout: Conceptual
title: Microsoft Defender for Identity – privacy - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/privacy-compliance
feedback_system: Standard
feedback_product_url: https://aka.ms/MDIcommunity
breadcrumb_path: /azure-advanced-threat-protection/bread/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: microsoft-defender-for-identity
uhfHeaderId: MSDocsHeader-MicrosoftDefender
ms.suite: ems
description: Learn how Microsoft Defender for Identity collects data in a manner that protects personal privacy.
ms.date: 2025-09-28T00:00:00.0000000Z
ms.topic: article
ms.reviewer: rlitinsky
locale: en-us
document_id: 564fc12f-19b3-f30b-05c1-bd44d314b559
document_version_independent_id: 564fc12f-19b3-f30b-05c1-bd44d314b559
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/privacy-compliance.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: privacy-compliance
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/privacy-compliance.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 8d2ce0e8-9ff0-6c0e-8c89-cefc66106a32
---

# Microsoft Defender for Identity – privacy - Microsoft Defender for Identity | Microsoft Learn

This article describes how Microsoft Defender for Identity collects data in a manner that protects personal privacy.

Note

If you're interested in viewing or deleting personal data, please review Microsoft's guidance in [Windows Data Subject Requests for the GDPR](/en-us/microsoft-365/compliance/gdpr-dsr-windows). If you're looking for general information about GDPR, see the [GDPR section of the Service Trust portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

## What data is collected?

Microsoft Defender for Identity monitors information generated from your organization's Active Directory, network activities, and event activities to detect suspicious activity. The monitored activity information enables Defender for Identity to help you determine the validity of each potential threat and correctly triage and respond.

For more information, see: [Microsoft Defender for Identity monitored activities](monitored-activities).

## Data location

Defender for Identity operates in the Microsoft Azure data centers in the following locations:

- Asia (Southeast Asia)
- Australia (Australia East, Australia Southeast)
- Europe (West Europe, North Europe)
- India (Central India, South India)
- North America (East US, West US, West US2)
- Switzerland (Switzerland North, Switzerland West)
- United Arab Emirates (UAE North and UAE Central)
- United Kingdom (UK South)

Customer data collected by the service might be stored as follows:

- Your workspace is automatically created in the data center that's geographically closest to your Microsoft Entra ID. Once created, Defender for Identity workspaces can't be moved to another data center. Your workspace's data center is listed in the Microsoft Defender portal, under **Settings** &gt; **Identity** &gt; **About** &gt; **Geolocation**.
- A geographic location as defined by the data storage rules of an online service, if the online service is used by Defender for Identity to process such data.

## Data retention

Microsoft Defender for Identity retains data for 180 days, which is visible across the portal.

Your data is kept and is available to you while the license is under grace period or suspended mode. At the end of this period, that data will be erased from Microsoft's systems to make it unrecoverable, no later than 180 days from contract termination or expiration.

## Data sharing

Defender for Identity shares data, including customer data, among any of the following Microsoft products that are also licensed by the customer. For customers in the Government Community Cloud (GCC), data sharing between government and commercial cloud environments may occur, depending on the location of the service offering.

- Microsoft Defender
- Microsoft Defender for Cloud Apps
- Microsoft Defender for Endpoint
- Microsoft Defender for Cloud
- Microsoft Sentinel
- Microsoft Security Exposure Management (public preview)