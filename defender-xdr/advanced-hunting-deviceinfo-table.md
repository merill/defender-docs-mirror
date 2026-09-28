---
layout: Conceptual
title: DeviceInfo table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-deviceinfo-table
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about OS, computer name, and other machine information in the DeviceInfo table of the advanced hunting schema
ms.service: defender-xdr
ms.subservice: adv-hunting
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- tier3
- m365-security
ms.custom:
- cx-ti
- cx-ah
- msecd-doc-authoring-1015
ms.topic: reference
ms.date: 2026-07-27T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: aa5380eb-1596-6ffd-3e1a-931e1db54e4c
document_version_independent_id: aa5380eb-1596-6ffd-3e1a-931e1db54e4c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-deviceinfo-table.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-deviceinfo-table
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-deviceinfo-table.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 2962cd3f-e947-ba8a-b5fa-f717dac44715
---

# DeviceInfo table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn

The `DeviceInfo` table in the [advanced hunting](advanced-hunting-overview) schema contains information about devices in the organization, including OS version, active users, and computer name. Use this reference to construct queries that return information from this table.

Important

Some information relates to prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

This advanced hunting table is populated by records from various Microsoft services. If your organization hasn't deployed the service in Microsoft Defender, queries that use the table aren't going to work or return any results. For more information about how to deploy a Microsoft service in the Defender portal, read [Deploy supported services](deploy-supported-services).

For information on other tables in the advanced hunting schema, [see the advanced hunting reference](advanced-hunting-schema-tables).

| Column name | Data type | Description |
| --- | --- | --- |
| `Timestamp` | `datetime` | Last date and time recorded for the device |
| `DeviceId` | `string` | Unique identifier for the device in the service |
| `DeviceName` | `string` | Fully qualified domain name (FQDN) of the device |
| `ClientVersion` | `string` | Version of the endpoint agent or sensor running on the device |
| `PublicIP` | `string` | Public IP address used by the onboarded device to connect to the Microsoft Defender for Endpoint service. This could be the IP address of the device itself, a NAT device, or a proxy. |
| `OSArchitecture` | `string` | Architecture of the operating system running on the device |
| `OSPlatform` | `string` | Platform of the operating system running on the device. This indicates specific operating systems, including variations within the same family, such as Windows 11, Windows 10 and Windows 7. |
| `OSBuild` | `long` | Build version of the operating system running on the device |
| `IsAzureADJoined` | `boolean` | Boolean indicator of whether device is joined to Microsoft Entra ID |
| `JoinType` | `string` | The device's Microsoft Entra ID join type |
| `AadDeviceId` | `string` | Unique identifier for the device in Microsoft Entra ID |
| `LoggedOnUsers` | `string` | List of all users that are logged on the device at the time of the event in JSON array format |
| `RegistryDeviceTag` | `string` | Device tag added through the registry |
| `OSVersion` | `string` | Version of the operating system running on the device |
| `MachineGroup` | `string` | Machine group of the device. This group is used by role-based access control to determine access to the device. |
| `ReportId` | `long` | Event identifier based on a repeating counter. To identify unique events, this column must be used in conjunction with the DeviceName and Timestamp columns. |
| `OnboardingStatus` | `string` | Indicates whether the device is currently onboarded or not to Microsoft Defender for Endpoint or if the device is not supported |
| `AdditionalFields` | `string` | Additional information about the event in JSON array format |
| `DeviceCategory` | `string` | Broader classification that groups certain device types under the following categories: Endpoint, Network device, IoT, Unknown |
| `DeviceType` | `string` | Type of device based on purpose and functionality, such as network device, workstation, server, mobile, gaming console, or printer |
| `DeviceSubtype` | `string` | Additional modifier for certain types of devices, for example, a mobile device can be a tablet or a smartphone; only available if device discovery finds enough information about this attribute |
| `Model` | `string` | Model name or number of the product from the vendor or manufacturer, only available if device discovery finds enough information about this attribute |
| `Vendor` | `string` | Name of the product vendor or manufacturer, only available if device discovery finds enough information about this attribute |
| `OSDistribution` | `string` | Distribution of the OS platform, such as Ubuntu or RedHat for Linux platforms |
| `OSVersionInfo` | `string` | Additional information about the OS version, such as the popular name, code name, or version number |
| `MergedDeviceIds` | `string` | Previous device IDs that have been assigned to the same device |
| `MergedToDeviceId` | `string` | The most recent device ID assigned to a device |
| `IsInternetFacing` | `boolean` | Indicates whether the device is internet-facing |
| `SensorHealthState` | `string` | Indicates health of the device's EDR sensor, if onboarded to Microsoft Defender for Endpoint |
| `IsExcluded` | `bool` | Determines if the device is currently excluded from Microsoft Defender for Vulnerability Management experiences |
| `ExclusionReason` | `string` | Indicates the reason for device exclusion |
| `ExposureLevel` | `string` | The device's level of vulnerability to exploitation based on its exposure score; can be: Low, Medium, High |
| `AssetValue` | `string` | Priority or value assigned to the device in relation to its importance in computing the organization's exposure score; can be: Low, Normal (Default), High |
| `DeviceManualTags` | `string` | Device tags created manually using the portal UI or public API |
| `DeviceDynamicTags` | `string` | Device tags added and removed dynamically based on dynamic rules |
| `ConnectivityType` | `string` | Type of connectivity from the device to the cloud |
| `HostDeviceId` | `string` | Device ID of the device running Windows Subsystem for Linux |
| `AzureResourceId` | `string` | Unique identifier of the Azure resource associated with the device |
| `AwsResourceName` | `string` | Unique identifier specific to Amazon Web Services devices, containing the Amazon resource name |
| `GcpFullResourceName` | `string` | Unique identifier specific to Google Cloud Platform devices, containing a combination of zone and ID for GCP |
| `HardwareUuid` | `string` | Universally Unique Identifier (UUID) of the device's hardware |
| `CloudPlatforms` | `string` | The cloud platforms that the device belongs to. Can be Azure, Amazon Web Services, Google Cloud Platform and Azure Arc. |
| `AzureVmId` | `string` | Unique identifier assigned to the device in Azure |
| `AzureVmSubscriptionId` | `string` | Unique identifier of the Azure subscription associated with the device |
| `IsTransient` | `boolean` | Indicates whether this device is classified as short-lived or transient based on the frequency of appearance of the device on the network |
| `OsBuildRevision` | `string` | Build revision number of the operating system running on the machine |
| `MitigationStatus` | `string` | Indicates the mitigation action applied to a device |
| `Site` | `string` | Represents the physical location where the device is located |
| `DiscoverySources` | `string` | Products or services that have seen or reported the device, including when they last reported it |
| `DeviceRoles` | `string` | Device roles and characteristics associated with the device, in JSON format. Includes roles identified by the system or defined by users, confidence levels, and the last time each role was seen. |
| `DlpInfo` | `string` | Properties related to Endpoint Data Loss Prevention (DLP).* |

\* For information about the properties available in the `DlpInfo` column, see [Troubleshooting endpoint data loss prevention configuration and policy sync.](/en-us/purview/dlp-edlp-tshoot-sync#access-device-attribute-data-using-advanced-hunting)

The DeviceInfo table is updated continuously, and all updates contain the full current device data for that device.

## Sample query

You can use the following sample query to get the latest state of a device:

```kusto
// Get latest information on user/device
DeviceInfo
| extend IngestionTime = ingestion_time()
| where DeviceName == "example" and isnotempty(OSPlatform)
| summarize arg_max(IngestionTime, *) by DeviceId
```