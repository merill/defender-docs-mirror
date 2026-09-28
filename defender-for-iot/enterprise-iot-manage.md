---
layout: Conceptual
title: Manage enterprise IoT security for Microsoft Defender for IoT in the Defender portal - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-iot/enterprise-iot-manage
breadcrumb_path: /defender-for-iot/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to monitor enterprise IoT devices and review security alerts, recommendations, and vulnerabilities in Microsoft Defender for IoT in the Defender portal.
ms.service: defender-for-iot
author: limwainstein
ms.author: lwainstein
ms.localizationpriority: medium
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: cff1c1c2-e739-bd82-ba59-f3d277b2514a
document_version_independent_id: cff1c1c2-e739-bd82-ba59-f3d277b2514a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot/enterprise-iot-manage.md
site_name: Docs
depot_name: Learn.defender-for-iot
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: enterprise-iot-manage
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot/enterprise-iot-manage.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 0b532906-0585-2015-0bf2-0880ebf4b3f1
---

# Manage enterprise IoT security for Microsoft Defender for IoT in the Defender portal - Microsoft Defender for IoT | Microsoft Learn

Enterprise IoT security improves the monitoring and protection of the IoT devices in your network, such as printers, smart TVs, Voice over Internet Protocol (VoIP) devices, conferencing systems and purpose-built, proprietary devices.

When enterprise IoT is activated, the data for recommendations and vulnerabilities is shown in the Microsoft Defender portal.

This article describes how to view alerts, security recommendations, and vulnerabilities for your IoT devices, use advanced hunting queries to identify threats, and turn off enterprise IoT security when you no longer need it.

This article explains how to view enterprise IoT security data, hunt for threats, use advanced hunting queries to monitor your IoT devices, and turn off enterprise IoT security in the Defender portal.

## View enterprise IoT data in the Defender portal

To view enterprise IoT security data:

1. In [Microsoft Defender portal](https://security.microsoft.com/), select **Assets** &gt; **Devices** to open the **Device inventory** page.
2. Select the **IoT devices** tab and select a specific device **IP** to drill down for more details. For example:

    [![Screenshot of the IoT devices tab in Microsoft Defender portal.](media/enterprise-iot-manage/select-a-device.png)](media/enterprise-iot-manage/select-a-device.png#lightbox)
3. When you select a specific device, the device details page opens. Explore the following tabs to view data added by enterprise IoT security for your device:

    - On the **Alerts** tab, check for any alerts triggered by the device. Simulate alerts in Microsoft Defender for Enterprise IoT using the Raspberry Pi scenario available in the Microsoft Defender [Evaluation & Tutorials](https://security.microsoft.com/tutorials/all) page.

        You can also set up advanced hunting queries to create custom alert rules. For more information, see advanced hunting queries for enterprise IoT security.
    - On the **Security recommendations** tab, check for any recommendations available for the device to reduce risk and maintain a smaller attack surface.
    - On the **Discovered vulnerabilities** tab, check for any known CVEs associated with the device. Known CVEs can help decide whether to patch, remove, or contain the device and mitigate risk to your network. Alternatively, use advanced hunting queries to collect vulnerabilities across all your devices.

## Hunt for threats on the Device inventory page

On the **Device inventory** page, select **Go hunt** to query devices using tables like the *[DeviceInfo](/en-us/microsoft-365/security/defender/advanced-hunting-deviceinfo-table)* table. On the **Advanced hunting** page, query data using other schemas.

## Advanced hunting queries for enterprise IoT

The following sample advanced hunting queries can help you monitor and secure your IoT devices with enterprise IoT security in Microsoft Defender.

### Find devices by specific type or subtype

Use the following query to identify devices that exist in your corporate network by type of device, such as routers: 

```kusto
DeviceInfo
| summarize arg_max(Timestamp, *) by DeviceId
| where DeviceType == "NetworkDevice" and DeviceSubtype == "Router"  
```

### Find and export vulnerabilities for your IoT devices

Use the following query to list all vulnerabilities on your IoT devices:

```kusto
DeviceInfo
| where DeviceCategory =~ "iot"
| join kind=inner DeviceTvmSoftwareVulnerabilities on DeviceId
```

For more information, see [Advanced hunting](/en-us/microsoft-365/security/defender/advanced-hunting-overview) and [Understand the advanced hunting schema](/en-us/microsoft-365/security/defender/advanced-hunting-schema-tables).

## Turn off enterprise IoT security

Customers with Microsoft 365 E5 or E5 Security plans who no longer need the **enterprise IoT security** service can turn off the feature.

**To turn off enterprise IoT security**:

1. In [Microsoft Defender portal](https://security.microsoft.com/), select **Settings** &gt; **Device discovery** &gt; **Enterprise IoT**.
2. Toggle the option to **Off**.

When enterprise IoT security is turned off, you lose access to purpose-built alerts, vulnerabilities, and recommendations in the Defender portal.

Customers with a Microsoft Defender for Endpoint P2 license who don't add a standalone license by the time the trial ends, have the trial automatically canceled, and lose access to enterprise IoT security features. For more information, see [Purchase the standalone enterprise IoT security license](enterprise-iot-get-started#purchase-the-standalone-license).