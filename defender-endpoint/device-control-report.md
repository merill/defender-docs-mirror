---
layout: Conceptual
title: View device control events and information in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/device-control-report
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Monitor your organization's data security through device control reports.
ms.service: defender-endpoint
ms.localizationpriority: medium
ms.date: 2024-06-25T00:00:00.0000000Z
ms.author: lwainstein
author: limwainstein
ms.topic: article
ms.subservice: asr
ms.collection:
- m365-security
- tier2
- mde-asr
ms.custom: sfi-ga-nochange
locale: en-us
document_id: ee79560c-d3af-b74e-47e8-f930bb13f010
document_version_independent_id: ee79560c-d3af-b74e-47e8-f930bb13f010
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/device-control-report.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: device-control-report
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/device-control-report.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 8e5104c9-ca23-56c8-7603-5b988422a820
---

# View device control events and information in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Microsoft Defender for Endpoint device control helps protect your organization from potential data loss, malware, or other cyberthreats by allowing or preventing certain devices to be connected to users' computers. Your security team can view information about device control events with advanced hunting or by using the device control report.

Important

Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

To access the [Microsoft Defender portal](https://security.microsoft.com/advanced-hunting), your subscription must include Microsoft 365 for E5 reporting.

Select each tab to learn more about advanced hunting and the device control report.

# [Advanced hunting](#tab/advhunt)
## Advanced hunting

When a device control policy is triggered, an event is visible with advanced hunting, regardless of whether it was initiated by the system or by the user who signed in. This section includes some example queries you can use in advanced hunting.

### Example 1: Removable storage policy triggered by disk and file system level enforcement

When a `RemovableStoragePolicyTriggered` action occurs, event information about the disk and file system level enforcement is available.

Tip

Currently, in advanced hunting, there's a limit of 300 events per device per day for `RemovableStoragePolicyTriggered` events. Use the device control report to view additional data.

```kusto

//RemovableStoragePolicyTriggered: event triggered by Disk and file system level enforcement for both Printer and Removable storage based on your policy
DeviceEvents
| where ActionType == "RemovableStoragePolicyTriggered"
| extend parsed=parse_json(AdditionalFields)
| extend RemovableStorageAccess = tostring(parsed.RemovableStorageAccess)
| extend RemovableStoragePolicyVerdict = tostring(parsed.RemovableStoragePolicyVerdict)
| extend MediaBusType = tostring(parsed.BusType)
| extend MediaClassGuid = tostring(parsed.ClassGuid)
| extend MediaClassName = tostring(parsed.ClassName)
| extend MediaDeviceId = tostring(parsed.DeviceId)
| extend MediaInstanceId = tostring(parsed.DeviceInstanceId)
| extend MediaName = tostring(parsed.MediaName)
| extend RemovableStoragePolicy = tostring(parsed.RemovableStoragePolicy)
| extend MediaProductId = tostring(parsed.ProductId)
| extend MediaVendorId = tostring(parsed.VendorId)
| extend MediaSerialNumber = tostring(parsed.SerialNumber)
|project Timestamp, DeviceId, DeviceName, InitiatingProcessAccountName, ActionType, RemovableStorageAccess, RemovableStoragePolicyVerdict, MediaBusType, MediaClassGuid, MediaClassName, MediaDeviceId, MediaInstanceId, MediaName, RemovableStoragePolicy, MediaProductId, MediaVendorId, MediaSerialNumber, FolderPath, FileSize
| order by Timestamp desc

```

# [Device control report](#tab/report)
## Device control report

**Applies to:**

- [Microsoft Defender for Endpoint Plan 1](microsoft-defender-endpoint)
- [Microsoft Defender for Endpoint Plan 2](microsoft-defender-endpoint)
- [Microsoft Defender for Business](/en-us/defender-business)

With the device control report, you can view events that relate to media usage. Such events include:

- **Audit events:** Shows the number of audit events that occur when external media is connected.
- **Policy events:** Shows the number of policy events that occur when a device control policy is triggered.

Note

The audit event to track media usage is enabled by default for devices onboarded to Microsoft Defender for Endpoint.

### Understanding the audit events

The audit events include:

- **USB drive mount and unmount:** Audit events that are generated when a USB drive is mounted or unmounted.
- **PnP:** Plug and Play audit events are generated when removable storage, a printer, or Bluetooth media is connected.
- **Removable storage access control:** Events are generated when a removable storage access control policy is triggered. It can be Audit, Block, or Allow.

### Monitor device control security

Device control in Defender for Endpoint empowers security administrators with tools that enable them to track their organization's device control security through reports. You can find the device control report in the Microsoft Defender portal (https://security.microsoft.com). Go to **Reports** &gt; **Endpoints**. Find **Device control** card, and select the link to open the report.

In the **Reports** dashboard, the **Device protection** card shows the number of audit events generated by media type, over the last 180 days. Under **View details**, raw events over the last 30 days are listed.

The **View details** button shows more media usage data in the **Device control report** page.

The page provides a dashboard with aggregated number of events per type and a list of events and shows 500 events per page, but if you're an administrator (such as a Security Administrator), you can scroll down to see more events and can filter on time range, media class name, and device ID.

[![The Device Control Report Details page in the Microsoft Defender portal](media/detaileddevicecontrolreport.png)](media/detaileddevicecontrolreport.png#lightbox)

When you select an event, an **Event information** details flyout opens to show more information:

- **General details:** Date, Action mode, the policy, and Access of this event.
- **Media information:** Media information includes Media name, Class name, Class GUID, Device ID, Vendor ID, Serial number, and Bus type.
- **Location details:** Device name, User, and MDATP device ID.

[![The Filter On Device Control Report page](media/devicecontrolreportfilter.png)](media/devicecontrolreportfilter.png#lightbox)

To see real-time activity for this media across the organization, select ![](media/defender-portal-icon-no.png)**Open Advanced hunting** at the top of the flyout. This includes an embedded, predefined query.

[![The Query On Device Control Report page](media/devicecontrolreportquery.png)](media/devicecontrolreportquery.png#lightbox)

To see the security of the device, select the **Open device page** button at the bottom of the flyout. This button opens the device entity page.

[![The Device Entity Page](media/devicesecuritypage.png)](media/devicesecuritypage.png#lightbox)

### Reporting delays

There might be a delay of up to six hours from the time a media connection occurs to the time the event is reflected in the card or in the domain list.

Note

When you export data, such as a list of events, from the device control report to Excel, up to 500 events are exported. However, if your organization is using Microsoft Sentinel, you can integrate Defender for Endpoint with Sentinel so that all incidents and alerts are streamed. For more information, see [Connect data from Microsoft Defender to Microsoft Sentinel](/en-us/azure/sentinel/connect-microsoft-365-defender).

---