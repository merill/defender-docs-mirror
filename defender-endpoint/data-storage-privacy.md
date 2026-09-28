---
layout: Conceptual
title: Microsoft Defender for Endpoint data storage and privacy - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/data-storage-privacy
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn about how Microsoft Defender for Endpoint handles privacy and data that it collects.
keywords: Microsoft Defender for Endpoint, data storage and privacy, storage, privacy, licensing, geolocation, data retention, data
ms.service: defender-endpoint
ms.author: lwainstein
author: limwainstein
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
- essentials-privacy
- essentials-security
- essentials-compliance
ms.topic: concept-article
ms.date: 2026-05-27T00:00:00.0000000Z
locale: en-us
document_id: f53dec94-fd88-20c6-8a75-d13b1301e0e7
document_version_independent_id: f53dec94-fd88-20c6-8a75-d13b1301e0e7
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/data-storage-privacy.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: data-storage-privacy
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/data-storage-privacy.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: a4e2f87e-b3aa-dcb2-5f72-6f182c73c8fe
---

# Microsoft Defender for Endpoint data storage and privacy - Microsoft Defender for Endpoint | Microsoft Learn

This article provides information about data storage and privacy for Microsoft Defender for Endpoint, including [Microsoft Defender Vulnerability Management](/en-us/defender-vulnerability-management/defender-vulnerability-management).

Note

