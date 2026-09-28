---
layout: Conceptual
title: Get started for Enterprise IoT for Microsoft Defender for IoT in the Defender portal - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-iot/enterprise-iot-get-started
breadcrumb_path: /defender-for-iot/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to set up and start monitoring enterprise IoT devices using Microsoft Defender for IoT in the Microsoft Defender portal.
ms.service: defender-for-iot
author: limwainstein
ms.author: lwainstein
ms.localizationpriority: medium
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: cf46a62e-b4a3-a5f1-4dd9-65b73cde0b53
document_version_independent_id: cf46a62e-b4a3-a5f1-4dd9-65b73cde0b53
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot/enterprise-iot-get-started.md
site_name: Docs
depot_name: Learn.defender-for-iot
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: enterprise-iot-get-started
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot/enterprise-iot-get-started.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: b9fc1477-a780-f526-327b-d77fa7fe9337
---

# Get started for Enterprise IoT for Microsoft Defender for IoT in the Defender portal - Microsoft Defender for IoT | Microsoft Learn

Enterprise IoT security improves the monitoring and protection of the IoT devices in your network, such as printers, smart TVs, Voice over Internet Protocol (VoIP) devices, conferencing systems and purpose-built, proprietary devices.

The security monitoring includes IoT related vulnerabilities and recommendations that are integrated with your existing Microsoft Defender for Endpoint data. To understand more about the integration between Defender for Endpoint and Defender for IoT, see [enterprise IoT overview](enterprise-iot).

In this article you'll learn how to add enterprise IoT to your Microsoft Defender portal and use the IoT specific security features to protect your IoT environment.

Important

This article discusses Microsoft Defender for IoT in the Defender portal (Preview).

Some features are not yet available in the Defender portal. If you're interested in these features, or you're an existing customer working on the Azure portal, see the [Defender for IoT on Azure documentation](/en-us/azure/defender-for-iot/organizations/overview).

