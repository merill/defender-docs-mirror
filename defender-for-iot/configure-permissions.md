---
layout: Conceptual
title: Configure the permissions needed for Microsoft Defender for IoT in the Defender portal - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-iot/configure-permissions
breadcrumb_path: /defender-for-iot/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Configure RBAC roles and permissions for Microsoft Defender for IoT in the Defender portal, including how to review, adjust, and extend access for IoT alerts, incidents, device inventory, and vulnerabilities.
ms.service: defender-for-iot
author: limwainstein
ms.author: lwainstein
ms.localizationpriority: medium
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ms.custom: sfi-ga-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 23ce6765-2b4d-0d04-0b79-0ed6804aa576
document_version_independent_id: 23ce6765-2b4d-0d04-0b79-0ed6804aa576
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot/configure-permissions.md
site_name: Docs
depot_name: Learn.defender-for-iot
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-permissions
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot/configure-permissions.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: cc9ce7db-975f-1ebd-7541-b715845761fb
---

# Configure the permissions needed for Microsoft Defender for IoT in the Defender portal - Microsoft Defender for IoT | Microsoft Learn

## Overview of Defender for IoT roles and permissions

The Microsoft Defender portal allows granular access to features and data based on user roles and the permissions given to each user with Role-Based Access Control (RBAC).

Microsoft Defender for IoT is part of the Defender portal and user access permissions for alerts, incidents, device inventory, device groups and vulnerabilities should already be configured. Nevertheless, with the added features of Defender for IoT you might want to check, adjust or add to the existing roles and permissions of your team in the Defender portal.

This article shows you how to make general changes to RBAC roles and permissions that relate to all areas of Defender for IoT in the Defender portal. Before you begin, make sure you meet the prerequisites. To set up roles and permissions specifically for site security, see [set up RBAC permissions for site security](set-up-rbac).

Important

This article discusses Microsoft Defender for IoT in the Defender portal (Preview).

Some features are not yet available in the Defender portal. If you're interested in these features, or you're an existing customer working on the Azure portal, see the [Defender for IoT on Azure documentation](/en-us/azure/defender-for-iot/organizations/overview).

Learn more about the [Defender for IoT management portals](/en-us/defender-for-iot/microsoft-defender-iot#what-are-the-different-management-portals-for-microsoft-defender-for-iot).

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Prerequisites

Before you begin, make sure you have the following:

- Review [the general prerequisites for Microsoft Defender for IoT](prerequisites).
- Details of all users to be assigned updated roles and permissions for the Defender portal.

## Access management options

Depending on whether your organization uses Microsoft Entra global roles or Microsoft Defender unified RBAC, you can manage user access to the Defender portal in one of two ways. Each system has different named permissions that allow access for Defender for IoT. The two systems are:

- [Global Microsoft Entra roles](/en-us/entra/identity/role-based-access-control/permissions-reference).
- [Microsoft Defender unified RBAC](/en-us/defender-xdr/custom-roles): Use Microsoft Defender unified role-based access control (RBAC) to manage access to specific data, tasks, and capabilities in the Defender portal.

The following role-assignment procedure and permission mappings apply to Defender unified RBAC roles for features in Defender for IoT.

### RBAC for version 1 or 2 only

Depending on your Microsoft Defender tenant configuration, you might have access to RBAC version 1 or 2 instead of Defender unified RBAC. Assign RBAC permissions and roles, based on the summary of roles and permissions for Defender for IoT features later in this article (covering alerts, incidents, vulnerabilities, inventory, and device groups), to give users access to general Defender for IoT features. However, follow the instructions in [Defender for Endpoint deployment guidance for RBAC version 1](/en-us/defender-endpoint/prepare-deployment), or [Defender for Endpoint permission options for RBAC version 2](/en-us/defender-endpoint/user-roles#permission-options).

If you're using the Defender portal for the first time, you need to set up all of your roles and permissions. For more information, see [manage portal access using role-based access control](/en-us/defender-xdr/manage-rbac).

## Defender unified RBAC roles for features in Defender for IoT

Use Defender unified role-based access control (RBAC) to assign permissions and roles that give users access to general Defender for IoT features. Based on the roles and permissions summary for Defender for IoT features, assign the appropriate roles:

1. In the Defender portal, either:

    1. Select **Settings** &gt; **Microsoft XDR** &gt; **Permissions and roles**.

        1. Enable **Endpoints & Vulnerability Management**.
        2. Select **Go to Permissions and roles**.
    2. Select **Permissions** &gt; **Microsft Defender XDR (1)** &gt; **Roles**.
2. Select **Create custom role**.
3. Type a **Role name**, and select **Next** for **Permissions**.

    [![Screenshot of the permissions set up page with the categories of permissions for site security](media/permissions/permissions-choose.png)](media/permissions/permissions-choose.png#lightbox)
4. Select **Security operations**, select the permissions as needed, and select **Apply**.
5. Select **Security posture**, select the permissions as needed, and select **Apply**.
6. Select **Authorization and settings**, select the permissions as needed, and select **Apply**.

    [![Screenshot of the permissions set up page with the specific permissions chosen for site security](media/permissions/permissions-choose-options.png)](media/permissions/permissions-choose-options.png#lightbox)
7. Select **Next** for **Assignments**.
8. Select **Add assignment**.

    1. Type a name.
    2. Choose users and groups.
    3. Select the Data sources.
    4. Select **Add**.
9. Select **Next** for **Review and finish**.
10. Select **Submit**.

### Summary of roles and permissions for all Defender for IoT features

The following table summarizes the roles and permissions required for each Defender for IoT feature.

| Feature | Write permissions | Read permissions |
| --- | --- | --- |
| Alerts and incidents | **Defender Permissions**: Alerts (manage) **Entra ID roles**: Global Administrator, Security Administrator, Security Operator | Write roles**Defender Permissions**: Security data basics**Entra ID roles**: Global Reader, Security Reader |
| Vulnerabilities | **Defender Permissions**: Response (manage)/ Security operations / Security data **Entra ID roles**: Global Administrator, Security Administrator, Security Operator | Write roles**Defender Permissions**: Vulnerability management (read) **Entra ID roles**: Global Reader, Security Reader |
| Inventory | **Defender Permissions**: Onboard offboard device: Detection tuning (manage)  Manage device tags: Alerts (manage) **Entra ID roles**: Global Administrator, Security Administrator, Security Operator | Write roles **Defender Permissions**: Security data basics/Security operations / Security data **Entra ID roles**: Global Reader, Security Reader |
| Device group | **Defender Permissions**: Authorization (Read and manage) **Entra ID roles**: Global Administrator, Security Administrator | **Defender Permissions**: Authorization (write roles, Read-only) |

To assign roles and permissions for other Microsoft Defender for Endpoint features, such as alerts, incidents and inventory, see [assign roles and permissions for Defender for Endpoint](/en-us/defender-endpoint/prepare-deployment).

For more information, see [map Defender unified RBAC permissions](/en-us/defender-xdr/compare-rbac-roles#microsoft-entra-global-roles-access).