This article explains the data storage and privacy details related to Defender for Endpoint (including Defender Vulnerability Management) and Defender for Business. For more information related to Defender for Endpoint and other products and services like Microsoft Defender Antivirus and Windows, see [Microsoft Privacy Statement](https://go.microsoft.com/fwlink/?linkid=827576).

## What are we collecting?

Microsoft Defender for Endpoint collects information from your configured devices and stores it in a customer-dedicated and segregated tenant specific to the service for administration, tracking, and reporting purposes.

Information collected includes:

- File data (file names, sizes, and hashes)
- Process data (running processes, hashes)
- Registry data
- Network connection data (host IPs and ports)
- Device details (device identifiers, names, and the operating system version)
- Software inventory data for Defender Vulnerability Management capabilities (installed applications, operating system versions, firmware, hardware components, and other relevant software details to identify vulnerabilities, assess risk levels, and provide actionable insights to help you secure your environment)

Microsoft stores this data securely in Microsoft Azure and maintains it in accordance with Microsoft privacy practices and [Microsoft Trust Center policies](https://go.microsoft.com/fwlink/?linkid=827578).

This data lets Defender for Endpoint:

- Proactively identify indicators of attack (IOAs) in your organization
- Generate alerts if a possible attack was detected
- Provide your security operations with a view into devices, files, and URLs related to threat signals from your network, enabling you to investigate and explore the presence of security threats on the network.

Microsoft doesn't use your data for advertising.

## Data location

Defender for Endpoint (including Defender Vulnerability Management) operates in the Microsoft Azure data centers in the European Union, the United Kingdom, the United States, Australia, Switzerland, India, or the United Arab Emirates (UAE). Customer data collected by the service might be stored in: (a) the geolocation of the tenant as identified during provisioning or, (b) the geolocation as defined by the data storage rules of an online service if this online service is used by Defender for Endpoint to process such data. For more information, see [Where your Microsoft 365 customer data is stored](/en-us/microsoft-365/enterprise/o365-data-locations).

(a) the geolocation of the tenant as identified during provisioning; or

(b) the geolocation as defined by the data storage rules of an online service if this online service is used by Defender for Endpoint to process such data.

## Data retention

Data from Microsoft Defender for Endpoint is retained for 180 days, visible across the portal.

Your data is kept and is available to you while the license is under grace period or suspended mode. At the end of this period, that data will be erased from Microsoft's systems to make it unrecoverable, no later than 180 days from contract termination or expiration.

In the advanced hunting investigation experience, it's accessible via a query for 30 days.

### Data retention for Defender Vulnerability Management inventory data

Inventory entries in Defender Vulnerability Management expire after **7 days** or **31 days** depending on the source as described in the following table:

| Data source | Retention period | Details |
| --- | --- | --- |
| Android apps | 7 days or 31 days | Depends on source event category. |
| Browser extensions^\*^ | 7 days | User-scoped and volatile. Expires quickly without refresh. |
| Certificates^\*^ | Up to two days before latest report (fallback is seven days) | Retention aligns to certificate reporting timestamps. |
| Deleted registry products | 30 days | Grace window after a product is marked deleted in the registry. |
| Firmware and hardware^\*^ | 31 days | Expires if the machine didn't report within 31 days or becomes unmanaged. |
| iOS apps | 7 days or 31 days | Depends on source event category. |
| Linux packages | 7 days or 31 days | Depends on source event category: <br>- **User/file scan**: 7 days.<br>- **System-scoped**: 31 days. |
| Software components from user/file scan sources | 7 days | Transient file/handle scans and other volatile sources. |
| User-scoped file paths (paths containing USERS) | 7 days | User profile locations. |
| User-scoped registry keys (HKU) | 7 days | User-specific hive data. |
| Default (all other sources) | 31 days | System-scoped and stable sources. |

^\*^ This data source isn't included in Microsoft Defender for Endpoint Plan 2. To get it, you need one of the following options:

- The Defender Vulnerability Management Add-on for Microsoft Defender for Endpoint Plan 2.
- Microsoft Defender Vulnerability Management Standalone if you don't already have Microsoft Defender for Endpoint Plan 2.

## Data recovery

Defender for Endpoint (including Defender Vulnerability Management) incorporates a regional disaster recovery strategy aligned with Microsoft's broader resiliency framework. For more information, see [Resiliency and continuity - Microsoft Service Assurance | Microsoft Learn](/en-us/compliance/assurance/assurance-resiliency-and-continuity). In the event of a service disruption, all MDE components are designed to fail over to a paired region within the same geographic boundary, thereby maintaining data residency requirements.

However, due to current service limitations in the United Arab Emirates, MDE components that depend on Azure Synapse workloads are supported with zonal resiliency only. At this time, for the workloads, there is no cross-region business continuity and disaster recovery (BCDR) capability available. For more information on Synapse’s disaster recovery capabilities, refer to the official documentation.

## Data sharing for Microsoft Defender for Endpoint

Defender for Endpoint (including Defender Vulnerability Management) shares data, including customer data, among the following Microsoft products, also licensed by the customer. For customers in the Government Community Cloud (GCC), data sharing between government and commercial cloud environments may occur, depending on the location of the service offering.

- Microsoft Defender
- Microsoft Defender for Cloud Apps
- Microsoft Sentinel
- Microsoft Tunnel for Mobile Application Management - Android
- Microsoft Defender for Cloud
- Microsoft Defender for Identity
- Microsoft Security Exposure Management
- Intune
- Agent 365

## Data visibility for Defender Vulnerability Management

Data visibility refers to what you see in the Microsoft Defender portal. If a device or specific software on the device stops reporting signals, Microsoft Defender Vulnerability Management stops showing related device or software vulnerabilities after **30 consecutive days**.

The following table describes how Defender Vulnerability Management retains and displays data for different scenarios:

| Retention scenario | Description | Learn more |
| --- | --- | --- |
| Inactive devices | A device can be listed as inactive for several reasons:- The device wasn't used for more than seven days.- The device was reinstalled or renamed. The previous device entity remains and is marked as **Inactive**.- The device was offboarded from Defender for Endpoint. After seven days, the health state of the device changes to **Inactive**.- The device didn't send signals to Microsoft Defender for Endpoint for more than seven days. Defender Vulnerability Management continues to display the last vulnerability snapshot for **up to 30 days** from the time the device stopped reporting. **After 30 days**, the device is marked as **Inactive** and associated vulnerabilities are no longer shown in the Defender portal. Defender for Endpoint retains data on inactive devices for up to 180 days for compliance and forensics. | - [Inactive devices in Microsoft Defender for Endpoint](fix-unhealthy-sensors#inactive-devices)- [Exclude devices](manage-device-scope-relevance#exclude-devices) |
| Uninstalled or inactive software | If specific software on an **active** device stops sending signals **for 30 consecutive days**, Defender Vulnerability Management assumes the software was removed or is inactive. Defender Vulnerability Management automatically stops flagging software vulnerabilities for the software on the device in the Defender portal. | [Software inventory](/en-us/defender-vulnerability-management/tvm-software-inventory) |

Note

For more information related to privacy in Defender Vulnerability Management and other products and services like Microsoft Defender Antivirus and Windows, see [Microsoft Privacy Statement](https://go.microsoft.com/fwlink/p/?linkid=827576).