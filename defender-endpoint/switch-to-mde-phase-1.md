---
layout: Conceptual
title: Migrate to Microsoft Defender for Endpoint - Prepare - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/switch-to-mde-phase-1
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Prepare to migrate to Microsoft Defender for Endpoint by updating devices, confirming licenses, configuring portal access, and reviewing connectivity requirements.
ms.service: defender-endpoint
ms.subservice: onboard
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- m365solution-migratetomdatp
- highpri
- tier1
ms.topic: how-to
ms.custom:
- msecd-doc-authoring-1015
- migrationguides
- admindeeplinkDEFENDER
ms.date: 2026-09-15T00:00:00.0000000Z
ms.reviewer: jesquive, chventou, jonix, chriggs, owtho, yongrhee
ai-usage: ai-assisted
locale: en-us
document_id: f148372b-1055-b99f-e643-e954f7f6cdf5
document_version_independent_id: f148372b-1055-b99f-e643-e954f7f6cdf5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/switch-to-mde-phase-1.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: switch-to-mde-phase-1
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/switch-to-mde-phase-1.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: b1b0aff8-a23d-e5d5-8cdd-25e3f905e138
---

# Migrate to Microsoft Defender for Endpoint - Prepare - Microsoft Defender for Endpoint | Microsoft Learn

Prepare your organization to migrate to Defender for Endpoint by updating devices, confirming licenses, configuring portal access, reviewing connectivity, and capturing baseline performance data before onboarding.

## Phase 1: Prepare

