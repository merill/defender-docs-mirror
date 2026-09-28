---
layout: Conceptual
title: Set up enterprise IoT security - Defender for IoT - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/eiot-defender-for-endpoint
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
description: Enable enterprise IoT security for your IoT devices, using added security value in Microsoft Defender for IoT.
ms.topic: quickstart
ms.date: 2023-09-13T00:00:00.0000000Z
ms.custom:
- enterprise-iot
- sfi-image-nochange
locale: en-us
document_id: 1969c9cb-dbb5-b977-bc38-fa7e9dc6493d
document_version_independent_id: 98e243e4-39c6-2343-d1dd-99c584a166ee
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/eiot-defender-for-endpoint.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/eiot-defender-for-endpoint
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/eiot-defender-for-endpoint.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 4bc2ea4f-dcff-2972-8861-31b41e211716
---

# Set up enterprise IoT security - Defender for IoT - Microsoft Defender for IoT | Microsoft Learn

This article describes how [Microsoft Defender for Endpoint](/en-us/microsoft-365/security/defender-endpoint/) customers can enable enterprise IoT security for their IoT devices, using added security value in Microsoft Defender for IoT.

While the IoT device inventory is already available for Defender for Endpoint P2 customers, turning on enterprise IoT security adds alerts, recommendations, and vulnerability data, purpose-built for IoT devices in your enterprise network.

IoT devices include printers, cameras, VOIP phones, smart TVs, and more. Turning on enterprise IoT security means, for example, that you can use a recommendation in Microsoft Defender to open a single IT ticket for patching vulnerable applications on both servers and printers.

## Prerequisites

Before you start the procedures in this article, read through [Secure IoT devices in the enterprise](concept-enterprise) to understand more about the integration between Defender for Endpoint and Defender for IoT.

Make sure that you have:

- IoT devices in your network, visible in the Microsoft Defender **Device inventory**
- Access to the Microsoft Defender Portal as a [Security administrator](/en-us/azure/active-directory/roles/permissions-reference#security-administrator)
- Microsoft Defender for Endpoint agents deployed in your environment. For more information, see [onboard Microsoft Defender for Endpoint](/en-us/defender-endpoint/onboarding).
- One of the following licenses:

    - A Microsoft 365 E5 (ME5) or E5 Security license
    - Microsoft Defender for Endpoint P2, with an extra, standalone **Microsoft Defender for IoT - EIoT Device License - add-on** license, available for purchase or trial from the Microsoft 365 admin center.

    Tip

    If you have a standalone license, you don't need to toggle on **Enterprise IoT Security** and can skip directly to View added security value in Microsoft Defender XDR.

    For more information, see [Enterprise IoT security in Microsoft Defender XDR](concept-enterprise#enterprise-iot-security-in-microsoft-defender-xdr).

## Turn on enterprise IoT security monitoring

This procedure describes how to turn on enterprise IoT monitoring in Microsoft Defender, and is relevant only for ME5/E5 Security customers.

Skip this procedure if you have one of the following types of licensing plans:

- Customers with legacy Enterprise IoT pricing plan and an ME5/E5 Security license.
- Customers with standalone, per-device licenses added on to Microsoft Defender for Endpoint P2. In such cases, the Enterprise IoT security setting is turned on as read-only.

**To turn on enterprise IoT monitoring**:

1. In [Microsoft Defender XDR](https://security.microsoft.com/), select **Settings** &gt; **[Device Discovery](/en-us/microsoft-365/security/defender-endpoint/device-discovery)** &gt; **Enterprise IoT**.

Note

Ensure you have turned on Device Discovery in **Settings** &gt; **Endpoints** &gt; **Advanced Features**.

1. Toggle the Enterprise IoT security option to **On**. For example:

    ![Screenshot of Enterprise IoT toggled on in Microsoft Defender XDR.](media/enterprise-iot/eiot-toggle-on.png)

## View added security value in Microsoft Defender XDR

This procedure describes how to view related alerts, recommendations, and vulnerabilities for a specific device in Microsoft Defender, when the **Enterprise IoT security** option is turned on.

**To view added security value**:

1. In [Microsoft Defender XDR](https://security.microsoft.com/), select **Assets** &gt; **Devices** to open the **Device inventory** page.
2. Select the **IoT devices** tab and select a specific device **IP** to drill down for more details. For example:

    [![Screenshot of the IoT devices tab in Microsoft Defender XDR.](media/enterprise-iot/select-a-device.png)](media/enterprise-iot/select-a-device.png#lightbox)
3. On the device details page, explore the following tabs to view data added by the enterprise IoT security for your device:

    - On the **Alerts** tab, check for any alerts triggered by the device. Simulate alerts in Microsoft 365 Defender for Enterprise IoT using the Raspberry Pi scenario available in the Microsoft 365 Defender [Evaluation & Tutorials](https://security.microsoft.com/tutorials/all) page.

        You can also set up advanced hunting queries to create custom alert rules. For more information, see sample advanced hunting queries for Enterprise IoT monitoring.
    - On the **Security recommendations** tab, check for any recommendations available for the device to reduce risk and maintain a smaller attack surface.
    - On the **Discovered vulnerabilities** tab, check for any known CVEs associated with the device. Known CVEs can help decide whether to patch, remove, or contain the device and mitigate risk to your network. Alternatively, use advanced hunting queries to collect vulnerabilities across all your devices.

**To hunt for threats**:

On the **Device inventory** page, select **Go hunt** to query devices using tables like the *[DeviceInfo](/en-us/microsoft-365/security/defender/advanced-hunting-deviceinfo-table)* table. On the **Advanced hunting** page, query data using other schemas.

## Sample advanced hunting queries for Enterprise IoT

This section lists sample advanced hunting queries that you can use in Microsoft 365 Defender to help you monitor and secure your IoT devices with Enterprise for IoT security.

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