Learn more about the [Defender for IoT management portals](/en-us/defender-for-iot/microsoft-defender-iot#what-are-the-different-management-portals-for-microsoft-defender-for-iot).

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Prerequisites

Before you start, you need:

- IoT devices in your network, visible in the Microsoft Defender portal **Device inventory**
- Access to the Microsoft Defender Portal as a [Security administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator)
- One of the following licenses:

    - A Microsoft 365 E5 (ME5) or E5 Security license. Enterprise IoT security is included in this package and needs to be turned on.
    - Microsoft Defender for Endpoint P2, with an extra, standalone **Microsoft Defender for IoT - EIoT Device License - add-on** license, available for trial or purchase from the Microsoft 365 admin center.

## Add enterprise IoT security in the Defender portal

There are two ways to add enterprise IoT to the Defender portal:

- ME5/ E5 Security customers: Turn on support for enterprise IoT Security in the Defender Portal. For more information, see turn on enterprise IoT security.
- Defender for Endpoint P2 customers: Start with a free trial or purchase standalone, per-device licenses to gain the same IoT-specific security value. For more information, see set up a standalone trial license. To purchase a full license, see purchase the standalone full license.

## Turn on enterprise IoT security for ME5/E5 Security customers

Turn on enterprise IoT security in the Defender portal if you have an ME5 or E5 Security license.

If you have extra devices that aren't covered by your ME5/E5 licenses, you can purchase standalone licenses. For more information, see set up a standalone full license.

**To turn on enterprise IoT security**:

1. In [Microsoft Defender portal](https://security.microsoft.com/), select **Settings** &gt; **Device Discovery** &gt; **Enterprise IoT**.

    Note

    Ensure you have turned on Device Discovery in **Settings** &gt; **Endpoints** &gt; **Advanced Features**.
2. Toggle the Enterprise IoT security option to **On**. For example:

    ![Screenshot of enterprise IoT toggled on in Microsoft Defender portal.](media/enterprise-iot-get-started/eiot-toggle-on.png)

## Set up enterprise IoT security for Defender for Endpoint P2 customers

Customers with a Microsoft Defender for Endpoint P2 license only can use a trial standalone license for enterprise IoT security.

You can also purchase a license using the Microsoft 365 admin center. Before purchasing the license you need to calculate the number of monitored devices in your network to determine how many licenses you need.

### Set up a standalone trial license

Note

After obtaining your licenses, make sure to [assign your licenses to specific users](/en-us/microsoft-365/admin/manage/assign-licenses-to-users) to start using them.

**To start an enterprise IoT trial**:

1. Go to the [Microsoft 365 admin center](https://portal.office.com/AdminPortal/Home#/catalog) &gt; **Marketplace**.
2. Search for the **Microsoft Defender for IoT - EIoT Device License - add-on** and filter the results by **Other services**. For example:

    ![Screenshot of the Marketplace search results for the EIoT Device License.](media/enterprise-iot-get-started/eiot-standalone.png)

    Important

    The prices shown in this image are for example purposes only and are not intended to reflect actual prices.
3. Under **Microsoft Defender for IoT - EIoT Device License - add-on**, select **Details**.
4. On the **Microsoft Defender for IoT - EIoT Device License - add-on** page, select **Start free trial**. On the **Check out** page, select **Try now**.

Tip

Make sure to [assign your licenses to specific users](/en-us/microsoft-365/admin/manage/assign-licenses-to-users) to start using them.

### Set up a standalone full license

Before purchasing a license you must calculate the number of devices you're monitoring.

#### Calculate monitored devices for enterprise IoT security

Use the following procedure to calculate how many devices you need to monitor if:

- You're an ME5/E5 Security customer and think you need to monitor more devices than the devices allocated per ME5/E5 Security license
- You're a Defender for Endpoint P2 customer who's purchasing standalone enterprise IoT licenses

**To calculate the number of devices you're monitoring:**

1. In [Microsoft Defender portal](https://security.microsoft.com/), select **Assets** &gt; **Devices** to open the **Device inventory** page.
2. Note down the total number of **IoT devices** listed.

    For example:

    [![Screenshot of network device and IoT devices in the device inventory in Microsoft Defender for Endpoint.](media/enterprise-iot-get-started/device-inventory-iot.png)](media/enterprise-iot-get-started/device-inventory-iot.png#lightbox)
3. Round your total to a multiple of 100 and compare it against the number of licenses you have. For example:

    - If in Microsoft Defender portal **Device inventory**, you have *1204* IoT devices.
    - Round down to *1200* devices.
    - You have 240 ME5 licenses, which cover **1200** devices.

    You need another **4** standalone devices to cover the gap.

For more information, see the [Defender for Endpoint Device discovery overview](/en-us/microsoft-365/security/defender-endpoint/device-discovery).

Note

Devices listed on the **Computers & Mobile** tab, including those managed by Defender for Endpoint or otherwise, are not included in the number of [identified unique devices](device-discovery#identified-unique-devices) monitored by Defender for IoT.

#### Purchase the standalone license

To purchase the standalone full license:

1. Go to the [Microsoft 365 admin center](https://portal.office.com/AdminPortal/Home#/catalog)**Billing &gt; Purchase services**. If you don't have this option, select **Marketplace** instead.
2. Search for the **Microsoft Defender for IoT - EIoT Device License - add-on** and filter the results by **Other services**. For example:

    ![Screenshot of the Marketplace search results for the EIoT Device License.](media/enterprise-iot-get-started/eiot-standalone.png)

    Important

    The prices shown in this image are for example purposes only and are not intended to reflect actual prices.
3. On the **Microsoft Defender for IoT - EIoT Device License - add-on** page, enter your selected license quantity, select a billing frequency, and then select **Buy**.

For more information, see the [Microsoft 365 admin center help](/en-us/microsoft-365/admin/).