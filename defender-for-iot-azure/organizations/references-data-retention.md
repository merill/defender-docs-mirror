---
layout: Conceptual
title: Data retention and sharing across Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/references-data-retention
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
description: Learn about the data retention periods and capacities for Microsoft Defender for IoT data stored in Microsoft Azure and the OT sensor.
ms.topic: concept-article
ms.date: 2024-06-30T00:00:00.0000000Z
locale: en-us
document_id: 3c6c3ec4-4d65-ec53-1e1a-76459e90de9c
document_version_independent_id: 6b191f31-4933-3260-212b-fa01f0d806b6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/references-data-retention.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/references-data-retention
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/references-data-retention.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 05057394-3907-3999-7d87-1bd3bbce4fc1
---

# Data retention and sharing across Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn

Microsoft Defender for IoT stores data in the Microsoft Azure portal, in OT network sensors.

Each storage type has varying storage capacity options and retention times. This article describes the data retention policy for the amount of data and length of time the data is stored in each storage type before being deleted or overwritten.

## What are we collecting?

Defender for IoT collects information from your configured devices and stores it in a service specific, customer-dedicated and segregated tenant. The stored data is for administration, tracking, and reporting purposes.

Information collected includes network connection data (IPs and ports), and device details (device identifiers, names, operating system versions, firmware versions). Defender for IoT stores this data securely in accordance with Microsoft privacy practices and [Microsoft Trust Center policies](https://azure.microsoft.com/explore/trusted-cloud/).

This data enables Defender for IoT to:

- Proactively identify indicators of attack (IOAs) in your organization.
- Generate alerts if a possible attack is detected.
- Provide your security team a view into devices and addresses related to threat signals from your network, enabling you to investigate and explore possible network security threats.

Microsoft doesn't use your data for advertising.

## Data location

Defender for IoT uses the Microsoft Azure data centers in the European Union and the United States. Customer data collected by the service might be stored in one of two geo-locations:

- The geolocation of the tenant as identified during provisioning.
- The geolocation as defined by the data storage rules of an online service, that's used by Defender for IoT to process its data.

## Data retention

Data from Defender for IoT is retained for as long as a customer is active or for 90 days after the end of your contract. During this period the data is visible across your other services on the portal.

Your data is kept and is available while your license is under a grace period or in suspended mode. 90 days after the end of this period, your data is erased from Microsoft's systems making it unrecoverable.

## Device data retention periods

The following table lists how long device data is stored in each Defender for IoT storage type.

| Storage type | Details |
| --- | --- |
| **Azure portal** | 90 days from the date of the **Last activity** value.  For more information, see [Manage your device inventory from the Azure portal](how-to-manage-device-inventory-for-organizations). |
| **OT network sensor** | 90 days from the date of the **Last activity** value.  For more information, see [Manage your OT device inventory from a sensor console](how-to-investigate-sensor-detections-in-a-device-inventory). |

## Alert data retention

The following table lists how long alert data is stored in each Defender for IoT storage type. Alert data is stored as listed, regardless of the alert's status, or whether it's been learned or muted.

| Storage type | Details |
| --- | --- |
| **Azure portal** | 90 days from the date in the **First detection** value.  For more information, see [View and manage alerts from the Azure portal](how-to-manage-cloud-alerts). |
| **OT network sensor** | 90 days from the date in the **First detection** value. For more information, see [View alerts on your sensor](how-to-view-alerts). |

### OT alert PCAP data retention

The following table lists how long PCAP data is stored in each Defender for IoT storage type.

| Storage type | Details |
| --- | --- |
| **Azure portal** | PCAP files are available for download from the Azure portal for as long as the OT network sensor stores them.  Once downloaded, the files are cached on the Azure portal for 48 hours.  For more information, see [Access alert PCAP data](how-to-manage-cloud-alerts#access-alert-pcap-data). |
| **OT network sensor** | Dependent on the sensor's storage capacity allocated for PCAP files, which determines its [hardware profile](ot-appliance-sizing): - **C5600**: 130 GB - **E1800**: 130 GB - **E1000** : 78 GB- **E500**: 78 GB - **L500**: 7 GB - **L100**: 2.5 GB If a sensor exceeds its maximum storage capacity, the oldest PCAP file is deleted to accommodate the new one.  For more information, see [Access alert PCAP data](how-to-view-alerts#access-alert-pcap-data) and [Pre-configured physical appliances for OT monitoring](ot-pre-configured-appliances). |

The usage of available PCAP storage space depends on factors such as the number of alerts, the type of the alert, and the network bandwidth, all of which affect the size of the PCAP file.

Tip

To avoid being dependent on the sensor's storage capacity, use external storage to back up your PCAP data.

## Security recommendation retention

Defender for IoT security recommendations are stored only on the Azure portal, for 90 days from when the recommendation is first detected.

For more information, see [Enhance security posture with security recommendations](recommendations).

## OT event timeline retention

OT event timeline data is stored on OT network sensors only, and the storage capacity differs depending on the sensor's [hardware profile](ot-appliance-sizing).

The retention of event timeline data isn't limited by time. However, assuming a frequency of 500 events per day, all hardware profiles are able to retain the events for at least **90 day**s.

If a sensor exceeds its maximum storage size, the oldest event timeline data file is deleted to accommodate the new one.

The following table lists the maximum number of events that can be stored for each hardware profile:

| Hardware profile | Number of events |
| --- | --- |
| **C5600** | 10M events |
| **E1800** | 10M events |
| **E1000** | 6M events |
| **E500** | 6M events |
| **L500** | 3M events |
| **L100** | 500-K events |

For more information, see [Track sensor activity](how-to-track-sensor-activity) and [Pre-configured physical appliances for OT monitoring](ot-pre-configured-appliances).

## OT log file retention

Service and processing log files are stored on the Azure portal for 30 days from their creation date.

Other OT monitoring log files are stored only on the OT network sensor.

For more information, see:

- [Troubleshoot the sensor](how-to-troubleshoot-sensor)

## Backup file capacity

The OT network sensor has automated backups running daily, and older backup files are overwritten when the configured storage capacity reaches its limit.

For more information, see:

- [Set up backup and restore files on an OT sensor](back-up-restore-sensor#set-up-backup-and-restore-files)

### Backups on the OT network sensor

The retention of backup files depends on the sensor's architecture, as each hardware profile has a set amount of hard disk space allocated for backup history:

| Hardware profile | Allocated hard disk space |
| --- | --- |
| **L100** | Backups aren't supported |
| **L500** | 20 GB |
| **E1000** | 60 GB |
| **E1800** | 100 GB |
| **C5600** | 100 GB |

## Data sharing for Microsoft Defender for IoT

Microsoft Defender for IoT shares data, including customer data, among the following Microsoft products, also licensed by the customer.

- Microsoft Defender
- Microsoft Sentinel
- Microsoft Threat Intelligence Center
- Microsoft Defender for Cloud
- Microsoft Defender for Endpoint
- Microsoft Security Exposure Management