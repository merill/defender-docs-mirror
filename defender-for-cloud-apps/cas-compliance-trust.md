---
layout: Conceptual
title: Microsoft Defender for Cloud Apps – privacy - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/cas-compliance-trust
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: Learn about how Microsoft Defender for Cloud Apps manages user privacy.
ms.date: 2025-06-17T00:00:00.0000000Z
ms.topic: concept-article
locale: en-us
document_id: 19018d44-4afb-8bba-d145-88346b6971a0
document_version_independent_id: 19018d44-4afb-8bba-d145-88346b6971a0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/cas-compliance-trust.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: cas-compliance-trust
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/cas-compliance-trust.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: ccea6a8a-888c-0e47-fd86-37fceb54c1c0
---

# Microsoft Defender for Cloud Apps – privacy - Microsoft Defender for Cloud Apps | Microsoft Learn

Microsoft Defender for Cloud Apps is a critical component of the Microsoft cloud security stack, which helps you stay in control over your cloud applications with comprehensive visibility, auditing, and granular controls over your sensitive data.

This article provides an overview of the data security and privacy practices for Microsoft Defender for Cloud Apps.

## Data collected by Defender for Cloud Apps

Microsoft Defender for Cloud Apps collects information from your configured cloud apps and data sources. Information collected from those sources includes:

- Network data
- OAuth app configuration and usage
- Audits on cloud app usage by users and other apps
- File metadata and content
- System settings and policies
- User and group configurations

Note

The data collected from the various applications is dependent on the customer-provided data from the various applications and might include personal information.

## Data storage location

Defender for Cloud Apps operates in the Microsoft Azure data centers in the following geographical regions:

| Customer provisioning location | Data storage location |
| --- | --- |
| **Customers whose tenants are provisioned in the United States** | United States |
| **Customers whose tenants are provisioned in the European Union or the United Kingdom** | The European Union or the United Kingdom, depending on service availability. |
| **Customers whose tenants are provisioned in any other region** | The United States and/or a data center in the region that's nearest to the location of where the customer's Microsoft Entra tenant has been provisioned. |

In addition to the locations above, the App Governance features within Defender for Cloud Apps operate in the Microsoft Azure data centers in the following geographical regions listed below. Customer with App Governance enabled will have data stored within the data storage location the customer provisions in above, and in a second data storage location as described below:

| Customer provisioning location | Data storage location |
| --- | --- |
| **Customers whose tenants are provisioned in the United States** | United States |
| **Customers whose tenants are provisioned in in the European Union** | European Union |
| **Customers whose tenants are provisioned in the United Kingdom** | United Kingdom |
| **Customers whose tenants are provisioned in Australia** | Australia |
| **Customers whose tenants are provisioned in Germany** | Germany |
| **Customers whose tenants are provisioned in Canada** | Canada |
| **Customers whose tenants are provisioned in France** | France |
| **Customers whose tenants are provisioned in Japan** | Japan |
| **Customers whose tenants are provisioned in India** | India |
| **Customers whose tenants are provisioned in Asia Pacific** | Asia Pacific |
| **Customers whose tenants are provisioned in any other region** | The United States and/or a data center in the region that's nearest to the location of where the customer's Microsoft Entra tenant has been provisioned. |

Customer data collected by Defender for Cloud Apps is either stored in your tenant location, as described in the previous tables, or in the geographic location of another online service that Defender for Cloud Apps shares data with, as defined by the data storage rules of that online service.

### View your data storage location

To view your Defender for Cloud Apps tenant location in the Microsoft Defender portal, go to **Settings &gt; Cloud Apps &gt; About &gt; Region**.

Note

If Defender for Cloud Apps data is stored in your tenant location, your tenant isn't movable after having been created.

## Data retention

Data from Microsoft Defender for Cloud Apps is retained for up to 180 days, and is visible across the portal.

Your data is kept and is available to you while the license is under grace period or suspended mode. At the end of this period, that data is erased from Microsoft's systems to make it unrecoverable, no later than 180 days from contract termination or expiration.

## Data sharing for Microsoft Defender for Cloud Apps

Defender for Cloud Apps shares data, including customer data, among the following Microsoft products also licensed by the customer. For customers in the Government Community Cloud (GCC), data sharing between government and commercial cloud environments might occur, depending on the location of the service offering.

- Microsoft Defender
- Microsoft Defender for Cloud
- Microsoft Sentinel
- Microsoft Defender for Endpoint
- Microsoft Security Exposure Management
- Microsoft Purview
- Microsoft Entra ID Protection