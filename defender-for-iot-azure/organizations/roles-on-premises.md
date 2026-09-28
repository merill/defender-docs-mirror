---
layout: Conceptual
title: On-premises users and roles for Defender for IoT - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/roles-on-premises
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
description: Learn about the on-premises user roles available for OT monitoring with Microsoft Defender for IoT network sensors.
ms.date: 2023-12-19T00:00:00.0000000Z
ms.topic: concept-article
locale: en-us
document_id: a8ba49fc-0c23-cb00-51db-e29392eedbf0
document_version_independent_id: 8428c53f-9b25-d9d3-5693-e72ad632991e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/roles-on-premises.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/roles-on-premises
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/roles-on-premises.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 2eed8c17-b2ae-0a11-5539-18a5edb4426b
---

# On-premises users and roles for Defender for IoT - Microsoft Defender for IoT | Microsoft Learn

When working with OT networks, Defender for IoT services and data is available from on-premises OT network sensors, in addition to Azure.

This article provides:

- A description of the default, privileged users that come with Defender for IoT software installation
- A reference of the actions available for each on-premises user role, on both OT network sensors

Important

Defender for IoT now recommends using Microsoft cloud services or existing IT infrastructure for central monitoring and sensor management, and [plans to retire the on-premises management console](whats-new-archive#new-architecture-for-hybrid-and-air-gapped-support) on **January 1st, 2025**.

For more information, see [Deploy hybrid or air-gapped OT sensor management](ot-deploy/air-gapped-deploy).

## Default privileged on-premises users

By default, each sensor is installed with a default, privileged *admin* user, with access to advanced tools for troubleshooting and setup, such as the CLI.

When first setting up your sensor, sign in with the *admin* user, create an initial user with an **Admin** role, and then use that admin user to create other users with other roles.

For more information, see:

- [Install OT monitoring software on OT sensors](ot-deploy/install-software-ot-sensor)
- [Configure and activate your OT sensor](ot-deploy/activate-deploy-sensor)
- [Create and manage users on an OT network sensor](manage-users-sensor)

### Legacy users

| Legacy scenario | Description |
| --- | --- |
| **Sensor versions earlier than 23.2.0** | In sensor versions earlier than [23.2.0](whats-new-archive#default-privileged-user-is-now-admin-instead-of-support), the default *admin* user is named *support*. The *support* user is available and supported only on versions earlier than 23.2.0.Documentation refers to the *admin* user to match the latest version of the software. |
| **Sensor software versions earlier than 23.1.x** | In sensor software versions earlier than [23.1.x]whats-new-archive.md#july-2023), the *cyberx* and *cyberx\_host* privileged users are also in use. In newly installed versions 23.1.x and higher, the *cyberx* and *cyberx\_host* users are available, but not enabled by default. To enable these extra privileged users, such as to use the [Defender for IoT CLI](references-work-with-defender-for-iot-cli-commands), change their passwords. For more information, see [Recover privileged access to a sensor](manage-users-sensor#recover-privileged-access-to-a-sensor). |
| **On-premises management consoles** | The [on-premises management console](legacy-central-management/install-software-on-premises-management-console) is installed with privileged *support* and *cyberx* users.  When first setting up an on-premises management console, first sign in with the *support* user, create an initial user with an **Admin** role, and then use that admin user to create other users with other roles. |

### Access per privileged user

The following table describes the access available to each privileged user, including legacy users.

| Name | Connects to | Permissions |
| --- | --- | --- |
| **admin** | The OT sensor's `configuration shell` | A powerful administrative account with access to: - All CLI commands - The ability to manage log files - Start and stop services- View the sensor Support pageThis user has no filesystem access. In legacy software versions, this user is named *support*. |
| **cyberx** | The OT sensor's `terminal (root)` | Serves as a root user and has unlimited privileges on the appliance. Used only for the following tasks:- Change default passwords- Troubleshoot- Filesystem access- View the sensor Support page |
| **cyberx\_host** | The OT sensor's host OS `terminal (root)` | Serves as a root user and has unlimited privileges on the appliance host OS.Used for: - Network configuration- Application container control - Filesystem access |

## On-premises user roles

The following roles are available on OT network sensors:

| Role | Description |
| --- | --- |
| **Admin** | Admin users have access to all tools, including system configurations, creating and managing users, and more. |
| **Security Analyst** | Security Analysts don't have admin-level permissions for configurations, but can perform actions on devices, acknowledge alerts, and use investigation tools. Security Analysts can access options on the sensor displayed in the **Discover** and **Analyze** menus on the sensor. |
| **Read-Only** | Read-only users perform tasks such as viewing alerts and devices on the device map. Read-Only users can access options displayed in the **Discover** and **Analyze** menus on the sensor, in read-only mode |

When first deploying an OT monitoring system, sign in to your sensors with one of the default, privileged users described above. Create your first **Admin** user, and then use that user to create other users and assign them to roles.

See the tables below for the permissions available for each role on the sensor.

## Role-based permissions for OT network sensors

To view role-based permissions, see Access per privileged user.

| Permission | Read Only | Security Analyst | Admin |
| --- | --- | --- | --- |
| **View the dashboard** | ✔ | ✔ | ✔ |
| **Control map zoom views** | - | - | ✔ |
| **View alerts** | ✔ | ✔ | ✔ |
| **Manage alerts**: acknowledge, learn, and mute | - | ✔ | ✔ |
| **View events in a timeline** | ✔ | ✔ | ✔ |
| **Authorize devices**, known scanning devices, programming devices | - | ✔ | ✔ |
| **Merge and delete devices** | - | - | ✔ |
| **View investigation data** | ✔ | ✔ | ✔ |
| **Manage system settings** | - | - | ✔ |
| **Manage users** | - | - | ✔ |
| **Change passwords** | - | - | ✔* |
| **DNS servers for reverse lookup** | - | - | ✔ |
| **Send alert data to partners** | - | ✔ | ✔ |
| **Create alert comments** | - | ✔ | ✔ |
| **View programming change history** | ✔ | ✔ | ✔ |
| **Create customized alert rules** | - | ✔ | ✔ |
| **Manage multiple notifications simultaneously** | - | ✔ | ✔ |
| **Manage certificates** | - | - | ✔ |

Note

**Admin** users can only change passwords for themselves or for other users with the **Security Analyst** and **Read-only** roles.