| ![Diagram of migration phases highlighting Phase 1: Prepare as the current step.](media/phase-diagrams/prepare.png#lightbox)Phase 1: Prepare | [![Diagram of migration phases highlighting Phase 2: Set up.](media/phase-diagrams/setup.png#lightbox)](switch-to-mde-phase-2)[Phase 2: Set up](switch-to-mde-phase-2) | [![Diagram of migration phases highlighting Phase 3: Onboard.](media/phase-diagrams/onboard.png#lightbox)](switch-to-mde-phase-3)[Phase 3: Onboard](switch-to-mde-phase-3) |
| --- | --- | --- |
| *You're here!* |  |  |

**Welcome to the Prepare phase of [migrating to Defender for Endpoint](switch-to-mde-overview#the-migration-process)**.

In this phase, you prepare your environment before you set up and onboard Defender for Endpoint.

This migration phase includes the following steps:

1. Update your organization's devices.
2. Get Microsoft Defender for Endpoint Plan 1 or Plan 2.
3. Grant access to the Microsoft Defender portal.
4. Review device proxy and internet connectivity settings.
5. Capture endpoint performance baseline data.

Important

If you want to run multiple security solutions side by side, see [Considerations for performance, configuration, and support](/en-us/defender-endpoint/mde-side-by-side).

You might have already configured mutual security exclusions for devices onboarded to Microsoft Defender for Endpoint. If you still need to set mutual exclusions to avoid conflicts, see [Add Microsoft Defender for Endpoint to the exclusion list for your existing solution](/en-us/defender-endpoint/switch-to-mde-phase-2#step-2-add-microsoft-defender-for-endpoint-to-the-exclusion-list-for-your-existing-solution).

## Step 1: Update your organization's devices

Before migration, update your existing endpoint protection solution, operating systems, and apps. Current software and security updates can help prevent compatibility and deployment problems when you introduce Microsoft Defender Antivirus.

### Update your existing security solution

Install the latest updates for your existing endpoint protection solution. Review your solution provider's documentation for update requirements and procedures.

### Update your organization's devices

Use the following resources to update operating systems:

| OS | Resource |
| --- | --- |
| Windows | [Microsoft Update](/en-us/windows/deployment/update/how-windows-update-works) |
| macOS | [How to update the software on your macOS devices](https://support.apple.com/HT201541) |
| iOS | [Update your iPhone, iPad, or iPod touch](https://support.apple.com/HT204204) |
| Android | [Check & update your Android version](https://support.google.com/android/answer/7680439) |
| Linux | [Linux 101: Updating Your System](https://www.linux.com/training-tutorials/linux-101-updating-your-system) |

## Step 2: Get Microsoft Defender for Endpoint Plan 1 or Plan 2

Get Defender for Endpoint, assign the required licenses, and verify that the service is provisioned.

1. Buy or try Defender for Endpoint today. [Start a free trial or request a quote](https://aka.ms/mdatp). For current licensing information, see [Microsoft Defender for Endpoint licensing guidance](/en-us/office365/servicedescriptions/microsoft-365-service-descriptions/microsoft-365-tenantlevel-services-licensing-guidance#microsoft-defender-for-endpoint).
2. Verify that your licenses are provisioned. See [Check your license state](production-deployment#check-your-license-state).
3. Set up your dedicated cloud instance of Defender for Endpoint. See [Defender for Endpoint setup: Tenant configuration](production-deployment#tenant-configuration).
4. If any devices in your organization use a proxy to access the internet, follow the guidance in [Defender for Endpoint setup: Network configuration](production-deployment#network-configuration).

After you provision licenses and configure your Defender for Endpoint organization, grant your security administrators and security operators access to the [Microsoft Defender portal](https://security.microsoft.com).

## Step 3: Grant access to the Microsoft Defender portal

The [Microsoft Defender portal](https://security.microsoft.com) is where you and your security team access and configure features and capabilities of Defender for Endpoint. For an overview of portal features and navigation, see [Overview of the Microsoft Defender portal](/en-us/defender-xdr/microsoft-365-defender-portal).

Use Microsoft Defender unified role-based access control (RBAC) to provide centralized, granular permissions to the Microsoft Defender portal.

Important

Starting February 16, 2025, new Microsoft Defender for Endpoint customers have access only to Unified Role-Based Access Control (URBAC). Existing customers retain their current roles and permissions. For more information, see [Microsoft Defender unified role-based access control](/en-us/defender-xdr/manage-rbac).

To grant portal access, complete the steps that apply to your organization's permissions model:

1. Plan the roles and permissions for your security administrators and security operators. See [Role-based access control](prepare-deployment#role-based-access-control).
2. Configure access to the Microsoft Defender portal:

    - If your organization uses unified RBAC, on the **Permissions and roles** page in the Microsoft Defender portal at https://security.microsoft.com/mtp_roles, [create custom roles](/en-us/defender-xdr/create-custom-rbac-roles), assign the roles to users or Microsoft Entra security groups, and [activate the applicable Defender workloads](/en-us/defender-xdr/activate-defender-rbac).
    - If your organization retains the Defender for Endpoint RBAC model, see [Manage portal access using role-based access control](rbac).

## Step 4: Review device proxy and internet connectivity settings

Your devices might require proxy or internet settings to communicate with Defender for Endpoint. Use the following resources for each operating system and subscription:

| Subscription | Operating systems | Resources |
| --- | --- | --- |
| [Defender for Endpoint Plan 1](defender-endpoint-plan-1) | [Windows 11](/en-us/windows/whats-new/windows-11-overview)[Windows 10](/en-us/windows/release-health/release-information)[Windows Server 1803 or later](/en-us/windows-server/get-started/whats-new-in-windows-server-1803)[Windows Server 2016 and later](/en-us/windows-server/get-started/whats-new-in-windows-server-2016)\*[Windows Server 2012 R2](/en-us/windows/release-health/status-windows-8.1-and-windows-server-2012-r2)\*Azure Local nodes running Azure Stack HCI OS, version 23H2 and later | [Configure and validate Microsoft Defender Antivirus network connections](configure-network-connections-microsoft-defender-antivirus) |
| [Defender for Endpoint Plan 1](defender-endpoint-plan-1) | macOS (see [System requirements](microsoft-defender-endpoint-mac-prerequisites)) | [Defender for Endpoint on macOS: Network connections](microsoft-defender-endpoint-mac-prerequisites#network-connectivity) |
| [Defender for Endpoint Plan 1](defender-endpoint-plan-1) | Linux (see [System requirements](mde-linux-prerequisites)) | [Verify that devices can connect to Defender for Endpoint cloud services](mde-linux-prerequisites#verify-if-devices-can-connect-to-defender-for-endpoint-cloud-services) |
| [Defender for Endpoint Plan 2](microsoft-defender-endpoint) | [Windows 11](/en-us/windows/whats-new/windows-11-overview)[Windows 10](/en-us/windows/release-health/release-information)Azure Local nodes running Azure Stack HCI OS, version 23H2 and later[Windows Server 1803 or later](/en-us/windows-server/get-started/whats-new-in-windows-server-1803)[Windows Server 2016 and later](/en-us/windows/release-health/status-windows-10-1607-and-windows-server-2016)[Windows Server 2012 R2](/en-us/windows/release-health/status-windows-8.1-and-windows-server-2012-r2) | [Configure machine proxy and internet connectivity settings](configure-proxy-internet) |
| [Defender for Endpoint Plan 2](microsoft-defender-endpoint) | [Windows Server 2008 R2 SP1](/en-us/windows/release-health/status-windows-7-and-windows-server-2008-r2-sp1)[Windows 8.1](/en-us/windows/release-health/status-windows-8.1-and-windows-server-2012-r2)[Windows 7 SP1](/en-us/windows/release-health/status-windows-7-and-windows-server-2008-r2-sp1) | [Configure proxy and internet connectivity settings](onboard-downlevel#configure-proxy-and-internet-connectivity-settings) |
| [Defender for Endpoint Plan 2](microsoft-defender-endpoint) | macOS (see [System requirements](microsoft-defender-endpoint-mac)) | [Defender for Endpoint on macOS: Network connections](microsoft-defender-endpoint-mac-prerequisites#network-connectivity) |

\* Windows Server 2016 and Windows Server 2012 R2 require the modern unified solution. For more information, see [Onboard Windows Server 2012 R2 and Windows Server 2016 to Microsoft Defender for Endpoint](onboard-server).

Important

The standalone versions of Defender for Endpoint Plan 1 and Plan 2 don't include server licenses. To onboard servers, you need a server license, such as [Microsoft Defender for Servers Plan 1 or Plan 2](/en-us/azure/defender-for-cloud/plan-defender-for-servers-select-plan). For more information, see [Defender for Endpoint onboarding Windows Server](onboard-windows-server).

## Step 5: Capture endpoint performance baseline data

Before migration, capture baseline performance data from endpoints that will run Defender for Endpoint. Comparing performance before and after onboarding helps you distinguish existing resource usage from changes that might be associated with Microsoft Defender Antivirus.

Collect the process list, aggregate CPU usage, memory usage, and available disk space on all mounted partitions.

Use Windows Performance Monitor (`perfmon`) to collect a performance baseline on Windows client devices or Windows Server. For instructions, see [Set up local Performance Monitor on a Windows client or Windows Server](/en-us/archive/blogs/yongrhee/setting-a-local-perfmon-in-a-windows-client-or-windows-server).