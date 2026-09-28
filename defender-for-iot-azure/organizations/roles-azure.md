---
layout: Conceptual
title: Azure user roles and permissions for Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/roles-azure
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
description: Learn about the Azure user roles and permissions available for OT and Enterprise IoT monitoring with Microsoft Defender for IoT on the Azure portal.
ms.date: 2023-10-22T00:00:00.0000000Z
ms.topic: concept-article
ms.custom: enterprise-iot
ms.collection:
- zerotrust-extra
locale: en-us
document_id: 6f8f12f4-a888-e00a-411a-e1e4feb80ec0
document_version_independent_id: 8a8d1e16-03cf-814d-6d34-a8f074647f3d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/roles-azure.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/roles-azure
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/roles-azure.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 5e5fd7a1-bf71-1c30-a028-c4039f0ea273
---

# Azure user roles and permissions for Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn

Microsoft Defender for IoT uses [Azure Role-Based Access Control (RBAC)](/en-us/azure/role-based-access-control/) to provide access to Defender for IoT monitoring services and data on the Azure portal.

The built-in Azure [Security Reader](/en-us/azure/role-based-access-control/built-in-roles#security-reader), [Security Admin](/en-us/azure/role-based-access-control/built-in-roles#security-admin), [Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor), and [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) roles are relevant for use in Defender for IoT.

This article provides a reference of Defender for IoT actions available for each role in the Azure portal. For more information, see [Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles).

## Roles and permissions reference

Permissions are applied to user roles across an entire Azure subscription, or in some cases, across individual Defender for IoT sites. For more information, see [Zero Trust and your OT networks](concept-zero-trust) and [Manage site-based access control (Public preview)](manage-users-portal#manage-site-based-access-control-public-preview).

| Action and scope | [Security Reader](/en-us/azure/role-based-access-control/built-in-roles#security-reader) | [Security Admin](/en-us/azure/role-based-access-control/built-in-roles#security-admin) | [Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor) | [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) |
| --- | --- | --- | --- | --- |
| **[Grant permissions to others](manage-users-portal)**Apply per subscription or site | - | - | - | ✔ |
| **Onboard [OT](onboard-sensors) or [Enterprise IoT sensors](eiot-sensor)**Apply per subscription only | - | ✔ | ✔ | ✔ |
| **[Download OT sensor software](update-ot-software#download-the-update-package-from-the-azure-portal)**Apply per subscription only | ✔ | ✔ | ✔ | ✔ |
| **[Download sensor endpoint details](how-to-manage-sensors-on-the-cloud#endpoint)**Apply per subscription only | ✔ | ✔ | ✔ | ✔ |
| **[Download sensor activation files](how-to-manage-sensors-on-the-cloud#reactivate-an-ot-sensor)**Apply per subscription only | - | ✔ | ✔ | ✔ |
| **[View values on the Plans and pricing page](how-to-manage-subscriptions)**Apply per subscription only | ✔ | ✔ | ✔ | ✔ |
| **[Modify values on the Plans and pricing page](how-to-manage-subscriptions)**Apply per subscription only | - | ✔ | ✔ | ✔ |
| **[View values on the Sites and sensors page](how-to-manage-sensors-on-the-cloud)**Apply per subscription only | ✔ | ✔ | ✔ | ✔ |
| **[Modify values on the Sites and sensors page](how-to-manage-sensors-on-the-cloud#sensor-management-options-from-the-azure-portal)** , including remote OT sensor updatesApply per subscription only | - | ✔ | ✔ | ✔ |
| **[Recover OT sensor passwords](how-to-manage-sensors-on-the-cloud#sensor-deployment-and-access)**Apply per subscription only | - | ✔ | ✔ | ✔ |
| **[Download OT threat intelligence packages](how-to-work-with-threat-intelligence-packages#manually-update-locally-managed-sensors)**Apply per subscription only | ✔ | ✔ | ✔ | ✔ |
| **[Push OT threat intelligence updates](how-to-work-with-threat-intelligence-packages#manually-push-updates-to-cloud-connected-sensors)**Apply per subscription only | - | ✔ | ✔ | ✔ |
| **[View Azure alerts](how-to-manage-cloud-alerts)**Apply per subscription or site | ✔ | ✔ | ✔ | ✔ |
| **[Modify Azure alerts](how-to-manage-cloud-alerts) (write access - change status, learn, download PCAP, suppression rules)**Apply per subscription or site | - | ✔ | ✔ | ✔ |
| **[View Azure device inventory](how-to-manage-device-inventory-for-organizations)**Apply per subscription or site | ✔ | ✔ | ✔ | ✔ |
| **[Manage Azure device inventory](how-to-manage-device-inventory-for-organizations) (write access)**Apply per subscription or site | - | ✔ | ✔ | ✔ |
| **[View Azure workbooks](workbooks)**Apply per subscription or site | ✔ | ✔ | ✔ | ✔ |
| **[Manage Azure workbooks](workbooks) (write access)**Apply per subscription or site | - | ✔ | ✔ | ✔ |
| **[View Defender for IoT settings](configure-sensor-settings-portal)**Apply per subscription | ✔ | ✔ | ✔ | ✔ |
| **[Configure Defender for IoT settings](configure-sensor-settings-portal)**Apply per subscription | - | ✔ | ✔ | ✔ |

For an overview on creating new Azure custom roles, see [Azure custom roles](/en-us/azure/role-based-access-control/custom-roles). To set up a role, you need to add permissions from the actions listed in the [Internet of Things security permissions table](/en-us/azure/role-based-access-control/permissions/internet-of-things#microsoftiotsecurity).

Important

After adding a new subscription to Defender for IoT, the initial login for that subscription must be performed using either the Owner or Contributor roles. For all subsequent logins the Security Admin role is sufficient.