---
layout: Conceptual
title: Assign roles and permissions - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/prepare-deployment
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Configure permissions deploying Microsoft Defender for Endpoint
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- m365solution-endpointprotect
- m365solution-scenario
- highpri
- tier1
ms.topic: install-set-up-deploy
ms.subservice: onboard
ms.date: 2025-01-28T00:00:00.0000000Z
ms.custom: sfi-ga-nochange
locale: en-us
document_id: e2dc5a37-0d93-94ca-57a7-0e718fc838ae
document_version_independent_id: e2dc5a37-0d93-94ca-57a7-0e718fc838ae
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/prepare-deployment.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: prepare-deployment
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/prepare-deployment.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: b55b537e-33fb-5164-c8c0-a5f420a555d7
---

# Assign roles and permissions - Microsoft Defender for Endpoint | Microsoft Learn

The next step when deploying Defender for Endpoint is to assign roles and permissions for the Defender for Endpoint deployment.

Important

Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

## Role-based access control

Microsoft recommends using the concept of least privileges. Defender for Endpoint applies built-in roles within Microsoft Entra ID. [Review the different roles available](/en-us/azure/active-directory/roles/permissions-reference) and choose the right one to solve your needs for each persona for this application. Some roles may need to be applied temporarily and removed after the deployment has been completed.

Microsoft recommends using [Privileged Identity Management](/en-us/azure/active-directory/active-directory-privileged-identity-management-configure) to manage your roles to provide more auditing, control, and access review for users with directory permissions.

Defender for Endpoint supports two ways to manage permissions:

- **Basic permissions management**: Set permissions to either full access or read-only. Users with a role, such as Security Administrator in Microsoft Entra ID have full access. The Security reader role has read-only access and doesn't grant access to view machines/device inventory.
- **Role-based access control (RBAC)**: Set granular permissions by defining roles, assigning Microsoft Entra user groups to the roles, and granting the user groups access to device groups. For more information. see [Manage portal access using role-based access control](rbac).

Microsoft recommends applying RBAC to ensure that only users that have a business justification can access Defender for Endpoint.

You can find details on permission guidelines here: [Create roles and assign the role to a Microsoft Entra group](user-roles#create-roles-and-assign-the-role-to-an-azure-active-directory-group).

Important

Starting February 16, 2025, new Microsoft Defender for Endpoint customers will only have access to the Unified Role-Based Access Control (URBAC). Existing customers keep their current roles and permissions. For more information, see URBAC [Unified Role-Based Access Control (URBAC) for Microsoft Defender for Endpoint](/en-us/defender-xdr/manage-rbac)

The following example table serves to identify the Cyber Defense Operations Center structure in your environment that will help you determine the RBAC structure required for your environment.

| Tier | Description | Permissions required |
| --- | --- | --- |
| Tier 1 | **Local security operations team / IT team** This team usually triages and investigates alerts contained within their geolocation and escalates to Tier 2 in cases where an active remediation is required. | View data |
| Tier 2 | **Regional security operations team** This team can see all the devices for their region and perform remediation actions. | View data  Alerts investigation  Active remediation actions |
| Tier 3 | **Global security operations team** This team consists of security experts and is authorized to see and perform all actions from the portal. | View data  Alerts investigation  Active remediation actions  Manage portal system settings  Manage security settings |