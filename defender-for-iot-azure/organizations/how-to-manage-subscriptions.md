---
layout: Conceptual
title: Manage OT Plans and Licenses - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/how-to-manage-subscriptions
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
description: Manage Microsoft Defender for IoT plans and licenses for OT monitoring.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 928a7031-d289-104e-443a-398acb5a7946
document_version_independent_id: 00a67b26-cd1a-fcd5-9888-6a950d72a8f4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/how-to-manage-subscriptions.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/how-to-manage-subscriptions
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/how-to-manage-subscriptions.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 537541c5-0510-57ee-d3e1-e9b1abb5886b
---

# Manage OT Plans and Licenses - Microsoft Defender for IoT | Microsoft Learn

Your Microsoft Defender for IoT deployment for OT monitoring is managed through a site-based license, purchased in the Microsoft 365 admin center. After you've purchased your license, apply that license to your OT plan in the Azure portal.

If you're looking to manage support for enterprise IoT security, see [Manage enterprise IoT monitoring support with Microsoft Defender for IoT](manage-subscriptions-enterprise).

These licensing and plan-management instructions apply to commercial Defender for IoT customers.

If you're a government customer, contact your Microsoft sales representative for more information.

## Prerequisites

Before performing the procedures in this article, make sure that you have:

- A Microsoft 365 tenant, with access to the [Microsoft 365 admin center](https://portal.office.com/AdminPortal/Home#/catalog) as Global or Billing admin.

    For more information, see [Buy or remove Microsoft 365 licenses for a subscription](/en-us/microsoft-365/commerce/licenses/buy-licenses) and [About admin roles in the Microsoft 365 admin center](/en-us/microsoft-365/admin/add-users/about-admin-roles).
- An Azure subscription. If you need an Azure subscription, [Sign up for a free Azure account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- A [Security admin](/en-us/azure/role-based-access-control/built-in-roles#security-admin), [Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor), or [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) user role for the Azure subscription that you're using for the integration
- An understanding of your site size. For more information, see [Calculate devices in your network](best-practices/plan-prepare-deploy#calculate-devices-in-your-network).

## Purchase a Defender for IoT license

This procedure describes how to purchase Defender for IoT licenses in the Microsoft 365 admin center.

To purchase Defender for IoT licenses:

1. Go to the [Microsoft 365 admin center](https://portal.office.com/AdminPortal/Home#/catalog)**Billing &gt; Purchase services**. If you don't have this option, select **Marketplace** instead.
2. Search for **Defender for IoT**.
3. Choose the license appropriate for the size of your site.
4. Complete the purchasing instructions.

    Make sure to select the number of licenses you want to purchase, based on the number of sites you want to monitor at the selected size.

Important

All license management procedures are done from the Microsoft 365 admin center, including buying, canceling, renewing, setting to auto-renew, auditing, and more. For more information, see the [Microsoft 365 admin center documentation](/en-us/microsoft-365/admin/).

## Add an OT plan to your Azure subscription

This procedure describes how to add an OT plan for Defender for IoT in the Azure portal, based on the Defender for IoT licenses you purchased in the Microsoft 365 admin center (see Purchase a Defender for IoT license).

To add an OT plan in Defender for IoT:

1. In [Defender for IoT](https://portal.azure.com/#view/Microsoft_Azure_IoT_Defender/IoTDefenderDashboard/%7E/Getting_started), select **Plans and pricing** &gt; **Add plan**.
2. In the **Plan settings** pane, select the Azure subscription where you want to add a plan. You can only add a single subscription, and you need a [Security admin](/en-us/azure/role-based-access-control/built-in-roles#security-admin), [Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor), or [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) role for the selected subscription.

    Note

    If your subscription isn't listed, check your account details and confirm your permissions with the subscription owner. Also make sure that you have the right subscriptions selected in your Azure settings &gt; **Directories + subscriptions** page.

    The **Price plan** value is updated automatically to reflect your purchased Microsoft Defender for IoT licenses in Microsoft 365.
3. Select **Next** and review the details for any of your licensed sites. The details listed on the **Review and purchase** pane reflect any licenses you've purchased from the Microsoft 365 admin center.
4. Select the terms and conditions.
5. When you're finished, select **Save**.

Your new plan is listed under the Azure subscription you selected on the **Plans and pricing** &gt; **Plans** page.

## Cancel a Defender for IoT plan for OT networks

You might need to cancel a Defender for IoT plan from your Azure subscription, for example, if you need to work with a different subscription, or if you no longer need the service.

**Prerequisites**: Before canceling your plan, make sure to delete any sensors that are associated with the subscription. For more information, see [Sensor management options from the Azure portal](how-to-manage-sensors-on-the-cloud#sensor-management-options-from-the-azure-portal).

To cancel an OT network plan:

1. In the Azure portal, go to **Defender for IoT** &gt; **Plans and pricing**.
2. On the subscription row, select the options menu (**...**) at the right and select **Cancel plan**.
3. In the cancellation dialog, select **I agree** to cancel the Defender for IoT plan from the subscription.

    Your changes take effect one hour after confirmation.

### Cancel your Defender for IoT licenses

Canceling an OT plan in the Azure portal *doesn't* also cancel your Defender for IoT license. To change your billed licenses, make sure that you also cancel your Defender for IoT license from the Microsoft 365 admin center.

For more information, see the [Cancel a purchase or trial subscription in Microsoft 365](/en-us/microsoft-365/commerce/subscriptions/manage-self-service-purchases-admins#cancel-a-purchase-or-trial-subscription).

## Migrate from a legacy OT plan

If you're an existing customer with a legacy OT plan, we recommend migrating your plan to a site-based Microsoft 365 plan. After you select **Microsoft 365** in the **Price plan** field and save your changes, make sure to update your site details with a site size that matches your Microsoft 365 license.

After migrating your plan to a site-based Microsoft 365 plan, edits are supported only in the Microsoft 365 admin center.

Note

Defender for IoT supports migration for a single subscription only. If you have multiple subscriptions, choose the one you want to migrate, and then move all sensors to that subscription before you update your plan settings.

For more information, see Move existing sensors to a different subscription.

To migrate your plan:

1. Purchase a new, site-based license in the Microsoft 365 Marketplace for the site size that you need. For more information, see Purchase a Defender for IoT license.
2. In Defender for IoT in the Azure portal, go to **Plans and pricing** and locate the subscription for the plan you want to migrate.
3. On the subscription row, select the options menu (**...**) at the right &gt; select **Edit plan**.
4. In the **Price plan** field, select **Microsoft 365 (recommended)** &gt; **Next**. For example:

    ![Screenshot of updating your pricing plan to Microsoft 365.](media/release-notes/migrate-to-365.png)
5. Review your plan details and select **Save**.

To update your site sizes:

1. In Defender for IoT in the Azure portal, select **Sites and sensors** and then select the name of the site you want to migrate.
2. In the **Edit site** pane, in the **Size** field, edit your site size to match your licensed sites. For example:

    ![Screenshot of editing a site size on the Azure portal.](media/release-notes/edit-site-size.png)

## Legacy procedures for plan management in the Azure portal

Starting June 1, 2023, Microsoft Defender for IoT licenses for OT monitoring are available for purchase only in the [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/Home), and OT sensors are onboarded to Defender for IoT based on your licensed site sizes. For more information, see [OT plans billed by site-based licenses](whats-new-archive#ot-plans-billed-by-site-based-licenses).

Existing customers can continue to use any legacy OT plan, with no changes in functionality. For legacy customers, *committed devices* are the number of devices you're monitoring. For more information, see [Devices monitored by Defender for IoT](architecture#devices-monitored-by-defender-for-iot).

### Warnings for exceeding committed devices

If the number of actual devices detected by Defender for IoT exceeds the number of committed devices currently listed on your subscription, you might see a warning message in the Azure portal and on your OT sensor that you have exceeded the maximum number of devices for your subscription.

The exceeded-device-limit warning indicates that you need to update the number of committed devices on the affected subscription to match the actual number of devices being monitored. Select the link in the warning message to take you to the **Plans and pricing** page, with the **Edit plan** pane already open.

### Move existing sensors to a different subscription

If you have multiple legacy subscriptions and are migrating to a Microsoft 365 plan, you'll first need to consolidate your sensors to a single subscription. To consolidate your sensors, register the sensors under the new subscription and remove them from the original subscription.

- Devices are synchronized automatically from each sensor to the new subscription.
- Manual edits made in the portal aren't migrated.
- New alerts created by each sensor are created under the new subscription, and existing alerts in the old subscription can be closed in bulk.

To move sensors to a different subscription:

1. In the Azure portal, for each sensor you want to move, [onboard the sensor](onboard-sensors) from scratch to the new subscription in order to create a new activation file. When onboarding each sensor:

    - Replicate the existing site and sensor hierarchy from the original subscription.
    - For sensors monitoring overlapping network segments, create the activation file under the same zone. Identical devices that are detected in more than one sensor in a zone are merged into one device.
2. On your sensor, upload the new activation file.
3. Delete the sensor identities from the previous subscription. For more information, see [Site management options from the Azure portal](how-to-manage-sensors-on-the-cloud#site-management-options-from-the-azure-portal).
4. If relevant, cancel the Defender for IoT plan from the previous subscription. For more information, see Cancel a Defender for IoT plan for OT networks.

### Edit a legacy plan on the Azure portal

Use the following steps to edit a legacy Defender for IoT plan in the Azure portal.

1. In the Azure portal, go to **Defender for IoT** &gt; **Plans and pricing**.
2. On the subscription row, select the options menu (**...**) at the right &gt; select **Edit plan**.
3. Make any of the following changes as needed:

    - Change your price plan to a monthly, annual, or Microsoft 365 plan
    - Update the number of [committed devices](best-practices/plan-prepare-deploy#calculate-devices-in-your-network) (monthly and annual plans only)
    - Update the number of sites (annual plans only)
4. Select the **I accept the terms and conditions** option, and then select **Save**.
5. After any changes are made, make sure to reactivate your sensors. For more information, see [Reactivate an OT sensor](how-to-manage-sensors-on-the-cloud#reactivate-an-ot-sensor).

Changes to your plan take effect one hour after confirming the change. This change appears on your next monthly statement, and you're charged based on the length of time each plan was in effect.