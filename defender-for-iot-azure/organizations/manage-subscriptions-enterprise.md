---
layout: Conceptual
title: Manage EIoT monitoring support - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/manage-subscriptions-enterprise
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
description: Calculate detected enterprise IoT devices to assess standalone licensing needs and learn how to cancel EIoT monitoring support in Microsoft Defender for IoT.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom:
- msecd-doc-authoring-1014
- enterprise-iot
- sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: dd047512-f05a-0807-b469-c9e7d1ab1e1d
document_version_independent_id: d1580c5b-a6ef-06bc-2a8f-83e698e29e3e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/manage-subscriptions-enterprise.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/manage-subscriptions-enterprise
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/manage-subscriptions-enterprise.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: a44e095e-14d0-d53e-d9fb-8aab533012c4
---

# Manage EIoT monitoring support - Microsoft Defender for IoT | Microsoft Learn

Enterprise IoT security monitoring with Defender for IoT is supported by a Microsoft 365 E5 (ME5) or E5 Security license, or extra standalone, per-device licenses purchased as add-ons to Microsoft Defender for Endpoint.

This article describes how to:

- Calculate the devices detected in your environment so that you can understand if you need extra, standalone licenses.
- Cancel support for enterprise IoT monitoring with Microsoft Defender for IoT.

If you're looking to manage OT plans, see [Manage Defender for IoT plans for OT security monitoring](how-to-manage-subscriptions).

## Prerequisites

Before performing the procedures in this article, make sure that you have:

- One of the following sets of licenses:

    - A Microsoft 365 E5 (ME5) or E5 Security license and a Microsoft Defender for Endpoint P2 license
    - A Microsoft Defender for Endpoint P2 license alone

        For more information, see [Enterprise IoT security in Microsoft Defender XDR](concept-enterprise#enterprise-iot-security-in-microsoft-defender-xdr).
- Access to the Microsoft Defender Portal as a [Security administrator](/en-us/azure/active-directory/roles/permissions-reference#security-administrator)

## Obtain a standalone Enterprise IoT trial license

This procedure describes how to start using a trial, standalone license for enterprise IoT monitoring, for customers who have a Microsoft Defender for Endpoint P2 license only.

Customers with ME5/E5 Security plans have support for enterprise IoT monitoring included in the license and need to turn it on in the Defender portal. They don't need to start a trial. For more information, see [Get started with enterprise IoT monitoring in Microsoft Defender](eiot-defender-for-endpoint).

Start your enterprise IoT trial using the [Microsoft Defender for IoT - EIoT Device License - add-on wizard](https://signup.microsoft.com/get-started/signup?products=b2f91841-252f-4765-94c3-75802d7c0ddb&amp;ali=1&amp;bac=1) or via the Microsoft 365 admin center.

To start an Enterprise IoT trial:

1. Go to the [Microsoft 365 admin center](https://portal.office.com/AdminPortal/Home#/catalog) &gt; **Marketplace**.
2. Search for the **Microsoft Defender for IoT - EIoT Device License - add-on** and filter the results by **Other services**. For example:

    ![Screenshot of the Marketplace search results for the EIoT Device License.](media/enterprise-iot/eiot-standalone.png)

    Important

    The prices shown in this image are for example purposes only and are not intended to reflect actual prices.
3. Under **Microsoft Defender for IoT - EIoT Device License - add-on**, select **Details**.
4. On the **Microsoft Defender for IoT - EIoT Device License - add-on** page, select **Start free trial**. On the **Check out** page, select **Try now**.

Tip

Make sure to [assign your licenses to specific users](/en-us/microsoft-365/admin/manage/assign-licenses-to-users) to start using them.

For more information, see [Enterprise IoT free trial](billing#enterprise-iot-free-trial).

## Calculate monitored devices for Enterprise IoT monitoring

Use the following procedure to calculate how many devices you need to monitor if:

- You're an ME5/E5 Security customer and thinks you need to monitor more devices than the devices allocated per ME5/E5 Security license
- You're a Defender for Endpoint P2 customer who's purchasing standalone enterprise IoT licenses

To calculate the number of devices you're monitoring::

1. In the [Defender portal](https://security.microsoft.com/), select **Assets** &gt; **Devices** to open the **Device inventory** page.
2. Note down the total number of **IoT devices** listed.

    For example:

    [![Screenshot of network device and IoT devices in the device inventory in Microsoft Defender for Endpoint.](media/how-to-manage-subscriptions/device-inventory-iot.png)](media/how-to-manage-subscriptions/device-inventory-iot.png#lightbox)
3. Round your total to a multiple of 100 and compare the rounded total against the number of licenses you have.

For example:

- If in the Defender portal **Device inventory**, you have *1204* IoT devices.
- Round down to *1200* devices.
- You have 240 ME5 licenses, which cover **1200** devices

You need another **4** standalone devices to cover the gap.

For more information, see the [Defender for Endpoint Device discovery overview](/en-us/microsoft-365/security/defender-endpoint/device-discovery).

Note

Devices listed on the **Computers & Mobile** tab, including those managed by Defender for Endpoint or otherwise, are not included in the number of [devices](billing#defender-for-iot-devices) monitored by Defender for IoT.

## Purchase standalone licenses

Purchase standalone, per-device licenses if you're an ME5/E5 Security customer who needs more than the five devices allocated per license, or if you're a Defender for Endpoint customer who wants to add enterprise IoT security to your organization.

To purchase standalone licenses:

1. Go to the [Microsoft 365 admin center](https://portal.office.com/AdminPortal/Home#/catalog)**Billing &gt; Purchase services**. If you don't have this option, select **Marketplace** instead.
2. Search for the **Microsoft Defender for IoT - EIoT Device License - add-on** and filter the results by **Other services**. For example:

    ![Screenshot of the Marketplace search results for the EIoT Device License.](media/enterprise-iot/eiot-standalone.png)

    Important

    The prices shown in this image are for example purposes only and are not intended to reflect actual prices.
3. On the **Microsoft Defender for IoT - EIoT Device License - add-on** page, enter your selected license quantity, select a billing frequency, and then select **Buy**.

For more information, see the [Microsoft 365 admin center help](/en-us/microsoft-365/admin/).

## Turn off enterprise IoT security

This procedure describes how to turn off enterprise IoT monitoring in the Defender portal, and is supported only for customers who don't have any standalone, per-device licenses added on to Microsoft Defender.

Turn off the **Enterprise IoT security** option if you're no longer using the service.

Warning

Turning off Enterprise IoT security stops all purpose-built alerts, vulnerabilities, and recommendations in Microsoft Defender.

To turn off enterprise IoT monitoring:

1. In the [Defender portal](https://security.microsoft.com/), select **Settings** &gt; **Device discovery** &gt; **Enterprise IoT**.
2. Toggle the option to **Off**.

You stop getting security value in Microsoft Defender, including purpose-built alerts, vulnerabilities, and recommendations.

### Cancel a legacy Enterprise IoT plan

If you have a legacy Enterprise IoT plan, are *not* an ME5/E5 Security customer, and no longer use the service, cancel your plan as follows:

1. In the [Defender portal](https://security.microsoft.com/), select **Settings** &gt; **Device discovery** &gt; **Enterprise IoT**.
2. Select **Cancel plan**. The **Cancel plan** page is available only for legacy Enterprise IoT plan customers.

After you cancel your plan, the integration stops and you'll no longer get added security value in Microsoft Defender, or detect new Enterprise IoT devices in Defender for IoT.

The cancellation takes effect one hour after confirming the change. This change appears on your next monthly statement, and you're charged based on the length of time the plan was in effect.